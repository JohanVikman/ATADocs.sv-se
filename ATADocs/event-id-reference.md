---
title: "ATA-händelse-ID referens | Microsoft Docs"
description: "Innehåller en lista över ATA-händelser ID: N och deras beskrivningar."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 3ef6322a4c63c15bbdae0669a7d116dfd80756db
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/06/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# <a name="ata-event-id-reference"></a>ID-referens för ATA-händelse

ATA Center Loggboken loggar händelser för ATA. Den här artikeln innehåller en lista över händelse-ID och en beskrivning av varje.

Händelserna som finns här:

![plats för händelse-ID](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA-hälsa händelser

1001 – ATA Center databasdata enhet hälsoavisering för ledigt utrymme 

1003 – ATA Center överbelastad hälsoavisering 

1004 – hälsoavisering för certifikatet upphör att gälla 

1005 – centerdatabas frånkopplad hälsoavisering 

1006 – ATA Gateway directory services-konto lösenord upphör att gälla hälsa varning 

1007 – ATA Gateway-domän synkroniseraren som inte har tilldelats hälsoavisering 

1008 – ATA Gateway avbilda felaktig hälsoavisering för nätverket nätverkskort 

1009 – ATA Gateway avbilda nätverkskortet saknade hälsoavisering 

1010 – ATA Gateway directory services-klienten anslutning hälsoavisering 

1011 – ATA Gateway avbrutna hälsoavisering 

1012 – ATA Gateway överlagrade aktiviteter om hälsa aviseringar 

1013 – ATA Gateway överbelastad hälsoavisering aktiviteter för nätverk 

1014 – hälsoavisering för center e-post 

1015 – health center Syslog-avisering 

1016 – ATA-gatewayer inaktuella hälsoavisering 

1017 – center inte tar emot trafik hälsoavisering 

1018 – ATA-gatewayen startar hälsa avisering 

1 019 – ATA Gateway minnesbrist hälsoavisering 

1020 – ATA Gateway RADIUS-lyssnaren hälsa aviseringar 

1021 – ATA Gateway Syslog listener hälsa aviseringar 

1022 – ATA Center externa IP-adress upplösning hälsa avisering 
 
## <a name="ata-suspicious-activity-events"></a>ATA misstänkt aktivitetshändelser

2001 – onormalt beteende misstänkt aktivitet 

2002 – onormal protokollet misstänkt aktivitet 

2003 – kontot uppräkningen misstänkt aktivitet 

2004 – LDAP brute force misstänkt aktivitet 

2005 – datorn förautentisering misslyckades misstänkt aktivitet 

2006 – directory services replikering misstänkt aktivitet 

2007 – DNS-rekognosering misstänkt aktivitet 

2008-kryptering för nedgradering av misstänkt aktivitet 

2012 – räkna upp sessioner misstänkt aktivitet 

2013 – förfalskad PAC misstänkt aktivitet 

2014 – Honeytoken aktivitet misstänkt aktivitet 

2015 – LDAP Rensa text lösenord misstänkt aktivitet 

2016 – omfattande objektet tas bort misstänkt aktivitet 

2017 – skicka hash misstänkt aktivitet 

2018 – skicka biljett misstänkt aktivitet 

2019 – fjärrkörning misstänkt aktivitet 

2020 – hämta data protection säkerhetskopiering viktiga misstänkt aktivitet 

2021 – SAMR rekognosering misstänkt aktivitet 

2022 – golden ticket misstänkt aktivitet 

2023 – brute force misstänkt aktivitet 

2024 - onormal känsliga gruppmedlemskap ändra misstänkt aktivitet  

## <a name="ata-auditing-events"></a>ATA-granskningshändelser

3001 – ändra till ATA-konfiguration 

3002 – ATA Gateway har lagts till

3003 – ATA Gateway som har tagits bort

3004 - ATA-licens som aktiverats

3005 – logga in på ATA-konsolen

3006 – manuell ändring hälsostatus för aktiviteten 

3007 – manuell ändring av status för misstänkt aktivitet 


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
