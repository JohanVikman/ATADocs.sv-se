---
title: Advanced Threat Analytics personuppgifter princip | Microsoft Docs
description: Innehåller länkar till information om hur du tar bort personlig information och dina personliga data från ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: cf08f2d46eaa939f414d1e3793446384cd22100b
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*

# <a name="ata-data-security"></a>Datasäkerhet i ATA 

Information om ATA förtroende och kompatibilitet finns i [Service förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) och [webbplatsen Microsoft 365 Enterprise BNPR efterföljande](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

## <a name="searching-for-and-identifying-personal-data"></a>Söker efter och identifiera personliga data 

Alla data i ATA som är kopplat till entiteter är härledd från Active Directory (AD) och replikeras till ATA därifrån. När du söker efter personliga data, är den första plats bör du söker AD. 

Använd sökfältet från ATA Center, för att visa identifierbar personlig information som lagras i databasen. Användare kan söka efter en specifik användare eller enhet. När du klickar på entiteten öppnas användaren eller enheten profilsida. Profilen ger omfattande information om entiteten, dess historik och relaterade nätverksaktivitet som härletts från AD. 

## <a name="updating-personal-data"></a>Uppdaterar personliga data 

Personliga data om användare och enheter i ATA härleds från användarens objekt i din organisation har AD. Därmed visas alla ändringar i användarprofilen i AD i ATA. 

## <a name="deleting-personal-data"></a>Ta bort personliga data 

> [!NOTE]
> Om du vill visa eller ta bort personliga data, läser du riktlinjerna för Microsofts i den [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) och i avsnittet [BNPR på webbplatsen Microsoft 365 Enterprise efterföljande] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Om du letar efter allmän information om BNPR finns i [BNPR avsnitt av tjänsten förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Även om data i ATA replikeras och alltid uppdateras från AD, när en enhet tas bort i AD upprätthålls entitetsdata i ATA för tillämpning av säkerhet undersökning. 

Så här om du vill ta bort användarrelaterade data permanent från ATA-databasen: 

1. [Hämta](https://aka.ms/ata-gdpr-script) MongoDB-skript (gdpr.js).  

2. Kopiera skriptet till ATA Center-datorn och kör följande kommando från ATA Center-datorn: 

Använda ATA GDPR databasen skript för att ta bort entiteter och ta bort entiteten aktivitetsdata, enligt beskrivningen i följande avsnitt.

### <a name="delete-entities"></a>Ta bort enheter

Den här åtgärden tar permanent bort en entitet från ATA-databasen. Om du vill köra det här kommandot ger kommandonamnet `deleteAccount`, och `SamName`, `UpnName` eller `GUID` av dator- eller användarnamn som du vill ta bort. Exempel: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteAccount,admin1@contoso.com;” GDPR.js `

Kör detta helt tar bort enheten med UPN admin1@contoso.com från databasen tillsammans med alla aktiviteter och säkerhetsaviseringar som associeras med entiteten. 

### <a name="delete-entity-activity-data"></a>Ta bort entiteten aktivitetsdata

Den här åtgärden tar permanent bort en entitet aktiviteter data från ATA-databasen. Alla enheter kommer är oförändrade men aktiviteter och säkerhetsaviseringar som rör dem för angivet tidsintervall tas bort. 

Om du vill köra det här kommandot ger kommandonamnet `deleteOldData`, och antalet dagars data som du vill ha kvar i databasen. 

Exempel: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteOldData,30;” GDPR.js`

Det här skriptet tar bort alla data för alla aktiviteter som entiteten och säkerhetsaviseringar från databasen som är äldre än 30 dagar. Du behåller endast under de senaste 30 dagarna av data.

## <a name="exporting-personal-data"></a>Exportera personliga data 

> [!NOTE]
> Om du vill visa eller ta bort personliga data, läser du riktlinjerna för Microsofts i den [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) och i avsnittet [BNPR på webbplatsen Microsoft 365 Enterprise efterföljande] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Om du letar efter allmän information om BNPR finns i [BNPR avsnitt av tjänsten förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Eftersom de data som rör entiteter i ATA är härledd från AD, lagras bara en delmängd av dessa data i ATA-databasen. Därför ska du exportera entitet-relaterade data från AD. 

ATA kan du exportera till Excel alla säkerhetsrelaterad information som kan innehålla personuppgifter. 

 
## <a name="opt-out-of-system-generated-logs"></a>CEIP systemgenererade loggar 

> [!NOTE]
> Om du vill visa eller ta bort personliga data, läser du riktlinjerna för Microsofts i den [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) och i avsnittet [BNPR på webbplatsen Microsoft 365 Enterprise efterföljande] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Om du letar efter allmän information om BNPR finns i [BNPR avsnitt av tjänsten förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

ATA samlar in anonymiserade systemgenererade loggar för varje distribution och överför dessa data via HTTPS till Microsoft-servrar. Dessa data används av Microsoft för att förbättra kommande versioner av ATA. 

Mer information finns i [hantera systemgenererade loggar](manage-telemetry-settings.md).

Inaktivera datainsamling:

1. Logga in på ATA-konsolen, klicka på de tre punkterna i verktygsfältet och välj **Om**. 
2. Avmarkera kryssrutan **Skicka användningsinformation till oss för att förbättra kundupplevelsen i framtiden**. 

 

 

 

## <a name="additional-resources"></a>Ytterligare resurser

[Microsoft Security Channel 9 sida](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Gruppresurser

[ATA-bloggen](https://aka.ms/ATABlog)
[ATA community](https://aka.ms/ATACommunity)
[ge feedback om ATA](https://aka.ms/ATAUserVoice)
