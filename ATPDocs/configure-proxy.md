---
title: Konfigurera proxyservern eller brandväggen för att aktivera Azure ATP-kommunikation med sensorn | Microsoft Docs
description: Beskriver hur du ställer in din brandvägg eller proxy för att tillåta kommunikation mellan Azure ATP-Molntjänsten och Azure ATP-sensorer
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2e8a4cdccad7f371601941e20ede20000aeef5ec
ms.sourcegitcommit: a5823d0dfc48783ab990a99ca3f65b614fb49e75
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/12/2018
ms.locfileid: "44697199"
---
*Gäller för: Azure Avancerat skydd*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurera slutpunkten för proxy och Internet-anslutningsinställningarna för din Azure ATP-sensorn

Varje Azure Advanced Threat Protection (ATP)-sensor kräver en Internetanslutning till Azure ATP-Molntjänsten att fungera korrekt. I vissa organisationer har domänkontrollanterna inte är direkt ansluten till Internet, men det är anslutna via en proxyanslutning för webben. Varje Azure ATP-sensorn kräver att du använder Microsoft Windows Internet (WinINET) proxykonfigurationen till sensorn rapportdata och kommunicera med Azure ATP-tjänsten. Om du använder WinHTTP proxykonfiguration kan behöva du fortfarande konfigurera proxyinställningar för Windows Internet (WinINet) webbläsaren för kommunikation mellan sensorn och Azure ATP-Molntjänsten.


När du konfigurerar proxyservern kommer du behöver veta att Azure ATP inbäddat sensortjänsten körs i kontexten med det **LocalService** konto och Azure ATP-sensorn Updater-tjänsten körs i systemkontexten med **LocalSystem** konto. 

> [!NOTE]
> Om du använder Transparent proxy eller WPAD i din nätverkstopologi, behöver du inte konfigurera WinINET för proxyservern.

## <a name="configure-the-proxy"></a>Konfigurera proxyn 

Konfigurera proxy-servern manuellt med hjälp av en registerbaserade statisk proxy, att tillåta Azure ATP-sensorn till diagnostikdata för rapporten och kommunicera med Azure ATP-Molntjänsten när en dator inte har behörighet att ansluta till Internet.

> [!NOTE]
> Ändringar i registret bör tillämpas endast på LocalService och LocalSystem.

Statisk proxyn kan konfigureras via registret. Du måste kopiera proxykonfigurationen som du använder i användarkontext localsystem och localservice. Kopiera proxyinställningarna användaren kontext:

1.   Se till att säkerhetskopiera registernycklarna innan du ändrar dem.

2. Sök efter värdet i registret, `DefaultConnectionSetting` som REG_BINARY under registernyckeln `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` och kopiera den.
 
2.  Om LocalSystem inte har rätt proxyinställningarna (de inte har konfigurerats eller de skiljer sig från Current_User), kopiera proxyinställning från Current_User LocalSystem. Under registernyckeln `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Klistra in värdet från Current_user `DefaultConnectionSetting` som REG_BINARY.

4.  Om LocalService inte har rätt proxyinställningarna, kopierar du proxyinställning från Current_User till LocalService. Under registernyckeln `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Klistra in värdet från Current_User `DefaultConnectionSetting` som REG_BINARY.

> [!NOTE]
> Detta påverkar alla program, inklusive Windows-tjänster som använder WinINET med LocalService LocalSytem kontext.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Aktivera åtkomst till URL: er i Azure ATP-tjänsten i proxyservern

Om en proxy eller brandvägg blockerar all trafik som standard och så att endast vissa domäner via eller HTTPS genomsökning (SSL-kontroll) är aktiverad måste du kontrollera att följande webbadresser är vit anges för att tillåta kommunikation med Azure ATP-tjänsten på port 443:

|Tjänstlokalisering|. Atp.Azure.com DNS-post|
|----|----|
|USA |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Europa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Asien|triprd1wcasse1sensorapi.ATP.Azure.com|


Du kan även skydda brandvägg eller proxyserver regler för en viss arbetsyta du skapade genom att skapa en regel för följande DNS-poster:
- \<ditt Arbetsytenamn >. atp.azure.com – för konsolen anslutning. Till exempel ”Contoso-corp.atp.azure.com”
- \<ditt Arbetsytenamn > sensorapi.atp.azure.com – för sensorer anslutning. Till exempel ”contoso-corpsensorapi.atp.azure.com”

 
> [!NOTE]
> När du utför SSL-kontroll på Azure ATP-nätverkstrafik (mellan sensorn och Azure ATP-tjänsten), SSL-kontroll måste ha stöd för ömsesidig granskning.


## <a name="see-also"></a>Se även
- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)