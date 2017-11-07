---
title: "Exkludera entiteter från att identifieras i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du stoppar ATA från att identifiera specifika enhetsaktiviteter som misstänkta"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c185060a4fb889121c6a02b353fb0d176f0c9274
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/06/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="excluding-entities-from-detections"></a>Exkludera entiteter från att identifieras
Det här avsnittet beskriver hur du exkludera entiteter från att utlösa aviseringar, så att du minimerar de ofarliga positiva träffarna samtidigt som du ser till att identifiera de sanna positiva träffarna. Om du vill undvika ATA gör för mycket onödigt väsen av aktiviteter, som för vissa användare kan vara naturliga inslag i den dagliga verksamheten, så kan du tysta, eller exkludera, vissa entiteter, så att de inte genererar några aviseringar.

Det kan t.ex. handla om att du har en säkerhetsskanner som gör DNS-rekognoseringar eller en administratör som fjärrkör skript på domänkontrollanten, och att dessa aktiviteter är sanktionerade som ett naturligt inslag i det normala IT-arbetet i din organisation.

Så här exkluderar du entiteter så att de inte utlöser aviseringar i ATA:

Du kan exkludera entiteter på två sätt. Antingen från själva den misstänkta aktiviteten, eller från fliken **Undantag** på sidan **Konfiguration**.

- **Från den misstänkta aktiviteten**: Högerklicka, i den misstänkta aktivitetens tidslinje, på de tre punkterna i slutet av raden för den misstänkta aktiviteten på enheten, och välj **Stäng och undanta**. <br></br>Detta medför att användaren, datorn eller IP-adressen läggs till i undantagslistan för den misstänkta aktiviteten. Det medför även att den misstänkta aktiviteten stängs och inte längre listas i händelselistan **Öppna** på **tidslinjen för misstänkta aktiviteter**.

    ![Exkludera entitet](./media/exclude-in-sa.png)

- **Från sidan Konfiguration**: Om du vill granska eller ändra eventuella gör du så här: klicka på **Undantag**under **Konfiguration** och välj sedan den misstänkta aktiviteten, t.ex. **Exponerade känsliga kontoautentiseringsuppgifter**.

    ![Konfiguration av undantag](./media/exclusions-config-page.png)

Ta bort en entitet från konfigurationen **Undantag**: klicka på minustecknet intill entitetens namn och klicka sedan på **Spara** längst ned på sidan.

Vi rekommenderar att du lägger till undantag till identifieringar först efter det att du har fått aviseringar av den aktuella typen och fastställt att de är ofarliga positiva identifieringar. 

> [!NOTE]
> Av säkerhetsskäl är det inte möjligt att ange undantag för alla identifieringar. 

Vissa av identifieringarna ger tips som kan hjälpa dig att avgöra vad som ska undantas. 

Varje undantag beror på kontexten. För vissa kan du ange användare, och för andra datorer eller IP-adresser. 

När du har möjlighet att exkludera en IP-adress eller en dator, räcker det att du exkluderar enbart den ena - du behöver inte ange båda.

> [!NOTE]
> Konfigurationssidorna kan bara ändras av ATA-administratörer.


## <a name="see-also"></a>Se även
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändra ATA-konfiguration](modifying-ata-center-configuration.md)
