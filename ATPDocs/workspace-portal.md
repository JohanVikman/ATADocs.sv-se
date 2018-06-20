---
title: Förstå Azure Advanced Threat Protection arbetsytan portal | Microsoft Docs
description: Beskriver hur du loggar in Azure ATP arbetsytan portal och komponenter i arbetsytan-portalen
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40e139cc5e7dc6396914b0314d2d698a4782af02
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444713"
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Arbeta med Azure ATP arbetsytan portal

Använda Azure ATP arbetsytan portal för att övervaka och svara på misstänkt aktivitet identifieras av ATP.

Att skriva den `?` nyckeln innehåller kortkommandon för Azure ATP arbetsytan portal hjälpmedel. 

Azure ATP arbetsytan portal ger dig en snabb överblick över alla misstänkta aktiviteter i kronologisk ordning. Den gör det möjligt att visa detaljer om alla aktiviteter och utföra åtgärder baserat på dessa aktiviteter. Arbetsytan portalen visar även meddelanden och aviseringar som belyser problem som ses av Azure ATP eller nya aktiviteter som bedöms som misstänkta.

Den här artikeln beskriver hur du arbetar med de viktigaste beståndsdelarna i Azure ATP arbetsytan portal.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Aktivera åtkomst till Azure ATP arbetsytan portal
Du måste logga in med en användare som har tilldelats rätt Azure Active Directory-säkerhetsgrupp åt Azure ATP arbetsytan portalen för att logga in på Azure ATP arbetsytan portalen. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP rollgrupper](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Logga in på Azure ATP arbetsytan portal

1. Du kan ange arbetsytan portal genom att logga in på hanteringsportalen arbetsytan [ https://portal.atp.azure.com ](https://portal.atp.azure.com) och sedan välja relevanta arbetsytan eller bläddra till URL: en för arbetsytan: [https:// *workspacename*. atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Använder den token att logga in på Azure ATP arbetsytan portal Azure ATP stöder enkel inloggning integrerad med Windows-autentisering - om du redan har loggat in på datorn, Azure ATP. Du kan också logga in med ett smartkort. Din behörighet i Azure ATP motsvarar dina [administratörsroll](atp-role-groups.md).

 > [!NOTE]
 > Se till att logga in på datorn som du vill komma åt Azure ATP-arbetsytan-portalen med ditt Azure ATP admin användarnamn och lösenord. Du kan också köra din webbläsare som en annan användare eller loggar ut från Windows- och loggfiler med din Azure ATP administratörsanvändare. 


### <a name="attack-time-line"></a>Tidslinje för attacker

Detta är den standardsida du kommer till när du loggar in på Azure ATP arbetsytan portal. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan filtrera tidslinjen för att visa alla, öppna, avvisade eller Suppressed misstänkta aktiviteter. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet.

![Azure ATP bild för tidslinje för attacker](media/atp-sa-timeline.png)

Mer information finns i [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Nyheter

När en ny version av Azure ATP släpps, den **nyheter** visas i övre högra så att du vet vad har lagts till i den senaste versionen. Det ger dig också med en länk till version hämtningen.

### <a name="filtering-panel"></a>Filtreringspanel

Du kan filtrera vilka misstänkta aktiviteter som visas i tidslinjen för attacker eller som visas på entitetsprofilens flik för misstänkta aktiviteter baserat på status och allvarlighetsgrad.

### Sökfält <a name="search-bar"></a>

Du kan hitta ett sökfält i den översta menyn. Du kan söka efter en viss användare, dator eller grupper i Azure ATP. Om du vill prova är det bara att börja skriva. Antalet sökresultat hittades anges längst ned i sökfältet. 

![Azure portal-sökning avbildning för ATP arbetsytan](media/atp-workspace-portal-search.png)

Om du klickar på antalet kan du komma åt sökresultatsidan där du kan filtrera resultaten efter entitetstypen för ytterligare undersökning.

![sökresultat](media/search-results.png)

### <a name="health-center"></a>Health center

Health center visar aviseringar om något inte fungerar korrekt i Azure ATP-arbetsyta.

![Azure bild ATP health center](media/atp-health-issue.png)

Varje gång systemet upptäcker ett problem, till exempel ett anslutningsfel eller en frånkopplad Azure ATP fristående sensor får ikonen för Health Center du reda på genom att visa en röd punkt. 

![Azure ATP health center bild med röd punkt](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Känsliga grupper

Mer information om känsliga grupper i ATP finns [arbeta med känsliga grupper](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Om du håller muspekaren över en entitet, var som helst i arbetsytan portal där det finns en enda entitet presenteras, t.ex en användare eller en dator, en miniprofil automatiskt öppnas med följande information, om tillgängliga och relevanta:

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
- Skapas på – när entiteten har skapats i Active Directory. Om skapades innan Azure ATP startade övervakningen, kommer det inte visas.
- Första gången – första gången Azure ATP observerats en aktivitet från den här entiteten.
- Senast visade - senast Azure ATP observerats en aktivitet från den här entiteten.
- SA Aktivitetsikon - visas om misstänkta aktiviteter som är associerade med den här entiteten.
- WD ATP Aktivitetsikon-kommer att visas om misstänkta aktiviteter i Windows Defender ATP som är associerade med den här entiteten.
- Lateral förflyttning sökvägar badge - visas om det har gjorts lateral förflyttning sökvägar identifieras för den här entiteten inom de senaste två dagarna.


## <a name="see-also"></a>Se även

- [Skapa Azure ATP arbetsytor](install-atp-step1.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)