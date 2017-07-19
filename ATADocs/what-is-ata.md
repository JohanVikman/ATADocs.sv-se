---
title: "Vad är Microsoft Advanced Threat Analytics (ATA)? | Microsoft Docs"
description: "Förklarar vad Microsoft Advanced Threat Analytics (ATA) är och vilka typer av misstänkta aktiviteter det kan upptäcka"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c338441b37c41b810023ecf5c5ae348651f5ad64
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# <a name="what-is-advanced-threat-analytics"></a>Vad är Advanced Threat Analytics?
Advanced Threat Analytics (ATA) är en lokal plattform som skyddar ditt företag från flera typer av avancerade riktade cyberattacker och insiderhot.

## <a name="how-ata-works"></a>Så här fungerar ATA

ATA använder en egen nätverksparsningsmotor för att samla in och parsa nätverkstrafiken för flera protokoll (till exempel Kerberos, DNS, RPC, NTLM med flera) för autentisering, auktorisering och insamling av information. Den här informationen samlas in av ATA via:

-   Portspegling från domänkontrollanter och DNS-servrar mot ATA-gatewayen och/eller
-   Distribuera en ATA Lightweight Gateway (LGW) direkt på domänkontrollanter

ATA använder information från flera datakällor, t.ex. loggar och händelser i ditt nätverk, för att lära sig beteendet hos användare och andra entiteter i organisationen och skapar en beteendeprofil om dem.
ATA kan ta emot händelser och loggar från:

-   SIEM-integrering
-   Vidarebefordran av Windows-händelser (WEF)
-   Direkt från Windows Event Collector (för Lightweight Gateway)


Läs mer om ATA-arkitektur under [ATA-arkitektur](ata-architecture.md).

## <a name="what-does-ata-do"></a>Vad gör ATA?

ATA-teknik identifierar flera misstänkta aktiviteter och fokuserar på flera faser av cyberattackkedjan, inklusive:

-   Rekognosering under vilken angripare samlar in information om hur miljön har skapats, vilka olika tillgångarna och enheter som finns och vanligtvis planerar för angreppets nästkommande faser.
-   Lateral rörelsecykel då en angripare investerar tid och möda i spridning av sin angreppsyta i nätverket.
-   Domändominans (persistence) då en angripare samlar information för att kunna återuppta sina kampanjer med olika startpunkter, autentiseringsuppgifter och tekniker. 

Faserna för en cyberattack är liknande och förutsägbara, oavsett vilken typ av företag som är utsatt för en attack eller vilken typ av information som bearbetas.
ATA söker efter tre typer av angrepp: skadliga attacker, onormalt beteende och säkerhetsfrågor och risker.

**Skadliga attacker** upptäcks deterministiskt, genom att söka efter en fullständig lista över kända angreppstyper inklusive:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Förfalskade PAC (MS14-068)
-   Golden ticket
-   Skadliga replikeringarna
-   Rekognosering
-   Brute force
-   Fjärrkörning

En fullständig lista över identifieringar och deras beskrivningar finns i [Vilka misstänkta aktiviteter kan ATA identifiera?](ata-threats.md)
ATA identifierar dessa misstänkta aktiviteter och hämtar information i ATA-konsolen, inklusive en överblick av Vem, Vad, När och Hur. Som ser på den här enkla och användarvänliga instrumentpanelen informeras du om att ATA misstänker att ett Pass-the-Ticket-angrepp gjorts på Client 1- och Client 2-datorer i nätverket.

 ![Exempel på ATA-skärm för pass-the-ticket](media/pass_the_ticket_sa.png)

**Onormalt beteende** identifieras av ATA med beteendeanalyser och utnyttjande av Machine Learning för att visa tveksamma aktiviteter och onormalt beteende hos användare och enheter i nätverket, inklusive:

-   Avvikande inloggningar
-   Okända hot
-   Lösenordsdelning
-   Lateral förflyttning
-   Ändring av känsliga grupper


Du kan se misstänkta aktiviteter av den här typen på ATA-instrumentpanelen. I följande exempel aviserar ATA när en användare ansluter till 4 datorer som normalt inte kan nås av den här användaren, vilken kan vara en anledning till larm.

 ![exempel på ATA-skärm för onormalt beteende](media/abnormal-behavior-sa.png) 

ATA upptäcker också **säkerhetsproblem och risker**, inklusive:

-   Brutet förtroende
-   Svaga protokoll
-   Kända sårbarheter i protokoll

Du kan se misstänkta aktiviteter av den här typen på ATA-instrumentpanelen. I följande exempel låter ATA dig veta att det finns en bruten förtroenderelation mellan en dator i nätverket och domänen.

  ![exempel på ATA-skärm för bruten förtroende](media/broken-trust-sa.png)


## <a name="known-issues"></a>Kända problem

- Om du uppdaterar till ATA 1.7 och sedan omedelbart till ATA 1.8 utan att först uppdatera ATA-gatewayerna, kan du inte migrera till ATA 1.8. Du måste uppdatera alla gatewayer till version 1.7.1 eller 1.7.2 innan du uppdaterar ATA Center till version 1.8.

- Om du väljer att utföra en fullständig migrering kan det ta lång tid, beroende på databasens storlek. När du väljer migreringsalternativ visas den beräknade tiden – notera tiden innan du bestämmer vilket alternativ du ska välja. 


## <a name="whats-next"></a>Vad händer nu?

-   Mer information om hur ATA passar in i nätverket: [ATA-arkitektur](ata-architecture.md)

-   Komma igång med att distribuera ATA: [Installera ATA](install-ata-step1.md)

## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
