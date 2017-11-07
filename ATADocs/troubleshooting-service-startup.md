---
title: "Felsök Advanced Threat Analytics med hjälp av loggarna | Microsoft Docs"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 760e03e764ddb502a2b11cdd3a2570b548837dc4
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/06/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Felsöka starten av ATA Center-tjänsten

Om ATA Center inte startar utför du följande felsökningssteg:

1.  Kör följande Windows PowerShell-kommando: Get-Service Pla | Välj Status för att kontrollera att tjänsten för prestandaräknare körs. Om den inte körs rör det sig om ett plattformsproblem, och du måste få tjänsten att köra igen.
2.  Om tjänsten körs provar du att starta om den och ser om det löser problemet: Restart-Service Pla
3.  Prova att skapa en ny datainsamlare manuellt (vilken som helst fungerar, till exempel bara insamling av datorns CPU-användning).
Om tjänsten kan starta är plattformen förmodligen okej, om inte rör det sig fortfarande om ett problem med plattformen.

4.  Prova att återskapa ATA-datainsamlaren manuellt från en upphöjd kommandotolk genom att köra följande kommandon: sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
