---
title: Installera ATA | Microsoft Advanced Threat Analytics
description: "I det sista steget i ATA-installationen konfigurerar du undernäten med kortsiktiga lån och honeytokenanvändaren."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 76305bc5f55e956c787fe3e8bd954a56f40fc56f


---

# Installera ATA – Steg 6

>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)

## Steg 6. Konfigurera undernät med kortsiktiga lån och honeytokenanvändare
Undernät med kortsiktiga lån är undernät där tilldelningen av IP-adresser ändras mycket snabbt – inom några sekunder eller minuter. Till exempel IP-adresser som används för VPN och IP-adresser i Wi-Fi. Ange listan med undernät med kortsiktiga lån som används i organisationen enligt följande:

1.  Från ATA-konsolen på ATA Gateway-datorn klickar du på ikonen för inställningar och väljer **Konfiguration**.

    ![Konfigurationsinställningar för ATA](media/ATA-config-icon.JPG)

2.  Under **Identifiering** anger du följande för undernät med kortsiktiga lån. Ange undernäten med kortsiktiga lån med snedstrecksnotation, till exempel `192.168.0.0/24`, och klicka på plustecknet.

3.  Som SID för honeytokenkontot anger du SID för det användarkonto som inte kommer att ha någon nätverksaktivitet och klickar på plustecknet. Till exempel: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Om du vill hitta SID för en användare söker du efter användaren i ATA-konsolen och klickar sedan på fliken **Kontoinformation**. 

4.  Konfigurera undantag: Du kan konfigurera IP-adresser som ska undantas från specifika misstänkta aktiviteter. Mer information finns i [Arbeta med identifieringsinställningar i ATA](working-with-detection-settings.md).

5.  Klicka på **Spara**.

![Spara ändringar](media/ATA-VPN-Subnets.JPG)

Gratulerar, Microsoft Advanced Threat Analytics har distribuerats!

På tidslinjen för attacker kan du visa identifierade misstänkta aktiviteter och söka efter användare eller datorer och visa deras profiler.

ATA startar sökning efter misstänkta aktiviteter omedelbart. En del aktiviteter, t.ex. vissa av aktiviteterna för misstänkt beteende, är inte tillgängliga förrän ATA har fått tid att skapa beteendeprofiler (minst tre veckor).


>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)


## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


