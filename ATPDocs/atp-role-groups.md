---
title: Azure Avancerat skydd-rollgrupper för åtkomsthantering | Microsoft Docs
description: Beskriver hur du arbetar med Azure ATP-rollgrupper.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e7af3846d31031b645c65c7550b696fe4738e5d
ms.sourcegitcommit: a9b8bc26d3cb5645f21a68dc192b4acef8f54895
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/16/2018
ms.locfileid: "39064074"
---
*Gäller för: Azure Avancerat skydd*




# <a name="azure-atp-role-groups"></a>Azure ATP-rollgrupper

Azure ATP ger rollbaserad säkerhet för att skydda data i enlighet med organisationens säkerhets- och behov. Azure ATP stöder tre separata roller: administratörer, användare och användare. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Rollgrupper aktivera åtkomsthantering för Azure ATP. Genom att använda rollgrupper kan du särskilja uppgifter inom din säkerhetsgrupp och endast ge den mängd åtkomst som användare behöver att utföra sitt arbete. Den här artikeln förklarar åtkomsthantering och Azure ATP-rollbehörighet och hjälper dig att komma igång med rollgrupper i ATP.

> [!NOTE]
> Alla global administratör eller säkerhetsadministratör på klientens Azure Active Directory blir automatiskt en Azure ATP-administratör.

## <a name="accessing-the-workspace-management-portal"></a>Åtkomst till arbetsytehanteringsportalen

Åtkomst till arbetsytehanteringsportalen (portal.atp.azure.com) kan endast utföras av en Azure AD-användare som har katalogrollen global administratör eller säkerhetsadministratör. När du har angett på portalen kan du skapa olika arbetsytor. För varje arbetsyta Azure ATP-tjänsten skapar tre säkerhetsgrupper i Azure Active Directory-klient: administratörer, användare, visningsprogram. 

> [!NOTE]
> Åtkomst till Azure ATP-arbetsyteportalen ges endast till användare i Azure AD-säkerhetsgrupper för den arbetsytan och globala administratörer och säkerhetsadministratörer.


## <a name="types-of-azure-atp-security-groups"></a>Typer av Azure ATP-säkerhetsgrupper 

Azure ATP introducerar tre typer av säkerhetsgrupp: Azure ATP *Arbetsytenamn* administratörer, Azure ATP *Arbetsytenamn* användare och Azure ATP *Arbetsytenamn* visningsprogram . I följande tabell beskrivs vilken typ av åtkomst i den Azure ATP-arbetsyteportalen tillgängliga per roll. Beroende på vilken roll som du tilldelar, olika skärmar och menyalternativ i Azure ATP-arbetsyteportalen är inte tillgängliga, enligt följande:

|Aktivitet |Azure ATP *Arbetsytenamn* administratörer|Azure ATP *Arbetsytenamn* användare|Azure ATP *Arbetsytenamn* visningsprogram|
|----|----|----|----|
|Inloggning|Tillgänglig|Tillgänglig|Tillgänglig|
|Ändra status för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Dela/exportera misstänkt aktivitet via e-post/get-länk|Tillgänglig|Tillgänglig|Tillgänglig|
|Ändra status för Övervaka aviseringar|Tillgänglig|Saknas|Saknas|
|Uppdatera Azure ATP-konfigurationen|Tillgänglig|Saknas|Saknas|
|sensorn – Lägg till|Tillgänglig|Saknas|Saknas|
|sensorn – ta bort |Tillgänglig|Saknas|Saknas|
|Övervakad DC – lägg till |Tillgänglig|Saknas|Saknas|
|Övervakad DC – ta bort|Tillgänglig|Saknas|Saknas|
|Visa aviseringar och misstänkta aktiviteter|Tillgänglig|Tillgänglig|Tillgänglig|


När användare försöker komma åt en sida som inte är tillgänglig för deras rollgrupp, omdirigeras till sidan Azure ATP obehörig. 

## <a name="add-and-remove-users"></a>Lägga till och ta bort användare 


Azure ATP använder Azure AD-säkerhetsgrupper som bas för rollgrupper. Rollgrupperna kan hanteras från [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups ](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Endast Azure AD-användare kan läggs till eller tas bort från säkerhetsgrupper. 

## <a name="see-also"></a>Se även
- [ATA-storleksverktyget](http://aka.ms/aatpsizingtool)
- [ATA-arkitektur](atp-architecture.md)
- [Installera ATA](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)

