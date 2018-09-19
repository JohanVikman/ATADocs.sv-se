---
title: Installera Advanced Threat Analytics steg 4 | Microsoft Docs
description: I steg fyra av ATA-installationen får du hjälp att installera ATA Gateway.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6f6324877ea42547d526be56ae2676f8d36cd25d
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133726"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="install-ata---step-4"></a>Installera ATA – Steg 4

>[!div class="step-by-step"]
[« Steg 3](install-ata-step3.md)
[Steg 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Steg 4. Installera ATA Gateway

Innan du installerar ATA Gateway på en dedikerad server ska du kontrollera att portspegling är korrekt konfigurerad och att ATA-gatewayen kan se trafik till och från domänkontrollanterna. Mer information finns i [verifiera portspegling](validate-port-mirroring.md).


> [!IMPORTANT]
> Kontrollera att [KB2919355](http://support.microsoft.com/kb/2919355/) har installerats.  Kontrollera om snabbkorrigeringen är installerad genom att köra följande PowerShell-cmdlet:
>
> `Get-HotFix -Id kb2919355`

På ATA Gateway-servern utför du följande steg.

1.  Extrahera filerna från ZIP-filen. 
> [!NOTE] 
> Det går inte att installera direkt från zip-filen.

2.  Kör **Microsoft ATA Gateway Setup.exe** och följ installationsguiden.

3.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

4.  Installationsguiden kontrollerar automatiskt om servern är en domänkontrollant eller en dedikerad server. Om det är en domänkontrollant, ATA Lightweight Gateway har installerats, om det är en dedikerad server, ATA Gateway har installerats. 
    
    För en ATA-Gateway visas exempelvis följande skärm så att du vet att en ATA Gateway kommer att installeras på din dedikerade server:
    
    ![ATA Gateway-installation](media/ata-gw-install.png) Klicka på **Nästa**.

    > [!NOTE] 
    > Om domänkontrollanten eller dedikerad server inte uppfyller de lägsta maskinvarukraven för installation, får du en varning. Detta förhindrar inte att du klickar på **Nästa** och fortsätter med installationen. Det kan vara rätt alternativ för installation av ATA i en liten labbtestmiljö där du inte behöver lika mycket utrymme för lagring av data. I produktionsmiljöer, rekommenderas det att arbeta med ATA:s guide för [kapacitetsplanering](ata-capacity-planning.md) för att se till att dina domänkontrollanter eller dedikerade servrar uppfyller de nödvändiga kraven.

4.  Under **Configure the Gateway** (Konfigurera gatewayen) anger du följande information baserat på din miljö:

    ![Bild av ATA Gateway-konfiguration](media/ata-gw-configure.png)

    > [!NOTE]
    > När du distribuerar ATA Gateway, behöver du inte ange autentiseringsuppgifter. Om installationen av ATA Gateway inte kan hämta dina autentiseringsuppgifter med hjälp av enkel inloggning (t.ex, det kan hända om ATA Center inte är i domänen, om ATA Gateway inte är i domänen, har du inte administratörsautentiseringsuppgifter för ATA), uppmanas du att ange autentiseringsuppgifter, som i följande skärmbild: 

  ![Ange autentiseringsuppgifter för ATA gateway](media/ata-install-credentials.png)

   - Installationssökväg: Det här är den plats där ATA Gateway är installerad. Som standard är sökvägen %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Lämna standardvärdet.
    
5. Klicka på **Installera**. Följande komponenter installeras och konfigureras under installationen av ATA Gateway:

    -   KB 3047154 (endast för Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installera inte KB 3047154 på en virtualiseringsvärd (värden som kör virtualiseringen, det går bra att köra den på en virtuell dator). Det kan leda till att portspegling slutar fungera ordentligt. 
        > -   Installera inte Analysverktyg för meddelanden, Wireshark eller någon annan programvara för nätverksavbildning på ATA Gateway. Om du behöver avbilda nätverkstrafik installerar och använder du Microsoft Network Monitor 3.4.

    -   ATA Gateway-tjänst
    -   Microsoft Visual C++ 2013 Redistributable
    -   Anpassad datasamlingsuppsättning för Prestandaövervakaren

5.  Gör så här när installationen är klar: för ATA Gateway klickar du på **Starta** för att öppna webbläsaren och logga in på ATA-konsolen, för ATA Lightweight Gateway klickar du på **Avsluta**.


>[!div class="step-by-step"]
[« Steg 3](install-ata-step3.md)
[Steg 5 »](install-ata-step5.md)


## <a name="related-videos"></a>Relaterade videor
- [Översikt över ATA-distribution](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Välja rätt typ av ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Se även
- [ATA POC-Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

