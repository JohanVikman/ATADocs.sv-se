---
title: Felsöka Azure ATP kända problem | Microsoft Docs
description: Beskriver hur du kan felsöka problem i Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a56845c619e93ed2fae0e10876a4d49a49e23e7d
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166328"
---
*Gäller för: Azure Avancerat skydd*


# <a name="troubleshooting-azure-atp-known-issues"></a>Felsöka Azure ATP-kända problem 


## <a name="deployment-log-location"></a>Loggplatsen för distribution
 
Azure ATP-distributionsloggarna finns i temp-katalogen för den användare som installerade produkten. På standardplatsen för installation finns på: C:\Users\Administrator\AppData\Local\Temp (eller en katalog över % temp %). Mer information finns i [felsökning ATP med loggar](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-licensing-error"></a>Problem med autentisering i proxy presenterar som licensiering fel

Under installationen av sensorn du får följande fel: **sensorn kunde inte registreras pga licensieringsproblem.**

Loggposter för distribution: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 Info InteractiveDeploymentManager ValidateCreateSensorAsync returnerade [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 c 60 : 1AA8] [2018-03-24T23:59:56] i000: 2018-03-25 02:59:56.4856 Info InteractiveDeploymentManager ValidateCreateSensorAsync returnerade [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 C 60: 1AA8] [2018-03-25T00:27:56] i000: 2018-03-25 03:27:56.7399 felsöka SensorBootstrapperApplication Engine.Quit [\[] deploymentResultStatus = 1602 isRestartRequired = False [\]] [1 C 60: 15B8] [2018-03-25T00:27:56] i500: har påbörjat slutkod: 0x642


**Orsak:**

I vissa fall, när de kommunicerar via en proxyserver under autentiseringen kan de svara på Azure ATP-sensorn med fel 401 eller 403 i stället för fel 407. Azure ATP-sensorn tolkar fel 401 eller 403 som ett problem med licensiering och inte som ett proxy-autentisering-problem. 

**Lösning:**

Se till att sensorn kan bläddra till *. atp.azure.com via den konfigurerade proxyn utan autentisering. Mer information finns i [konfigurera proxyn för att aktivera kommunikation](configure-proxy.md).




## Azure ATP-sensorn NIC teaming problemet <a name="nic-teaming"></a>

Om du försöker installera ATP-sensorn på en dator som konfigureras med en NIC-teamindelningsadapter, får du ett fel vid installation. Om du vill installera ATP-sensorn på en dator som konfigureras med NIC-teamindelning, följer du dessa anvisningar:

Om du inte har installerat sensorn ännu:

1.  Hämta Npcap från [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Avinstallera WinPcap, om den har installerats.
3.  Installera Npcap med följande alternativ: loopback_support = Nej & winpcap_mode = Ja
4.  Installera sensorpaketet.

Om du redan har installerat sensorn:

1.  Hämta Npcap från [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Avinstallera sensorn.
3.  Avinstallera WinPcap.
4.  Installera Npcap med följande alternativ: loopback_support = Nej & winpcap_mode = Ja
5.  Installera om sensorpaketet.

## <a name="windows-defender-atp-integration-issue"></a>Windows Defender ATP-integrering problemet

Azure Advanced Threat Protection kan du integrera Azure ATP med Windows Defender ATP. 

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware-dator sensor problemet

Om du har en Azure ATP-sensorn på virtuella VMware-datorer kan du få övervakningsaviseringen **en del nätverkstrafik analyseras inte**. Detta inträffar på grund av ett konfigurationsmatchningsfel i VMware.

Att lösa problemet:

Ange följande inställningar **0** eller **inaktiverad** i konfigurationen för den virtuella datorns nätverkskort: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> För Azure ATP-sensorer, behöver du bara inaktivera **IPv4 TSO Offload** under konfigurationen av nätverkskort.

 ![VMware sensor problemet](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)