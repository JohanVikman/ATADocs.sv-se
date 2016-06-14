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

## Ange e-postserverinställningar för ATA
ATA kan meddela dig när det identifierar en misstänkt aktivitet. Om ATA ska kunna skicka e-postaviseringar måste du först konfigurera **E-postserverinställningar**.

1.  På ATA Center-servern klickar du på ikonen **Microsoft Advanced Threat Analytics Management** på skrivbordet.

2.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

3.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

4.  På fliken **Allmänt** anger du följande information under **E-postserver**:

    |Fält|Beskrivning|Värde|
    |---------|---------------|---------|
    |SMTP-serverslutpunkt (krävs)|Ange SMTP-serverns fullständiga domännamn.|Exempel:<br />smtp.contoso.com|
    |SSL|Växla SSL om SMTP-servern kräver SSL. **Obs!** Om du aktiverar SSL måste du också ändra portnumret.|Standardvärdet är inaktiverat|
    |Autentisering|Aktivera om SMTP-servern kräver autentisering. **Obs!** Om du aktiverar autentisering måste du ange ett användarnamn och lösenord för ett e-postkonto som har behörighet att ansluta till SMTP-servern.|Standardvärdet är inaktiverat|
    |Skicka från (krävs)|Ange en e-postadress som e-postmeddelandet ska skickas från.|Exempel:<br />ATA@contoso.com|
    ![Bild för e-postserverinställningar i ATA](media/ATA-email-server.png)

## Ange Syslog-serverinställningar för ATA
ATA kan meddela dig när systemet identifierar misstänkt aktivitet genom att skicka aviseringen till Syslog-servern. Du kan ange följande om du aktiverar Syslog-aviseringar.

1.  Innan du konfigurerar Syslog-aviseringar arbetar du med SIEM-administratören för att ta reda på följande information:

    -   FQDN eller IP-adress för SIEM-servern

    -   Porten som SIEM-servern lyssnar på

    -   Vilken transport som ska användas: UDP, TCP eller TLS (skyddad Syslog)

    -   Format för att skicka data, RFC 3164 eller 5424

2.  På ATA Center-servern klickar du på ikonen **Microsoft Advanced Threat Analytics Management** på skrivbordet.

3.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

4.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

5.  Välj **Syslog-server** och ange följande information:

    |Fält|Beskrivning|
    |---------|---------------|
    |Syslog-serverns slutpunkt|FQDN för Syslog-servern|
    |Transport|Kan vara UDC, TCP eller TLS (skyddad Syslog)|
    |Format|Det här är formatet som ATA använder för att skicka händelser till SIEM-servern, antingen RFC 5424 eller RFC 3164.|





## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


