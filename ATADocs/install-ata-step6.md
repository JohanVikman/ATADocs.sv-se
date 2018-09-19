---
title: Installera Advanced Threat Analytics steg 6 | Microsoft Docs
description: I det här ATA-installationssteget konfigurerar du datakällor.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1a8df6ebb4b2ea6f16f1087b4b615922b4f122ff
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133522"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="install-ata---step-6"></a>Installera ATA – Steg 6

>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)
[Steg 7 »](vpn-integration-install-step.md)

## <a name="step-6-configure-event-collection"></a>Steg 6. Konfigurera händelseinsamling
### <a name="configure-event-collection"></a>Konfigurera händelseinsamling
För att förbättra identifieringsfunktionerna behöver ATA följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045. Dessa kan antingen läsas automatiskt av ATA Lightweight Gateway eller, om ATA Lightweight Gateway inte har distribuerats, vidarebefordras till ATA Gateway på något av två sätt genom att ATA Gateway konfigureras att lyssna efter SIEM-händelser eller genom att [vidarebefordran av Windows-händelser konfigureras](configure-event-collection.md). 

> [!NOTE]
> För ATA versions 1.8 och senare behövs inte längre konfiguration av händelseinsamling för ATA Lightweight-gatewayer. ATA Lightweight Gateway kan nu läsa händelser lokalt, utan att du behöver konfigurera vidarebefordran av händelser.

Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan ATA använda Windows-händelser för att förbättra identifieringarna ytterligare. Tjänsten använder händelse 4776 för NTLM som förbättrar olika identifieringar, och händelserna 4732, 4733, 4728, 4729, 4756 och 4757 för att förbättra identifieringen av ändringar av känsliga grupper. Den kan fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger ATA ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.

#### <a name="siemsyslog"></a>SIEM/Syslog
Om ATA ska kunna använda data från en Syslog-server måste du utföra följande steg:

-   Konfigurera ATA Gateway-servrarna så att de lyssnar på och godkänner händelser som vidarebefordras från SIEM/Syslog-servern.
> [!NOTE]
> ATA lyssnar endast på IPv4 och inte på IPv6. 
-   Konfigurera SIEM/Syslog-servern så att den vidarebefordrar specifika händelser till ATA Gateway.

> [!IMPORTANT]
> -   Vidarebefordra inte alla Syslog-data till ATA Gateway.
> -   ATA stöder UDP-trafik från SIEM/Syslog-servern.

Se SIEM/Syslog-serverns produktdokumentation för information om hur du konfigurerar vidarebefordran av specifika händelser till en annan server. 

> [!NOTE]
>Om du inte använder en SIEM/Syslog-server kan du konfigurera Windows-domänkontrollanterna så att de vidarebefordrar Windows händelse-ID 4776 så att den samlas in och analyseras av ATA. Windows händelse-ID 4776 innehåller data om NTLM-autentiseringar.

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Konfigurera ATA Gateway för att lyssna efter SIEM-händelser

1.  Under **Datakällor** i ATA-konfiguration klickar du på **SIEM** och aktiverar **Syslog** och klickar på **Spara**.

    ![Bild för att aktivera syslog listener UDP](media/ATA-enable-siem-forward-events.png)

2.  Konfigurera SIEM- eller Syslog-servern för att vidarebefordra Windows-händelse-ID 4776 till IP-adressen för en av ATA-gatewayarna. Mer information om hur du konfigurerar SIEM finns i din onlinehjälpen för SIEM eller alternativ för teknisk support för specifika formateringskrav för varje SIEM-server.

ATA har stöd för SIEM-händelser i följande format:  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Syslog-rubrik&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog-rubriken är valfri.

-   Teckenavskiljaren ”\n” krävs mellan alla fält.

-   Fälten är, i ordning:

    1.  RsaSA-konstant (måste visas).

    2.  Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Helst på millisekunder är detta viktigt.

    3.  Windows-händelse-ID

    4.  Providernamn för Windows-händelse

    5.  Loggnamn för Windows-händelse

    6.  Namnet på den dator som tar emot händelsen (i det här fallet DC)

    7.  Namnet på den autentiserande användaren

    8.  Namnet på källans värdnamn

    9. Resultatkod för NTLM

-   Ordningen är viktig och inget annat får inkluderas i meddelandet.

#### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Domänkontrollanten försökte verifiera inloggningsuppgifter för ett konto.|Låg| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Måste överensstämma med protokolldefinitionen.

-   Ingen syslog-rubrik.

-   Rubrikdelen (delen som separeras med ett lodstreck) måste finnas (vilket anges i protokollet).

-   Följande nycklar i delen _Tillägg_ måste finnas i händelsen:

    -   externalId = Windows händelse-ID

    -   rt = tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Helst på millisekunder är detta viktigt.

    -   cat = Loggnamn för Windows-händelse

    -   shost = Källans värdnamn

    -   dhost = Den dator som tar emot händelsen (i det här fallet DC)

    -   duser = Den autentiserande användaren

-   Ordningen är inte viktigt för delen _Tillägg_

-   Det måste finnas en anpassad nyckel och nyckeletikett för dessa två fält:

    -   ”EventSource”

    -   ”Reason or Error Code” = Resultatkoden för NTLM

#### <a name="splunk"></a>Splunk
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

    -   TimeGenerated = Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, noggrannhet på millisekunder, detta är viktigt.

    -   ComputerName = Källans värdnamn

    -   Message = Den ursprungliga händelsetexten från Windows-händelsen

-   Meddelandenyckel och värde MÅSTE vara sist.

-   Ordningen är inte viktig för paren nyckel=värde.

#### <a name="qradar"></a>QRadar
QRadar aktiverar händelseinsamling via en agent. Om data samlas in med hjälp av en agent samlas tidsformatet in utan data för millisekunder. Eftersom ATA kräver data för millisekunder är det nödvändigt att konfigurera QRadar att använda Windows-händelseinsamling utan agent. Mer information finns i [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: utan Agent samling för Windows-händelser med MSRPC-protokollet").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

De obligatoriska fälten är:

- Agenttypen för insamlingen
- Providernamn för Windows-händelselogg
- Källa för Windows-händelselogg
- Domänkontrollantens fullständiga kvalificerade domännamn
- Windows-händelse-ID

TimeGenerated är tidsstämpeln för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, noggrannhet på millisekunder, detta är viktigt.

Message är den ursprungliga händelsetexten från Windows-händelsen

Se till att det finns \t mellan nyckel=värde-paren.

>[!NOTE] 
> Användning av WinCollect för Windows-händelseinsamling stöds inte.



>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)
[Steg 7 »](vpn-integration-install-step.md)



## <a name="related-videos"></a>Relaterade videor
- [Översikt över ATA-distribution](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Välja rätt typ av ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [ATA POC-Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

