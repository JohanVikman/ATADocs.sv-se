---
title: Installera Azure Advanced Threat Protection – steg 6 | Microsoft Docs
description: I det här steget för att installera ATP integrera du ditt VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ce1bbbda96cc8a10b026f2f422ac79b1b2bae55
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454113"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-6"></a>Installera Azure ATP - steg 6

> [!div class="step-by-step"]
> [« Steg 5](install-atp-step5.md)
> [Steg 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Steg 6. Integrera VPN

Azure Advanced Threat Protection (ATP) kan samla in redovisningsinformation från VPN-lösningar. När konfigurerad, omfattar information från VPN-anslutningar, till exempel IP-adresser och platser där anslutningar har sitt ursprung i användarens profilsida. Detta kompletterar undersökningsprocessen genom att tillhandahålla ytterligare information om användaren som en ny identifiering av onormal VPN-anslutningar. Anropet för att lösa en extern IP-adress till en plats är anonyma. Ingen personligt ID skickas i det här anropet.

Azure ATP kan integreras med din VPN-lösning genom att lyssna på RADIUS-redovisningshändelser som vidarebefordras till Azure ATP-sensorer. Den här mekanismen baseras på standard RADIUS-redovisning ([RFC 2866](https://tools.ietf.org/html/rfc2866)), och följande VPN-leverantörer stöds:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Krav

Om du vill aktivera VPN-integrering, se till att ange följande parametrar:

-   Öppna port 1813 med UDP på din Azure ATP fristående sensorer och Azure ATP-sensorn.


I exemplet nedan används Microsoft Routing and Remote Access Server (RRAS) för att beskriva konfigurationsprocessen VPN.

Om du använder en VPN-lösning från tredje part dokumentationen sina anvisningar om hur du aktiverar RADIUS-redovisning.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurera RADIUS-redovisning på VPN-system

Utför följande steg på RRAS-servern.
 
1.  Öppna konsolen Routning och fjärråtkomst.
2.  Högerklicka på servernamnet och klickar på **egenskaper**.
3.  I den **Security** fliken, under **redovisning providern**väljer **RADIUS-redovisning** och klicka på **konfigurera**.

    ![RADIUS-konfiguration](./media/radius-setup.png)

4.  I den **Lägg till RADIUS-Server** fönster och skriver den **servernamn** närmaste Azure ATP fristående sensorn eller Azure ATP-sensorn. Under **Port**, kontrollera standard 1813 har konfigurerats. Klicka på **ändra** och Skriv en ny delad hemlighet sträng med alfanumeriska tecken som du kan komma ihåg. Du måste fylla i det senare i din Azure ATP-konfiguration. Kontrollera den **skicka RADIUS-konto och redovisning inaktivera meddelanden** rutan och klicka sedan på **OK** på alla öppna dialogrutor.
 
     ![VPN-konfigurationen](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurera VPN i ATP

Azure ATP samlar in VPN-data som hjälper till att profilen platser från vilka datorer ansluta till nätverket och för att kunna identifiera misstänkt VPN-anslutningar.

Konfigurera VPN-data i ATP:

1.  I Azure ATP-arbetsyteportalen, klickar du på kugghjulet för konfiguration och sedan **VPN**.
 

2.  Aktivera **RADIUS-redovisning**, och Skriv den **delad hemlighet** du tidigare konfigurerat på RRAS VPN-servern. Klicka sedan på **Spara**.
 

  ![Konfigurera Azure ATP-VPN](./media/atp-vpn-radius.png)


När detta är aktiverat kommer port alla Azure ATP fristående sensorer och sensorer lyssnar på 1813 för RADIUS-redovisningshändelser. 

Din konfiguration har slutförts. 

När Azure ATP-sensorn tar emot VPN-händelser och skickar dem till Azure ATP-Molntjänsten för bearbetning, entitetsprofilen visar distinkta används VPN-platser och aktiviteter i profilen visar platser.





> [!div class="step-by-step"]
> [«Steg 6](install-atp-step5.md)
> [steg 7»](install-atp-step7.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
