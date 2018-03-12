---
title: "Vad är nytt i Azure ATP | Microsoft Docs"
description: "Beskriver de senaste versionerna av Azure ATP och innehåller information om vad är nytt i varje version."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4a81d84a46b9710c2376bbc50f699966a24138db
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/12/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Vad är nytt i Azure ATP 

## <a name="azure-atp-release-224"></a>Azure ATP versionen 2.24

Publicerat 11 mars 2018

**Nya och uppdaterade identifieringar**
  - Skapa en misstänkt tjänst – angripare försöka köra misstänkta tjänster i nätverket. Azure ATP skapar nu en avisering när den identifierar att någon på en specifik dator kör en ny tjänst som verkar misstänkt. Denna identifiering baserat på händelser (inte nätverkstrafik) och upptäcks på någon domänkontrollant i nätverket som vidarebefordrar händelse 7045 till Azure ATP. Mer information finns i [misstänkt aktivitet guiden](suspicious-activity-guide.md).

**Förbättrad undersökning**
  - Azure ATP innehåller en utökade [entitetsprofilen](entity-profiles.md). Entitetsprofilen ger en plattform som är avsedd för djupdykning undersökning av användaraktiviteter detta inkluderar resurser de använde, datorer som de har loggat in på och mycket mer. Entitetsprofilen också innehåller katalogdata och ger dig möjlighet att identifiera potentiella lateral förflyttning sökvägar till eller från enheten, så att du vill veta mer om potentiella överträdelser i din organisation.

  - ATP gör att du kan manuellt taggen entiteter som *känsliga* att förbättra identifieringar och övervakning. Den här taggning påverkar många Azure ATP identifieringar som känsliga grupp ändring identifiering och [lateral förflyttning sökvägen](use-case-lateral-movement-path.md), som förlitar sig på enheter som anses vara känslig.

**Nya rapporter som hjälper dig att undersöka**
  - Den [lösenord exponeras i klartext rapporten](reports.md) kan du identifiera när tjänster skickar autentiseringsuppgifter skickas i klartext. På så sätt kan du undersöka tjänster och förbättra din nivå för nätverkssäkerhet. Den här rapporten ersätter klartext misstänkt Aktivitetsaviseringar.
  - Den [Lateral förflyttning sökvägar till rapporten känsliga konton](reports.md) visar känsliga konton som exponeras via lateral förflyttning sökvägar. På så sätt kan du minimera dessa sökvägar och skydda ditt nätverk för att minimera ytan risken för angrepp. Detta gör att du kan förhindra lateral förflyttning så att angripare inte kan flytta över nätverket mellan användare och datorer tills de har nått högsta vinsten virtuella säkerhet: dina känsliga admin-autentiseringsuppgifter.

- Du kan nu lätt ge åtkomst i dokumentationen från en länk i en avisering om misstänkt aktivitet för att kunna visa [undersökningen steg som du kan vidta](suspicious-activity-guide.md). 

**Prestandaförbättringar**
 -  Azure ATP sensor infrastruktur har förbättrats för prestanda: aggregerade för att visa trafiken gör det möjligt för optimering av processor- och paket pipeline och återanvänder sockets till domänkontrollanter för att minimera SSL-sessioner till domänkontrollanten.

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)