---
title: Advanced Threat Analytics-resurser och beredskap roadamp | Microsoft Docs
description: Innehåller en lista över ATA-resurser, videor, komma igång, distribution och beredskap översikten länkar.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 48756cbde8b288116975c05567beeac76e83a717
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133777"
---
*Gäller för: Advanced Threat Analytics version 1.9*

# <a name="ata-readiness-roadmap"></a>Översikt över ATA-beredskap 
Det här dokumentet innehåller en beredskapsöversikt som hjälper dig att komma igång med Advanced Threat Analytics.

## <a name="understanding-ata"></a>Så här fungerar ATA

Advanced Threat Analytics (ATA) är en lokal plattform som skyddar ditt företag från flera typer av avancerade riktade cyberattacker och insiderhot. Använd följande resurser för mer information om ATA:

- [ATA-översikt](what-is-ata.md)

- [ATA introduktionsvideo - kort](https://aka.ms/ATAShort)

- [Introduktionsvideo om ATA - fullständig](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Distributionsbeslut

ATA består av ATA Center, som du kan installera på en server och ATA-gatewayer som du kan installera på separata datorer eller genom att använda Lightweight Gateway direkt på domänkontrollanterna. Innan du kommer igång, är det viktigt att fatta följande distribution:

|KONFIGURATION|BESLUT|
|----|----|
|Maskinvarutyp|Fysiska, virtuella Azure-VM|
|Arbetsgrupp eller domän|Arbetsgrupp, domän|
|Storlek för gateway|Fullständig Gateway, Lightweight Gateway|
|Certifikat|PKI, självsignerade|

Om du använder fysiska servrar, bör du planera kapacitet. Du kan få hjälp att tilldela utrymme för ATA-storleksverktyget:

[ATA-storleksverktyget](ata-capacity-planning.md) -storleksverktyget automatiserar samling mängden trafik som ATA behöver. Den tillhandahåller automatiskt support och resurs rekommendationer för både ATA Center och ATA Lightweight-gatewayer.

[ATA-kapacitetsplanering](ata-capacity-planning.md)

## <a name="deploy-ata"></a>Distribuera ATA

Dessa resurser kan du ladda ned och installera ATA Center, ansluta till Active Directory, ladda ned ATA Gateway-paketet, konfigurera händelseinsamling och du kan också integrera med din VPN och konfigurera honeytoken-konton och undantag.

[Hämta ATA](http://aka.ms/ataeval) -innan du distribuerar ATA om du inte har bestämt dig för att köpa ATA måste du hämta utvärderingsversionen. 

[ATA POC-strategibok](http://aka.ms/atapoc) -guide om hur du alla steg som krävs för att göra en POC-distributionen av ATA.

[ATA-distributionen video](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) – den här videon ger en översikt över ATA-distribution steg i mindre än 10 minuter.

## <a name="ata-settings"></a>ATA-inställningar

De grundläggande nödvändiga inställningarna i ATA konfigureras som en del av installationsguiden. Men finns det ett antal andra inställningar som du kan konfigurera för att finjustera ATA gör identifieringar exaktare för din miljö, till exempel SIEM-integrering och granska inställningar.

[Granska inställningar](https://aka.ms/ataauditingblog) – granska din domain controller hälsotillstånd före och efter en ATA-distribution.

[ATA allmän dokumentation](https://docs.microsoft.com/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Arbeta med ATA

När ATA är igång, kommer du att kunna se misstänkta aktiviteter som identifieras i attacktidslinjen. Det här är den standardsida du kommer till när du loggar in på ATA-konsolen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet. Undersöka varje misstänkt aktivitet genom att gå nedåt i entiteter (datorer, enheter, användare) för att öppna sina profilsidorna som innehåller mer information. Dessa resurser kan hjälpa dig arbeta med ATA: s misstänkta aktiviteter:

[ATA misstänkt aktivitet spelbok](http://aka.ms/ataplaybook) -den här artikeln vägleder dig igenom attackteknikerna för stöld av autentiseringsuppgifter med hjälp av tillgängliga diagnostiska verktyg på Internet. Du kan se hur ATA hjälper dig att få insyn i dessa hot vid varje punkt i attacken.

[Guide för misstänkt aktivitet i ATA](suspicious-activity-guide.md)



## <a name="security-best-practices"></a>Rekommenderade säkerhetsmetoder

[Metodtips för ATA](https://aka.ms/atasecbestpractices) -Metodtips för att skydda ATA.

[Vanliga frågor om ATA](ata-technical-faq.md) -den här artikeln innehåller en lista över vanliga frågor och svar om ATA och ger insikt och svar.

## <a name="additional-resources"></a>Ytterligare resurser

[Microsoft Security Channel 9-sidan](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Gruppresurser

[ATA-bloggen](https://aka.ms/ATABlog)
[ATA community](https://aka.ms/ATACommunity)
[ge feedback om ATA](https://aka.ms/ATAUserVoice)
