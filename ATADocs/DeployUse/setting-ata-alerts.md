---
title: "Ställ in Advanced Threat Analytics-aviseringar | Microsoft Docs"
description: "Beskriver hur du ställer in ATA-meddelanden så att du meddelas när misstänkta aktiviteter identifieras."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 782c066e6a7ef8a5da9e2b8ceb16742da6f52506


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="set-ata-notifications"></a>Konfigurera ATA-meddelanden
ATA kan meddela dig när det upptäcker misstänkt aktivitet, antingen via e-post eller genom att använda vidarebefordran av ATA-händelser och vidarebefordra händelsen till SIEM/syslog-servern. Innan du väljer vilka meddelanden du vill ta emot måste du [konfigurera e-postservern och Syslog-servern](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-postmeddelanden innehåller en länk som tar användaren direkt till den misstänkta aktivitet som har identifierats. Värdnamnsdelen i länken kommer från inställningen för ATA-konsolens URL på sidan för ATA Center. ATA-konsolens URL är som standard den IP-adress som väljs vid installation av ATA Center.  Om du ska konfigurera e-postaviseringar rekommenderar vi att du använder en FQDN som URL för ATA-konsolen.
> -   Meddelanden skickas från ATA Center till antingen SMTP-servern eller Syslog-servern.

## <a name="mail-notifications"></a>E-postaviseringar
Ange följande för att ta emot e-postaviseringar:


1. I ATA-konsolen väljer du inställningsalternativ i verktygsfältet och väljer **Konfiguration**.
![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

2. Under sektionen **Meddelanden**, välj **Inställningar**.
3. Under **E-postmottagare** ange vilka mottagare som ska ta emot aviseringar via e-post.
>   [!NOTE]
>   E-postaviseringar för misstänkta aktiviteter skickas endast när den misstänkta aktiviteten skapas.

4. Under **Avisera bör:** använder du knapparna för att välja vilka meddelanden som ska skickas:
  - Ny misstänkt aktivitet har identifierats
  - Nytt hälsoproblem har identifierats
  - Ny programvaruuppdatering är tillgänglig

5. Klicka på **Spara**.

![Bild för inställning av ATA-e-postaviseringar](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Syslog-meddelande

Ange följande för att ta emot Syslog-aviseringar:


1. I ATA-konsolen väljer du inställningsalternativ i verktygsfältet och väljer **Konfiguration**.
![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

2. Under sektionen **Meddelanden**, välj **Inställningar**.
3. Under **Syslog-aviseringar** använder du knapparna för att välja vilka meddelanden som ska skickas:


    - Ny misstänkt aktivitet har identifierats
    - Befintlig misstänkt aktivitet har uppdaterats
    - Nytt hälsoproblem har identifierats
5. Klicka på **Spara**.

![Bild för inställning av ATA-meddelanden](media/ATA-syslog-notification-settings-1.7.png)




## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


