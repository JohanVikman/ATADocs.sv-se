---
title: Installera Advanced Threat Analytics – steg 7 | Microsoft Docs
description: I det här steget av ATA-installationen kan du integrera ditt VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a6396013be0efaa5ae68e3fb8849c50af28876c7
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126090"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="install-ata---step-7"></a>Installera ATA – steg 7

>[!div class="step-by-step"]
[«Steg 5](install-ata-step5.md)
[steg 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Steg 7. Integrera VPN

Microsoft Advanced Threat Analytics (ATA) version 1.8 kan samla in redovisningsinformation från VPN-lösningar. När konfigurerad, omfattar information från VPN-anslutningar, till exempel IP-adresser och platser där anslutningar har sitt ursprung i användarens profilsida. Detta kompletterar undersökningsprocessen genom att tillhandahålla ytterligare information om användaraktivitet. Anropet för att lösa en extern IP-adress till en plats är anonyma. Ingen personligt ID skickas i det här anropet.

ATA kan integreras med din VPN-lösning genom att lyssna på RADIUS-redovisningshändelser som vidarebefordras till ATA-gatewayer. Den här mekanismen baseras på standard RADIUS-redovisning ([RFC 2866](https://tools.ietf.org/html/rfc2866)), och följande VPN-leverantörer stöds:

-   Microsoft
-   F5
-   Cisco ASA

## <a name="prerequisites"></a>Krav

Om du vill aktivera VPN-integrering, se till att ange följande parametrar:

-   Öppna port 1813 med UDP på ATA-gatewayer och ATA Lightweight-gatewayer.

-   ATA Center måste kunna komma åt *ti.ata.azure.com* med hjälp av HTTPS (port 443) så att den kan fråga platsen för inkommande IP-adresser.

I exemplet nedan används Microsoft Routing and Remote Access Server (RRAS) för att beskriva konfigurationsprocessen VPN.

Om du använder en VPN-lösning från tredje part dokumentationen sina anvisningar om hur du aktiverar RADIUS-redovisning.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurera RADIUS-redovisning på VPN-system

Utför följande steg på RRAS-servern.
 
1.  Öppna konsolen Routning och fjärråtkomst.
2.  Högerklicka på servernamnet och klickar på **egenskaper**.
3.  I den **Security** fliken, under **redovisning providern**väljer **RADIUS-redovisning** och klicka på **konfigurera**.

    ![RADIUS-konfiguration](./media/radius-setup.png)

4.  I den **Lägg till RADIUS-Server** fönster och skriver den **servernamn** närmaste ATA Gateway eller ATA Lightweight Gateway. Under **Port**, kontrollera standard 1813 har konfigurerats. Klicka på **ändra** och Skriv en ny delad hemlighet sträng med alfanumeriska tecken som du kan komma ihåg. Du måste fylla i det senare i ATA-konfigurationen. Kontrollera den **skicka RADIUS-konto och redovisning inaktivera meddelanden** rutan och klicka sedan på **OK** på alla öppna dialogrutor.
 
     ![VPN-konfigurationen](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurera VPN i ATA

ATA samlar in VPN-data och identifierar när och där autentiseringsuppgifter används via VPN och integrerar data i din undersökning. Detta ger ytterligare information för att undersöka aviseringar som rapporteras av ATA.

Konfigurera VPN-data i ATA:

1.  Öppna sidan ATA-konfiguration i ATA-konsolen och gå till **VPN**.
 
  ![ATA-konfigurationsmeny](./media/config-menu.png)

2.  Aktivera **RADIUS-redovisning**, och Skriv den **delad hemlighet** du tidigare konfigurerat på RRAS VPN-servern. Klicka sedan på **Spara**.
 

  ![Konfigurera VPN för ATA](./media/vpn.png)


När den är aktiverad, lyssnar alla ATA gateway och Lightweight gateway på port 1813 för RADIUS-redovisningshändelser. 

Din konfiguration är klar och du kan nu se VPN-aktivitet i användarens profilsida:
 
   ![VPN-konfigurationen](./media/vpn-user.png)

När ATA-gatewayen tar emot VPN-händelser och skickar dem till ATA Center för bearbetning, ATA Center behöver åtkomst till *ti.ata.azure.com* med hjälp av HTTPS (port 443) för att kunna matcha de externa IP-adresserna i VPN-händelser till deras geografiska plats.




>[!div class="step-by-step"]
[« Steg 6](install-ata-step5.md)
[Steg 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Relaterade videor
- [Översikt över ATA-distribution](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Välja rätt typ av ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [ATA POC-Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

