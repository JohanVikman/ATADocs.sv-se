---
title: Arbeta med misstänkta aktiviteter i Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du granskar misstänkta aktiviteter som identifieras av ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1557dff19375a5751eb655205dabadd684c655ba
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133182"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="working-with-suspicious-activities"></a>Arbeta med misstänkta aktiviteter
Den här artikeln förklarar grunderna för hur du arbetar med Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Granska misstänkta aktiviteter på attacktidslinjen
När du loggar in på ATA-konsolen kommer du automatiskt till den öppna **tidslinjen med misstänkta aktiviteter**. Misstänkta aktiviteter visas i kronologisk ordning med de senaste misstänkta aktiviteterna längst upp i tidslinjen.
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
> -   Om du klickar på en entitet kommer du till entitetsprofilen för användaren eller datorn.

![Tidslinjebild för misstänkta aktiviteter i ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrera lista med misstänkta aktiviteter
Filtrera listan med misstänkta aktiviteter:

1.  I den **filtrera efter** fönstret till vänster på skärmen väljer du något av följande alternativ: **alla**, **öppna**, **stängd**, eller **Ignorerade**.

2.  Om du vill filtrera listan ytterligare väljer **hög**, **medel**, eller **låg**.

**Allvarlighetsgrad för misstänkt aktivitet**

-   **Låg**

    Visar misstänkta aktiviteter som kan leda till attacker som har utformats för att användare eller programvara med skadliga avsikter ska få åtkomst till organisationsdata.

-   **Medel**

    Visar misstänkta aktiviteter som kan utsätta vissa identiteter för risk för mer allvarliga attacker som kan leda till identitetsstöld eller eskalering av privilegier

-   **Hög**

    Visar misstänkta aktiviteter som kan leda till identitetsstöld, eskalering eller andra attacker med stor effekt




## <a name="remediating-suspicious-activities"></a>Åtgärda misstänkta aktiviteter
Du kan ändra status för en misstänkt aktivitet genom att klicka på den misstänkta aktiviteten aktuella status och välja något av följande **öppna**, **ignorerad**, **stängd**, eller **bort**.
Du gör det genom att klicka på de tre punkterna i det övre högra hörnet för en specifik misstänkt aktivitet så att listan över tillgängliga åtgärder visas.

![ATA-åtgärder för misstänkta aktiviteter](./media/sa-actions.png)

**Status för misstänkt aktivitet**

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > Om samma aktivitet identifieras igen inom en kort tidsperiod, kan ATA öppna en stängd aktivitet.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Det innebär som om det finns en liknande avisering ATA inte öppna den igen. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, du aviseras igen.

- **Ta bort**: Om du tar bort en avisering tas bort från systemet och från databasen och du kommer inte att återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.

- **Undanta**: Möjligheten att undanta en entitet så att den inte genererar fler aviseringar av en viss typ. Du kan till exempel ange att ATA ska undanta en specifik entitet (användare eller dator) så att den inte utlöser aviseringar igen för en viss typ av misstänkt aktivitet, t.ex. en specifik administratör som kör fjärrkod eller ett säkerhetsgenomsökningsverktyg som utför en DNS-rekognosering. Förutom att lägga till undantag direkt för den misstänkta aktiviteten när den identifieras på tidslinjen kan du även gå till **Undantag** från sidan Konfiguration och, för varje misstänkt aktivitet, manuellt lägga till och ta bort undantagna enheter eller undernät (till exempel för Pass-the-Ticket). 
> [!NOTE]
> Konfigurationssidorna kan bara ändras av ATA-administratörer.


## <a name="related-videos"></a>Relaterade videor
- [Koppla säkerhets-communityn](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Se även
- [Spelboken för ATA-misstänkt aktivitet](http://aka.ms/ataplaybook)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändra ATA-konfiguration](modifying-ata-center-configuration.md)
