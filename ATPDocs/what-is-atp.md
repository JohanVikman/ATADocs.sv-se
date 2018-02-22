---
title: "Vad är Azure Advanced Threat Protection (ATP)? | Microsoft Docs"
description: "Beskriver vad Azure Advanced Threat Protection (ATP) är och vilka typer av misstänkta aktiviteter kan identifiera"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="what-is-azure-advanced-threat-protection"></a>Vad är Azure Advanced Threat Protection?
Azure avancerade Threat Protection (ATP) är en molnbaserad tjänst som hjälper dig att skydda din enterprise hybridmiljöer från flera typer av cyber för avancerade riktade attacker och insiderhot.

## <a name="how-azure-atp-works"></a>Hur fungerar Azure ATP

Azure ATP utnyttjar ett eget nätverk parsning av motorn för att samla in och analysera nätverkstrafik för flera protokoll (till exempel Kerberos, DNS, RPC, NTLM och andra) för autentisering, auktorisering och insamling av information. Den här informationen samlas in av Azure ATP via antingen:

-   Distribuera Azure ATP sensorer direkt på domänkontrollanterna
-   Portspegling från domänkontrollanter och DNS-servrar till Azure ATP fristående sensor

Azure ATP tar information från flera-datakällor, till exempel loggar och händelser i nätverket, att lära sig hur användare och andra enheter i organisationen och skapa en profil för beteendebaserade om dem.
Azure ATP kan ta emot händelser och loggar från:

-   SIEM-integrering
-   Vidarebefordran av Windows-händelser (WEF)
-   Direkt från Windows Event Collector (för sensor)
-   RADIUS-redovisning från VPN-anslutningar


Läs mer på Azure ATP arkitektur [Azure ATP arkitektur](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Vad är Azure ATP?

Azure ATP teknik identifierar flera misstänkta aktiviteter som fokuserar på flera faser cyber attack kill kedjan inklusive:

-   Rekognosering, då angripare samla in information om hur miljön skapas, vilka de olika tillgångarna är och vilka entiteter finns. De bygger vanligtvis deras plan för nästa faser för angrepp.
-   Lateral rörelsecykel då en angripare investerar tid och möda i spridning av sin angreppsyta i nätverket.
-   Domändominans (beständiga) under vilka en angripare fångar information så att de kan återuppta sina kampanj med olika uppsättningar med startpunkter, autentiseringsuppgifter och tekniker. 

Faserna för en cyberattack är liknande och förutsägbara, oavsett vilken typ av företag som är utsatt för en attack eller vilken typ av information som bearbetas.
Azure ATP söker efter tre typer av attacker: skadliga attacker, onormalt beteende och säkerhetsproblem och risker.

**Skadliga attacker** identifieras deterministiskt samt via analyser onormalt beteende. En fullständig lista över kända attacker typer innehåller:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Förfalskade PAC (MS14-068)
-   Golden ticket
-   Skadliga replikering
-   Directory Service uppräkning
-   SMB-sessionsuppräkning
-   DNS-spaning
-   Vågrät Brute Force 
-   Lodrät Brute Force
-   Dyrk
-   Unusual Protocol
-   Nedgradering av kryptering
-   Fjärrkörning
-   Skapa en skadlig tjänst


Azure ATP identifierar dessa misstänkta aktiviteter och hämtar information i Azure ATP arbetsytan portal inklusive överblick av vem, vad, när och hur. Som du kan se genom att övervaka den här instrumentpanelen för enkelt och användarvänligt meddelas du att Azure ATP misstänker att en attack med Pass-the-Ticket utfördes på klienten 1 och 2 för klient datorer i nätverket.

 ![exemplet Azure ATP skärmen pass-the-ticket](media/pass-the-ticket-sa.png)


Dessutom upptäcks Azure ATP **säkerhetsproblem och risker**, inklusive:

-   Svaga protokoll
-   Kända sårbarheter i protokoll
-   [Lateral förflyttning sökvägen till känsliga konton](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Vilka hot Azure ATP leta efter

Azure ATP ger identifiering för följande olika faser i en avancerad attack: rekognosering, avslöjade autentiseringsuppgifter, lateral förflyttning, eskalering av privilegier, domändominans och andra. Dessa identifieringar är avsedda att identifiera avancerade attacker och insiderhot innan de skadar organisationen.

Identifieringen av varje fas ger flera misstänkta aktiviteter som är relevanta för fasen i fråga, där varje misstänkt aktivitet motsvarar olika varianter av möjliga attacker.
Faserna i kill-kedjan där Azure ATP innehåller identifieringar som för närvarande är markerade i följande bild:

![Azure ATP fokus på lateral aktivitet i attack kill kedja](media/attack-kill-chain-small.jpg)


Mer information finns i [arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md) och [Azure ATP misstänkt aktivitet guiden](suspicious-activity-guide.md).

## <a name="whats-next"></a>Vad händer nu?

-   Mer information om hur Azure ATP passar in i nätverket: [Azure ATP-arkitektur](atp-architecture.md)

-   Börja distribuera ATP: [installera ATP](install-atp-step1.md)


## <a name="see-also"></a>Se även
- [Vanliga och frågor svar om Azure ATP](atp-technical-faq.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)