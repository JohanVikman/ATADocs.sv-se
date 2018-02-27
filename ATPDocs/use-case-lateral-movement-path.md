---
title: "Undersöka lateral förflyttning sökväg attacker med Azure ATP | Microsoft Docs"
description: "Den här artikeln beskriver hur du identifiera lateral förflyttning sökväg attacker med Azure Advanced Threat Protection (ATP)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection version 1.9.*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Undersöka lateral förflyttning sökvägar med Azure ATP

Azure ATP kan hjälpa dig att förhindra angrepp som använder lateral förflyttning sökvägar. Även om du gör ditt bästa att skydda känsliga användarna dina administratörer har komplexa lösenord som de ändras ofta sina datorer har blivit hårdare och deras data lagras på ett säkert sätt, angripare kan fortfarande använda lateral förflyttning sökvägar, flytta över nätverket mellan användare och datorer tills de har nått högsta vinsten virtuella säkerhet: dina känsliga admin-autentiseringsuppgifter.

## <a name="what-is-a-lateral-movement-path"></a>Vad är lateral förflyttning sökvägen?

Lateral förflyttning är när en angripare proaktivt icke-känsliga konton används för att få åtkomst till känsliga konton. De kan använda någon av metoderna som beskrivs i den [misstänkt aktivitet guide](suspicious-activity-guide.md) att få första icke-känsliga lösenordet och sedan använda ett verktyg som Bloodhound, för att förstå som administratörerna i nätverket och vilka datorer de använde. De kan sedan dra nytta av data som är tillgängliga för angripare på domänkontrollanterna att veta vem som har vilka konton och åtkomst till vilka resurser och filer och kan stjäla autentiseringsuppgifter från andra användare (ibland känsliga användare) lagras på datorer som de har redan nås och flytta sedan sidled till fler användare och resurser förrän de uppnå administratörsrättigheter i nätverket. 

Azure ATP kan du vidta åtgärder för pre-emptive i nätverket för att förhindra angripare från att lyckas på lateral förflyttning.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Identifiering av dina vilka känsliga konton

Följ dessa steg för att identifiera vilka känsliga konton i nätverket är sårbara på grund av sin anslutning till icke-känsliga konton och resurser. För att skydda nätverket från lateral förflyttning attacker Azure ATP fungerar från slutet bakåt, vilket innebär att Azure ATP ger dig en karta som startar från dina Privilegierade konton och sedan visar vilka användare och enheter är lateral sökvägen till dessa användare och deras autentiseringsuppgifter.

1. Klicka på ikonen rapporter i portalen menyn Azure ATP arbetsytan ![ikonen rapporter](./media/atp-report-icon.png).

2. Under **Lateral förflyttning sökvägar till känsliga konton**, om det finns inga lateral förflyttning sökvägar hitta rapporten är nedtonad. Om det finns lateral förflyttning sökvägar, sedan datum för rapporten väljer automatiskt först datum när det relevanta data. Lateral förflyttning sökväg rapporten innehåller data för de senaste 60 dagarna.

 ![rapporter](./media/reports.png)

3. Klicka på **hämta**.

3. Excel-filen som skapas innehåller information om din känsliga konton som är i fara. Den **sammanfattning** innehåller diagram som innehåller information om antalet känsliga konton, datorer och medelvärden för vilka resurser. Den **information** innehåller en lista över känsliga konton som du bör vara orolig.

4. Instruktioner om hur du ställer in dina servrar så att Azure ATP utföra SAM-R-åtgärder som behövs för identifiering av lateral förflyttning sökväg, [konfigurera SAM-R](install-atp-step8-samr.md).

## <a name="investigate"></a>Undersök

Nu när du vet vilka känsliga konton är i fara, kan du djupa fördjupa dig i Azure ATP vill veta mer och vidta förebyggande åtgärder.

1. I arbetsytan ATP Azure-portalen titta på den användare vars konto anges som sårbara i den **Lateral förflyttning sökvägar till känsliga konton** rapport, till exempel Samira Abbasi. Du kan också söka efter Lateral förflyttning Aktivitetsikon som har lagts till entitetsprofilen när enheten är i en lateral förflyttning sökväg ![lateral ikonen](./media/lateral-movement-icon.png) eller ![sökväg ikonen](./media/paths-icon.png). Detta är tillgängligt om det fanns lateral förflyttning inom de senaste två dagarna. 

2. I den användarprofilsidan som öppnas, klickar du på den **Lateral förflyttning sökvägar** fliken. 

3. Som visas i diagrammet innehåller en karta över möjliga sökvägar till känsliga användaren. Diagrammet visar anslutningar som har gjorts under de senaste två dagarna, så den är ny. Om aktiviteten inte upptäcks under de senaste två dagarna inte visas i diagrammet, men [lateral förflyttning sökväg rapporten](reports.md) kommer fortfarande att kunna ge dig information om lateral förflyttning sökvägar under de senaste 60 dagarna.

4. Granska diagram om du vill se vad du kan lära dig om exponering av känsliga användarens autentiseringsuppgifter. Till exempel i den här kartan Samira Abbasi kan du följa den **loggas i av** grå pilar Se där Samira loggat in med sina Privilegierade autentiseringsuppgifter. I det här fallet har Samiras känsliga autentiseringsuppgifter sparats på datorn REDMOND-WA-Utvecklartestning Sedan se vilka andra användare är inloggad på vilka datorer som skapats mest exponering och säkerhetsproblem. Du kan se detta genom att titta på den **administratör på** svarta pilar vem som har administratörsrättigheter på resursen. I det här exemplet har alla i gruppen Alla Contoso möjlighet att komma åt autentiseringsuppgifter från den här resursen.  

 ![sökvägar för användarens profil lateral förflyttning](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Förebyggande bästa praxis

- Det bästa sättet att förhindra lateral förflyttning är att säkerställa att känsliga användare använder administratörskontot endast när du loggar in på strikt datorer. I det här exemplet kontrollerar du att om administratören Samira behöver åtkomst till REDMOND-WA-utveckling, de loggar in med ett användarnamn och lösenord än sina autentiseringsuppgifter som administratör.

- Det rekommenderas också att du ser till att ingen har onödiga administrativ behörighet. I det här exemplet ska du kontrollera om alla i Contoso alla verkligen behöver administratörsrättigheter på REDMOND-WA-Utvecklartestning

- Det är alltid en bra idé att kontrollera att personer har endast åtkomst till resurser. Som du ser i exemplet utökar Oscar Posada avsevärt Samiras exponering. Är det nödvändigt att användaren ska ingå i Contoso alla? Finns det undergrupper som du kan skapa för att minska exponeringen?


## <a name="see-also"></a>Se även

- [Konfigurera SAM-R krävs behörigheter](install-atp-step8-samr.md)
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)