---
title: Ange aviseringsinställningar för e-post i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver hur du får Azure ATP meddela dig (via e-post eller genom vidarebefordran av Azure ATP-händelser) när det upptäcker misstänkta aktiviteter
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 399773b174f52cfc26888fcaa9923de4f258e897
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166892"
---
*Gäller för: Azure Avancerat skydd*



# <a name="integrate-with-syslog"></a>Integrera med Syslog

Azure ATP kan meddela dig när det upptäcker misstänkta aktiviteter och hälsovarningar genom att skicka aviseringen till Syslog-servern. Du kan ange följande om du aktiverar Syslog-aviseringar.

1.  Innan du konfigurerar Syslog-aviseringar arbetar du med SIEM-administratören för att ta reda på följande information:

    -   FQDN eller IP-adress för SIEM-servern

    -   Porten som SIEM-servern lyssnar på

    -   Vilken transport som ska användas: UDP, TCP eller TLS (skyddad Syslog)

    -   Format för att skicka data, RFC 3164 eller 5424

2.  Ange arbetsytans portal URL: en.

3.  Ange din Azure Active Directory-användarnamn och lösenord och klicka på **logga in**.

4.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Azure ATP ikon för konfigurationsinställningar](media/ATP-config-menu.png)

5.  Klicka på **meddelanden**, och under **Syslog-aviseringar** klickar du på **konfigurera** och ange följande information:

    |Fält|Description|
    |---------|---------------|
    |Sensorn|Välj en avsedda sensor som ansvarar för att sammanställa alla Syslog-händelser och vidarebefordrar dem till din SIEM-server.|
    |Tjänsteslutpunkt|Det fullständiga domännamnet för Syslog-servern och du kan också ändra portnumret (standard 514)|
    |Transport|Kan vara UDP, TCP eller TLS (skyddad Syslog)|
    |Format|Detta är det format som Azure ATP använder för att skicka händelser till SIEM-servern, antingen RFC 5424 eller RFC 3164.|

 ![Azure ATP Syslog bild för inställning av server](media/atp-syslog.png)

6. Du kan välja vilka händelser som ska skicka till Syslog-servern. Under **Syslog-aviseringar**, ange vilka meddelanden ska skickas till Syslog-servern - nya säkerhetsaviseringar, uppdaterade säkerhetsaviseringar och nya hälsorelaterade problem.


## <a name="see-also"></a>Se även

- [Arbeta med känsliga konton](sensitive-accounts.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)