---
title: Vad är nytt i ATA version 1.9. | Microsoft Docs
description: Visar en lista över nyheter i ATA version 1.9 tillsammans med kända problem
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: f4a0776d52a69ba519e5cfdd0befb6bbd39d73c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202399"
---
# <a name="whats-new-in-ata-version-19"></a>Vad är nytt i ATA version 1.9.

Den senast uppdaterade versionen av ATA går att [ladda ned från Download Center](https://www.microsoft.com/download/details.aspx?id=56725). Det går också att ladda ned den fullständig versionen från [utvärderingscentret](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Dessa versionsanmärkningar innehåller information om uppdateringar, nya funktioner, felkorrigeringar och kända problem i den här versionen av Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nya och uppdaterade identifieringar

-  **Skapa en misstänkt tjänst**: angripare försöker köra en misstänkt tjänst i nätverket. Nu genererar ATA en varning när den identifierar någon kör en ny tjänst som verkar misstänkt bör på en domänkontrollant. Denna identifiering är baserat på händelser (inte nätverkstrafik), mer information, se den [misstänkt aktivitet guiden](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nya rapporter som underlättar dina undersökningar 

-   Den [ **lösenord exponeras i klartext** ](reports.md) kan du identifiera när konton känsliga och icke-känsliga, skickar autentiseringsuppgifter i klartext. På så sätt kan du undersöka och minska användningen av enkla LDAP-bindning i din miljö, förbättra nivå för nätverkssäkerhet. Den här rapporten ersätter tjänsten och aviseringar för känsligt konto klartext misstänkt aktivitet.

- Den [ **Lateral förflyttning sökvägar till känsliga konton** ](reports.md) visar känsliga konton som exponeras via lateral förflyttning sökvägar. På så sätt kan du minimera dessa sökvägar och skydda ditt nätverk för att minimera ytan risken för angrepp. Detta gör att du kan förhindra lateral förflyttning så att angripare inte kan flytta över nätverket mellan användare och datorer tills de har nått högsta vinsten virtuella säkerhet: dina känsliga admin-autentiseringsuppgifter.

## <a name="improved-investigation"></a>Förbättrad undersökning

-  ATA 1,9 innehåller en ny och förbättrad [entitetsprofilen](entity-profiles.md). Du får en instrumentpanel som utformats för fullständig djupdykning undersökning av användare, resurser som de används och deras tidigare entitetsprofilen. Entitetsprofilen kan du identifiera känsliga användare som är tillgängliga via lateral förflyttning sökvägar. 

-   ATA 1,9 gör det möjligt att [manuellt tagga grupper](tag-sensitive-accounts.md) eller konton som är känsliga att förbättra identifieringar. Den här märkning påverkar många ATA-identifieringar, till exempel känsliga grupp ändring identifiering och lateral förflyttning sökväg förlitar sig på vilka grupper och konton anses vara känslig.

## <a name="performance-improvements"></a>Prestandaförbättringar

- ATA Center-infrastrukturen har förbättrats för prestanda: aggregerade visningen av trafiken kan optimering av processor- och paket pipeline och återanvänder sockets till domänkontrollanter för att minimera SSL-sessioner till domänkontrollanten.



## <a name="additional-changes"></a>Ytterligare ändringar

- När du har installerat en ny version av ATA i [ **nyheter** ](working-with-ata-console.md) ikon som visas i verktygsfältet så att du vet vad som ändrats i den senaste versionen. Det ger dig också med en länk till djupgående version changelog.


## <a name="removed-and-deprecated-features"></a>Borttagna och föråldrade funktioner

- Den **bruten litar på misstänkt aktivitet** aviseringen har tagits bort.
- Lösenord i klartext misstänkt aktivitet har tagits bort. Den har ersatts med den [ **lösenord exponeras i klartext rapporten**](reports.md).



## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.9 – Migreringsguide](ata-update-1.9-migration-guide.md)

