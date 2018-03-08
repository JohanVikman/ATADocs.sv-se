---
title: Verifiera portspegling i Azure Advanced Threat Protection | Microsoft Docs
description: "Beskriver hur du verifierar att portspegling är korrekt konfigurerad i Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7628fa491ddbe477cab7eb414409028c0f94f44d
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/08/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="validate-port-mirroring"></a>Verifiera portspegling
> [!NOTE] 
> Den här artikeln gäller bara om du distribuerar distribuera Azure ATP fristående Sensor i stället för Azure ATP Sensor. Om du behöver använda Azure ATP Sensor finns [att välja rätt sensor för din distribution](atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment).
 
Följande steg vägleder dig genom processen för att verifiera att portspegling har konfigurerats korrekt. För Azure ATP ska fungera korrekt, kunna Azure ATP fristående sensor Se trafiken till och från domänkontrollanten. Den huvudsakliga datakälla som används av Azure ATP är djup paketinspektion av nätverkstrafiken till och från domänkontrollanterna. För Azure ATP att se nätverkstrafiken, måste portspegling konfigureras. Portspegling kopierar trafiken från en port (källport) till en annan port (målport).

## <a name="validate-port-mirroring-using-net-mon"></a>Validera portspegling med Net Mon
1.  Installera [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) på den fristående ATP-sensor som du vill validera.

    > [!IMPORTANT]
    > Om du väljer att installera Wireshark för att verifiera portspegling, starta om Azure ATP fristående sensor när valideringen.

2.  Öppna Network Monitor och skapa en ny avbildningsflik.

    1.  Välj endast nätverkskortet att **avbilda** eller nätverkskortet som är anslutet till växelporten som har konfigurerats som portspeglingsmål.

    2.  Se till att P-Mode har aktiverats.

    3.  Klicka på **Ny avbildning**.

        ![Bild för fliken skapa ny avbildning](media/atp-port-mirroring-capture.png)

3.  I fönstret Visa filter anger du filtret **KerberosV5 OR LDAP** och klickar sedan på **Verkställ**.

    ![Bild för att använda KerberosV5 or LDAP-filter](media/atp-port-mirroring-filter-settings.png)

4.  Klicka på **Starta** för att starta avbildningssessionen. Om du inte ser trafik till och från domänkontrollanten kontrollerar du konfigurationen av portspeglingen.

    ![Bild för att starta avbildningssession](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Det är viktigt att du kan se trafiken till och från domänkontrollanterna.
    

5.  Om du bara ser trafik i en riktning fungera med din nätverks- eller virtualiseringsteamen för att felsöka konfigurationen av portspeglingen.

## <a name="see-also"></a>Se även

- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Konfigurera portspegling](configure-port-mirroring.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
