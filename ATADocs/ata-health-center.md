---
title: "Övervaka systemhälsa och händelser i Advanced Threat Analytics | Microsoft Docs"
description: "Använd ATA Health Center för att kontrollera hur ATA-tjänsten fungerar och om du vill bli meddelad om potentiella problem och granska händelser i Loggboken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdd046eeaca1d8aeb7ea3afa001b34b82cb468b0
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2017
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

-   Alla öppna aviseringar kan hanteras genom att ange dem **Stäng**, **utelämna**, eller **ta bort** genom att klicka på de tre punkterna i hörnet av aviseringen och göra valet.

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: Används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat.

    > [!NOTE]
    > ATA kan öppna en stängd aktivitet om det samma aktivitet identifieras igen under en kort tidsperiod.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Det innebär att om det finns en liknande avisering så öppnas den inte igen av ATA. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, så aviseras du igen.

- **Ta bort**: Om du tar bort en avisering tas den bort från systemet och från databasen och du kan INTE återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.



![Bild av ATA Health Center-problem](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
