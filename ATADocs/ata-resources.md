---
title: Advanced Threat Analytics resurser och beredskap roadamp | Microsoft Docs
description: "Visar en lista över ATA resurser, videor, komma igång, distribution och beredskap översikt över länkar."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/15/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 33aec9dd89fc189144387e59c3b48b9d440936d2
ms.sourcegitcommit: 55f7ac32bcd4ac8edb8b8b3b47993bf96b9acce2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/15/2018
---
*Gäller för: Advanced Threat Analytics version 1.8*

# <a name="ata-readiness-roadmap"></a>Översikt över ATA-beredskap 
Det här dokumentet innehåller en översikt över beredskap som hjälper dig att komma igång med Advanced Threat Analytics.

## <a name="understanding-ata"></a>Förstå ATA

Advanced Threat Analytics (ATA) är en lokal plattform som skyddar ditt företag från flera typer av avancerade riktade cyberattacker och insiderhot. Använd följande resurser om du vill veta mer om ATA:

- [ATA-översikt](https://aka.ms/ATAOverview)

- [ATA introduktion video - kort](https://aka.ms/ATAShort)

- [ATA inledande video – fullständig](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Distributionsbeslut

ATA består av ATA Center, som du kan installera på en server och ATA-gatewayer som du kan installera på separata datorer eller med hjälp av Lightweight Gateway direkt på domänkontrollanterna. Innan du komma igång, är det viktigt att fatta följande distributionsbeslut:

|KONFIGURATION|BESLUT|
|----|----|
|Maskinvarutyp|Fysiska, virtuella, Azure VM|
|Arbetsgrupp eller domän|Arbetsgrupp, domän|
|Storlek för gateway|Fullständig Gateway, Lightweight Gateway|
|Certifikat|PKI, självsignerade|

Om du använder fysiska servrar bör du planera kapaciteten. Du kan få hjälp att tilldela utrymme för ATA-storleksverktyget:

[ATA-storleksverktyget](http://aka.ms/atasizing) -storleksverktyget automatiserar samling mängden trafik måste ATA. Tillhandahåller det automatiskt support och resursen rekommendationer för både ATA Center och ATA Lightweight-gatewayer.

[ATA-kapacitetsplanering](https://docs.microsoft.com/en-us/advanced-threat-analytics/ata-capacity-planning)

## <a name="deploy-ata"></a>Distribuera ATA

Dessa resurser hjälper dig att hämta och installera ATA Center, ansluta till Active Directory, hämta ATA Gateway-paketet, konfigurera händelseinsamling och om du vill integrera med din VPN och konfigurera honeytoken konton och undantag.

[Hämta ATA](http://aka.ms/ataeval) -innan du distribuerar ATA, om du inte har bestämt dig för att köpa ATA måste du hämta utvärderingsversionen. 

[ATA POC playbook](http://aka.ms/atapoc) -Guide för att alla steg som krävs för att göra ett POC distributionen av ATA.

[ATA-distributionen video](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) – det här videoklippet ger en översikt över ATA-distributionen steg på mindre än 10 minuter.

## <a name="ata-settings"></a>Inställningar för ATA

Grundläggande nödvändiga inställningar i ATA konfigureras som en del av installationsguiden. Det finns ett antal andra inställningar som du kan konfigurera för att finjustera ATA identifieringar exaktare för din miljö, till exempel SIEM-integrering och granska inställningar.

[Granska inställningar](https://aka.ms/ataauditingblog) – granska din hälsa före och efter en ATA-distribution.

[ATA allmän dokumentation](https://docs.microsoft.com/en-us/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Arbeta med ATA

När ATA är igång, kommer du att kunna visa misstänkta aktiviteter som identifieras i tidslinjen för attacker. Det här är den standardsida du kommer till när du loggar in på ATA-konsolen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet. Granska varje misstänkt aktivitet genom att gå nedåt i entiteter (datorer, enheter, användare) för att öppna profilsidorna som innehåller mer information. Dessa resurser hjälper dig att arbeta med ATA: s misstänkta aktiviteter:

[ATA misstänkt aktivitet playbook](http://aka.ms/ataplaybook) -den här artikeln vägleder dig genom autentiseringsuppgifter attack tekniker för stöld av tillgängliga research verktygen på Internet. Vid varje angrepp, kan du se hur ATA hjälper dig att få insyn i dessa hot.

[Guide för ATA-misstänkt aktivitet](http://aka.ms/atasaguide)



## <a name="security-best-practices"></a>Metodtips för säkerhet

[Metodtips för ATA](https://aka.ms/atasecbestpractices) -Metodtips för att skydda ATA.

[Vanliga frågor om ATA](http://aka.ms/atafaq) -den här artikeln innehåller en lista med vanliga frågor och svar om ATA och ger insikt och svar.

## <a name="additional-resources"></a>Ytterligare resurser

[Microsoft Security Channel 9 sida](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Gruppresurser

[ATA-bloggen](https://aka.ms/ATABlog)
[ATA community](https://aka.ms/ATACommunity)
[ge feedback om ATA](https://aka.ms/ATAUserVoice)
