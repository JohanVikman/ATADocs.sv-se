---
title: Konfigurera portspegling vid distribution av Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver alternativ för portspegling och hur du konfigurerar dem för Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ac3c584f5eb73b33415c6c1250eee4c41a12763
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125999"
---
*Gäller för: Azure Avancerat skydd*



# <a name="configure-port-mirroring"></a>Konfigurera portspegling
> [!NOTE] 
> Den här artikeln gäller bara om du distribuerar Azure ATP fristående sensorn i stället för Azure ATP-sensorn. För att avgöra om du behöver använda Azure ATP-sensorn fristående, se [välja rätt sensorer för din distribution](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Den huvudsakliga datakälla som används av Azure ATP är djup paketinspektion för nätverkstrafiken till och från domänkontrollanterna. För Azure ATP att se nätverkstrafiken måste du antingen konfigurera portspegling eller använda en nätverks-TAP.

För portspegling konfigurerar du **portspegling** för varje domänkontrollant som ska övervakas, som **källan** till nätverkstrafiken. Vanligtvis måste du arbeta med nätverks- eller -teamet att konfigurera portspegling.
Mer information finns i dokumentationen från leverantören.

Dina domänkontrollanter och fristående Azure ATP-sensorn kan vara antingen fysiska eller virtuella. Nedan hittar du vanliga metoder för portspegling och några saker att tänka på. Mer information finns i din växelns eller virtualiseringsserverns produktdokumentation. Växeltillverkaren kan använda annan terminologi.

**SPAN (Switched Port Analyzer)** – kopierar nätverkstrafik från en eller flera växelportar till en annan växelport på samma växel. Båda i Azure ATP fristående sensorn och domänkontrollanterna måste vara ansluten till samma fysiska växel.

**RSPAN (Remote Switch Port Analyzer)** – gör att du kan övervaka nätverkstrafik från källportar som är fördelade på flera fysiska växlar. RSPAN kopierar källtrafiken till ett särskilt RSPAN-konfigurerat VLAN. Detta VLAN måste trunkeras till de andra berörda växlarna. RSPAN fungerar på lager 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)** – är en upphovsrättsskyddad Cisco-teknik som fungerar på lager 3. ERSPAN gör att du kan övervaka trafik för växlar utan att behöva VLAN-trunkar. ERSPAN använder GRE (Generic Routing Encapsulation) för att kopiera övervakad nätverkstrafik. Azure ATP för närvarande inte direkt ta emot ERSPAN-trafik. För Azure ATP att fungera med ERSPAN-trafik, måste en växel eller router som kan avkapsla trafiken konfigureras som mål för ERSPAN där trafiken är avkapslade. Konfigurera sedan växeln eller routern avkapslade trafiken till Azure ATP fristående sensorn med SPAN eller RSPAN.

> [!NOTE]
> Om domänkontrollanten som portspeglas är ansluten via en WAN-länk ska du kontrollera att WAN-länken kan hantera den ytterligare belastningen av ERSPAN-trafiken.
> Azure ATP stöder endast trafiköverföring när trafiken når nätverkskortet och domänkontrollanten på samma sätt. Azure ATP stöder inte trafiköverföring när trafiken har brutits ut till olika portar.

## <a name="supported-port-mirroring-options"></a>Alternativ för portspegling som stöds

|Azure ATP fristående sensor|Domänkontrollant|Överväganden|
|---------------|---------------------|------------------|
|Virtuell|Virtuell på samma värd|Den virtuella växeln måste ha stöd för portspegling.<br /><br />Portspeglingen kan sluta fungera om en av de virtuella datorerna flyttas till en annan värd själv.|
|Virtuell|Virtuell på olika värdar|Kontrollera att den virtuella växeln har stöd för det här scenariot.|
|Virtuell|Fysiskt|Kräver ett dedikerat nätverkskort som annars Azure ATP ser all trafik som kommer in och ut från värden, även den trafik som skickas till Azure ATP-Molntjänsten.|
|Fysiskt|Virtuell|Kontrollera att den virtuella växeln har stöd för det här scenariot – och konfiguration av portspegling på de fysiska växlarna baserat på scenariot:<br /><br />Om den virtuella värden finns på samma fysiska växel, måste du konfigurera på växelnivå.<br /><br />Om den virtuella värden finns på en annan växel, måste du konfigurera RSPAN eller ERSPAN&#42;.|
|Fysiskt|Fysisk på samma växel|Fysisk växel måste ha stöd för SPAN/portspegling.|
|Fysiskt|Fysisk på en annan växel|Kräver att fysiska växlar har stöd för RSPAN eller ERSPAN&#42;.|

&#42;ERSPAN stöds endast när avkapsling utförs innan trafiken analyseras av ATP.

> [!NOTE]
> Se till att domänkontrollanter och Azure ATP-fristående sensorn som de ansluter har tidsinställningen synkroniserad högst fem minuter från varandra.

**Om du arbetar med virtualiseringskluster:**

-   Konfigurera tillhörighet mellan domänkontrollanten och fristående Azure ATP-sensorn för varje domänkontrollant som körs i virtualiseringsklustret på en virtuell dator med fristående Azure ATP-sensorn. Det här sättet när domänkontrollanten flyttar till en annan värd i klustret fristående Azure ATP-sensorn följer den. Det fungerar bra om det finns några få domänkontrollanter.

 > [!NOTE]
 > Om miljön har stöd för virtuell till virtuell på olika värdar (RSPAN) behöver du inte oroa dig över tillhörighet.
 
-   För att säkerställa fristående Azure ATP-sensorn har rätt storlek för att hantera övervakning av alla domänkontrollanter själva, testa det här alternativet: Installera en virtuell dator på varje Virtualiseringsvärd och installera en fristående Azure ATP-sensorn på varje värd. Konfigurera varje Azure ATP fristående sensor för att övervaka alla domänkontrollanter som körs i klustret. Det här sättet, övervakas alla värdar som domänkontrollanterna körs på.

När du har konfigurerat portspegling ska du kontrollera att portspegling fungerar innan du installerar den fristående Azure ATP-sensorn.

## <a name="see-also"></a>Se även
- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
