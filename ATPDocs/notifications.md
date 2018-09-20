---
title: Konfigurera Azure Advanced Threat Protection-meddelanden | Microsoft Docs
description: Beskriver hur du ställer in Azure ATP-aviseringar så att du meddelas när misstänkta aktiviteter identifieras.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362433"
---
*Gäller för: Azure Avancerat skydd*


# <a name="set-azure-atp-notifications"></a>Ange Azure ATP-aviseringar

Azure ATP kan meddela dig när det upptäcker misstänkt aktivitet eller en hälsovarning via e-post. 

Ange följande parametrar för att ta emot meddelanden till en specifik e-postadress:


1. I Azure ATP-arbetsyteportalen, väljer du inställningsalternativ i verktygsfältet och välj **Configuration**.

![Azure ATP ikon för konfigurationsinställningar](media/atp-config-menu.png)

2. Klicka på **meddelanden**.
3. Under **e-postaviseringar**, ange vilka meddelanden ska skickas via e-post – de kan skickas för nya aviseringar (misstänkta aktiviteter) och nya hälsorelaterade problem. 
 
 >  [!NOTE]
 >   E-postaviseringar för misstänkta aktiviteter skickas endast när den misstänkta aktiviteten skapas.
 
4. Klicka på **Spara**.

 ![Azure ATP-aviseringar](media/atp-notifications.png)



## <a name="see-also"></a>Se även

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Ange Syslog-inställningar](setting-syslog.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
