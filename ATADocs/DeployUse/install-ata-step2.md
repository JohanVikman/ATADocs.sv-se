---
title: "Installera ATA – Steg 2 | Microsoft Advanced Threat Analytics"
description: "I steg två av ATA-installationen får du hjälp att konfigurera domänanslutningsinställningarna på ATA Center-servern"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 73e2eb84e1e21cbc5afcb7a100f9a67da63c66a5


---

# Installera ATA – Steg 2

>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)

## Steg 2. Konfigurera allmänna inställningar för ATA Gateway
Inställningarna på inställningsfliken **Allmänt** gäller för alla ATA-gatewayer som hanteras av ATA Center.

Gör så här för att konfigurera allmänna inställningar för ATA Gateway:

1.  Öppna ATA-konsolen och logga in. Instruktioner finns i [Arbeta med ATA-konsolen](working-with-ata-console.md).

2.  Klicka på inställningsikonen och välj **Konfiguration**.

    ![Konfigurationsinställningar för ATA Gateway](media/ATA-config-icon.JPG)

3.  På fliken **Allmänt** anger du följande information under **ATA Gateways** och klickar på **Spara**.

    |Fält|Kommentar|
    |---------|------------|
    |**Användarnamn** (krävs)|Ange det skrivskyddade användarnamnet, till exempel: **användare1**.|
    |**Lösenord** (krävs)|Ange lösenordet för den skrivskyddade användaren, till exempel: **Penna1**. **Obs:** Kontrollera att lösenordet är korrekt. Om du sparar fel lösenord stoppas ATA-tjänsten på ATA Gateway-servrarna.|
    |**Domän** (krävs)|Ange domänen för den skrivskyddade användaren, till exempel: **contoso.com**. **Obs:** Det är viktigt att du anger det fullständiga FQDN för domänen där användaren finns. Om användarens konto exempelvis finns i domänen corp.contoso.com måste du ange `corp.contoso.com`, inte contoso.com|
    |Uppdatera alla ATA-gatewayer automatiskt |Om du aktiverar den här inställningen kommer alla ATA-gatewayer att uppdateras automatiskt vid kommande versioner när du uppdaterar ATA Center.|

    ![Bild av domänanslutningsinställningar för ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)


## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jun16_HO4-->


