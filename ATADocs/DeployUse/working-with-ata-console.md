---
title: Arbeta med ATA-konsolen | Microsoft ATA
description: "Beskriver hur man loggar in på ATA-konsolen och konsolens komponenter"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a4ba68547d6746625a44aca5d05790c3ad138f4e
ms.openlocfilehash: ab9abce7479971c80544476c54cbf0911d1a5822


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Arbeta med ATA-konsolen

Använd ATA-konsolen för att övervaka och svara på misstänkt aktivitet som identifieras av ATA.

## Aktivera åtkomst till ATA-konsolen
För att kunna logga in på ATA-konsolen måste du logga in med en användare som har tilldelats rätt ATA-roll för att komma åt ATA-konsolen. Mer information om rollbaserad åtkomstkontroll (RBAC) i ATA finns i [Arbeta med ATA-rollgrupper](ata-role-groups.md).

## Logga in på ATA-konsolen

1. I ATA Center-servern klickar du på ikonen **Microsoft ATA Console** på skrivbordet och bläddrar till ATA-konsolen.

    ![ATA-serverikon](media/ata-server-icon.png)

>[!NOTE]
> Du kan även öppna en webbläsare från antingen ATA Center eller ATA Gateway och bläddra till den IP-adress du har konfigurerat i ATA Center-installationen för ATA-konsolen.    

2.  Ange ditt användarnamn och lösenord och klicka på **Logga in**.

![Bild av ATA-inloggningssidan](media/ATA-log-in-screen.png)


## ATA-konsolen

ATA-konsolen ger en snabb överblick över alla misstänkta aktiviteter i kronologisk ordning. Den gör det möjligt att visa detaljer om alla aktiviteter och utföra åtgärder baserat på dessa aktiviteter. Konsolen visar även meddelanden och aviseringar som belyser problem med ATA-nätverket eller nya aktiviteter som bedöms som misstänkta.

Dessa är de viktigaste objekten i ATA-konsolen.


### Tidslinje för attacker

Det här är den standardsida du kommer till när du loggar in på ATA-konsolen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan filtrera tidslinjen för attacker för att visa alla, öppna, avvisade eller lösta misstänkta aktiviteter. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet.

![Bild för tidslinje för attacker i ATA](media/attack-timeline-1.7.png)

Mer information finns i [Arbeta med misstänkta aktiviteter](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Meddelandefält

När en ny misstänkt aktivitet identifieras öppnas meddelandefältet automatiskt till höger. Om det finns nya misstänkta aktiviteter sedan den senaste gången du loggade in öppnas meddelandefältet när du har loggat in. Du kan klicka på pilen till höger när som helst för att öppna meddelandefältet.

![Bild för meddelandefält i ATA](media/notification-bar-1.7.png)

### Filtreringspanel

Du kan filtrera vilka misstänkta aktiviteter som visas i tidslinjen för attacker eller som visas på entitetsprofilens flik för misstänkta aktiviteter baserat på status och allvarlighetsgrad.

### Sökfält

Det finns ett sökfält i den översta menyn. Du kan söka efter en viss användare, dator eller grupp i ATA. Om du vill prova är det bara att börja skriva.

![Bild för sökning i ATA-konsolen](media/ATA-console-search.png)

### Health Center

Health Center visar aviseringar om något inte fungerar korrekt i ATA-distributionen.

![Bild för ATA health center](media/ATA-Health-Issue.jpg)

Om systemet upptäcker ett problem, t.ex. ett anslutningsfel eller en frånkopplad ATA Gateway, meddelar ikonen för Health Center detta genom att visa en röd punkt. ![Bild med röd punkt för ATA health center](media/ATA-Health-Center-Alert-red-dot.png)

Health Center-aviseringar kan avvisas eller lösas och de kategoriseras som Hög, Medel eller Låg beroende på deras allvarlighetsgrad. Om du löser en avisering som ATA-tjänsten identifierar som fortfarande aktiv flyttas den automatiskt till listan med öppna aviseringar. Om systemet upptäcker att det inte längre finns någon orsak till en avisering (situationen har åtgärdats) flyttas den automatiskt till listan med lösta aviseringar.

### Användar- och datorprofiler

ATA skapar en profil för alla användare och datorer i nätverket. I användarprofilen visar ATA allmän information, t.ex. gruppmedlemskap, senaste inloggningar och resurser som har använts nyligen.

![Användarprofil](media/user-profile.png)

I datorprofilen visar ATA allmän information, t.ex. senaste inloggningar och resurser som har använts nyligen.

![Datorprofil](media/computer-profile.png)

ATA tillhandahåller ytterligare information om entiteter (datorer, enheter, användare) på följande sidor: Sammanfattning, Aktiviteter och Misstänkta aktiviteter.

En profil som ATA inte har kunnat lösa helt visas med en halvfull cirkelformad ikon.


![Bild för olöst profil i ATA](media/ATA-Unresolved-Profile.jpg)

### Miniprofil

Var som helst i konsolen där en enda entitet presenteras, t.ex. en användare eller dator, kan du placera pekaren över entiteten så öppnas en miniprofil automatiskt som visar följande information, om tillgängligt:

![Bild för miniprofil i ATA](media/ATA-mini-profile.jpg)

-   Namn

-   Bild

-   E-post

-   Telefon

-   Antal misstänkta aktiviteter efter allvarlighetsgrad



## Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


