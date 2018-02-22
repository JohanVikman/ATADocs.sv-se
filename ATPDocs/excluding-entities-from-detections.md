---
title: "Exkludera entiteter från identifieringar i Azure Advanced Threat Protection | Microsoft Docs"
description: "Beskriver hur du stoppar Azure ATP inte kan identifiera specifika enheten aktiviteter som misstänkt"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="excluding-entities-from-detections"></a>Exkludera entiteter från att identifieras
Den här artikeln beskriver hur du exkludera entiteter från utlöst aviseringar för att minimera true ofarlig positiva identifieringar men samtidigt, se till att upptäcka true positiva identifieringar. För att skydda Azure ATP från att vara mycket om aktiviteter som från specifika användare, kan vara en del av din normala takt till företag du quiet - eller utesluta - specifika entiteter från utlöst aviseringar.

Det kan t.ex. handla om att du har en säkerhetsskanner som gör DNS-rekognoseringar eller en administratör som fjärrkör skript på domänkontrollanten, och att dessa aktiviteter är sanktionerade som ett naturligt inslag i det normala IT-arbetet i din organisation. Mer information om Azure ATP identifieringar för att avgöra vilka enheter som ska undantas finns i [misstänkta aktiviteter guiden](suspicious-activity-guide.md).

För att utesluta entiteter från utlöst aviseringar i Azure ATP:

Du kan exkludera entiteter på två sätt. Antingen från själva den misstänkta aktiviteten, eller från fliken **Undantag** på sidan **Konfiguration**.

- **Från den misstänkta aktiviteten**: I den misstänkta aktiviteten tidslinje, när du får en avisering för en aktivitet för en användare eller dator eller IP-adress som är tillåtet att utföra en viss aktivitet och kan göra det ofta, högerklicka på de tre punkterna i slutet av raden för misstänkt aktivitet på den enheten och välj **Stäng och utelämna**. <br></br>Användare, dator eller IP-adress läggs till i undantagslistan för den misstänkta aktiviteten. Den stänger den misstänkta aktiviteten och visas inte längre i den **öppna** -listan i den **misstänkt aktivitet tidslinjen**.

    ![Exkludera entitet](./media/exclude-in-sa.png)

- **Från konfigurationssidan**: vill granska eller ändra några undantag: under **Configuration**, klickar du på **undantag** och välja den misstänkta aktiviteten, till exempel **DNS rekognosering**.

    ![Konfiguration av undantag](./media/exclusions.png)

Att lägga till en entitet från den **undantag** konfiguration: Ange entitetsnamnet och klicka sedan på plustecknet och klicka sedan på **spara** längst ned på sidan.

Ta bort en entitet från konfigurationen **Undantag**: klicka på minustecknet intill entitetens namn och klicka sedan på **Spara** längst ned på sidan.

Vi rekommenderar att du lägger till undantag till identifieringar först efter det att du har fått aviseringar av den aktuella typen och fastställt att de är ofarliga positiva identifieringar. 

> [!NOTE]
> Av säkerhetsskäl är det inte möjligt att ange undantag för alla identifieringar. 

Vissa av identifieringarna ger tips som kan hjälpa dig att avgöra vad som ska undantas. 

Varje undantag beror på kontexten, i vissa du kan ange användare medan andra kan du ange datorer eller IP-adresser. 

När du har möjlighet att exkludera en IP-adress eller en dator behöver kan du undanta en av -du inte ange båda.

> [!NOTE]
> Konfigurationssidorna kan bara ändras av Azure ATP administratörer.


## <a name="see-also"></a>Se även

- [Integrering med Windows Defender ATP](integrate-wd-atp.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)