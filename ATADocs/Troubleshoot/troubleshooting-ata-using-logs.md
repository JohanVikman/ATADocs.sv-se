---
title: "Felsöka ATA med ATA-loggarna | Microsoft ATA"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: f13b448399f4184ebb110883800e87902d3b7ac3


---

# Felsöka ATA med ATA-loggarna
ATA-loggarna ger information om vad varje komponent i ATA gör vid en viss tidpunkt.

## ATA Gateway-loggar
I det här avsnittet gäller varje hänvisning till ATA Gateway också ATA Lightweight Gateway. 

ATA Gateway-loggarna finns i undermappen **Logs**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Gateway\Logs**.

ATA Gateway har följande loggar:

-   **Microsoft.Tri.Gateway.log** – den här loggfilen innehåller allt som händer i ATA Gateway (inklusive lösning och fel). Den används huvudsakligen för att hämta övergripande status för alla åtgärder i kronologisk ordning som de inträffade.

-   **Microsoft.Tri.Gateway-Resolution.log** – den här loggfilen innehåller lösningsinformationen för de entiteter som setts i trafik av ATA-gatewayen. Den används huvudsakligen för att undersöka lösningsproblem för entiteter.

-   **Microsoft.Tri.Gateway-Errors.log** – den här loggfilen innehåller bara de fel som fångas av ATA Gateway. Den används huvudsakligen för att utföra hälsokontroller och undersöka problem som behöver korreleras till specifika tidpunkter.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – den här loggfilen grupper alla liknande fel och undantag, och mäter deras antal.
    Filen är tom från början varje gång ATA Gateway-tjänsten startar och uppdateras varje minut. Den används huvudsakligen för att förstå om det finns nya fel eller problem med ATA Gateway – eftersom felen grupperas är det lättare att läsa och se om det finns en ny typ av fel eller problem.

> [!NOTE]
> De första tre loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn.

## ATA Center-loggar
ATA Center-loggarna finns i undermappen **Logs**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Center\Logs**".

ATA Center har följande loggar:

-   **Microsoft.Tri.Center.log** – den här loggfilen innehåller allt som händer i ATA Center, inklusive identifieringar och fel. Den används huvudsakligen för att hämta övergripande status för alla åtgärder i kronologisk ordning som de inträffade.

-   **Microsoft.Tri.Center Detection.log** – den här loggfilen innehåller bara identifieringsinformationen för ATA Center. Den används huvudsakligen för att undersöka identifieringsproblem.

-   **Microsoft.Tri.Center-Errors.log** – den här loggfilen innehåller bara de fel som fångas av ATA Center. Den används huvudsakligen för att utföra hälsokontroller och undersöka problem som behöver korreleras till specifika tidpunkter.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – den här loggfilen grupper alla liknande fel och undantag, och mäter deras antal.
    Filen är tom från början varje gång ATA Center-tjänsten startar och uppdateras varje minut. Den används huvudsakligen för att förstå om det finns nya fel eller problem med ATA Center – eftersom felen grupperas är det lättare att läsa och se om det finns en ny typ av fel eller problem.

> [!NOTE]
> De första tre loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn.

## ATA-konsolloggar
ATA-konsolloggarna (hanterings-API-loggarna) finns i undermappen **Logs**. På standardplatsen för installation finns den i: **C:\Program\Microsoft Advanced Threat Analytics\Management\Logs**.

ATA-konsolen har följande loggar:

-   **w3wp.log** – den här loggfilen innehåller allt som händer i hanteringen (IIS).


-   **w3wp-Errors.log** – den här loggfilen innehåller bara de fel som fångas av hanteringen (IIS).


-   **8e75f9f1-ExceptionStatistics.log** – den här loggfilen grupper alla liknande fel och undantag, och mäter deras antal.
    Filen är tom från början varje gång gatewaytjänsten startar och uppdateras varje minut. Den används huvudsakligen för att förstå om det finns nya fel eller problem med ATA Center – eftersom felen grupperas är det lättare att läsa och se om det finns en ny typ av fel eller problem.

> [!NOTE]
> De första två loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn.

## ATA-distributionsloggar
ATA-distributionsloggarna finns i temp-katalogen för användaren som installerade produkten. På standardplatsen för installation finns den i: **C:\Användare\Administrator\AppData\Local\Temp** (eller en katalog över %temp%).

ATA Center-distributionsloggar:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra distributionsprocessen för ATA Center.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** – den här loggfilen innehåller stegen i MongoDB-distributionsprocessen för ATA Center. Den används huvudsakligen för att spåra MongoDB-distributionsprocessen.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Center-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Center-binärfilerna.

Distributionsloggar för ATA Gateway och ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Gateway. Den används huvudsakligen för att spåra distributionsprocessen för ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** – den här loggfilen innehåller stegen i distributionsprocessen för ATA Gateway-binärfilerna. Den används huvudsakligen för att spåra distributionen av ATA Gateway-binärfilerna.

## Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


