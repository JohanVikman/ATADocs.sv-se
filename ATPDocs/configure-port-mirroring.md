---
title: "Konfigurera portspegling när du distribuerar Azure Advanced Threat Protection | Microsoft Docs"
description: "Beskriver alternativ för portspegling och hur du konfigurerar dem för Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1cc622f1a8306530423920873e5efa05e8c87064
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="configure-port-mirroring"></a>Konfigurera portspegling
> [!NOTE] 
> Den här artikeln gäller bara om du distribuerar Azure ATP fristående sensor i stället för Azure ATP sensor. Om du behöver använda Azure ATP fristående sensor finns [att välja rätt sensorer för din distribution](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Den huvudsakliga datakälla som används av Azure ATP är djup paketinspektion av nätverkstrafiken till och från domänkontrollanterna. För Azure ATP att se nätverkstrafiken, måste du antingen konfigurera portspegling eller använda en nätverks-TAP.

För portspegling konfigurerar du **portspegling** för varje domänkontrollant som ska övervakas, som **källan** till nätverkstrafiken. Normalt behöver arbeta med nätverks- eller -teamet för att konfigurera portspegling.
Mer information finns i leverantörens dokumentation.

Dina domänkontrollanter och Azure ATP fristående sensor kan vara antingen fysiska eller virtuella. Nedan hittar du vanliga metoder för portspegling och några saker att tänka på. Mer information finns i växelns eller virtualiseringsserverns produktdokumentation. Växeltillverkaren kan använda annan terminologi.

**SPAN (Switched Port Analyzer)** – kopierar nätverkstrafik från en eller flera växelportar till en annan växelport på samma växel. Både de Azure ATP fristående sensor och domänkontrollanterna måste vara ansluten till samma fysiska växel.

**RSPAN (Remote Switch Port Analyzer)** – gör att du kan övervaka nätverkstrafik från källportar som är fördelade på flera fysiska växlar. RSPAN kopierar källtrafiken till ett särskilt RSPAN-konfigurerat VLAN. Detta VLAN måste trunkeras till de andra berörda växlarna. RSPAN fungerar på lager 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)** – är en upphovsrättsskyddad Cisco-teknik som fungerar på lager 3. ERSPAN gör att du kan övervaka trafik för växlar utan att behöva VLAN-trunkar. ERSPAN använder GRE (Generic Routing Encapsulation) för att kopiera övervakad nätverkstrafik. Azure ATP för närvarande inte direkt ta emot ERSPAN-trafik. För Azure ATP ska fungera med ERSPAN-trafik, måste en växel eller router som kan avkapsla trafiken konfigureras som mål för ERSPAN där trafiken är avkapslade. Konfigurera sedan växeln eller routern avkapslade trafiken till Azure ATP fristående sensorn med SPAN eller RSPAN.

> [!NOTE]
> Om domänkontrollanten som portspeglas är ansluten via en WAN-länk ska du kontrollera att WAN-länken kan hantera den ytterligare belastningen av ERSPAN-trafiken.
> Azure ATP endast stöd för övervakning av nätverkstrafik när trafiken når NIC och domänkontrollanten på samma sätt. Azure ATP stöder inte övervakning av nätverkstrafik när trafiken delas till olika portar.

## <a name="supported-port-mirroring-options"></a>Alternativ för portspegling som stöds

|Azure ATP fristående sensor|Domänkontrollant|Överväganden|
|---------------|---------------------|------------------|
|Virtuell|Virtuell på samma värd|Den virtuella växeln måste ha stöd för portspegling.<br /><br />Portspeglingen kan sluta fungera om en av de virtuella datorerna flyttas till en annan värd själv.|
|Virtuell|Virtuell på olika värdar|Kontrollera att den virtuella växeln har stöd för det här scenariot.|
|Virtuell|Fysiskt|Kräver ett dedikerat nätverkskort annars Azure ATP ser all trafik som kommer till och från värden, även den trafik som skickas till Azure ATP-Molntjänsten.|
|Fysiskt|Virtuell|Kontrollera att den virtuella växeln har stöd för det här scenariot – och konfiguration av portspegling på de fysiska växlarna baserat på scenariot:<br /><br />Om den virtuella värden finns på samma fysiska växel, måste du konfigurera på växelnivå.<br /><br />Om den virtuella värden finns på en annan växel, måste du konfigurera RSPAN eller ERSPAN &#42;.|
|Fysiskt|Fysisk på samma växel|Fysisk växel måste ha stöd för SPAN/portspegling.|
|Fysiskt|Fysisk på en annan växel|Kräver att fysiska växlar har stöd för RSPAN eller ERSPAN&#42;.|
&#42; ERSPAN stöds endast när avkapsling utförs innan trafiken analyseras av ATP.

> [!NOTE]
> Se till att domänkontrollanter och de ansluter Azure ATP fristående sensorn har tidsinställningen synkroniserad högst 5 minuter från varandra.

**Om du arbetar med virtualiseringskluster:**

-   För varje domänkontrollant som körs i virtualiseringsklustret på en virtuell dator med Azure ATP fristående sensor, konfigurera tillhörighet mellan domänkontrollanten och Azure ATP fristående sensorn. Det här sättet när domänkontrollanten flyttar till en annan värd i klustret Azure ATP fristående sensor följer den. Det fungerar bra om det finns några få domänkontrollanter.

 > [!NOTE]
 > Om miljön har stöd för virtuell till virtuell på olika värdar (RSPAN) behöver du inte oroa dig över tillhörighet.
 
-   Kontrollera att Azure ATP fristående sensorn har rätt storlek för att hantera övervakning av alla domänkontrollanter själva genom att testa det här alternativet: Installera en virtuell dator på varje Virtualiseringsvärd och installera en fristående Azure ATP-sensor på varje värd. Konfigurera varje Azure ATP fristående sensor om du vill övervaka alla domänkontrollanter som körs på klustret. På så sätt kan övervakas alla värdar som domänkontrollanterna körs på.

Verifiera att portspegling fungerar innan du installerar Azure ATP fristående sensor när du har konfigurerat portspegling.

## <a name="see-also"></a>Se även
- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)