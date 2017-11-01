---
title: "Installera Advanced Threat Analytics – steg 7 | Microsoft Docs"
description: "I det här steget av ATA-installationen kan du integrera din VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 748121a709ac05756edf34e04e13b996190e9711
ms.sourcegitcommit: b951c64228d4f165ee1fcc5acc0ad6bb8482d6a2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-7"></a>Installera ATA – steg 7

>[!div class="step-by-step"]
[«Steg 5](install-ata-step5.md)
[steg 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Steg 7. Integrera VPN

Microsoft Advanced Threat Analytics (ATA) version 1.8 kan samla in redovisningsinformation från VPN-lösningar. När konfigurerats tas användarens profilsida information från VPN-anslutningar, till exempel IP-adresser och platser där anslutningar har sitt ursprung. Detta kompletterar undersökningsprocessen ger ytterligare information om användaraktivitet. Anrop att matcha en extern IP-adress till en plats är anonym. Ingen personligt ID skickas i det här anropet.

ATA kan integreras med din VPN-lösning genom att lyssna på RADIUS-redovisningshändelser som vidarebefordras till ATA-gatewayer. Den här mekanismen baseras på standard RADIUS-redovisning ([RFC 2866](https://tools.ietf.org/html/rfc2866)), och följande leverantörer stöds:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Förutsättningar

Om du vill aktivera VPN integration måste du ange följande:

-   Öppna porten UDP 1813 på ATA-gatewayer och ATA Lightweight-gatewayer.

-   Ansluta ATA Center till Internet så att den kan fråga platsen för inkommande IP-adresser.

I exemplet nedan använder vi Microsoft Routing and Remote Access Server (RRAS) för att beskriva den VPN-konfigurationen.

Om du använder en 3 part VPN-lösning dokumentationen sina anvisningar om hur du aktiverar RADIUS-redovisning.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurera RADIUS-redovisning på VPN-system

Utför följande på RRAS-servern.
 
1.  Öppna konsolen Routning och fjärråtkomst.
2.  Högerklicka på namnet på servern och på **egenskaper**.
3.  I den **säkerhet** fliken, under **redovisning providern**väljer **RADIUS-redovisning** och på **konfigurera**.

    ![RADIUS-installationen](./media/radius-setup.png)

4.  I den **Lägg till RADIUS-Server** fönster, Skriv den **servernamn** närmaste ATA Gateway eller ATA Lightweight Gateway. Under **Port**, kontrollera standard 1813 har konfigurerats. Klicka på **ändra** och Skriv en ny delad hemlig sträng med alfanumeriska tecken som du kan komma ihåg. Du måste fylla i det senare i ATA-konfiguration. Kontrollera den **skicka RADIUS-konto och redovisning inaktivera meddelanden** och klicka sedan på **OK** på alla öppna dialogrutor.
 
     ![VPN-konfiguration](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurera VPN i ATA

ATA samlar in VPN som hjälper profil platser från vilka datorer ansluta till nätverket och för att kunna identifiera onormalt VPN-anslutningar.

Konfigurera VPN-data i ATA:

1.  Öppna sidan ATA-konfiguration i ATA-konsolen och gå till **VPN**.
 
  ![ATA config-menyn](./media/config-menu.png)

2.  Aktivera **RADIUS-redovisning** på, och Skriv den **delad hemlighet** du tidigare konfigurerat på RRAS VPN-servern. Klicka sedan på **Spara**.
 

  ![Konfigurera ATA VPN](./media/vpn.png)


När den är aktiverad, lyssna alla ATA-gatewayer och Lightweight-gatewayer på porten 1813 för RADIUS-redovisningshändelser. 

Installationen är klar och du ser nu VPN-aktivitet i användarnas profilsida:
 
   ![VPN-konfiguration](./media/vpn-user.png)

När ATA-gatewayen tar emot VPN-händelser och skickar dem till ATA Center för bearbetning, behöver ATA Center Internet-anslutning för HTTPS-port 443 för att kunna matcha de externa IP-adresserna i VPN-händelser till deras geolokalisering.





>[!div class="step-by-step"]
[« Steg 6](install-ata-step5.md)
[Steg 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Relaterade videor
- [Översikt över ATA-distribution](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Välja rätt ATA Gateway-typ](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [ATA POC Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

