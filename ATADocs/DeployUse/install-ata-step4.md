---
title: Installera Advanced Threat Analytics steg 4 | Microsoft Docs
description: "I steg fyra av ATA-installationen får du hjälp att installera ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 9b5891f4e864dcd7bfa8c5cc5ba6d9977806e033


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-4"></a>Installera ATA – Steg 4

>[!div class="step-by-step"]
[« Steg 3](install-ata-step3.md)
[Steg 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Steg 4. Installera ATA Gateway

Innan du installerar ATA Gateway på en dedikerad server ska du kontrollera att portspegling är korrekt konfigurerad och att ATA-gatewayen kan se trafik till och från domänkontrollanterna. Mer information finns i [Verifiera portspegling](validate-port-mirroring.md).


> [!IMPORTANT]
> Kontrollera att [KB2919355](http://support.microsoft.com/kb/2919355/) har installerats.  Kontrollera om snabbkorrigeringen är installerad genom att köra följande PowerShell-cmdlet:
>
> `Get-HotFix -Id kb2919355`

På ATA Gateway-servern utför du följande steg.

1.  Extrahera filerna från ZIP-filen. 
> [!NOTE] 
> Installation direkt från ZIP-filen misslyckas.

2.  Kör **Microsoft ATA Gateway Setup.exe** och följ installationsguiden.

3.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

4.  Installationsguiden kommer automatiskt att kontrollera om servern är en domänkontrollant eller en dedikerad server. Om den är en domänkontrollant kommer ATA Lightweight Gateway att installeras, om det är en dedikerad server, kommer ATA Gateway att installeras. 
    
    Till exempel vid en ATA Lightweight Gateway, visas följande skärmbild så att du vet att en ATA Lightweight Gateway kommer att installeras på domänkontrollanten:
    
    ![Installation av ATA Lightweight Gateway](media/ATA-lightweight-gateway-install-selected.png) klicka på **Nästa**.

    > [!NOTE] 
    > Om domänkontrollanten eller dedikerad server inte uppfyller maskinvarukraven för installation, får du en varning. Detta förhindrar inte att du klickar på **Nästa** och fortsätter med installationen. Detta kan vara rätt alternativ för installation av ATA i en liten labbtestmiljö där du inte behöver lika mycket utrymme för lagring av data. I produktionsmiljöer, rekommenderas det att arbeta med ATA:s guide för [kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning) för att se till att dina domänkontrollanter eller dedikerade servrar uppfyller de nödvändiga kraven.

4.  Under **ATA Gateway-konfiguration** anger du följande information baserat på miljön:

    ![Bild av ATA Gateway-konfiguration](media/ATA-Gateway-Configuration.png)

    |Fält|Beskrivning|Kommentar|
    |---------|---------------|------------|
    |Installationssökväg|Det här är den plats där ATA Gateway kommer att installeras. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Låt standardvärdet vara kvar|
    |SSL-certifikat för Gateway-tjänsten|Det här är det certifikat som kommer att användas av ATA Gateway.|Använd bara ett självsignerat certifikat för labbmiljöer.|
    |Gateway-registrering|Ange ATA-administratörens användarnamn och lösenord.|För att ATA-gatewayen ska registreras i ATA Center anger du användarnamn och lösenord för den användare som installerade ATA Center. Användaren måste vara medlem i någon av följande lokala grupper i ATA Center.<br /><br />-   Administratörer<br />-   Microsoft Advanced Threat Analytics-administratörer **Obs!** De här autentiseringsuppgifterna används enbart för registrering och lagras inte i ATA.|
    
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

## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Feb17_HO1-->


