---
title: Konfigurera SAM-R för att aktivera laterala sökvägen i Azure ATP | Microsoft Docs
description: Beskriver hur du konfigurerar SAM-R för att aktivera laterala sökvägen i Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/17/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a529c9751fc993ec0913a54772d46161f39199f6
ms.sourcegitcommit: 8feb9b65dc0e1de0ace00aca11784e54f9852a15
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/17/2018
ms.locfileid: "39098176"
---
*Gäller för: Azure Avancerat skydd*

# <a name="install-azure-atp---step-8"></a>Installera Azure ATP - steg 8

>[!div class="step-by-step"]
[«Steg 7](install-atp-step7.md)
[steg 9»](atp-multi-forest.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Steg 8. Konfigurera SAM-R obligatoriska behörigheter

Den [lateral rörelsesökväg](use-case-lateral-movement-path.md) identifieringen baseras på frågor som identifierar lokala administratörer på specifika datorer. Dessa frågor utförs med SAM-R-protokollet via Azure ATP-Service-kontot som skapades i [steg 2. Anslut till AD](install-atp-step2.md).
 
Se till att Windows-klienter och servrar tillåta Azure ATP-konto för att utföra åtgärden SAM-R en ändring av **Grupprincip** måste göras för att lägga till kontot Azure ATP-tjänsten utöver de Konfigurera konton som visas i  **Nätverksåtkomst** princip.

1. Leta upp principen:

 - Principnamn: Nätverksåtkomst - begränsa klienter som har tillåtelse att göra fjärranrop till SAM
 - Plats: Datorkonfiguration, Windows-inställningar, säkerhetsinställningar, lokala principer, säkerhetsalternativ
  
  ![Leta upp principen](./media/samr-policy-location.png)

2. Lägg till Azure ATP-tjänsten i listan över godkända konton kan utföra den här åtgärden på de moderna Windows-System.
 
  ![Lägga till tjänsten](./media/samr-add-service.png)

3. Den **AATP Service** (Azure ATP tjänsten skapades under installation) har nu rätt behörighet för att utföra SAMR i miljön.

Mer information om SAM-R och den här grupprincipen, finns det [Nätverksåtkomst: begränsa klienter som har tillåtelse att göra fjärranrop till SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Steg 7](install-atp-step7.md)
[steg 9»](atp-multi-forest.md)



## <a name="see-also"></a>Se även
- [Utreda attacker med laterala sökväg med Azure ATP](use-case-lateral-movement-path.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)