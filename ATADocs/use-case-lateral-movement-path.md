---
title: "Undersöka lateral förflyttning sökväg attacker med ATA | Microsoft Docs"
description: "Den här artikeln beskriver hur du identifiera lateral förflyttning sökväg attacker med Advanced Threat Analytics (ATA)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Undersöka lateral förflyttning sökvägar med ATA

När du gör dina bästa för att skydda känsliga användarna och dina administratörer har komplexa lösenord som de ändras ofta sina datorer har blivit hårdare och deras data lagras på ett säkert sätt kan kan angripare fortfarande använda lateral förflyttning sökvägar att komma åt känsliga konton. I lateral förflyttning attacker utnyttjar angripare instanser när känsliga användare loggar in på en dator där en användare med icke-känsliga har lokala rättigheter. Angripare kan sedan flytta sidled, åtkomst till mindre känsliga användaren och sedan flytta över datorn att komma över autentiseringsuppgifter för känsliga användaren. 

## <a name="what-is-a-lateral-movement-path"></a>Vad är lateral förflyttning sökvägen?

Lateral förflyttning är när en angripare proaktivt icke-känsliga konton används för att få åtkomst till känsliga konton. De kan använda någon av metoderna som beskrivs i den [misstänkt aktivitet guide](suspicious-activity-guide.md) att få första icke-känsliga lösenordet och sedan använda ett verktyg som Bloodhound, för att förstå som administratörerna i nätverket och vilka datorer de använde. De kan sedan komma åt data på domänkontrollanterna att veta vem som har vilka konton och åtkomst till vilka resurser och filer, stjäla autentiseringsuppgifter från andra användare (ibland känsliga användare) som är lagrade på de datorer som de redan har använt och sedan Flytta sidled över användare och resurser förrän de uppnå administratörsrättigheter i nätverket. 

ATA kan du vidta åtgärder för pre-emptive i nätverket för att förhindra angripare från att lyckas på lateral förflyttning.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Identifiering av dina vilka känsliga konton

Följ dessa steg för att identifiera vilka känsliga konton i nätverket är sårbara på grund av sin anslutning till icke-känsliga konton och resurser. För att skydda nätverket från lateral förflyttning attacker fungerar ATA från slutet bakåt, vilket innebär att ATA ger dig en karta som startar från dina Privilegierade konton och sedan visar vilka användare och enheter är lateral sökvägen till dessa användare och sina autentiseringsuppgifter.

1. I menyn ATA-konsolen klickar du på ikonen rapporter ![ikonen rapporter](./media/ata-report-icon.png).

2. Under **Lateral förflyttning sökvägar till känsliga konton**, om det finns inga lateral förflyttning sökvägar hitta rapporten är nedtonad. Om det finns lateral förflyttning sökvägar, sedan datum för rapporten väljer automatiskt först datum när det relevanta data. 

 ![rapporter](./media/reports.png)

3. Klicka på **hämta**.

3. Excel-filen som skapas innehåller information om din känsliga konton som är i fara. Den **sammanfattning** innehåller diagram som innehåller information om antalet känsliga konton, datorer och medelvärden för vilka resurser. Den **information** innehåller en lista över känsliga konton som du bör vara orolig.


## <a name="investigate"></a>Undersök

Nu när du vet vilka känsliga konton är i fara, kan du djupa fördjupa dig i ATA att lära sig mer och vidta förebyggande åtgärder.

1. I ATA-konsolen titta på den användare vars konto anges som sårbara i den **Lateral förflyttning sökvägar till känsliga konton** rapport, till exempel Samira Abbasi. Du en också söka efter Lateral förflyttning Aktivitetsikon som har lagts till entitetsprofilen när enheten är i en lateral förflyttning sökväg ![lateral ikonen](./media/lateral-movement-icon.png) eller ![sökväg ikonen](./media/paths-icon.png).

2. I den användarprofilsidan som öppnas, klickar du på den **Lateral förflyttning sökvägar** fliken.

3. Som visas i diagrammet innehåller en karta över möjliga sökvägar till känsliga användaren. Diagrammet visar anslutningar som har gjorts under de senaste två dagarna, så den är ny.

4. Granska diagram om du vill se vad du kan lära dig om exponering av känsliga användarens autentiseringsuppgifter. Till exempel i den här kartan Samira Abbasi kan du följa den **loggas i av** grå pilar Se där Samira loggat in med sitt Privilegierade autentiseringsuppgifter. I det här fallet har Samiras känsliga autentiseringsuppgifter sparats på datorn REDMOND-WA-Utvecklartestning Sedan se vilka andra användare är inloggad på vilka datorer som skapats mest exponering och säkerhetsproblem. Du kan se detta genom att titta på den **administratör på** svarta pilar vem som har administratörsrättigheter på resursen. I det här exemplet har alla i gruppen Alla Contoso möjlighet att komma åt autentiseringsuppgifter från den här resursen.  

 ![sökvägar för användarens profil lateral förflyttning](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Förebyggande bästa praxis

- Det bästa sättet att förhindra lateral förflyttning är att säkerställa att känsliga användare använder administratörskontot endast när du loggar in på strikt datorer där det finns inga icke-känsliga användare som har administratörsrättigheter på samma dator. I det här exemplet kontrollerar du att om Samira behöver åtkomst till REDMOND-WA-utveckling, hon loggar in med ett användarnamn och lösenord än sitt administratörsautentiseringsuppgifter eller ta bort gruppen Alla Contoso från den lokala administratörsgruppen på REDMOND-WA-Utvecklartestning

- Det rekommenderas också att du ser till att ingen har onödiga lokal administratörsbehörighet. I det här exemplet ska du kontrollera om alla i Contoso alla verkligen behöver administratörsrättigheter på REDMOND-WA-Utvecklartestning

- Det är alltid en bra idé att kontrollera att personer har endast åtkomst till resurser. Som du ser i exemplet utökar Oscar Posada avsevärt Samiras exponering. Är det nödvändigt att han ska ingå i Contoso alla? Finns det undergrupper som du kan skapa för att minska exponeringen?


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
