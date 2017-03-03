---
title: "Advanced Threat Analytics-rollgrupper för åtkomsthantering | Microsoft Docs"
description: "Vägleder dig i att arbeta med ATA-rollgrupper."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 88ca89f2311bf4e73b3d0b57db3e4377e99fd8b2
ms.openlocfilehash: 7919c9658f2e05b448e3a773bd5ab4c6cb96625f


---

*Gäller för: Advanced Threat Analytics version 1.7*




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
|Lägg till/redigera information för misstänkta aktiviteter|Tillgänglig|Tillgänglig|Saknas|
|Ändra status för Övervaka aviseringar|Tillgänglig|Tillgänglig|Saknas|
|Uppdatera ATA-konfiguration|Tillgänglig|Saknas|Saknas|
|Gateway – lägg till|Tillgänglig|Saknas|Saknas|
|Gateway – ta bort |Tillgänglig|Saknas|Saknas|
|Övervakad DC – lägg till |Tillgänglig|Saknas|Saknas|
|Övervakad DC – ta bort|Tillgänglig|Saknas|Saknas|

När användare försöker komma åt en sida som inte är tillgänglig för deras rollgrupp, kommer de att omdirigeras till sidan ATA-obehörig. 

## <a name="add--remove-users---ata-role-groups"></a>Lägg till\ta bort användare – ATA-rollgrupper 

ATA använder lokala Windows-grupper som bas för rollgrupper. Om du vill lägga till eller ta bort användare, använd **Lokala användare och grupper** MMC (Lusrmgr.msc). Du kan lägga till domänkonton som lokala konton på en domänansluten dator. 




<!--HONumber=Feb17_HO1-->


