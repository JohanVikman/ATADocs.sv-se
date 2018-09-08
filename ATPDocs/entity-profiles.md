---
title: Arbeta med användarprofiler i Azure Advanced Threat Protection-arbetsyteportalen | Microsoft Docs
description: Beskriver hur du undersöker användare från skärmen användare profiler i Azure ATP-arbetsyteportalen
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/06/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b4353de9d004358ddcdc929271fd96665e1c7322
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165855"
---
*Gäller för: Azure Avancerat skydd*



# <a name="understanding-entity-profiles"></a>Förstå entitetsprofiler

Entitetsprofilen ger dig en heltäckande entitet sida med utformat för fullständig djupdykning undersökning av användare, datorer, enheter, och de resurser som de har åtkomst till och deras historik. Profilsidan drar nytta av den nya logiska aktivitet translator för Azure ATP som kan titta på en grupp med aktiviteter som inträffar (aggregerade upp till en minut) och gruppera dem i en enda logisk aktivitet att ge en bättre förståelse för faktiska aktiviteter dina användare.

Klicka på namnet på entiteten, till exempel ett användarnamn i tidslinjen för misstänkta aktiviteter för att komma åt en sida för entiteten.

Du får alla Active Directory-informationen finns på enhet – e-postadress, domän, första sågs datumet i den vänstra menyn. Om entiteten är känsliga, meddelar du varför. Exempelvis kan användaren märkts känslig eller medlem i en känslig grupp?
Om det är en känsliga användare, visas ikonen under användarens namn.

## <a name="view-entity-activities"></a>Visa entitet aktiviteter

Visa alla aktiviteter som utförts av användaren eller utförs på en entitet, klicka på den **aktiviteter** fliken. 

 ![profilen användaraktiviteter](media/user-profile-activities.png)

Huvudfönster entitetsprofilen visar en tidslinje för entitetens aktiviteter med en historik över upp till sex månader tillbaka, där du kan också granska nedåt i de entiteter som används av användaren eller för entiteter är användare som anslöt entitet som standard.

Överst på sidan kan du visa sammanfattning av panelerna som ger dig en snabb överblick över vad du behöver att förstå i korthet om din enhet – hur många datorer som användaren har loggat in till, hur många resurser som användes och platser där en användare loggat in VPN (om konfigurerad) . 

Med hjälp av den **filtrera efter** knappen ovanför tidslinjen aktivitet kan du filtrera aktiviteter av aktivitetstypen. Du kan också filtrera ut en viss (bort störande) typ av aktivitet. Det här är användbart om du behöver mer information om du vill förstå grunderna om vad en entitet gör i nätverket. Du kan även gå till ett visst datum och du kan exportera aktiviteterna som filtrerats till Excel. Den exporterade filen innehåller en sida för directory services ändringar (sådant som ändrats i Active Directory för kontot) och en separat sida för aktiviteter. 

## <a name="view-directory-data"></a>Visa katalogdata

Den **katalogdata** fliken innehåller statisk information som är tillgängliga från Active Directory, inklusive Säkerhetsflaggor för användaren åtkomstkontroll. Azure ATP visar även gruppmedlemskap för användaren så att du kan se om användaren har en direkt medlemskap eller ett rekursiva medlemskap. Azure ATP visar en lista över medlemmar i gruppen för grupper.

 ![directory data för användarprofiler](media/user-profile-dir-data.png)

I den **Användaråtkomstkontroll** avsnittet säkerhetsinställningar för Azure ATP Surface-enheter som kan behöva din attentions. Du kan se viktiga flaggor om användaren, till exempel kan den användaren genom att trycka på RETUR för att kringgå lösenordet, har användaren ett lösenord som upphör aldrig att gälla osv. 

## <a name="view-lateral-movement-paths"></a>Visa laterala rörelsebanor

Genom att klicka på fliken Lateral förflyttning sökvägar, kan du visa en helt dynamisk och klickbara karta som ger dig en visuell representation av laterala rörelsebanor till och från den här användaren som kan användas till att infiltrera ditt nätverk.

Kartan ger dig en lista över hur många hopp mellan datorer eller användare angriparen till och från den här användaren att angripa ett känsligt konto och om användaren har ett känsligt konto, kan du se hur många resurser och -konton är direkt anslutna.

Om aktiviteten inte identifieras under de senaste två dagarna i diagrammet visas inte längre, men [lateral förflyttning sökväg rapporten](reports.md) kommer att kunna ge dig information om laterala rörelsebanor under de senaste 60 dagarna. 

Mer information finns i [Lateral förflyttning](use-case-lateral-movement-path.md). 

 ![användarens profil laterala rörelsebanor](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Se även

- [Undersöka laterala förflyttningssökvägar med Azure ATP](use-case-lateral-movement-path.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)