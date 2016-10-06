---
title: Installera ATA | Microsoft ATA
description: "I det sista ATA-installationssteget konfigurerar du Honeytoken-användaren."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 9ee2f36d8f0b7eae061873e8735139ccc4da00d1


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Installera ATA – Steg 6

>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)

## Steg 6. Konfigurera undantag för IP-adress och Honeytoken-användare
ATA aktiverar uteslutning av IP-adresser och IP-undernät från två typer av identifieringar: **DNS-rekognosering** och **Pass-the-Ticket**. 

Till exempel kan ett **DNS-rekognoseringsundantag** vara en säkerhetsskanner som använder DNS som en skanningsmekanism. Undantaget hjälper ATA att ignorera dessa skannrar. Ett exempel på ett *Pass-the-Ticket*-undantag är en NAT-enhet.    

ATA möjliggör också konfiguration av en Honeytoken-användare som används som en fälla för skadliga aktörer – all verifiering som är associerade med kontot (normalt vilande) ska utlösa en avisering.

Följ de här stegen när du ska konfigurera ovan nämnda:

1.  I ATA-konsolen klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Konfigurationsinställningar för ATA](media/ATA-config-icon.JPG)

2.  Under **Identifieringsundantag**, anger du följande för IP-adresser för antingen *DNS-rekognosering* eller *Pass-the-Ticket*. Använda CIDR-format, till exempel:  `192.168.1.0/24` och klicka på *plus*-tecknet.

    ![Spara ändringar](media/ATA-exclusions.png)

3.  Under **Identifieringsinställningar**, ange Honeytoken-kontots SID:er och klicka på plustecknet. Till exempel: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Konfigurationsinställningar för ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Om du vill hitta SID för en användare söker du efter användaren i ATA-konsolen och klickar sedan på fliken **Kontoinformation**. 

4.  Klicka på **Spara**.


Gratulerar, Microsoft Advanced Threat Analytics har distribuerats!

På tidslinjen för attacker kan du visa identifierade misstänkta aktiviteter och söka efter användare eller datorer och visa deras profiler.

ATA startar sökning efter misstänkta aktiviteter omedelbart. En del aktiviteter, t.ex. vissa av aktiviteterna för misstänkt beteende, är inte tillgängliga förrän ATA har fått tid att skapa beteendeprofiler (minst tre veckor).


>[!div class="step-by-step"]
[« Steg 5](install-ata-step5.md)


## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Sep16_HO4-->


