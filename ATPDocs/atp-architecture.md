---
title: Azure Advanced Threat Protection-arkitektur | Microsoft Docs
description: Här beskrivs arkitekturen för Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb9e99d43a800f6b7bc080fa3fe0bc2453f3d754
ms.sourcegitcommit: 8e80f59409c65e7d8d60ec7de8b96b621795699a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/25/2018
ms.locfileid: "47168577"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-architecture"></a>Azure ATP-arkitektur

Azure ATP övervakar dina domänkontrollanter genom att samla in och parsa nätverkstrafik och att använda Windows-händelser (direkt från domänkontrollanterna eller från en SIEM-server) och analyserar data beträffande attacker och hot. Använda profilering deterministisk identifiering, machine learning- och beteendealgoritmer Azure ATP lär sig om nätverket, aktiverar identifiering av avvikelser och varnar dig för misstänkta aktiviteter.

Azure Advanced Threat Protection-arkitektur:

![Topologidiagram för Azure ATP-arkitektur](media/atp-architecture-topology.png)

Det här avsnittet beskrivs hur flödet av Azure ATP nätverk och händelseinsamling fungerar och beskriver funktionerna för huvudkomponenterna: Azure ATP-portalen, Azure ATP-sensorn och Azure ATP-molntjänst. 

Installerad direkt på domänkontrollanterna, Azure ATP-sensorn har åtkomst till nödvändiga händelseloggarna direkt från domänkontrollanten. När loggarna och nätverkstrafik parsas av sensorn, skickar Azure ATP endast parsade information till Molntjänsten Azure ATP (endast en del av loggarna skickas). 

## <a name="azure-atp-components"></a>Azure ATP-komponenter
Azure ATP består av följande komponenter:

-   **Azure ATP-portal** <br>
Azure ATP-portalen kan du skapa din Azure ATP-instans, visar de data som mottagits från Azure ATP-sensorer och gör att du kan övervaka, hantera och undersöka hot i din nätverksmiljö.  

-   **Azure ATP-sensorn**<br>
Azure ATP-sensorer installeras direkt på domänkontrollanterna. Sensorn övervakar direkt domain controller trafik, utan att behöva en dedikerad server eller konfiguration av portspegling.

-   **Azure ATP-molntjänst**<br>
Azure ATP-molntjänst som körs på Azure-infrastrukturen och för närvarande har distribuerats i USA, Europa och Asien. Azure ATP-molntjänst är ansluten till Microsofts intelligent security graph. 

## <a name="azure-atp-portal"></a>Azure ATP-portal 
Använd Azure ATP-portalen för att:
- Skapa din Azure ATP-instans
- Integrera med andra Microsoft-säkerhetstjänster 
- Hantera konfigurationsinställningar för Azure ATP-sensorn 
- Visa data som mottagits från sensorer Azure ATP
- Övervaka identifierade misstänkta aktiviteter och misstänkta attacker baserat på modellen attack kill kedja
- **Valfritt**: portalen kan också konfigureras för att skicka e-post och händelser när säkerhetsaviseringar eller hälsoproblem har identifierats

> [!NOTE]
> - Om inga sensorn installeras på din arbetsyta inom 60 dagar, arbetsytan kan tas bort och du kommer måste återskapa den.

## <a name="azure-atp-sensor"></a>Azure ATP-sensorn
Azure ATP-sensorn har följande grundläggande funktioner:
- Samla in och inspektera domänkontrollantens nätverkstrafik (lokal trafik på domänkontrollanten)
- Ta emot Windows-händelser direkt från domänkontrollanterna 
- Ta emot RADIUS-redovisningsinformation från VPN-leverantören
- Hämta information om användare och datorer från Active Directory-domänen
- Matcha nätverksentiteter (användare, grupper och datorer)
- Överföra relevanta data till Molntjänsten Azure ATP
> [!NOTE]
> - Som standard stöder Azure ATP upp till 100 sensorer. Kontakta Azure ATP-supporten om du vill installera fler.
 
## <a name="azure-atp-sensor-features"></a>Funktioner i Azure ATP-sensorn
Azure ATP-sensorn läser händelser lokalt, utan att behöva köpa och underhålla ytterligare maskinvara eller konfigurationer. Azure ATP-sensorn har även stöd för tråd för Windows ETW (Event) som tillhandahåller logginformation för flera identifieringar. ETW baserat identifieringar omfattar både misstänkt replikering begära och misstänkta befordran av domänkontrollant, båda är eventuella DC Shadow attacker.
- Kandidat för domänsynkronisering

    Kandidat för domänsynkronisering ansvarar för att proaktivt synkronisera alla entiteter från en specifik Active Directory-domän (liknar mekanismen som används av själva domänkontrollanterna för replikering). En sensor väljs slumpmässigt från listan över kandidater för att fungera som domänsynkroniserare. 

    Om synkroniseraren är offline i mer än 30 minuter väljs en annan kandidat i stället. Om det finns någon domänsynkroniserare tillgänglig för en specifik domän, synkroniserar entiteter och deras ändringar proaktivt i Azure ATP men Azure ATP hämtar nya entiteter när de hittas i övervakad trafik. 
    
    Om det finns någon domänsynkroniserare tillgänglig och du söker efter en entitet som inte har någon trafik relaterad till den, visas inga sökresultat.

    Som standard är inte Azure ATP-sensorer som kandidater för domänsynkronisering. För att manuellt ange Azure ATP-sensorn som kandidat för domänsynkronisering, följer du stegen i den [Azure ATP-installation arbetsflöde](install-atp-step5.md#step-5-configure-the-azure-atp-sensor-settings).
- Resursbegränsningar

    Azure ATP-sensorn innehåller en övervakningskomponent som utvärderar den tillgängliga beräknings- och minneskapaciteten på den domänkontrollant där den körs. Övervakningsprocessen körs var tionde sekund och uppdaterar dynamiskt processor- och minnesanvändningskvoten på processen för Azure ATP-sensorn. Övervakningsprocessen ser till att domänkontrollanten har alltid minst 15% lediga beräknings- och minnesresurser resurser som är tillgängliga.

    Oavsett vad som händer på domänkontrollanten, frigör övervakningsprocessen kontinuerligt resurser för att se till att domänkontrollantens grundläggande funktioner påverkas aldrig.

    Om övervakningsprocessen gör Azure ATP-sensorn till slut på resurser, endast delvis trafik övervakas och övervakning varning ”förlorad portspeglad nätverkstrafik” visas på hälsosidan för Azure ATP-portalen.

-  Windows-händelser

    Att förbättra Azure ATP-identifieringsomfattningen av Pass-the-Hash, misstänkta autentiseringsfel, ändring av känsliga grupper, skapa misstänkta tjänster och Honeytoken-aktivitetstyper av angrepp, Azure ATP-behov att analysera loggarna för följande Windows-händelser: 4776,4732,4733,4728,4729,4756,4757 och 7045. Dessa händelser läses automatiskt av Azure ATP-sensorer med rätt [avancerade inställningar för granskningsprinciper](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-storleksverktyget](http://aka.ms/trisizingtool)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
