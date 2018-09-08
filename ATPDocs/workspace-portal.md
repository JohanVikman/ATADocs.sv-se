---
title: Förstå Azure Advanced Threat Protection-arbetsyteportalen | Microsoft Docs
description: Beskriver hur du loggar in på Azure ATP-arbetsyteportalen och komponenterna i arbetsytans portal
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fa8c1e19fde1ec779699b3a2c5411dea0908451
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166337"
---
*Gäller för: Azure Avancerat skydd*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Arbeta med Azure ATP-arbetsyteportalen

Använda Azure ATP-arbetsyteportalen för att övervaka och svara på misstänkt aktivitet har identifierats av ATP.

Att skriva den `?` nyckeln innehåller kortkommandon för Azure ATP arbetsytans portal tillgänglighet. 

Azure ATP-arbetsyteportalen ger dig en snabb överblick över alla misstänkta aktiviteter i kronologisk ordning. Den gör det möjligt att visa detaljer om alla aktiviteter och utföra åtgärder baserat på dessa aktiviteter. Arbetsytans portal visar även meddelanden och aviseringar som belyser problem som kan uppstå genom Azure ATP eller nya aktiviteter som bedöms som misstänkta.

Den här artikeln beskriver hur du arbetar med de viktigaste elementen i Azure ATP-arbetsyteportalen.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Aktivera åtkomst till Azure ATP-arbetsyteportalen
Du måste logga in med en användare som har tilldelats rätt Azure Active Directory-säkerhetsgrupp för åtkomst till arbetsytan Azure ATP-portalen för att du har loggat in till Azure ATP-arbetsyteportalen. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP-rollgrupper](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Logga in på Azure ATP-arbetsyteportalen

1. Du kan ange arbetsytans portal genom att logga in arbetsytehanteringsportalen [ https://portal.atp.azure.com ](https://portal.atp.azure.com) och sedan väljer du relevant arbetsyta, eller bläddra till URL: en arbetsyta: [https:// *workspacename*. atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP stöder enkel inloggning integrerat med Windows-autentisering – om du redan har loggat in på datorn, Azure ATP använder du den token för att logga in i Azure ATP-arbetsyteportalen. Du kan också logga in med ett smartkort. Dina behörigheter i Azure ATP som motsvarar din [administratörsroll](atp-role-groups.md).

 > [!NOTE]
 > Se till att logga in på den dator som du vill komma åt Azure ATP-arbetsyteportalen med din Azure ATP-administratörsanvändarnamn och lösenord. Du kan också köra webbläsaren som en annan användare eller logga ut från Windows och logga med din Azure ATP-administratörsanvändare. 


### <a name="attack-time-line"></a>Tidslinje för attacker

Det här är den standardsida du kommer till när du loggar in på Azure ATP-arbetsyteportalen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan filtrera tidslinjen för att visa alla, öppna, avvisade eller ignorerad misstänkta aktiviteter. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet.

![Bild för tidslinje Azure ATP-attack](media/atp-sa-timeline.png)

Mer information finns i [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Nyheter

När en ny version av Azure ATP släpps den **nyheter** visas uppe till höger så att du vet vad har lagts till i den senaste versionen. Det ger dig också med en länk för nedladdning av version.

### <a name="filtering-panel"></a>Filtreringspanel

Du kan filtrera vilka misstänkta aktiviteter som visas i tidslinjen för attacker eller som visas på entitetsprofilens flik för misstänkta aktiviteter baserat på status och allvarlighetsgrad.

### Sökfältet <a name="search-bar"></a>

Du kan hitta ett sökfält i den översta menyn. Du kan söka efter en viss användare, dator eller grupper i Azure ATP. Om du vill prova är det bara att börja skriva. Längst ned i sökfältet anges antalet sökresultat har hittats. 

![Bild för portalen sökning Azure ATP-arbetsyta](media/atp-workspace-portal-search.png)

Om du klickar på siffran som du kan komma åt sidan med sökresultat som du kan filtrera resultaten efter entitetstypen för vidare studier.

![Sökresultat](media/search-results.png)

### <a name="health-center"></a>Hälsocenter

Health center visar aviseringar om något inte fungerar korrekt på din Azure ATP-arbetsyta.

![Azure ATP health center-avbildning](media/atp-health-issue.png)

När som helst om systemet upptäcker ett problem, till exempel ett anslutningsfel eller en frånkopplad Azure ATP fristående sensorn med hjälp av ikonen för Health Center får du reda på genom att visa en röd punkt. 

![Azure ATP health center bild med röd punkt](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Känsliga grupper

Information om känsliga grupper i ATP finns [arbeta med känsliga grupper](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Om du håller muspekaren över en entitet, var som helst i arbetsytans portal där det finns en enda entitet presenteras, t.ex en användare eller en dator, en miniprofil automatiskt öppnas visar följande information, om tillgänglig och relevanta:

![Bild för miniprofil för Azure ATP](media/atp-mini-profile.png)

- Namn
- Titel
- Avdelning
- AD-taggar
- E-post
- Office
- Telefonnummer
- Domain
- SAM-namn
- Skapad – när entiteten skapades i Active Directory. Om har skapats innan Azure ATP startade övervakningen kan visas den inte.
- Först sedd – första gången Azure ATP observerade en aktivitet från den här entiteten.
- Senast sedd - senast Azure ATP observerade en aktivitet från den här entiteten.
- SA-märket - visas om det finns misstänkta aktiviteter som är associerade med den här entiteten.
- WD ATP märket-kommer att visa om det finns misstänkta aktiviteter i Windows Defender ATP som är associerade med den här entiteten.
- Lateral förflyttning sökvägar ge en skylt – visas om det har gjorts laterala rörelsebanor identifieras för den här entiteten inom de senaste två dagarna.


## <a name="see-also"></a>Se även

- [Skapa Azure ATP-arbetsytor](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)