---
title: "Konfigurera proxyservern eller brandväggen för att aktivera Azure ATP kommunikation med sensorn | Microsoft Docs"
description: "Beskriver hur du ställer in din brandvägg eller proxyserver för att tillåta kommunikation mellan Azure ATP-Molntjänsten och Azure ATP sensorer"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 47fa5ad5d6fb7800c7df4b878d16ec335e2b70e5
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Konfigurera proxyservern för att tillåta kommunikation mellan Azure ATP sensorer och Molntjänsten Azure ATP

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna: *. atp.azure.com port 443 i din brandvägg eller proxyserver. Konfigurationen måste vara på datornivå (= datorkonto) och inte på nivån för kontot. Du kan testa din konfiguration med följande steg:
 
1.  Bekräfta att den **aktuell användare** har åtkomst till processorn slutpunkten med hjälp av Internet Explorer, genom att bläddra till följande URL från domänkontrollanten: https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (för USA) som du bör få fel 503:

 ![tjänsten är inte tillgänglig](/media/service-unavailable.png)
 
2.  Om du inte får ett felmeddelande 503, kontrollera proxykonfigurationen och försök igen.

3.  Om proxykonfigurationen fungerar för den **CURRENT_USER** (det vill säga du se 503-fel), kontrollera om WinInet-proxyinställningarna är aktiverade för den **LOCAL_SYSTEM** konto (används av sensor updater tjänsten) genom att köra följande kommando i en kommandotolk med förhöjd behörighet:
 
    Reg jämför ”HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections” ”HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections” /v DefaultConnectionSettings

Om du får felet ”fel: Det gick inte att hitta den angivna registernyckeln eller registervärdet”. Det innebär att ingen proxyserver har angetts för den **LOCAL_SYSTEM** nivå
 
 ![lokalt system proxyfel](/media/proxy-local-system-error.png)

Om resultatet är ”resultatet Compared: olika” detta innebär att proxy är inställd för den **LOCAL_SYSTEM** men det är inte samma som den **CURRENT_USER**:
 
  ![Proxy resultatet jämfört med](/media/proxy-result-compared.png)

5.  Om den **LOCAL_SYSTEM** har inte rätt proxyinställningar (antingen inte konfigurerats eller skiljer sig från den **CURRENT_USER**), och du kan behöva kopiera proxyinställning från den **CURRENT_ ANVÄNDAREN** till den **LOCAL_SYSTEM**. Se till att säkerhetskopiera den här registernyckeln innan du ändrar den:

 Den aktuella användaren nyckeln: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings ”lokalt systemnyckel: HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\ DefaultConnectionSettings ”

 
6.  Slutför steg 4 och 5 för den**Local_Service** konto (det är samma som **Local_System** men bör vara S-1-5-19 i stället för S-1-5-18.



## <a name="see-also"></a>Se även
- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)