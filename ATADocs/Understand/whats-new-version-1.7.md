---
title: Nyheter i ATA version 1.7 | Microsoft ATA
description: "Visar en lista över nyheter i ATA version 1.7 tillsammans med kända problem"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a024cab5e706b32273d563095f5d7e690d6ed055
ms.openlocfilehash: dec9fc03cdf718627dd72ac0c48f934fe507c7ac


---

# Nyheter i ATA version 1.7
Dessa versionsanmärkningar innehåller information om kända problem i denna version av Advanced Threat Analytics.

## Vad är nytt i ATA 1.7-uppdateringen?
Uppdateringen för ATA 1.7 ger förbättringar inom följande områden:

-   Nya och uppdaterade identifieringar

-   Rollbaserad åtkomstkontroll

-   Stöd för Windows Server 2016 och Windows Server Core

-   Förbättringar av användarupplevelse

-   Mindre ändringar


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

 > [!IMPORTANT]
 Automatisk certifikatförnyelse för de certifikat som används av ATA stöds inte. Användningen av dessa certifikat kan orsaka att ATA slutar att fungera när certifikatet förnyas automatiskt. 

### Inget webbläsarstöd för JIS-kodning
**Problem:** ATA-konsolen kanske inte fungerar som förväntat i webbläsare som använder JIS-kodning **Lösning:** Ändra webbläsarens kodning till Unicode UTF-8.
 
### Ignorerad portspeglingstrafik när VMware används

Aviseringar om ignorerad portspeglingstrafik när Lightweight Gateway används på VMware

Om du använder domänkontrollanter på virtuella VMware-datorer kan du få aviseringar om **ignorerad portspeglingstrafik**. Detta kan inträffa på grund av ett konfigurationsmatchningsfel i VMware. För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade: TsoEnable, LargeSendOffload, IPv4, TSO Offload. Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen om VMware.

## Mindre ändringar

- Nu använder ATA OWIN i stället för IIS för ATA-konsolen.
- Om ATA Center-tjänsten har problem kan du inte komma åt ATA-konsolen.
- Korta lån av undernät krävs inte längre på grund av ändringar i ATA NNR.

## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.7 – migreringsguide](ata-update-1.7-migration-guide.md)




<!--HONumber=Oct16_HO2-->


