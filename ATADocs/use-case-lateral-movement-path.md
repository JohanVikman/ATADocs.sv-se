---
title: Utreda attacker med laterala sökväg med ATA | Microsoft Docs
description: Den här artikeln beskriver hur du identifiera lateral förflyttning sökväg attacker med Advanced Threat Analytics (ATA).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0d247671c43e4c62f740eca263f2e0e680c7d319
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133994"
---
*Gäller för: Advanced Threat Analytics version 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Undersöka laterala förflyttningssökvägar med ATA

Även om du gör din bästa för att skydda din känsliga användare och administratörer har komplexa lösenord som de ändras ofta, är härdade sina datorer och deras data lagras på ett säkert sätt, kan angripare fortfarande använda laterala rörelsebanor till känsliga konton. Vid laterala attacker drar angriparen nytta av instanser när känsliga användare loggar in på en dator där en icke-känsliga användare har lokala rättigheter. Angripare kan sedan flytta i sidled, åtkomst till mindre känsliga användaren och sedan flytta mellan datorn att få autentiseringsuppgifter för känsliga användare. 

## <a name="what-is-a-lateral-movement-path"></a>Vad är en lateral rörelsesökväg?

Lateral förflyttning är när en angripare använder icke-känsliga konton för att få åtkomst till känsliga konton. Detta kan göras med hjälp av metoderna som beskrivs i den[guide för misstänkt aktivitet](suspicious-activity-guide.md). Angriparen kan komma åt för att förstå som administratörerna ingår i ditt nätverk och vilka datorer, angriparen kan dra nytta av data på domänkontrollanterna. 

ATA kan du vidta förebyggande åtgärder för nätverket för att förhindra angripare från att lyckas på lateral förflyttning.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Identifiering av din Projektstatistik känsliga konton

För att identifiera vilka känsliga konton i ditt nätverk var sårbara på grund av sin anslutning till icke-känsliga konton eller resurser i en viss tidsperiod, Följ stegen nedan. 

1. I menyn ATA-konsolen klickar du på ikonen rapporter ![ikonen rapporter](./media/ata-report-icon.png).

2. Under **laterala rörelsebanor till känsliga konton**, om det finns inga laterala rörelsebanor hittades i rapporten är nedtonade. Om det finns laterala rörelsebanor, sedan datum i rapporten väljer automatiskt först datum när det relevanta data. 

 ![rapporter](./media/reports.png)

3. Klicka på **hämta**.

3. Excel-filen som skapas får du information om dina känsliga konton som är i fara. Den **sammanfattning** visar fliken diagram som specificerar antalet känsliga konton, datorer och medelvärden för Projektstatistik resurser. Den **information** fliken innehåller en lista över känsliga konton som du bör vara orolig. Observera att sökvägarna är sökvägar som fanns tidigare, och kanske inte är tillgängliga idag.


## <a name="investigate"></a>Undersök

Nu när du vet vilka känsliga konton riskerar du djupgående kan fördjupa dig i ATA för att lära dig mer och vidta förebyggande åtgärder.

1. Sök efter Lateral förflyttning märket som läggs till entitetsprofilen när enheten är i en lateral rörelsesökväg i ATA-konsolen ![lateral ikon](./media/lateral-movement-icon.png) eller ![ikon för sökvägen](./media/paths-icon.png). Detta är tillgängligt om det var en lateral rörelsesökväg under de senaste två dagarna.

2. I användarprofilsidan som öppnas, klickar du på den **Lateral förflyttning** fliken.

3. Diagrammet som visas innehåller en karta över möjliga sökvägarna till känsliga användare. Diagrammet visar anslutningar som har gjorts under de senaste två dagarna.

4. Granska i grafen för att se vad du kan lära dig om exponering av känsliga-användarens autentiseringsuppgifter. Till exempel i den här kartan du följa den **inloggad på av** grå pilar att se där Samira loggat in med sina Privilegierade autentiseringsuppgifter. I det här fallet har Samiras känsliga autentiseringsuppgifter sparats på datorn REDMOND-WA-utveckling. Sedan kan se vilka andra användare är inloggad på vilka datorer som skapats mest exponering och säkerhetsproblem. Du kan se detta genom att titta på den **administratör på** svarta pilarna för att se vem som har administratörsrättigheter på resursen. I det här exemplet, alla i gruppen **Contoso alla** har möjlighet att komma åt autentiseringsuppgifter från den här resursen.  

 ![användarens profil laterala rörelsebanor](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Förebyggande Metodtips

- Det bästa sättet att förhindra lateral förflyttning är att se till att känsliga användare använder sina administratörsautentiseringsuppgifter för bara när du loggar in härdade datorer där det finns inga icke-känsliga användare som har administratörsrättigheter på samma dator. I det här exemplet kontrollerar du att om Samira behöver åtkomst till REDMOND-WA-utveckling, hon loggar in med ett användarnamn och lösenord än sina administratörsautentiseringsuppgifter för eller ta bort gruppen för Contoso alla från den lokala administratörsgruppen på REDMOND-WA-utveckling.

- Vi rekommenderar också att du ser till att ingen har onödiga lokal administratörsbehörighet. I det här exemplet ska du kontrollera om alla i Contoso alla verkligen måste ha administratörsrättigheter på REDMOND-WA-utveckling.

- Kontrollera att användare bara har åtkomst till resurser som krävs. I det här exemplet utökar Oscar Posada avsevärt Samiras exponering. Är det nödvändigt att han tas med i gruppen **Contoso alla**? Finns det undergrupper som du kan skapa för att minska exponeringen?

**Tips** – om aktiviteten inte har identifierats under de senaste två dagarna, visas inte i diagrammet, men rapporten laterala sökvägen kommer fortfarande att kunna ge dig information om laterala rörelsebanor under de senaste 60 dagarna.

**Tips** – information om hur du ställer in dina servrar till att ATA kan utföra SAM-R-åtgärder som krävs för identifiering av laterala sökväg, [konfigurera SAM-R](install-ata-step9-samr.md).




## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
