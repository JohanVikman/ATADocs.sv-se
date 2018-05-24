---
title: Azure Advanced Threat Protection personuppgifter princip | Microsoft Docs
description: Innehåller länkar till information om hur du tar bort personlig information och dina personliga data från Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: d6bf11d55743b7422985577f512f16af93159618
ms.sourcegitcommit: 571297209b15e9dc4d43c5e57da359973da8d207
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/23/2018
---
*Gäller för: Azure Advanced Threat Protection*

# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP datasäkerhet och sekretess

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Söka efter och identifiera personliga data 

I Azure Advanced Threat Protection kan du visa identifierbar personlig information från den [arbetsytan portal](workspace-portal.md) med hjälp av den [sökfältet](workspace-portal.md#search-bar). 

Du kan söka efter en viss användare eller dator och klicka på entiteten leder till användaren eller datorn [profilsida](entity-profiles.md). Profilen som innehåller omfattande information om entiteten från Active Directory, inklusive nätverksaktivitet som rör den enheten och dess historik.

Azure ATP personuppgifter samlas in från Active Directory via Azure ATP-sensor och lagras i en backend-databas.

## <a name="update-personal-data"></a>Uppdatera personliga data 

Eftersom Azure ATP användarens personliga data hämtas från användarobjektet i Active Directory för organisationen, visas alla ändringar i användarprofilen i AD i Azure ATP.


## <a name="delete-personal-data"></a>Ta bort personliga data 

När en användare har tagits bort från organisationens Active Directory, Azure ATP tas automatiskt bort användarprofilen och eventuella relaterade nätverksaktivitet inom ett år. Du kan också [ta bort](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) några säkerhetsaviseringar som innehåller personuppgifter. 

## <a name="export-personal-data"></a>Exportera personliga data 

I Azure ATP har du möjlighet att [export]((working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) avisering säkerhetsinformation till Excel. Detta kan också exportera personliga data. 
 
## <a name="audit-personal-data"></a>Gransknings-och personliga data

Azure ATP implementerar granskning av ändringar av personliga data, inklusive den tas bort och export av personuppgifter poster. Granska spår kvarhållningstiden är 90 dagar. Granskning i Azure ATP är en backend-funktion och inte tillgängliga för kunder.
 
## <a name="additional-resources"></a>Ytterligare resurser

- Information om Azure ATP förtroende och kompatibilitet finns i [Service förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) och [webbplatsen Microsoft 365 Enterprise BNPR efterföljande](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
