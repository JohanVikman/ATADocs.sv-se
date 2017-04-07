---
title: Nyheter i ATA version 1.7 | Microsoft Docs
description: "Visar en lista över nyheter i ATA version 1.7 tillsammans med kända problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: b9ba013c76c785290649037c8a01af1cd2feced5
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
# <a name="whats-new-in-ata-version-17"></a>Nyheter i ATA version 1.7
Dessa versionsanmärkningar innehåller information om kända problem i denna version av Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Vad är nytt i ATA 1.7-uppdateringen?
Uppdateringen för ATA 1.7 ger förbättringar inom följande områden:

-   Nya och uppdaterade identifieringar

-   Rollbaserad åtkomstkontroll

-   Stöd för Windows Server 2016 och Windows Server 2016 Core

-   Förbättringar av användarupplevelse

-   Mindre ändringar


### <a name="new--updated-detections"></a>Nya och uppdaterade identifieringar


- **Rekognosering med uppräkning av katalogtjänster** Som en del av rekognoseringsfasen samlar angripare in information om enheter i nätverket med olika metoder. Uppräkning av katalogtjänster med SAM-R-protokollet gör det möjligt för angripare att erhålla en lista över användare och grupper i en domän och förstå interaktionen mellan olika entiteter. 

- **Förbättringar av Pass-the-Hash** För att förbättra Pass-the-Hash-identifiering, har vi lagt till flera beteendemodeller för autentiseringsmönster för entiteter. Dessa modeller gör det möjligt för ATA att korrelera entitetsbeteende med misstänkta NTLM-autentiseringar och särskilja verkliga Pass-the-Hash-attacker från beteenden vid falskpositiva scenarier.

- **Förbättringar av Pass-the-Ticket** För att kunna identifiera avancerade attacker i allmänhet och Pass-the-Ticket i synnerhet, måste sambandet mellan en IP-adress och datorkontot vara korrekt. Detta är en utmaning i miljöer där IP-adresser ändras snabbt i utformning (till exempel Wi-Fi-nätverk och flera virtuella datorer som delar samma värd). För att lösa denna utmaning och förbättra identifiering av Pass-the-Ticket, har ATA:s mekanism Network Name Resolution (NNR) förbättrats avsevärt för att minska falskpositiva resultat.

- **Förbättringar för onormalt beteende** I ATA 1.7 har NTLM-autentiseringsdata lagts till som en datakälla för identifieringar av onormalt beteende, vilket ger algoritmer med bredare täckning för entitetsbeteende i nätverket. 

- **Förbättringar av onormal protokollimplementering** ATA identifierar nu ovanlig protokollimplementering i Kerberos-protokollet, tillsammans med ytterligare avvikelser i NTLM-protokollet. Dessa nya avvikelser för Kerberos används särskilt ofta i Over-pass-the-Hash-attacker.


### <a name="infrastructure"></a>Infrastruktur

- **Rollbaserad åtkomstkontroll** Förmåga för rollbaserad åtkomstkontroll (RBAC). ATA 1.7 innehåller tre roller: ATA-administratör, ATA-analytiker och ATA-chefer.

- **Stöd för Windows Server 2016 och Windows Server Core** ATA 1.7 stöder distribution av Lightweight Gateways på domänkontrollanter som kör Windows Server 2008 R2 SP1 (inkluderar inte Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (inkluderar Core men inte Nano). Den här versionen stöder dessutom Windows Server 2016 både för komponenterna ATA Center och ATA Gateway.

### <a name="user-experience"></a>Användarens upplevelse
- **Konfigurationsupplevelse** I den här versionen har konfigurationsupplevelsen för ATA gjorts om för en bättre användarupplevelse och bättre stöd för miljöer med flera ATA-gatewayar. Den här versionen beskriver även ATA Gateways uppdateringssida för enklare och bättre hantering av automatiska uppdateringar för olika gatewayar.

## <a name="known-issues"></a>Kända problem
Följande kända problem finns i den här versionen.

### <a name="gateway-automatic-update-may-fail"></a>Det gick inte att uppdatera gatewayen automatiskt
**Problem:** I miljöer med långsamma WAN-länkar, kan uppdateringen av ATA Gateway nå tidsgränsen för uppdatering (100 sekunder) och kan inte slutföras.
I ATA-konsolen har ATA Gateway statusen "Uppdatera (hämta paketet)" under en lång tid och misslyckas slutligen.
**Lösning:** Undvik det här problemet, ladda ned det senaste ATA Gateway-paketet från ATA-konsolen och uppdatera ATA Gateway manuellt.

 > [!IMPORTANT]
 Automatisk certifikatförnyelse för de certifikat som används av ATA stöds inte. Användningen av dessa certifikat kan orsaka att ATA slutar att fungera när certifikatet förnyas automatiskt. 

### <a name="no-browser-support-for-jis-encoding"></a>Inget webbläsarstöd för JIS-kodning
**Problem:** ATA-konsolen kanske inte fungerar som förväntat i webbläsare som använder JIS-kodning **Lösning:** Ändra webbläsarens kodning till Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>Ignorerad portspeglingstrafik när VMware används

Aviseringar om ignorerad portspeglingstrafik när Lightweight Gateway används på VMware.

Om du använder domänkontrollanter på virtuella VMware-datorer kan du få aviseringar om **ignorerad portspeglingstrafik**. Detta kan inträffa på grund av ett konfigurationsmatchningsfel i VMware. För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade i den virtuella datorn:  

- TsoEnable
- LargeSendOffload(IPv4)
- IPv4 TSO Offload

Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen om VMware.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Automatisk uppdatering av Gateway misslyckas vid uppdatering till 1.7 uppdatering 1

Både den automatiska uppdateringen för ATA Gateway och den manuella installationen av Gateway med hjälp av Gateway-paketet kanske inte fungerar som förväntat när du uppdaterar från ATA 1.7 till ATA 1.7 uppdatering 1.
Det här problemet uppstår om certifikatet som används av ATA Center har ändrats innan du uppdaterar ATA.
Kontrollera det här problemet genom att granska **Microsoft.Tri.Gateway.Updater.log** på ATA Gateway och leta efter följande undantag: **System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IdentityModel.Tokens.SecurityTokenValidationException: Failed to validate certificate thumbprint**

![bugg vid uppdatering av ATA-gateway](media/17update_gatewaybug.png)

För att lösa det här problemet kan du bläddra till följande plats från en upphöjd kommandotolk efter att du ändrat certifikatet: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** och köra följande:

1. Mongo.exe ATA (ATA måste anges med versaler.) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})

### <a name="export-suspicious-activity-details-to-excel-may-fail"></a>Det kanske inte går att exportera information om misstänkt aktivitet till Excel
Om du försöker exportera information om misstänkt aktivitet till en Excel-fil kanske åtgärden misslyckas och följande felmeddelande visas: *Fel [BsonClassMapSerializer`1] System.FormatException: Ett fel inträffade under deserialiseringen av egenskapen Activity av klassen Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity: Elementet ”ResourceIdentifier” matchar inte något fält eller någon egenskap av klassen Microsoft.Tri.Common.Data.EventActivities.NtlmEvent. ---> System.FormatException: Elementet ”ResourceIdentifier” matchar inte något fält eller någon egenskap av klassen Microsoft.Tri.Common.Data.EventActivities.NtlmEvent.*

För att lösa det här problemet kan du bläddra till följande plats från en upphöjd kommandotolk: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** och köra följande:
1.    **Mongo.exe ATA** (ATA måste anges med versaler)
2.    **db.SuspiciousActivityActivity.update({ "Activity._t": "NtlmEvent" },{$unset: {"Activity.ResourceIdentifier": ""}}, {multi: true});**

## <a name="minor-changes"></a>Mindre ändringar

- Nu använder ATA OWIN i stället för IIS för ATA-konsolen.
- Om ATA Center-tjänsten har problem kan du inte komma åt ATA-konsolen.
- Korta lån av undernät krävs inte längre på grund av ändringar i ATA NNR.

## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.7 – migreringsguide](ata-update-1.7-migration-guide.md)

