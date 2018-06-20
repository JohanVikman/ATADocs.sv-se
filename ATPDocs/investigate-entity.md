---
title: Undersöka användare och datorer med Azure ATP | Microsoft Docs
description: Beskriver hur du undersöker misstänkta aktiviteter som utförs av användare, enheter, datorer eller enheter med hjälp av Azure Advanced Threat Protection (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190459"
---
*Gäller för: Azure Advanced Threat Protection version 1.9.*



# <a name="investigate-an-entity-with-azure-atp"></a>Undersöka en entitet med Azure ATP

Den här artikeln beskriver processen för att undersöka entiteter när misstänkta aktiviteter har upptäckts med Azure Advanced Threat Protection (ATP). När du visar en misstänkt aktivitet i i tidslinjen kan du detaljnivån i entiteten som ingår i aktiviteten och använda följande parametrar och information för att lära dig mer om vad som hänt och vad du behöver göra för att minska risken.

## <a name="look-at-the-entity-profile"></a>Titta på entitetsprofilen

Entitetsprofilen ger dig en omfattande entitet sida med utformade för fullständig djupdykning undersökning av användare, datorer, enheter, och de har åtkomst till resurser och deras historik. Profilsidan drar nytta av den nya logiska aktivitet konverterare för Azure ATP som kan titta på en grupp av aktiviteter som inträffar (aggregerade upp till en minut) och gruppera dem i en enskild logisk aktivitet att ge en bättre förståelse för faktiska aktiviteter dina användare.

Klicka på namnet på enheten, till exempel ett användarnamn i tidslinjen misstänkt aktivitet för att komma åt en entitet profilsida. Du kan också se en mini version av entitetsprofilen på sidan misstänkt aktivitet genom att hovra över entitetsnamnet.

Entitetsprofilen kan du visa entitet aktiviteter, visa katalogdata och visa lateral förflyttning sökvägar för entiteten. Mer information finns i [undersöker entitetsprofiler ](entity-profiles.md).

## <a name="check-entity-tags"></a>Kontrollera entitetstaggar

Azure ATP hämtar taggar utanför Active Directory för att ge ett enda gränssnitt för övervakning av dina Active Directory-användare och enheter. Dessa taggar ger dig information om entiteten från Active Directory, inklusive:
- Partiell: Användaren, datorn eller gruppen har synkroniserats inte från domänen och löstes delvis via en global katalog. Vissa attribut är inte tillgängliga.
- Olösta: Datorn kunde inte matchas till en giltig entitet i active directory-skogen. Ingen directory-information är tillgänglig.
- Borttagen: Enheten har tagits bort från Active Directory.
- Inaktiverat: Enheten har inaktiverats i Active Directory.
- Låst: Entiteten har angett ett felaktigt lösenord för många gånger och är låst.
- Upphört att gälla: Entiteten har upphört att gälla i Active Directory.
- Nya: Entiteten skapades mindre än 30 dagar sedan.

## <a name="look-at-the-user-access-control-flags"></a>Titta på användaren åtkomstkontroll flaggor

Användaren åtkomstkontroll flaggor är också importeras från Active Directory. Azure ATP innehåller 10 flaggor som gäller för undersökning: 
- Lösenordet upphör aldrig att gälla
- Betrodd för delegering
- Smartkort krävs
- Lösenordet har upphört att gälla
- Tomma lösenord tillåts
- Lösenord i oformaterad text lagras
- Kan inte delegeras
- DES-kryptering
- Kerberos-förautentisering krävs inte
- Kontot är inaktiverat 

Azure ATP får du reda på om dessa flaggor är på eller stänga av i Azure Active Directory. Färgade ikoner anger att flaggan är aktiverad i Active Directory. i exemplet nedan, endast **kontot inaktiveras** är aktiverad i Active Directory.

 ![användaren åtkomstkontroll flaggor](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Dubbelkontrollera med Windows Defender

För att ge kryssprodukten insikter innehåller entitetsprofilen entiteter som har öppna aviseringar i Windows Defender med en bricka. Den här Aktivitetsikon får du reda på hur många öppna aviseringar entiteten har i Windows Defender och deras allvarlighetsgrad är. Klicka på bricka gå direkt till aviseringar relaterade till den här entiteten i Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Hålla ett öga på känsliga användare och grupper

Azure ATP importerar användar- och gruppinformation från Azure Active Directory, så att du kan identifiera vilka användare automatiskt betraktas som känslig eftersom de är medlemmar i följande grupper i Active Directory:

-   Administratörer
-   Privilegierade användare
-   Kontoansvariga
-   Serveransvariga
-   Skrivaransvariga
-   Ansvariga för säkerhetskopiering
-   Ansvariga för replikering
-   Användare av fjärrskrivbord 
-   Ansvariga för nätverkskonfigurering 
-   Incoming Forest Trust Builders
-   Domänadministratörer
-   Domänkontrollanter
-   Skapare och ägare av grupprincip 
-   skrivskyddade domänkontrollanter 
-   Företagets skrivskyddade domänkontrollanter 
-   Schemaadministratörer 
-   Företagsadministratörer

Dessutom kan du **manuellt tagga** entiteter som känslig inom Azure ATP. Detta är viktigt eftersom vissa Azure ATP identifieringar, till exempel känsliga grupp ändring identifiering och lateral förflyttning sökväg förlitar sig på en entitet känslighet status. Om du manuellt lägga till märkord ytterligare användare eller grupper som skiftlägeskänslig, till exempel styrelsemedlemmar, chefer och chef för försäljning, ska Azure ATP anses vara känslig. Mer information finns i [arbeta med känsliga konton](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Tänk på att lateral förflyttning sökvägar

Azure ATP kan hjälpa dig att förhindra angrepp som använder lateral förflyttning sökvägar. Lateral förflyttning är när en angripare proaktivt icke-känsliga konton används för att få åtkomst till känsliga konton.

Om det finns en lateral förflyttning sökväg för en entitet i profilsida entitet du kan klicka på den **Lateral förflyttning sökvägar** fliken. Som visas i diagrammet innehåller en karta över möjliga sökvägar till känsliga användaren. 

Mer information finns i [Investigating lateral förflyttning sökvägar med Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Är det en honeytoken-enhet?

Det är viktigt att veta om enheten är en honeytoken innan du flyttar på med din undersökning. För din bekvämlighet kan Azure ATP du taggen konton och de entiteter som honeytokens. Sedan, under undersökningen, när du öppnar entitetsprofilen eller Mini-profil, visas honeytoken-skylt att varna dig om att du tittar på aktiviteten utfördes med ett konto som du taggade som en honeytoken.


    
## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)