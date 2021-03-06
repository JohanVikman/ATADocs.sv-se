---
title: Guide för misstänkt aktivitet i ATA | Microsoft Docs
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/29/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: be809f422e797f08655b7841fc7f9ecb7423a0a6
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133930"
---
*Gäller för: Advanced Threat Analytics version 1.9*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Guide för misstänkt aktivitet för avancerad Hotanalys

Följande rätt undersökning misstänkta aktiviteter kan klassificeras som:

-   **Sann positiv händelse**: en skadlig åtgärd som identifierats av ATA.

-   **Godartad sann positiv**: en åtgärd som identifierats av ATA som fungerar som ett hot men inte är skadlig, till exempel ett genomslagstest.

-   **Falsk positiv identifiering**: ett larm som false, vilket innebär att aktiviteten inte inträffa.

Mer information om hur du arbetar med ATA-aviseringar finns i [arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).

Frågor eller feedback, kontakta ATA-teamet på [ ATAEval@microsoft.com ](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Onormal modifiering av känslig grupp


**Beskrivning**

Angripare kan du lägga till användare i mycket Privilegierade grupper. De gör att få åtkomst till fler resurser och ta persistens. Identifieringen baseras på Profileringen gruppaktiviteter för ändring av användare och aviseringar när ett onormalt tillägg till en känslig grupp visas. Profilering utförs kontinuerligt av ATA. Minsta tid ska gå innan en avisering aktiveras är en månad per varje domänkontrollant.

En definition av känsliga grupper i ATA finns [arbeta med ATA-konsolen](working-with-ata-console.md#sensitive-groups).


Den här identifieringen baseras på [händelser granskas på domänkontrollanter](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Om du vill se till att dina domänkontrollanter granska nödvändiga händelser, använder du verktyget som refereras i [ATA granskning (AuditPol, avancerade granska inställningar tvingande, tjänstidentifiering för Lightweight Gateway)](https://aka.ms/ataauditingblog).

**Undersökning**

1. Är den grupp ändringen legitima? </br>Legitima gruppändringar som sällan inträffar och inte lärt dig som ”normal”, kan orsaka en avisering som kan betraktas som en godartad sann positiv händelse.

2. Om objektet har lagts till var ett användarkonto, kontrollerar du vilka åtgärder som användarkonton som tog efter som läggs till i administratörsgruppen. Gå till sidan för användaren i ATA för att få mer kontext. Misstänkta aktiviteter som är associerade med kontot före eller efter det att det inte har någon annan ägde rum? Ladda ned den **ändring av känsliga grupper** rapporten för att se vad andra ändringar har gjorts och av vem under samma tidsperiod.

**Reparation**

Minimera antalet användare som har behörighet att ändra känsliga grupper.

Konfigurera [Privileged Access Management för Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) om tillämpligt.

## <a name="broken-trust-between-computers-and-domain"></a>Brutet förtroende mellan datorer och domän

> ! [OBS] Den här misstänkt aktivitet är inaktuell och visas bara i ATA-versioner före 1.9.

**Beskrivning**

Brutet förtroende innebär att Active Directorys säkerhetskrav inte kanske gäller för datorer i fråga. Detta betraktas ofta som ett grundläggande säkerhets- och efterlevnadsfel och ett enkelt mål för angripare. I den här identifieringen utlöses en avisering om fler än 5 Kerberos-autentiseringsfel registreras från ett datorkonto i 24 timmar.

**Undersökning**

Är datorn i fråga tillåter användare att logga in? 
- Om Ja, kan du ignorera den här datorn i anvisningarna för reparation.

**Reparation**

Ansluta datorn till domänen igen om det behövs eller Återställ datorns lösenord.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Råstyrkeattack med enkel LDAP-bindning

**Beskrivning**

>[!NOTE]
> Den största skillnaden mellan **misstänkta autentiseringsfel** och denna identifiering är att ATA i den här identifieringen kan avgöra om olika lösenord användes.

En angripare försöker autentisera med många olika lösenord för olika konton tills rätt lösenord hittas för minst ett konto i en brute force-attack. Hitta en gång, kan en angripare logga in med det kontot.

I den här identifieringen utlöses en avisering när ATA identifierar ett stort antal enkla bindningsautentiseringar. Detta kan vara antingen *vågrätt* med en liten uppsättning lösenord för många användare; eller *lodrätt ”* med ett stort antal lösenord på bara några få användare; eller en kombination av de här två alternativen.

**Undersökning**

1. Om det finns många konton som ingår, klickar du på **Hämtningsinformation** att visa en lista i ett Excel-kalkylblad.

2. Klicka på aviseringen för att gå till dess särskild sida. Kontrollera om alla inloggningsförsök avslutades med en lyckad autentisering. Försöker visas som **gissade konton** på höger sida av informationsgrafiken. Om Ja, är några av de **gissade konton** normalt används från källdatorn? Om Ja, **utelämna** den misstänkta aktiviteten.

3. Om det finns inga **gissade konton**, är några av de **angripna konton** normalt används från källdatorn? Om Ja,**utelämna** den misstänkta aktiviteten.

**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.

## <a name="encryption-downgrade-activity"></a>Krypteringsnedgraderingsaktivitet

**Beskrivning**

Nedgradering av kryptering är en metod för lägre Kerberos genom att nedgradera krypteringsnivån för olika fält i protokollet som vanligtvis är krypterade med den högsta nivån av kryptering. Ett lägre krypterade fält kan vara ett enklare mål för råstyrkeattacker som offline. Olika metoder för angrepp använda svaga produktidentifieringsförteckning för Kerberos-kryptering. I den här identifieringen ATA lär sig de Kerberos-krypteringstyperna används av datorer och användare och varnar dig när en svagare korrekt är att använda den: (1) är ovanlig för källdatorn och/eller användaren. och (2) matchar känt attackteknikerna.

Det finns tre identifieringstyper:

1.  Skadlig Skeleton Key – är skadlig kod som körs på domänkontrollanter och tillåter autentisering för domänen med ett konto utan att känna till lösenordet. Den skadliga koden använder ofta svagare krypteringsalgoritmer för att hash-användarens lösenord på domänkontrollanten. I den här identifieringen har krypteringsmetod för KRB_ERR meddelandet från domänkontrollanten att det konto som ber om en biljett nedgraderas jämfört med tidigare inlärda beteende.

2.  Guld biljett – i en [Golden Ticket](#golden-ticket) aviseringen, krypteringsmetod för fältet TGT i TGS_REQ (tjänstbegäran) meddelandet från källdatorn har nedgraderas jämfört med tidigare inlärda beteende. Detta baseras inte på en gång avvikelseidentifiering (som i andra Golden Ticket identifieringen). Det var dessutom ingen Kerberos-autentiseringsbegäran som är associerade med den tidigare tjänstbegäran som identifieras av ATA.

3.  Overpass-the-Hash – en angripare kan använda en svag stulen hash för att skapa en stark biljett med en Kerberos-AS-begäran. I den här identifieringen AS_REQ kryptering meddelandetypen från källdatorn har nedgraderas jämfört med tidigare inlärda beteendet (det vill säga datorn har med AES).

**Undersökning**

Först kontrollerar du beskrivningen av aviseringen för att se vilka av de ovanstående tre identifieringstyper hanterar du med. För ytterligare information, hämta Excel-kalkylblad.
1.  Skadlig Skeleton Key – du kan kontrollera om Skeleton Key har påverkat domänkontrollanterna med hjälp av den [genomsökningsverktyget som utvecklats av ATA-teamet](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Om skannern hittar skadlig kod på 1 eller flera av dina domänkontrollanter, är det en sann positiv händelse.
2.  Gyllene biljett – i Excel-kalkylblad, gå till den **nätverksaktivitet** fliken. Du ser att relevanta nedgraderat fältet är **begär kryptering Biljettyp**, och **stöds krypteringstyper som källa datorn** innehåller starkare krypteringsmetoder.
  a.    Kontrollera käll- och konto eller om det finns flera källdatorer och konton kontrollera om de har något i gemensamma (till exempel alla som marknadsföring personal använder en viss app som gör att aviseringen ska utlösas). Det finns fall där ett anpassat program som används sällan autentiseras med hjälp av ett chiffer med lägre kryptering. Kontrollera om det finns några anpassade appar på källdatorn. Om så är det troligen en godartad sann positiv händelse och du kan **utelämna** den.
  b.    Kontrollera resursen som används av dessa biljetter, om det finns en resurs som de kommer alla åt, verifiera den, se till att det är en giltig resurs som de ska komma åt. Kontrollera också om målresurs stöder stark krypteringsmetoder. Du kan kontrollera detta i Active Directory genom att kontrollera attributet `msDS-SupportedEncryptionTypes`, resurs-tjänstkontots.
3.  Overpass-the-Hash – i Excel-kalkylblad, gå till den **nätverksaktivitet** fliken. Du ser att relevanta nedgraderat fältet är **krypterade tidsstämpel krypteringstyp** och **stöds krypteringstyper som källa datorn** innehåller starkare krypteringsmetoder.
  a.    Det finns fall där den här aviseringen kan utlösas när användare loggar in med smartkort om smartkort-konfigurationen har ändrats nyligen. Kontrollera om det fanns ändringar så här för konton som ingår. Om så detta beror troligen en godartad sann positiv händelse och du kan **utelämna** den.
  b.    Kontrollera resursen som används av dessa biljetter, om det finns en resurs som de kommer alla åt, verifiera den, se till att det är en giltig resurs som de ska komma åt. Kontrollera också om målresurs stöder stark krypteringsmetoder. Du kan kontrollera detta i Active Directory genom att kontrollera attributet `msDS-SupportedEncryptionTypes`, resurs-tjänstkontots.

**Reparation**

1.  Stommen Key – ta bort den skadliga koden. Mer information finns i [Dyrken analys av skadlig kod](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Gyllene biljett – Följ instruktionerna för den [Golden Ticket](#golden-ticket) misstänkta aktiviteter.   
    Dessutom eftersom skapar en Golden Ticket kräver administratörsrättigheter i domänen, implementera [skicka hash-rekommendationer](http://aka.ms/PtH).

3.  Overpass-the-Hash – återställa om kontot som är inblandade inte är känsliga, sedan lösenordet för kontot. Detta förhindrar angriparen från att skapa nya Kerberos-biljetter från lösenords-hash, även om de befintliga biljetterna kan fortfarande användas tills de upphör att gälla. Om det är ett känsligt konto bör du återställa KRBTGT-kontot två gånger som den misstänkta aktiviteten Golden Ticket. När du återställer KRBTGT två gånger upphäver alla Kerberos uppgifterna i den här domänen så planera innan du gör det. Läs mer i [KRBTGT Account Password Reset Scripts nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Se även med hjälp av den [återställa verktyget lösenord/nycklar för KRBTGT-kontot](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Eftersom det här är en teknik för lateral förflyttning, följer du de bästa metoderna för [skicka hash-rekommendationer](http://aka.ms/PtH).


## <a name="honeytoken-activity"></a>Honeytoken-aktivitet


**Beskrivning**

Honeytoken-konton är attrappkonton som skapas ställa in för att identifiera och spåra skadliga aktiviteter där dessa konton. Honeytoken-konton bör lämnas oanvända, samtidigt som du har ett attraktivt namn att locka angripare (till exempel SQL-administratör). Alla aktiviteter från dem kan tyda på skadligt beteende.

Mer information om honeytoken-konton finns i [installera ATA – steg 7](install-ata-step7.md).

**Undersökning**

1.  Kontrollera om ägaren av källdatorn används Honeytoken-konto för att autentisera, med hjälp av den metod som beskrivs i sidan misstänkt aktivitet (till exempel Kerberos, LDAP, NTLM).

2.  Bläddra till källan datorer profilsidor och kontrollera vilka konton som autentiserats från dem. Kontrollera med ägarna av dessa konton om de har använt Honeytoken-konto.

3.  Detta kan vara en icke-interaktiv inloggning, så se till att söka efter program eller skript som körs på källdatorn.

Anta att det här är skadliga om när du har utfört steg 1 till 3, om det inte finns några tecken på ofarliga användning.

**Reparation**

Se till att Honeytoken konton används endast för deras syfte, annars många aviseringar kan genereras.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Identitetsstöld med Pass-the-Hash-attack

**Beskrivning**

Pass the Hash är en teknik för lateral förflyttning där stjäl angriparen NTLM-hash för en användare från en dator och använda den för att få åtkomst till en annan dator. 

**Undersökning**

Användes hash-värdet från en dator som den angivna användaren äger eller regelbundet använder? Om Ja, är det här en falsk positiv identifiering. Om inte, beror det troligen en sann positiv händelse.

**Reparation**

1. Om kontot ingår inte är känsliga, återställer du lösenordet för kontot. Detta förhindrar angriparen från att skapa nya Kerberos-biljetter från lösenords-hash, även om de befintliga biljetterna kan fortfarande användas tills de upphör att gälla. 

2. Om det är ett känsligt konto bör du återställa KRBTGT-kontot två gånger som den misstänkta aktiviteten Golden Ticket. När du återställer KRBTGT två gånger upphäver alla Kerberos uppgifterna i den här domänen så planera innan du gör det. Finns i riktlinjerna i [KRBTGT Account Password Reset Scripts nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), se även med hjälp av den [återställa verktyget lösenord/nycklar för KRBTGT-kontot](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Eftersom det här är en teknik för lateral förflyttning, följer du de bästa metoderna för [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitetsstöld med Pass-the-Ticket-attack

**Beskrivning**

Pass the Ticket är en teknik för lateral förflyttning där stjäl angriparen en Kerberos-biljett från en dator och använda den för att få åtkomst till en annan dator genom att återanvända den stulna biljetten. I den här identifieringen visas en Kerberos-biljett som användas på två (eller fler) olika datorer.

**Undersökning**

1. Klicka på den **Hämtningsinformation** för att visa en fullständig lista över IP-adresser som ingår. Har IP-adressen för en eller båda datorerna tillhör ett undernät som allokeras från en underdimensionerad DHCP-pool, till exempel VPN eller Wi-Fi? Delas IP-adressen? Till exempel genom en NAT-enhet? Om svaret på någon av dessa frågor är Ja, är det en falsk positiv identifiering.

2. Finns det ett anpassat program som vidarebefordrar biljetter åt användare? Om det är alltså en godartad sann positiv händelse.

**Reparation**

1. Om kontot ingår inte är känsliga, återställer du lösenordet för kontot. Detta förhindrar angriparen från att skapa nya Kerberos-biljetter från lösenords-hash, även om de befintliga biljetterna kan fortfarande användas tills de upphör att gälla.  

2. Om det är ett känsligt konto bör du återställa KRBTGT-kontot två gånger som den misstänkta aktiviteten Golden Ticket. När du återställer KRBTGT två gånger upphäver alla Kerberos uppgifterna i den här domänen så planera innan du gör det. Finns i riktlinjerna i [KRBTGT Account Password Reset Scripts nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), se även med hjälp av den [återställa verktyget lösenord/nycklar för KRBTGT-kontot](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Eftersom det här är en teknik för lateral förflyttning, följ rekommenderade metoder i [skicka hash-rekommendationer](http://aka.ms/PtH).

## Guld för Kerberos-biljett<a name="golden-ticket"></a>

**Beskrivning**

Angripare med administratörsrättigheter i domänen kan påverka den [KRBTGT-kontot](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). De kan använda KRBTGT-kontot för att skapa Kerberos biljettbeviljande biljetter (TGT) som tillhandahåller auktorisering till alla resurser och ange förfallodatum för biljett till någon godtycklig tidpunkt. Den här falska TGT kallas en ”gyllene biljett” och gör att angripare kan tillskansa sig beständighet i nätverket.

I den här identifieringen en avisering utlöses när en Kerberos-biljett beviljad biljett används under mer än den tillåtna tiden tillåts som anges i den [högsta livstid för användarbiljett](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) säkerhetsprincip.

**Undersökning**

1. Det har alla de senaste (inom de senaste timmarna) ändringar på den **högsta livstid för användarbiljett** i Grupprincip? Om Ja, sedan **Stäng** aviseringen (det var en falsk positiv identifiering).

2. Är ATA Gateway som ingår i den här aviseringen en virtuell dator? Om Ja, det nyligen återupptas från ett sparat tillstånd? Om Ja, sedan **Stäng** den här aviseringen.

3. Om svaret på dessa frågor är Nej, förutsätter att detta är skadliga.

**Reparation**

Ändra lösenordet för Kerberos-biljett biljettbeviljande biljetter (KRBTGT) två gånger enligt riktlinjerna i [KRBTGT Account Password Reset Scripts nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)med hjälp av den [återställa KRBTGT-kontot lösenord/nycklar verktyget](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). När du återställer KRBTGT två gånger upphäver alla Kerberos uppgifterna i den här domänen så planera innan du gör det.  
Dessutom eftersom skapar en Golden Ticket kräver administratörsrättigheter i domänen, implementera [skicka hash-rekommendationer](http://aka.ms/PtH).


## <a name="malicious-data-protection-private-information-request"></a>Skadlig privat informationsbegäran för dataskydd

**Beskrivning**

Data Protection API (DPAPI) används av Windows för att skydda lösenord som sparats av webbläsare, krypterade filer och andra känsliga data på ett säkert sätt. Domänkontrollanter lagrar en reservhuvudnyckel som kan användas för att dekryptera alla hemligheter som krypterats med DPAPI på domänanslutna Windows-datorer. Angripare kan använda den huvudnyckeln för att dekryptera alla hemligheter som skyddas av DPAPI på alla domänanslutna datorer.
I den här identifieringen utlöses en avisering när av DPAPI används för att hämta huvudnyckeln för säkerhetskopiering.

**Undersökning**

1. Är den källdator som kör en organisation godkänd Avancerat Säkerhetsskanner mot Active Directory?

2. Om Ja och den bör alltid gjort det, **Stäng och undanta** den misstänkta aktiviteten.

3. Om Ja och den bör inte göra detta, **Stäng** den misstänkta aktiviteten.

**Reparation**

Om du vill använda DPAPI måste angriparen administratörsrättigheter i domänen. Implementera [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="malicious-replication-of-directory-services"></a>Skadlig replikering av katalogtjänster


**Beskrivning**

Active Directory-replikering är en process som synkroniseras ändringar som görs på en domänkontrollant med alla andra domänkontrollanter. Med tillräcklig behörighet kan initiera angripare en replikeringsbegäran så att de kan hämta data som lagras i Active Directory, inklusive lösenords-hash.

I den här identifieringen utlöses en avisering när en replikeringsbegäran initieras från en dator som inte är en domänkontrollant.

**Undersökning**

1.  Är datorn i fråga en domänkontrollant? Till exempel en nyligen uppgraderade domänkontrollant som hade problem med replikering. Om Ja, **Stäng** den misstänkta aktiviteten. 
2.  Datorn i fråga ska vara replikering av data från Active Directory? Till exempel Azure AD Connect. Om Ja, **Stäng och undanta** den misstänkta aktiviteten.
3.  Klicka på källdatorn eller konto för att gå till dess profilsida. Kontrollera vad som hände vid tidpunkten för replikering, söker efter ovanliga aktiviteter, till exempel: vem som har loggat in, vilka resurser där nås. 


**Reparation**

Verifiera följande behörigheter: 

- Replikera katalogändringar   

- Replikera alla katalogändringar  

Mer information finns i [bevilja Active Directory Domain Services-behörigheter för profilsynkronisering i SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Du kan utnyttja [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) eller skapa ett Windows PowerShell-skript för att fastställa vem i domänen har dessa behörigheter.

## <a name="massive-object-deletion"></a>Massiv objektborttagning

**Beskrivning**

I vissa situationer kan utföra angripare en denial of service (DoS) i stället för bara stjäla information. Tar bort ett stort antal konton är en DoS-teknik.

I den här identifieringen utlöses en avisering när mer än 5% av alla konton tas bort. Identifieringen kräver läsbehörighet till behållaren borttagna objekt.  
Information om hur du konfigurerar läsbehörigheter för behållaren för borttagna objekt finns i **ändring av behörigheter i en behållare för borttagna objekt** i [visa eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Undersökning**

Granska listan över konton som har tagits bort och förstå om det finns ett mönster eller en affärsskäl som kan motivera enorma borttagningen.

**Reparation**

Ta bort behörigheter för användare som kan ta bort konton i Active Directory. Mer information finns i [visa eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Behörighetseskalering med förfalskade auktoriseringsdata

**Beskrivning**

Kända sårbarheter i äldre versioner av Windows Server gör att angripare kan manipulera för den certifikatet PAC (Privileged Attribute), ett fält i Kerberos-biljetten som innehåller en användare auktoriseringsdata (i Active Directory är detta gruppmedlemskap), beviljar ytterligare behörigheter för angripare.

**Undersökning**

1. Klicka på aviseringen för att komma till dess informationssida.

2. Är måldatorn (under den **ACCESSED** kolumn) korrigerade med MS14-068 (domänkontrollanten) eller MS11-013 (server)? Om Ja, **Stäng** den misstänkta aktiviteten (det är ett falsklarm).

3. Om inte, körs på källdatorn (under den **FROM** kolumn) ett OS/program som kan ändra PAC-certifikatet? Om Ja, **utelämna** den misstänkta aktiviteten (det är en godartad sann positiv).

4. Om svaret var inte anta detta är skadliga på ovanstående två frågor.

**Reparation**

Kontrollera att alla domänkontrollanter med operativsystem upp till Windows Server 2012 R2 är installerade med [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) och att alla medlemsservrar och domänkontrollanter upp till 2012 R2 är uppdaterade med KB2496930. Mer information finns i avsnitten om [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) och [förfalskat PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekognosering med kontouppräkning

**Beskrivning**

En ordlista använder med tusentals användarnamn eller verktyg, till exempel KrbGuess en angripare konto uppräkning rekognosering, för att försöka gissa användarnamn i din domän. Angriparen gör Kerberos-begäranden med hjälp av dessa namn innan du kan försöka att hitta ett giltigt användarnamn i din domän. Om en gissning avgör har ett användarnamn, får angriparen Kerberos-fel **förautentisering krävs** i stället för **säkerhetsobjekt okänd**. 

I den här identifieringen kan ATA identifiera var angreppet kommer ifrån, det totala antalet försök att gissa och hur många kunde matchas. Om det finns för många okänd användare kan identifierar ATA den som en misstänkt aktivitet. 

**Undersökning**

1. Klicka på aviseringen för att komma till dess informationssida. 

2. Den här värddatorn ska fråga domänkontrollanten avseende om konton finns (till exempel Exchange-servrar)? <br></br>
Finns det ett skript eller program som körs på värden som kan generera problemet? <br></br>
Om svaret på något av dessa frågor är Ja, **Stäng** misstänkt aktivitet (det är en godartad sann positiv) och Uteslut som är värdar för från den misstänkta aktiviteten.

3. Hämta information om aviseringen i ett Excel-kalkylblad för att visa listan över konto försök, uppdelat i befintliga och icke-existerande konton. Om du tittar på den icke befintliga konton blad i kalkylbladet och kontona Se bekant ut, de kan vara inaktiverade konton eller medarbetare som lämnat företaget. I det här fallet är det osannolikt att försöket kommer från en ordlista. Det är troligen ett program eller skript som kontrollerar om du vill se vilka konton som finns kvar i Active Directory, vilket innebär att det är en godartad sann positiv händelse.

3. Matchade någon av försök att gissa befintliga kontonamn i Active Directory om namn är i stort sett bekant? Om det finns inga matchningar, inloggningsförsöket futile, men du bör ta hänsyn till aviseringen för att se om det uppdateras med tiden.

4. Om någon av gissning försöker matcha befintliga kontonamn angriparen redan vet om förekomsten av konton i din miljö och försöka använda brute-force för att få åtkomst till din domän med identifierade användarnamnen. Kontrollera att gissa kontonamn för ytterligare misstänkta aktiviteter. Kontrollera om något av de matchade kontona är känsliga konton.


**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.


## <a name="reconnaissance-using-directory-services-queries"></a>Rekognosering med kontotjänstfrågor

**Beskrivning**

Rekognosering av katalogtjänster används av angripare för att mappa katalogstrukturen och Privilegierade målkonton för senare steg i ett angrepp. Security Account Manager Remote (SAM-R)-protokollet är en av metoderna som används för att fråga katalogen om du vill utföra sådan mappning.

Inga aviseringar skulle aktiveras i den första månaden efter att ATA har distribuerats i den här identifieringen. Under learning tiden ATA profilerna vilka SAM-R-frågor görs från vilka datorer både uppräkning och enskilda frågor för känsliga konton.

**Undersökning**

1. Klicka på aviseringen för att komma till dess informationssida. Kontrollera vilka frågor som har utförts (till exempel, Företagsadministratörer eller administratör) och om de lyckades.

2. Sådana frågor ska göras från käll-datorn i fråga?

3. Om Ja och aviseringen uppdateras **utelämna** den misstänkta aktiviteten.

4. Om Ja och den inte göra detta längre **Stäng** den misstänkta aktiviteten.

5. Om det finns information om kontot som ingår: typen av frågor ska göras av det kontot eller gör det kontot normalt logga in på källdatorn?

 - Om Ja och aviseringen uppdateras **utelämna** den misstänkta aktiviteten.

 - Om Ja och den inte göra detta längre **Stäng** den misstänkta aktiviteten.

 - Om svaret var inte till alla anges ovan förutsätter att detta är skadliga.

6. Om det finns ingen information om det konto som var inblandad, kan du gå till slutpunkten och kontrollera vilket konto som har loggats i vid tidpunkten för aviseringen.

**Reparation**

Använd den [SAMRi10 verktyget](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) att stärka din miljö mot den här tekniken.
Om verktyget inte gäller för din DC:
1. Datorn kör ett säkerhetsproblem sökverktyget?  
2. Undersök om vilken efterfrågade användare och grupper i angreppet är privilegierad eller hög värdekonton (d.v.s. VD, Ekonomichef, IT-hantering, osv.).  I så, fall kontrollera andra aktiviteter på slutpunkten samt och övervaka datorer som de efterfrågade kontona är inloggad på, eftersom de är förmodligen mål för lateral förflyttning.

## <a name="reconnaissance-using-dns"></a>Rekognosering med DNS

**Beskrivning**

DNS-servern innehåller en karta över alla datorer, IP-adresser och tjänster i nätverket. Den här informationen används av angripare för att mappa din nätverksinfrastruktur och för att angripa intressanta datorer i efterföljande steg i attacken.

Det finns flera frågetyper i DNS-protokollet. ATA identifierar AXFR (Transfer)-begäranden som kommer från icke-DNS-servrar.

**Undersökning**

1. Är källdatorn (**från...** ) en DNS-server? Om Ja, är detta förmodligen en falsk positiv identifiering. Verifiera genom att klicka på aviseringen för att komma till dess informationssida. I tabellen under **fråga**, kontrollera vilka domäner efterfrågades. Är dessa befintliga domäner? Om Ja, sedan **Stäng** den misstänkta aktiviteten (det är ett falsklarm). Dessutom kan du kontrollera att UDP-port 53 är öppen mellan ATA-gatewayen och måldatorn för att förhindra framtida falska positiva identifieringar.
2.  Källdatorn kör en Säkerhetsskanner? Om Ja, **undanta** entiteter i ATA, antingen direkt med **Stäng och undanta** eller via den **undantag** sida (under **Configuration** – tillgängligt för ATA-administratörer).
3.  Om svaret för alla föregående fråga är Nej, Behåll undersöka fokusera på källdatorn. Klicka på källdatorn för att gå till dess profilsida. Kontrollera vad skedde vid ungefär samma tid för begäran, söker efter ovanliga aktiviteter, till exempel: vem som har loggat in, vilka resurser där nås.


**Reparation**

Du kan skydda en intern DNS-server för att förhindra rekognosering med DNS genom att inaktivera eller begränsa zonöverföringar till endast angivna IP-adresser. Mer information om hur du begränsar zonöverföringar finns [begränsa zonöverföringar](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Ändringar av zonöverföringar är en av uppgifterna i en checklista som bör åtgärdas för [Skydda DNS-servrar från både interna och externa attacker](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognosering med SMB-sessionsuppräkning


**Beskrivning**

Uppräkning av Server Message Block (SMB) gör det möjligt för angripare att få information där användare nyligen har loggat in. När angripare har den här informationen kan kan de flytta sidled i nätverket till en specifik känsligt konto.

I den här identifieringen utlöses en avisering när en SMB-sessionsuppräkning utförs mot en domänkontrollant, eftersom det inte borde ske.

**Undersökning**

1. Klicka på aviseringen för att komma till dess informationssida. Kontrollera vilken kontot/s utförde åtgärden och vilka konton som exponerades, om sådana.

 - Finns det någon typ av Säkerhetsskanner som körs på källdatorn? Om Ja, **Stäng och undanta** den misstänkta aktiviteten.

2. Kontrollera vilka som ingår användare/s utförde åtgärden. Gör de normalt logga in på källdatorn eller är de administratörer som ska användas till detta?  

3. Om Ja och aviseringen uppdateras **utelämna** den misstänkta aktiviteten.  

4. Om Ja och den inte göra detta längre **Stäng** den misstänkta aktiviteten.

5. Om svaret på alla ovanstående är förutsätter Nej, det här är skadliga.

**Reparation**

Använd den [Net upphöra verktyget](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) att stärka din miljö mot angrepp.

## <a name="remote-execution-attempt-detected"></a>Försök till fjärrkörning har identifierats

**Beskrivning**

Angripare som äventyra administratörsbehörighet eller använder en nolldagsattacker utnyttja kan köra fjärrkommandon på domänkontrollanten. Detta kan användas för att få beständighet, samla in information, denial of service (DOS)-attacker eller någon annan anledning. ATA identifierar PSexec- och fjärr-WMI-anslutningar.

**Undersökning**

1. Detta är vanligt för administrativa arbetsstationer samt IT-teammedlemmar och tjänstkonton som utför administrativa uppgifter mot domänkontrollanterna. Om det här är det här fallet och aviseringen uppdateras eftersom samma admin eller datorn utför aktiviteten, sedan **utelämna** aviseringen.
2.  Är datorn i fråga tillåtet att utföra den här fjärrkörningen mot din domänkontrollant?
  - Kontot i fråga kan utföra den här fjärrkörningen mot din domänkontrollant?
  - Om svaret på båda frågor är Ja, sedan **Stäng** aviseringen.
3.  Om svaret på båda frågor är Nej, sedan detta bör beaktas en sann positiv händelse. Försök att hitta källan för försöket genom att kontrollera dator och kontonamn profiler. Klicka på källdatorn eller konto för att gå till dess profilsida. Kontrollera vad som hände ungefär samma tidpunkt som dessa försök söka efter ovanliga aktiviteter, till exempel: vem som har loggat in, vilka resurser där nås.


**Reparation**

1. Begränsa fjärråtkomst till domänkontrollanter från datorer som inte är Nivå 0-datorer.

2. Implementera [privilegierad åtkomst](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) till att endast härdade datorer att ansluta till domänkontrollanter för administratörer.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Känsliga kontouppgifter avslöjas & tjänster exponerar kontoautentiseringsuppgifter

> [!NOTE]
> Den här misstänkt aktivitet är inaktuell och visas bara i ATA-versioner före 1.9. ATA 1.9 och senare, finns i avsnittet [rapporter](reports.md).

**Beskrivning**

Vissa tjänster skickar autentiseringsuppgifter i klartext. Detta kan även inträffa för känsliga konton. Angripare som övervakar nätverkstrafiken kan fånga upp och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. Alla lösenord i klartext för ett känsligt konto utlöser aviseringen, medan för icke-känsliga konton som varningen utlöses om fem eller fler olika konton skickar lösenord i klartext från samma källdator. 

**Undersökning**

Klicka på aviseringen för att komma till dess informationssida. Se vilka konton som exponerades. Om det finns många konton, klickar du på **Hämtningsinformation** att visa en lista i ett Excel-kalkylblad.

Det är vanligtvis ett skript eller äldre program på källdatorerna som använder enkel LDAP-bindning.

**Reparation**

Kontrollera konfigurationen på källdatorerna och se till att du inte använder enkel LDAP-bindning. Du kan använda LDAP SALS eller LDAPS i stället för enkla LDAP-bindningar.

## <a name="suspicious-authentication-failures"></a>Misstänkta autentiseringsfel

**Beskrivning**

En angripare försöker autentisera med många olika lösenord för olika konton tills rätt lösenord hittas för minst ett konto i en brute force-attack. Hitta en gång, kan en angripare logga in med det kontot.

I den här identifieringen en avisering utlöses när många autentiseringsfel med Kerberos eller NTLM inträffade, det kan vara antingen vågrätt med en liten uppsättning lösenord över många användare. eller lodrätt med en stor uppsättning lösenord på bara några få användare. eller en kombination av de här två alternativen. Minsta tid ska gå innan en avisering aktiveras är en vecka.

**Undersökning**

1.  Klicka på **Hämtningsinformation** Visa fullständig information i ett Excel-kalkylblad. Du kan få följande information: 
  - Lista över angripna konton
  - Lista över gissade konton i vilken inloggningsförsök avslutades med lyckad autentisering
  - Om autentiseringsförsök har utförts med hjälp av NTLM, visas relevanta händelseaktiviteter 
  - Om autentiseringsförsök har utförts med Kerberos, visas relevanta Nätverksaktiviteter
2.  Klicka på källdatorn för att gå till dess profilsida. Kontrollera vad som hände ungefär samma tidpunkt som dessa försök söka efter ovanliga aktiviteter, till exempel: vem som har loggat in, vilka resurser där nås. 
3.  Om autentiseringen har utförts med hjälp av NTLM och du ser att aviseringen uppstår flera gånger, och det finns inte tillräckligt med information om den server som källdatorn försökte få åtkomst till, bör du aktivera **NTLM granskning** på den domänkontrollanter som ingår. Gör detta genom att aktivera event 8004. Detta är den NTLM-autentisering-händelse som omfattar information om källdatorn, användarkontot och **server** som källdatorn försökte få åtkomst till. När du vet vilken servern skickade valideringen av autentisering, bör du undersöka servern genom att markera händelser som 4624 att bättre förstå autentiseringsprocessen. 


**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.

## Misstänkt skapande av tjänst <a name="suspicious-service-creation"></a>

**Beskrivning**

Angripare försöker köra misstänkta tjänster i nätverket. ATA genererar en avisering när en ny tjänst som verkar misstänkt har skapats på en domänkontrollant. Den här aviseringen är beroende av händelsen 7045 och den identifieras från varje domänkontrollant som omfattas av en ATA Gateway eller Lightweight Gateway.

**Undersökning**

1. Om datorn i fråga är en administrativ arbetsstation, eller en dator på vilken IT-teammedlemmar och tjänsten konton för att utföra administrativa uppgifter, detta kan vara en falsk positiv identifiering och du kan behöva **utelämna** aviseringen och lägger till den i den Undantagslistan om det behövs.

2. Är tjänsten något du känner igen på den här datorn?

 - Är den **konto** i fråga kan installera den här tjänsten?

 - Om svaret på båda frågor är *Ja*, sedan **Stäng** aviseringen eller lägga till den i undantagslistan.

3. Om svaret på båda frågor är *inga*, och sedan detta bör beaktas en sann positiv händelse.

**Reparation**

- Implementera mindre privilegierade åtkomst på datorer i domänen så att endast specifika användare behörighet att skapa nya tjänster.



## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Misstanke om identitetsstöld baserat på onormalt beteende

**Beskrivning**

ATA lär sig entitetsbeteende för användare, datorer och resurser under en glidande tre veckor. Beteende-modell som baseras på följande aktiviteter: datorerna entiteterna som inloggad på, de resurser som entiteten begärt åtkomst till och den tid som de här åtgärderna ägde rum. ATA skickar en avisering när det finns en avvikelse från entitetens beteende baserat på machine learning-algoritmer. 

**Undersökning**

1. Användaren i fråga ska att utföra dessa åtgärder?

2. Överväg följande fall som potentiellt falska positiva identifieringar: en användare som returneras från semester, IT-personal som utför ytterligare åtkomst som en del av sin användning (till exempel en topp i helpdesk-stöd i en viss dag eller en vecka), remote desktop program. + Om du **Stäng och undanta** aviseringen, användare som inte längre vara en del av identifieringen


**Reparation**

Beroende på vad som orsakade det här onormalt beteende ska ske, olika åtgärder som vidtas. Till exempel om det är på grund av genomsökning av nätverket kan ska den datorn där detta inträffade blockeras från nätverket (om det har godkänts).

## <a name="unusual-protocol-implementation"></a>Onormal protokollimplementering


**Beskrivning**

Angripare använda verktyg som implementerar olika protokoll (SMB, Kerberos, NTLM) på vanligt sätt. Även om den här typen av nätverkstrafik godkänns av Windows utan varningar, kan ATA identifiera potentiella skadliga avsikter. Beteendet är en indikation på tekniker som over-pass-the-Hash, samt kryphål som används av avancerade utpressningstrojaner, till exempel wannacry-angrepp.

**Undersökning**

Identifiera det protokoll som är ovanligt – från tidslinjen för misstänkt aktivitet, klickar du på den misstänkta aktiviteten till dess informationssida; protokollet visas ovanför pilen: Kerberos eller NTLM.

- **Kerberos**: detta ofta utlöses om ett kodar verktyget som Mimikatz har använts kan eventuellt utföra en Overpass-the-Hash-attack. Kontrollera om källdatorn körs ett program som implementerar sin egen Kerberos-stacken, inte i enlighet med Kerberos RFC. Om så är fallet, är det en godartad sann positiv händelse och du kan **Stäng** aviseringen. Om aviseringen håller utlöses och det fortfarande är fallet, kan du **utelämna** aviseringen.

- **NTLM**: kan vara antingen WannaCry eller verktyg som Metasploit, Medusa och Hydra.  

För att avgöra om detta är en WannaCry-attack, utför du följande steg:

1. Kontrollera om källdatorn körs ett angrepp verktyg som Metasploit, Medusa eller Hydra.

2. Om det finns inga attack verktyg kan du kontrollera om källdatorn kör ett program som implementerar sin egen NTLM- eller SMB-stacken.

3. Om det inte kontrollera om detta orsakas av wannacry-angrepp genom att köra ett WannaCry-skannern skript, till exempel [skannern](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) mot källdatorn som ingår i den misstänkta aktiviteten. Om skannern hittar som datorn som infekterade eller sårbara, arbetet med korrigeringar på datorn och ta bort den skadliga koden och blockerar den från nätverket.

4. Om skriptet inte hittar att datorn är infekterade eller sårbara och det fortfarande vara smittade men SMBv1 kan ha inaktiverats eller har konfigurerats för datorn, vilket påverkar genomsökningsverktyget.

**Reparation**

Korrigera alla datorer, särskilt användning av säkerhetsuppdateringar.

1. [Inaktivera SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Ta bort wannacry-angrepp](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi kan dekryptera data i händerna på vissa ransom program, men endast om användaren inte har startats om eller stängs av datorn. Mer information finns i [vill Cry Utpressningstrojaner](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


>[!NOTE]
> Kontakta supporten om du vill inaktivera en misstänkt aktivitet.

## <a name="related-videos"></a>Relaterade videor
- [Koppla säkerhets-communityn](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Se även
- [Spelboken för ATA-misstänkt aktivitet](http://aka.ms/ataplaybook)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
