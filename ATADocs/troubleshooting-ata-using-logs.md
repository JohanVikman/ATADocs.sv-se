---
title: "Felsök Advanced Threat Analytics med hjälp av loggarna | Microsoft Docs"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/30/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d5a3587de2aa628eb61ace199b2282e7d7fe773a
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# Felsöka ATA med ATA-loggarna
<a id="troubleshooting-ata-using-the-ata-logs" class="xliff"></a>
ATA-loggarna ger information om vad varje komponent i ATA gör vid en viss tidpunkt.

## ATA Gateway-loggar
<a id="ata-gateway-logs" class="xliff"></a>
I det här avsnittet gäller varje hänvisning till ATA Gateway också ATA Lightweight Gateway. 

ATA Gateway-loggar finns i en undermapp som heter **Loggar** där ATA är installerat. standardplatsen är: **C:\Program Files\Microsoft Advanced Threat Analytics\**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Gateway\Logs**.

ATA Gateway har följande loggar:

-   **Microsoft.Tri.Gateway.log** – den här loggfilen innehåller allt som händer i ATA Gateway (inklusive lösning och fel). Den används huvudsakligen för att hämta övergripande status för alla åtgärder i kronologisk ordning som de inträffade.

-   **Microsoft.Tri.Gateway-Resolution.log** – den här loggfilen innehåller lösningsinformationen för de entiteter som setts i trafik av ATA-gatewayen. Den används huvudsakligen för att undersöka lösningsproblem för entiteter.

-   **Microsoft.Tri.Gateway-Errors.log** – den här loggfilen innehåller bara de fel som fångas av ATA Gateway. Den används huvudsakligen för att utföra hälsokontroller och undersöka problem som behöver korreleras till specifika tidpunkter.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – den här loggfilen grupper alla liknande fel och undantag, och mäter deras antal.
    Filen är tom från början varje gång ATA Gateway-tjänsten startar och uppdateras varje minut. Den används huvudsakligen för att förstå om det finns nya fel eller problem med ATA Gateway (eftersom felen grupperas är det lättare att läsa och förstå snabbt om det finns nya problem).
-   **Microsoft.Tri.Gateway.Updater.log** - Den här loggen används för gateway-uppdateringsprocessen som ansvarar för att uppdatera gatewayen om den konfigurerats att göra det automatiskt. För ATA Lightweight Gateway ansvarar också gateway- uppdateringsprocessen för resursbegränsningar av ATA Lightweight Gateway.
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** – Den här loggfilen grupper samman alla liknande fel och undantag, och mäter deras antal. Filen startar tom varje gång ATA Updater-tjänsten startar och uppdateras varje minut. Det gör att du kan förstå om det finns nya fel eller problem med ATA Updater. Felen grupperas för att göra det enklare att snabbt förstå om några nya fel eller problem har identifierats.

> [!NOTE]
> De första tre loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn. Som standard tas den äldsta filen bort om det redan finns fler än 10 filer från samma typ.

## ATA Center-loggar
<a id="ata-center-logs" class="xliff"></a>
ATA Center-loggarna finns i undermappen **Logs**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Center\Logs**".
> [!Note]
> ATA-konsolen loggar som tidigare var under IIS-loggar finns nu under ATA Center-loggar.

ATA Center har följande loggar:

-   **Microsoft.Tri.Center.log** – den här loggfilen innehåller allt som händer i ATA Center, inklusive identifieringar och fel. Den används huvudsakligen för att hämta övergripande status för alla åtgärder i kronologisk ordning som de inträffade.

-   **Microsoft.Tri.Center Detection.log** – den här loggfilen innehåller bara identifieringsinformationen för ATA Center. Den används huvudsakligen för att undersöka identifieringsproblem.

-   **Microsoft.Tri.Center-Errors.log** – den här loggfilen innehåller bara de fel som fångas av ATA Center. Den används huvudsakligen för att utföra hälsokontroller och undersöka problem som behöver korreleras till specifika tidpunkter.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – den här loggfilen grupper alla liknande fel och undantag, och mäter deras antal.
    Filen är tom från början varje gång ATA Center-tjänsten startar och uppdateras varje minut. Den används huvudsakligen för att förstå om det finns nya fel eller problem med ATA Center – eftersom felen grupperas är det lättare förstå om det finns nya fel eller problem.

> [!NOTE]
> De första tre loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn. Som standard tas den äldsta filen bort om det redan finns fler än 10 filer från samma typ.


## ATA-distributionsloggar
<a id="ata-deployment-logs" class="xliff"></a>
ATA-distributionsloggarna finns i temp-katalogen för användaren som installerade produkten. På standardplatsen för installation finns den i: **C:\Användare\Administrator\AppData\Local\Temp** (eller en katalog över %temp%).

ATA Center-distributionsloggar:

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra distributionsprocessen för ATA Center.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_0_MongoDBPackage.log** – Den här loggfilen innehåller stegen i MongoDB-distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra MongoDB-distributionsprocessen.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_1_MsiPackage.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Center-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Center-binärfilerna.

Distributionsloggar för ATA Gateway och ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra distributionsprocessen för ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS_001_MsiPackage.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Gateway-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Gateway-binärfilerna.


> [!NOTE] 
> Förutom de distributionsloggar som nämns här finns det även andra loggar som börjar med "Microsoft Advanced Threat Analytics" och som kan ge ytterligare information om distributionsprocessen.


## Se även
<a id="see-also" class="xliff"></a>
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
