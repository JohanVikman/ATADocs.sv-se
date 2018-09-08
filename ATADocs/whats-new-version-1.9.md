---
title: Vad är nytt i ATA version 1.9 | Microsoft Docs
description: Visar en lista över nyheter i ATA version 1.9 tillsammans med kända problem
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: ddb93c2776dbb6e076314051068c4ca3544db756
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166620"
---
# <a name="whats-new-in-ata-version-19"></a>Vad är nytt i ATA version 1.9

Den senast uppdaterade versionen av ATA går att [ladda ned från Download Center](https://www.microsoft.com/download/details.aspx?id=56725). Det går också att ladda ned den fullständig versionen från [utvärderingscentret](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Dessa versionsanmärkningar innehåller information om uppdateringar, nya funktioner, felkorrigeringar och kända problem i den här versionen av Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nya och uppdaterade identifieringar

-  **Misstänkt skapande av tjänst**: angripare försöker köra en misstänkt tjänst i ditt nätverk. Nu genererar ATA en varning när den identifierar någon kör en ny tjänst som verkar misstänkt bör på en domänkontrollant. Den här identifieringen baseras på händelser (inte trafik), mer information, se den [guide för misstänkt aktivitet](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nya rapporter som underlättar dina undersökningar 

-   Den [ **lösenord som exponerats i klartext** ](reports.md) kan du identifiera när konton känsliga och ickekänsliga, skickar autentiseringsuppgifter i klartext. På så sätt kan du undersöka och minska användningen av enkel LDAP-bindning i din miljö kan förbättra din nivå för nätverkssäkerhet. Den här rapporten ersätter service och aviseringar för känsligt konto klartext misstänkt aktivitet.

- Den [ **laterala rörelsebanor till känsliga konton** ](reports.md) visar en lista över känsliga konton som exponeras via lateral förflyttning. På så sätt kan du minska dessa sökvägar och förstärka nätverket för att minimera risken attack surface. Detta gör att du kan förhindra lateral förflyttning så att angripare inte kan flytta över nätverket mellan användare och datorer tills de når virtual Secure högsta vinsten: dina känsliga administratörsautentiseringsuppgifter för kontot.

## <a name="improved-investigation"></a>Förbättrad undersökning

-  ATA 1.9 innehåller en ny och förbättrad [entitetsprofilen](entity-profiles.md). Entitetsprofilen ger dig en instrumentpanel som utformats för djupgående om undersökning av användare, vilka resurser de använde och deras historik. Entitetsprofilen hjälper dig att identifiera känsliga användare som är tillgängliga via lateral förflyttning. 

-   ATA 1.9 gör det möjligt att [manuellt tagga grupper](tag-sensitive-accounts.md) eller konton som känsliga för att förbättra identifieringar. Den här taggning påverkan många ATA-identifieringar, till exempel känsliga grupp ändring av identifiering och lateral rörelsesökväg är beroende av vilka grupper och konton betraktas som känslig.

## <a name="performance-improvements"></a>Prestandaförbättringar

- ATA Center-infrastrukturen har fått förbättrad prestanda: aggregerade vyn trafik som gör det möjligt för optimering av processor- och paket pipeline och återanvänder sockets till domänkontrollanterna för att minimera SSL-sessioner till domänkontrollanten.



## <a name="additional-changes"></a>Ytterligare ändringar

- När en ny version av ATA har installerats måste den [ **nyheter** ](working-with-ata-console.md) ikon som visas i verktygsfältet för att låta dig veta vad som ändrats i den senaste versionen. Det ger dig också med en länk till djupgående version-ändringsloggen.


## <a name="removed-and-deprecated-features"></a>Borttagna och föråldrade funktioner

- Den **bruten förtroende misstänkt aktivitet** aviseringen har tagits bort.
- De lösenord som exponerats i klartext misstänkt aktivitet har tagits bort. Den har ersatts med den [ **lösenord som exponerats i klartext rapporten**](reports.md).



## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.9 – Migreringsguide](ata-update-1.9-migration-guide.md)

