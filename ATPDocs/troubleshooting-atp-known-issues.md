---
title: Felsöka Azure ATP kända problem | Microsoft Docs
description: Beskriver hur du felsöker problem i Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 15c857085fb7d003f783981a89fe02e920a8e49a
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Felsöka Azure ATP kända problem 


## <a name="deployment-log-location"></a>Platsen för distribution
 
Azure ATP-distributionsloggar finns i temp-katalogen för den användare som installerade produkten. På standardplatsen för installation finns på: C:\Users\Administrator\AppData\Local\Temp (eller en katalog över % temp %).

## <a name="proxy-authentication-problem-presents-as-licensing-error"></a>Problem med autentisering i proxy presenteras som licensieringsfel

Under installationen av sensor du följande felmeddelande: **sensorn kunde inte registreras på grund av problem.**

Distribution loggposter: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 Info InteractiveDeploymentManager ValidateCreateSensorAsync returnerade [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 c 60 : 1AA8] [2018-03-24T23:59:56] i000: 2018-03-25 02:59:56.4856 Info InteractiveDeploymentManager ValidateCreateSensorAsync returnerade [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 C 60: 1AA8] [2018-03-25T00:27:56] i000: 2018-03-25 03:27:56.7399 felsöka SensorBootstrapperApplication Engine.Quit [\[] deploymentResultStatus = 1602 isRestartRequired = False [\]] [1 C 60: 15B8] [2018-03-25T00:27:56] i500: avslutas, slutkod: 0x642


**Orsak:**

I vissa fall, när de kommunicerar via en proxyserver under autentiseringen kan den svara på Azure ATP sensor med fel 401 eller 403 i stället för fel 407. Azure ATP-sensor tolkar fel 401 eller 403 som ett licensiering problem och inte som en proxy-autentiseringsproblem. 

**Lösning:**

Se till att sensorn kan bläddra till *. atp.azure.com via den konfigurerade proxyn utan autentisering. Mer information finns i [konfigurera proxy för att aktivera kommunikation](configure-proxy.md).




## Azure ATP sensor NIC-teamindelning problemet <a name="nic-teaming"></a>

Om du försöker installera ATP-sensor på en dator som har konfigurerats med ett NIC-Teamindelning kort får ett fel vid installation. Om du vill installera ATP-sensor på en dator som har konfigurerats med NIC-teamindelning, följer du dessa anvisningar:

Om du inte har installerat sensorn ännu:

1.  Hämta Npcap från [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Avinstallera WinPcap, om den har installerats.
3.  Installera Npcap med följande alternativ: loopback_support = Nej & winpcap_mode = Ja
4.  Installera sensor-paketet.

Om du redan har installerat sensorn:

1.  Hämta Npcap från [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
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