---
title: Ange Azure Advanced Threat Protection-meddelanden | Microsoft Docs
description: Beskriver hur du ställer in Azure ATP aviseringar så att du meddelas när misstänkta aktiviteter identifieras.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 85fe887df373d8132df932cdb3d1eaf5ab954a1d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445982"
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="set-azure-atp-notifications"></a>Ange Azure ATP meddelanden

Azure ATP kan meddela dig när det upptäcker misstänkt aktivitet eller en hälsoavisering via e-post. 

Ange följande parametrar för att ta emot meddelanden till en specifik e-postadress:


1. I Azure ATP arbetsytan portal, väljer du inställningsalternativ i verktygsfältet och välj **Configuration**.

![Azure ATP ikon för konfigurationsinställningar](media/atp-config-menu.png)

2. Klicka på **meddelanden**.
3. Under **e-postaviseringar**, ange vilka meddelanden som ska skickas via e-post - de kan skickas för nya aviseringar (misstänkta aktiviteter) och nya problem. 
 
 >  [!NOTE]
 >   E-postaviseringar för misstänkta aktiviteter skickas endast när den misstänkta aktiviteten skapas.

5. Klicka på **Spara**.

 ![Azure ATP-meddelanden](media/atp-notifications.png)



## <a name="see-also"></a>Se även

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Ange inställningar för Syslog](setting-syslog.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)