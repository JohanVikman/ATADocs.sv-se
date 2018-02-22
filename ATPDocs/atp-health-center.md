---
title: "Övervaka systemhälsa i Azure Advanced Threat Protection och händelser | Microsoft Docs"
description: "Använd Azure ATP arbetsytan health center för att kontrollera hur Azure ATP-tjänsten fungerar och bli informerad om potentiella problem och visa händelser i Loggboken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86eb90f452d5aee2504e525e64bfc62c22207880
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Arbeta med Azure ATP arbetsytan hälsa och händelser

## <a name="azure-atp-workspace-health-center"></a>Azure ATP arbetsytan health center 

Azure ATP arbetsytan health center får du reda på hur Azure ATP arbetsytan utförs och problem som du om det uppstår problem.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Arbeta med Azure ATP arbetsytan health center

Azure ATP arbetsytan health center får du veta att det finns ett problem genom att en avisering (en röd punkt) ovanför Health Center-ikonen på menyraden.

![Azure ATP arbetsytan health center verktygsfält med röd punkt](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Hantera Azure ATP arbetsytan hälsa
Du kan kontrollera din arbetsyta övergripande hälsa, klicka på Health Center-ikonen på menyraden ![Azure ATP arbetsytan health center-ikonen](media/atp-red-dot.png)

-   Alla öppna problem kan hanteras genom att ange dem **Stäng**, eller **utelämna**, genom att klicka på de tre punkterna i hörnet av aviseringen och göra valet.

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > Azure ATP kan öppna en stängd aktivitet om samma aktivitet identifieras igen inom en kort tidsperiod.
    > Varje arbetsyta har sin egen health center.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Om det finns en liknande avisering Azure ATP inte öppna den igen. Men om aviseringen slutar i sju dagar och sedan visas igen, du meddelas igen.

-   **Öppna**: Om du stänga eller ignorera problemet kan du öppna det så att den visas öppna i tidslinjen igen.
- 
- **Ta bort**: från inom tidslinjen misstänkta aktiviteter också har du möjlighet att ta bort ett hälsoproblem. Om du tar bort en avisering tas bort från arbetsytan och du kommer inte att kunna återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.



![Azure ATP arbetsytan bild health center problem](media/atp-health-issue.png)






## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
