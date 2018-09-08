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
ms.openlocfilehash: 080b3469c862d4063db5a4832f63dd3614905fac
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166073"
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

5. Klicka på **Spara**.

 ![Azure ATP-aviseringar](media/atp-notifications.png)



## <a name="see-also"></a>Se även

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Ange Syslog-inställningar](setting-syslog.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)