---
title: Ändra konfigurationen för ATA Center (Advanced Threat Analytics ) | Microsoft Docs
description: Beskriver hur du ändrar IP-adress, port, konsol-URL eller certifikat för ATA Center.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1d01b206cfab1edaef7774da5de8963e47fcb504
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133975"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Ändra konfigurationen för ATA Center


Efter den första distributionen bör ändringar i ATA Center genomföras med försiktighet. Använd följande procedurer när du uppdaterar konsolens URL och certifikatet.

## <a name="the-ata-console-url"></a>ATA-konsolens URL

URL:en används i följande scenarier:

-   Det här är den URL som används av ATA-gatewayer för att kommunicera med ATA Center.

- Installation av ATA-gatewayer – när en ATA-gateway installeras registreras den i ATA Center. Registreringen utförs genom att ansluta till ATA-konsolen. Om du anger ett FQDN som ATA-konsolens URL måste du se till att ATA-gatewayen kan matcha detta FQDN till IP-adressen som är bunden till ATA-konsolen.

-   Aviseringar – när ATA skickar ut en SIEM- eller e-postavisering innehåller den en länk till den misstänkta aktiviteten. Värddelen av länken är URL-inställningen i ATA-konsolen.

-   Om du har installerat ett certifikat från din interna certifikatutfärdare (CA) kan du matcha URL: en till ämnesnamnet i certifikatet. Detta förhindrar användare från att få ett varningsmeddelande när du ansluter till ATA-konsolen.

-   Med ett FQDN som ATA-konsolens URL kan du ändra IP-adressen som används av ATA-konsolen utan att förstöra aviseringar som tidigare eller ladda ned ATA Gateway-paketet igen. Du behöver bara uppdatera DNS med den nya IP-adressen.

1. Kontrollera att den nya URL som du vill använda som motsvarar IP-adressen för ATA-konsolen.

2. I ATA-inställningarna under **Center**, ange den nya URL. Nu använder ATA Center-tjänsten fortfarande den ursprungliga URL: en. 

 ![Ändra ATA-konfiguration](media/change-center-config.png)

  > [!NOTE]
  > Om du har angett en anpassad IP-adress kan du klicka på **aktivera** förrän du har installerat den IP-adressen på ATA Center.
    
3. Vänta tills ATA-gatewayer att synkronisera. Nu har de två möjliga URL: er via vilken du kan komma åt ATA-konsolen. Så länge ATA Gateway kan ansluta med hjälp av den ursprungliga URL: en, försöker den inte den nya servern.

4. När alla ATA-gatewayer har synkroniserats med den uppdaterade konfigurationen konfigurationssida Center klickar du på den **aktivera** knappen för att aktivera den nya URL: en. När du aktiverar den nya URL: en ATA-gatewayer nu att använda den nya URL: en till ATA Center. När du har anslutit till ATA Center-tjänsten, ATA Gateway kommer att hämta den senaste konfigurationen och har bara den nya URL för ATA-konsolen. 
5. 
 ![Aktivera certifikatet](media/center-activation.png)

> [!NOTE]
> -   Om en ATA Gateway var offline när du aktiverat den nya URL och aldrig fick den uppdaterade konfigurationen kan du manuellt uppdatera konfigurationens JSON-fil på ATA-gatewayen.
> -   Om du vill distribuera en ny ATA Gateway efter aktivering av den nya URL: en måste du hämta installationspaketet för ATA Gateway igen.


## <a name="the-ata-center-certificate"></a>Certifikatet för ATA Center

> [!WARNING]
> - Processen för att förnya ett befintligt certifikat stöds inte. Det är det enda sättet att förnya ett certifikat genom att skapa ett nytt certifikat och konfigurera ATA om du vill använda det nya certifikatet.


Ersätter du certifikatet genom att följa den här processen:

1. Innan det aktuella certifikatet upphör att gälla, skapa ett nytt certifikat och kontrollera att den är installerad på ATA Center-servern. <br></br>Vi rekommenderar att du väljer ett certifikat från en intern certifikatutfärdare, men det är också möjligt att skapa ett nytt självsignerat certifikat. Mer information finns i [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. I ATA-inställningarna under **Center**, välja det här nya certifikatet. ATA Center-tjänsten är då fortfarande kopplad till det ursprungliga certifikatet. 

 ![Ändra ATA-konfiguration](media/change-center-config.png)

3. Vänta tills ATA-gatewayer att synkronisera. Nu har de två möjliga certifikat som är giltiga för ömsesidig autentisering. Så länge ATA Gateway kan ansluta med det ursprungliga certifikatet, försöker den inte den nya servern.

4. När alla ATA-gatewayer har synkroniserats med den uppdaterade konfigurationen, kan du aktivera det nya certifikatet som ATA Center-tjänsten är bunden till. När du aktiverar det nya certifikatet Binder ATA Center-tjänsten till det nya certifikatet. ATA-gatewayer kan du nu använda det nya certifikatet för autentisering med ATA Center. När du har anslutit till ATA Center-tjänsten, ATA Gateway kommer att hämta den senaste konfigurationen och har det nya certifikatet för ATA Center. 

> [!NOTE]
> -   Om en ATA Gateway var offline när du har aktiverat det nya certifikatet och aldrig fick den uppdaterade konfigurationen kan du manuellt uppdatera konfigurationens JSON-fil på ATA-gatewayen.
> -   Certifikatet som du använder måste vara betrott av ATA-gatewayerna.
> -   Certifikatet används också för ATA-konsolen så att den ska matcha ATA-konsolens adress för att undvika webbläsarvarningar.
> -   Om du behöver distribuera en ny ATA-gateway efter aktivering av det nya certifikatet måste du hämta ATA-gatewaykonfigurationspaketet igen.



 
## <a name="see-also"></a>Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Ta en titt i ATA-forumet!](https://aka.ms/ata-forum)
