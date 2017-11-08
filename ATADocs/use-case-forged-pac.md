---
title: "Undersöka behörighetseskalering via attacker med förfalskade auktoriseringsdata | Microsoft Docs"
description: "Den här artikeln beskriver behörighetseskalering via attacker med förfalskad auktoriseringsdata och innehåller instruktioner för hur du undersöker det här hotet när det identifieras i ditt nätverk."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1820687d1340dfbef703129e5fad7d7a63cfd632
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*

# <a name="investigating-privilege-escalation-using-forged-authorization-data-attacks"></a>Undersöka behörighetseskalering via attacker med förfalskade auktoriseringsdata

Microsoft arbetar ständigt för att förbättra säkerhetsfunktioner för identifiering och möjligheten att tillhandahålla värdefull information till säkerhetsanalytiker i nära realtid. Microsoft Advanced Threat Analytics (ATA) är ledande när det gäller de här förbättringarna. Om ATA identifierar ett privilegium eskalering med förfalskad auktorisering data misstänkt aktivitet på ditt nätverk och varnar dig om det, den här artikeln får du förstå och undersöka den.

## <a name="what-is-a-privileged-attribute-certificate-pac"></a>Vad är ett PAC (Privileged Attribute Certificate)?

Privilege Attribute Certificate (PAC) är en datastruktur i Kerberos-biljett, som innehåller auktoriseringsinformation om, inklusive gruppmedlemskap, säkerhetsidentifierare och användarens profilinformation. I en Active Directory-domän blir det möjligt att skicka auktoriseringsdata som tillhandahålls av domänkontrollanten (DC) till andra medlemsservrar och arbetsstationer för autentisering och auktorisering. Utöver information om medlemskap innehåller PAC även ytterligare autentiseringsinformation, profil- och principinformation samt säkerhetsmetadata som stöds. 

PAC-datastrukturen används av autentiseringsprotokoll (protokoll som verifierar identiteter) för att transportera autentiseringsinformation som styr åtkomst till resurser.

### <a name="pac-validation"></a>PAC-verifiering

PAC-verifiering är en säkerhetsfunktion för att hindra angripare från att få obehörig åtkomst till ett system eller dess resurser med ett man-in-the-middle-angrepp, särskilt i program där användarpersonifiering används. Personifiering rör en betrodd identitet, till exempel ett tjänstkonto som har beviljats utökade behörigheter för att komma åt resurser och utföra åtgärder. PAC-verifiering förstärker en säkrare auktoriseringsmiljö i inställningarna för Kerberos-autentisering där personifiering inträffar. [PAC-verifiering](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) ser till att en användare anger exakta auktoriseringsdata, som de är beviljade i Kerberos-biljetten, och att biljettens behörigheter inte har ändrats.

När PAC-verifieringen sker kodar servern ett meddelande med en begäran som innehåller PAC-signaturtypen och längden och skickar den till domänkontrollanten. Domänkontrollanten avkodar begäran och extraherar kontrollsumman för servern och KDC-kontrollsummorna. Om verifieringen av kontrollsumman lyckas returnerar domänkontrollanten returkoden till servern. Ett misslyckad returkod indikerar att PAC har ändrats. 

Innehållet i Kerberos-PAC signeras två gånger: 
- En gång med huvudnyckeln för KDC för att förhindra att skadliga tjänster på serversidan ändrar i auktoriseringsdata
- En gång med huvudnyckeln för kontot på resursservern som är målet för att förhindra användare från att ändra PAC-innehållet och lägga till egna auktoriseringsdata

### <a name="pac-vulnerability"></a>PAC-säkerhetsrisk
Säkerhetsbulletinerna [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) och [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) åtgärdar säkerhetsproblem i Kerberos KDC som gör att en angripare kan manipulera PAC-fältet i en giltig Kerberos-biljett, vilket gör att personen kan bevilja sig själv ytterligare behörigheter.

## <a name="privilege-escalation-using-forged-authorization-data-attack"></a>Attack via behörighetseskalering med förfalskade auktoriseringsdata

En attack via behörighetseskalering med förfalskade auktoriseringsdata är ett försök av en angripare att dra nytta av PAC-säkerhetsrisker för att utöka sina privilegier i din Active Directory-skog eller Active Directory-domän. För att utföra angreppet måste angriparen:
-   Ha autentiseringsuppgifterna för en domänanvändare.
-   Ha nätverksanslutning till en domänkontrollant som kan användas för att autentisera mot komprometterade domänautentiseringsuppgifter.
-   Ha de rätta verktygen. Python Kerberos utnyttjande Kit (PyKEK) är ett känt verktyg som forges PACs.

Om angriparen har de nödvändiga autentiseringsuppgifterna och anslutningarna så kan han eller hon ändra eller förfalska PAC (Privileged Attribute Certificate) för en befintlig Kerberos-användarinloggningstoken (TGT). Angriparen ändrar kravet för gruppmedlemskap så att en grupp med högre privilegier tas med (till exempel ”Domänadministratörer” eller ”Företagsadministratörer”). Angriparen tar sedan med det ändrade PAC-certifikatet i Kerberos-biljetten. Kerberos-biljetten används sedan för att begära en tjänstbiljett från en okorrigerad domänkontrollant som ger angriparen utökade behörigheter i domänen och auktoritet att utföra åtgärder som personen inte ska kunna utföra. En angripare kan använda den ändrade inloggningstoken för användare (TGT) för att få tillgång till alla resurser i domänen genom att begära token för resursåtkomst (TGS). Detta innebär att en angripare kan kringgå konfigurerade alla resurs ACL: er som begränsar åtkomst i nätverket med förfalskning auktoriseringsdata (PAC) för alla användare i Active Directory.

## <a name="discovering-the-attack"></a>Identifiera angreppet
När angripare försöker öka sina privilegier, ATA identifierar den och markera det som en hög allvarlighetsgrad.

![Misstänkt förfalskad PAC-aktivitet](./media/forged-pac.png)

ATA anger för misstänkt aktivitet aviseringen om eskalering av privilegier med förfalskad auktoriseringsdata lyckades eller om den inte. Både aviseringar om lyckade och misslyckade försök bör undersökas eftersom misslyckade försök kan tyda på att en angripare finns i miljön.

## <a name="investigating"></a>Undersöka
När du har fått aviseringen om behörighetseskalering med auktoriseringsdata i ATA måste du avgöra vad som behöver göras för att undvika angreppet. Om du vill göra detta måste klassificera du först aviseringen som en av följande typer av aviseringar: 
-   Sann positiv: En skadlig åtgärd som identifierats av ATA
-   Falsk positiv identifiering: En falsk avisering – behörighetseskaleringen med förfalskade auktoriseringsdata inträffade egentligen aldrig (det rör sig om en händelse som ATA misstog för en attack via behörighetseskalering med förfalskade auktoriseringsdata)
-   Godartad sann positiv: En åtgärd som identifierats av ATA som fungerar som ett hot men som inte är skadlig, till exempel ett genomslagstest

Följande diagram hjälper dig att avgöra hur du ska agera:

![Diagram över förfalskat PAC](./media/forged-pac-diagram.png)

1. Kontrollera först aviseringen i attacktidslinjen i ATA för att se om försöket att förfalska auktoriseringen lyckades, misslyckades eller bara var ett försök (attacker som bara är försök är också misslyckade attacker). Både lyckade och misslyckade försök kan leda till sanna positiva försök, men med olika grader av allvarlighet i miljön.
 
 ![Misstänkt förfalskad PAC-aktivitet](./media/forged-pac-sa.png)


2.  Om den identifierade attacken via behörighetseskalering med förfalskade auktoriseringsdata lyckades:
    -   Om domänkontrollanten där aviseringen skapades är korrekt uppdaterad är det en falsk positiv händelse. I det här fallet bör du stänga av aviseringen och skicka ett e-postmeddelande till ATA-teamet på ATAEval@microsoft.com så att ATA kan kontinuerligt förbättra dess identifieringar. 
    -   Om domänkontrollanten i aviseringen inte är korrekt uppdaterad:
        -   Om tjänsten som anges i aviseringen inte har en egen auktoriseringsmekanism så är det en sann positiv händelse och du bör köra organisationens IR-process. 
        -   Om tjänsten som anges i aviseringen har en intern auktoriseringsmekanism som begär auktoriseringsdata, kan händelsen felaktigt identifieras som en attack via behörighetseskalering med förfalskade auktoriseringsdata. 

3.  Om den identifierade attacken misslyckades:
    -   Om operativsystemet eller programmet kan ändra PAC-certifikatet så är det troligen en godartad sann positiv händelse och du bör arbeta tillsammans med programmets eller operativsystemets ägare för att åtgärda problemet.

    -   Om operativsystemet eller programmet inte kan ändra PAC-certifikatet: 

        -   Om tjänsten som anges inte har en egen auktoriseringstjänst är det en sann positiv händelse och du bör köra organisationens IR-process. Även om angripare inte rensades öka sina privilegier i domänen, kan du anta det finns en angripare i nätverket och du vill söka efter dem så snart som möjligt innan de försöker andra kända avancerade beständiga attacker att upphöja sina privilegier. 
        -   Om tjänsten som anges i aviseringen har sin egen auktoriseringsmekanism som begär auktoriseringsdata, kan händelsen felaktigt identifieras som en attack via behörighetseskalering med förfalskade auktoriseringsdata.

## <a name="post-investigation"></a>Efter undersökningen
Microsoft rekommenderar att du använder ett professionellt team för incidentsvar och återställning, som kan nås via ditt Microsoft-kontoteam, för att få hjälp med att identifiera om en angripare har distribuerat ihållande metoder i nätverket.


## <a name="mitigation"></a>Lösningar

Använd säkerhetsbulletinerna [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) och [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) som åtgärdar säkerhetsbrister i Kerberos KDC. 


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
