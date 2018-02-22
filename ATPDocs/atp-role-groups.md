---
title: "Azure Advanced Threat Protection rollgrupper för access management | Microsoft Docs"
description: "Vägleder dig genom att arbeta med Azure ATP rollgrupper."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86cb55fd2b5ce81460dead4b8b753c88f79edd7b
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure ATP rollgrupper

Rollgrupper kan åtkomsthantering för Azure ATP. Genom att använda rollgrupper kan du särskilja uppgifter inom din säkerhetsgrupp och endast ge den mängd åtkomst som användare behöver att utföra sitt arbete. Den här artikeln förklarar åtkomsthantering och Azure ATP auktorisering av roller och hjälper du komma igång med rollgrupper i ATP.

> [!NOTE]
> Alla globala administratörer eller säkerhetsadministratör på klientens Azure Active Directory är automatiskt en Azure ATP-administratör.

## <a name="accessing-the-workspace-management-portal"></a>Åtkomst till arbetsytan management portal

Åtkomst till hanteringsportalen arbetsytan (portal.atp.azure.com) kan bara utföras av en Azure AD-användare som har directory rollen som global administratör eller säkerhetsadministratör. När du har angett portalen kan du skapa olika arbetsytorna. För varje arbetsyta tjänsten Azure ATP skapas tre säkerhetsgrupper i Azure Active Directory-klient: administratörer, användare, visningsprogram. 

> [!NOTE]
> Åtkomst till Azure ATP arbetsytan portal beviljas endast till användare i Azure AD-säkerhetsgrupper för den arbetsytan och globala administratörer och säkerhetsadministratörerna.


## <a name="types-of-azure-atp-security-groups"></a>Typer av Azure ATP säkerhetsgrupper 

Azure ATP introducerar tre typer av säkerhetsgrupp: Azure ATP *Arbetsytenamn* administratörer, Azure ATP *Arbetsytenamn* användare och Azure ATP *Arbetsytenamn* visningsprogram . I följande tabell beskrivs typ av åtkomst i Azure ATP arbetsytan portal tillgängliga per roll. Beroende på vilken roll som du tilldelar, olika skärmar och menyalternativen i Azure ATP arbetsytan portalen är inte tillgängliga, enligt följande:

|Aktivitet |Azure ATP *Arbetsytenamn* administratörer|Azure ATP *Arbetsytenamn* användare|Azure ATP *Arbetsytenamn* visningsprogram|
|----|----|----|----|
|Inloggning|Tillgänglig|Tillgänglig|Tillgänglig|
|Ange kommentarer angående misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Dela/exportera misstänkt aktivitet via e-post/get-länk|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för Övervaka aviseringar|Tillgänglig|Tillgänglig|Saknas|
|Uppdatera konfigurationen av Azure ATP|Tillgänglig|Saknas|Saknas|
|temperatursensor – Lägg till|Tillgänglig|Saknas|Saknas|
|temperatursensor – ta bort |Tillgänglig|Saknas|Saknas|
|Övervakad DC – lägg till |Tillgänglig|Saknas|Saknas|
|Övervakad DC – ta bort|Tillgänglig|Saknas|Saknas|
|Visa aviseringar och misstänkta aktiviteter|Tillgänglig|Tillgänglig|Tillgänglig|


När användare försöker komma åt en sida som inte är tillgänglig för sin roll-grupp måste omdirigeras till sidan Azure ATP obehörig. 

## <a name="add-and-remove-users"></a>Lägga till och ta bort användare 

Azure ATP använder Azure AD-säkerhetsgrupper som bas för rollgrupper. Rollgrupper kan hanteras från [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All grupper](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  AAD-användare kan läggas till eller tas bort från säkerhetsgrupper. 


## <a name="see-also"></a>Se även
- [ATA-storleksverktyget](http://aka.ms/aatpsizingtool)
- [ATA-arkitektur](atp-architecture.md)
- [Installera ATA](install-atp-step1.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)

