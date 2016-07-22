---
title: "Vanliga frågor och svar om ATA | Microsoft Advanced Threat Analytics"
description: "Visar en lista med vanliga frågor om ATA och tillhörande svar"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: bb6bc2bf0d0df3112ecfdb33c8e9d6e41f183145


---

# Vanliga frågor och svar om ATA
Den här artikeln innehåller en lista med vanliga frågor om ATA och ger insikt och svar.


## Hur licensieras ATA?
Licensieringsinformation finns i [Köpa Advanced Threat Analytics](https://www.microsoft.com/server-cloud/products/advanced-threat-analytics/Purchasing.aspx)


## Vad gör jag om ATA-gatewayen inte startar?
Titta på det senaste felet i den aktuella felloggen (där ATA är installerat under mappen "Loggar").
## Hur kan jag testa ATA?
Du kan simulera misstänkta aktiviteter som är ett test slutpunkt till slutpunkt på något av följande sätt:

1.  DNS-rekognosering med hjälp av Nslookup.exe
2.  Fjärrkörning med hjälp av psexec.exe


Detta måste fjärrköras mot domänkontrollanten som övervakas och inte från ATA-gatewayen.

## Hur kan jag bekräfta vidarebefordran av Windows-händelser?
Du kan köra följande från en kommandotolk i katalogen: **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## Fungerar ATA med krypterad trafik?
Krypterad trafik analyseras inte (till exempel: LDAPS, IPSEC ESP).
## Fungerar ATA med Kerberos Armoring?
Aktivering av Kerberos Armoring, som även kallas Flexible Authentication Secure Tunneling (FAST), stöds av ATA, med undantag för identifiering av ”over-pass the hash” som inte fungerar.
## Hur många ATA-gatewayer behöver jag?

Till att börja med rekommenderar vi att du använder ATA Lightweight Gateway på alla domänkontrollanter som kan hantera det. Information om att fastställa detta finns i [ATA Lightweight Gateway Sizing](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

Om alla domänkontrollanter kan omfattas av ATA Lightweight Gateway behövs ingen ATA Gateway.

Tänk på följande när du bestämmer hur många ATA-gatewayer du behöver för domänkontrollanter som inte omfattas av ATA Lightweight Gateway:

 - Den totala mängden trafik domänkontrollanterna producerar, samt nätverksarkitekturen (för att kunna konfigurera portspegling). Om du vill läsa mer om att avgöra hur mycket trafik som domänkontrollanterna producerar kan du se [Beräkning av trafik för domänkontrollanter](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation)
 - Driftbegränsningarna för portspegling avgör också hur många ATA-gatewayer du behöver för att stödja domänkontrollanterna, t.ex. per växel, per datacenter, per region – alla miljöer har egna överväganden. 

## Hur mycket lagringsutrymme måste jag ha för ATA?
För varje hel dag med i genomsnitt 1 000 paket/sek behöver du 0,3 GB lagring.<br /><br />Mer information om storlek för ATA Center finns i [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Varför anses vissa konton känsliga?
Detta inträffar när ett konto är medlem i vissa grupper som vi anser vara känsliga (t.ex. "Domänadministratörer").

Om du vill förstå varför ett konto är känsligt kan du granska dess gruppmedlemskap för att förstå vilka känsliga grupper det tillhör (den grupp det tillhör kan också vara känslig till följd av en annan grupp, så samma process bör utföras tills du hittar den känsliga grupp som har högst nivå).

## Hur övervakar jag en virtuell domänkontrollant med ATA?
De flesta virtuella domänkontrollanter kan omfattas av ATA Lightweight Gateway. Information för att fastställa om ATA Lightweight Gateway är lämpligt för din miljö finns i [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Om en virtuell domänkontrollant inte kan omfattas av ATA Lightweight Gateway kan du ha antingen en virtuell eller fysisk ATA Gateway enligt beskrivningen i [Konfigurera portspegling](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Det enklaste sättet är att ha en virtuell ATA-gateway på varje värd där det finns en virtuell domänkontrollant.<br />Om de virtuella domänkontrollanterna flyttas mellan olika värdar måste du göra följande:

-   När den virtuella domänkontrollanten flyttar till en annan värd ska ATA-gatewayen på den värden förkonfigureras för att ta emot trafiken från den virtuella domänkontrollant som precis har flyttats.
-   Se till att du kopplar den virtuella ATA-gatewayen till den virtuella domänkontrollanten, så att om den flyttas följer ATA-gatewayen med.
-   Det finns några virtuella växlar som kan skicka trafik mellan värdar.

## Hur säkerhetskopierar jag ATA?
Det finns två saker att säkerhetskopiera:

-   Trafik och händelser som lagras av ATA, som kan säkerhetskopieras med valfri metod för databassäkerhetskopiering som stöds. Mer information finns i [ATA-databashantering](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   Konfiguration av ATA, som lagras i databasen och säkerhetskopieras automatiskt varje timme. 

## Vad kan ATA identifiera?
ATA identifierar kända skadliga attacker och tekniker, säkerhetsproblem och risker.
En fullständig lista över ATA-identifieringar finns i [Vad är Microsoft Advanced Threat Analytics?](what-is-ata.md).

## Vilken typ av lagring behöver jag för ATA?
Vi rekommenderar snabb lagring (diskar med 7 200 RPM rekommenderas inte) som har diskåtkomst med låg latens (mindre än 10 ms). RAID-konfigurationen ska ha stöd för tung skrivbelastning (RAID-5/6 och tillhörande produkter rekommenderas inte).

## Hur många nätverkskort kräver ATA-gatewayen?
ATA-gatewayen måste ha minst två nätverkskort:<br>1. Ett nätverkskort för att ansluta till det interna nätverket och ATA Center<br>2. Ett nätverkskort som används för att avbilda domänkontrollantens nätverkstrafik via portspegling.<br>* Det här gäller inte för ATA Lightweight Gateway, som internt använder alla nätverkskort som domänkontrollanten använder.

## Vilken typ av integrering har ATA med SIEM?
ATA har en dubbelriktad integrering med SIEM enligt följande:

1. ATA kan konfigureras för att skicka en Syslog-avisering vid misstänkt aktivitet till valfri SIEM-server som använder CEF-formatet.
2. ATA kan konfigureras för att ta emot Syslog-meddelanden för varje Windows-händelse med ID 4776, från [dessa SIEM-servrar](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support).

## Kan ATA övervaka domänkontrollanter som är visualiserade på IaaS-lösningen?

Ja, du kan använda ATA Lightweight Gateway för att övervaka domänkontrollanter som finns i valfri IaaS-lösning.

## Är detta ett lokalt eller molnbaserat erbjudande?
Microsoft Advanced Threat Analytics är en lokal produkt.

## Kommer det här att vara en del av Azure Active Directory eller lokal Active Directory?
Den här lösningen är för närvarande ett fristående erbjudande, det är inte en del av Azure Active Directory eller lokal Active Directory.

## Måste man skriva sina egna regler och skapa en tröskel/baslinje?
Med Microsoft Advanced Threat Analytics behöver du inte skapa regler, trösklar eller baslinjer och sedan finjustera. ATA analyserar beteende hos användare, enheter och resurser, samt deras förhållande till varandra, och kan identifiera misstänkt beteende och kända attacker snabbt. Tre veckor efter distributionen börjar ATA att identifiera misstänkta aktiviteter baserat på beteende. ATA börjar dock identifiera kända skadliga attacker och säkerhetsproblem direkt efter distributionen.

## Kan Microsoft Advanced Threat Analytics identifiera onormalt beteende om det redan har skett ett intrång?
Ja, även om ATA installeras efter att ett intrång har skett kan ATA identifiera misstänkta aktiviteter hos hackaren. ATA tittar inte bara på användarens beteenden utan jämför också med andra användare på organisationens säkerhetskarta. Under den inledande analystiden identifieras angriparens beteende, om det är onormalt, som en ”avvikare” och ATA fortsätter att rapportera det onormala beteendet. Dessutom kan ATA identifiera en misstänkt aktivitet om hackaren försöker stjäla en annan användares autentiseringsuppgifter, t.ex. vid Pass-the-Ticket, eller försök att utföra en fjärrkörning av en av domänkontrollanterna.

## Använder detta endast trafik från Active Directory?
Förutom att analysera Active Directory-trafik med teknik för djup paketinspektion kan ATA också samla in relevanta händelser från SIEM (Security Information and Event Management) och skapa entitetsprofiler baserat på information från Active Directory Domain Services. ATA kan också samla in händelser från händelseloggarna om organisationen konfigurerar vidarebefordran av Windows-händelseloggar.

## Vad är portspegling?
Portspegling kallas även SPAN (Switched Port Analyzer) och är en metod för att övervaka nätverkstrafik. När portspegling är aktiverat skickar växeln en kopia av alla nätverkspaket som syns på en port (eller ett helt VLAN) till en annan port där paketet kan analyseras.

## Övervakar ATA endast domänanslutna enheter?
Nej. ATA övervakar alla enheter i nätverket som utför autentiserings- och auktoriseringsförfrågningar mot Active Directory, inklusive enheter som inte har Windows och mobila enheter.

## Övervakar ATA både datorkonton och användarkonton?
Ja. Eftersom datorkonton (samt eventuella andra entiteter) kan användas för att utföra skadliga aktiviteter övervakar ATA beteendet hos alla datorkonton och alla andra entiteter i miljön.

## ATA kan stödja flera domäner och flera skogar?
Vid allmän tillgänglighet kommer Microsoft Advanced Threat Analytics att ha stöd för flera domäner med samma skogsgräns. Själva skogen är den faktiska ”säkerhetsgränsen”, vilket innebär att stöd för flera domäner gör det möjligt för våra kunder att ha 100 % täckning för sina miljöer med ATA.

## Går det att se den övergripande hälsan för distributionen?
Ja, det går att se både den övergripande hälsan för distributionen och specifika problem som är relaterade till konfiguration, anslutning osv., och du får en avisering när de inträffar.


## Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO4-->


