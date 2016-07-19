---
title: Konfigurera portspegling | Microsoft Advanced Threat Analytics
description: "Beskriver alternativ för portspegling och hur du konfigurerar dem för ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 121f54e6d8da8220f1827188039e9a89c038f7ac
ms.openlocfilehash: a4befce4003951b18a5e1a9d8bc1addf9e7ea255


---

# Konfigurera portspegling
> [!NOTE] 
> Den här artikeln gäller bara om du distribuerar ATA Gateway i stället för ATA Lightweight Gateway. Mer information om hur du tar reda på om du behöver använda ATA Gateway finns i [Välja rätt gatewayer för distributionen](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)
 
Den huvudsakliga datakälla som används av ATA är djup paketinspektion av nätverkstrafiken till och från domänkontrollanterna. Om ATA ska kunna se nätverkstrafiken måste du konfigurera portspegling eller använda en nätverks-TAP.

För portspegling konfigurerar du **portspegling** för varje domänkontrollant som ska övervakas, som **källan** till nätverkstrafiken. Vanligtvis behöver du samarbeta med nätverks- eller virtualiseringsteamet när du vill konfigurera portspegling.
Mer information finns i leverantörens dokumentation.

Domänkontrollanterna och ATA-gatewayerna kan vara fysiska eller virtuella. Nedan hittar du vanliga metoder för portspegling och några saker att tänka på. Mer information finns i växelns eller virtualiseringsserverns produktdokumentation. Växeltillverkaren kan använda annan terminologi.

**SPAN (Switched Port Analyzer)** – kopierar nätverkstrafik från en eller flera växelportar till en annan växelport på samma växel. Både ATA-gatewayen och domänkontrollanterna måste vara anslutna till samma fysiska växel.

**RSPAN (Remote Switch Port Analyzer)** – gör att du kan övervaka nätverkstrafik från källportar som är fördelade på flera fysiska växlar. RSPAN kopierar källtrafiken till ett särskilt RSPAN-konfigurerat VLAN. Detta VLAN måste trunkeras till de andra berörda växlarna. RSPAN fungerar på lager 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)** – är en upphovsrättsskyddad Cisco-teknik som fungerar på lager 3. ERSPAN gör att du kan övervaka trafik för växlar utan att behöva VLAN-trunkar. ERSPAN använder GRE (Generic Routing Encapsulation) för att kopiera övervakad nätverkstrafik. ATA kan för närvarande inte ta emot ERSPAN-trafik direkt. För att ATA ska fungera med ERSPAN-trafik måste en växel eller router som kan avkapsla trafiken konfigureras som mål för ERSPAN där trafiken avkapslas. Växeln eller routern måste sedan konfigureras så att den vidarebefordras till ATA-gatewayen med SPAN eller RSPAN.

> [!NOTE]
> Om domänkontrollanten som portspeglas är ansluten via en WAN-länk ska du kontrollera att WAN-länken kan hantera den ytterligare belastningen av ERSPAN-trafiken.

## Alternativ för portspegling som stöds

|ATA Gateway|Domänkontrollant|Överväganden|
|---------------|---------------------|------------------|
|Virtuell|Virtuell på samma värd|Den virtuella växeln måste ha stöd för portspegling.<br /><br />Portspeglingen kan sluta fungera om en av de virtuella datorerna flyttas till en annan värd själv.|
|Virtuell|Virtuell på olika värdar|Kontrollera att den virtuella växeln har stöd för det här scenariot.|
|Virtuell|Fysiskt|Kräver ett dedikerat nätverkskort. Annars ser ATA all trafik som kommer in till och ut från värden, även den trafik som skickas till ATA Center.|
|Fysiskt|Virtuell|Kontrollera att den virtuella växeln har stöd för det här scenariot – och konfiguration av portspegling på de fysiska växlarna baserat på scenariot:<br /><br />Om den virtuella värden finns på samma fysiska växel behöver du konfigurera SPAN på växelnivå.<br /><br />Om den virtuella värden finns på en annan växel behöver du konfigurera RSPAN eller ERSPAN&#42;.|
|Fysiskt|Fysisk på samma växel|Fysisk växel måste ha stöd för SPAN/portspegling.|
|Fysiskt|Fysisk på en annan växel|Kräver att fysiska växlar har stöd för RSPAN eller ERSPAN&#42;.|
&#42; ERSPAN stöds endast när avkapsling utförs innan trafiken analyseras av ATA.

> [!NOTE]
> Kontrollera att domänkontrollanterna och ATA-gatewayerna som de ansluter till har tidsinställningen synkroniserad högst 5 minuter från varandra.

**Om du arbetar med virtualiseringskluster:**

-   Konfigurera tillhörighet mellan domänkontrollanten och ATA-gatewayen för varje domänkontrollant som körs i virtualiseringsklustret på en virtuell dator med ATA-gatewayen. På så sätt följer ATA-gatewayen domänkontrollanten när den flyttas till en annan värd i klustret. Det fungerar bra om det finns några få domänkontrollanter.
> [!NOTE]
> Om miljön har stöd för virtuell till virtuell på olika värdar (RSPAN) behöver du inte oroa dig över tillhörighet.
> 
-   Om du vill se till att ATA-gatewayerna har rätt storlek för att hantera övervakning av alla domänkontrollanter själva testar du det här alternativet: Installera en virtuell dator på varje virtualiseringsvärd och installera en ATA-gateway på varje värd. Konfigurera varje ATA-gateway så att den övervakar alla domänkontrollanter som körs i klustret. På så sätt övervakas alla värdar som domänkontrollanterna körs på.

När du har konfigurerat portspegling ska du kontrollera att det fungerar innan du installerar ATA-gatewayen.

## Se även
- [Verifiera portspegling](validate-port-mirroring.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO5-->


