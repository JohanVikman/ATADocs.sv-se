---
title: "Förstå Advanced Threat Analytics-konsolen | Microsoft Docs"
description: "Beskriver hur man loggar in på ATA-konsolen och konsolens komponenter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d687087dd9e1ae7f7642f9fdd7d89420f3bec27
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# Arbeta med ATA-konsolen
<a id="working-with-the-ata-console" class="xliff"></a>

Använd ATA-konsolen för att övervaka och svara på misstänkt aktivitet som identifieras av ATA.

Om du skriver ? visas tangentbordsgenvägar för ATA-portalens hjälpmedelsfunktioner. 

## Aktivera åtkomst till ATA-konsolen
<a id="enabling-access-to-the-ata-console" class="xliff"></a>
För att kunna logga in på ATA-konsolen måste du logga in med en användare som har tilldelats rätt ATA-roll för att komma åt ATA-konsolen. Mer information om rollbaserad åtkomstkontroll (RBAC) i ATA finns i [Arbeta med ATA-rollgrupper](ata-role-groups.md).

## Logga in på ATA-konsolen
<a id="logging-into-the-ata-console" class="xliff"></a>

1. I ATA Center-servern klickar du på ikonen **Microsoft ATA Console** på skrivbordet och bläddrar till ATA-konsolen.

    ![ATA-serverikon](media/ata-server-icon.png)

>[!NOTE]
> Du kan även öppna en webbläsare från antingen ATA Center eller ATA Gateway och bläddra till den IP-adress du har konfigurerat i ATA Center-installationen för ATA-konsolen.    

2.  Om både den dator som ATA Center är installerat på och den dator som du försöker komma åt ATA-konsolen från är domänanslutna har ATA stöd för enkel inloggning integrerat med Windows-autentisering – om du redan har loggat in på datorn använder ATA den token för att logga in dig till ATA-konsolen. Du kan också logga in med ett smartkort. Dina behörigheter i ATA motsvarar din [administratörsroll](ata-role-groups.md).

> [!NOTE]
> Var noga med att logga in på datorn som du vill komma åt ATA-konsolen från med ditt administratörsanvändarnamn och ditt administratörslösenord för ATA. Du kan också köra webbläsaren som en annan användare eller logga ut från Windows och logga in med ditt administratörsanvändarnamn för ATA. Om du vill att ATA Console ska uppmana dig att ange dina autentiseringsuppgifter ansluter du till konsolen med hjälp av en IP-adress, så uppmanas du att ange autentiseringsuppgifter.

Om du vill logga in med enkel inloggning kontrollerar du att ATA-konsolen har definierats som en lokal intranätplats i webbläsaren och ansluter till konsolen med ett kortnamn eller en localhost.

> [!NOTE]
> Förutom att logga varje avisering om misstänkt aktivitet och hälsorelaterade problem, loggas varje konfigurationsändring som du gör i ATA-konsolen i Windows-händelseloggen på ATA Center-datorn i **loggen för program och tjänster** och sedan **Microsoft ATA**. Alla inloggningar till ATA-konsolen loggas också.<br></br>  All konfiguration som påverkar ATA Gateway loggas också i Windows-händelseloggen på ATA Gateway-datorn. 



## ATA-konsolen
<a id="the-ata-console" class="xliff"></a>

ATA-konsolen ger en snabb överblick över alla misstänkta aktiviteter i kronologisk ordning. Den gör det möjligt att visa detaljer om alla aktiviteter och utföra åtgärder baserat på dessa aktiviteter. Konsolen visar även meddelanden och aviseringar som belyser problem med ATA-nätverket eller nya aktiviteter som bedöms som misstänkta.

Dessa är de viktigaste objekten i ATA-konsolen.


### Tidslinje för attacker
<a id="attack-time-line" class="xliff"></a>

Det här är den standardsida du kommer till när du loggar in på ATA-konsolen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan filtrera tidslinjen för attacker för att visa alla, öppna, avvisade eller lösta misstänkta aktiviteter. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet.

![Bild för tidslinje för attacker i ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Mer information finns i [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).

### Meddelandefält
<a id="notification-bar" class="xliff"></a>

När en ny misstänkt aktivitet identifieras öppnas meddelandefältet automatiskt till höger. Om det finns nya misstänkta aktiviteter sedan den senaste gången du loggade in öppnas meddelandefältet när du har loggat in. Du kan klicka på pilen till höger när som helst för att öppna meddelandefältet.

![Bild för meddelandefält i ATA](media/notification-bar-1.7.png)

### Filtreringspanel
<a id="filtering-panel" class="xliff"></a>

Du kan filtrera vilka misstänkta aktiviteter som visas i tidslinjen för attacker eller som visas på entitetsprofilens flik för misstänkta aktiviteter baserat på status och allvarlighetsgrad.

### Sökfält
<a id="search-bar" class="xliff"></a>

Det finns ett sökfält i den översta menyn. Du kan söka efter en viss användare, dator eller grupp i ATA. Om du vill prova är det bara att börja skriva.

![Bild för sökning i ATA-konsolen](media/ATA-console-search.png)

### Health Center
<a id="health-center" class="xliff"></a>

Health Center visar aviseringar om något inte fungerar korrekt i ATA-distributionen.

![Bild för ATA health center](media/ATA-Health-Issue.jpg)

Om systemet upptäcker ett problem, t.ex. ett anslutningsfel eller en frånkopplad ATA Gateway, meddelar ikonen för Health Center detta genom att visa en röd punkt. ![Bild med röd punkt för ATA health center](media/ATA-Health-Center-Alert-red-dot.png)

Health Center-aviseringar kan avvisas eller lösas och de kategoriseras som Hög, Medel eller Låg beroende på deras allvarlighetsgrad. Om du löser en avisering som ATA-tjänsten identifierar som fortfarande aktiv flyttas den automatiskt till listan med öppna aviseringar. Om systemet upptäcker att det inte längre finns någon orsak till en avisering (situationen har åtgärdats) flyttas den automatiskt till listan med lösta aviseringar.

### Användar- och datorprofiler
<a id="user-and-computer-profiles" class="xliff"></a>

ATA skapar en profil för alla användare och datorer i nätverket. I användarprofilen visar ATA allmän information, t.ex. gruppmedlemskap, senaste inloggningar och resurser som har använts nyligen. Den innehåller också en lista med platser där användaren har anslutit via VPN. En lista över gruppmedlemskap som ATA betraktar som känsliga finns nedan.

![Användarprofil](media/user-profile.png)

I datorprofilen visar ATA allmän information, t.ex. de senaste inloggningarna och resurser som har använts nyligen.

![Datorprofil](media/computer-profile.png)

ATA tillhandahåller ytterligare information om entiteter (datorer, enheter, användare) på följande sidor: Sammanfattning, Aktiviteter och Misstänkta aktiviteter.

En profil som ATA inte har kunnat lösa helt visas med en halvfull cirkelformad ikon.


![Bild för olöst profil i ATA](media/ATA-Unresolved-Profile.jpg)

### Känsliga grupper
<a id="sensitive-groups" class="xliff"></a>

Följande lista med grupper betraktas som **känsliga** av ATA. Dessa är grupper som flaggas som grupper med administrativa privilegier och genererar aviseringar för känsliga konton:

- Skrivskyddade företagsdomänkontrollanter 
- Domänadministratörer 
- Domänkontrollanter 
- Schemaadministratörer
- Företagsadministratörer 
- Skapare och ägare av grupprincip 
- Skrivskyddade domänkontrollanter 
- Administratörer  
- Privilegierade användare  
- Kontoansvariga  
- Serveransvariga   
- Skrivaransvariga
- Ansvariga för säkerhetskopiering
- Ansvariga för replikering 
- Användare av fjärrskrivbord 
- Ansvariga för nätverkskonfigurering 
- Incoming Forest Trust Builders 
- DNS-administratörer 


### Miniprofil
<a id="mini-profile" class="xliff"></a>

Var som helst i konsolen där en enda entitet presenteras, t.ex. en användare eller dator, kan du placera pekaren över entiteten så öppnas en miniprofil automatiskt som visar följande information, om tillgängligt:

![Bild för miniprofil i ATA](media/ATA-mini-profile.jpg)

-   Namn

-   Bild

-   E-post

-   Telefon

-   Antal misstänkta aktiviteter efter allvarlighetsgrad



## Se även
<a id="see-also" class="xliff"></a>
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
