---
title: Azure Advanced Threat Protection avancerade Audit Principkontrollen | Microsoft Docs
description: Den här artikeln innehåller en översikt över Azure ATP avancerad granskningsprincip kontroll.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7207388702c659a08258862326ee89a49ae3ac2
ms.sourcegitcommit: f3f80c5d3e2e5c1bcf975ae0cbae1469da7ab74d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/12/2018
ms.locfileid: "44515516"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-advanced-audit-policy-check"></a>Azure ATP avancerad granskningsprincip-kontroll

Azure ATP-identifieringen baseras på specifika Windows händelseloggar för synlighet i vissa fall, till exempel NTLM-inloggningar, gruppändringar för säkerhet och liknande händelser. För rätt händelser som granskas och ingår i Windows-händelseloggen, kräva domänkontrollanterna korrekta inställningar för avancerad granskningsprincip. Felaktiga inställningar av avancerad granskningsprincip lämna kritiska händelser från loggar, och resultatet i ofullständig Azure ATP-täckning.

Om du vill göra det enklare att verifiera den aktuella statusen för var och en av din domänkontrollant avancerade granskningsprinciper, kontrollerar Azure ATP automatiskt dina befintliga avancerade granskningsprinciper och problem hälsovarningar för principinställningar som behöva ändras. Varje hälsoavisering innehåller specifik information om domänkontrollanten, den problematiska principen samt åtgärdsförslag.

![Hälsoavisering för avancerade granskningsprinciper princip](media/atp-health-alert-audit-policy.png)


Avancerade granskningsprincip är aktiverat via **standardprincip för domänkontrollanter** grupprincipobjekt. Dessa granska händelser som ska registreras på domänkontrollantens Windows-händelser. 

<br>Ändra granskningsprinciper avancerade för domänkontrollanten att följa dessa anvisningar:

1. Logga in på servern som **domänadministratören**.
2. Läsa in redigeraren för Grupprinciphantering från **Serverhanteraren** > **verktyg** > **Grupprinciphantering**. 
3. Expandera den **organisationsenheter i domänen domänkontrollanter**, högerklicka på **standardprincip för domänkontrollanter** och välj **redigera**. 

    ![Redigera princip för domänkontrollant](media/atp-advanced-audit-policy-check-step-1.png)

4. Från fönstret som öppnas, går du till **Datorkonfiguration** > **principer** > **Windows-inställningar**  >  **Säkerhetsinställningar** > **konfiguration av avancerad granskningsprincip**.

    ![Konfiguration av avancerade granskningsprinciper](media/atp-advanced-audit-policy-check-step-2.png)

5. Gå till kontoinloggning, dubbelklicka på **granska verifiering av autentiseringsuppgifter** och välj **konfigurera följande granskningshändelser** för både lyckade och misslyckade händelser. 

    ![Verifiering av autentiseringsuppgifter](media/atp-advanced-audit-policy-check-step-3.png)

6. Gå till kontohantering, dubbelklicka på **granska grupp säkerhetshantering** och välj **konfigurera följande granskningshändelser** för både lyckade och misslyckade händelser.

    ![Granska hantering av säkerhetsgrupp](media/atp-advanced-audit-policy-check-step-4.png)

7. Efter att de via GPO nya händelser visas under din **Windows-händelseloggar**.

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
