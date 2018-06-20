---
title: Lista över användbara resurser för Azure Advanced Threat Protection | Microsoft Docs
description: Den här artikeln innehåller en lista över användbara resurser för Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8d91468664a76436078772ad1fc8510ea56d67a
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298504"
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Azure ATP beredskap guide

Den här artikeln ger en översikt över beredskap som ger dig en lista med resurser som hjälper dig att komma igång med Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Förstå Azure ATP

Azure avancerade Threat Protection (ATP) är en molnbaserad tjänst som hjälper dig att skydda företaget från flera typer av avancerade riktade cyber-attacker och insiderhot. Använd följande resurser om du vill veta mer om Azure ATP: 
- [Översikt över Azure ATP](what-is-atp.md)
- [Azure ATP inledande video - Full](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Distributionsbeslut

Azure ATP består av en molnbaserad tjänst som finns i Azure och sensorer som kan installeras på en domänkontrollant eller på dedicerade servrar. Innan du kan hämta Azure ATP igång, är det viktigt att välja vilken typ av sensorer bättre passa din distribution.<br>Om du använder fysiska servrar bör du planera kapaciteten. Du kan få hjälp från storleksverktyget att allokera utrymme för din sensorer: 
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool) -storleksverktyget automatiserar mängden trafik som övervakar Azure ATP samling. Det ger automatiskt support och resursen rekommendationer för sensorer. 
- [Planering vägledning för ATA-kapacitet](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Distribuera Azure ATP

Dessa resurser hjälper dig att ställa in Azure ATP, ansluta till Active Directory, hämta sensor, konfigurera händelseinsamling och om du vill integrera med din VPN och konfigurera honeytoken konton och undantag. 
- [Prova Azure ATP (ingår i EMS E5)](http://aka.ms/aatptrial) utvärderingsversionen är giltig i 90 dagar.
- [Distributionsguide för](install-atp-step1.md) distribuera Azure ATP i din miljö följa de här stegen.
- [Integrera Azure ATP med Windows Defender ATP](integrate-wd-atp.md)
- 
## <a name="azure-atp-settings"></a>Azure ATP-inställningar

Grundläggande nödvändiga inställningar i Azure ATP konfigureras när du skapar arbetsytan. Det finns dock andra inställningar som du kan konfigurera för att finjustera Azure ATP identifieringar exaktare för din miljö, till exempel SIEM-integrering och granska inställningar. 

- [Azure ATP allmän dokumentation](what-is-atp.md)
- [Granska inställningar](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – granska din hälsa före och efter en ATA-distribution. 

## <a name="work-with-azure-atp"></a>Arbeta med Azure ATP

När Azure ATP är igång, kommer du att kunna visa misstänkta aktiviteter som identifieras i i tidslinjen för aktiviteten. Detta är den standardsida du kommer till när du loggar in på Azure ATP-portalen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet. Granska varje misstänkt aktivitet genom att gå nedåt i entiteter (datorer, enheter, användare) för att öppna profilsidorna som innehåller mer information. Dessa resurser hjälper dig att arbeta med Azure ATP misstänkta aktiviteter: 

- [Azure ATP misstänkt aktivitet guide](suspicious-activity-guide.md) Lär dig att hantera och ta med din Azure ATP identifieringar nästa steg.
- [Tagga grupper som känsliga](sensitive-accounts.md) insyn i exponering av autentiseringsuppgifter på känsliga säkerhetsgrupper.

## <a name="security-best-practices"></a>Metodtips för säkerhet

- [Azure ATP vanliga frågor och svar](atp-technical-faq.md) -den här artikeln innehåller en lista med vanliga frågor och svar om Azure ATP och ger insikt och svar. 
## <a name="community-resources"></a>Gruppresurser

Blogg: [Azure ATP blogg](https://aka.ms/aatpblog)

Offentliga Community: [Azure ATP teknisk Community](https://aka.ms/AatpCom)

Privat Community: [Azure ATP Yammer-grupp](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Microsoft Security Channel 9 sida](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Se även

- [Arbeta med känsliga konton](sensitive-accounts.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)