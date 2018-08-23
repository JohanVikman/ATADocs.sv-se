---
title: Lista över användbara resurser för Azure Advanced Threat Protection | Microsoft Docs
description: Den här artikeln innehåller en lista över användbara resurser för Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7018fb46a9d9da326ba999aff34a5ac2de6b860c
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734771"
---
*Gäller för: Azure Avancerat skydd*



# <a name="azure-atp-readiness-guide"></a>För med Azure ATP-beredskap

Den här artikeln ger en beredskapsöversikt som ger dig en lista med resurser som hjälper dig komma igång med Azure Advanced Threat Protection. 

## <a name="understanding-azure-atp"></a>Förstå Azure ATP

Azure avancerade Threat Protection (ATP) är en molnbaserad tjänst som hjälper dig att identifiera och skydda ditt företag från flera typer av avancerade riktade cyberattacker och insiderhot. Använd följande resurser om du vill veta mer om Azure ATP: 
- [Översikt över Azure ATP](what-is-atp.md)
- [Azure ATP introduktionsvideon – fullständig](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Distributionsbeslut

Azure ATP består av en molnbaserad tjänst som finns i Azure, och integrerade sensorer som kan installeras på en domänkontrollant eller fristående sensorer på dedicerade servrar. Innan du får Azure ATP igång, är det viktigt att välja vilken typ av sensorer som bäst passar din distribution och dina behov. Azure ATP integrerade sensorer ger förbättrad säkerhet, lägre driftskostnader och underlättar distributionen. Azure ATP fristående sensorer kräver fysisk maskinvara, additionl konfigurationssteg och tyngre driftskostnader. <br>Om du använder fysiska servrar, är det viktigt att planera för kapaciteten. Du kan få hjälp från storleksverktyget att allokera minne för dina sensorer: 
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool) -storleksverktyget automatiserar samling mängden trafik som övervakar Azure ATP. Automatiskt tillhandahåller support och resurs rekommendationer för sensorer. 
- [Kapacitetsplanering vägledning för ATA-kapacitet](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Distribuera Azure ATP

Dessa resurser kan du konfigurera Azure ATP, ansluta till Active Directory, hämtningspaketet sensor, konfigurera händelseinsamling och du kan också integrera med din VPN och konfigurera honeytoken-konton och undantag. 
- [Prova Azure ATP (ingår i EMS E5)](http://aka.ms/aatptrial) utvärderingsversionen gäller i 90 dagar.
- [Distributionsguide](install-atp-step1.md) distribuera Azure ATP i din miljö följa dessa steg.
- [Integrera Azure ATP med Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Azure ATP-inställningar

De grundläggande inställningarna som krävs i Azure ATP konfigureras när du skapar arbetsytan. Det finns dock flera ytterligare inställningar som du kan konfigurera för att finjustera Azure ATP som gör identifieringar exaktare för din miljö, till exempel SIEM-integrering och granska inställningar. 

- [Allmän dokumentation för Azure ATP](what-is-atp.md)
- [Granska inställningar](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – granska din domain controller hälsotillstånd före och efter en ATP-distribution. 

## <a name="work-with-azure-atp"></a>Arbeta med Azure ATP

När du har Azure ATP är igång och körs, visa identifierade misstänkta aktiviteter på tidslinjen för Azure ATP-portal aktivitet. Tidslinjen för aktiviteten är standardsidan när du loggar in på Azure ATP-portalen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet. Undersöka varje misstänkt aktivitet genom att gå nedåt i entiteter (datorer, enheter, användare) för att öppna sina profilsidorna med mer information. De här resurserna hjälpa dig arbeta med Azure ATP misstänkta aktiviteter: 

- [Guide för misstänkt aktivitet för Azure ATP](suspicious-activity-guide.md) Lär dig att sortera och fortsätt sedan med din Azure ATP-identifieringar.
- [Tagga grupper som känsliga](sensitive-accounts.md) få insyn i exponering av autentiseringsuppgifter på känsliga säkerhetsgrupper.

## <a name="security-best-practices"></a>Rekommenderade säkerhetsmetoder

- [Azure ATP vanliga frågor och svar](atp-technical-faq.md) -den här artikeln innehåller en lista över vanliga frågor och svar om Azure ATP och ger insikt och svar. 

## <a name="community-resources"></a>Gruppresurser

Blogg: [Azure ATP-bloggen](https://aka.ms/aatpblog)

Offentliga Community: [Azure ATP-Tech-Community](https://aka.ms/AatpCom)

Privat Community: [Azure ATP Yammer-grupp](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Microsoft Security Channel 9-sidan](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Se även

- [Arbeta med känsliga konton](sensitive-accounts.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)