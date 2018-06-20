---
title: Felsökning av Advanced Threat Analytics startades | Microsoft Docs
description: Beskriver hur du felsöker problem med start av ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 87d3f1de8167c1198e6b334826f90df83cc96780
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009276"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="troubleshooting-service-startup"></a>Felsöka startades

## <a name="troubleshooting-ata-center-service-startup"></a>Felsöka starten av ATA Center-tjänsten

Om ATA Center inte startar, gör du följande felsökning:

1.  Kör följande Windows PowerShell-kommandot: `Get-Service Pla | Select Status` att säkerställa prestandaräknartjänsten körs. Om den inte körs rör det sig om ett plattformsproblem, och du måste få tjänsten att köra igen.
2.  Om den kördes försök att starta om den och se om det löser problemet: `Restart-Service Pla`
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

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Felsöka ATA Lightweight Gateway Start

**Symptom**

ATA-gatewayen startar inte och du får detta fel:<br></br>
*System.Net.Http.HttpRequestException: Svarsstatuskoden indikerar inte lyckade: 500 (Internt serverfel)*

**Beskrivning**

Detta inträffar eftersom som en del av installationen av Lightweight Gateway, ATA allokerar en CPU-tröskel som gör det möjligt för Lightweight Gateway att använda processor med en buffert på 15%. Om du oberoende av varandra har angett ett tröskelvärde med registernyckeln: konflikten hindrar Lightweight Gateway från att starta. 

**Lösning**

1. Under registret nycklar, om det finns en DWORD-värdet kallas **Inaktivera prestandaräknare** Kontrollera att den är inställd på **0**:  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Starta sedan om tjänsten Pla. ATA Lightweight Gateway upptäcks ändringen automatiskt och starta om tjänsten.


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
