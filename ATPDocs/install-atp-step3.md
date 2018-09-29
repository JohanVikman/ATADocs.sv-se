---
title: Installera Azure Advanced Threat Protection – steg 3 | Microsoft Docs
description: Steg tre av Azure ATP-installationen kan du hämta installationspaketet för Azure ATP fristående sensorn.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 96d459bd00d39bb21ce363d079b5b24ceca4ace7
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454028"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-3"></a>Installera Azure ATP - steg 3

> [!div class="step-by-step"]
> [« Steg 2](install-atp-step2.md)
> [Steg 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Steg 3. Hämta installationspaketet för Azure ATP-sensorn
När du har konfigurerat anslutningsinställningarna för domänen, kan du hämta installationspaketet för Azure ATP-sensorn. Azure ATP-sensorn installationspaketet kan installeras på en dedikerad server eller på en domänkontrollant. När du installerar direkt på en domänkontrollant, den installeras som en Azure ATP-sensorn när du installerar på en dedikerad server och använda portspegling kan den installeras som fristående Azure ATP-sensorn. Läs mer på Azure ATP-sensorn [Azure ATP-arkitektur](atp-architecture.md). 

Klicka på **hämta** i listan med steg överst på sidan för att gå till den **Sensor** sidan.

![Konfigurationsinställningar för Azure ATP-sensorn](media/atp-sensor-config.png)

> [!NOTE] 
> För att nå konfigurationsskärmen sensor senare, klickar du på den **inställningsikonen** (uppe till höger) och välj **Configuration**, sedan, under **System**, klickar du på **sensor**.  

1.  Klicka på **sensor**.
2.  Spara paketet lokalt.
3.  Kopiera den **åtkomstnyckel**. Åtkomstnyckeln krävs för Azure ATP-sensorn att ansluta till din Azure ATP-arbetsyta. Åtkomstnyckeln är en en-gång-lösenord för sensor distribution, varefter utförs all kommunikation med hjälp av certifikat för autentisering och TLS-kryptering. Använd den **återskapa** knappen om du skulle behöva återskapa den nya åtkomstnyckeln, kan du och det påverkar inte någon tidigare distribuerad sensorer, eftersom den används endast för registreringen av sensorn.
4.  Kopiera paketet till den dedikerade servern eller domänkontrollanten där du installerar Azure ATP-sensorn. Alternativt kan du öppna Azure ATP-arbetsyteportalen från den dedikerade servern eller domänkontrollanten och hoppa över detta steg.

Zip-filen innehåller följande filer:

-   Installationsprogram för Azure ATP-sensorn

-   Konfigurationsfilen med informationen som krävs för att ansluta till Molntjänsten Azure ATP


> [!div class="step-by-step"]
> [« Steg 2](install-atp-step2.md)
> [Steg 4 »](install-atp-step4.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Krav för Azure ATP](atp-prerequisites.md)

- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)