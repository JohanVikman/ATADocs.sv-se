---
title: Konfigurera SAM-R om du vill aktivera lateral förflyttning sökväg identifiering Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du konfigurerar SAM-R för att kunna identifiera lateral förflyttning-sökvägen i Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/25/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6e32f3ce59b049d0ced68a1330eefca7315bf49d
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298375"
---
*Gäller för: Advanced Threat Analytics version 1.9.*

# <a name="install-ata---step-9"></a>Installera ATA – steg 9

>[!div class="step-by-step"]
[«Steg 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Steg 9. Konfigurera SAM-R krävs behörigheter

Den [lateral förflyttning sökvägen](use-case-lateral-movement-path.md) identifiering förlitar sig på frågor som identifierar lokala administratörer på specifika datorer. De här frågorna utförs via SAM-R-protokollet via ATA tjänstkontot som skapats i [steg 2. Anslut till AD](install-ata-step2.md).
 
Att se till att Windows-klienter och servrar tillåter ATA-tjänstkontot för denna åtgärd SAM-R, en ändring av din **Grupprincip** måste göras som lägger till ATA-tjänstkontot förutom konfigurerade kontona i den **nätverksåtkomst** princip.

1. Leta upp principen:

 - Principnamn: Nätverksåtkomst - begränsa klienter kan göra fjärranrop till SAM
 - Plats: Datorkonfiguration, Windows-inställningar, säkerhetsinställningar, lokala principer, säkerhetsalternativ
  
  ![Leta upp principen](./media/samr-policy-location.png)

2. Lägga till ATA-tjänsten i listan över godkända konton kan utföra denna åtgärd på moderna Windows-datorer.
 
  ![Lägga till tjänsten](./media/samr-add-service.png)

3. Den **ATA-tjänsten** (ATA-tjänsten skapas under installationen) nu har rätt behörighet för att utföra SAMR i miljön.

Mer information om SAM-R- och den här grupprincipen finns i [Nätverksåtkomst: begränsa klienter kan göra fjärranrop till SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Steg 8](install-ata-step7.md)

## <a name="see-also"></a>Se även
- [ATA POC Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)
