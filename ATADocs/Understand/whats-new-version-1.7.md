---
title: Nyheter i ATA version 1.7 | Microsoft ATA
description: "Visar en lista över nyheter i ATA version 1.7 tillsammans med kända problem"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Nyheter i ATA version 1.7
Dessa versionsanmärkningar innehåller information om kända problem i denna version av Advanced Threat Analytics.

## Vad är nytt i ATA 1.7-uppdateringen?
Uppdateringen för ATA 1.7 ger förbättringar inom följande områden:

-   Nya och uppdaterade identifieringar

-   Rollbaserad åtkomstkontroll

-   Stöd för Windows Server 2016 och Windows Server Core

-   Förbättringar av användarupplevelse


### Nya och uppdaterade identifieringar


- **Rekognosering med uppräkning av katalogtjänster** Som en del av rekognoseringsfasen samlar angripare in information om enheter i nätverket med olika metoder. Uppräkning av katalogtjänster med SAM-R-protokollet gör det möjligt för angripare att erhålla en lista över användare och grupper i en domän och förstå interaktionen mellan olika entiteter. 

- **Förbättringar av Pass-the-Hash** För att förbättra Pass-the-Hash-identifiering, har vi lagt till flera beteendemodeller för autentiseringsmönster för entiteter. Dessa modeller gör det möjligt för ATA att korrelera entitetsbeteende med misstänkta NTLM-autentiseringar och särskilja verkliga Pass-the-Hash-attacker från beteenden vid falskpositiva scenarier.

- **Förbättringar av Pass-the-Ticket** För att kunna identifiera avancerade attacker i allmänhet och Pass-the-Ticket i synnerhet, måste sambandet mellan en IP-adress och datorkontot vara korrekt. Detta är en utmaning i miljöer där IP-adresser ändras snabbt i utformning (till exempel Wi-Fi-nätverk och flera virtuella datorer som delar samma värd). För att lösa denna utmaning och förbättra identifiering av Pass-the-Ticket, har ATA:s mekanism Network Name Resolution (NNR) förbättrats avsevärt för att minska falskpositiva resultat.

- **Förbättringar för onormalt beteende** I ATA 1.7 har NTLM-autentiseringsdata lagts till som en datakälla för identifieringar av onormalt beteende, vilket ger algoritmer med bredare täckning för entitetsbeteende i nätverket. 

- **Förbättringar av onormal protokollimplementering** ATA identifierar nu ovanlig protokollimplementering i Kerberos-protokollet, tillsammans med ytterligare avvikelser i NTLM-protokollet. Dessa nya avvikelser för Kerberos används särskilt ofta i Over-pass-the-Hash-attacker.


### Infrastruktur

- **Rollbaserad åtkomstkontroll** Förmåga för rollbaserad åtkomstkontroll (RBAC). ATA 1.7 innehåller tre roller: ATA-administratör, ATA-analytiker och ATA-chefer.

- **Stöd för Windows Server 2016 och Windows Server Core** ATA 1.7 stöder distribution av Lightweight Gateways på domänkontrollanter som kör Server Core för Windows Server 2012 och Server Core för Windows Server 2012 R2. Den här versionen stöder dessutom Windows Server 2016 både för komponenterna ATA Center och ATA Gateway.

### Användarens upplevelse
- **Konfigurationsupplevelse** I den här versionen har konfigurationsupplevelsen för ATA gjorts om för en bättre användarupplevelse och bättre stöd för miljöer med flera ATA-gatewayar. Den här versionen beskriver även ATA Gateways uppdateringssida för enklare och bättre hantering av automatiska uppdateringar för olika gatewayar.

## Kända problem
Följande kända problem finns i den här versionen.

### Det gick inte att uppdatera gatewayen automatiskt
**Problem:** I miljöer med långsamma WAN-länkar, kan uppdateringen av ATA Gateway nå tidsgränsen för uppdatering (100 sekunder) och kan inte slutföras.
I ATA-konsolen har ATA Gateway statusen "Uppdatera (hämta paketet)" under en lång tid och misslyckas slutligen.

**Lösning:** Undvik det här problemet, ladda ned det senaste ATA Gateway-paketet från ATA-konsolen och uppdatera ATA Gateway manuellt.

### Migreringsfel vid uppdatering från ATA 1.6
Vid uppdatering till ATA 1.7 kan uppdateringen misslyckas med följande felkod *0x80070643*:

![Fel vid uppdatering av ATA till 1.7](media/ata-update-error.png)

Granska distributionsloggen för att ta reda på orsaken till felet. Distributionsloggen finns på följande plats: **% temp %\..\Microsoft Advanced Thread Analytics Center_{date_stamp}_MsiPackage.log**. 

I tabellen nedan visas olika fel du kan söka efter och det motsvarande Mongo-skriptet du kan använda för att åtgärda felet. Se exemplen i tabellen nedan som visar hur du kör Mongo-skriptet:

| Fel i loggfilen för distribution                                                                                                                  | Mongo-skript                                                                                                                                                                         |
|---|---|
| System.FormatException: Storleken {size} är större än MaxDocumentSize 16777216 <br>Längre ned i filen:<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: Undantag av typen ”System.OutOfMemoryException” uppstod<br>Längre ned i filen:<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords(IMongoCollection`1 suspiciousActivityCollection, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Felaktig längd<br>Längre ned i filen:<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Följ anvisningarna nedan för att köra det aktuella skriptet. 

1.  Bläddra till följande plats från en upphöjd kommandotolk: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Typ – **Mongo.exe ATA**   (*OBS*: ATA måste anges med versaler.)
3.  Klistra in det skript som matchar felet i loggen för distribution från tabellen ovan.

![ATA Mongo-skript](media/ATA-mongoDB-script.png)

Du bör nu kunna starta om uppgraderingen.

### ATA rapporterar ett stort antal misstänkta aktiviteter med ”*Reconnaissance using directory services enumerations*” (Rekognoscering med katalogtjänstuppräkning):
 
Detta beror sannolikt på att ett skanningsverktyg för nätverk körs på alla (eller många) klientdatorer i organisationen. Om du ser det här problemet:

1. Skicka ett e-postmeddelande till ATAEval på Microsoft.com med informationen om du kan identifiera orsaken eller det specifika program som körs på klientdatorerna.
2. Använd följande mongo-skript för att avvisa dessa händelser (se ovan för hur du kör mongo-skriptet):

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### ATA skickar meddelanden för avvisade misstänkta aktiviteter:
Om meddelanden har konfigurerats kan ATA fortsätta skicka meddelanden (e-post, syslog och händelseloggar) om avvisade misstänkta aktiviteter.
Det finns ingen lösning för det här problemet just nu. 

### ATA Gateway kan inte registrera med ATA Center om TLS 1.0 och TLS 1.1 är inaktiverade:
Om TLS 1.0 och TLS 1.1 är inaktiverade på ATA Gateway (eller Lightweight Gateway) kan gatewayen misslyckas med att registrera sig på ATA Center

### Automatisk certifikatförnyelse för de certifikat som används av ATA stöds inte
Användningen av automatisk certifikatförnyelse kan orsaka att ATA slutar att fungera när certifikatet förnyas automatiskt. 


## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.7 – migreringsguide](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->


