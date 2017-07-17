---
title: "Ställ in inställningar för e-postmeddelanden i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du får ATA att meddela dig (via e-post eller vidarebefordran av ATA-händelser) när det upptäcker misstänkta aktiviteter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 47d1125856631ecedcbc7779bf0529741c3da61f
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# Ange e-postserverinställningar för ATA
<a id="provide-ata-with-your-email-server-settings" class="xliff"></a>
ATA kan meddela dig när det identifierar en misstänkt aktivitet. Om ATA ska kunna skicka e-postaviseringar måste du först konfigurera **E-postserverinställningar**.

1.  På ATA Center-servern klickar du på ikonen **Microsoft Advanced Threat Analytics Management** på skrivbordet.

2.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

3.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)

4.  I avsnittet **Meddelanden** under **E-postserver**, anger du följande information:

    |Fält|Beskrivning|Värde|
    |---------|---------------|---------|
    |SMTP-serverslutpunkt (krävs)|Ange det fullständiga domännamnet för SMTP-servern och du kan också ändra portnumret (standard 25).|Exempel:<br />smtp.contoso.com|
    |SSL|Växla SSL om SMTP-servern kräver SSL. **Obs!** Om du aktiverar SSL måste du också ändra portnumret.|Standardvärdet är inaktiverat|
    |Autentisering|Aktivera om SMTP-servern kräver autentisering. **Obs!** Om du aktiverar autentisering måste du ange ett användarnamn och lösenord för ett e-postkonto som har behörighet att ansluta till SMTP-servern.|Standardvärdet är inaktiverat|
    |Skicka från (krävs)|Ange en e-postadress som e-postmeddelandet ska skickas från.|Exempel:<br />ATA@contoso.com|
    ![Bild för e-postserverinställningar i ATA](media/ata-email-server.png)

## Ange Syslog-serverinställningar för ATA
<a id="provide-ata-with-your-syslog-server-settings" class="xliff"></a>
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



## Se även
<a id="see-also" class="xliff"></a>
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
