---
title: Exkludera entiteter från att identifieras i Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du stoppar ATA från att identifiera specifika enhetsaktiviteter som misstänkta
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3b731593e08cfb1b52e01b83f52b0403dd74aadc
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133046"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="excluding-entities-from-detections"></a>Exkludera entiteter från att identifieras
Den här artikeln förklarar hur du exkludera entiteter från att utlösa aviseringar, så att du minimerar de ofarliga positiva men samtidigt, se till att du ser de sanna positiva träffarna. För att hålla ATA från att vara väsen av aktiviteter som för vissa användare kan vara en del av företag om du vill kan du tysta, eller exkludera, vissa entiteter från att skicka aviseringar.

Det kan t.ex. handla om att du har en säkerhetsskanner som gör DNS-rekognoseringar eller en administratör som fjärrkör skript på domänkontrollanten, och att dessa aktiviteter är sanktionerade som ett naturligt inslag i det normala IT-arbetet i din organisation.

Så här exkluderar du entiteter så att de inte utlöser aviseringar i ATA:

Du kan exkludera entiteter på två sätt. Antingen från själva den misstänkta aktiviteten, eller från fliken **Undantag** på sidan **Konfiguration**.

- **Från den misstänkta aktiviteten**: I den misstänkta aktivitetens tidslinje, när du får en avisering på en aktivitet för en användare eller dator eller IP-adress som är tillåtet att utföra viss aktivitet och kan göra det ofta, högerklicka på de tre punkterna i slutet av raden för den misstänkta aktiviteten på denna entitet och välj **Stäng och undanta**. <br></br>Den användare, dator eller IP-adressen läggs till i undantagslistan för den misstänkta aktiviteten. Den sluter misstänkt aktivitet och den inte längre visas i den **öppna** händelselistan den **tidslinjen för misstänkta aktiviteter**.

    ![Exkludera entitet](./media/exclude-in-sa.png)

- **Från sidan konfiguration**: vill granska eller ändra eventuella gör: under **Configuration**, klickar du på **undantag** och välj sedan den misstänkta aktiviteten, till exempel  **Känsliga kontouppgifter avslöjas**.

    ![Konfiguration av undantag](./media/exclusions-config-page.png)

Ta bort en entitet från konfigurationen **Undantag**: klicka på minustecknet intill entitetens namn och klicka sedan på **Spara** längst ned på sidan.

Vi rekommenderar att du lägger till undantag till identifieringar först efter det att du har fått aviseringar av den aktuella typen och fastställt att de är ofarliga positiva identifieringar. 

> [!NOTE]
> Av säkerhetsskäl är det inte möjligt att ange undantag för alla identifieringar. 

Vissa av identifieringarna ger tips som kan hjälpa dig att avgöra vad som ska undantas. 

Varje undantag beror på kontexten, i vissa du kan ange användare, och så att andra kan du ange datorer eller IP-adresser. 

När du har möjlighet att exkludera en IP-adress eller en dator, behöver du kan utesluta ena eller den andra - du inte ange båda.

> [!NOTE]
> Konfigurationssidorna kan bara ändras av ATA-administratörer.


## <a name="see-also"></a>Se även
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändra ATA-konfiguration](modifying-ata-center-configuration.md)
