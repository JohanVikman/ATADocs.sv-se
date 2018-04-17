---
title: Azure ATP misstänkt aktivitet guide | Microsoft Docs
d|Description: This article provides a list of the suspicious activities Azure ATP can detect and steps for remediation.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6246849cf7e8566b27c969b73e9c96cb0e7b7978
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/16/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-suspicious-activity-guide"></a>Azure Advanced Threat Protection misstänkt aktivitet guide

Följande rätt undersökningen eventuell misstänkt aktivitet kan klassificeras som:

-   **True positiva**: en skadlig åtgärd som identifieras av Azure ATP.

-   **Ofarlig true positiva**: en åtgärd som identifieras av Azure ATP som är verkliga men inte skadlig, till exempel ett intrång test.

-   **Falsklarm**: ett larm som false, vilket betyder att aktiviteten inte inträffa.

Mer information om hur du arbetar med Azure ATP aviseringar finns [arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md).


## <a name="abnormal-sensitive-group-modification"></a>Onormal modifiering av känslig grupp


**Beskrivning**

Angripare kan du lägga till användare i mycket Privilegierade grupper. De gör att få tillgång till fler resurser och få lagring. Identifieringen är beroende av profilering av ändring gruppaktiviteter för användare och avisering när ett onormalt tillägg till en känslig grupp visas. Profilering utförs kontinuerligt av ATP. Minsta tid innan en avisering kan utlösas är en månad per varje domänkontrollant.

En definition av känsliga grupper i Azure ATP finns [arbeta med känsliga konton](sensitive-accounts.md).


Identifieringen förlitar sig på [händelser granskas på domänkontrollanter](configure-event-collection.md).
Kontrollera att din domän granska domänkontrollanter nödvändiga händelser.

**Undersökning**

1. Är den grupp ändringen legitima? </br>Legitima grupp ändringar som sällan inträffar och inte lärt dig som ”normal”, kan leda till en avisering som kan betraktas som ett ofarlig true positivt.

2. Om objektet lagts till ett användarkonto, ska du kontrollera vilka åtgärder som användarkonton som tog efter att den lagts till i administratörsgruppen. Gå till sidan för användaren i Azure ATP få mer kontext. Misstänkta aktiviteter som är associerat med kontot före eller efter det att det har andra ägde rum? Hämta den **känsliga grupp ändras** rapporten för att se vad andra ändringar har gjorts och av vem under samma tidsperiod.

**Reparation**

Minimera antalet användare som har behörighet att ändra känsliga grupper.

Ställ in [Privileged Access Management för Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) om tillämpligt.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Nyckelsökningsangrepp med enkla LDAP-bindning

**Beskrivning**

>[!NOTE]
> Den största skillnaden mellan **misstänkta autentiseringsfel** och denna identifiering är att Azure ATP i denna identifiering kan avgöra om olika lösenord användes.

En angripare försöker autentisera med många olika lösenord för olika konton förrän rätt lösenord hittades för minst ett konto i en brute force-attacker. En gång hittades kan en angripare logga in med det kontot.

I denna identifiering utlöses en avisering när Azure ATP identifierar ett stort antal enkel bindning autentiseringar. Detta kan vara antingen *vågrätt* med en liten uppsättning lösenord för många användare, eller *lodrätt ”* med ett stort utbud av lösenord på bara några få användare; eller en kombination av de här två alternativen.

**Undersökning**

1. Om det finns många konton som ingår, klickar du på **hämta information** att visa en lista i Excel.

2. Klicka på aviseringen för att gå till en särskild sida. Kontrollera om alla inloggningsförsök avslutades med en lyckad autentisering. Försöker visas som **gissa konton** på höger sida av infographic. Om Ja, är några av de **gissa konton** normalt används från källdatorn? Om Ja, **utelämna** misstänkt aktivitet.

3. Om det finns inga **gissa konton**, är några av de **angripna konton** normalt används från källdatorn? Om Ja, **utelämna** misstänkt aktivitet.

**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.

## <a name="encryption-downgrade-activity"></a>Kryptering för nedgradering av aktiviteten

**Beskrivning**

Nedgradering av kryptering är en metod för lägre Kerberos av nedgradera krypteringsnivån för olika fält i protokollet som vanligtvis är krypterade med den högsta nivån av kryptering. En lägre krypterade fältet kan vara ett enklare mål offline brute force försöken. Olika metoder för attack använda svaga produktidentifieringsförteckning för Kerberos-kryptering. I denna identifiering Azure ATP lär sig Kerberos krypteringstyper som används av datorer och användare och varnar dig när en svagare korrekt är att använda den: (1) är ovanligt för källdatorn och/eller användare. och (2) matchar kända attacker tekniker.

Det finns tre typer av identifiering:

1.  Skadlig Skeleton Key – är skadlig kod som körs på domänkontrollanter och tillåter autentisering i domänen med ett konto utan att känna till lösenordet. Den här skadliga koden använder ofta svagare krypteringsalgoritmer till hash-lösenord på domänkontrollanten. I denna identifiering har kryptering för att KRB_ERR-meddelande från domänkontrollanten till det konto som ber om en tjänstbiljett nedgraderas jämfört med tidigare inlärda beteende.

2.  Guld biljett – i en [Golden Ticket](#golden-ticket) aviseringen krypteringsmetod i fältet TGT för TGS_REQ (service request) meddelande från källdatorn har nedgraderas jämfört med tidigare inlärda beteende. Detta baseras inte på en gång avvikelseidentifiering (som andra Golden Ticket identifieringen). Dessutom kan det fanns ingen begäran om Kerberos-autentisering som är associerade med den tidigare tjänstbegäran som identifieras av ATP.

3.  Overpass-the-Hash – en angripare kan använda en svag stulen hash för att skapa en stark biljett med en Kerberos-AS-begäran. I denna identifiering AS_REQ kryptering meddelandetypen från källdatorn har nedgraderas jämfört med tidigare inlärda beteendet (det vill säga datorn var med AES).

**Undersökning**

Kontrollera först beskrivningen av aviseringen, för att se vilken av ovanstående tre identifiering typer du hantera. Undersökningen först kontrollera beskrivningen av aviseringen för att se vilken av ovanstående tre identifiering typer du hantera. För ytterligare information, hämta Excel-kalkylblad.

1.  Skadlig Skeleton Key – du kan kontrollera om Skeleton Key påverkar domänkontrollanter med hjälp av [skannern skrivs av Azure ATP-teamet](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Om skannern hittar skadlig kod på 1 eller flera domänkontrollanter, är det ett true positivt.

2.  Golden Ticket – i excel-kalkylblad, gå till fliken nätverk aktivitet. Du ser att relevanta nedgraderat fältet är **begära biljett krypteringstyp**, och **källa stöds kryptering datortyper** innehåller starkare kryptering.

  1. Kontrollera käll- och kontot, eller om det finns flera källdatorer och konton kontrollerar du om de har något gemensam (till exempel alla som marknadsföring personal använder en viss app som gör att aviseringen ska utlösas). Finns det fall där ett anpassat program som används sällan autentiseras med hjälp av en lägre kryptering cipher. Kontrollera om det finns några anpassade appar på källdatorn. I så fall, är förmodligen ett ofarlig true positivt och kan förhindras.
  
  2. Kontrollera resursen via dessa biljetter, om det finns en resurs som de alla använder, verifiera den, kontrollera att den är en giltig resurs som de ska komma åt. Kontrollera också om målresurs stöder stark kryptering. Du kan kontrollera detta i Active Directory genom att kontrollera det attributet msDS-SupportedEncryptionTypes-namn, för resurs-tjänstkontot.

3.  Overpass-the-Hash – i excel-kalkylblad, gå till fliken nätverk aktivitet. Du ser att relevanta nedgraderat fältet är **krypterade tidsstämpel krypteringstyp** och **källa stöds kryptering datortyper** innehåller starkare kryptering.

  1. Finns det fall där den här aviseringen kan utlösas när användare loggar in med smartkort om smartkort konfigurationen ändrades senast. Kontrollera om det fanns ändringar så här för konton ingår. I så fall, detta är troligen ett ofarlig true positivt och kan förhindras.
  2. Kontrollera resursen via dessa biljetter, om det finns en resurs som de alla använder, verifiera den, kontrollera att den är en giltig resurs som de ska komma åt. Kontrollera också om målresurs stöder stark kryptering. Du kan kontrollera detta i Active Directory genom att kontrollera det attributet msDS-SupportedEncryptionTypes-namn, för resurs-tjänstkontot.

**Reparation**

1.  Stommen Key – ta bort den skadliga koden. Mer information finns i [Skeleton Key skadlig kod Analysis](https://www.secureworks.com/research/skeleton-key-malware-analysis) av SecureWorks.

2.  Gyllene biljett – Följ instruktionerna för den [Golden Ticket](#golden-ticket) misstänkta aktiviteter.   
    Dessutom eftersom skapar Golden Ticket kräver administratörsrättigheter i domänen, implementera [skicka hash-rekommendationer](http://aka.ms/PtH).

3.  Overpass-the-Hash – återställa om kontot ingår inte är skiftlägeskänslig, sedan lösenordet för kontot. Detta förhindrar att angripare skapar nya Kerberos-biljetter från lösenords-hash, även om befintliga biljetter kan fortfarande användas tills de upphör att gälla. Om det är känsligt konto bör du återställa KRBTGT-kontot två gånger som Golden Ticket misstänkt aktivitet. Återställer KRBTGT två gånger upphäver alla Kerberos biljetter i den här domänen så planerar innan du gör det. Se vägledningen i [KRBTGT-kontot lösenord återställa skript finns nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Se även med hjälp av den [återställa verktyget KRBTGT-kontot lösenord/nycklar](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Eftersom det är en teknik som lateral förflyttning följer bästa praxis för [skicka hash-rekommendationer](http://aka.ms/PtH).

## Golden Ticket<a name="golden-ticket"></a>

**Beskrivning**

Angripare med administratörsrättigheter i domänen kan påverka den [KRBTGT-kontot](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). De kan använda KRBTGT-kontot för att skapa Kerberos biljettbeviljande biljetter (TGT) som ger behörighet till en resurs och som helst godtycklig biljett upphör att gälla. Den här falska TGT kallas ”Golden Ticket” och tillåter angripare att uppnå lagring i nätverket.

I denna identifiering en avisering utlöses när en Kerberos-biljett beviljande biljetter används för mer än den tillåtna tiden tillåts som anges i den [högsta livstid för användarbiljett](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) säkerhetsprincip.

**Undersökning**

1. Det har alla nyligen (inom de senaste några timmarna) ändringar på den **högsta livstid för användarbiljett** i Grupprincip? Om Ja, sedan **Stäng** aviseringen (den var ett falsklarm).

2. Är Azure ATP fristående sensor ingår i en virtuell dator för den här aviseringen? Om Ja, den nyligen återupptas från ett sparat tillstånd? Om Ja, sedan **Stäng** aviseringen.

3. Om svaret på dessa frågor är Nej, förutsätter att det här är skadliga.

**Reparation**

Ändra Kerberos-biljett beviljande biljetter (KRBTGT) lösenord två gånger enligt riktlinjerna i [KRBTGT-kontot lösenord återställa skript finns nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)med hjälp av den [återställa KRBTGT-kontot lösenord/nycklar verktyget](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Återställer KRBTGT två gånger upphäver alla Kerberos biljetter i den här domänen så planerar innan du gör det. Dessutom eftersom skapar Golden Ticket kräver administratörsrättigheter i domänen, implementera [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Honeytoken-aktivitet


**Beskrivning**

Honeytoken-konton är decoy konton som skapas för att identifiera och spåra skadliga aktiviteter som omfattar dessa konton. Honeytoken-konton ska lämnas oanvända, samtidigt som du har en bra namn till locka angripare (till exempel SQL-administratör). Alla aktiviteter från dem kan tyda på skadligt beteende.

Mer information om honeytoken konton finns [installera Azure ATP - steg 7](install-atp-step7.md).

**Undersökning**

1.  Kontrollera om honeytokenkonto används ägaren av källdatorn för att autentisera, med den metod som beskrivs i sidan misstänkt aktivitet (exempelvis Kerberos, LDAP, NTLM).

2.  Bläddra till datakällan datorer profilsidor och kontrollera vilka konton som autentiseras från dem. Kontrollera med ägarna av dessa konton om de används i honeytokenkonto.

3.  Detta kan vara en icke-interaktiv inloggning, så se till att söka efter program eller skript som körs på källdatorn.

Om när du utför steg 1 till 3, om det inte finns några tecken på ofarlig användning måste anta att detta är skadliga.

**Reparation**

Se till att Honeytoken konton används endast för deras syfte, annars många aviseringar kan genereras.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Identitetsstöld med Pass-the-Hash-attack

**Beskrivning**

Pass the Hash är en lateral förflyttning teknik där angriparen stjäl en användares NTLM-hash från en dator och använda den för att få åtkomst till en annan dator. 

**Undersökning**

Användes hash från en dator som den aktuella användaren äger eller regelbundet använder? Om Ja, det är ett falsklarm. Om inte, är förmodligen ett true positivt.

**Reparation**

1. Om kontot ingår inte är känslig sedan återställa lösenordet för kontot. Detta förhindrar att angripare skapar nya Kerberos-biljetter från lösenords-hash, även om befintliga biljetter kan fortfarande användas tills de upphör att gälla. 

2. Om det är känsligt konto bör du återställa KRBTGT-kontot två gånger som Golden Ticket misstänkt aktivitet. Återställer KRBTGT två gånger upphäver alla Kerberos biljetter i den här domänen så planerar innan du gör det. Finns i [KRBTGT-kontot lösenord återställa skript finns nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), även finns med i [återställa verktyget KRBTGT-kontot lösenord/nycklar](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Eftersom det är en teknik som lateral förflyttning följer bästa praxis för [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitetsstöld med Pass-the-Ticket-attacker

**Beskrivning**

Pass the Ticket är en lateral förflyttning teknik som stjäl angriparen en Kerberos-biljett från en dator och använda den för att få åtkomst till en annan dator genom att återanvända den stulna biljetten. I denna identifiering visas en Kerberos-biljett används på två (eller fler) olika datorer.

**Undersökning**

1. Klicka på den **hämta information** för att visa en fullständig lista över IP-adresser som ingår. Lagrar IP-adressen för en eller båda datorerna hör till ett undernät som allokeras från en DHCP-adresspool som inte uppfyller till exempel VPN eller Wi-Fi? Delas IP-adress Till exempel genom en NAT-enhet? Är en eller flera av käll-IP-adresser som inte matchas av sensorn? (Detta kan tyda på att rätt portar från sensorn till enheter inte korrekt öppnas.) Om svaret på någon av dessa frågor är Ja, är det ett falsklarm.

2. Finns det ett anpassat program som vidarebefordrar biljetter åt användare? I så fall, är ett ofarlig true positivt.

**Reparation**

1. Om kontot ingår inte är känslig sedan återställa lösenordet för kontot. Detta förhindrar att angripare skapar nya Kerberos-biljetter från lösenords-hash, även om befintliga biljetter kan fortfarande användas tills de upphör att gälla.  

2. Om det är känsligt konto bör du återställa KRBTGT-kontot två gånger som Golden Ticket misstänkt aktivitet. Återställer KRBTGT två gånger upphäver alla Kerberos biljetter i den här domänen så planerar innan du gör det. Finns i [KRBTGT-kontot lösenord återställa skript finns nu tillgängligt för kunder](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), även finns med i [återställa verktyget KRBTGT-kontot lösenord/nycklar](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Eftersom det är en teknik som lateral förflyttning, följ rekommenderade metoder i [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="malicious-data-protection-private-information-request"></a>Skadlig privat informationsbegäran för dataskydd

**Beskrivning**

Data Protection API (DPAPI) används av Windows för att skydda lösenord som sparas av webbläsare, krypterade filer och andra känsliga data på ett säkert sätt. Domänkontrollanter håller en säkerhetskopiering huvudnyckel som kan användas för att dekryptera alla hemligheter som krypterats med DPAPI på domänanslutna Windows-datorer. Angripare kan använda den huvudnyckeln för att dekryptera alla hemligheter som skyddas av DPAPI på alla domänanslutna datorer.
I denna identifiering utlöses en avisering när av DPAPI används för att hämta huvudnyckeln för säkerhetskopiering.

**Undersökning**

1. Källdator som kör en organisation godkända är en avancerad säkerhetsskannern mot Active Directory?

2. Om Ja och den bör alltid att göra det, **Stäng och utelämna** misstänkt aktivitet.

3. Om Ja och den bör inte göra detta, **Stäng** misstänkt aktivitet.

**Reparation**

Om du vill använda DPAPI måste en angripare administratörsrättigheter i domänen. Implementera [skicka hash-rekommendationer](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Skadliga replikeringsbegäranden


**Beskrivning**

Active Directory-replikering är en process som synkroniseras ändringar som gjorts på en domänkontrollant med andra domänkontrollanter. Ges behörighet kan angripare initiera en replikeringsbegäran så att de kan hämta data som lagras i Active Directory, inklusive lösenordshashvärden.

I denna identifiering utlöses en avisering när en replikeringsbegäran om initieras från en dator som inte är en domänkontrollant.

**Undersökning**

1.  Är datorn i fråga en domänkontrollant? Till exempel en nyligen uppgraderat domänkontrollant som hade replikeringsproblem. Om Ja, **Stäng** misstänkt aktivitet. 
2.  Datorn i fråga ska vara replikering av data från Active Directory? Till exempel Azure AD Connect. Om Ja, **Stäng och utelämna** misstänkt aktivitet.
3.  Klicka på källdatorn igen eller konto för att gå till sidan sin profil. Kontrollera vad hände vid ungefär samma tidpunkt replikering, söka efter ovanliga aktiviteter, t.ex: som loggades i vilka resurser där nås. Om du har aktiverat Windows Defender ATP-integration klickar du på Windows Defender ATP-skylt ![Windows Defender ATP-skylt](./media/wd-badge.png) ytterligare undersöka datorn. I Windows Defender ATP ser du vilka processer och -varningar uppstod vid ungefär samma tidpunkt för aviseringen. 


**Reparation**

Verifiera följande behörigheter: 

- Replikera katalogändringar   

- Replikera alla katalogändringar  

Mer information finns i [bevilja Active Directory Domain Services-behörigheter för profilsynkronisering i SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Du kan utnyttja [AD Åtkomstkontrollista Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) eller skapa ett Windows PowerShell-skript för att fastställa vem i domänen har dessa behörigheter.


## <a name="password-exposed-in-cleartext-report"></a>Lösenord i klartext rapport

**Beskrivning**

Vissa tjänster skickar autentiseringsuppgifter i klartext. Detta kan även inträffa för användarkonton. Övervaka nätverkstrafik angripare kan fånga och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. 

**Undersökning**

Klicka på sidan rapporter och hämta lösenordet i klartext rapporten. Se vilka konton som exponerats i Excel-kalkylblad.
Det är vanligtvis ett skript eller äldre program på källdatorer som använder enkel LDAP-bindning.

**Reparation**

Kontrollera konfigurationen på källdatorerna och se till att du inte använder enkel LDAP-bindning. Du kan använda LDAP sal eller LDAPS istället för att använda enkla LDAP-bindningar.

## <a name="privilege-escalation-using-forged-authorization-data"></a>Privilegiet eskalering med förfalskad auktoriseringsdata

**Beskrivning**

Kända säkerhetsproblem i äldre versioner av Windows Server göra att angripare kan manipulera den privilegierade Attribute Certificate (PAC), ett fält i Kerberos-biljetten som innehåller en auktoriseringsdata för användare (i Active Directory är detta gruppmedlemskap), bevilja angripare ytterligare behörighet.

**Undersökning**

1. Klicka på aviseringen för att komma åt dess informationssidan.

2. Är måldatorn (under den **ACCESSED** kolumn) korrigeras med MS14-068 (domänkontrollanten) eller MS11-013 (server)? Om Ja, **Stäng** misstänkt aktivitet (det är ett falsklarm).

3. Om inte, körs på källdatorn (under den **FROM** kolumn) ett program eller det OS känt att ändra PAC? Om Ja, **utelämna** misstänkt aktivitet (det är ett ofarlig true positivt).

4. Om svaret var inte förutsätter detta är skadliga att dessa två frågor.

**Reparation**

Kontrollera att alla domänkontrollanter med operativsystem upp till Windows Server 2012 R2 är installerade med [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) och att alla medlemsservrar och domänkontrollanter upp till 2012 R2 är uppdaterade med KB2496930. Mer information finns i avsnitten om [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) och [förfalskat PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekognosering med kontouppräkning

**Beskrivning**

En ordlista använder med tusentals användarnamn eller verktyg, till exempel KrbGuess en angripare konto uppräkningen rekognosering, för att försöka gissa användarnamn i din domän. Angriparen gör Kerberos-begäranden som använder dessa namn för att försöka hitta ett giltigt användarnamn i din domän. Om en viss avgör har ett användarnamn, angriparen hämtar Kerberos-fel **förautentisering krävs** i stället för **säkerhetsobjekt okänd**. 

I denna identifiering identifiera Azure ATP var angreppet kommer ifrån, det totala antalet gissning försök och hur många matchade. Om det finns för många okända användare, identifierar Azure ATP den som en misstänkt aktivitet. 

**Undersökning**

1. Klicka på aviseringen för att komma åt dess informationssidan. 

2. Den här värddatorn ska fråga domänkontrollanten att om konton finns (till exempel Exchange-servrar)? <br></br>
Finns det ett skript eller ett program som körs på värden som kan generera det här problemet? <br></br>
Om svaret på någon av dessa frågor är Ja, **Stäng** misstänkt aktivitet (det är ett ofarlig true positivt) och utelämna som värd för från den misstänkta aktiviteten.

3. Hämta information om aviseringen i ett Excel-kalkylblad för att visa listan över konto försök indelat i befintliga och icke-befintliga konton. Om du tittar på det icke befintliga konton blad i kalkylbladet och kontona känner, de kan vara inaktiverade konton eller medarbetare som lämnar företaget. I det här fallet är det osannolikt att försöket kommer från en uppslagslista. Det är troligen ett program eller skript som kontrollerar om du vill se vilka konton fortfarande finns i Active Directory, vilket innebär att det är ett ofarlig true positivt.

3. Matchade någon gissning försöker befintliga kontonamn i Active Directory om namnen inte är i stort sett bekant? Om det finns inga matchningar, gick futile, men du bör du vara uppmärksam på aviseringen för att se om den uppdateras med tiden.

4. Om någon av gissning försöker matcha befintliga kontonamn angriparen känner av att finns konton i din miljö och försöka använda brute-force för att få åtkomst till din domän med hjälp av de identifierade namn. Kontrollera att gissa kontonamn för ytterligare misstänkta aktiviteter. Kontrollera om något av de matchade kontona är känsliga konton.


**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.


## <a name="reconnaissance-using-directory-services-queries"></a>Rekognosering med kontotjänstfrågor

**Beskrivning**

Directory services rekognosering används av angripare att mappa katalogstrukturen och rikta Privilegierade konton för senare steg i en attack. Fjärråtkomst för hanteraren för kontosäkerhet (SAM-R)-protokollet är en av metoderna som används för att fråga katalogen om du vill utföra sådan mappning.

Inga aviseringar skulle aktiveras i den första månaden när Azure ATP har distribuerats i denna identifiering. Under learning tiden Azure ATP profilerna där SAM-R-frågor kommer från vilka datorer både uppräkningen och enskilda frågor för känsliga konton.

**Undersökning**

1. Klicka på aviseringen för att komma åt dess informationssidan. Kontrollera vilka frågor som har utförts (till exempel, Företagsadministratörer eller administratör) och om de lyckades.

2. Sådana frågor ska göras från källdatorn i fråga?

3. Om Ja och aviseringen uppdateras **utelämna** misstänkt aktivitet.

4. Om Ja och den bör inte detta längre **Stäng** misstänkt aktivitet.

5. Om det finns information om kontot ingår: sådana frågor ska göras av det kontot eller har kontot normalt logga in på källdatorn?

 - Om Ja och aviseringen uppdateras **utelämna** misstänkt aktivitet.

 - Om Ja och den bör inte detta längre **Stäng** misstänkt aktivitet.

 - Om svaret var inte till alla anges ovan förutsätter att det här är skadliga.

6. Om det finns ingen information om det konto som är involverad, kan du gå till slutpunkten och kontrollera vilket konto som har loggats i vid tidpunkten för aviseringen.

**Reparation**

Skydda din miljö mot den här tekniken på följande sätt:
1. Datorn som kör en säkerhetsrisk genomsökning verktyget?  
2. Undersök om efterfrågade användare och grupper i angrepp är Privilegierade eller hög värdekonton (det vill säga VD, Ekonomichef, IT-hantering, osv.).  I så fall, kontrollera andra aktiviteter på slutpunkten samt och övervaka datorer som de efterfrågade kontona är inloggad på, eftersom de är förmodligen mål för lateral förflyttning.

## <a name="reconnaissance-using-dns"></a>Rekognosering med DNS

**Beskrivning**

DNS-servern innehåller en karta över alla datorer, IP-adresser och tjänster i nätverket. Den här informationen används av angripare för att mappa din nätverksinfrastruktur och för att angripa intressanta datorer i efterföljande steg i attacken.

Det finns flera frågetyper i DNS-protokollet. Azure ATP identifierar AXFR (Transfer) begäran kommer från icke-DNS-servrar.

**Undersökning**

1. Är källdatorn (**härstammar från...** ) en DNS-server? Om Ja, är detta troligen ett falsklarm. Om du vill validera, klickar du på aviseringen till dess informationssidan. I tabellen, under **frågan**, kontrollera vilka domäner frågades. Är de befintliga domänerna? Om Ja, sedan **Stäng** misstänkt aktivitet (det är ett falsklarm). Kontrollera dessutom att UDP-port 53 är öppen mellan Azure ATP fristående sensor och källdatorn för att förhindra framtida falska positiva identifieringar.

2. Körs på källdatorn en säkerhetsskannern? Om Ja, **undanta entiteterna** i ATP, antingen direkt med **Stäng och utelämna** eller via den **undantag** sida (under **Configuration** – tillgängligt för Azure ATP-administratörer).

3. Om svaret på alla föregående frågor är Nej, hålla undersöker fokusera på källdatorn. Klicka på källdatorn för att gå till sidan sin profil. Kontrollera vad inträffat runt samma tid för begäran, söka efter ovanliga aktiviteter, t.ex: som loggades i vilka resurser där nås. Om du har aktiverat Windows Defender ATP-integration klickar du på Windows Defender ATP-skylt ![Windows Defender ATP-skylt](./media/wd-badge.png) ytterligare undersöka datorn. I Windows Defender ATP ser du vilka processer och -varningar uppstod vid ungefär samma tidpunkt för aviseringen. 

**Reparation**

Du kan skydda en intern DNS-server för att förhindra rekognosering med DNS genom att inaktivera eller begränsa zonöverföringar till endast angivna IP-adresser. Mer information om hur du begränsar zonöverföringar finns [begränsa zonöverföringar](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Ändra zonöverföringar är en aktivitet i en checklista som bör åtgärdas för [Skydda DNS-servrar från både interna och externa attacker](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognosering med SMB-sessionsuppräkning


**Beskrivning**

Uppräkning av Server Message Block (SMB) gör det möjligt för angripare att få information om där användare nyligen har loggat in. När angripare har den här informationen kan kan de flytta sidled i nätverket till en specifik känsligt konto.

I denna identifiering utlöses en avisering när en SMB-sessionsuppräkningen utförs mot en domänkontrollant, eftersom det inte borde ske.

**Undersökning**

1. Klicka på aviseringen för att komma åt dess informationssidan. Kontrollera vilket konto/s utförs igen och vilka konton som exponerats eventuella.

 - Finns det någon typ av säkerhetsskannern som körs på källdatorn? Om Ja, **Stäng och utelämna** misstänkt aktivitet.

2. Kontrollera vilka berörda användare/s utföra åtgärden. Gör de normalt logga in på källdatorn, eller kan de administratörer som ska utföra dessa åtgärder?  

3. Om Ja och aviseringen uppdateras **utelämna** misstänkt aktivitet.  

4. Om Ja och den bör inte detta längre **Stäng** misstänkt aktivitet.

5. Om svaret på alla ovanstående är förutsätter Nej, detta är skadliga.

**Reparation**

Använd den [Net upphöra verktyget](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) att skydda din miljö mot angrepp.

## <a name="remote-execution-attempt"></a>Fjärrkörning försök

**Beskrivning**

Angripare som angripa administratörsbehörighet eller använder ett noll-dagars utnyttja kan köra fjärrkommandon på domänkontrollanten. Detta kan användas för att tillskansa sig beständighet, samla in information, DOS-attacker (Denial Of Service) eller i annat syfte. Azure ATP identifierar PSexec och fjärr-WMI-anslutningar.

**Undersökning**

1. Detta är vanligt för administrativa arbetsstationer och IT-gruppmedlemmar och tjänstkonton som kan utför administrativa uppgifter mot domänkontrollanter. Om detta är det här fallet och aviseringen uppdateras eftersom samma administratören och/eller datorn utför sedan aktiviteten, **utelämna** aviseringen.

2. Är den **datorn** i fråga tillåtelse för att utföra den här fjärrkörning mot domänkontrollanten?

 - Är den **konto** i fråga tillåtelse för att utföra den här fjärrkörning mot domänkontrollanten?

 - Om svaret på båda frågor är *Ja*, sedan **Stäng** aviseringen.

3. Om svaret på antingen frågor är Nej, sedan detta ska betraktas som ett true positivt. Försök att hitta källan till försöket genom att kontrollera att datorn och kontoinformation profiler. Klicka på källdatorn igen eller konto för att gå till sidan sin profil. Kontrollera vad hände vid ungefär samma tidpunkt dessa försök söka efter ovanliga aktiviteter, t.ex: som loggades i vilka resurser där nås. Om du har aktiverat Windows Defender ATPintegration klickar du på Windows Defender ATP-skylt ![Windows Defender ATP-skylt](./media/wd-badge.png) ytterligare undersöka datorn. I Windows Defender ATPyou kan se vilka processer och -varningar uppstod vid ungefär samma tidpunkt för aviseringen. 

**Reparation**

1. Begränsa fjärråtkomst till domänkontrollanter från datorer som inte är Nivå 0-datorer.

2. Implementera [privilegierad åtkomst](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) så att endast förstärkt datorer att ansluta till domänkontrollanterna för administratörer.

## <a name="suspicious-authentication-failures"></a>Misstänkt autentiseringsfel

**Beskrivning**

En angripare försöker autentisera med många olika lösenord för olika konton förrän rätt lösenord hittades för minst ett konto i en brute force-attacker. En gång hittades kan en angripare logga in med det kontot.

En avisering utlöses när många autentiseringsfel med Kerberos eller NTLM uppstod i denna identifiering, detta kan antingen vara vågrätt med en liten uppsättning lösenord för många användare. eller lodrätt med en stor uppsättning lösenord på bara några användare. eller en kombination av de här två alternativen. Minsta tid innan en avisering kan utlösas är en vecka.

**Undersökning**

1.  Klicka på **hämta information** Visa fullständig information i ett Excel-kalkylblad. Du kan få följande information: 
   -    Lista över angripna konton
   -    Lista över att gissa konton i vilken inloggningsförsök avslutades med lyckad autentisering
   -    Om autentiseringsförsök utfördes med hjälp av NTLM, ser du relevanta händelseaktiviteter 
   -    Om autentiseringsförsök utfördes med Kerberos, ser du relevanta Nätverksaktiviteter

2.  Klicka på källdatorn för att gå till sidan sin profil. Kontrollera vad hände vid ungefär samma tidpunkt dessa försök söka efter ovanliga aktiviteter, t.ex: som loggades i vilka resurser där nås. Om du har aktiverat Windows Defender ATP-integration klickar du på Windows Defender ATP-skylt ![Windows Defender ATP-skylt](./media/wd-badge.png) ytterligare undersöka datorn. I Windows Defender ATP ser du vilka processer och -varningar uppstod vid ungefär samma tidpunkt för aviseringen. 

3.  Om autentiseringen har utförts med hjälp av NTLM och du ser att aviseringen uppstår flera gånger, och det finns inte tillräckligt med information om den server som källdatorn försökte få åtkomst till, bör du aktivera **NTLM granskning** på ingår domänkontrollanter. Gör detta genom att aktivera händelsen 8004. Detta är händelsen NTLM-autentisering som innehåller information om källdatorn användarkonto och **server** som källdatorn försökte få åtkomst till. När du vet vilken server skickas valideringen av autentisering, bör du undersöka servern genom att markera en händelse som 4624 att bättre förstå autentiseringsprocessen. 

**Reparation**

[Komplexa och lång lösenord](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) ger den nödvändiga första säkerhetsnivån mot brute force-attacker.

## <a name="suspicious-service-creation"></a>Skapa en misstänkt tjänst

**Beskrivning**

En misstänkt tjänst har skapats på en domänkontrollant i din organisation. Den här aviseringen förlitar sig på händelsen 7045 för att identifiera den här misstänkt aktivitet på dina slutpunkter. 

**Undersökning**

1. Om datorn i fråga är en administrativ dator eller en dator på vilken IT gruppmedlemmar och tjänsten konton för att utföra administrativa uppgifter, det kan bero på ett falsklarm och du kan behöva **utelämna** aviseringen och lägger till den i den Undantagslistan om det behövs.

2. Är tjänsten något du känner igen på den här datorn?

 - Är den **konto** i fråga tillåts för att installera den här tjänsten?

 - Om svaret på båda frågor är *Ja*, sedan **Stäng** aviseringen eller lägga till den i undantagslistan.

3. Om svaret på antingen frågor är *inga*, och sedan detta ska betraktas som ett true positivt.

**Reparation**

- Implementera mindre privilegierad åtkomst på datorer i domänen så att bara vissa användare behörighet att skapa nya tjänster.

## <a name="unusual-protocol-implementation"></a>Onormal protokollimplementering


**Beskrivning**

Angripare använda verktyg som implementerar olika protokoll (SMB, Kerberos, NTLM) på sätt som inte är standard. När den här typen av nätverkstrafik godkänns av Windows utan varningar, kan Azure ATP identifiera potentiella skadliga åtgärder. Beteendet är jämförbar olika tekniker, till exempel Over-Pass-the-Hash och brute force och som används av avancerade är en utpressningstrojan som, till exempel WannaCry kryphål.

**Undersökning**

Identifiera det protokoll som är ovanligt – från i tidslinjen för misstänkt aktivitet, klickar du på den misstänkta aktiviteten till dess informationssidan; protokollet visas ovanför på pilen: Kerberos eller NTLM.

- **Kerberos**: detta ofta utlöses om en hackningsförsök verktyget som Mimikatz har använts potentiellt utför en Overpass-the-Hash-attack. Kontrollera om ett program som implementerar sin egen Kerberos-stacken inte överensstämmer med Kerberos RFC körs på källdatorn. Om så är fallet, är det en ofarlig true positiv och du kan **Stäng** aviseringen. Om varningen fortsätter att utlösas och det fortfarande är fallet, kan du **utelämna** aviseringen.

- **NTLM**: kan vara WannaCry eller verktyg som Metasploit, Medusa och Hydra.  

Utför följande steg för att avgöra om detta är en attack med WannaCry:

1. Kontrollera om en attack verktyg som till exempel Metasploit, Medusa eller Hydra körs på källdatorn.

2. Om inga attack verktyg påträffas, kontrollera källdatorn körs som ett program som implementerar sin egen NTLM eller SMB-stacken.

3. Om det inte kontrollera om det här orsakas av WannaCry genom att köra ett WannaCry skanner skript, till exempel [skannern](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) mot källdatorn ingår i den misstänkta aktiviteten. Om skannern konstaterar att datorn som infekterade eller sårbara, arbete på korrigeringar på datorn och ta bort den skadliga koden och blockerar den från nätverket.

4. Om skriptet inte kan hitta att datorn är infekterade eller sårbara, sedan den fortfarande vara angripna men SMBv1 kan ha inaktiverats eller har konfigurerats för datorn, vilket påverkar genomsökningsverktyget.

**Reparation**

Korrigera alla datorer, särskilt användning av säkerhetsuppdateringar.

1. [Inaktivera SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Ta bort WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi kan dekryptera data i händerna på vissa ransom program, men endast om användaren inte har startats om eller stängas av datorn. Mer information finns i [vill Cry är en utpressningstrojan som](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


> [!NOTE]
> Kontakta supporten om du vill inaktivera en misstänkt aktivitet.


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
