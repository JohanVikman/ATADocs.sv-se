---
title: Installera Azure Advanced Threat Protection tyst | Microsoft Docs
description: Det här beskriver tyst installation Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f27020f1b4a5fa7aa8fefbda28eac0c2ad6c64d0
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/12/2018
ms.locfileid: "29856489"
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="azure-atp-silent-installation"></a>Azure ATP tyst installation
Den här artikeln innehåller instruktioner för tyst installation av Azure ATP.

## <a name="prerequisites"></a>Krav

Azure ATP kräver installation av Microsoft .NET Framework 4.7. 

När du installerar Azure ATP .net Framework 4.7 är automatiskt installeras som en del av distributionen av Azure ATP.

> [!IMPORTANT] 
> Se till att du har den senaste versionen av .net Framework installerat. Om en tidigare version av .net har installerats kommer fastna i en slinga din Azure ATP tyst installation och inte installeras. 

> [!NOTE] 
> Installationen av .net framework 4.7 kan kräva att servern startas om. När du installerar Azure ATP sensor på domänkontrollanter, bör du schemalägga en underhållsperiod för dessa domänkontrollanter.
När du använder metoden för tyst installation av Azure ATP konfigureras installationsprogrammet automatiskt starta om servern i slutet av installationen (vid behov). På grund av ett Windows Installer-fel i *norestart* flaggan kan inte användas på ett tillförlitligt sätt att kontrollera att servern inte startar om, så se till att endast köra tyst installation under en underhållsperiod.

Om du vill spåra förloppet för distributionen, övervaka Azure ATP-installationsloggarna som finns i **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Azure ATP sensor tyst installation

> [!NOTE]
> När du distribuerar tyst Azure ATP sensor via System Center Configuration Manager eller andra system för distribution av programvara, rekommenderas det att skapa två distributionspaket:</br>-Net Framework 4.7 inklusive domänkontrollanten att startas om</br>-Azure ATP sensorn. </br>Gör Azure ATP sensor paketet beroende distributionen av .net Framework paketdistributionen. </br>Hämta den [.Net Framework 4.7 offline distributionspaketet](https://www.microsoft.com/download/details.aspx?id=49982). 


Använd följande kommando för att installera Azure ATP-sensor:

**Syntax**:

    Azure ATP sensor Setup.exe [/AccessKey=<Access Key>] [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
   

> [!NOTE]
> Kopiera snabbtangent från arbetsytan portal under **Configuration** och sedan **sensor**.


**Installationsalternativ**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst installation?|Description|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|

**Installationsparametrar**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst installation?|Description|
|-------------|----------|---------|---------|
|AccessKey|AccessKey="**"|Ja|Anger den åtkomstnyckel som används för att registrera Azure ATP-sensor med arbetsytan Azure ATP.|

**Exempel**: Om du vill installera Azure ATP-sensor, logga in på domänen ansluten dator med dina administratörsautentiseringsuppgifter för Azure ATP så att du inte behöver ange autentiseringsuppgifter som en del av installationen. Annars kan registrera den med Azure ATP Molntjänsten med angivna autentiseringsuppgifter:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Uppdatera Azure ATP-temperatursensor

Använd följande kommando för tyst uppdatering Azure ATP-sensor:

**Syntax**:

    Azure ATP  sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsalternativ**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst installation?|Description|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|


**Exempel**: tyst uppdatering Azure ATP-sensor:

        Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Avinstallera Azure ATP-sensor tyst

Använd följande kommando för att utföra en tyst avinstallation av Azure ATP-sensor: **Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Installationsalternativ**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst avinstallation?|Description|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör avinstallationsprogrammet utan att visa användargränssnitt och prompter.|
|Avinstallera|/uninstall|Ja|Kör en tyst avinstallation av Azure ATP-sensor från servern.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|

**Exempel**: utföra tyst avinstallation Azure ATP-sensor från servern:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Se även

- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)