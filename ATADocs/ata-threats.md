---
title: Vilka hot identifierar Advanced Threat Analytics? | Microsoft Docs
description: "Visar en lista över hot som identifieras av Advanced Threat Analytics"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 630bb2b74dafcf9ab9b3469c2afbf8abc59c2dbf
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*

# <a name="what-threats-does-ata-look-for"></a>Vilka hot letar ATA efter?

ATA ger identifiering för följande olika faser i en avancerad attack: rekognosering, avslöjade autentiseringsuppgifter, lateral förflyttning, eskalering av privilegier, domändominans med mera. Dessa identifieringar är avsedda att identifiera avancerade attacker och insiderhot innan de skadar organisationen.
Identifieringen av varje fas ger flera misstänkta aktiviteter som är relevanta för fasen i fråga, där varje misstänkt aktivitet motsvarar olika varianter av möjliga attacker.
Faserna i attackkedjan där ATA för närvarande identifierar hot är markerade på bilden nedan.

![ATA fokuserar på lateral aktivitet i attackkedjan](media/attack-kill-chain-small.jpg)


### <a name="reconnaissance"></a>Rekognosering

ATA identifierar rekognosering på flera sätt. Dessa identifieringar omfattar:

-   **Rekognosering med kontouppräkning**<br></br>Identifierar försök från angripare som använder Kerberos-protokollet för att upptäcka om en användare finns, även om aktiviteten inte har loggats som en händelse på domänkontrollanten.

-   **Nettosessionsuppräkning**<br></br>Som en del av rekognoseringsfasen kan angripare fråga DC om alla aktiva SMB-sessioner på servern och ge dem åtkomst till alla användare och IP-adresser som är kopplade till dessa SMB-sessioner. SMB-sessionsuppräkningen kan användas av angripare för rikta in sig på känsliga konton, vilket hjälper dem att flyttas i sidled över nätverket.

-   **Rekognosering med DNS**<br></br>DNS-information i målnätverk är ofta mycket användbar rekognoseringsinformation. DNS-informationen innehåller en lista över alla servrar och ofta alla klienter och mappningen till deras IP-adresser. Genom att visa DNS-information kan angriparna få en detaljerad vy av dessa enheter i miljön, vilket gör det möjligt för angripare att fokusera sitt arbete på de relevanta enheterna för kampanjen.

-   **Rekognosering med uppräkning av katalogtjänster**<br></br>Identifierar rekognosering för entiteter (användare, grupper osv.) som utförts med hjälp av protokollet SAM-remote för att köra frågor mot domänkontrollanterna. Den här rekognoseringsmetoden är vanlig i många typer av skadlig kod som syns i verkliga attackscenarier. 


### <a name="compromised-credentials"></a>Avslöjade autentiseringsuppgifter

I syfte att ge identifiering av avslöjade autentiseringsuppgifter använder ATA både maskininlärningsbaserad analys samt kända skadliga attacker och teknikidentifiering.
Genom att använda beteendeanalys och maskininlärning kan ATA identifiera misstänkta aktiviteter, t.ex. avvikande inloggningar, onormal resursåtkomst och onormal arbetstid, vilket kan tyda på avslöjade autentiseringsuppgifter. I syfte att skydda mot avslöjade autentiseringsuppgifter identifierar ATA följande kända skadliga attacker och tekniker:

-   **Brute force**<br></br>Vid brute force-attacker försöker angripare gissa sig till autentiseringsuppgifter genom att prova flera användare och koppla ihop dem med flera lösenordsförsök. Angriparna använder ofta komplexa algoritmer eller ordböcker för att prova så många värden som ett system tillåter.

- **Misstänkta misslyckade autentiseringar** (beteendebaserad brute force) <br></br> Angripare försöker köra en råstyrkeattack (brute force) för att få fram autentiseringsuppgifter och angripa konton. ATA genererar en avisering när onormalt beteende vid misslyckade autentiseringar identifieras.

-   **Känsligt konto exponerat i klartextautentisering**<br></br>Om ett konto med högprivilegierade autentiseringsuppgifter skickas som klartext varnar ATA dig så att du kan uppdatera datorkonfigurationen.

-   **Tjänsten exponerar konton i klartextautentisering** <br></br>Om en tjänst på en dator skickar flera kontoautentiseringsuppgifter som klartext varnar ATA dig så att du kan uppdatera tjänstekonfigurationen.

-   **Misstänkt aktivitet för Honung Token-konto**<br></br>Honey Token-konton är falska konton som skapas för att fånga, identifiera och spåra skadliga aktiviteter som försöker använda dessa falska konton. ATA varnar dig om alla aktiviteter för dessa Honey Token-konton.

-   **Onormal protokollimplementering**<br></br>Autentiseringsbegäranden (Kerberos eller NTLM) utförs vanligtvis med en normal uppsättning metoder och protokoll. För att kunna autentisera måste dock begäran uppfylla en specifik kravuppsättning. Angripare kan implementera dessa protokoll med mindre avvikelser från den normala implementeringen i miljön. Dessa avvikelser kan tyda på att det finns en angripare som försöker utnyttja eller som har lyckats utnyttja avslöjade autentiseringsuppgifter.

-   **Skadlig privat informationsbegäran för dataskydd**<br></br>API för dataskydd (DPAPI) är en lösenordsbaserad dataskyddstjänst. Den här skyddstjänsten används av olika program som lagrar användarens hemligheter, t.ex. webbplatslösenord och autentiseringsuppgifter för filresurser. I syfte att ge stöd för scenarier med förlorat lösenord kan användare kryptera data med hjälp av en återställningsnyckel som inte omfattar lösenordet. I en domänmiljö kan angripare stjäla återställningsnyckeln fjärranslutet och använda den för att dekryptera skyddade data i alla domänanslutna datorer.

-   **Onormalt beteende**<br></br>Vid insiderhot och avancerade attacker kan ofta kontoautentiseringsuppgifterna avslöjas med sociala manipulationsmetoder eller nya och än så länge okända metoder och tekniker. ATA kan identifiera dessa typer av avslöjanden genom att analysera entitetens beteende och identifiera och varna vid avvikelser i de åtgärder som utförs av entiteten.

### <a name="lateral-movement"></a>Lateral förflyttning

När användare använder autentiseringsuppgifter som ger åtkomst till resurser som de ska ha åtkomst till använder ATA både maskininlärningsbaserad beteendeanalys samt identifiering av skadliga attacker och tekniker för att ge skydd mot lateral förflyttning.
Med hjälp av beteendeanalys och maskininlärning identifierar ATA onormal resursåtkomst, onormala enheter som används eller andra indikatorer som tyder på lateral förflyttning.
Dessutom kan ATA identifiera lateral förflyttning genom att upptäcka de tekniker som angripare använder för att utföra lateral förflyttning, t.ex.:

-   **Pass the ticket** <br></br>Vid pass the ticket-attacker stjäl angriparen en Kerberos-biljett från en dator och använder den för att få åtkomst till en annan dator genom att utge sig för att vara en entitet i nätverket.

-   **Pass the hash** <br></br>Vid pass the hash-attacker stjäl angriparen NTLM-hash för en entitet och använder den för att autentisera sig hos NTLM och utge sig för att vara den entiteten och få åtkomst till resurser i nätverket.

-   **Over-pass the hash**<br></br>Over-pass the hash är attacker där angriparen använder en stulen NTLM-hash för att autentisera sig hos Kerberos och få en giltig Kerberos TGT-biljett, som sedan används för att autentisera sig som en giltig användare och få åtkomst till resurser i nätverket.

-   **Onormalt beteende**<br></br>Lateral förflyttning är en teknik som angripare ofta använder för att gå mellan enheter och områden i offrets nätverk för att få åtkomst till autentiseringsuppgifter eller känslig information som är intressant för angriparen. ATA kan identifiera lateral förflyttning genom att analysera beteendet för användare, enheter och deras förhållande i företagsnätverket, och identifiera eventuella onormala åtkomstmönster som kan tyda på att en lateral förflyttning utförs av en angripare.

### <a name="privilege-escalation"></a>Eskalering av privilegier

ATA identifierar lyckade och testade attacker med eskalering av privilegier, där angripare försöker öka befintliga privilegier och använda dem flera gånger för att så småningom få fullständig kontroll över offrets miljö.
ATA möjliggör identifiering av eskalering av privilegier genom att kombinera beteendeanalys för att identifiera avvikande beteende samt identifiering av kända och skadliga attacker och tekniker som ofta används för att eskalera privilegier, t.ex.:

-   **MS14-068-kryphål (förfalskat PAC)**<br></br>Förfalskad PAC är attacker där angriparen placerar auktoriseringsdata i en giltig TGT-biljett i form av en förfalskad auktoriseringsrubrik som ger ytterligare behörighet som inte har beviljats av organisationen. I det här scenariot använder angripare tidigare avslöjade autentiseringsuppgifter, eller autentiseringsuppgifter som har inhämtats under åtgärder med lateral förflyttning.

-   **MS11-013-kryphål (Silver PAC)**<br></br>Attacker med MS11-013-kryphål utnyttjar en säkerhets för privilegier i Kerberos som gör det möjligt att förfalska vissa aspekter av en Kerberos-tjänstbiljett. En obehörig användare eller angripare som utnyttjar denna säkerhetsrisk kan hämta en token med högre behörighet på domänkontrollanten. I det här scenariot använder angripare tidigare avslöjade autentiseringsuppgifter, eller autentiseringsuppgifter som har inhämtats under åtgärder med lateral förflyttning.

-   **Onormal ändring av känsliga grupper**  <br></br>Som en del av behörighetseskaleringsfasen ändrar angripare grupper med höga privilegier för att få åtkomst till känsliga resurser. Nu identifierar ATA onormala ändringar i grupper med höga privilegier.

### <a name="domain-dominance"></a>Domändominans

ATA identifierar angripare som försöker eller lyckas uppnå fullständig kontroll eller dominans över offrets miljö genom att utföra identifiering via kända tekniker som används av angripare, till exempel:

-   **Skadlig Skeleton Key-kod**<br></br>Vid Skeleton Key-attacker installeras skadlig kod på domänkontrollanten som gör det möjligt för angripare att autentisera sig som valfri användare, samtidigt som behöriga användare kan logga in.

-   **Golden ticket**<br></br>Vid golden ticket-attacker stjäl en angripare KBTGT-autentiseringsuppgifterna, Kerberos Golden Ticket. Den biljetten gör det möjligt för angriparen att skapa en TGT-biljett offline, som används för att få åtkomst till resurser i nätverket.

-   **Fjärrkörning**<br></br>Angripare kan försöka få kontroll över nätverket genom att köra kod fjärrstyrt på domänkontrollanten.

- **Fjärrkörningsförsök – WMI-exekvering**<br></br>Angripare kan försöka få kontroll över nätverket genom att köra kod fjärrstyrt på domänkontrollanten. ATA identifierar fjärrkörning som utnyttjar WMI-metoder för att köra kod via en fjärranslutning.

-   **Skadliga replikeringsbegäranden** <br></br>I Active Directory-miljöer (AD) sker replikering regelbundet mellan domänkontrollanter. En angripare kan imitera en AD-replikeringsbegäran (ibland genom att utge sig för att vara domänkontrollant) vilket gör det möjligt för angriparen att hämta data som finns lagrad i AD, inklusive lösenordshashvärden, utan att använda mer påträngande tekniker som Volume Shadow Copy.


## <a name="whats-next"></a>Vad händer nu?

-   Mer information om hur ATA passar in i nätverket: [ATA-arkitektur](ata-architecture.md)

-   Komma igång med att distribuera ATA: [Installera ATA](install-ata-step1.md)

## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
