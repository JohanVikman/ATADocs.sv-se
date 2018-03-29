---
title: Installera Azure Advanced Threat Protection | Microsoft Docs
description: I det här steget av installationen ATP konfigurerar du datakällor.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/28/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2c2a8e6d70d937c559c110a18feec4afc75271e9
ms.sourcegitcommit: 45d0108d0cbf8fe7550d13486d3d9c06c1e58506
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/28/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp"></a>Installera Azure ATP

## <a name="configure-event-collection"></a>Konfigurera händelseinsamling

För att förbättra identifieringsfunktionerna Azure ATP måste följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045. Dessa kan antingen läsas automatiskt av Azure ATP-sensor eller om Azure ATP-sensor inte har distribuerats, den kan vidarebefordras till Azure ATP fristående sensor i ett av två sätt, genom att konfigurera fristående Azure ATP sensorn så att den lyssnar efter SIEM-händelser eller genom att [Konfigurera vidarebefordran av Windows-händelse](configure-event-forwarding.md).

> [!NOTE]
> Det är viktigt att köra ATA granskning skriptet innan du konfigurerar händelseinsamling för att säkerställa att domänkontrollanterna är rätt konfigurerade för att registrera de nödvändiga händelserna. 

Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan kan Azure ATP använda Windows-händelser för att förbättra ytterligare identifieringar. Den använder händelse 4776 för NTLM, vilket förbättrar olika identifieringar och händelser 4732, 4733, 4728, 4729, 4756, 4757 och 7045 för att förbättra identifiera känsliga grupp ändringar och skapa en tjänst. Den kan fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger Azure ATP med ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.

### <a name="siemsyslog"></a>SIEM/Syslog
För Azure ATP för att kunna använda data från en Syslog-server, måste du utföra följande steg:

-   Konfigurera Azure ATP sensor-servrar för att lyssna på och godkänner händelser som vidarebefordras från SIEM/Syslog-servern.

 > [!NOTE]
 > Azure ATP lyssnar bara på IPv4 och IPv6 inte. 

-   Konfigurera SIEM/Syslog-servern för att vidarebefordra specifika händelser till Azure ATP-sensor.

> [!IMPORTANT]
> -   Vidarebefordra inte alla Syslog-data till Azure ATP-sensor.
> -   Azure ATP stöder UDP-trafik från SIEM/Syslog-servern.

Se SIEM/Syslog-serverns produktdokumentation för information om hur du konfigurerar vidarebefordran av specifika händelser till en annan server. 

> [!NOTE]
>Om du inte använder en SIEM/Syslog-servern kan du konfigurera din Windows-domänkontrollanter för att vidarebefordra alla nödvändiga händelser som ska samlas in och analyseras av ATP.

### <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Konfigurera Azure ATP sensor så att den lyssnar efter SIEM-händelser

1.  I Azure ATP konfigurationen under **datakällor** klickar du på **SIEM** och aktivera **Syslog** och på **spara**.

    ![Bild för att aktivera syslog listener UDP](media/atp-siem-config.png)

2.  Konfigurera SIEM- eller Syslog-servern för att vidarebefordra alla nödvändiga händelser till IP-adressen för en Azure ATP sensorer. Mer information om hur du konfigurerar SIEM finns i din onlinehjälpen för SIEM eller alternativ för teknisk support för specifika formateringskrav för varje SIEM-server.

Azure ATP har stöd för SIEM-händelser i följande format:  

### <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Syslog-rubrik&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog-rubriken är valfri.

-   Teckenavskiljaren ”\n” krävs mellan alla fält.

-   Fälten är, i ordning:

    1.  RsaSA-konstant (måste visas).

    2.  Tidsstämpel för den faktiska händelsen (se till att den inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATP). Helst noggrannhet på millisekunder är detta viktigt.

    3.  Windows-händelse-ID

    4.  Providernamn för Windows-händelse

    5.  Loggnamn för Windows-händelse

    6.  Namnet på den dator som tar emot händelsen (i det här fallet DC)

    7.  Namnet på den autentiserande användaren

    8.  Namnet på källans värdnamn

    9. Resultatkod för NTLM

-   Ordningen är viktig och inget annat får inkluderas i meddelandet.

### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Domänkontrollanten försökte verifiera inloggningsuppgifter för ett konto.|Låg| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Måste överensstämma med protokolldefinitionen.

-   Ingen syslog-rubrik.

-   Rubrikdelen (delen som separeras med ett lodstreck) måste finnas (vilket anges i protokollet).

-   Följande nycklar i delen _Tillägg_ måste finnas i händelsen:

    -   externalId = Windows händelse-ID

    -   rt = tidsstämpel för den faktiska händelsen (se till att den inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATP). Helst noggrannhet på millisekunder är detta viktigt.

    -   cat = Loggnamn för Windows-händelse

    -   shost = Källans värdnamn

    -   dhost = Den dator som tar emot händelsen (i det här fallet DC)

    -   duser = Den autentiserande användaren

-   Ordningen är inte viktigt för delen _Tillägg_

-   Det måste finnas en anpassad nyckel och nyckeletikett för dessa två fält:

    -   ”EventSource”

    -   ”Reason or Error Code” = Resultatkoden för NTLM

### <a name="splunk"></a>Splunk
&lt;Syslog-rubrik&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Datorn försökte verifiera inloggningsuppgifter för ett konto.

Autentiseringspaket:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Inloggningskonto: Administratör

Källarbetsstation:       SIEM

Felkod:         0x0

-   Syslog-rubriken är valfri.

-   Teckenavskiljaren ”\r\n” finns mellan alla obligatoriska fält.

-   Fälten har formatet nyckel=värde.

-   Följande nycklar måste finnas och ha ett värde:

    -   EventCode = Windows händelse-ID

    -   Logfile = Loggnamn för Windows-händelse

    -   SourceName = Providernamn för Windows-händelse

    -   TimeGenerated = tidsstämpel för den faktiska händelsen (se till att den inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATP). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, helst noggrannhet på millisekunder, detta är viktigt.

    -   ComputerName = Källans värdnamn

    -   Message = Den ursprungliga händelsetexten från Windows-händelsen

-   Meddelandenyckel och värde MÅSTE vara sist.

-   Ordningen är inte viktig för paren nyckel=värde.

### <a name="qradar"></a>QRadar
QRadar aktiverar händelseinsamling via en agent. Om data samlas in med hjälp av en agent samlas tidsformatet in utan data för millisekunder. Eftersom Azure ATP kräver data för millisekunder är det nödvändigt att konfigurera QRadar att använda Windows-händelseinsamling utan Agent. Mer information finns i [ http://www-01.ibm.com/support/docview.wss?uid=swg21700170 ] (http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: utan Agent insamling av Windows-händelser med MSRPC-protokollet").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

De obligatoriska fälten är:

- Agenttypen för insamlingen
- Providernamn för Windows-händelselogg
- Källa för Windows-händelselogg
- Domänkontrollantens fullständiga kvalificerade domännamn
- Windows-händelse-ID

TimeGenerated är tidsstämpeln för den faktiska händelsen (se till att den inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATP). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, helst noggrannhet på millisekunder, detta är viktigt.

Message är den ursprungliga händelsetexten från Windows-händelsen

Se till att det finns \t mellan nyckel=värde-paren.

>[!NOTE] 
> Användning av WinCollect för Windows-händelseinsamling stöds inte.




## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Referens till Azure ATP SIEM](cef-format-sa.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
