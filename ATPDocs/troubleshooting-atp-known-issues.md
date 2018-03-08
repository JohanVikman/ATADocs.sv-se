---
title: "Felsöka Azure ATP kända problem | Microsoft Docs"
description: "Beskriver hur du felsöker problem i Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/6/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2895a38e2328fb7de4fe7f47d00c4e40ac854e74
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/08/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Felsöka Azure ATP kända problem 

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Azure ATP sensor NIC-teamindelning problemet

Om du försöker installera ATP-sensor på en dator som har konfigurerats med ett NIC-Teamindelning kort får ett fel vid installation. Om du vill installera ATP-sensor på en dator som har konfigurerats med NIC-teamindelning, följer du dessa anvisningar:

Om du inte har installerat sensorn ännu:

1.  Hämta Npcap från [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Avinstallera WinPcap, om den har installerats.
3.  Installera Npcap med följande alternativ: loopback_support = Nej & winpcap_mode = Ja
4.  Installera sensor-paketet.

Om du redan har installerat sensorn:

1.  Hämta Npcap från [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Avinstallera sensorn.
3.  Avinstallera WinPcap.
4.  Installera Npcap med följande alternativ: loopback_support = Nej & winpcap_mode = Ja
5.  Installera om sensor-paketet.

## <a name="windows-defender-atp-integration-issue"></a>Windows Defender ATP-integrering problemet

Azure Advanced Threat Protection kan du integrera Azure ATP med Windows Defender ATP. Integrering är för närvarande bara tillgänglig om du är Windows Defender ATP privat förhandsversion kund. 

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware virtuella sensor problemet

Om du har en Azure ATP sensor på virtuella VMware-datorer som kan aviseringen övervakning **nätverkstrafik analyseras inte**. Detta inträffar på grund av ett matchningsfel i VMware.

Så här löser du problemet:

Ange följande inställningar till **0** eller **inaktiverad** i konfiguration av den virtuella datorns nätverkskort: TsoEnable, LargeSendOffload, Systemansvarig avlastning, Giant Systemansvarig-avlastning.
> [!NOTE]
> För Azure ATP sensorer, behöver du bara inaktivera **IPv4 Systemansvarig Offload** under konfigurationen av nätverkskort.

 ![VMware sensor problemet](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)