---
title: "Konfigurera händelseinsamling | Microsoft Advanced Threat Analytics"
description: "Beskriver alternativen för att konfigurera händelseinsamling med ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 17f30cbe478a868f3b6887bf48d8084934624191


---

# Konfigurera händelseinsamling
För att förbättra identifieringsfunktionerna behöver ATA Windows-händelselogg ID 4776. Den kan vidarebefordras till ATA Gateway på ett av två sätt, antingen genom att konfigurera ATA Gateway så att den lyssnar efter SIEM-händelser eller genom att [Konfigurera vidarebefordran av Windows-händelser](#configuring-windows-event-forwarding).

## Händelseinsamling
Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan ATA använda Windows-händelse 4776 för att förbättra ATA Pass-the-Hash-identifiering ytterligare. Den kan fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger ATA ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.

### SIEM/Syslog
För att ATA ska kunna använda data från en Syslog-server måste du göra följande:

-   Konfigurera en av ATA Gateway-servrarna så att den lyssnar på och godkänner händelser som vidarebefordras från SIEM/Syslog-servern.

-   Konfigurera SIEM/Syslog-servern så att den vidarebefordrar specifika händelser till ATA Gateway.

> [!IMPORTANT]
> -   Vidarebefordra inte alla Syslog-data till ATA Gateway.
> -   ATA stöder UDP-trafik från SIEM/Syslog-servern.

Se SIEM/Syslog-serverns produktdokumentation för information om hur du konfigurerar vidarebefordran av specifika händelser till en annan server. 

### Vidarebefordran av Windows-händelser
Om du inte använder en SIEM/Syslog-server kan du konfigurera Windows-domänkontrollanterna så att de vidarebefordrar Windows händelse-ID 4776 så att den samlas in och analyseras av ATA. Windows händelse-ID 4776 innehåller data om NTLM-autentiseringar.

## Konfigurera ATA Gateway för att lyssna efter SIEM-händelser

1.  På ATA Gateway-konfigurationen aktiverar du **Syslog Listener UDP**.

    Ange IP-adressen som lyssnar på det sätt som beskrivs i bilden nedan. Standardporten är 514.

    ![Bild för att aktivera syslog listener UDP](media/ATA-enable-siem-forward-events.png)

2.  Konfigurera SIEM- eller Syslog-servern för att vidarebefordra Windows händelse-ID 4776 till IP-adressen som valdes ovan. Ytterligare information om hur du konfigurerar SIEM finns onlinehjälpen för SIEM eller alternativ för teknisk support för specifika formateringskrav för varje SIEM-server.

### Stöd för SIEM
ATA har stöd för SIEM-händelser i följande format:

#### RSA Security Analytics
&lt;Syslog-rubrik&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog-rubriken är valfri.

-   Teckenavskiljaren ”\n” krävs mellan alla fält.

-   Fälten är, i ordning:

    1.  RsaSA-konstant (måste visas).

    2.  Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Helst med en noggrannhet på millisekunder, detta är mycket viktigt.

    3.  Windows händelse-ID

    4.  Providernamn för Windows-händelse

    5.  Loggnamn för Windows-händelse

    6.  Namnet på den dator som tar emot händelsen (i det här fallet DC)

    7.  Namnet på den autentiserande användaren

    8.  Namnet på källans värdnamn

    9. Resultatkod för NTLM

-   Ordningen är viktig och inget annat får inkluderas i meddelandet.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Domänkontrollanten försökte verifiera inloggningsuppgifter för ett konto.|Låg| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Måste överensstämma med protokolldefinitionen.

-   Ingen syslog-rubrik.

-   Rubrikdelen (delen som separeras med ett lodstreck) måste finnas (vilket anges i protokollet).

-   Följande nycklar i delen _Tillägg_ måste finnas i händelsen:

    -   externalId = Windows händelse-ID

    -   rt = Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Helst med en noggrannhet på millisekunder, detta är mycket viktigt.

    -   cat = Loggnamn för Windows-händelse

    -   shost = Källans värdnamn

    -   dhost = Den dator som tar emot händelsen (i det här fallet DC)

    -   duser = Den autentiserande användaren

-   Ordningen är inte viktigt för delen _Tillägg_

-   Det måste finnas en anpassad nyckel och nyckeletikett för dessa två fält:

    -   ”EventSource”

    -   ”Reason or Error Code” = Resultatkoden för NTLM

#### Splunk
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

    -   TimeGenerated = Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, helst med en noggrannhet på millisekunder, detta är mycket viktigt.

    -   ComputerName = Källans värdnamn

    -   Message = Den ursprungliga händelsetexten från Windows-händelsen

-   Meddelandenyckel och värde MÅSTE vara sist.

-   Ordningen är inte viktig för paren nyckel=värde.

#### QRadar
QRadar aktiverar händelseinsamling via en agent. Om data samlas in med hjälp av en agent samlas tidsformatet in utan data för millisekunder. Eftersom ATA kräver data för millisekunder är det nödvändigt att konfigurera QRadar att använda Windows-händelseinsamling utan agent. Mer information finns i [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Windows-händelseinsamling utan agent med MSRPC-protokollet").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

De obligatoriska fälten är:

- Agenttypen för insamlingen
- Providernamn för Windows-händelselogg
- Källa för Windows-händelselogg
- Domänkontrollantens fullständiga kvalificerade domännamn
- Windows händelse-ID

TimeGenerated är tidsstämpeln för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, helst med en noggrannhet på millisekunder, detta är mycket viktigt.

Message är den ursprungliga händelsetexten från Windows-händelsen

Se till att det finns \t mellan nyckel=värde-paren.

>[!NOTE] 
> Användning av WinCollect för Windows-händelseinsamling stöds inte.

## Konfigurera vidarebefordran av Windows-händelser
Om du inte har en SIEM-server kan du konfigurera domänkontrollanterna så att de vidarebefordrar Windows händelse-ID 4776 direkt till någon av dina ATA-gatewayer.

1.  Logga in på alla domänkontrollanter och ATA Gateway-datorer med ett domänkonto som har administratörsbehörighet.
2. Kontrollera att alla domänkontrollanter och ATA-gatewayer som du ansluter är kopplade till samma domän.
3.  Skriv följande i en upphöjd kommandotolk på varje domänkontrollant:
```
winrm quickconfig
```
4.  Skriv följande i en upphöjd kommandotolk på ATA Gateway:
```
wecutil qc
```
5.  På varje domänkontrollant går du till **Active Directory – användare och datorer**, går till mappen **Builtin** och dubbelklickar på gruppen **Händelseloggläsare**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Högerklicka på den och välj **Egenskaper**. På fliken **Medlemmar** lägger du till datorkontot för varje ATA Gateway.
![wef_ad event log reader popup](media/wef_ad-event-log-reader-popup.png)
6.  På ATA Gateway öppnar du Loggboken och högerklickar på **Prenumerationer** och väljer **Skapa prenumeration**.  

    a. Under **Prenumerationstyp och källdatorer** klickar du på **Välj datorer** och lägger till domänkontrollanterna och testar anslutningen.
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b. Under **Händelser som ska samlas in** klickar du på **Välj händelser**. Välj **Efter logg** och bläddra ned för att välja **Säkerhet**. I **Tar med/undantar händelse-ID** skriver du sedan **4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. Under **Ändra användarkonto eller konfigurera avancerade inställningar** klickar du på **Avancerat**.
Ställ in **Protokoll** på **HTTP** och **Port** på **5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [Valfritt] Om du vill ha ett kortare avsökningsintervall anger du prenumerationens hjärtslag till 5 sekunder på ATA Gateway för att få ett kortare avsökningsintervall.
    wecutil ss <CollectionName>/cm:custom wecutil ss <CollectionName> /hi:5000

8. På konfigurationssidan för ATA Gateway aktiverar du **Insamling av vidarebefordran av Windows-händelser**.

> [!NOTE]
> När den här inställningen aktiveras tittar ATA Gateway i loggen för vidarebefordrade händelser om det finns Windows-händelser som har vidarebefordrats till den från domänkontrollanterna.

Mer information finns i: [Konfigurera datorerna att vidarebefordra och samla in händelser](https://technet.microsoft.com/library/cc748890)

## Se även
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=Jun16_HO4-->


