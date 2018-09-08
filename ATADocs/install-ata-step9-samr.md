---
title: Konfigurera SAM-R för att aktivera laterala sökväg i Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du konfigurerar SAM-R för att aktivera identifiering av laterala sökväg i Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a1de6e0f3d5234eb96d710b54ded8c8a894f440
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125745"
---
*Gäller för: Advanced Threat Analytics version 1.9*

# <a name="install-ata---step-9"></a>Installera ATA – steg 9

>[!div class="step-by-step"]
[«Steg 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Steg 9. Konfigurera SAM-R obligatoriska behörigheter

Den [lateral rörelsesökväg](use-case-lateral-movement-path.md) identifieringen baseras på frågor som identifierar lokala administratörer på specifika datorer. Dessa frågor utförs med SAM-R-protokollet via ATA tjänstkontot som skapats i [steg 2. Anslut till AD](install-ata-step2.md).
 
Att se till att Windows-klienter och servrar tillåter ATA-tjänstkontot för den här SAM-R-åtgärden, en ändring av din **Grupprincip** måste göras som lägger till ATA-tjänstkontot utöver de Konfigurera konton som visas i den **nätverksåtkomst** princip.

1. Leta upp principen:

 - Principnamn: Nätverksåtkomst - begränsa klienter som har tillåtelse att göra fjärranrop till SAM
 - Plats: Datorkonfiguration, Windows-inställningar, säkerhetsinställningar, lokala principer, säkerhetsalternativ
  
  ![Leta upp principen](./media/samr-policy-location.png)

2. Lägg till ATA-tjänsten i listan över godkända konton kan utföra den här åtgärden på de moderna Windows-System.
 
  ![Lägga till tjänsten](./media/samr-add-service.png)

3. Den **ATA-tjänsten** (ATA-tjänsten skapas under installationen) har nu rätt behörighet för att utföra SAM-R i miljön.

> [!NOTE]
> Kontrollera att miljön förblir säkert, utan att påverka programkompatibilitet genom att aktivera och verifiera dina föreslagna ändringar i granskningsläge innan de verkställer nya principer. 

 Mer information om SAM-R och grupprinciper finns i [Nätverksåtkomst: begränsa klienter som har tillåtelse att göra fjärranrop till SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Steg 8](install-ata-step7.md)

## <a name="see-also"></a>Se även
- [ATA POC-Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)
