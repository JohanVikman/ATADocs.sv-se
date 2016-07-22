---
title: "Vad är Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics"
description: "Förklarar vad Microsoft Advanced Threat Analytics (ATA) är och vilka typer av misstänkta aktiviteter det kan upptäcka"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 4831e7a773b69a87bbcd505a8116230f14611250


---


## Vad är ATA?
Microsoft Advanced Threat Analytics (ATA) är en ledande lösning på marknaden för analys av användar- och entitetsbeteende, som hjälper IT-säkerhetsproffs att skydda sin organisation från avancerade riktade attacker (APT) och insiderhot. Genom att automatiskt analysera, lära in och identifiera normalt och onormalt enhetsbeteende (användare, enheter och resurser) med avancerad teknik för maskininlärning hjälper ATA till att identifiera kända skadliga attacker och tekniker, säkerhetsproblem och risker. Med hjälp av förstklassiga kunskaper och insikter från säkerhetsforskare har den här nyskapande tekniken utformats för att hjälpa företag att fokusera på att identifiera säkerhetsintrång innan de orsakar skada.

## Vad gör ATA?
ATA identifierar:

  - Avancerade permanenta hot (APT) tidigt i attackkedjan, innan de kan orsaka skada

  - Insiderhot

ATA hjälper dig att skilja verkliga misstänkta aktiviteter från störningar, för att kunna fokusera på det som är viktigt.

ATA:s identifieringsmotor använder maskininlärning, djup paketinspektion med entitetssammanhang, logganalys och information från Active Directory (AD) för att analysera användar- och entitetsbeteende.

ATA utför djupanalys av organisationens trafik och använder maskininlärning för att skapa en karta över hur normal aktivitet, trafik och användning ser ut i organisationen. ATA söker sedan efter och meddelar dig när onormala händelser sker. Det här uppnås genom att köra Microsofts teknik för djup paketinspektion (DPI) med entitetssammanhang för att få en djupare nivå av trafiktolkning, som gör det möjligt för ATA att analysera alla nivåer av nätverkstrafiken.

ATA samlar även in relevanta händelser från SIEM-system och domänkontrollanter. Efter analys skapar ATA en dynamisk och kontinuerligt uppdaterad vy över alla användare, enheter och resurser i en organisation. Med hjälp av denna omfattande vy kan ATA identifiera kända skadliga attacker som pass-the-hash, pass-the-ticket, rekognoseringsattacker med mera, samt söka efter eventuella avvikelser i entiteternas beteende i nätverket.

När en misstänkt aktivitet har identifierats genererar ATA en varning och antalet falska positiva identifieringar som visas minimeras med hjälp av avancerade algoritmer för aggregering och sammanhangsverifiering.



## Vilka hot letar ATA efter?

ATA ger identifiering för följande olika faser i en avancerad attack: rekognosering, avslöjade autentiseringsuppgifter, lateral förflyttning, eskalering av privilegier, domändominans med mera. Dessa identifieringar är avsedda att identifiera avancerade attacker och insiderhot innan de skadar organisationen.

Identifieringen av varje fas ger flera misstänkta aktiviteter som är relevanta för fasen i fråga, där varje misstänkt aktivitet motsvarar olika varianter av möjliga attacker.

### Rekognosering
ATA identifierar rekognosering på flera sätt. Dessa identifieringar omfattar:

-   **Rekognosering med kontouppräkning**<br>Identifierar försök från angripare som använder Kerberos-protokollet för att upptäcka om en användare finns, även om aktiviteten inte har loggats som en händelse på domänkontrollanten.
-   **Nettosessionsuppräkning**<br>
Som en del av rekognoseringsfasen kan angripare fråga DC om alla aktiva SMB-sessioner på servern och ge dem åtkomst till alla användare och IP-adresser som är kopplade till dessa SMB-sessioner. SMB-sessionsuppräkningen kan användas av angripare för rikta in sig på känsliga konton, vilket hjälper dem att flyttas i sidled över nätverket.
-   **Rekognosering med DNS**<br>
DNS-information i målnätverk är ofta mycket användbar rekognoseringsinformation. DNS-informationen innehåller en lista över alla servrar och ofta alla klienter och mappningen till deras IP-adresser. Genom att visa DNS-information kan angriparna få en detaljerad vy av dessa enheter i miljön, vilket gör det möjligt för angripare att fokusera sitt arbete på de relevanta enheterna för kampanjen.

### Avslöjade autentiseringsuppgifter

I syfte att ge identifiering av avslöjade autentiseringsuppgifter använder ATA både maskininlärningsbaserad analys samt kända skadliga attacker och teknikidentifiering.

Genom att använda beteendeanalys och maskininlärning kan ATA identifiera misstänkta aktiviteter, t.ex. avvikande inloggningar, onormal resursåtkomst och onormal arbetstid, vilket kan tyda på avslöjade autentiseringsuppgifter.
I syfte att skydda mot avslöjade autentiseringsuppgifter identifierar ATA följande kända skadliga attacker och tekniker:

 - **Brute force** <br>Vid brute force-attacker försöker angripare gissa sig till autentiseringsuppgifter genom att prova flera användare och koppla ihop dem med flera lösenordsförsök. Angriparna använder ofta komplexa algoritmer eller ordböcker för att prova så många värden som ett system tillåter.

- **Känsligt konto exponerat i klartextautentisering**<br>
Om ett konto med högprivilegierade autentiseringsuppgifter skickas som klartext varnar ATA dig så att du kan uppdatera datorkonfigurationen.

- **Tjänsten exponerar konton i klartextautentisering** <br>
Om en tjänst på en dator skickar flera kontoautentiseringsuppgifter som klartext varnar ATA dig så att du kan uppdatera tjänstekonfigurationen.

- **Misstänkt aktivitet för Honung Token-konto**<br>
Honey Token-konton är falska konton som skapas för att fånga, identifiera och spåra skadliga aktiviteter som försöker använda dessa falska konton. ATA varnar dig om alla aktiviteter för dessa Honey Token-konton.
-   **Onormal protokollimplementering**<br>
Autentiseringsbegäranden (Kerberos eller NTLM) utförs vanligtvis med en normal uppsättning metoder och protokoll. För att kunna autentisera måste dock begäran uppfylla en specifik kravuppsättning. Angripare kan implementera dessa protokoll med mindre avvikelser från den normala implementeringen i miljön. Dessa avvikelser kan tyda på att det finns en angripare som försöker utnyttja eller som har lyckats utnyttja avslöjade autentiseringsuppgifter.
-   **Skadlig privat informationsbegäran för dataskydd**<br>
API för dataskydd (DPAPI) är en lösenordsbaserad dataskyddstjänst. Den här skyddstjänsten används av olika program som lagrar användarens hemligheter, t.ex. webbplatslösenord och autentiseringsuppgifter för filresurser. I syfte att ge stöd för scenarier med förlorat lösenord kan användare kryptera data med hjälp av en återställningsnyckel som inte omfattar lösenordet. I en domänmiljö kan angripare stjäla återställningsnyckeln fjärranslutet och använda den för att dekryptera skyddade data i alla domänanslutna datorer.
-   **Onormalt beteende**<br>
Vid insiderhot och avancerade attacker kan ofta kontoautentiseringsuppgifterna avslöjas med sociala manipulationsmetoder eller nya och än så länge okända metoder och tekniker. ATA kan identifiera dessa typer av avslöjanden genom att analysera entitetens beteende och identifiera och varna vid avvikelser i de åtgärder som utförs av entiteten.

### Lateral förflyttning
När användare använder autentiseringsuppgifter som ger åtkomst till resurser som de ska ha åtkomst till använder ATA både maskininlärningsbaserad beteendeanalys samt identifiering av skadliga attacker och tekniker för att ge skydd mot lateral förflyttning.

Med hjälp av beteendeanalys och maskininlärning identifierar ATA onormal resursåtkomst, onormala enheter som används eller andra indikatorer som tyder på lateral förflyttning.

Dessutom kan ATA identifiera lateral förflyttning genom att upptäcka de tekniker som angripare använder för att utföra lateral förflyttning, t.ex.:

- **Pass the Ticket** <br>
Vid pass the ticket-attacker stjäl angriparen en Kerberos-biljett från en dator och använder den för att få åtkomst till en annan dator genom att utge sig för att vara en entitet i nätverket.
- **Pass the hash** <br>
Vid pass the hash-attacker stjäl angriparen NTLM-hash för en entitet och använder den för att autentisera sig hos NTLM och utge sig för att vara den entiteten och få åtkomst till resurser i nätverket.
- **Over-pass the hash**<br>
Over-pass the hash är attacker där angriparen använder en stulen NTLM-hash för att autentisera sig hos Kerberos och få en giltig Kerberos TGT-biljett, som sedan används för att autentisera sig som en giltig användare och få åtkomst till resurser i nätverket.
-   **Onormalt beteende**<br>
Lateral förflyttning är en teknik som angripare ofta använder för att gå mellan enheter och områden i offrets nätverk för att få åtkomst till autentiseringsuppgifter eller känslig information som är intressant för angriparen. ATA kan identifiera lateral förflyttning genom att analysera beteendet för användare, enheter och deras förhållande i företagsnätverket, och identifiera eventuella onormala åtkomstmönster som kan tyda på att en lateral förflyttning utförs av en angripare.

### Eskalering av privilegier
ATA identifierar lyckade och testade attacker med eskalering av privilegier, där angripare försöker öka befintliga privilegier och använda dem flera gånger för att så småningom få fullständig kontroll över offrets miljö. 

ATA möjliggör identifiering av eskalering av privilegier genom att kombinera beteendeanalys för att identifiera avvikande beteende samt identifiering av kända och skadliga attacker och tekniker som ofta används för att eskalera privilegier, t.ex.:

- **MS14-068-kryphål (förfalskad PAC)**<br>
Förfalskad PAC är attacker där angriparen placerar auktoriseringsdata i en giltig TGT-biljett i form av en förfalskad auktoriseringsrubrik som ger ytterligare behörighet som inte har beviljats av organisationen. I det här scenariot använder angripare tidigare avslöjade autentiseringsuppgifter, eller autentiseringsuppgifter som har inhämtats under åtgärder med lateral förflyttning.
- **MS11-013-kryphål (silver-PAC)**<br>
Attacker med MS11-013-kryphål utnyttjar en säkerhets för privilegier i Kerberos som gör det möjligt att förfalska vissa aspekter av en Kerberos-tjänstbiljett. En obehörig användare eller angripare som utnyttjar denna säkerhetsrisk kan hämta en token med högre behörighet på domänkontrollanten. I det här scenariot använder angripare tidigare avslöjade autentiseringsuppgifter, eller autentiseringsuppgifter som har inhämtats under åtgärder med lateral förflyttning.

### Domändominans
ATA identifierar angripare som försöker eller lyckas uppnå fullständig kontroll eller dominans över offrets miljö genom att utföra identifiering via kända tekniker som används av angripare, till exempel:

- **Skadlig Skeleton Key-kod**<br>
Vid Skeleton Key-attacker installeras skadlig kod på domänkontrollanten som gör det möjligt för angripare att autentisera sig som valfri användare, samtidigt som behöriga användare kan logga in.
- **Golden ticket**<br>
Vid golden ticket-attacker stjäl en angripare KBTGT-autentiseringsuppgifterna, Kerberos Golden Ticket. Den biljetten gör det möjligt för angriparen att skapa en TGT-biljett offline, som används för att få åtkomst till resurser i nätverket.
- **Fjärrkörning**<br>
Angripare kan försöka få kontroll över nätverket genom att köra kod fjärrstyrt på domänkontrollanten.
-   **Skadliga replikeringsbegäranden** I Active Directory-miljöer (AD) sker replikering regelbundet mellan domänkontrollanter. En angripare kan imitera en AD-replikeringsbegäran (ibland genom att utge sig för att vara domänkontrollant) vilket gör det möjligt för angriparen att hämta data som finns lagrad i AD, inklusive lösenordshashvärden, utan att använda mer påträngande tekniker som Volume Shadow Copy.

## Vad händer nu?

-   Mer information om hur ATA passar in i nätverket: [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture)

-   Komma igång med att distribuera ATA: [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata)

## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


