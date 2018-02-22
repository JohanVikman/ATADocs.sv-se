---
title: "Arbeta med användarprofiler i Azure Advanced Threat Protection arbetsytan portal | Microsoft Docs"
description: "Beskriver hur du undersöker användare från skärmen användaren profiler i Azure ATP arbetsytan portal"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6ceefeeba6a52abf5da7ff44135cff55e9beab02
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="investigating-entity-profiles"></a>Undersöka entitetsprofiler

Entitetsprofilen ger dig en omfattande entitet sida med utformade för fullständig djupdykning undersökning av användare, datorer, enheter, och de har åtkomst till resurser och deras historik. Profilsidan drar nytta av den nya logiska aktivitet konverterare för Azure ATP som kan titta på en grupp av aktiviteter som inträffar (aggregerade upp till en minut) och gruppera dem i en enskild logisk aktivitet att ge en bättre förståelse för faktiska aktiviteter dina användare.

Klicka på namnet på enheten, till exempel ett användarnamn i tidslinjen misstänkt aktivitet för att komma åt en entitet profilsida.

Du får alla Active Directory-informationen finns på enhet - e-postadress, domän, första datumet som visas i den vänstra menyn. Om entiteten är känsligt meddelar du varför. Till exempel märks användaren med känslig eller medlem i en känsliga grupp?
Om det är en känslig ikonen under användarens namn.

## <a name="view-entity-activities"></a>Visa entitet aktiviteter

Att visa alla aktiviteter som utförs av användaren eller utförs på en enhet, klicka på den **aktiviteter** fliken. 

 ![profilen användaraktiviteter](media/user-profile-activities.png)

Som standard visar huvudfönster entitetsprofilen en tidslinje för entitetens aktiviteter med en historik över upp till sex månader tillbaka, där du kan också detaljnivån i enheter som nås av användaren eller för enheter, användare som kan komma åt enheten.

Du kan visa sammanfattning paneler som ger en snabb överblick över vad du behöver förstå i korthet om entiteten - hur många datorer som användaren loggade in, hur många resurser användes och platser där användaren loggat in VPN (om konfigurerad) överst . 

Med hjälp av den **filtrera efter** knappen ovanför tidslinjen aktivitet kan du filtrera aktiviteter efter aktivitetstyp. Du kan också filtrera ut en specifik (störningar) typ av aktivitet. Detta är användbart för undersökning om du vill förstå grunderna för en entitet gör i nätverket. Du kan även gå till ett visst datum och du kan exportera aktiviteter som filtrerats till Excel. Den exporterade filen innehåller en sida för directory services-ändringar (sådant som ändrats i Active Directory för kontot) och en separat sida för aktiviteter. 

## <a name="view-directory-data"></a>Visa katalogdata

Den **katalogdata** fliken finns tillgänglig statisk information från Active Directory, inklusive användare access control Säkerhetsflaggor. Azure ATP visar även gruppmedlemskap för användaren så att du kan se om användaren har en direkt medlemskap eller en rekursiv medlemskap. För grupper visar Azure ATP medlemmarna i gruppen.

 ![data för användarprofiler directory](media/user-profile-dir-data.png)

I den **Användaråtkomstkontroll** avsnittet Azure ATP hämtar säkerhetsinställningar som kan behöva din attentions. Du kan se viktig flaggor om användaren, som kan användaren tryck på RETUR för att kringgå lösenordet, har användaren ett lösenord som upphör aldrig att gälla, osv. 

## <a name="view-lateral-movement-paths"></a>Visa lateral förflyttning sökvägar

Du kan visa en fullständigt dynamiska och klickbar karta som ger dig en bild av lateral förflyttning sökvägar till och från den här användaren som kan användas för att infiltrera nätverket genom att klicka på fliken Lateral förflyttning sökvägar.

Kartan ger dig en lista över hur många hopp mellan datorer eller användare angriparen till och från den här användaren att angripa känsligt konto och om användaren har en känsligt konto, kan du se hur många resurser och konton som är anslutna direkt.

Om aktiviteten inte upptäcks under de senaste två dagarna i diagrammet visas inte längre, men [lateral förflyttning sökväg rapporten](reports.md) kommer att kunna ge dig information om lateral förflyttning sökvägar under de senaste 60 dagarna. 

Mer information finns i [Lateral förflyttning sökvägar](use-case-lateral-movement-path.md). 

 ![sökvägar för användarens profil lateral förflyttning](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Se även

- [Undersök lateral förflyttning sökvägar med Azure ATP](use-case-lateral-movement-path.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)