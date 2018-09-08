---
title: Vad är Azure Advanced Threat Protection (ATP)? | Microsoft Docs
description: Förklarar vad Azure Advanced Threat Protection (ATP) är och vilka typer av misstänkta aktiviteter kan identifiera
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7e78d5db2babc682de8eae50091193e1ccee8433
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166149"
---
*Gäller för: Azure Avancerat skydd*


# <a name="what-is-azure-advanced-threat-protection"></a>Vad är Azure Advanced Threat Protection?
Azure Advanced Threat Protection (ATP) är en molntjänst som hjälper dig att skydda dina företagshybridmiljöer från flera typer av avancerade riktade cyberattacker och insiderhot.

## <a name="how-azure-atp-works"></a>Hur fungerar Azure ATP

Azure ATP utnyttjar en nätverkstolkningsmotor för att samla in och tolka nätverkstrafiken hos flera protokoll (till exempel Kerberos, DNS, RPC, NTLM och andra) för autentisering, auktorisering och insamling av information. Den här informationen samlas in av Azure ATP via antingen:

-   Distribuera Azure ATP-sensorer direkt på domänkontrollanterna
-   Portspegling från domänkontrollanter och DNS-servrar till fristående Azure ATP-sensorn

Azure ATP tar information från flera datakällor, till exempel loggar och händelser i nätverket, att lära sig beteendet hos användare och andra entiteter i organisationen och skapar en beteendeprofil om dem.
Azure ATP kan ta emot händelser och loggar från:

-   SIEM-integrering
-   Vidarebefordran av Windows-händelser (WEF)
-   Direkt från Windows Event Collector (för sensorn)
-   RADIUS-redovisning från virtuella privata nätverk


Mer information om Azure ATP-arkitekturen finns i [Azure ATP-arkitektur](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Vad är Azure ATP?

Azure ATP-teknik identifierar flera misstänkta aktiviteter och fokuserar på flera faser av cyberattackkedjan kill chain, inklusive:

-   Rekognosering, under vilken angripare samla in information om hur miljön har skapats, vilka olika tillgångarna är och vilka entiteter finns. De skapar vanligtvis planerar för nästkommande faser av angrepp.
-   Lateral rörelsecykel då en angripare investerar tid och möda i spridning av sin angreppsyta i nätverket.
-   Domändominans (persistence) då en angripare samlar information för att kunna återuppta sina kampanjer med olika uppsättningar av startpunkter, autentiseringsuppgifter och tekniker. 

Faserna för en cyberattack är liknande och förutsägbara, oavsett vilken typ av företag som är utsatt för en attack eller vilken typ av information som bearbetas.
Azure ATP söker efter tre typer av angrepp: skadliga attacker, onormalt beteende och säkerhetsproblem och risker.

**Skadliga attacker** upptäcks deterministiskt, samt via onormalt beteende analytics. En fullständig lista över kända angreppstyper innehåller:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Förfalskade PAC (MS14-068)
-   Golden ticket
    -   tid anomoly
    -   icke befintligt konto – ny
-   Skadlig replikering
-   Directory Service-uppräkning
-   SMB-sessionsuppräkning
-   DNS-spaning
-   Vågrät Brute Force 
-   Lodrät Brute Force
-   Dyrk
-   Ovanligt protokoll
-   Nedgradering av kryptering
-   Fjärrkörning
-   Skapa skadliga tjänster
-   Misstänkt befordran av domänkontrollant (möjlig DCShadow-attack) – ny
-   Misstänkt replikeringsbegäran (möjlig DCShadow-attack) – ny
-   VPN 


Azure ATP identifierar dessa misstänkta aktiviteter och hämtar information i Azure ATP-arbetsyteportalen, inklusive en överblick av vem, vad, när och hur. Som du kan se den här enkla och användarvänliga instrumentpanelen informeras du att Azure ATP misstänker att ett Pass-the-Ticket-angrepp gjorts på Client 1 och 2-datorer i nätverket.

 ![exemplet Azure ATP skärm för pass-the-ticket](media/pass-the-ticket-sa.png)


Azure ATP identifierar också **säkerhetsproblem och risker**, inklusive:

-   Svaga protokoll
-   Kända sårbarheter i protokoll
-   [Lateral förflyttning sökvägen till känsliga konton](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Vilka hot Azure ATP leta efter

Azure ATP ger identifiering för följande olika faser i en avancerad attack: rekognosering, avslöjade autentiseringsuppgifter, lateral förflyttning, eskalering av privilegier, domändominans och andra. Dessa identifieringar är avsedda att identifiera avancerade attacker och insiderhot innan de skadar organisationen.

Identifieringen av varje fas ger flera misstänkta aktiviteter som är relevanta för fasen i fråga, där varje misstänkt aktivitet motsvarar olika varianter av möjliga attacker.
Faserna i attackkedjan där Azure ATP för närvarande kan identifiera hot är markerade på följande bild:

![Azure ATP-fokuserar på lateral aktivitet i attackkedjan](media/attack-kill-chain-small.jpg)


Mer information finns i [arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md) och [Azure ATP-guide för misstänkt aktivitet](suspicious-activity-guide.md).

## <a name="whats-next"></a>Vad händer nu?

-   Mer information om hur Azure ATP passar in i ditt nätverk: [Azure ATP-arkitektur](atp-architecture.md)

-   Du kommer igång med att distribuera ATP: [installera ATP](install-atp-step1.md)


## <a name="see-also"></a>Se även
- [Vanliga och frågor svar om Azure ATP](atp-technical-faq.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)