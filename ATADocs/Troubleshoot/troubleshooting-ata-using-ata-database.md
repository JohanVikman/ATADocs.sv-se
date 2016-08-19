---
title: "Felsöka ATA med ATA-databasen | Microsoft ATA"
description: "Beskriver hur du kan använda ATA-databasen som hjälp för att felsöka problem"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: c86b6dc880238e262f696e88c54bc1bc7e01a1db


---

# Felsöka ATA med ATA-databasen
ATA använder MongoDB som databas.
Du kan interagera med databasen med hjälp av standardkommandoraden eller ett gränssnittsverktyg för att utföra avancerade åtgärder och felsökning.

## Interagera med databasen
Standardsättet, som är det mest grundläggande sättet, för att ställa frågor till databasen är att använda Mongo shell:

1.  Öppna ett kommandoradsfönster och ändra sökvägen till MongoDB Bin-mappen. Standardsökvägen är: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Kör: `mongo.exe ATA`. Tänk på att skriva ATA med versaler.

|Gör så här...|Syntax|Anteckningar|
|-------------|----------|---------|
|Kontrollera om det finns samlingar i databasen.|`show collections`|Det kan användas som ett test för slutpunkt till slutpunkt för att se att trafiken skrivs till databasen och att händelsen 4776 tas emot av ATA.|
|Hämta information om en användare/dator/grupp (UniqueEntity), t.ex. användar-ID.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Hitta Kerberos-autentiseringstrafik som kommer från en viss dator en viss dag.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Om du vill hämta &lt;ID för källdatorn&gt; kan du fråga UniqueEntity-samlingarna på det sätt som visas i exemplet.<br /><br />Varje aktivitetstyp, till exempel Kerberos-autentiseringar, har en egen samling per UTC-datum.|
|Hitta NTLM-trafik från en viss dator som är relaterad till ett visst konto en viss dag.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Om du vill hämta &lt;ID för källdatorn&gt; och &lt;ID för kontot&gt; kan du fråga UniqueEntity-samlingarna på det sätt som visas i exemplet.<br /><br />Varje aktivitetstyp, till exempel NTLM-autentiseringar, har en egen samling per UTC-datum.|
|Sök efter avancerade egenskaper, till exempel aktiva datum för ett konto. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Om du vill hämta &lt;ID för kontot&gt; kan du fråga UniqueEntity-samlingarna på det sätt som visas i exemplet.<br>Egenskapsnamnet som visar de datum då kontot har varit aktivt heter: "ActiveDates". <br>
Du kanske vill veta om ett konto har minst 21 dagars aktivitet för att maskininlärningsalgoritmen för onormalt beteende ska kunna köras på den.|
|Gör avancerade konfigurationsändringar. I det här exemplet ändrar vi sändningsköstorleken för alla ATA-gatewayer till 10 000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Följande exempel visar exempelkod med den syntax som anges ovan. Om du undersöker en misstänkt aktivitet som inträffade 20/10/2015 och vill veta mer om de NTLM-aktiviteter som "John Berg" har utfört den dagen:<br /><br />Hitta först ID för "John Berg"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Anteckna personens ID som anges med värdet "`_id`". I vårt exempel antar vi att ID är "`123bdd24-b269-h6e1-9c72-7737as875351`"<br>Sök sedan efter den samling som har det datum som är närmast före datumet du letar efter, i vårt exempel 20/10/2015.<br>Sök sedan efter NTLM-aktiviteter för John Bergs konto: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## ATA-konfigurationsfil
Konfigurationen av ATA lagras i samlingen "SystemProfile" i databasen.
Den här samlingen säkerhetskopieras varje timme av ATA Center-tjänsten till en fil som heter: "SystemProfile.json". Den finns i en undermapp som heter "Backup". På standardplatsen för ATA-installation finns den här:  **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**. 

**Obs**! Vi rekommenderar att du säkerhetskopierar den här filen någonstans när du gör större ändringar av ATA.

Det går att återställa alla inställningar genom att köra följande kommando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


