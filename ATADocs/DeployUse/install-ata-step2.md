---
title: "Installera ATA – Steg 2 | Microsoft ATA"
description: "I steg två av ATA-installationen får du hjälp att konfigurera domänanslutningsinställningarna på ATA Center-servern"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: fc268bcb2e3d027b09fa3349427934f60783b971


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Installera ATA – Steg 2

>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)

## Steg 2. Ange ett användarnamn och lösenord för att ansluta till Active Directory-skogen

Första gången du öppnar ATA-konsolen visas följande skärmbild:

![ATA - välkommen, steg 1](media/ATA_1.7-welcome-provide-username.png)

1.  Ange följande information och klicka på **Spara**:

    |Fält|Kommentar|
    |---------|------------|
    |**Användarnamn** (krävs)|Ange det skrivskyddade användarnamnet, till exempel: **ATA-användare**.|
    |**Lösenord** (krävs)|Ange lösenordet för den skrivskyddade användaren, till exempel: **Penna1**.|
    |**Domän** (krävs)|Ange domänen för den skrivskyddade användaren, till exempel: **contoso.com**. **Obs:** Det är viktigt att du anger det fullständiga FQDN för domänen där användaren finns. Om användarens konto exempelvis finns i domänen corp.contoso.com måste du ange `corp.contoso.com`, inte contoso.com|
    |Uppdatera alla ATA-gatewayer automatiskt |Om du aktiverar den här inställningen kommer alla ATA-gatewayer att uppdateras automatiskt vid kommande versioner när du uppdaterar ATA Center.|

    Välkomstmeddelandet i konsolen ändras till följande när det sparats: ![ATA - välkommen, steg 1 slutfört](media/ATA_1.7-welcome-provide-username-finished.png)

2. I administratörskonsolen, klicka på **Hämta Gateway-installationen och installera den första gatewayen** för att fortsätta.


>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)


## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Aug16_HO5-->


