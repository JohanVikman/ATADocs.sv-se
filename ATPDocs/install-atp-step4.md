---
title: Installera Azure Advanced Threat Protection - steg 4 | Microsoft Docs
description: "Steg fyra av Azure ATP-installationen hjälper dig att installera Azure ATP fristående sensorn."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7b003882f21f22b3427fb95534ca2bde255b14e6
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-4"></a>Installera Azure ATP - steg 4

>[!div class="step-by-step"]
[« Steg 3](install-atp-step3.md)
[Steg 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Steg 4. Installera Azure ATP-temperatursensor

Innan du installerar Azure ATP fristående sensor på en dedikerad server att verifiera att portspegling är korrekt konfigurerad och att Azure ATP fristående sensor kan se trafik till och från domänkontrollanterna. 


> [!IMPORTANT]
>Se till att .net Framework 4.7 är installerat på datorn. Om .net Framework 4.7 är inte installerat installationspaketet för Azure ATP sensor installerar den, vilket kräver en omstart av servern. Kontrollera att datorn är ansluten till Azure ATP molnet tjänstslutpunkten: https://triprd1wceuw1sensorapi.atp.azure.com (för Europa) eller https://triprd1wcuse1sensorapi.atp.azure.com (för USA).

Utför följande steg på Azure ATP sensor servern eller domänkontrollanten.

1.  Extrahera filerna från ZIP-filen. 
> [!NOTE] 
> Det går inte att installera direkt från zip-filen.

2.  Kör **Azure ATP sensor setup.exe** och följ installationsguiden.

3.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

     ![Azure ATP fristående sensor installationen språk](media/sensor-install-language.png)


4.  Installationsguiden kontrollerar automatiskt du om servern är en domänkontrollant eller en dedikerad server. Om det är en domänkontrollant, Azure ATP-temperatursensor installeras, om det är en dedikerad server Azure ATP fristående sensorn har installerats. 
    
    För en fristående sensor Azure ATP exempelvis visas följande skärm så att du vet att en Azure ATP fristående sensor är installerad på en dedikerad server:
    
    ![Azure ATP fristående sensor installation](media/sensor-install-deployment-type.png)

    Klicka på **Nästa**.

    > [!NOTE] 
    > Om domänkontrollanten eller dedicerad server inte uppfyller minimikraven för installationen, visas ett varningsmeddelande. Detta förhindrar inte att du klickar på **Nästa** och fortsätter med installationen. Det kan vara rätt alternativ för installation av Azure ATP i små testa labbmiljö där du inte behöver lika mycket utrymme för lagring av data. För produktionsmiljöer, rekommenderas att arbeta med Azure ATP [kapacitetsplanering](atp-capacity-planning.md) guide för att se till att dina domänkontrollanter eller dedikerade servrar uppfyller de nödvändiga kraven.

4.  Under **Konfigurera sensorn**, ange installationssökvägen och åtkomstnyckel som du kopierade i föregående steg, baserat på miljön:

    ![Azure ATP fristående-bild för konfiguration av sensor](media/sensor-install-config.png)

      - Installationssökväg: Detta är den plats där Azure ATP fristående sensor är installerat. Som standard är detta %programfiles%\Azure Advanced Threat Protection sensor. Lämna standardvärdet.

      - Åtkomstnyckel: Denna hämtas från arbetsytan portalen i föregående steg.
    
5. Klicka på **Installera**. Följande komponenter installeras och konfigureras under installationen av Azure ATP-sensor:

    -   KB 3047154 (endast för Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installera inte KB 3047154 på en virtualiseringsvärd (värden som kör virtualiseringen, det går bra att köra den på en virtuell dator). Det kan leda till att portspegling slutar fungera ordentligt. 
        > -   Om Wireshark är installerad på den ATP sensor datorn när du har kört Wireshark som du måste starta om ATP-sensor eftersom den använder samma drivrutiner.

    -   Tjänsten för Azure ATP sensor och Azure ATP sensor uppdateringstjänsten
    -   Microsoft Visual C++ 2013 Redistributable

5.  När installationen är klar klickar du på **starta** att öppna webbläsaren och logga in på Azure ATP arbetsytan portalen.


>[!div class="step-by-step"]
[« Steg 3](install-atp-step3.md)
[Steg 5 »](install-atp-step5.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)

- [Konfigurera händelseinsamling](configure-event-collection.md)

- [Krav för Azure ATP](atp-prerequisites.md)

- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)