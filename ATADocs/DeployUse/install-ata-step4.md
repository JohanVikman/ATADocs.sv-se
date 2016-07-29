---
title: "Installera ATA – Steg 4 | Microsoft ATA"
description: "I steg fyra av ATA-installationen får du hjälp att installera ATA Gateway."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 6052a911c12f8dbb757ab8445f9e0c6ec09b530e


---

# Installera ATA – Steg 4

>[!div class="step-by-step"]
[« Steg 3](install-ata-step3.md)
[Steg 5 »](install-ata-step5.md)

## Steg 4. Installera ATA Gateway

Innan du installerar ATA Gateway på en dedikerad server ska du kontrollera att portspegling är korrekt konfigurerad och att ATA-gatewayen kan se trafik till och från domänkontrollanterna. Mer information finns i [Verifiera portspegling](validate-port-mirroring.md).


> [!IMPORTANT]
> Kontrollera att [KB2919355](http://support.microsoft.com/kb/2919355/) har installerats.  Kontrollera om snabbkorrigeringen är installerad genom att köra följande PowerShell-cmdlet:
>
> `Get-HotFix -Id kb2919355`

På ATA Gateway-servern utför du följande steg.

1.  Extrahera filerna från ZIP-filen. 
> [!NOTE] 
> Installation direkt från ZIP-filen misslyckas.

2.  Kör **Microsoft ATA Gateway Setup.exe** från en upphöjd kommandotolk och följ installationsguiden.

3.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

4.  Under **ATA Gateway-konfiguration** anger du följande information baserat på miljön:

    ![Bild av ATA Gateway-konfiguration](media/ATA-Gateway-Configuration.JPG)

    |Fält|Beskrivning|Kommentar|
    |---------|---------------|------------|
    |Installationssökväg|Det här är den plats där ATA Gateway kommer att installeras. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Låt standardvärdet vara kvar|
    |SSL-certifikat för ATA Gateway-tjänsten|Det här är det certifikat som kommer att användas av ATA Gateway.|Använd bara ett självsignerat certifikat för labbmiljöer.|
    |ATA Gateway-registrering|Ange ATA-administratörens användarnamn och lösenord.|För att ATA-gatewayen ska registreras i ATA Center anger du användarnamn och lösenord för den användare som installerade ATA Center. Användaren måste vara medlem i någon av följande lokala grupper i ATA Center.<br /><br />-   Administratörer<br />-   Microsoft Advanced Threat Analytics-administratörer **Obs!** De här autentiseringsuppgifterna används enbart för registrering och lagras inte i ATA.|
    Följande komponenter installeras och konfigureras under installationen av ATA Gateway:

    -   KB 3047154

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

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO4-->


