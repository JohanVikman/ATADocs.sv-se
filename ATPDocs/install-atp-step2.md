---
title: Installera Azure Advanced Threat Protection – steg 2 | Microsoft Docs
description: Steg två för att installera Azure ATP hjälper dig att konfigurera domänanslutningsinställningarna på din Azure ATP-molntjänst
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 45c1ddfc80c481549ceb08ed45f535ca029b9626
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453841"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-2"></a>Installera Azure ATP - steg 2

> [!div class="step-by-step"]
> [« Steg 1](install-atp-step1.md)
> [Steg 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Steg 2. Ange ett användarnamn och lösenord för att ansluta till Active Directory-skogen

Första gången du öppnar Azure ATP-arbetsyteportalen, visas följande skärmbild:

![Azure ATP-Välkommen, steg 1](media/directory-services.png)

> [!IMPORTANT]
> Användarens autentiseringsuppgifter här måste vara för ett användarkonto i den lokala Active Directory. 


1.  Ange följande information och klicka på **Spara**:

    |Fält|Kommentar|
    |---------|------------|
    |**Användarnamn** (krävs)|Ange det skrivskyddade Active Directory användarnamnet, till exempel: **ATPuser**.|
    |**Lösenord** (krävs)|Ange lösenordet för den skrivskyddade användaren, till exempel: **Penna1**.|
    |**Domän** (krävs)|Ange domänen för den skrivskyddade användaren, till exempel: **contoso.com**. **Obs:** Det är viktigt att du anger det fullständiga FQDN för domänen där användaren finns. Om användarens konto exempelvis finns i domänen corp.contoso.com måste du ange `corp.contoso.com`, inte contoso.com|

3. I arbetsyteportalen klickar du på **hämta sensorkonfiguration och installera den första sensorn** att fortsätta.


> [!div class="step-by-step"]
> [« Steg 1](install-atp-step1.md)
> [Steg 3 »](install-atp-step3.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)