---
title: Installera Azure Avancerat skydd tyst | Microsoft Docs
description: Det här beskriver tyst installation av Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/7/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 363400531fe2b4e2634fa80ec1f65ad80923606f
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125795"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-switches-and-silent-installation"></a>Azure ATP-växlar och tyst installation
Den här artikeln ger vägledning och anvisningar om hur Azure ATP-växlar och tyst installation.

## <a name="prerequisites"></a>Krav

Azure ATP kräver installation av Microsoft .NET Framework 4.7. 

När du installerar Azure ATP .net Framework 4.7 är automatiskt installeras som en del av distributionen av Azure ATP.

> [!IMPORTANT] 
> Se till att du har den senaste versionen av .net Framework installerat. Om en tidigare version av .net installeras, kommer fastnar i en loop din Azure ATP tyst installation och inte installeras. 

> [!NOTE] 
> Installationen av .net framework 4.7 kan kräva att servern startas om. När du installerar Azure ATP-sensorn på domänkontrollanter kan du överväga att schemalägga en underhållsperiod för domänkontrollanter.
Med Azure ATP tyst installation kan konfigureras installationsprogrammet automatiskt starta om servern i slutet av installationen (vid behov). Se till att köras tyst installation endast under en underhållsperiod. På grund av en Windows Installer-bugg i *norestart* flaggan inte användas på ett tillförlitligt sätt att kontrollera att servern inte startar.

Om du vill spåra förloppet distribution, övervaka Azure ATP-installationsloggar, som finns i **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Azure ATP-sensorn tyst installation

> [!NOTE]
> När du distribuerar tyst Azure ATP-sensorn via System Center Configuration Manager eller andra system för distribution av programvara, rekommenderar vi att du skapar två distributionspaket:</br>-Net Framework 4.7 inklusive starta om domänkontrollanten</br>– Azure ATP-sensorn. </br>Se Azure ATP-sensorpaketet beroende på distributionen av .net Framework paketdistributionen. </br>Hämta den [.Net Framework 4.7 offline distributionspaketet](https://www.microsoft.com/download/details.aspx?id=49982). 


Använd följande kommando för att utföra en helt tyst installation av Azure ATP-sensorn:


**Syntax**:

    Azure ATP sensor Setup.exe /AccessKey=<Access Key> /quiet NetFrameworkCommandLineArguments ="/q" 
   

> [!NOTE]
> Kopiera åtkomstnyckeln från arbetsytans portal under **Configuration** och sedan **sensor**.


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
|accessKey|AccessKey = ”\*\*”|Ja|Anger den åtkomstnyckel som används för att registrera Azure ATP-sensorn med Azure ATP-arbetsytan.|

**Exempel**: Om du vill göra en obevakad installation Azure ATP-sensorn, logga in på domänen domänanslutna datorn med dina autentiseringsuppgifter för Azure ATP-administratör så att du inte behöver ange autentiseringsuppgifter som en del av installationen. Annars registrerar du den med Azure ATP-Molntjänsten med angivna autentiseringsuppgifter:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Uppdatera Azure ATP-sensorn

Använd följande kommando för tyst uppdatering Azure ATP-sensorn:

**Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsalternativ**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst installation?|Description|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör installationsprogrammet utan att visa användargränssnitt och prompter.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Anger parametrarna för installationen av .Net Framework. Måste anges för att tvinga fram den tysta installationen av .Net Framework.|


**Exempel**: tyst uppdatering av Azure ATP-sensorn:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Avinstallera Azure ATP-sensorn tyst

Använd följande kommando för att utföra en tyst avinstallation av Azure ATP-sensorn: **Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Installationsalternativ**:

> [!div class="mx-tableFixed"]
|Namn|Syntax|Obligatoriskt för tyst avinstallation?|Description|
|-------------|----------|---------|---------|
|Tyst|/quiet|Ja|Kör avinstallationsprogrammet utan att visa användargränssnitt och prompter.|
|Avinstallera|/uninstall|Ja|Kör en tyst avinstallation av Azure ATP-sensorn från servern.|
|Hjälp|/help|Nej|Ger hjälp och snabbreferens. Visar rätt användning av installationskommandot, inklusive en lista över alla alternativ och beteenden.|

**Exempel**: utföra tyst avinstallation Azure ATP-sensorn från servern:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Se även

- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
