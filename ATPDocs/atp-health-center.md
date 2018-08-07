---
title: Övervaka Azure Advanced Threat Protection systemhälsa och händelser | Microsoft Docs
description: Använd Azure ATP arbetsytan health center för att kontrollera hur Azure ATP-tjänsten fungerar och bli informerad om potentiella problem och granska händelser i Loggboken.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5fb4acaca989922ad894cee4a799378bb912643d
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567992"
---
*Gäller för: Azure Avancerat skydd*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Arbeta med Azure ATP arbetsytan hälsa och händelser

## <a name="azure-atp-workspace-health-center"></a>Azure ATP arbetsytan health center 

Azure ATP arbetsytan health center får du reda på hur din Azure ATP-arbetsyta fungerar och varnar dig om det uppstår problem.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Arbeta med Azure ATP arbetsytan health center

Azure ATP arbetsytan health center får du veta att det finns ett problem genom att en avisering (en röd punkt) ovanför Health Center-ikonen på menyraden.

![Azure ATP arbetsytan health center verktygsfält med röd punkt](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Hantera Azure ATP arbetsytan hälsotillstånd
Du kan kontrollera din arbetsyta övergripande hälsa, klickar du på Health Center-ikonen på menyraden ![Azure ATP arbetsytan health center-ikonen](media/atp-red-dot.png)

-   Alla öppna ärenden kan hanteras genom att ange dem till **Stäng**, eller **utelämna**, genom att klicka på de tre punkterna i hörnet av aviseringen och ditt val.

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > Azure ATP kan öppna en stängd aktivitet om samma aktivitet identifieras igen inom en kort tidsperiod.
    > Varje arbetsyta har sin egen hälsocenter.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Om det finns en liknande avisering Azure ATP inte öppna den igen. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, du aviseras igen.

-   **Öppna**: du kan återaktivera en stängd eller ignorerade problemet så att den visas öppen i tidslinjen igen.
- 
- **Ta bort**: från i tidslinjen för misstänkta aktiviteter du har också möjlighet att ta bort ett hälsoproblem. Om du tar bort en avisering tas bort från arbetsytan och du kan inte återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.



![Azure ATP arbetsytan bild health center problem](media/atp-health-issue.png)






## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
