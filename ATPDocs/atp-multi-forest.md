---
title: Support för Azure Advanced Threat Protection använda skogar | Microsoft Docs
description: Hur du konfigurerar stöd för flera Active Directory-skogar i Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a3460c39d6428831cc34231321fff745dbe0701
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734819"
---
*Gäller för: Azure Avancerat skydd*

# <a name="install-azure-atp---step-9"></a>Installera Azure ATP - steg 9

>[!div class="step-by-step"]
[«Steg 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Steg 9.  Installera Azure Advanced Threat Protection stöd för flera skogar

Azure ATP stöder organisationer med flera skogar, vilket ger dig möjlighet att enkelt övervaka aktivitet och profilanvändare över flera skogar från en enda glasruta. 

Företag har vanligtvis flera Active Directory-skogar - används ofta för olika syften, inklusive äldre infrastruktur från företagets fusioner och förvärv, geografisk fördelning och säkerhetsgränser (red-skog). Du kan skydda flera skogar med hjälp av Azure ATP, vilket ger dig möjlighet att övervaka och undersöka via en enda glasruta.

Möjlighet att hantera flera Active Directory-skogar gör följande:
-   Visa och undersöka aktiviteter som utförs av användare i flera skogar från en enda glasruta. 
-   Förbättrad identifiering och minskade falska positiva identifieringar genom att tillhandahålla avancerade Active Directory-integrering och konto lösning. 
-   Bättre kontroll och underlättar distributionen. Förbättrad övervakning av aviseringar och rapportering för cross-org täckning när domänkontrollanter övervakas från en enda Azure ATP-konsol.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Hur Azure ATP identifierar aktiviteter i flera skogar 

Azure ATP-sensorer fråga för att identifiera aktiviteter mellan skogar, domänkontrollanter i fjärranslutna skogar för att skapa profiler för alla entiteter som berörs, inklusive användare och datorer från fjärranslutna skogar. 

> [!NOTE]
> - Azure ATP-sensorer kan installeras på alla skogar (om det finns ett minsta enkelriktat förtroende).
> - Användaren som du konfigurerar i Azure ATP-konsolen under **katalogtjänster** måste vara betrott i de andra skogarna.


Om du har skogar på vilka inga Azure ATP sensorer installeras, kan Azure ATP fortfarande visa och övervaka aktiviteter från dessa skogar. ATP-sensorer installerad kan fråga efter alla anslutna fjärrskog domänkontrollanter för att lösa användare, datorer och skapa profiler för var och en av dem. 

## <a name="installation-requirements"></a>Installationskrav 

-   Om Azure ATP fristående sensorer är installerade på fristående datorer istället för direkt på domänkontrollanterna, kontrollera att datorerna ska kunna kommunicera med alla fjärrskog domänkontrollanter med hjälp av LDAP. 
- Användaren som du konfigurerar i Azure ATP-konsolen under **katalogtjänster** måste vara betrott i de andra skogarna och måste ha minst läsbehörighet endast att köra LDAP-frågor för domänkontrollanterna.

- Öppna följande portar på varje demonstrationen på vilken ATP-sensorn installeras för Azure ATP-källan med ATP sensorer och ATP fristående sensorer:

 
  |Protokoll|Transport|Port|Till/från|Riktning|
  |----|----|----|----|----|
  |**Internet-portar**||||
  |SSL (*.atp.azure.com)|TCP|443|Azure ATP-molntjänst|Utgående|
  |**Interna portar**||||           
  |LDAP|TCP och UDP|389|Domänkontrollanter|Utgående|
  |Säkert LDAP (LDAPS)|TCP|636|Domänkontrollanter|Utgående|
  |LDAP till global katalog|TCP|3268|Domänkontrollanter|Utgående|
  |LDAPS till global katalog|TCP|3269|Domänkontrollanter|Utgående|


## <a name="multi-forest-support-network-traffic-impact"></a>Med flera skogar support nätverk trafik påverkan 

När Azure ATP mappar dina skogar, används en process som påverkar följande:

-   När Azure ATP-sensorn körs, frågar de fjärranslutna Active Directory-skogarna och hämtar en lista över användare och Maskindata för att skapa en profil.
-   Var femte minut, frågar varje Azure ATP-sensorn en domänkontrollant från en domän från varje skog att mappa alla skogar i nätverket.
-   Varje Azure ATP-sensorn mappar skogarna med det ”trustedDomain”-objektet i Active Directory genom att logga in och kontrollera vilken förtroende.
-   Du kan också se ad hoc-trafik när ATP-sensorn identifierar mellan skogar aktivitet. När detta inträffar kan skicka en LDAP-fråga till relevanta domänkontrollanter för att hämta entitetsinformation med ATP-sensorer. 

## <a name="known-limitations"></a>Kända begränsningar
-   Interaktiva inloggningar som genomförs av användare i en skog komma åt resurser i en annan skog visas inte i Azure ATP-instrumentpanelen.


>[!div class="step-by-step"]
[«Steg 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Se även
- [ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [ATP-arkitektur](atp-architecture.md)
- [Installera ATP](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)

