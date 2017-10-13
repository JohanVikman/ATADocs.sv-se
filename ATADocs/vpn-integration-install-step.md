---
title: "Installera Advanced Threat Analytics – steg 7 | Microsoft Docs"
description: "I det här steget av ATA-installationen kan du integrera din VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02649a6acb6a083145ba81b3b9c1647e7f8ea2a
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/09/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-7"></a>Installera ATA – steg 7

>[!div class="step-by-step"]
[«Steg 5](install-ata-step5.md)
[steg 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Steg 7. Integrera VPN

### <a name="configuring-vpn"></a>Konfigurera VPN

ATA samlar in VPN som hjälper profil platser från vilka datorer ansluta till nätverket och för att kunna identifiera onormalt VPN-anslutningar.

Konfigurera VPN-data i ATA:

1. Gå till **Configuration** och klicka sedan på den **VPN** fliken.

2. Ange den **konto delad hemlighet** av RADIUS-servern. Om du vill hämta den delade hemligheten finns i VPN-dokumentationen.

 ![Konfigurera ATA VPN](media/vpn.png)

3.  När den är aktiverad, lyssna alla ATA-gatewayer och Lightweight-gatewayer på porten 1813 för RADIUS-redovisningshändelser. 

4.  Den VPN RADIUS-redovisningshändelser ska vidarebefordras till ATA Gateway eller ATA Lightweight Gateway när det har konfigurerats.

5.  När ATA-gatewayen tar emot VPN-händelser och skickar dem till ATA Center för bearbetning, behöver ATA Center Internet-anslutning för HTTPS-port 443 för att kunna matcha de externa IP-adresserna i VPN-händelser till deras geolokalisering.

Anrop att matcha en extern IP-adress till en plats är anonym. Ingen personligt ID skickas i det här anropet.

Följande VPN-leverantörer stöds:
- Microsoft
- F5
- Check Point
- Cisco ASA




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

