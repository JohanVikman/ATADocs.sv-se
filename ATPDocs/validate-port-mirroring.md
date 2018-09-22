---
title: Verifiera portspegling i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver hur du verifierar att portspegling är korrekt konfigurerad i Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.service: ''
ms.technology: ''
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 15e53ef145b9d7bbbc980730acec6c3b92c1a0fa
ms.sourcegitcommit: e0b9252c770b3a3695af1642b76e3304f3df15d4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2018
ms.locfileid: "46566612"
---
*Gäller för: Azure Avancerat skydd*



# <a name="validate-port-mirroring"></a>Verifiera portspegling
> [!NOTE] 
> Den här artikeln är bara relevant om du distribuerar distribuera Azure ATP fristående sensorn i stället för Azure ATP-sensorn. För att avgöra om du behöver använda Azure ATP-sensorn, se [välja rätt sensorn för din distribution](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Följande steg vägleder dig genom processen för att verifiera att portspegling har konfigurerats korrekt. För Azure ATP ska fungera korrekt, kunna fristående Azure ATP-sensorn Se trafik till och från domänkontrollanten. Den huvudsakliga datakälla som används av Azure ATP är djup paketinspektion för nätverkstrafiken till och från domänkontrollanterna. För Azure ATP att se nätverkstrafiken måste portspegling vara konfigurerad. Portspegling kopierar trafiken från en port (källport) till en annan port (målport).

## <a name="validate-port-mirroring-using-net-mon"></a>Validera portspegling med Net Mon
1.  Installera [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) på fristående ATP-sensorn som du vill validera.

    > [!IMPORTANT]
    > Om du väljer att installera Wireshark för att verifiera portspegling, startar du om tjänsten Azure ATP fristående sensorn efter valideringen.

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

- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Konfigurera portspegling](configure-port-mirroring.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
