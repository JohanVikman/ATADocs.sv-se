---
title: "Ändra konfigurationen för ATA Center (Advanced Threat Analytics ) | Microsoft Docs"
description: "Beskriver hur du ändrar IP-adress, port, konsol-URL eller certifikat för ATA Center."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Ändra konfigurationen för ATA Center


Efter den första distributionen bör ändringar i ATA Center genomföras med försiktighet. Följ stegen nedan när du uppdaterar IP-adressen och porten, konsolens URL och certifikatet.

## <a name="the-ata-center-ip-address"></a>IP-adressen för ATA Center

ATA Gateways lagrar IP-adressen till det ATA Center de behöver ansluta till lokalt. De ansluter regelbundet till ATA Center och hämtar konfigurationsändringar. Det är en process i två steg att ändra hur en ATA Gateway ansluter till ATA Center.

-   Steg ett: uppdatera IP-adressen och porten du vill att ATA Center-tjänsten ska använda. I det här läget lyssnar ATA Center fortfarande på den ursprungliga IP-adressen och nästa gång ATA Gateway synkroniserar sin konfiguration får den två IP-adresser till ATA Center. Så länge ATA Gateway kan ansluta genom att använda den ursprungliga (första) IP-adressen kommer den inte att försöka använda den nya IP-adressen och porten.

-   Steg två: när alla ATA Gateways har synkroniserats med den uppdaterade konfigurationen ska den nya IP-adressen och porten som ATA Center lyssnar på aktiveras. När du aktiverar den nya IP-adressen kopplas ATA Center-tjänsten till denna. ATA Gateways kommer inte att kunna ansluta till den ursprungliga adressen och försöker nu att ansluta till den andra (nya) IP-adressen till ATA Center. Efter anslutning till ATA Center med den nya IP-adressen hämtar ATA Gateway den senaste konfigurationen och har en enda IP-adress för ATA Center. (Såvida du inte startade processen igen.)

> [!NOTE]
> -   Om en ATA Gateway var offline under det första steget och aldrig fick den uppdaterade konfigurationen måste du uppdatera konfigurationens JSON-fil manuellt på ATA Gatewayen.
> -   Om den nya IP-adressen är installerad på ATA Center-servern kan du välja den i listan med IP-adresser när ändringen genomförs. Om du av någon anledning inte kan installera IP-adressen på ATA Center-servern kan du välja en anpassad IP-adress och lägga till denna manuellt. Du kan inte aktivera den nya IP-adressen innan den har installerats på servern.
> -   Om du behöver distribuera en ny ATA Gateway efter aktivering av den nya IP-adressen måste du hämta konfigurationspaketet för ATA Gateway igen.

## <a name="the-console-url"></a>Konsolens URL

URL:en används i följande scenarier:

-   Installation av ATA-gatewayer – när en ATA-gateway installeras registreras den i ATA Center. Registreringen utförs genom att ansluta till ATA-konsolen. Om du anger ett FQDN som ATA-konsolens URL måste du se till att ATA-gatewayen kan matcha detta FQDN till IP-adressen som ATA-konsolen är bunden till.

-   Aviseringar – när ATA skickar ut en SIEM- eller e-postavisering innehåller den en länk till den misstänkta aktiviteten. Värddelen av länken är URL-inställningen i ATA-konsolen.

-   Om du har installerat ett certifikat från din interna certifikatutfärdare (CA) bör du matcha URL:en till ämnesnamnet i certifikatet så att användarna inte får ett varningsmeddelande när de ansluter till ATA-konsolen.

-   Med ett FQDN som ATA-konsolens URL kan du ändra IP-adressen som används av ATA-konsolen utan att förstöra aviseringar som har skickats tidigare eller behöva ladda ned ATA Gateway-paketet igen. Du behöver bara uppdatera DNS med den nya IP-adressen.

> [!NOTE]
> När du har ändrat ATA-konsolens URL bör du ladda ned installationspaketet för ATA Gateway innan du installerar nya ATA-gatewayer.

## <a name="the-ata-center-certificate"></a>Certifikatet för ATA Center
Om certifikaten håller på att löpa ut och behöver förnyas eller ersättas när det nya certifikatet har installerats i det lokala datorarkivet på ATA Center-servern ersätter du certifikatet genom att följa denna metod i två steg:

-   Första steget – Uppdatera certifikatet som du vill att ATA Center-tjänsten ska använda. ATA Center-tjänsten är då fortfarande kopplad till det ursprungliga certifikatet. När ATA-gatewayerna synkar sin konfiguration har de två möjliga certifikat som är giltiga för ömsesidig autentisering. Så länge ATA-gatewayen kan ansluta med det ursprungliga certifikatet försöker den inte använda det nya.

-   Andra steget – När alla ATA-gatewayer har synkroniserats med den uppdaterade konfigurationen kan du aktivera det nya certifikatet som ATA Center-tjänsten är bunden till. När du aktiverar det nya certifikatet ska ATA Center-tjänsten bindas till certifikatet. ATA-gatewayer kan inte genomföra korrekt ömsesidig autentisering av ATA Center-tjänsten och försöker autentisera det andra certifikatet. Efter anslutning till ATA Center-tjänsten hämtar ATA-gatewayen den senaste konfigurationen och har ett enda certifikat för ATA Center. (Såvida du inte startade processen igen.)

> [!NOTE]
> -   Om en ATA Gateway var offline under det första steget och aldrig fick den uppdaterade konfigurationen måste du uppdatera konfigurationens JSON-fil manuellt på ATA Gatewayen.
> -   Certifikatet som du använder måste vara betrott av ATA-gatewayerna.
> -   Certifikatet används också för ATA-konsolen, så att det ska matcha ATA-konsolens adress för att undvika webbläsarvarningar
> -   Om du behöver distribuera en ny ATA-gateway efter aktivering av det nya certifikatet måste du hämta ATA-gatewaykonfigurationspaketet igen.

## <a name="changing-the-ata-center-configuration"></a>Ändra konfigurationen för ATA Center

1.  Öppna ATA-konsolen.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)

3.  Välj **Center**.

  ![Ändra ATA-konfiguration](media/change-center-config.png)

4.  Välj **Add custom DNS name / IP address** (Lägg till anpassat DNS-namn/IP-adress) under **URL** eller välj det nya certifikatet under **Certifikat**.

5.  Klicka på **Spara**.

6.  Ett meddelande om hur många ATA Gateways som har synkats med den senaste konfigurationen visas.

    >[!IMPORTANT]
    >Verifiera att alla ATA-gatewayer synkroniseras med den senaste konfigurationen innan du aktiverar den nya konfigurationen. Om den nya konfigurationen aktiveras innan alla ATA-gatewayer har synkroniserats kan ATA Gateway sluta att fungera som förväntat. Om någon ATA Gateway inte är synkroniserad får du det här felet när du klickar på Aktivera:


7.  När alla ATA-gatewayerna har synkroniserats klickar du på **Aktivera** för att aktivera den nya IP-adressen eller det nya certifikatet.

    > [!NOTE]
    > Om du har angett en anpassad IP-adress går det inte att klicka på **Aktivera** förrän du har installerat den IP-adressen på ATA Center.

8.  Se till att alla ATA Gateways kan synkronisera sina konfigurationer efter att ändringen har aktiverats. Meddelandefältet visar hur många ATA Gateway-konfigurationer som synkroniserats.




## <a name="see-also"></a>Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Ta en titt i ATA-forumet!](https://aka.ms/ata-forum)
