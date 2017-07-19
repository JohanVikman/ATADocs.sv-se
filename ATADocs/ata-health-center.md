---
title: "Övervaka systemhälsa och händelser i Advanced Threat Analytics | Microsoft Docs"
description: "Använd ATA Health Center för att kontrollera hur ATA-tjänsten fungerar och om du vill bli meddelad om potentiella problem och granska händelser i Loggboken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 59e5cafcff7b84ffb9dc161cd0b50cd3014e455a
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# <a name="working-with-ata-system-health-and-events"></a>Arbeta med systemhälsa och händelser i ATA

## <a name="ata-health-center"></a>ATA Health Center
Med ATA Health Center får du reda på hur ATA-tjänsten fungerar och blir informerad om problem.

## <a name="working-with-the-ata-health-center"></a>Arbeta med ATA Health Center
Med ATA Health Center får du reda på att det finns ett problem genom att en avisering (en röd punkt) visas ovanför Health Center-ikonen på menyraden.

![Verktygsfält med röd punkt för ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Hantera ATA-hälsa
Du kan kontrollera systemets övergripande hälsa genom att klicka på Health Center-ikonen på menyraden ![ATA Health Center-ikon](media/ATA-red-dot.png)

-   Alla öppna aviseringar kan hanteras genom att ställa in dem på **Löst** eller **Avvisat**. I aviseringen klickar du på **Öppna** och rullar ned till **Löst** eller **Avvisat**.

-   Om du har löst ett problem och ATA upptäcker att problemet kvarstår flyttas problemet automatiskt tillbaka till problemlistan **Öppna**. Om ATA upptäcker att ett öppet problem är löst flyttas det automatiskt till problemlistan **Löst**.

-   **Avvisade** problem är problem som du inte vill att ATA ska fortsätta kontrollera – om du till exempel informeras om ett problem som du vet finns och inte planerar att lösa problemet, men inte vill fortsätta få meddelanden om det och inte längre vill se det i problemlistan **Öppna**, kan du ändra det till **Avvisat**.

![Bild av ATA Health Center-problem](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
