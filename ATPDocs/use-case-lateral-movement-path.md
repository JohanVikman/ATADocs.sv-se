---
title: Utreda attacker med laterala sökväg med Azure ATP | Microsoft Docs
description: Den här artikeln beskriver hur du identifiera lateral förflyttning sökväg attacker med Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 270b84c24ef8b52565ee97c2c15374645eb54a2c
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469659"
---
*Gäller för: Azure Avancerat skydd*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Undersöka laterala förflyttningssökvägar med Azure ATP


Lateral förflyttning är när en angripare använder icke-känsliga konton för att få åtkomst till känsliga konton. Detta kan göras med hjälp av metoderna som beskrivs i den [guide för misstänkt aktivitet](suspicious-activity-guide.md). Lateral förflyttning används av angripare för att identifiera och få åtkomst till känsliga konton och datorer i nätverket med hjälp av icke-känsliga konton som delar lagrade logga in autentiseringsuppgifter i konton, grupper och datorer. När en angripare har fått åtkomst kan kan angriparen också dra nytta av data på domänkontrollanterna.


## <a name="discover-your-at-risk-sensitive-accounts"></a>Identifiera dina Projektstatistik känsliga konton

Följ dessa steg för att identifiera vilka känsliga konton i nätverket är tillgängliga på grund av sin anslutning till icke-känsliga konton, grupper och datorer. 

1. Klicka på ikonen rapporter i portalen menyn Azure ATP-arbetsyta ![ikonen rapporter](./media/atp-report-icon.png).

2. Under **laterala rörelsebanor till känsliga konton**, om det finns inga risken laterala rörelsebanor hittades i rapporten är nedtonade. Om det finns potentiella lateral förflyttning, rapporten före väljer automatiskt först datum när relevanta data. Lateral förflyttning sökväg-rapporten innehåller data för upp till 60 dagar.

 ![rapporter](./media/reports.png)

3. Klicka på **hämta**.

4. En Excel-fil skapas som ger dig information om potentiella lateral förflyttning och känsligt konto exponeringen för de datum som valts. Den **sammanfattning** visar fliken diagram som specificerar antalet känsliga konton, datorer och medelvärden för Projektstatistik åtkomst. Den **information** fliken innehåller en lista över de känsliga konton som du bör undersöka vidare. Observera att sökvägar som beskrivs i nedladdningsbara rapporten kan inte längre vara tillgängliga eftersom de upptäcktes under de senaste 60 dagarna och kan ha ändrats eller har ändrats.


## <a name="investigate"></a>Undersök



1. I Azure ATP-arbetsyteportalen, söker du efter Lateral förflyttning märket som läggs till entitetsprofilen när enheten är i en lateral rörelsesökväg ![lateral ikon](./media/lateral-movement-icon.png) eller ![ikon för sökvägen](./media/paths-icon.png). Observera att Aktivitetsikoner visas bara om det har lateral förflyttning inom de senaste 48 timmarna. 

2. I användarprofilsidan som öppnas, klickar du på den **Lateral förflyttning** fliken. 

3. Diagrammet som visas innehåller en karta över möjliga sökvägarna till känsliga användare. Diagrammet visar möjliga anslutningar som observerats under de senaste 48 timmarna. Om ingen aktivitet har identifierats under de senaste två dagarna, visas inte i diagrammet. 

4. Granska i grafen för att se vad du kan lära dig om exponering av känsliga-användarens autentiseringsuppgifter. Till exempel i den här kartan du följa den **inloggad på av** grå pilar att se där Samira loggat in med sina autentiseringsuppgifter. I det här fallet sparades Samiras känsliga autentiseringsuppgifter på REDMOND-WA-DEV-dator. Titta nu, vilka andra användare som är inloggade i vilka datorer som skapats mest exponering och säkerhetsproblem. Du kan se detta genom att titta på den **administratör på** svarta pilarna för att se vem som har administratörsrättigheter på resursen. I det här exemplet har alla i gruppen Alla Contoso möjlighet att komma åt autentiseringsuppgifter från den här resursen.  

 ![användarens profil laterala rörelsebanor](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Förebyggande Metodtips

- Det bästa sättet att förhindra lateral förflyttning är att se till att känsliga användare använder sina administratörsautentiseringsuppgifter för bara när du loggar in härdade datorer. I det här exemplet kontrollerar du att om Samira administratören behöver åtkomst till REDMOND-WA-utveckling, de loggar in med ett användarnamn och lösenord än sina autentiseringsuppgifter som administratör.

- Vi rekommenderar också att du ser till att ingen har onödiga administrativ behörighet. I det här exemplet ska du kontrollera om alla i Contoso alla faktiskt kräver administratörsrättigheter på REDMOND-WA-utveckling.

- Kontrollera att användare bara har åtkomst till resurser som krävs. I det här exemplet utökar Oscar Posada avsevärt Samiras exponering. Är det nödvändigt att den här användaren tas med i gruppen **Contoso alla**? Finns det undergrupper som kan skapas för att minska exponeringen?

**Tips** – när ingen aktivitet har identifierats under de senaste 48 timmarna och diagrammet är inte tillgänglig, lateral förflyttning sökväg rapporten finns kvar och ger dig information om potentiella laterala rörelsebanor som identifierats under de senaste 60 dagarna. 

**Tips** – för instruktioner om hur du ställer in dina klienter och servrar för att tillåta Azure ATP att utföra SAM-R-åtgärder som krävs för identifiering av laterala sökväg, se [konfigurera SAM-R](install-atp-step8-samr.md).


## <a name="see-also"></a>Se även

- [Konfigurera SAM-R obligatoriska behörigheter](install-atp-step8-samr.md)
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)