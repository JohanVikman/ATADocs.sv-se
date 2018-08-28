---
title: Ställ in Advanced Threat Analytics-aviseringar | Microsoft Docs
description: Beskriver hur du ställer in ATA-meddelanden så att du meddelas när misstänkta aktiviteter identifieras.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 60e02ef1aff6b16bc56b12b8883ca2f5ed4a1f74
ms.sourcegitcommit: 56886d06abd25035ffc9885c69aca9b0ebf14abc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2018
ms.locfileid: "42903914"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="set-ata-notifications"></a>Konfigurera ATA-meddelanden
ATA kan meddela dig när det upptäcker misstänkt aktivitet, antingen via e-post eller genom att använda vidarebefordran av ATA-händelser och vidarebefordra händelsen till SIEM/syslog-servern. Innan du väljer vilka meddelanden du vill ta emot måste du [konfigurera e-postservern och Syslog-servern](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-postmeddelanden innehåller en länk som leder användaren direkt till den misstänkta aktiviteten som har identifierats. Värdnamnsdelen i länken kommer från inställningen för ATA-konsolens URL på sidan för ATA Center. ATA-konsolens URL är som standard den IP-adress som väljs vid installation av ATA Center. Om du ska konfigurera e-postaviseringar, rekommenderas att du använder en FQDN som ATA-konsolens URL.
> -   Meddelanden skickas från ATA Center till antingen SMTP-servern eller Syslog-servern.


Om du vill ta emot aviseringar måste du ange följande parametrar:


1. I ATA-konsolen väljer du inställningsalternativ i verktygsfältet och väljer **Konfiguration**.
    
    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)
    
1. Välj **Meddelanden** under **Notifications & Reports** (Meddelanden och rapporter).
1. Under **E-postaviseringar** anger du vilka meddelanden som ska skickas via e-post – nya misstänkta aktiviteter och nya hälsorelaterade problem. Du kan ange separata e-postadresser som misstänkta aktiviteter och hälsorelaterade aviseringar ska skickas till, så att till exempel aviseringar om misstänkt aktivitet skickas till din säkerhetsanalytiker och aviseringar om hälsorelaterade problem till IT-administratören.
    >   [!NOTE]
    >   E-postaviseringar för misstänkta aktiviteter skickas endast när den misstänkta aktiviteten skapas.
1. Under **Syslog-aviseringar**, ange vilka meddelanden ska skickas till Syslog-servern – nya misstänkta aktiviteter, uppdaterade misstänkta aktiviteter och nya hälsorelaterade problem.
1. Klicka på **Spara**.
    
    ![Bild för inställning av ATA-e-postaviseringar](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
