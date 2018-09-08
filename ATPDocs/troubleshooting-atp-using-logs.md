---
title: Felsöka Azure Advanced Threat Protection med hjälp av loggarna | Microsoft Docs
description: Beskriver hur du kan använda Azure ATP-loggarna för att felsöka problem
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: fee526b836b9fbbf28624bdce4354267ab968cd6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166100"
---
*Gäller för: Advanced Threat Protection*



# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Felsökning Azure Advanced Threat Protection (ATP) sensorn med ATP-loggar
ATP-loggarna ger information om vad varje komponent i Azure ATP-sensorn gör vid en given tidpunkt i tid.


Azure ATP-loggar finns i undermappen **loggar** där ATP är installerat; standardplatsen är: **c:\Program\Microsoft Files\Azure Advanced Threat Protection Sensor\\**. På standardplatsen för installation finns på: **c:\Program\Microsoft Files\Azure Advanced Threat Protection Sensor\version number\Logs**.

Azure ATP-sensorn har följande loggar:

-   **Microsoft.Tri.Sensor.log** – den här loggfilen innehåller allt som händer i Azure ATP-sensorn (inklusive lösning och fel). Den används huvudsakligen för att hämta övergripande status för alla åtgärder i kronologisk ordning som de inträffade.

-   **Microsoft.Tri.Sensor Resolution.log** – den här loggfilen innehåller för de entiteter som setts i trafik av ATP-sensorn. Den används huvudsakligen för att undersöka lösningsproblem för entiteter.

-   **Microsoft.Tri.Sensor-Errors.log** – den här loggfilen innehåller bara de fel som fångas av ATP-sensorn. Den används huvudsakligen för att utföra hälsokontroller och undersöka problem som behöver korreleras till specifika tidpunkter.

-   **Microsoft.Tri.Sensor.Updater.log** -den här loggen används för sensor-uppdateringsprocessen som ansvarar för att uppdatera ATP-sensorn om konfigurerad för att göra det automatiskt. 


> [!NOTE]
> De första tre loggfilerna har en maximal storlek på upp till 50 MB. När den storleken nås öppnas en ny loggfil och namnet på den tidigare ändras till "&lt;ursprungligt filnamn&gt;-arkiverad-00000", där talet ökar varje gång den får ett nytt namn. Som standard tas den äldsta filen bort om det redan finns fler än 10 filer från samma typ.

## <a name="azure-atp-deployment-logs"></a>Azure ATP-distributionsloggar
Azure ATP-distributionsloggarna finns i temp-katalogen för den användare som installerade produkten. På standardplatsen för installation finns den i: **C:\Användare\Administrator\AppData\Local\Temp** (eller en katalog över %temp%).

Azure ATP-sensorn-distributionsloggar:

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** -den här loggfilen innehåller stegen i distributionsprocessen för Azure ATP-sensorn. Den används huvudsakligen för att spåra distributionsprocessen för Azure ATP-sensorn.

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** -den här loggfilen innehåller stegen i distributionsprocessen för binärfilerna för Azure ATP-sensorn. Den används huvudsakligen för att spåra distributionen av binärfilerna för Azure ATP-sensorn.


> [!NOTE] 
> Förutom de distributionsloggar som nämns här, det finns andra loggar som börjar med ”Azure Advanced Threat Protection” som kan ge ytterligare information om distributionsprocessen.


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)