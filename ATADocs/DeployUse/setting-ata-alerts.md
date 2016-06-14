---
# required metadata

title: Konfigurera ATA-aviseringar | Microsoft Advanced Threat Analytics
description: Beskriver hur du får ATA att meddela dig (via e-post eller vidarebefordran av ATA-händelser) när det upptäcker misstänkta aktiviteter 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Konfigurera ATA-meddelanden
ATA kan meddela dig när det upptäcker misstänkt aktivitet, antingen via e-post eller genom att använda vidarebefordran av ATA-händelser och vidarebefordra händelsen till SIEM/syslog-servern. Innan du väljer vilka meddelanden du vill ta emot måste du [konfigurera e-postservern och Syslog-servern](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-postmeddelanden innehåller en länk som tar användaren direkt till den misstänkta aktivitet som har identifierats. Värdnamnsdelen i länken kommer från inställningen för ATA-konsolens URL på sidan för ATA Center. ATA-konsolens URL är som standard den IP-adress som väljs vid installation av ATA Center.  Om du ska konfigurera e-postaviseringar rekommenderar vi att du använder en FQDN som URL för ATA-konsolen.
> -   Meddelanden skickas från ATA Center till antingen SMTP-servern eller Syslog-servern.

Ange följande för att ta emot e-postaviseringar:


1. I ATA-konsolen väljer du inställningsalternativ i verktygsfältet och väljer **Konfiguration**.
![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

2. Välj **Meddelanden**.
3. Under **E-postaviseringar** använder du knapparna för att välja vilka meddelanden som ska skickas:


    - Ny misstänkt aktivitet har identifierats
    - Nytt hälsoproblem har identifierats
    - Ny programvaruuppdatering är tillgänglig

4. Ange vilka mottagare som ska ta emot meddelanden via e-post.

    [Obs!] E-postaviseringar för misstänkta aktiviteter skickas endast när den misstänkta aktiviteten skapas.


5. Klicka på **Spara**.

Ange följande för att ta emot Syslog-aviseringar:


1. I ATA-konsolen väljer du inställningsalternativ i verktygsfältet och väljer **Konfiguration**.
![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

2. Välj **Meddelanden**.
3. Under **Syslog-aviseringar** använder du knapparna för att välja vilka meddelanden som ska skickas:


    - Ny misstänkt aktivitet har identifierats
    - Befintlig misstänkt aktivitet har uppdaterats
    - Nytt hälsoproblem har identifierats
5. Klicka på **Spara**.
![Bild för inställning av ATA-meddelanden](media/ATA-notification-settings.png)




## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->

