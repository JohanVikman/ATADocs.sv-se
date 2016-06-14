---
# required metadata

title: Installera ATA tyst | Microsoft Advanced Threat Analytics
description: Det här beskriver tyst installation av ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Tyst installation av ATA
Den här artikeln innehåller instruktioner för tyst installation av ATA.
## Krav

Microsoft ATA 1.6 kräver installation av Microsoft .NET Framework 4.6.1. 

När du installerar eller uppdaterar ATA kommer .Net Framework 4.6.1 att installeras automatiskt som en del av distributionen av Microsoft ATA.

> [!Note] Installationen av .Net Framework 4.6.1 kan kräva att servern startas om. När du installerar ATA Gateway på domänkontrollanter kan du överväga att schemalägga en underhållsperiod för dessa domänkontrollanter.
När du använder metoden för tyst installation av ATA konfigureras installationsprogrammet automatiskt så att servern startas om i slutet av installationen (vid behov). Om du vill undvika att starta om servern som en del av installationen använder du flaggan `-NoRestart`. När du använder flaggan `-NoRestart` och omstart krävs som en del av installationen kommer installationsprogrammet att pausa tills servern har startats om. Följ distributionsförloppet genom att övervaka ATA-installationsloggarna som finns i **%AppData%\Local\Temp**.


## Installera ATA Center

Använd följande kommando för att installera ATA Center.

**Syntax**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Ja|Anger att licensen har lästs och godkänts. Måste anges för tyst installation.|

**Installationsparametrar**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|Nej|Anger sökvägen för installationen av ATA-binärfiler. Standardsökväg: C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|Nej|Anger sökvägen till datamappen för ATA-databasen. Standardsökväg: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Ja|Anger IP-adressen för ATA Center-tjänsten|
|CenterPort|CenterPort=<CenterPort>|Ja|Anger nätverksporten för ATA Center-tjänsten|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|Nej|Anger certifikatets tumavtryck för ATA Center-tjänsten. Det här certifikatet används för att skydda kommunikationen mellan ATA Center och ATA Gateway. Om det inte anges kommer installationen att generera ett självsignerat certifikat.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Ja|Anger IP-adressen för ATA-konsolen|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|Nej|Anger certifikatets tumavtryck för ATA-konsolen. Det här certifikatet används för att verifiera identiteten för ATA-konsolens webbplats. Om inget anges genererar installationen ett självsignerat certifikat|

**Exempel**:
Installera ATA Center med standardinstallationssökvägar och en enda IP-adress:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Installera ATA Center med standardinstallationssökvägar, två IP-adresser och användardefinierade tumavtryck för certifikatet:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Uppdatera ATA Center

Använd följande kommando för att uppdatera ATA Center.

**Syntax**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|


När du uppdaterar ATA upptäcker installationsprogrammet automatiskt att ATA redan är installerat på servern, och inget installationsalternativ för uppdatering krävs.

**Exempel**:
Uppdatera ATA Center tyst. I stora miljöer kan det ta en stund att slutföra ATA Center-uppdateringen. Övervaka ATA-loggar för att följa förloppet för uppdateringen.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Avinstallera ATA Center tyst

Använd följande kommando för att utföra en tyst avinstallation av ATA Center:
**Syntax**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst avinstallation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör avinstallationsprogrammet utan att visa användargränssnitt och prompter.|
|Avinstallera|/uninstall|Ja|Kör en tyst avinstallation av ATA Center från servern.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|

**Installationsparametrar**:

|Namn|Syntax|Obligatoriskt för tyst avinstallation?|Beskrivning|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Nej|Tar bort alla filer i den befintliga databasen.|

**Exempel**:
Tyst avinstallation av ATA Center från servern, som tar bort alla befintliga databasdata:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Tyst installation av ATA Gateway
Använd följande kommando för att installera ATA Gateway:

**Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Ja|Anger att licensen har lästs och godkänts. Måste anges för tyst installation.|

**Installationsparametrar**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|Nej|Anger certifikatets tumavtryck för ATA Center-tjänsten. Det här certifikatet används för att skydda kommunikationen mellan ATA Center och ATA Gateway. Om det inte anges kommer installationen att generera ett självsignerat certifikat.|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Ja|Anger namnet på det användarkonto (user@domain.com) som används för att registrera ATA Gateway med ATA Center.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Ja|Anger lösenordet för det användarkonto (user@domain.com) som används för att registrera ATA Gateway med ATA Center.|

**Exempel**:
Utföra tyst installation av ATA Gateway och registrera den med ATA Center med angivna autentiseringsuppgifter:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Uppdatera ATA Gateway

Använd följande kommando för tyst uppdatering av ATA Gateway:

**Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst installation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|


**Exempel**:
Tyst uppdatering av ATA Gateway:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Tyst avinstallation av ATA Gateway

Använd följande kommando för att utföra en tyst avinstallation av ATA Gateway:
**Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Installationsalternativ**:

|Namn|Syntax|Obligatoriskt för tyst avinstallation?|Beskrivning|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör avinstallationsprogrammet utan att visa användargränssnitt och prompter.|
|Avinstallera|/uninstall|Ja|Kör en tyst avinstallation av ATA Gateway från servern.|
|NoRestart|/norestart|Nej|Hindrar alla försök att starta om. Gränssnittet frågar som standard före omstart.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|

**Exempel**:
Utföra tyst avinstallation av ATA Gateway från servern:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

<!--HONumber=May16_HO1-->


