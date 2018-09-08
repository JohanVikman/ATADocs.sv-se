---
title: Hur du undersöker användare och datorer med Azure ATP | Microsoft Docs
description: Beskriver hur du undersöker misstänkta aktiviteter som utförs av användare, enheter, datorer eller enheter som använder Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/6/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0c0558dbe0b4eba849adb635a84bc934e406e56f
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166569"
---
*Gäller för: Azure Avancerat skydd*



# <a name="investigate-an-entity-with-azure-atp"></a>Undersöka en entitet med Azure ATP

Den här artikeln beskriver processen för att undersöka entiteter när misstänkta aktiviteter har identifierats med Azure Advanced Threat Protection (ATP). När du visar en misstänkt aktivitet på tidslinjen kan du granska nedåt i entiteten som ingår i aktiviteten och lära dig mer om vad som hände och vad du behöver göra för att minska riskerna med hjälp av följande parametrar och information.

## <a name="look-at-the-entity-profile"></a>Titta på entitetsprofilen

Entitetsprofilen ger dig en omfattande entitet-sida som utformats för djupgående om undersökning av användare, datorer, enheter och resurser som de har åtkomst till tillsammans med deras historik. Profilsidan drar nytta av den nya logiska aktivitet translator för Azure ATP som kan titta på en grupp med aktiviteter som inträffar (aggregerade upp till en minut) och gruppera dem i en enda logisk aktivitet att ge en bättre förståelse för faktiska aktiviteter dina användare.

Klicka på namnet på entiteten, till exempel ett användarnamn i tidslinjen för misstänkta aktiviteter för att komma åt en sida för entiteten. Du kan också se en mini version av entitetsprofilen på sidan misstänkt aktivitet genom att hovra över enhetens namn.

Entitetsprofilen kan du visa enhetsaktiviteter, visa katalogdata och visa laterala rörelsebanor för entiteten. Mer information finns i [förstå entitetsprofiler ](entity-profiles.md).

## <a name="check-entity-tags"></a>Kontrollera entitetstaggar

Azure ATP hämtar taggar från Active Directory för att ge dig ett enda gränssnitt för övervakning av dina Active Directory-användare och entiteter. Dessa taggar ger dig information om entiteten från Active Directory, inklusive:
- Partiell: Den här användaren, datorn eller gruppen synkroniserades inte från domänen och har delvis lösts via en global katalog. Vissa attribut är inte tillgängliga.
- Olöst: Datorn kunde inte matchas till en giltig entitet i active directory-skogen. Det finns inga kataloginformation.
- Borttagna: Entiteten har tagits bort från Active Directory.
- Inaktiverat: Entiteten är inaktiverad i Active Directory.
- Låst: Entiteten angav fel lösenord för många gånger och är låst.
- Har upphört att gälla: Entiteten har upphört att gälla i Active Directory.
- Nyhet: Entiteten skapades mindre än 30 dagar sedan.

## <a name="look-at-the-user-account-control-flags"></a>Titta på användare konto control flaggor

Användare konto control flaggor som också importeras från Active Directory. Azure ATP entitet directory data omfattar 10 flaggor som gäller för undersökning: 
- Lösenordet upphör aldrig att gälla
- Betrodd för delegering
- Smartkort krävs
- Lösenordet har upphört att gälla
- Tomma lösenord tillåts
- Lösenord lagrat i klartext
- Kan inte delegeras
- Enbart DES-kryptering
- Kerberos-förautentisering krävs inte
- Kontot har inaktiverats 

Azure ATP får du reda på om dessa flaggor är eller inaktivera i Azure Active Directory. Färgade ikoner och motsvarande reglage anger status för varje flagga. I exemplet nedan, endast **lösenordet upphör aldrig att gälla** finns på i Active Directory.

 ![användare konto control flaggor](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Kontrollera med Windows Defender

För att ge mellan produktkännedom standardentiteter din entitet profil som har öppna aviseringar i Windows Defender med en symbol. Den här skylten talar om hur många öppna aviseringar entiteten har i Windows Defender och deras allvarlighetsgrad är. Klicka på aktivitetsikonen och gå direkt till de aviseringar som rör den här entiteten i Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Håll ett öga på känsliga användare och grupper

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

Dessutom kan du **manuellt tagga** entiteter som känslig inom Azure ATP. Detta är viktigt eftersom vissa Azure ATP-identifieringar, till exempel känsliga grupp ändring av identifiering och lateral rörelsesökväg är beroende av en entitet känslighet status. Om du manuellt tagga ytterligare användare eller grupper som känsliga som styrelsemedlemmar, chefer och försäljning styrelsen ska Azure ATP anses vara känslig. Mer information finns i [arbeta med känsliga konton](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Tänk på lateral förflyttning

Azure ATP kan hjälpa dig att förhindra attacker som använder lateral förflyttning. Lateral förflyttning är när en angripare proaktivt använder icke-känsliga konton för att få åtkomst till känsliga konton.

Om en lateral rörelsesökväg finns för en entitet i profilsida entitet kommer du att kunna klickar du på den **Lateral förflyttning** fliken. Diagram som visas innehåller en karta över möjliga sökvägarna till din känsliga användare. 

Mer information finns i [Investigating laterala förflyttningssökvägar med Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Är det en honeytoken-enhet?

Det är viktigt att veta om entiteten är en honeytoken innan du går vidare med undersökningen. Du kan tagga konton och entiteter som honeytokens i Azure ATP. När du öppnar den entiteten eller en profil Mini för ett konto eller en entitet som du har taggats som en honeytoken visas honeytoken-märket. När du undersöker, aviserar honeytoken-märket att aktiviteten under granskning har utförts med ett konto som du har taggats som en honeytoken.


    
## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)