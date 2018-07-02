---
title: Azure Advanced Threat Protection-integrering med Windows Defender ATP | Microsoft Docs
description: Hur du integrerar Azure Avancerat skydd med Windows Defender ATP för fullständig threat identifieringsomfattningen
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/5/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d6c2cdb157d4e3f75794c8c40abfc7556e314d5
ms.sourcegitcommit: b218f60b42a25fe486d774d97719590e6fa74e10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34760081"
---
*Gäller för: Azure Avancerat skydd*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrera Azure ATP med Windows Defender ATP

Azure Advanced Threat Protection kan du integrera Azure ATP med Windows Defender ATP för en ännu mer komplett lösning för enhetsskydd. Medan Azure ATP övervakar trafiken på domänkontrollanterna, övervakar Windows Defender ATP dina slutpunkter tillsammans att tillhandahålla ett enda gränssnitt som du kan använda för att skydda din miljö.

Genom att integrera Windows Defender ATP i Azure ATP, du kan dra full nytta av båda tjänsterna och skydda din miljö, inklusive:

- Azure ATP-sensorer och fristående sensorer: kan vara direkt på dina domänkontrollanter eller port spegling från domänkontrollanterna till ATP att samla in och tolka nätverkstrafiken hos flera protokoll (till exempel Kerberos, DNS, RPC, NTLM och andra) för autentisering auktorisering och insamling av information. 

-   Slutpunkt-beteendesensorer: inbäddad i Windows 10, dessa sensorer som samlar in och bearbeta beteendeanalys signaler från operativsystemet (till exempel processen, registret, fil och nätverkskommunikation) och skickar den här sensordata till molnet privat, isolerad, instans av Windows Defender ATP.

- Molnet säkerhetsanalyser: utnyttjar stordata, maskininlärning och unika Microsoft-vyn i Windows-ekosystemet (till exempel den [Microsoft verktyget](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), enterprise molnprodukter (till exempel Office 365), och online tillgångar (t.ex Bing och SmartScreen-URL: en rykte), beteendeanalys signaler översättas till insikter, identifieringar, och rekommenderas svar på avancerade hot.

- Hotinformation: genereras av Microsoft intensiva kampanjperioder security team, och förstärkas med hotinformation som tillhandahålls av partner threat intelligence gör det möjligt för Windows Defender ATP att identifiera angripare verktyg, tekniker och procedurer och generera aviseringar när Dessa observeras i insamlade sensordata.

Azure ATP-teknik identifierar flera misstänkta aktiviteter och fokuserar på flera faser av cyberattackkedjan kill chain, inklusive:

- Rekognosering, under vilken angripare samla in information om hur miljön har skapats, vilka olika tillgångarna är och vilka entiteter finns. De skapar vanligtvis planerar för nästkommande faser av angrepp.

- Lateral rörelsecykel då en angripare investerar tid och möda i spridning av sin angreppsyta i nätverket.

- Domändominans (persistence) då en angripare samlar information för att kunna återuppta sina kampanjer med olika uppsättningar av startpunkter, autentiseringsuppgifter och tekniker.

På samma gång utnyttjar Windows Defender ATP Microsoft-teknik och kunskaper för att identifiera avancerade cyberattacker att tillhandahålla:

- Identifiering av beteendebaserad, molndrivna, avancerad attack<br></br>Söker efter de attacker som gjorts tidigare andra försvar (skicka intrång identifiering), ger användbara, korrelerade aviseringar för kända och okända angripare som försöker att dölja sitt arbete på slutpunkter.

- Omfattande tidslinje för kriminaltekniska undersökningar och minskning<br></br>Enkelt undersöka omfånget för brott eller misstänkta beteenden på en dator via en omfattande datorn tidslinje. Filen, URL: er och nätverket anslutningen inventering över nätverket. Få ytterligare insikter med djupgående insamling och analys (”detonation”) för en fil eller URL: er.

- Inbyggda unika threat kunskapsbas för tillgångsinformation<br></br>Oöverträffad threat optik innehåller aktören information och avsikt kontexten för varje intel-baserad identifiering av hot – kombinera första och tredje parts intelligenskällor.

## <a name="prerequisites"></a>Krav

Om du vill aktivera den här funktionen behöver en licens för både Azure ATP- och Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Hur du integrerar Azure ATP med Windows Defender ATP

1. Ange den arbetsyta du vill integrera som **primära**. Endast en arbetsyta kan vara den primära arbetsytan och endast en primär arbetsyta kan integrera med andra tjänster. Om du någon gång i framtiden, bör du se den här arbetsytan inte längre den primära arbetsytan, måste du först ta bort integrationen innan du kan ställa in det som icke-primär.

 ![primära arbetsytan](./media/primary-workspace.png)

2. Klicka på **Configuration**, och under **datakällor** Välj **Windows Defender ATP**. Klicka på länken till **arbetsytehantering**. Detta är bara tillgängligt om du har en licens för Windows Defender ATP och du redan har utfört registreringen av processen för Windows Defender ATP. 

3. I den primära arbetsytan klickar du på kugghjulet för inställningar.

 ![integrering av arbetsyta](./media/edit-workspace.png)
 
3. Inställd integrationen **på**. 

 ![aktivera integrering](./media/enable-integration.png)

4. I den [Windows Defender ATP-portalen](https://beta.securitycenter.windows.com/preferences/advanced)går du till **inställningar**, **avancerade funktioner** och ange **Azure ATP-integrering** till  **Vidare**. 

 ![Windows Defender ATP aktivera integrering](./media/wd-atp-enable.png)

5. Du kan kontrollera status för integrationen i Azure ATP-arbetsyteportalen, välja **inställningar** och sedan **Windows Defender ATP-integrering**. Du kan se status för integration. Om något är fel du ser ett fel. Du kan också se vilken arbetsyta som är integrerad med Windows Defender ATP.

## <a name="how-it-works"></a>Så här fungerar det

När Azure ATP- och Windows Defender ATP är fullständigt integrerade i Azure ATP-arbetsyteportalen, Mini profil popup-fönstret och profilsida entitet innehåller varje entitet som finns i Windows Defender ATP en symbol för att visa att den är integrerad med Windows Defender ATP. 

 ![Windows Defender ATP-aviseringar](./media/profile-alerts-wd.png)

Om entiteten innehåller aviseringar i Windows Defender ATP, är det ett tal bredvid märket så att du vet hur många aviseringar har aktiverats.

 ![Azure ATP-aviseringar](./media/atp-integrated-wd-icon-alerts.png)

Om du klickar på aktivitetsikonen, kommer du till Windows Defender ATP-portal där du kan visa och minimera aviseringarna. Om enheten inte kan identifieras av Windows Defender ATP, nedtonad märket. 

 ![Windows Defender ATP grå](./media/wd-grey.png)

När du klickar på en slutpunkt i Windows Defender ATP-portalen kan du visa Azure ATP-aviseringar. Om du klickar på aviseringar för den här entiteten i Windows Defender ATP öppnas entitetens profilsida i Azure ATP. 
 
 > ! [OBS] Azure ATP-integrering med Windows Defender ATP stöder för närvarande endast användare och datorer från lokalt AD. Användare från Azure AD och virtuella datorer som hanteras i Azure visas inte som en del av integreringen 

![Windows Defender ATP-aviseringar](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Se även

- [Undersöka laterala förflyttningssökvägar med Azure ATP](use-case-lateral-movement-path.md)
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Azure ATP-arkitektur](atp-architecture.md)
- [Installera ATP](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)

