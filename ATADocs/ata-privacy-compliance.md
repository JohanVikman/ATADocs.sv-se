---
title: Advanced Threat Analytics personuppgifter princip | Microsoft Docs
description: Innehåller länkar till information om hur du tar bort privat information och personliga data från ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 831fceafe3672d916d18801eb1273a62a81c84cd
ms.sourcegitcommit: f9400ae27d22607e4146dc9b8a0b9ba6f61fdd38
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/05/2018
ms.locfileid: "43743339"
---
*Gäller för: Advanced Threat Analytics version 1.9*

# <a name="ata-data-security-and-privacy"></a>ATA datasäkerhet och sekretess

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Söka efter och identifiera personliga data 

Alla data i ATA som rör entiteter är härledd från Active Directory (AD) som replikeras till ATA därifrån. När du söker efter personliga data, är den första plats bör du överväga att söka i AD. 

Använd sökfältet från ATA-Center för att visa identifierbar personlig data som lagras i databasen. Användare kan söka efter en viss användare eller enhet. Klicka på entiteten öppnas användaren eller enheten profilsida. Profilen som ger dig omfattande information om entiteten och dess historik relaterade nätverksaktivitet som härletts från AD. 

## <a name="updating-personal-data"></a>Uppdatera personliga data 

Personlig information om användare och entiteter i ATA härleds från användarens objekt i din organisation är AD. Därför återspeglas alla ändringar i användarprofilen i AD i ATA. 

## <a name="deleting-personal-data"></a>Ta bort personliga data 

Även om data i ATA replikeras och alltid uppdateras från AD, när en entitet tas bort i AD, underhålls entitetsdata i ATA för säkerhetsundersökning. 

Följ den här proceduren om du vill ta bort användarrelaterade data från ATA-databasen permanent: 

1. [Ladda ned](https://aka.ms/ata-gdpr-script) MongoDB-skript (gdpr.js).  

2. Kopiera skriptet till ATA Center-datorn och kör följande kommando från ATA Center-datorn: 

Använd ATA GDPR databasen skript för att ta bort entiteter och ta bort entiteten aktivitetsdata, enligt beskrivningen i följande avsnitt.

### <a name="delete-entities"></a>Ta bort entiteter

Den här åtgärden tar permanent bort en entitet från ATA-databasen. Om du vill köra det här kommandot ger kommandonamnet `deleteAccount`, och `SamName`, `UpnName` eller `GUID` på datorn eller användarnamn som du vill ta bort. Exempel: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

Kör det helt tar bort entiteten med UPN admin1@contoso.com från databasen tillsammans med alla aktiviteter och säkerhetsaviseringar som är associerade med entiteten. 

### <a name="delete-entity-activity-data"></a>Ta bort entitet aktivitetsdata

Den här åtgärden tar permanent bort en entitet aktiviteter data från ATA-databasen. Alla entiteter utgör oförändrade men aktiviteter och säkerhetsaviseringar som är relaterat till dem för den angivna tidsramen tas bort. 

Om du vill köra det här kommandot ger kommandonamnet `deleteOldData`, och antalet dagars data som du vill behålla i databasen. 

Exempel: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Det här skriptet tar bort alla data för alla enhetsaktiviteter och säkerhetsaviseringar från databasen som är äldre än 30 dagar. Du behåller endast de senaste 30 dagarna data.

## <a name="exporting-personal-data"></a>Exportera personliga data 

Eftersom de data som rör entiteter i ATA hämtas från AD, lagras endast en delmängd av dessa data i ATA-databasen. Därför bör du exportera entitet-relaterade data från AD. 

ATA kan du exportera till Excel alla säkerhetsrelaterad information, som kan innehålla personuppgifter. 

 
## <a name="opt-out-of-system-generated-logs"></a>Avstår från systemgenererade loggar 

ATA samlar in anonymiserade systemgenererade loggar om varje distribution och överför dessa data via HTTPS till Microsoft-servrar. Dessa data används av Microsoft för att förbättra kommande versioner av ATA. 

Mer information finns i [hantera systemgenererade loggar](manage-telemetry-settings.md).

Inaktivera datainsamling:

1. Logga in på ATA-konsolen, klicka på de tre punkterna i verktygsfältet och välj **Om**. 
2. Avmarkera kryssrutan **Skicka användningsinformation till oss för att förbättra kundupplevelsen i framtiden**. 

## <a name="additional-resources"></a>Ytterligare resurser

- Läs om hur ATA förtroende och efterlevnad i [Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) och [Dataskyddsförordningen för Microsoft 365 Enterprise plats](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
