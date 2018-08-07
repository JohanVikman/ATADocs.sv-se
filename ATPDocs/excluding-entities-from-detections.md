---
title: Exkludera entiteter från identifieringar i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver hur du stoppar Azure ATP från att identifiera specifika enhetsaktiviteter som misstänkta
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a91ebbe3811aeefe6fcef660807976794513f32
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567839"
---
*Gäller för: Azure Avancerat skydd*



# <a name="excluding-entities-from-detections"></a>Exkludera entiteter från att identifieras
Den här artikeln förklarar hur du exkludera entiteter från att utlösa aviseringar, så att du minimerar de ofarliga positiva men samtidigt, se till att du ser de sanna positiva träffarna. För att skydda Azure ATP från att vara väsen av aktiviteter som för vissa användare kan vara en del av företag om du vill kan du tysta, eller exkludera, vissa entiteter från att skicka aviseringar.

Det kan t.ex. handla om att du har en säkerhetsskanner som gör DNS-rekognoseringar eller en administratör som fjärrkör skript på domänkontrollanten, och att dessa aktiviteter är sanktionerade som ett naturligt inslag i det normala IT-arbetet i din organisation. Läs mer om Azure ATP-identifieringar för att avgöra vilka entiteter för att undanta den [misstänkta aktiviteter guiden](suspicious-activity-guide.md).

Du exkludera entiteter från att skicka aviseringar i Azure ATP:

Du kan exkludera entiteter på två sätt. Antingen från själva den misstänkta aktiviteten, eller från fliken **Undantag** på sidan **Konfiguration**.

- **Från den misstänkta aktiviteten**: I den misstänkta aktivitetens tidslinje, när du får en avisering på en aktivitet för en användare eller dator eller IP-adress som är tillåtet att utföra viss aktivitet och kan göra det ofta, högerklicka på de tre punkterna i slutet av raden för den misstänkta aktiviteten på denna entitet och välj **Stäng och undanta**. <br></br>Den användare, dator eller IP-adressen läggs till i undantagslistan för den misstänkta aktiviteten. Den sluter misstänkt aktivitet och den inte längre visas i den **öppna** händelselistan den **tidslinjen för misstänkta aktiviteter**.

    ![Exkludera entitet](./media/exclude-in-sa.png)

- **Från sidan konfiguration**: vill granska eller ändra eventuella gör: under **Configuration**, klickar du på **undantag** och välj sedan den misstänkta aktiviteten, till exempel **DNS rekognosering**.

    ![Konfiguration av undantag](./media/exclusions.png)

Att lägga till en entitet från den **undantag** konfiguration: ange enhetens namn och klicka sedan på plustecknet och klicka sedan på **spara** längst ned på sidan.

Ta bort en entitet från konfigurationen **Undantag**: klicka på minustecknet intill entitetens namn och klicka sedan på **Spara** längst ned på sidan.

Vi rekommenderar att du lägger till undantag till identifieringar först efter det att du har fått aviseringar av den aktuella typen och fastställt att de är ofarliga positiva identifieringar. 

> [!NOTE]
> Av säkerhetsskäl är det inte möjligt att ange undantag för alla identifieringar. 

Vissa av identifieringarna ger tips som kan hjälpa dig att avgöra vad som ska undantas. 

Varje undantag beror på kontexten, i vissa du kan ange användare, och så att andra kan du ange datorer eller IP-adresser. 

När du har möjlighet att exkludera en IP-adress eller en dator, behöver du kan utesluta ena eller den andra - du inte ange båda.

> [!NOTE]
> Konfigurationssidorna kan bara ändras av Azure ATP-administratörer.


## <a name="see-also"></a>Se även

- [Integrera med Windows Defender ATP](integrate-wd-atp.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)