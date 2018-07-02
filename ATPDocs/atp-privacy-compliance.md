---
title: Azure Avancerat skydd av personuppgifter-principen | Microsoft Docs
description: Innehåller länkar till information om hur du tar bort privat information och personliga data från Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: d64cc0d40acc31e2187305c38a625924a91db06b
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2018
ms.locfileid: "36948939"
---
*Gäller för: Azure Avancerat skydd*

# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP-datasäkerhet och sekretess

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Sök efter och identifiera personliga data 

I Azure Advanced Threat Protection kan du visa identifierbar personliga data från den [arbetsyteportalen](workspace-portal.md) med hjälp av den [sökfältet](workspace-portal.md#search-bar). 

Du kan söka efter en viss användare eller dator och klicka på entiteten kommer du till användaren eller datorn [profilsida](entity-profiles.md). Profilen innehåller omfattande information från Active Directory, inklusive nätverksaktivitet som är relaterade till entiteten och dess historik.

Azure ATP-personuppgifter samlas in från Active Directory via Azure ATP-sensorn och lagras i en backend-databas.

## <a name="update-personal-data"></a>Uppdatera personliga data 

Eftersom Azure ATP användarens personliga data hämtas från användarobjektet i Active Directory för organisationen, visas alla ändringar i användarprofilen i AD i Azure ATP.


## <a name="delete-personal-data"></a>Ta bort personliga data 

När en användare har tagits bort från organisationens Active Directory, Azure ATP tar automatiskt bort användarprofilen och alla relaterade nätverksaktivitet inom ett år. Du kan också [ta bort](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) alla säkerhetsaviseringar som innehåller personliga data. 

## <a name="export-personal-data"></a>Exportera personliga data 

I Azure ATP har du möjlighet att [exportera](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) security aviseringsinformation till Excel. Detta kommer också att exportera personliga data. 
 
## <a name="audit-personal-data"></a>Granska personliga data

Azure ATP implementerar granskning av personliga data ändras, inklusive den tas bort och export av personuppgifter. Kvarhållningstid för granskning spårning är 90 dagar. Granskning i Azure ATP är en funktion i backend-server eller inte tillgänglig för kunder.
 
## <a name="additional-resources"></a>Ytterligare resurser

- Läs om hur Azure ATP-förtroende och efterlevnad i [Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) och [Dataskyddsförordningen för Microsoft 365 Enterprise plats](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
