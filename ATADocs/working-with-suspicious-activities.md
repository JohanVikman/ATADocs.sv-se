---
title: "Arbeta med misstänkta aktiviteter i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du granskar misstänkta aktiviteter som identifieras av ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d943dc9aae7192f46f079175c2216b5b27e459e2
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# Arbeta med misstänkta aktiviteter
<a id="working-with-suspicious-activities" class="xliff"></a>
Det här avsnittet förklarar grunderna för hur du arbetar med Advanced Threat Analytics.

## Granska misstänkta aktiviteter på attacktidslinjen
<a id="review-suspicious-activities-on-the-attack-time-line" class="xliff"></a>
När du loggar in på ATA-konsolen kommer du automatiskt till den öppna **tidslinjen med misstänkta aktiviteter**. Misstänkta aktiviteter visas i kronologisk ordning med de senaste misstänkta aktiviteterna längst upp i tidslinjen.
Varje misstänkt aktivitet har följande information:

-   Entiteter som berörs, inklusive användare, datorer, servrar, domänkontrollanter och resurser.

-   Tidpunkter och tidsintervall för de misstänkta aktiviteterna.

-   Allvarlighetsgrad för den misstänkta aktiviteten, Hög, Medel eller Låg.

-   Status: Öppen, stängd eller ignorerad.

-   Möjlighet att

    -   Dela misstänkta aktiviteter med andra personer i organisationen via e-post.

    -   Exportera den misstänkta aktiviteten till Excel.

    -   Lägga till en anteckning till den misstänkta aktiviteten.

    -   Ange kommentarer om den misstänkta aktiviteten.

-   Innehåller rekommendationer för hur man kan reagera på den misstänkta aktiviteten.

> [!NOTE]
> -   När du håller muspekaren över en användare eller dator visas en entitetsminiprofil som innehåller ytterligare information om entiteten och som innehåller antalet misstänkta aktiviteter som entiteten är kopplad till.
> -   Om du klickar på en entitet kommer du till entitetsprofilen för användaren eller datorn.

![Tidslinjebild för misstänkta aktiviteter i ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtrera lista med misstänkta aktiviteter
<a id="filter-suspicious-activities-list" class="xliff"></a>
Filtrera listan med misstänkta aktiviteter:

1.  I rutan **Filtrera efter** till vänster på skärmen väljer du något av följande: **Alla**, **Öppet**, **Löst** eller **Avvisat**.

2.  Om du vill filtrera listan ytterligare väljer du **Hög**, **Medel** eller **Låg**.

**Allvarlighetsgrad för misstänkt aktivitet**

-   **Låg**

    Visar misstänkta aktiviteter som kan leda till attacker som har utformats för att användare eller programvara med skadliga avsikter ska få åtkomst till organisationsdata.

-   **Medel**

    Visar misstänkta aktiviteter som kan utsätta vissa identiteter för risk för mer allvarliga attacker som kan leda till identitetsstöld eller eskalering av privilegier

-   **Hög**

    Visar misstänkta aktiviteter som kan leda till identitetsstöld, eskalering av privilegier eller andra attacker med stor effekt




## Åtgärda misstänkta aktiviteter
<a id="remediating-suspicious-activities" class="xliff"></a>
Du kan ändra status för en misstänkt aktivitet genom att klicka på den misstänkta aktivitetens aktuella status och välja något av följande: **Öppen**, **Ignorerad**, **Stängd** eller **Borttagen**.
Du gör det genom att klicka på de tre punkterna i det övre högra hörnet för en specifik misstänkt aktivitet så att listan över tillgängliga åtgärder visas.

![ATA-åtgärder för misstänkta aktiviteter](./media/sa-actions.png)

**Status för misstänkt aktivitet**

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: Används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat.

    > [!NOTE]
    > ATA kan öppna en löst aktivitet igen om samma aktivitet identifieras igen under en kort tidsperiod.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Det innebär att om det finns en liknande avisering så öppnas den inte igen av ATA. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, så aviseras du igen.

- **Ta bort**: Om du tar bort en avisering tas den bort från systemet och från databasen och du kan INTE återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.

- **Undanta**: Möjligheten att undanta en entitet så att den inte genererar fler aviseringar av en viss typ. Du kan till exempel ange att ATA ska undanta en specifik entitet (användare eller dator) så att den inte utlöser aviseringar igen för en viss typ av misstänkt aktivitet, t.ex. en specifik administratör som kör fjärrkod eller ett säkerhetsgenomsökningsverktyg som utför en DNS-rekognosering. Förutom att lägga till undantag direkt för den misstänkta aktiviteten när den identifieras på tidslinjen kan du även gå till **Undantag** från sidan Konfiguration och, för varje misstänkt aktivitet, manuellt lägga till och ta bort undantagna enheter eller undernät (till exempel för Pass-the-Ticket). 
> [!NOTE]
> Konfigurationssidorna kan bara ändras av ATA-administratörer.


## Se även
<a id="see-also" class="xliff"></a>
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändra ATA-konfiguration](modifying-ata-center-configuration.md)
