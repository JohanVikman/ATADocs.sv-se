---
title: Förstå Advanced Threat Analytics-konsolen | Microsoft Docs
description: Beskriver hur man loggar in på ATA-konsolen och konsolens komponenter
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2ecffce7d692a9f1ecea8d8c5220ce3b2dbf848e
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009861"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="working-with-the-ata-console"></a>Arbeta med ATA-konsolen

Använd ATA-konsolen för att övervaka och svara på misstänkt aktivitet som identifieras av ATA.

Att skriva den `?` nyckeln innehåller kortkommandon för hjälpmedel för ATA-portalen. 

## <a name="enabling-access-to-the-ata-console"></a>Aktivera åtkomst till ATA-konsolen
Om du vill logga in till ATA-konsolen, måste du logga in med en användare som har tilldelats rollen rätt ATA för att komma åt ATA-konsolen. Mer information om rollbaserad åtkomstkontroll (RBAC) i ATA finns [arbeta med ATA rollgrupper](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Logga in på ATA-konsolen

>[!NOTE]
 > Från och med ATA 1.8 sker inloggningen till ATA-konsolen med hjälp av enkel inloggning.

1. I ATA Center-servern klickar du på ikonen **Microsoft ATA Console** på skrivbordet och bläddrar till ATA-konsolen.

    ![ATA-serverikon](media/ata-server-icon.png)

 >[!NOTE]
 > Du kan även öppna en webbläsare från antingen ATA Center eller ATA Gateway och bläddra till den IP-adress du har konfigurerat i ATA Center-installationen för ATA-konsolen.    

2.  Om datorn där ATA Center är installerat och den dator som du försöker komma åt ATA-konsolen som både domänen ansluten ATA har stöd för enkel inloggning integrerad med Windows-autentisering - om du redan har loggat in på datorn, ATA använder den token som används för att logga in på ATA-konsolen. Du kan också logga in med ett smartkort. Din behörighet i ATA motsvarar dina [administratörsroll](ata-role-groups.md).

 > [!NOTE]
 > Se till att logga in på datorn som du vill komma åt ATA-konsolen med ATA admin användarnamn och lösenord. Du kan också köra webbläsaren som en annan användare eller logga ut från Windows och logga in med ditt administratörsanvändarnamn för ATA. Om du vill fråga ATA-konsolen för att fråga om autentiseringsuppgifter, åtkomst till konsolen med en IP uppmanas-adress och du att ange autentiseringsuppgifter.

3. Kontrollera att platsen för ATA-konsolen har definierats som en lokal intranätplats i webbläsaren och att du åtkomst till den med hjälp av en kort filnamn eller en localhost för att logga in med enkel inloggning.

> [!NOTE]
> Förutom att logga varje avisering om misstänkt aktivitet och hälsorelaterade problem, loggas varje konfigurationsändring som du gör i ATA-konsolen i Windows-händelseloggen på ATA Center-datorn i **loggen för program och tjänster** och sedan **Microsoft ATA**. Alla inloggningar till ATA-konsolen loggas också.<br></br>  All konfiguration som påverkar ATA Gateway loggas också i Windows-händelseloggen på ATA Gateway-datorn. 



## <a name="the-ata-console"></a>ATA-konsolen

ATA-konsolen ger en snabb överblick över alla misstänkta aktiviteter i kronologisk ordning. Den gör det möjligt att visa detaljer om alla aktiviteter och utföra åtgärder baserat på dessa aktiviteter. Konsolen visar även meddelanden och aviseringar som belyser problem med ATA-nätverket eller nya aktiviteter som bedöms som misstänkta.

Dessa är de viktigaste objekten i ATA-konsolen.


### <a name="attack-time-line"></a>Tidslinje för attacker

Det här är den standardsida du kommer till när du loggar in på ATA-konsolen. Som standard visas alla öppna misstänkta aktiviteter på tidslinjen för attacker. Du kan filtrera tidslinjen för att visa alla, öppna, avvisade eller Suppressed misstänkta aktiviteter. Du kan också se allvarlighetsgrad som har tilldelats till varje aktivitet.

![Bild för tidslinje för attacker i ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Mer information finns i [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Meddelandefält

När en ny misstänkt aktivitet identifieras öppnas meddelandefältet automatiskt till höger. Om det finns nya misstänkta aktiviteter sedan den senaste gången du loggade in öppnas meddelandefältet när du har loggat in. Du kan klicka på pilen till höger när som helst för att öppna meddelandefältet.

![Bild för meddelandefält i ATA](media/notification-bar-1.7.png)

### <a name="whats-new"></a>Nyheter

När en ny version av ATA släpps, den **nyheter** visas i övre högra så att du vet vad har lagts till i den senaste versionen. Det ger dig också med en länk till version hämtningen.

### <a name="filtering-panel"></a>Filtreringspanel

Du kan filtrera vilka misstänkta aktiviteter som visas i tidslinjen för attacker eller som visas på entitetsprofilens flik för misstänkta aktiviteter baserat på status och allvarlighetsgrad.

### <a name="search-bar"></a>Sökfält

Du kan hitta ett sökfält i den översta menyn. Du kan söka efter en viss användare, dator eller grupp i ATA. Om du vill prova är det bara att börja skriva.

![Bild för sökning i ATA-konsolen](media/ATA-console-search.png)

### <a name="health-center"></a>Health Center

Health Center visar aviseringar om något inte fungerar korrekt i ATA-distributionen.

![Bild för ATA health center](media/ATA-Health-Issue.jpg)

Varje gång systemet upptäcker ett problem, till exempel ett anslutningsfel eller en frånkopplad ATA-Gateway med hjälp av ikonen för Health Center får du reda på genom att visa en röd punkt. ![Bild med röd punkt för ATA health center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="sensitive-groups"></a>Känsliga grupper

Följande lista med grupper betraktas som **känsliga** av ATA. En entitet som är medlem i dessa grupper betraktas som känslig:

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


### <a name="mini-profile"></a>Miniprofil

Om du håller muspekaren över en entitet, var som helst i konsolen där det finns en enda entitet presenteras, t.ex en användare eller en dator, öppnas en miniprofil automatiskt visar följande information om de är tillgängliga:

![Bild för miniprofil i ATA](media/ATA-mini-profile.jpg)

-   Namn

-   Bild

-   E-post

-   Telefon

-   Antal misstänkta aktiviteter efter allvarlighetsgrad



## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
