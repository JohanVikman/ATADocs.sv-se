---
title: Felsök Advanced Threat Analytics starttjänst | Microsoft Docs
description: Beskriver hur du kan felsöka problem med ATA-Start
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e3f59bc7c6873407d8764dc5ab64bfd7a52fdebe
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133352"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="troubleshooting-service-startup"></a>Felsökning av tjänsten startades

## <a name="troubleshooting-ata-center-service-startup"></a>Felsöka starten av ATA Center-tjänsten

Om ATA Center inte startar utför du följande felsökningssteg:

1.  Kör följande Windows PowerShell-kommando: `Get-Service Pla | Select Status`
    Om du vill kontrollera att körs tjänsten för prestandaräknare. Om den inte körs rör det sig om ett plattformsproblem, och du måste få tjänsten att köra igen.
2.  Om den kördes försök starta om den och se om det löser problemet: `Restart-Service Pla`
3.  Prova att skapa en ny datainsamlare manuellt (vilken som helst fungerar, till exempel bara insamling av datorns CPU-användning).
Om tjänsten kan starta är plattformen förmodligen bra. Om inte, det är fortfarande ett problem med plattformen.

4.  Försök att manuellt återskapa ATA-datainsamlaren, från en upphöjd kommandotolk kör dessa kommandon:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Felsöka ATA Lightweight Gateway Start

**Symtom**

ATA-gatewayen startar inte och du får felet:<br></br>
*System.Net.Http.HttpRequestException: Svarsstatuskod anger inte lyckad: 500 (Internt serverfel)*

**Beskrivning**

Detta inträffar eftersom som en del av installationsprocessen Lightweight Gateway, ATA allokerar en CPU-tröskelvärdet som gör det möjligt för Lightweight Gateway kan använda CPU och en buffert med 15%. Om du oberoende av varandra har angett ett tröskelvärde med registernyckeln: den här konflikten förhindrar Lightweight-Gateway från att starta. 

**Lösning**

1. Under registret nycklar, om det finns en DWORD-värdet kallas **Inaktivera prestandaräknare** kontrollerar den är inställd på **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\`
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Starta sedan om tjänsten Pla. ATA Lightweight Gateway identifierar ändringen automatiskt och starta om tjänsten.


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
