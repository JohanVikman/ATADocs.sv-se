---
title: Konfigurera SAM-R för att aktivera identifiering av lateral förflyttning sökväg i Azure ATP | Microsoft Docs
description: Beskriver hur du konfigurerar SAM-R för att aktivera identifiering av lateral förflyttning sökväg i Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24b42c5425933d8931a85e0ba454a69e0ca94a21
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298300"
---
*Gäller för: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Installera Azure ATP - steg 8

>[!div class="step-by-step"]
[«Steg 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Steg 8. Konfigurera SAM-R krävs behörigheter

Den [lateral förflyttning sökvägen](use-case-lateral-movement-path.md) identifiering förlitar sig på frågor som identifierar lokala administratörer på specifika datorer. De här frågorna utförs via SAM-R-protokollet via Azure ATP kontot skapas i [steg 2. Anslut till AD](install-atp-step2.md).
 
Se till att Windows-klienter och servrar Tillåt Azure ATP-konto för att utföra åtgärden SAM-R en ändring av **Grupprincip** måste göras för att lägga till tjänstkontot Azure ATP förutom konfigurerade kontona i  **Nätverksåtkomst** princip.

1. Leta upp principen:

 - Principnamn: Nätverksåtkomst - begränsa klienter kan göra fjärranrop till SAM
 - Plats: Datorkonfiguration, Windows-inställningar, säkerhetsinställningar, lokala principer, säkerhetsalternativ
  
  ![Leta upp principen](./media/samr-policy-location.png)

2. Lägg till tjänsten Azure ATP i listan över godkända konton kan utföra denna åtgärd på moderna Windows-datorer.
 
  ![Lägga till tjänsten](./media/samr-add-service.png)

3. Den **AATP Service** (Azure ATP tjänsten skapas under installationen) nu har rätt behörighet för att utföra SAMR i miljön.

Mer information om SAM-R- och den här grupprincipen finns i [Nätverksåtkomst: begränsa klienter kan göra fjärranrop till SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Steg 7](install-atp-step7.md)



## <a name="see-also"></a>Se även
- [Undersöka lateral förflyttning sökväg attacker med Azure ATP](use-case-lateral-movement-path.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)