---
title: ATA Health Center | Microsoft Docs
description: "Använd ATA Health Center om du vill kontrollera hur ATA-tjänsten fungerar och bli informerad om potentiella problem."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: bff593f07d70cd559a1ee75d3b75c61b6534432d


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="ata-health-center"></a>ATA Health Center
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
- [Arbeta med identifieringsinställningar i ATA](working-with-detection-settings.md)
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


