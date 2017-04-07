---
title: Installera Advanced Threat Analytics steg 2 | Microsoft Docs
description: "I steg två av ATA-installationen får du hjälp att konfigurera domänanslutningsinställningarna på ATA Center-servern"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fea114b062a7861ac284b4bf746fff68c5c1bd52
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-2"></a>Installera ATA – Steg 2

>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Steg 2. Ange ett användarnamn och lösenord för att ansluta till Active Directory-skogen

Första gången du öppnar ATA-konsolen visas följande skärmbild:

![ATA - välkommen, steg 1](media/ATA_1.7-welcome-provide-username.png)

1.  Ange följande information och klicka på **Spara**:

    |Fält|Kommentar|
    |---------|------------|
    |**Användarnamn** (krävs)|Ange det skrivskyddade användarnamnet, till exempel: **ATA-användare**.|
    |**Lösenord** (krävs)|Ange lösenordet för den skrivskyddade användaren, till exempel: **Penna1**.|
    |**Domän** (krävs)|Ange domänen för den skrivskyddade användaren, till exempel: **contoso.com**. **Obs:** Det är viktigt att du anger det fullständiga FQDN för domänen där användaren finns. Om användarens konto exempelvis finns i domänen corp.contoso.com måste du ange `corp.contoso.com`, inte contoso.com|

2. Alternativt kan du klicka på **Testa anslutning** för att testa anslutningen till domänen och kontrollera att autentiseringsuppgifterna som du fått ger åtkomst. Detta fungerar endast om ATA Center kan ansluta till domänen.     

    Välkomstmeddelandet i konsolen ändras till följande när det sparats: ![ATA – välkommen, steg 1 slutfört](media/ATA_1.7-welcome-provide-username-finished.png)

3. I administratörskonsolen, klicka på **Hämta Gateway-installationen och installera den första gatewayen** för att fortsätta.


>[!div class="step-by-step"]
[« Steg 1](install-ata-step1.md)
[Steg 3 »](install-ata-step3.md)


## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
