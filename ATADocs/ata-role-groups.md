---
title: "Advanced Threat Analytics-rollgrupper för åtkomsthantering | Microsoft Docs"
description: "Vägleder dig i att arbeta med ATA-rollgrupper."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/16/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1f531db341f442d135b802af965f714b37f69e3a
ms.sourcegitcommit: 3cd268cf353ff8bc3d0b8f9a8c10a34353d1fcf1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/16/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*




# <a name="ata-role-groups"></a>ATA-rollgrupper

Rollgrupper möjliggör åtkomsthantering för ATA. Genom att använda rollgrupper kan du särskilja uppgifter inom din säkerhetsgrupp och endast ge den mängd åtkomst som användare behöver att utföra sitt arbete. Den här artikeln förklarar åtkomsthantering och ATA-rollauktorisering, och hjälper dig att komma igång med rollgrupper i ATA.

> [!NOTE]
> En lokal administratör i ATA Center blir automatiskt en Microsoft Advanced Threat Analytics-administratör.

## <a name="types-of-ata-role-groups"></a>Typer av ATA-rollgrupper 

ATA introducerar 3 typer av rollgrupper: ATA-administratörer, ATA-användare och ATA-visningsprogram. Följande tabell beskriver vilken typ av åtkomst som är tillgänglig i ATA per roll. Beroende på vilken roll du tilldelar, kommer olika skärmar och menyalternativ i ATA inte att vara tillgängliga, enligt följande:

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


När användare försöker komma åt en sida som inte är tillgänglig för deras rollgrupp, kommer de att omdirigeras till sidan ATA-obehörig. 

## <a name="add--remove-users---ata-role-groups"></a>Lägg till\ta bort användare – ATA-rollgrupper 

ATA använder lokala Windows-grupper som bas för rollgrupper. Rollgrupperna måste hanteras på ATA Center-servern.
Om du vill lägga till eller ta bort användare, använd **Lokala användare och grupper** MMC (Lusrmgr.msc). Du kan lägga till domänkonton som lokala konton på en domänansluten dator. 

