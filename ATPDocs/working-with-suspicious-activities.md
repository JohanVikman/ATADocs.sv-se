---
title: Arbeta med misstänkta aktiviteter i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver hur du granskar misstänkta aktiviteter som identifieras av Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7caae52ff7402fdc8cb18ce1a01bba469c2d649b
ms.sourcegitcommit: f61616a8269d27a8fcde6ecf070a00e2c56481ac
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2018
ms.locfileid: "35259216"
---
*Gäller för: Azure Avancerat skydd*



# <a name="working-with-suspicious-activities"></a>Arbeta med misstänkta aktiviteter
Den här artikeln förklarar grunderna för hur du arbetar med Azure Advanced Threat Protection.

## Granska misstänkta aktiviteter på tidslinjen <a name="review-suspicious-activities-on-the-attack-time-line"></a>
När du har loggat in Azure ATP-arbetsyteportalen, kommer du automatiskt till öppen **tidslinjen för misstänkta aktiviteter**. Misstänkta aktiviteter visas i kronologisk ordning med de senaste misstänkta aktiviteterna längst upp i tidslinjen.
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

![Azure ATP bild för tidslinje för misstänkta aktiviteter](media/atp-sa-timeline.png)

## Förhandsversion av identifieringar<a name="preview-detections"></a>

Azure ATP research-teamet arbetar ständigt på att implementera nya identifieringar för nyligen identifierade attacker. Eftersom Azure ATP är en molnbaserad tjänst, är det möjligt att släppa dessa nya identifieringar snabbt om du vill aktivera Azure ATP-kunder kan dra nytta av nya identifieringar så snart som möjligt.

Dessa identifieringar är märkta med en symbol i förhandsversion, för att identifiera nya identifieringar och när de är nybörjare på produkten. Om du inaktiverar förhandsversion identifieringar de visas inte i Azure ATP-konsolen – inte i tidslinjen eller i entitetsprofiler - och kommer inte att öppna nya aviseringar.

![Förhandsgranska identifiering vpn](./media/preview-detection-vpn.png) 

Som standard aktiveras förhandsversion identifieringar i Azure ATP. 

Inaktivera förhandsgranskning identifieringar:

1. I Azure ATP-konsolen klickar du på kugghjulet för inställningar.
2. I den vänstra menyn under förhandsgranskning klickar du på **identifieringar**.
3. Använd skjutreglaget för att aktivera eller inaktivera förhandsgranskning identifieringar.
 
![förhandsversion av identifieringar](./media/preview-detections.png) 


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




## <a name="managing-suspicious-activities"></a>Hantera misstänkta aktiviteter
Du kan ändra status för en misstänkt aktivitet genom att klicka på den misstänkta aktiviteten aktuella status och välja något av följande **öppna**, **ignorerad**, **stängd**, eller **bort**.
Du gör det genom att klicka på de tre punkterna i det övre högra hörnet för en specifik misstänkt aktivitet så att listan över tillgängliga åtgärder visas.

![Azure ATP-åtgärder för misstänkta aktiviteter](./media/atp-sa-actions.png)

**Status för misstänkt aktivitet**

-   **Öppna**: Alla nya misstänkta aktiviteter visas i den här listan.

-   **Stäng**: används för att spåra misstänkta aktiviteter som du har identifierat, undersökt och åtgärdat för begränsade.

    > [!NOTE]
    > Om samma aktivitet identifieras igen inom en kort tidsperiod, kan Azure ATP öppna en stängd aktivitet.

-   **Ignorera**: Används för att ignorera en aktivitet tillsvidare, så att du bara aviseras igen om det finns en ny instans. Det innebär som om det finns en liknande avisering Azure ATP inte öppna den igen. Men om aviseringen stoppas under sju dagar, och sedan registreras igen, du aviseras igen.

- **Ta bort**: Om du tar bort en avisering tas bort från systemet och från databasen och du kommer inte att återställa den. När du klickar på Ta bort kan du ta bort alla misstänkta aktiviteter av samma typ.

- **Undanta**: Möjligheten att undanta en entitet så att den inte genererar fler aviseringar av en viss typ. Du kan till exempel ange Azure ATP att undanta en specifik entitet (användare eller dator) utlöser aviseringar igen för en viss typ av misstänkt aktivitet, till exempel en specifik administratör som kör fjärrkod eller ett säkerhetsgenomsökningsverktyg som utför DNS-rekognosering. Förutom att lägga till undantag direkt för den misstänkta aktiviteten när den identifieras på tidslinjen kan du även gå till **Undantag** från sidan Konfiguration och, för varje misstänkt aktivitet, manuellt lägga till och ta bort undantagna enheter eller undernät (till exempel för Pass-the-Ticket). 

> [!NOTE]
> Konfigurationssidorna kan bara ändras av Azure ATP-administratörer.


## <a name="see-also"></a>Se även

- [Arbeta med Azure ATP-arbetsyteportalen](workspace-portal.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)