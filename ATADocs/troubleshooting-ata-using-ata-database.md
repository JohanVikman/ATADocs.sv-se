---
title: Felsök Advanced Threat Analytics med hjälp av databasen | Microsoft Docs
description: Beskriver hur du kan använda ATA-databasen som hjälp för att felsöka problem
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7bd17d6ac340f1acf0166aadbfcbb7f3ef164fc3
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009446"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Felsöka ATA med ATA-databasen
ATA använder MongoDB som databas.
Du kan interagera med databasen med hjälp av standardkommandoraden eller ett gränssnittsverktyg för att utföra avancerade åtgärder och felsökning.

## <a name="interacting-with-the-database"></a>Interagera med databasen
Standardsättet, som är det mest grundläggande sättet, för att ställa frågor till databasen är att använda Mongo shell:

1.  Öppna ett kommandoradsfönster och ändra sökvägen till MongoDB bin-mappen. Standardsökvägen är: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Kör: `mongo.exe ATA`. Tänk på att skriva ATA med versaler.

> [!div class="mx-tableFixed"]
|Gör så här...|Syntax|Obs!|
|-------------|----------|---------|
|Kontrollera om det finns samlingar i databasen.|`show collections`|Det kan användas som ett test för slutpunkt till slutpunkt för att se att trafiken skrivs till databasen och att händelsen 4776 tas emot av ATA.|
|Hämta information om en användare/dator/grupp (UniqueEntity), t.ex. användar-ID.|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
|Hitta Kerberos-autentiseringstrafik som kommer från en viss dator en viss dag.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Om du vill hämta &lt;ID för källdatorn&gt; kan du fråga UniqueEntity-samlingarna på det sätt som visas i exemplet.<br /><br />Varje aktivitetstyp, till exempel Kerberos-autentiseringar, har en egen samling per UTC-datum.|
|Hitta NTLM-trafik från en viss dator som är relaterad till ett visst konto en viss dag.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Om du vill hämta &lt;ID för källdatorn&gt; och &lt;ID för kontot&gt; kan du fråga UniqueEntity-samlingarna på det sätt som visas i exemplet.<br /><br />Varje aktivitetstyp, till exempel NTLM-autentiseringar, har en egen samling per UTC-datum.|
|Gör avancerade konfigurationsändringar. I det här exemplet ändra sändningsköstorleken för alla ATA-gatewayer till 10 000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

I följande exempel visar exempelkod med den syntax som anges ovan. Om du undersöker en misstänkt aktivitet som inträffade 20/10/2015 och vill veta mer om de NTLM-aktiviteter som "John Berg" har utfört den dagen:<br /><br />Hitta först ID för "John Berg"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Anteckna ID som anges med värdet för `_id` anta att ID som är `123bdd24-b269-h6e1-9c72-7737as875351`<br>Sök sedan efter samlingen med det närmaste datum som infaller före datumet du letar efter, i exempel 20/10/2015.<br>Sök sedan efter NTLM-aktiviteter för John Bergs konto: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
