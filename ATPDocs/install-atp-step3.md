---
title: Installera Azure Advanced Threat Protection - steg 3 | Microsoft Docs
description: Steg tre av Azure ATP-installationen kan du hämta installationspaketet för Azure ATP fristående sensor.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: aa07d6ce4418c051362652e70968a8e41313affb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446045"
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-3"></a>Installera Azure ATP - steg 3

>[!div class="step-by-step"]
[« Steg 2](install-atp-step2.md)
[Steg 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Steg 3. Hämta installationspaketet för Azure ATP-temperatursensor
Du kan hämta installationspaketet för Azure ATP sensor när du har konfigurerat anslutningsinställningarna för domänen. Installationspaketet för Azure ATP sensor kan installeras på en dedikerad server eller på en domänkontrollant. När du installerar direkt på en domänkontrollant, installeras som en Azure ATP-sensor när du installerar på en dedikerad server och använder portspegling, installeras som Azure ATP fristående sensor. Mer information om Azure ATP-sensor finns [Azure ATP arkitektur](atp-architecture.md). 

Klicka på **hämta** i listan över steg längst upp på sidan för att gå till den **Sensor** sidan.

![Konfigurationsinställningar för Azure ATP-temperatursensor](media/atp-sensor-config.png)

> [!NOTE] 
> Om du vill nå skärm för konfiguration av sensor senare klickar du på den **inställningsikonen** (övre högra hörnet) och välj **Configuration**, sedan under **System**, klickar du på **sensor**.  

1.  Klicka på **sensor**.
2.  Spara paketet lokalt.
3.  Kopiera den **åtkomstnyckeln**. Snabbtangent krävs för Azure ATP sensor att ansluta till din Azure ATP-arbetsyta. Snabbtangent är en en-engångslösenord för sensor distributionen, efter vilken utförs all kommunikation med certifikat för autentisering och TLS-kryptering. Använd den **återskapa** knappen om du behöver återskapa åtkomstnyckeln, kan du och eventuella tidigare distribuerade sensorer, påverkas inte eftersom den används endast för registreringen av sensorn.
4.  Kopiera paketet till den dedikerade servern eller domänkontrollanten där du installerar Azure ATP sensorn. Alternativt kan du öppna Azure ATP arbetsytan portalen från den dedikerade servern eller domänkontrollanten och hoppa över detta steg.

Zip-filen innehåller följande filer:

-   Installationsprogram för Azure ATP-temperatursensor

-   Filen med informationen som krävs för att ansluta till Molntjänsten Azure ATP konfigurationsinställningar


>[!div class="step-by-step"]
[« Steg 2](install-atp-step2.md)
[Steg 4 »](install-atp-step4.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Krav för Azure ATP](atp-prerequisites.md)

- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)