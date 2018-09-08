---
title: Övervaka systemhälsa och händelser i Advanced Threat Analytics | Microsoft Docs
description: Använd ATA Health Center för att kontrollera hur ATA-tjänsten fungerar och om du vill bli meddelad om potentiella problem och granska händelser i Loggboken.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7bf91f258d1eaf9c83cc610fc43dfa52a2da3e6b
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166909"
---
*Gäller för: Advanced Threat Analytics version 1.9*


# <a name="working-with-ata-system-health-and-events"></a>Arbeta med systemhälsa och händelser i ATA

## <a name="ata-health-center"></a>ATA Health Center
Med ATA Health Center får du reda på hur ATA-tjänsten fungerar och blir informerad om problem.

## <a name="working-with-the-ata-health-center"></a>Arbeta med ATA Health Center
Med ATA Health Center får du reda på att det finns ett problem genom att en avisering (en röd punkt) visas ovanför Health Center-ikonen på menyraden.

![Verktygsfält med röd punkt för ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Hantera ATA-hälsa
Du kan kontrollera systemets övergripande hälsa genom att klicka på Health Center-ikonen på menyraden ![ATA Health Center-ikon](media/ATA-red-dot.png)

-   Alla öppna aviseringar kan hanteras genom att ange dem till **Stäng**, **utelämna**, eller **ta bort** genom att klicka på de tre punkterna i hörnet av aviseringen och ditt val.

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > ATA kan öppna en stängd aktivitet om samma aktivitet identifieras igen inom en kort tidsperiod.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Om det finns en liknande avisering ATA inte öppna den igen. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, du aviseras igen.

- **Ta bort**: Om du tar bort en avisering tas bort från systemet och från databasen och du kommer inte att återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.



![Bild av ATA Health Center-problem](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
