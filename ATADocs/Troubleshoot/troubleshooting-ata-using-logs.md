---
title: "Felsök Advanced Threat Analytics med hjälp av loggarna | Microsoft Docs"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 58df6ec3473118d0e11a5128eabd8feaa29f9fd2


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="troubleshooting-ata-using-the-ata-logs"></a>Felsöka ATA med ATA-loggarna
ATA-loggarna ger information om vad varje komponent i ATA gör vid en viss tidpunkt.

## <a name="ata-gateway-logs"></a>ATA Gateway-loggar
I det här avsnittet gäller varje hänvisning till ATA Gateway också ATA Lightweight Gateway. 

ATA Gateway-loggar finns i undermappen **Loggar** där ATA är installerat; standardplatsen är: **C:\Program Files\Microsoft Advanced Threat Analytics\**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Gateway\Logs**.

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

## <a name="ata-center-logs"></a>ATA Center-loggar
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


## <a name="ata-deployment-logs"></a>ATA-distributionsloggar
ATA-distributionsloggarna finns i temp-katalogen för användaren som installerade produkten. På standardplatsen för installation finns den i: **C:\Användare\Administrator\AppData\Local\Temp** (eller en katalog över %temp%).

ATA Center-distributionsloggar:

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra distributionsprocessen för ATA Center.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_0_MongoDBPackage.log** – Den här loggfilen innehåller stegen i MongoDB-distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra MongoDB-distributionsprocessen.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_1_MsiPackage.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Center-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Center-binärfilerna.

Distributionsloggar för ATA Gateway och ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra distributionsprocessen för ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS_001_MsiPackage.log** – Den här loggfilen innehåller stegen i distributionsprocessen för ATA Gateway-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Gateway-binärfilerna.


## <a name="see-also"></a>Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


