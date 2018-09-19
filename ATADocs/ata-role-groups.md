---
title: Advanced Threat Analytics-rollgrupper för åtkomsthantering | Microsoft Docs
description: Vägleder dig i att arbeta med ATA-rollgrupper.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ed4d112cda614053aa20a6a486cb29baa1fed58a
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133641"
---
*Gäller för: Advanced Threat Analytics version 1.9*




# <a name="ata-role-groups"></a>ATA-rollgrupper

Rollgrupper aktivera åtkomsthantering för ATA. Genom att använda rollgrupper kan du särskilja uppgifter inom din säkerhetsgrupp och endast ge den mängd åtkomst som användare behöver att utföra sitt arbete. Den här artikeln förklarar åtkomsthantering och ATA-rollauktorisering, och hjälper dig att komma igång med rollgrupper i ATA.

> [!NOTE]
> En lokal administratör i ATA Center blir automatiskt en Microsoft Advanced Threat Analytics-administratör.

## <a name="types-of-ata-role-groups"></a>Typer av ATA-rollgrupper 

ATA introducerar tre typer av rollgrupper: ATA-administratörer, ATA-användare och ATA-visningsprogram. Följande tabell beskriver vilken typ av åtkomst som är tillgänglig i ATA per roll. Beroende på vilken roll du tilldela olika skärmar och menyn Alternativ i ATA finns inte, enligt följande:

|Aktivitet |Administratörer för Microsoft Advanced Threat Analytics|Användare av Microsoft Advanced Threat Analytics|Visningsprogram för Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Inloggning|Tillgänglig|Tillgänglig|Tillgänglig|
|Ange kommentarer angående misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Dela/exportera misstänkt aktivitet via e-post/get-länk|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för Övervaka aviseringar|Tillgänglig|Tillgänglig|Saknas|
|Uppdatera ATA-konfiguration|Tillgänglig|Saknas|Saknas|
|Gateway – lägg till|Tillgänglig|Saknas|Saknas|
|Gateway – ta bort |Tillgänglig|Saknas|Saknas|
|Övervakad DC – lägg till |Tillgänglig|Saknas|Saknas|
|Övervakad DC – ta bort|Tillgänglig|Saknas|Saknas|
|Visa aviseringar och misstänkta aktiviteter|Tillgänglig|Tillgänglig|Tillgänglig|


När användare försöker komma åt en sida som inte är tillgänglig för deras rollgrupp, omdirigeras till sidan ATA obehörig. 

## <a name="add--remove-users---ata-role-groups"></a>Lägg till\ta bort användare – ATA-rollgrupper 

ATA använder lokala Windows-grupper som bas för rollgrupper. Rollgrupperna måste hanteras på ATA Center-servern.
Om du vill lägga till eller ta bort användare, använd **Lokala användare och grupper** MMC (Lusrmgr.msc). Du kan lägga till domänkonton som lokala konton på en domänansluten dator. 

