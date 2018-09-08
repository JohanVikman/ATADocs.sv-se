---
title: Arbeta med entitetsprofiler i Advanced Threat Analytics-konsolen | Microsoft Docs
description: Beskriver hur du undersöka entiteter från skärmen användare profiler i ATA-konsolen
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b809224710c022ec86453c32f0675b28fc45a6e7
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166229"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="investigating-entity-profiles"></a>Undersöka entitetsprofiler

Entitetsprofilen ger dig med en instrumentpanel för djupgående om undersökning av användare, datorer, enheter och resurser som de har åtkomst till och deras historik. Profilsidan drar nytta av den nya logiska aktivitet translator för ATA som kan titta på en grupp med aktiviteter som inträffar (aggregerat upp till en minut) och gruppera dem i en enda logisk aktivitet att ge en bättre förståelse för de faktiska aktiviteterna i din användare.

Klicka på namnet på entiteten, till exempel ett användarnamn i tidslinjen för misstänkta aktiviteter för att komma åt en sida för entiteten.

Du får alla Active Directory-informationen finns på enhet – e-postadress, domän, första sågs datumet i den vänstra menyn. Om entiteten är känsligt det får du veta varför. Exempelvis kan användaren märkts känslig eller medlem i en känslig grupp?
Om det är en känsliga användare visas ikonen under användarens namn.

## <a name="view-entity-activities"></a>Visa entitet aktiviteter

Visa alla aktiviteter som utförts av användaren eller utförs på en entitet, klicka på den **aktiviteter** fliken. 

 ![profilen användaraktiviteter](media/user-profile-activities.png)

Huvudfönster entitetsprofilen visar en tidslinje för entitetens aktiviteter med en historik över upp till 6 månader tillbaka, där du kan också granska nedåt i de entiteter som används av användaren eller för entiteter är användare som anslöt entitet som standard.

Du kan visa sammanfattning av panelerna som ger dig en snabb överblick över vad du behöver att förstå i korthet om din entitet överst på sidan. Dessa paneler ändras beroende på vilken typ av entiteten är för en användare visas:
- Hur många öppna misstänkta aktiviteter som finns för användaren
- Hur många datorer som användaren har loggat in på
- Hur många resurser som används av användaren
- Från vilka platser du loggat in VPN

  ![entitet-menyn](media/entity-menu.png)

För datorer som kan du se:
- Hur många öppna misstänkta aktiviteter som finns för datorn
- Hur många användare som loggat in på datorn
- Hur många resurser som används av datorn
- Hur många platser VPN användes från på datorn
- En lista som IP-adresser datorn har använt

  ![entiteten menyn dator](media/entity-computer.png)

Med hjälp av den **filtrera efter** knappen ovanför tidslinjen aktivitet kan du filtrera aktiviteter av aktivitetstypen. Du kan också filtrera ut en viss (bort störande) typ av aktivitet. Det här är verkligen behöver mer information om du vill förstå grunderna om vad en entitet gör i nätverket. Du kan även gå till ett visst datum och du kan exportera aktiviteterna som filtrerats till Excel. Den exporterade filen innehåller en sida för directory services ändringar (sådant som ändrats i Active Directory för kontot) och en separat sida för aktiviteter. 

## <a name="view-directory-data"></a>Visa katalogdata

Den **katalogdata** fliken innehåller statisk information som är tillgängliga från Active Directory, inklusive Säkerhetsflaggor för användaren åtkomstkontroll. ATA visar även gruppmedlemskap för användaren så att du kan se om användaren har en direkt medlemskap eller ett rekursiva medlemskap. ATA visar en lista över medlemmar i gruppen för grupper.

 ![directory data för användarprofiler](media/user-profile-dir-data.png)

I den **Användaråtkomstkontroll** avsnittet ATA ser du säkerhetsinställningar som kan behöva din attentions. Du kan se viktiga flaggor om användaren, till exempel kan den användaren genom att trycka på RETUR för att kringgå lösenordet, har användaren ett lösenord som upphör aldrig att gälla osv. 

## <a name="view-lateral-movement-paths"></a>Visa laterala rörelsebanor

Genom att klicka på den **Lateral förflyttning** fliken som du kan visa en helt dynamisk och klickbara karta som ger dig en visuell representation av laterala rörelsebanor till och från den här användaren som kan användas till att infiltrera ditt nätverk.

Kartan ger dig en lista över hur många hopp mellan datorer eller användare en angripare skulle ha till och från den här användaren att angripa ett känsligt konto, och om användaren själv har ett känsligt konto kan du se hur många resurser och konton som är direkt ansluten. Mer information finns i [Lateral förflyttning](use-case-lateral-movement-path.md). 

 ![användarens profil laterala rörelsebanor](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
