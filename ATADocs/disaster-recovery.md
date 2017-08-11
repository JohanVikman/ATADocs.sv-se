---
title: "Katastrofåterställning för Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du snabbt kan återställa ATA-funktioner efter en katastrof"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: d3621338070c257d9fa196fba8657a805216383b
ms.sourcegitcommit: 28f5d0f39149955c0d1059e13db289d13be9b642
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="ata-disaster-recovery"></a>ATA-katastrofåterställning
Den här artikeln beskriver hur du snabbt återställer ditt ATA-center och återställer ATA-funktioner när ATA Center-funktionen försvinner, men ATA-gatewayerna fortfarande fungerar. 

>[!NOTE]
> Processen som beskrivs kan inte återställa tidigare identifierade misstänkta aktiviteter men återställer ATA Center i fullt fungerande skick. Inlärningsperioden som behövs för viss beteendeidentifiering kommer även att startas om, men det mesta av identifieringen som ATA erbjuder fungerar direkt efter att ATA Center har återställts. 

## <a name="back-up-your-ata-center-configuration"></a>Säkerhetskopiera ATA Center-konfiguration

1. ATA Center-konfigurationen säkerhetskopieras till en fil varje timme. Leta upp den senaste säkerhetskopian av ATA Center-konfigurationen och spara den till en annan dator. En fullständig förklaring på hur du hittar de här filerna finns i [Exportera och importera ATA-konfigurationen](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportera ATA Center-certifikatet.
    1. I Certifikathanteraren, navigerar du till **Certifikat (lokal dator)** -> **personliga** ->**certifikat** och väljer **ATA Center**.
    2. Högerklicka på **ATA Center** och välj **Alla uppgifter** följt av **Exportera**. 
     ![ATA Center-certifikat](media/ata-center-cert.png)
    3. Följ anvisningarna för att exportera certifikatet. Var noga med att även exportera den privata nyckeln.
    4. Säkerhetskopiera den exporterade certifikatfilen på en annan dator.

  > [!NOTE] 
  > Om du inte kan exportera den privata nyckeln, måste du skapa ett nytt certifikat, distribuera det till ATA, som det beskrivs i [Ändra ATA Center-certifikatet](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert) och sedan exportera det. 

## <a name="recover-your-ata-center"></a>Återställa ATA Center

1. Skapa en ny Windows Server-dator med samma IP-adress och datornamn som den tidigare ATA Center-datorn.
4. Importera det säkerhetskopierade certifikatet till den nya servern.
5. Följ anvisningarna för att [Distribuera ATA Center](/advanced-threat-analytics/deploy-use/install-ata-step1) på den Windows Server du nyss skapade. Du behöver inte distribuera ATA-gatewayerna igen. När du uppmanas att ange ett certifikat, anger du det certifikat som du exporterade när du säkerhetskopierade ATA Center-konfigurationen . 
![ATA Center-återställning](media/disaster-recovery-deploymentss.png)
6. Importera den säkerhetskopierade ATA Center-konfiguration:
    1. Ta bort standardsystemprofildokumentet för ATA Center från MongoDB: 
        1. Gå till **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Kör `mongo.exe ATA` 
        3. Kör följande kommando för att ta bort standardsystemprofilen: `db.SystemProfile.remove({})`
    2. Kör kommandot: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` med säkerhetskopian från steg 1.</br>
    En fullständig förklaring på hur du hittar och importerar säkerhetskopior finns i [Exportera och importera ATA-konfigurationen](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Öppna ATA-konsolen. Du borde se alla ATA-gatewayer länkade under fliken konfiguration/gatewayer. 
    5. Se till att definiera en [**Directory Services-användare**](/advanced-threat-analytics/deploy-use/install-ata-step2) och välja en [**Domänkontrollant-synkroniserare**](/advanced-threat-analytics/deploy-use/install-ata-step5). 






## <a name="see-also"></a>Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
