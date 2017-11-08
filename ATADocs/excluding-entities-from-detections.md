---
title: "Exkludera entiteter från att identifieras i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du stoppar ATA från att identifiera specifika enhetsaktiviteter som misstänkta"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f9fce36074b5c31e35f95f028b856b18fa3bae0b
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="excluding-entities-from-detections"></a>Exkludera entiteter från att identifieras
Den här artikeln beskriver hur du exkludera entiteter från utlöst aviseringar för att minimera true ofarlig positiva identifieringar men samtidigt, se till att upptäcka true positiva identifieringar. För att hålla ATA från att vara mycket om aktiviteter som från specifika användare, kan vara en del av din normala takt till företag, kan quiet - eller utesluta - specifika entiteter från utlöst aviseringar.

Det kan t.ex. handla om att du har en säkerhetsskanner som gör DNS-rekognoseringar eller en administratör som fjärrkör skript på domänkontrollanten, och att dessa aktiviteter är sanktionerade som ett naturligt inslag i det normala IT-arbetet i din organisation.

Så här exkluderar du entiteter så att de inte utlöser aviseringar i ATA:

Du kan exkludera entiteter på två sätt. Antingen från själva den misstänkta aktiviteten, eller från fliken **Undantag** på sidan **Konfiguration**.

- **Från den misstänkta aktiviteten**: I den misstänkta aktiviteten tidslinje, när du får en avisering för en aktivitet för en användare eller dator eller IP-adress som är tillåtet att utföra en viss aktivitet och kan göra det ofta, högerklicka på de tre punkterna i slutet av raden för misstänkt aktivitet på den enheten och välj **Stäng och utelämna**. <br></br>Användare, dator eller IP-adress läggs till i undantagslistan för den misstänkta aktiviteten. Den stänger den misstänkta aktiviteten och visas inte längre i den **öppna** -listan i den **misstänkt aktivitet tidslinjen**.

    ![Exkludera entitet](./media/exclude-in-sa.png)

- **Från konfigurationssidan**: vill granska eller ändra några undantag: under **Configuration**, klickar du på **undantag** och välj sedan den misstänkta aktiviteten som  **Känsligt kontoautentiseringsuppgifter exponerade**.

    ![Konfiguration av undantag](./media/exclusions-config-page.png)

Ta bort en entitet från konfigurationen **Undantag**: klicka på minustecknet intill entitetens namn och klicka sedan på **Spara** längst ned på sidan.

Vi rekommenderar att du lägger till undantag till identifieringar först efter det att du har fått aviseringar av den aktuella typen och fastställt att de är ofarliga positiva identifieringar. 

> [!NOTE]
> Av säkerhetsskäl är det inte möjligt att ange undantag för alla identifieringar. 

Vissa av identifieringarna ger tips som kan hjälpa dig att avgöra vad som ska undantas. 

Varje undantag beror på kontexten, i vissa du kan ange användare medan andra kan du ange datorer eller IP-adresser. 

När du har möjlighet att exkludera en IP-adress eller en dator behöver kan du undanta en av -du inte ange båda.

> [!NOTE]
> Konfigurationssidorna kan bara ändras av ATA-administratörer.


## <a name="see-also"></a>Se även
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändra ATA-konfiguration](modifying-ata-center-configuration.md)
