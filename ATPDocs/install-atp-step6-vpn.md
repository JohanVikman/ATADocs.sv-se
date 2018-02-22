---
title: Installera Azure Advanced Threat Protection - steg 6 | Microsoft Docs
description: "I det här steget av installationen ATP integrera din VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-6"></a>Installera Azure ATP - steg 6

>[!div class="step-by-step"]
[« Steg 5](install-atp-step5.md)
[Steg 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Steg 6. Integrera VPN

Azure Advanced Threat Protection (ATP) kan samla in redovisningsinformation från VPN-lösningar. När konfigurerats omfattar användarens profilsida information från VPN-anslutningar, till exempel IP-adresser och platser där anslutningar har sitt ursprung. Detta kompletterar undersökningsprocessen ger ytterligare information om användaren som en ny identifiering för onormalt VPN-anslutningar. Anrop att matcha en extern IP-adress till en plats är anonym. Ingen personligt ID skickas i det här anropet.

Azure ATP integreras med din VPN-lösning genom att lyssna på RADIUS-redovisningshändelser som vidarebefordras till Azure ATP sensorer. Den här mekanismen baseras på standard RADIUS-redovisning ([RFC 2866](https://tools.ietf.org/html/rfc2866)), och följande leverantörer stöds:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Krav

Om du vill aktivera VPN-integrering, se till att ange följande parametrar:

-   Öppna porten UDP 1813 på Azure ATP fristående sensorer och Azure ATP sensor.


Exemplet nedan använder Microsoft Routing and Remote Access Server (RRAS) för att beskriva den VPN-konfigurationen.

Om du använder en VPN-lösning från tredje part dokumentationen sina anvisningar om hur du aktiverar RADIUS-redovisning.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurera RADIUS-redovisning på VPN-system

Utför följande steg på RRAS-servern.
 
1.  Öppna konsolen Routning och fjärråtkomst.
2.  Högerklicka på namnet på servern och på **egenskaper**.
3.  I den **säkerhet** fliken, under **redovisning providern**väljer **RADIUS-redovisning** och på **konfigurera**.

    ![RADIUS-installationen](./media/radius-setup.png)

4.  I den **Lägg till RADIUS-Server** fönster, Skriv den **servernamn** närmaste Azure ATP fristående sensor eller Azure ATP sensor. Under **Port**, kontrollera standard 1813 har konfigurerats. Klicka på **ändra** och Skriv en ny delad hemlig sträng med alfanumeriska tecken som du kan komma ihåg. Du måste fylla i det senare i Azure ATP konfigurationen. Kontrollera den **skicka RADIUS-konto och redovisning inaktivera meddelanden** och klicka sedan på **OK** på alla öppna dialogrutor.
 
     ![VPN-konfiguration](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurera VPN i ATP

Azure ATP samlar in VPN som hjälper profil platser från vilka datorer ansluta till nätverket och för att kunna identifiera onormalt VPN-anslutningar.

Konfigurera VPN-data i ATP:

1.  I arbetsytan ATP Azure-portalen klickar du på kugghjulet för konfiguration och sedan **VPN**.
 

2.  Aktivera **RADIUS-redovisning**, och Skriv den **delad hemlighet** du tidigare konfigurerat på RRAS VPN-servern. Klicka sedan på **Spara**.
 

  ![Konfigurera Azure ATP VPN](./media/atp-vpn-radius.png)


När den är aktiverad, port alla Azure ATP fristående sensorer och sensorer lyssnar på 1813 för RADIUS-redovisningshändelser. 

Installationen har slutförts. 

När Azure ATP-sensor tar emot VPN-händelser och skickar dem till Azure ATP-Molntjänsten för bearbetning, entitetsprofilen visar distinkta komma åt VPN-platser och aktiviteter i profilen visar platser.





>[!div class="step-by-step"]
[«Steg 6](install-atp-step5.md)
[steg 7»](install-atp-step7.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
