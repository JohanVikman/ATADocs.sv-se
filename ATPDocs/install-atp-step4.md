---
title: Installera Azure Advanced Threat Protection – steg 4 | Microsoft Docs
description: Steg fyra av Azure ATP-installationen hjälper dig att installera den fristående Azure ATP-sensorn.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9eaa6b37d56c3d8b18c3f5d015581cf7975d6e93
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126339"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-4"></a>Installera Azure ATP - steg 4

>[!div class="step-by-step"]
[« Steg 3](install-atp-step3.md)
[Steg 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Steg 4. Installera Azure ATP-sensorn

Innan du installerar Azure ATP-sensorn fristående på en dedikerad server måste du verifiera att portspegling är korrekt konfigurerad och att den fristående Azure ATP-sensorn kan se trafik till och från domänkontrollanterna. 


> [!IMPORTANT]
>Se till att .net Framework 4.7 är installerad på datorn. Om .net Framework 4.7 är inte installerat Azure ATP-sensorn installationspaketet installerar den, vilket kräver en omstart av servern.

Utför följande steg på Azure ATP-sensorn servern eller domänkontrollanten.

1. Kontrollera att datorn är ansluten till relevanta Azure ATP-tjänsten molnslutpunkten:
  - https://triprd1wceuw1sensorapi.atp.azure.com (för Europa)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (för USA)
  - https://triprd1wcasse1sensorapi.atp.azure.com (för Asien)

2. Extrahera installationsfilerna från zip-filen. 
> [!NOTE] 
> Det går inte att installera direkt från zip-filen.

3.  Kör **Azure ATP-sensorn setup.exe** och följ installationsguiden.

4.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

     ![Azure ATP fristående sensorn installationsspråk](media/sensor-install-language.png)


5.  Installationsguiden kontrollerar automatiskt om servern är en domänkontrollant eller en dedikerad server. Om det är en domänkontrollant, Azure ATP-sensorn installeras, om det är en dedikerad server, fristående Azure ATP-sensorn installeras. 
    
    För ett fristående Azure ATP-sensorn exempelvis visas följande skärm så att du vet att en fristående Azure ATP-sensorn är installerad på din dedikerade server:
    
    ![Azure ATP fristående sensorn installation](media/sensor-install-deployment-type.png)

    Klicka på **Nästa**.

    > [!NOTE] 
    > Om domänkontrollanten eller dedikerad server inte uppfyller de lägsta maskinvarukraven för installation, får du en varning. Detta förhindrar inte att du klickar på **Nästa** och fortsätter med installationen. Det kan vara rätt alternativ för installation av Azure ATP i en liten labbtestmiljö där du inte behöver lika mycket utrymme för lagring av data. För produktionsmiljöer, rekommenderas att arbeta med Azure ATP [kapacitetsplanering](atp-capacity-planning.md) guide för att se till att dina domänkontrollanter eller dedikerade servrar uppfyller de nödvändiga kraven.

6.  Under **Konfigurera sensorn**, ange installationssökvägen och åtkomstnyckel som du kopierade i föregående steg, baserat på miljön:

    ![Azure ATP fristående sensorn configuration bild](media/sensor-install-config.png)

      - Installationssökväg: Det här är den plats där fristående Azure ATP-sensorn är installerad. Som standard är detta %programfiles%\Azure Advanced Threat Protection sensorn. Lämna standardvärdet.

      - Åtkomstnyckel: Denna hämtas från arbetsytans portal i föregående steg.
    
7. Klicka på **Installera**. Följande komponenter installeras och konfigureras under installationen av Azure ATP-sensorn:

    -   KB 3047154 (endast för Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installera inte KB 3047154 på en virtualiseringsvärd (värden som kör virtualiseringen, det går bra att köra den på en virtuell dator). Det kan leda till att portspegling slutar fungera ordentligt. 
        > -   Om Wireshark är installerad på ATP-sensorn datorn när du kör Wireshark som du måste starta om ATP-sensorn eftersom den använder samma drivrutiner.

    -   Azure ATP-sensorn-tjänsten och uppdateringstjänsten för Azure ATP-sensorn
    -   Microsoft Visual C++ 2013 Redistributable

8.  När installationen är klar klickar du på **starta** att öppna webbläsaren och logga in på Azure ATP-arbetsyteportalen.


>[!div class="step-by-step"]
[« Steg 3](install-atp-step3.md)
[Steg 5 »](install-atp-step5.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Krav för Azure ATP](atp-prerequisites.md)

- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
