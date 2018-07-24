---
title: Support för Azure Advanced Threat Protection använda skogar | Microsoft Docs
description: Hur du konfigurerar stöd för flera Active Directory-skogar i Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/20/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a48bf96bd6a71282455d932a35aac23ba4c8193a
ms.sourcegitcommit: 7909deafdd9323f074d0ff2f590e307bcfaaabad
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/23/2018
ms.locfileid: "39202140"
---
*Gäller för: Azure Avancerat skydd*

# <a name="install-azure-atp---step-9"></a>Installera Azure ATP - steg 9

>[!div class="step-by-step"]
[«Steg 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Steg 9.  Installera Azure Advanced Threat Protection stöd för flera skogar

Azure ATP stöder organisationer med flera skogar där du kan övervakaraktivitet och profilanvändare i skogar. 

En enterprise-organisation kan ha flera Active Directory-skogar - används ofta för olika syften, inklusive äldre infrastruktur från företagets fusioner och förvärv, geografisk fördelning och säkerhetsgränser (red-skog). Du kan skydda flera skogar med hjälp av Azure ATP, rapporterar alla data till en enda, primär arbetsyta, vilket ger dig möjlighet att övervaka och undersöka via en enda glasruta.

Möjlighet att hantera flera Active Directory-skogar gör följande:
-   Du kan visa och undersöka aktiviteter som utförs av användare i flera skogar från en enda glasruta. 
-   Stöd för flera skogar förbättrar identifiering och minskar antalet falska positiva identifieringar genom att tillhandahålla avancerade Active Directory-integrering och konto-lösning. 
-   Eftersom flera foresst support eliminerar behovet av flera arbetsytor, har du större kontroll och underlättar distributionen, även om domänkontrollanterna är alla övervakade centralt från en enda Azure ATP konsolen som ger bättre övervakningsaviseringar och rapportering för cross-org täckning.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Hur Azure ATP identifierar aktiviteter i flera skogar 

Azure ATP-sensorer fråga för att identifiera aktiviteter mellan skogar, domänkontrollanter i fjärranslutna skogar för att skapa profiler för alla entiteter som berörs, inklusive användare och datorer från fjärranslutna skogar. 

> [!NOTE]
> - Azure ATP-sensorer kan installeras på alla skogar (om det finns ett minsta enkelriktat förtroende).
> - Användaren som du konfigurerar i Azure ATP-konsolen under **katalogtjänster** måste vara betrott i de andra skogarna.


Om du har skogar på vilka inga Azure ATP sensorer installeras, kan Azure ATP fortfarande visa och övervaka aktiviteter från dessa skogar. ATP-sensorer installerad kan fråga efter alla anslutna fjärrskog domänkontrollanter för att lösa användare och datorer och skapa profiler för var och en av dem. 

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
-   Du kan också se ad hoc-trafik när ATP-sensorn identifierar mellan skogar aktivitet. När detta inträffar skickar ATP-sensorer en LDAP-fråga till relevanta domänkontrollanter i ordning hämta entitetsinformation. 

## <a name="known-limitations"></a>Kända begränsningar
-   Interaktiva inloggningar som genomförs av användare i en skog komma åt resurser i en annan skog visas inte i Azure ATP-instrumentpanelen.


>[!div class="step-by-step"]
[«Steg 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Se även
- [ATA-storleksverktyget](http://aka.ms/aatpsizingtool)
- [ATA-arkitektur](atp-architecture.md)
- [Installera ATA](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)

