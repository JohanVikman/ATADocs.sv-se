---
title: "Arbeta med rollgrupper – Slutföra | Microsoft ATA"
description: "Vägleder dig i att arbeta med ATA-rollgrupper."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*Gäller för: Advanced Threat Analytics version 1.7*




# ATA-rollgrupper

Rollgrupper möjliggör åtkomsthantering för ATA. Genom att använda rollgrupper kan du särskilja uppgifter inom din säkerhetsgrupp och endast ge den mängd åtkomst som användare behöver att utföra sitt arbete. Den här artikeln förklarar åtkomsthantering och ATA-rollauktorisering, och hjälper dig att komma igång med rollgrupper i ATA.
## Typer av ATA-rollgrupper 

ATA introducerar tre typer av rollgrupper: ATA-administratör, ATA-analytiker och ATA-ansvarig. Följande tabell beskriver vilken typ av åtkomst som är tillgänglig i ATA per roll. Beroende på vilken roll du tilldelar, kommer olika skärmar och menyalternativ i ATA inte att vara tillgängliga, enligt följande:

|Aktivitet |Administratör för Microsoft Advanced Threat Analytics|Analytiker för Microsoft Advanced Threat Analytics|Ansvarig för Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Inloggning|Tillgänglig|Tillgänglig|Tillgänglig|
|Ange kommentarer angående misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Dela/exportera misstänkt aktivitet via e-post/get-länk|Tillgänglig|Tillgänglig|Saknas|
|Lägg till/redigera information för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för Övervaka aviseringar|Tillgänglig|Tillgänglig|Saknas|
|Uppdatera ATA-konfiguration|Tillgänglig|Saknas|Saknas|
|Gateway – lägg till|Tillgänglig|Saknas|Saknas|
|Gateway – ta bort |Tillgänglig|Saknas|Saknas|
|Övervakad DC – lägg till |Tillgänglig|Saknas|Saknas|
|Övervakad DC – ta bort|Tillgänglig|Saknas|Saknas|

När användare försöker komma åt en sida som inte är tillgänglig för deras rollgrupp, kommer de att omdirigeras till sidan ATA-obehörig. 

## Lägg till\ta bort användare – ATA-rollgrupper 

ATA använder lokala Windows-grupper som bas för rollgrupper. Om du vill lägga till eller ta bort användare, använd **Lokala användare och grupper** MMC (Lusrmgr.msc). Du kan lägga till domänkonton som lokala konton på en domänansluten dator. 




<!--HONumber=Sep16_HO4-->


