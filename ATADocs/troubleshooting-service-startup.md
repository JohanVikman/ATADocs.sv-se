---
title: "Felsök Advanced Threat Analytics med hjälp av loggarna | Microsoft Docs"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Felsöka starten av ATA Center-tjänsten

Om ATA Center inte startar, gör du följande felsökning:

1.  Kör följande Windows PowerShell-kommandot: `Get-Service Pla | Select Status` att säkerställa prestandaräknartjänsten körs. Om den inte körs rör det sig om ett plattformsproblem, och du måste få tjänsten att köra igen.
2.  Om den kördes försök att starta om den och se om det löser problemet:`Restart-Service Pla`
3.  Prova att skapa en ny datainsamlare manuellt (vilken som helst fungerar, till exempel bara insamling av datorns CPU-användning).
Om det går att starta är plattformen troligtvis inte skadad. Om inte, det beror på fortfarande plattform.

4.  Försök att manuellt återskapa ATA datainsamlaren, med hjälp av en förhöjd behörighet kör följande kommandon:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
