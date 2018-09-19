---
title: Referens för ATA händelse-ID | Microsoft Docs
description: 'Innehåller en lista över ATA-händelser ID: N och deras beskrivningar.'
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 38610c6b8f94dbe1a31e218e064750bf2bde2c49
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133148"
---
*Gäller för: Advanced Threat Analytics version 1.9*


# <a name="ata-event-id-reference"></a>Referens för ATA händelse-ID

ATA Center-Loggboken loggar händelser för ATA. Den här artikeln innehåller en lista över händelse-ID och ger en beskrivning av varje.

Händelserna finns här:

![plats för händelse-ID](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA Health-händelser

1001 – ATA Center databasdata enhet hälsoavisering för ledigt utrymme 

1003 – ATA Center överbelastade hälsoavisering 

1004 – hälsoavisering för certifikatet upphör att gälla 

1005 – centerdatabas frånkopplad hälsoavisering 

1006 – ATA Gateway directory services-konto lösenord förfallodatum hälsotillstånd varning 

1007 – hälsoavisering för ATA Gateway-domän synkroniseraren som inte har tilldelats 

1008 – felaktig hälsoavisering för ATA Gateway avbildning för network adapter 

1009 – ATA Gateway capture network adapter saknas hälsoavisering 

1010 – ATA Gateway hälsoavisering för directory services-klienten anslutning 

1011 – frånkopplade hälsoavisering för ATA Gateway 

1012 – ATA Gateway överbelastad hälsoavisering för händelsen aktiviteter 

1013 – ATA Gateway överbelastad hälsoavisering för nätverket aktiviteter 

1014 – hälsoavisering för center e-post 

1015 – hälsoavisering för center Syslog 

1016 – inaktuella hälsoavisering för ATA-gatewayer 

1017 – center inte tar emot trafik hälsoavisering 

1018 – hälsoavisering för ATA Gateway-startfel 

1019 – ATA Gateway hälsoavisering för lite minne 

1020 – hälsoavisering för ATA Gateway RADIUS händelse lyssnare 

1021 – hälsoavisering för ATA Gateway Syslog händelse lyssnare 

1022 – ATA Center externa IP-adress upplösning fel hälsoavisering 
 
## <a name="ata-suspicious-activity-events"></a>ATA-händelser för misstänkta aktiviteter

2001 – onormalt beteende misstänkt aktivitet 

2002 – onormalt protokollet misstänkt aktivitet 

2003 – misstänkt kontouppräkningsaktivitet 

2004 – LDAP brute force misstänkt aktivitet 

2006 – katalogtjänster replikering misstänkt aktivitet 

2007 – DNS-rekognosering misstänkt aktivitet 

2008 – misstänkt aktivitet för nedgradering av kryptering 

2012 – räkna upp sessioner misstänkt aktivitet 

2013 – förfalskad PAC misstänkt aktivitet 

2014 – misstänkt aktivitet för Honeytoken-aktivitet 

2016 – enormt objekt borttagning av misstänkt aktivitet 

2017 – skicka hash misstänkt aktivitet 

2018 – skicka biljetten misstänkt aktivitet 

2019 – fjärrkörning misstänkt aktivitet 

2020 – hämta data protection backup viktiga misstänkt aktivitet 

2021 – SAMR rekognosering misstänkt aktivitet 

2022 – misstänkt golden ticket-aktivitet 

2023 – brute force misstänkt aktivitet 

2024 - onormalt känslig gruppmedlemskap ändras misstänkt aktivitet  

## <a name="ata-auditing-events"></a>ATA-granskningshändelser

3001 – ändra till ATA-konfiguration 

3002 – ATA Gateway har lagts till

3003 – ATA-gatewayen har tagits bort

3004 – ATA-licens som aktiverats

3005 – logga in på ATA-konsolen

3006 – manuell ändring av hälsostatus för aktivitet 

3007 – manuell ändring av status för misstänkt aktivitet 


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
