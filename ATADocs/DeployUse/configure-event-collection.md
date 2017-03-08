---
title: "Konfigurera händelseinsamling i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver alternativen för att konfigurera händelseinsamling med ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f807b428dfcc12a15b814106cc190f2a72fa4254
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gäller för: Advanced Threat Analytics version 1.6 och 1.7*



# <a name="configure-event-collection"></a>Konfigurera händelseinsamling
För att förbättra identifieringsfunktionerna behöver ATA Windows-händelselogg ID 4776. Den kan vidarebefordras till ATA Gateway på ett av två sätt, antingen genom att konfigurera ATA Gateway så att den lyssnar efter SIEM-händelser eller genom att [Konfigurera vidarebefordran av Windows-händelser](#configuring-windows-event-forwarding).

## <a name="event-collection"></a>Händelseinsamling
Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan ATA använda Windows-händelse 4776 för att förbättra ATA Pass-the-Hash-identifiering ytterligare. Den kan fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger ATA ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.

### <a name="siemsyslog"></a>SIEM/Syslog
För att ATA ska kunna använda data från en Syslog-server måste du göra följande:

-   Konfigurera ATA Gateway-servrarna så att de lyssnar på och godkänner händelser som vidarebefordras från SIEM/Syslog-servern.
> [!NOTE]
> ATA lyssnar endast på IPv4 och inte på IPv6. 
-   Konfigurera SIEM/Syslog-servern så att den vidarebefordrar specifika händelser till ATA Gateway.

> [!IMPORTANT]
> -   Vidarebefordra inte alla Syslog-data till ATA Gateway.
> -   ATA stöder UDP-trafik från SIEM/Syslog-servern.

Se SIEM/Syslog-serverns produktdokumentation för information om hur du konfigurerar vidarebefordran av specifika händelser till en annan server. 

### <a name="windows-event-forwarding"></a>Vidarebefordran av Windows-händelser
Om du inte använder en SIEM/Syslog-server kan du konfigurera Windows-domänkontrollanterna så att de vidarebefordrar Windows händelse-ID 4776 så att den samlas in och analyseras av ATA. Windows händelse-ID 4776 innehåller data om NTLM-autentiseringar.

## <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Konfigurera ATA Gateway för att lyssna efter SIEM-händelser

1.  I ATA-konfigurationen, under fliken "Händelser", aktiverar du **Syslog** och trycker på **Spara**.

    ![Bild för att aktivera syslog listener UDP](media/ATA-enable-siem-forward-events.png)

2.  Konfigurera SIEM- eller Syslog-servern för att vidarebefordra Windows-händelse-ID 4776 till IP-adressen för en av ATA-gatewayarna. Ytterligare information om hur du konfigurerar SIEM finns onlinehjälpen för SIEM eller alternativ för teknisk support för specifika formateringskrav för varje SIEM-server.

### <a name="siem-support"></a>Stöd för SIEM
ATA har stöd för SIEM-händelser i följande format:  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
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

#### <a name="hp-arcsight"></a>HP Arcsight
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

    -   TimeGenerated = Tidsstämpel för den faktiska händelsen (se till att det inte är tidsstämpeln för ankomst till SIEM eller när det skickas till ATA). Formatet måste överensstämma med yyyyMMddHHmmss.FFFFFF, helst med en noggrannhet på millisekunder, detta är mycket viktigt.

    -   ComputerName = Källans värdnamn

    -   Message = Den ursprungliga händelsetexten från Windows-händelsen

-   Meddelandenyckel och värde MÅSTE vara sist.

-   Ordningen är inte viktig för paren nyckel=värde.

#### <a name="qradar"></a>QRadar
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

## <a name="configuring-windows-event-forwarding"></a>Konfigurera vidarebefordran av Windows-händelser

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>WEF-konfiguration för ATA-gatewayar med portspegling

När du konfigurerat portspegling från domänkontrollanter till ATA Gateway, följ anvisningarna nedan för att konfigurera vidarebefordran av Windows-händelse med källinitierad konfiguration. Detta är ett sätt att konfigurera vidarebefordran av Windows-händelse. 

**Steg 1: Lägg till konto för nätverkstjänst i domänens händelselogg för läsargrupp** 

I det här scenariot antar vi att ATA-gatewayen är medlem i domänen.

1.    Öppna Active Directory-användare och -datorer, navigera till mappen **BuiltIn** och dubbelklicka på **händelseloggläsare**. 
2.    Välj **medlemmar**.
4.    Om **Nätverkstjänst** inte visas klicka på **Lägg till**, skriv **Nätverkstjänst** i fältet **Ange de objektnamn som ska väljas**. Klicka på **Kontrollera namn** och klicka på **OK**. 

Observera att du efter att ha lagt till **nätverkstjänsten** i gruppen **Händelseloggläsare** måste starta om domänkontrollanterna för att ändringen ska börja gälla.

**Steg 2: Skapa en princip på domänkontrollanterna för att ställa in inställningen Konfigurera målprenumerationshanterare.** 
> [!Note] 
> Du kan skapa en grupprincip för de här inställningarna och använda grupprincipen till varje domänkontrollant som övervakas av ATA Gateway. Stegen nedan ändrar den lokala principen på domänkontrollanten.     

1.    Kör följande kommando på varje domänkontrollant: *winrm quickconfig*
2.  Från en kommandotolk, ange *gpedit.msc*.
3.    Expandera **Datorkonfiguration > Administrativa mallar > Windows-komponenter > Vidarebefordran av händelse**

 ![Bild av gruppredigerare för lokal princip](media/wef 1 local group policy editor.png)

4.    Dubbelklicka på **Konfigurera målprenumerationshanterare**.
   
    1.    Välj **Aktiverad**.
    2.    Under **Alternativ** klickar du på **Visa**.
    3.    Under **SubscriptionManagers** anger du följande värde och klickar på **OK**:    *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (Till exempel: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Konfigurera målprenumerationsbild](media/wef 2 config target sub manager.png)
   
    5.    Klicka på **OK**.
    6.    Från en upphöjd kommandotolk skriver du: *gpupdate/force*. 

**Steg 3: Utför följande steg på ATA-Gateway** 

1.    Öppna en upphöjd kommandotolk och skriv *wecutil qc*
2.    Öppna **Loggboken**. 
3.    Högerklicka på **Prenumerationer** och välj **Skapa prenumeration**. 

   1.    Ange namn och beskrivning för prenumerationen. 
   2.    För **Målloggen**, bekräfta att **Vidarebefordrade händelser** har valts. För att ATA ska läsa händelser måste målloggen vara **Vidarebefordrade händelser**. 
   3.    Välj **Källdatorn initierad** och klicka på **Välj datorgrupper**.
        1.    Klicka på **Lägg till domändator**.
        2.    Ange namnet på domänkontrollanten i fältet **Ange ett objektnamn du vill markera**. Klicka sedan på **Kontrollera namn** och klicka på **OK**. 
       
        ![Loggboksbild](media/wef3 event viewer.png)
   
        
        3.    Klicka på **OK**.
   4.    Klicka på **Välj händelser**.

        1. Klicka på **Av logg** och välj **Säkerhet**.
        2. I fältet **Inkludera/exkludera händelse-ID**, skriv **4776** och klicka på **OK**. 

 ![Frågefilterbild](media/wef 4 query filter.png)

   5.    Högerklicka på den skapade prenumerationen och välj **Körningsstatus** för att se om det finns problem med statusen. 
   6.    Kontrollera efter ett par minuter att händelse 4776 visas i vidarebefordrade händelser på ATA-gatewayen.


### <a name="wef-configuration-for-the-ata-lightweight-gateway"></a>WEF-konfiguration för ATA Lightweight Gateway
När du installerar ATA Lightweight Gateway på domänkontrollanterna kan du konfigurera att domänkontrollanterna vidarebefordrar händelserna till sig själva. Utför följande steg för att konfigurera vidarebefordran av Windows-händelser när du använder ATA Lightweight Gateway. Detta är ett sätt att konfigurera vidarebefordran av Windows-händelse.  

**Steg 1: Lägg till konto för nätverkstjänst i domänens händelselogg för läsargrupp** 

1.    Öppna Active Directory-användare och -dator, navigera till mappen **BuiltIn** och dubbelklicka på **händelseloggläsare**. 
2.    Välj **medlemmar**.
3.    Om **Nätverkstjänst** inte visas klickar du på **Lägg till** och skriv **Nätverkstjänst** i fältet **Ange de objektnamn som ska väljas**. Klicka på **Kontrollera namn** och klicka på **OK**. 

**Steg 2: Utför följande steg på domänkontrollanten efter att ATA Lightweight Gateway har installerats** 

1.    Öppna en upphöjd kommandotolk och skriv *winrm quickconfig* och *wecutil qc* 
2.    Öppna **Loggboken**. 
3.    Högerklicka på **Prenumerationer** och välj **Skapa prenumeration**. 

   1.    Ange namn och beskrivning för prenumerationen. 
   2.    För **Målloggen**, bekräfta att **Vidarebefordrade händelser** har valts. För att ATA ska läsa händelser måste målloggen vara Vidarebefordrade händelser.

        1.    Välj **Insamlarinitierad** och klicka på **Välj datorer**. Klicka sedan på **Lägg till domändator**.
        2.    Ange namnet på domänkontrollanten i **Ange ett objektnamn du vill markera**. Klicka sedan på **Kontrollera namn** och klicka på **OK**.

            ![Bild av prenumerationsegenskaper](media/wef 5 sub properties computers.png)

        3.    Klicka på **OK**.
   3.    Klicka på **Välj händelser**.

        1.    Klicka på **Av logg** och välj **Säkerhet**.
        2.    I **Inkludera/exkludera händelse-ID**, skriv *4776* och klicka på **OK**. 

![Frågefilterbild](media/wef 4 query filter.png)


  4.    Högerklicka på den skapade prenumerationen och välj **Körningsstatus** för att se om det finns problem med statusen. 

> [!Note] 
> Du kan behöva starta om domänkontrollanten innan inställningarna börjar gälla. 

Kontrollera efter ett par minuter att händelse 4776 visas i vidarebefordrade händelser på ATA-gatewayen.



Mer information finns i: [Konfigurera datorerna att vidarebefordra och samla in händelser](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Se även
- [Installera ATA](install-ata-step1.md)
- [Ta en titt i ATA-forumet!!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
