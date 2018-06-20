---
title: Ändra konfigurationen för ATA Center (Advanced Threat Analytics ) | Microsoft Docs
description: Beskriver hur du ändrar IP-adress, port, konsol-URL eller certifikat för ATA Center.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 294b9204f9ca6a40a835e5360a7011947e3255b4
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010048"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="modifying-the-ata-center-configuration"></a>Ändra konfigurationen för ATA Center


Efter den första distributionen bör ändringar i ATA Center genomföras med försiktighet. Använd följande procedurer när du uppdaterar konsolen URL-Adressen och certifikatet.

## <a name="the-ata-console-url"></a>ATA-konsolens URL

URL:en används i följande scenarier:

-   Det här är den URL som används av ATA-gatewayer för att kommunicera med ATA Center.

- Installation av ATA-gatewayer – när en ATA-gateway installeras registreras den i ATA Center. Registreringen utförs genom att ansluta till ATA-konsolen. Om du anger ett FQDN som ATA-konsolens URL måste du se till att ATA-gatewayen kan matcha detta FQDN till IP-adress som är bunden till ATA-konsolen.

-   Aviseringar – när ATA skickar ut en SIEM- eller e-postavisering innehåller den en länk till den misstänkta aktiviteten. Värddelen av länken är URL-inställningen i ATA-konsolen.

-   Om du har installerat ett certifikat från din interna certifikatutfärdare (CA) måste matcha URL: en till ämnesnamnet i certifikatet. Detta förhindrar användare från att få en varning visas när du ansluter till ATA-konsolen.

-   Med ett FQDN som ATA-konsolens URL kan du ändra IP-adressen som används av ATA-konsolen utan att förstöra tidigare aviseringar eller hämta ATA Gateway-paketet igen. Du behöver bara uppdatera DNS med den nya IP-adressen.

1. Kontrollera att den nya URL som du vill använda matchar IP-adressen för ATA-konsolen.

2. I ATA-inställningarna under **Center**, ange den nya URL. Nu kan ATA Center-tjänsten fortfarande använder den ursprungliga URL: en. 

 ![Ändra ATA-konfiguration](media/change-center-config.png)

  > [!NOTE]
  > Om du har angett en anpassad IP-adress kan du klicka på **aktivera** förrän du har installerat den IP-adressen på ATA Center.
    
3. Vänta tills ATA-gatewayer att synkronisera. Det har två möjliga URL: er via vilken du kan komma åt ATA-konsolen. Så länge ATA Gateway kan ansluta med hjälp av den ursprungliga URL: en kan försöker den inte den nya servern.

4. När alla ATA-gatewayer synkroniseras med den uppdaterade konfigurationen i konfigurationssidan Center klickar du på den **aktivera** för att aktivera den nya URL. När du aktiverar den nya URL ATA-gatewayer nu att använda den nya URL till ATA Center. Efter anslutning till ATA Center-tjänsten, ATA Gateway kommer att hämta den senaste konfigurationen och har bara den nya URL för ATA-konsolen. 
5. 
 ![Aktivera certifikatet](media/center-activation.png)

> [!NOTE]
> -   Om en ATA Gateway var offline när du aktiverat den nya URL och aldrig fick den uppdaterade konfigurationen, manuellt uppdatera konfigurationens JSON-fil på ATA Gateway.
> -   Om du behöver distribuera en ny ATA Gateway efter aktivering av den nya URL som du behöver hämta installationspaketet för ATA Gateway igen.


## <a name="the-ata-center-certificate"></a>Certifikatet för ATA Center

> [!WARNING]
> - Processen för att förnya ett befintligt certifikat stöds inte. Det enda sättet att förnya ett certifikat är genom att skapa ett nytt certifikat och hur du konfigurerar ATA för att använda det nya certifikatet.


Ersätter du certifikatet genom att följa den här processen:

1. Innan det aktuella certifikatet upphör att gälla, skapa ett nytt certifikat och kontrollera att den är installerad på ATA Center-servern. <br></br>Vi rekommenderar att du väljer ett certifikat från en intern certifikatutfärdare, men det är också möjligt att skapa ett nytt självsignerat certifikat. Mer information finns i [ny SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. I ATA-inställningarna under **Center**, Välj nyligen skapade certifikatet. ATA Center-tjänsten är nu fortfarande kopplad till det ursprungliga certifikatet. 

 ![Ändra ATA-konfiguration](media/change-center-config.png)

3. Vänta tills ATA-gatewayer att synkronisera. Det har två möjliga certifikat som är giltiga för ömsesidig autentisering. Så länge ATA Gateway kan ansluta med det ursprungliga certifikatet kan försöker den inte den nya servern.

4. När alla ATA-gatewayer synkroniseras med den uppdaterade konfigurationen, kan du aktivera det nya certifikatet som ATA Center-tjänsten är bunden till. När du aktiverar det nya certifikatet Binder ATA Center-tjänsten till det nya certifikatet. ATA-gatewayer nu använda det nya certifikatet för autentisering med ATA Center. Efter anslutning till ATA Center-tjänsten, ATA Gateway kommer att hämta den senaste konfigurationen och har det nya certifikatet för ATA Center. 

> [!NOTE]
> -   Om en ATA Gateway var offline när du har aktiverat det nya certifikatet och aldrig fick den uppdaterade konfigurationen, manuellt uppdatera konfigurationens JSON-fil på ATA Gateway.
> -   Certifikatet som du använder måste vara betrott av ATA-gatewayerna.
> -   Certifikatet används också för ATA-konsolen så att den matcha adressen som ATA-konsolen för att undvika webbläsarvarningar.
> -   Om du behöver distribuera en ny ATA-gateway efter aktivering av det nya certifikatet måste du hämta ATA-gatewaykonfigurationspaketet igen.



 
## <a name="see-also"></a>Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Ta en titt i ATA-forumet!](https://aka.ms/ata-forum)
