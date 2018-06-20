---
title: Installera Azure Advanced Threat Protection - steg 2 | Microsoft Docs
description: Steg två i installerar Azure ATP hjälper dig att konfigurera domänanslutningsinställningarna på Molntjänsten Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 11f9d5bf69ffda0843a94c7a2bb31869dc980dce
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446493"
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-2"></a>Installera Azure ATP - steg 2

>[!div class="step-by-step"]
[« Steg 1](install-atp-step1.md)
[Steg 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Steg 2. Ange ett användarnamn och lösenord för att ansluta till Active Directory-skog

Första gången du öppnar arbetsytan-portalen Azure ATP visas följande skärm:

![Azure ATP Välkommen fas 1](media/directory-services.png)

> [!IMPORTANT]
> Användarens autentiseringsuppgifter här måste vara för ett användarkonto i Active Directory lokalt. 


1.  Ange följande information och klicka på **Spara**:

    |Fält|Kommentar|
    |---------|------------|
    |**Användarnamn** (krävs)|Ange skrivskyddad Active Directory användarnamnet, till exempel: **ATPuser**.|
    |**Lösenord** (krävs)|Ange lösenordet för den skrivskyddade användaren, till exempel: **Penna1**.|
    |**Domän** (krävs)|Ange domänen för den skrivskyddade användaren, till exempel: **contoso.com**. **Obs:** Det är viktigt att du anger det fullständiga FQDN för domänen där användaren finns. Om användarens konto exempelvis finns i domänen corp.contoso.com måste du ange `corp.contoso.com`, inte contoso.com|

3. I arbetsytan-portalen klickar du på **hämtar sensor installationsprogrammet och installerar den första sensorn** att fortsätta.


>[!div class="step-by-step"]
[« Steg 1](install-atp-step1.md)
[Steg 3 »](install-atp-step3.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)