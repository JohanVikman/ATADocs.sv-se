---
title: "Arbeta med misstänkta aktiviteter i Azure Advanced Threat Protection | Microsoft Docs"
description: "Beskriver hur du granskar misstänkta aktiviteter som identifieras av Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a5e7598e94e1d6d4b09c827770e062be9fefd1c4
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="working-with-suspicious-activities"></a>Arbeta med misstänkta aktiviteter
Den här artikeln förklarar grunderna för hur du arbetar med Azure Advanced Threat Protection.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Granska misstänkta aktiviteter på attacktidslinjen
När du loggar in på Azure ATP arbetsytan portal kommer du automatiskt till öppen **tidslinje för misstänkta aktiviteter**. Misstänkta aktiviteter visas i kronologisk ordning med de senaste misstänkta aktiviteterna längst upp i tidslinjen.
Varje misstänkt aktivitet har följande information:

-   Entiteter som berörs, inklusive användare, datorer, servrar, domänkontrollanter och resurser.

-   Tidpunkter och tidsintervall för de misstänkta aktiviteterna.

-   Allvarlighetsgrad för den misstänkta aktiviteten, Hög, Medel eller Låg.

-   Status: Öppen, stängd eller ignorerad.

-   Möjlighet att

    -   Dela misstänkta aktiviteter med andra personer i organisationen via e-post.

    -   Exportera den misstänkta aktiviteten till Excel.

> [!NOTE]
> -   När du håller muspekaren över en användare eller dator visas en entitetsminiprofil som innehåller ytterligare information om entiteten och som innehåller antalet misstänkta aktiviteter som entiteten är kopplad till.
> -   Om du klickar på en enhet går du till entitetsprofilen för användaren eller datorn.

![Bild för tidslinje Azure ATP misstänkta aktiviteter](media/atp-sa-timeline.png)

## <a name="filter-suspicious-activities-list"></a>Filtrera lista med misstänkta aktiviteter
Filtrera listan med misstänkta aktiviteter:

1.  I den **filtrera efter** till vänster på skärmen väljer du något av följande alternativ: **alla**, **öppna**, **stängd**, eller **Ignorerade**.

2.  Om du vill filtrera listan ytterligare väljer **hög**, **medel**, eller **låg**.

**Allvarlighetsgrad för misstänkt aktivitet**

-   **Låg**

    Visar misstänkta aktiviteter som kan leda till attacker som har utformats för att användare eller programvara med skadliga avsikter ska få åtkomst till organisationsdata.

-   **Medel**

    Visar misstänkta aktiviteter som kan utsätta vissa identiteter för risk för mer allvarliga attacker som kan leda till identitetsstöld eller eskalering av privilegier

-   **Hög**

    Visar misstänkta aktiviteter som kan leda till identitetsstöld, eskalering eller andra attacker med stor effekt




## <a name="managing-suspicious-activities"></a>Hantera misstänkta aktiviteter
Du kan ändra status för en misstänkt aktivitet genom att klicka på den misstänkta aktiviteten aktuella status och välja något av följande **öppna**, **Suppressed**, **stängd**, eller **bort**.
Du gör det genom att klicka på de tre punkterna i det övre högra hörnet för en specifik misstänkt aktivitet så att listan över tillgängliga åtgärder visas.

![Azure ATP åtgärder för misstänkta aktiviteter](./media/atp-sa-actions.png)

**Status för misstänkt aktivitet**

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > Om samma aktivitet identifieras igen under en kort tidsperiod, kan Azure ATP öppna en stängd aktivitet.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Det innebär som om det finns en liknande avisering Azure ATP inte öppna den igen. Men om aviseringen slutar i sju dagar och sedan visas igen, du meddelas igen.

- **Ta bort**: Om du tar bort en avisering, tas bort från systemet från databasen och du kommer inte att kunna återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.

- **Undanta**: Möjligheten att undanta en entitet så att den inte genererar fler aviseringar av en viss typ. Du kan till exempel ange Azure ATP att undanta en viss enhet (användare eller dator) mellan avisering igen för en viss typ av misstänkt aktivitet, till exempel en viss administratör som kör kod eller ett säkerhetsskannern som tillåter DNS-rekognosering. Förutom att lägga till undantag direkt för den misstänkta aktiviteten när den identifieras på tidslinjen kan du även gå till **Undantag** från sidan Konfiguration och, för varje misstänkt aktivitet, manuellt lägga till och ta bort undantagna enheter eller undernät (till exempel för Pass-the-Ticket). 

> [!NOTE]
> Konfigurationssidorna kan bara ändras av Azure ATP administratörer.


## <a name="see-also"></a>Se även

- [Arbeta med Azure ATP arbetsytan portal](workspace-portal.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)