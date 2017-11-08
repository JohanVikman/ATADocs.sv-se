---
title: "Ställ in inställningar för e-postmeddelanden i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du får ATA att meddela dig (via e-post eller vidarebefordran av ATA-händelser) när det upptäcker misstänkta aktiviteter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 70e076dea5b1ff200b1b9f2a6529a76c175c7a88
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="provide-ata-with-your-email-server-settings"></a>Ange e-postserverinställningar för ATA
ATA kan meddela dig när det identifierar en misstänkt aktivitet. Om ATA ska kunna skicka e-postaviseringar måste du först konfigurera **E-postserverinställningar**.

1.  På ATA Center-servern klickar du på ikonen **Microsoft Advanced Threat Analytics Management** på skrivbordet.

2.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

3.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)

4.  I avsnittet **Meddelanden** under **E-postserver**, anger du följande information:

    |Fält|Beskrivning|Värde|
    |---------|---------------|---------|
    |SMTP-serverslutpunkt (krävs)|Ange det fullständiga domännamnet för SMTP-servern och du kan också ändra portnumret (standard 25).|Exempel:<br />smtp.contoso.com|
    |SSL|Växla SSL om SMTP-servern kräver SSL. **Obs:** om du aktiverar SSL måste du också behöva ändra portnumret.|Standardvärdet är inaktiverat|
    |Autentisering|Aktivera om SMTP-servern kräver autentisering. **Obs:** om du aktiverar autentisering måste du ange ett användarnamn och lösenord för ett e-postkonto som har behörighet att ansluta till SMTP-servern.|Standardvärdet är inaktiverat|
    |Skicka från (krävs)|Ange en e-postadress som e-postmeddelandet ska skickas från.|Exempel:<br />ATA@contoso.com|
    ![Bild för e-postserverinställningar i ATA](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Ange Syslog-serverinställningar för ATA
ATA kan meddela dig när systemet identifierar misstänkt aktivitet genom att skicka aviseringen till Syslog-servern. Du kan ange följande om du aktiverar Syslog-aviseringar.

1.  Innan du konfigurerar Syslog-aviseringar arbetar du med SIEM-administratören för att ta reda på följande information:

    -   FQDN eller IP-adress för SIEM-servern

    -   Porten som SIEM-servern lyssnar på

    -   Vilken transport som ska användas: UDP, TCP eller TLS (skyddad Syslog)

    -   Format för att skicka data, RFC 3164 eller 5424

2.  På ATA Center-servern klickar du på ikonen **Microsoft Advanced Threat Analytics Management** på skrivbordet.

3.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

4.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)

5.  Under avsnittet Meddelanden, välj **Syslog-server** och ange följande information:

    |Fält|Beskrivning|
    |---------|---------------|
    |Syslog-serverns slutpunkt|Det fullständiga domännamnet för Syslog-servern och du kan också ändra portnumret (standard 514)|
    |Transport|Kan vara UDP, TCP eller TLS (skyddad Syslog)|
    |Format|Det här är formatet som ATA använder för att skicka händelser till SIEM-servern, antingen RFC 5424 eller RFC 3164.|

 ![Avbildning av ATA Syslog-serverinställningar](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
