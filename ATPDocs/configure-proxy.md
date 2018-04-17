---
title: Konfigurera proxyservern eller brandväggen för att aktivera Azure ATP kommunikation med sensorn | Microsoft Docs
description: Beskriver hur du ställer in din brandvägg eller proxyserver för att tillåta kommunikation mellan Azure ATP-Molntjänsten och Azure ATP sensorer
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/11/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1e5e0d0665dfcf5251954cd8b0916c7cf80a722c
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/16/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurera endpoint proxy och inställningar för Internet-anslutning för din Azure ATP-temperatursensor

Varje Azure Advanced Threat Protection (ATP) sensor kräver Internet-anslutning till Azure ATP-Molntjänsten att fungera korrekt. I vissa organisationer domänkontrollanterna inte är direkt ansluten till Internet, men är anslutna via en proxy-anslutning för webbprogram. Varje Azure ATP sensor kräver att du använder Microsoft Windows Internet (WinINET) proxy conifguration till sensor rapportdata och kommunicera med tjänsten Azure ATP. Om du använder WinHTTP för proxykonfiguration behöver du fortfarande konfigurera proxyinställningar för Windows Internet (WinINet) webbläsaren för kommunikation mellan sensorn och Azure ATP-Molntjänsten.


När du konfigurerar proxyservern, behöver du veta att inbäddade Azure ATP sensor tjänsten körs i kontexten med hjälp av **LocalService** kontot och tjänsten Azure ATP Sensor Updater körs i systemkontexten med **LocalSystem** konto. 

> [!NOTE]
> Om du använder Transparent proxy eller WPAD i din nätverkstopologi, behöver du inte konfigurera WinINET för proxyservern.

## <a name="configure-the-proxy"></a>Konfigurera proxy 

Konfigurera proxy-servern manuellt med hjälp av en registerbaserade statisk proxy, Tillåt Azure ATP sensor till rapporten diagnostikdata och kommunicera med Azure ATP molntjänst när en dator inte har behörighet att ansluta till Internet.

> [!NOTE]
> Registerändringar bör tillämpas endast på LocalService och lokalt system.

Statisk proxy kan konfigureras via registret. Localsystem och localservice måste du kopiera proxykonfigurationen som du använder i en användarkontext. Så här kopierar proxyinställningarna kontexten för användaren:

1.   Se till att säkerhetskopiera registernycklar innan du ändrar dem.

2. Sök efter värdet i registret, `DefaultConnectionSetting` som REG_BINARY under registernyckeln `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` och kopiera den.
 
2.  Om LocalSystem inte har rätt proxy-inställningar (de inte konfigurerats eller de skiljer sig från Current_User), kopiera proxyinställning från Current_User till LocalSystem. Under registernyckeln `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Klistra in värdet från Current_user `DefaultConnectionSetting` som REG_BINARY.

4.  Om LocalService inte har rätt proxyinställningar, kopierar du proxyinställning från Current_User till LocalService. Under registernyckeln `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Klistra in värdet från Current_User `DefaultConnectionSetting` som REG_BINARY.

> [!NOTE]
> Detta påverkar alla program, inklusive Windows-tjänster som använder WinINET med LocalService LocalSytem kontext.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Aktivera åtkomst till Azure ATP webbadresserna i proxyservern

Om en proxyserver eller brandvägg blockerar all trafik som standard och så att bara vissa domäner via eller HTTPS genomsökning (SSL-kontroll) är aktiverat, kontrollera att följande webbadresser är tomt anges att tillåta kommunikation med Windows Defender ATP-tjänsten i porten 443:

|Tjänstlokalisering|. Atp.Azure.com DNS-post|
|----|----|
|OSS |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Europa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Asien|triprd1wcasse1sensorapi.ATP.Azure.com|

> [!NOTE]
> När du utför SSL-kontroll på Azure ATP nätverkstrafik (mellan sensorn och tjänsten Azure ATP), måste SSL-kontroll stödja ömsesidig kontroll.


## <a name="see-also"></a>Se även
- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)