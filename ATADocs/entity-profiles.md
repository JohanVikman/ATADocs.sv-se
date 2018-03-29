---
title: Arbeta med entitetsprofiler i konsolen Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du undersöker entiteter från skärmen användaren profiler i ATA-konsolen
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f2fd6f28eb6bf11aa3705f5320fcdae01d02f6d0
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/28/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="investigating-entity-profiles"></a>Undersöka entitetsprofiler

Entitetsprofilen ger dig en instrumentpanel för fullständig djupdykning undersökning av användare, datorer, enheter och resurser som de har åtkomst till och deras historik. Profilsidan drar nytta av den nya logiska aktivitet konverterare för ATA som kan titta på en grupp av aktiviteter som inträffar (tillsammans upp till en minut) och gruppera dem i en enskild logisk aktivitet att ge en bättre förståelse för de faktiska aktiviteterna för din användare.

Klicka på namnet på enheten, till exempel ett användarnamn i tidslinjen misstänkt aktivitet för att komma åt en entitet profilsida.

Du får alla Active Directory-informationen finns på enhet - e-postadress, domän, första datumet som visas i den vänstra menyn. Om entiteten är känsligt den får du veta varför. Till exempel märks användaren med känslig eller medlem i en känsliga grupp?
Om det är en känsliga användare ser ikonen under användarens namn.

## <a name="view-entity-activities"></a>Visa entitet aktiviteter

Att visa alla aktiviteter som utförs av användaren eller utförs på en enhet, klicka på den **aktiviteter** fliken. 

 ![profilen användaraktiviteter](media/user-profile-activities.png)

Som standard visar huvudfönster entitetsprofilen en tidslinje för entitetens aktiviteter med en historik över upp till 6 månader tillbaka, där du kan också detaljnivån i enheter som nås av användaren eller för enheter, användare som kan komma åt enheten.

Du kan visa sammanfattning paneler som ger en snabb överblick över vad du behöver förstå i korthet om entiteten överst. Dessa paneler ändras beroende på vilken typ av enhet är för en användare visas:
- Hur många öppna misstänkta aktiviteter som finns för användaren
- Hur många datorer som användaren loggar in
- Hur många resurser som användaren används
- Från vilka platser som användaren loggat in VPN

  ![entitet-menyn](media/entity-menu.png)

För datorer som kan du se:
- Hur många öppna misstänkta aktiviteter som finns för datorn
- Hur många användare är inloggad på datorn
- Hur många resurser som används av datorn
- Hur många platser VPN öppnade från på datorn
- En lista som IP-adresser och datorn har använt

  ![entiteten menyn dator](media/entity-computer.png)

Med hjälp av den **filtrera efter** knappen ovanför tidslinjen aktivitet kan du filtrera aktiviteter efter aktivitetstyp. Du kan också filtrera ut en specifik (störningar) typ av aktivitet. Detta är mycket användbart för undersökning när du vill förstå grunderna för en entitet gör i nätverket. Du kan även gå till ett visst datum och du kan exportera aktiviteter som filtrerats till Excel. Den exporterade filen innehåller en sida för directory services-ändringar (sådant som ändrats i Active Directory för kontot) och en separat sida för aktiviteter. 

## <a name="view-directory-data"></a>Visa katalogdata

Den **katalogdata** fliken finns tillgänglig statisk information från Active Directory, inklusive användare access control Säkerhetsflaggor. ATA visar även gruppmedlemskap för användaren så att du kan se om användaren har en direkt medlemskap eller en rekursiv medlemskap. För grupper visar ATA medlemmarna i gruppen.

 ![data för användarprofiler directory](media/user-profile-dir-data.png)

I den **Användaråtkomstkontroll** avsnittet ATA tillhandahåller säkerhetsinställningar som kan behöva din attentions. Du kan se viktig flaggor om användaren, som kan användaren tryck på RETUR för att kringgå lösenordet, har användaren ett lösenord som upphör aldrig att gälla, osv. 

## <a name="view-lateral-movement-paths"></a>Visa lateral förflyttning sökvägar

Genom att klicka på den **Lateral förflyttning sökvägar** fliken som du kan visa en fullständigt dynamiska och klickbar karta som ger dig en bild av lateral förflyttning sökvägar till och från den här användaren som kan användas för att infiltrera nätverket.

Kartan ger dig en lista över hur många routerhopp mellan datorer eller användare en angripare skulle ha till och från den här användaren att angripa känsligt konto, och om användaren själva har känsligt konto, ser du hur många resurser och konton som direkt ansluten. Mer information finns i [Lateral förflyttning sökvägar](use-case-lateral-movement-path.md). 

 ![sökvägar för användarens profil lateral förflyttning](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
