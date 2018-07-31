---
title: Vad är nytt i Azure ATP | Microsoft Docs
description: Beskriver de senaste versionerna av Azure ATP och innehåller information om nyheter i varje version.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ebdae7617dd550631186ab87cba922758649fd45
ms.sourcegitcommit: 759e99f670c42c2dd60d07b2200d3de01ddf6055
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/30/2018
ms.locfileid: "39335987"
---
*Gäller för: Azure Avancerat skydd*


# <a name="whats-new-in-azure-atp"></a>Vad är nytt i Azure ATP 

## <a name="azure-atp-release-242"></a>Azure ATP-versionen 2.42

Gavs ut den 29 juli 2018

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 


## <a name="azure-atp-release-241"></a>Azure ATP-versionen 2.41

Publicerad 22 juli 2018

- **Support för Azure ATP-flera skogar distribueras gradvis (förhandsversion)** <br> Azure ATP har nu stöd för organisationer med flera skogar där du kan övervakaraktivitet och profilanvändare i skogar. Den här nya funktionen kan du:

  - Visa och undersöka aktiviteter som utförs av användare i flera skogar från en enda glasruta.
  - Förbättrar identifiering och minskar antalet falska positiva identifieringar genom att tillhandahålla avancerade Active Directory-integrering och konto-lösning.
  - Få bättre övervakning av aviseringar och rapportering för cross-org täckning.


-   **Nya identifieringar: DCShadow**<br>Två nya identifieringar har lagts till för att skydda mot attacker för domain controller shadow (DCShadow):

    -   Misstänkt befordran av domänkontrollant (möjlig DCShadow-attack) – den här identifieringen hjälper dig att identifiera attacker där en dator för att personifiera en domänkontrollant och sedan försöker använda replikering för att sprida ändringarna till andra domänkontrollanter i domänen.

    -   Misstänkt-replikeringsbegäran (möjlig DCShadow-attack) – den här identifieringen som hjälper dig att skydda mot attacker som försöker utföra befordran av domänkontrollanter för datorer som inte är domänkontrollanter för att kunna ändra katalogobjekt.

-   **Förbättrad information för nedgradering av kryptering**<br>Kryptering nedgradering identifiering nu ger mer information om vilken typ av attack upptäcktes: overpass-the-hash och gyllene biljett dyrken. Dessutom kan har de här aviseringarna aggregerats om du vill aktivera enklare undersökning.
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 



## <a name="azure-atp-release-240"></a>Azure ATP-versionen 2,40

Gavs ut den 15 juli 2018

- Pass-the-ticket-identifiering nu innehåller ett bevis avsnitt på sidan aviseringsinformation. Detta ger ytterligare information för att undersöka aviseringen.

- Användaren åtkomstkontroll flaggor som finns i en användares profil under katalogdata, innehåller nu en förklaring så att du bättre kan förstå vilka attribut som är på och som är inaktiverade.  

## <a name="azure-atp-release-239"></a>Azure ATP-versionen 2,39

Publicerad den 5 juli 2018
-   **Ny identifiering har lagts till: Kerberos golden ticket - icke-befintligt konto** (förhandsversion)<br>Den här nya identifieringen kan du skydda din organisation från attacker som en gyllene biljett har skapats för ett konto som inte finns i din domän. Mer information finns i den [Azure Advanced Threat Protection guide för misstänkt aktivitet](suspicious-activity-guide.md#golden-ticket)

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 


## <a name="azure-atp-release-238"></a>Azure ATP-versionen 2.38

Gavs ut den 1 juli 2018

- Den här versionen innehåller korrigeringar och förbättringar för flera problem samt förbättringar i Azure ATP-portalen.

## <a name="azure-atp-release-237"></a>Azure ATP-versionen 2.37

Publicerad 24 juni 2018

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 

## <a name="azure-atp-release-236"></a>Azure ATP-versionen 2,36

Gavs ut den 17 juni 2018

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 


## <a name="azure-atp-release-235"></a>Azure ATP-versionen 2,35

Gavs ut den 10 juni 2018
 
- **Den nya förhandsversionen identifieringar**<br></br>Nu kan Azure ATP kan dra nytta av det faktum att det är en tjänst i molnet, där nya funktioner kan tillhandahållas i snabb cykler – och ge dig nya identifieringar så snabbt som möjligt från. Dessa nya identifieringar taggas när ”förhandsversion” när de är första tillgängliga. Vanligtvis flyttas en ny identifiering från förhandsversion till allmänt tillgängliga inom ett par veckor. Som standard visas förhandsversion identifieringar. Läs om hur avanmäla [Förhandsgranska identifieringar](working-with-suspicious-activities.md#preview-detections).
 
- **Identifiering av misstänkt VPN**<br></br>Den här versionen innehåller en förhandsversion av misstänkt VPN-identifiering. Azure ATP lär sig användarbeteende för VPN, inklusive datorerna som de användare som loggat in på och de platser som användarna att ansluta från och varnar dig när det finns en avvikelse från förväntat beteende. Mer information finns i [identifiering av misstänkt VPN](suspicious-activity-guide.md#suspicious-vpn-detection).

- **Försenade update**<br></br>Nu har du möjlighet att ange Azure ATP-sensorer att uppdatera vid ett senare tillfälle, varje gång Azure ATP-uppdateringar. Du kan nu konfigurera varje Azure ATP-sensorn med **fördröjd update** så att den kommer att uppdatera 24 timmar efter tjänstuppdateringar för Azure ATP-molnet. Den här funktionen kan du testa uppdateringen på specifikt test sensorer och endast uppdatera din produktion sensorer vid ett senare tillfälle. Öppna ett supportärende om du upptäcker ett problem vid första uppdateringscykeln. Mer information finns i [uppdatering Azure ATP-sensorer](sensor-update.md).

- **Uppdaterade ovanligt protokoll implementering identifiering**<br></br>Ovanlig implementering identifieringen nu innehåller mer information. Du kan se vilka potentiella angrepp verktyget Azure ATP misstänker är på arbetet i nätverket. Mer information finns i den [guide för misstänkt aktivitet](suspicious-activity-guide.md).
 
- **Inaktuella sensor avisering**<br></br>Azure ATP innehåller en ny övervakningsavisering så att du vet om en sensor är fler än tre versioner är inaktuell. Om du ser den här aviseringen, bör du uppdatera sensorn eller undersöka varför sensorn uppdateras inte automatiskt. Om aviseringen återkommer kan du avinstallera och installera sensorn.

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 

## <a name="azure-atp-release-234"></a>Azure ATP-versionen 2.34

Gavs ut den 3 juni 2018
 
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 

 
## <a name="azure-atp-release-233"></a>Azure ATP-versionen 2,33

Utgiven: 27 maj 2018

- Förhandsversion av funktionen: Azure ATP stöder nu nya språk och 13 nya språken:
    - Tjeckiska
    - Ungerska
    - Italienska
    - Koreanska
    - Nederländska
    - Polska
    - Portugisiska (Brasilien)
    - portugisiska (Portugal)
    - Ryssland
    - Svenska
    - Turkiska
    - Kinesiska (Kina)
    - Kinesiska (Taiwan)



## <a name="azure-atp-release-232"></a>Azure ATP-versionen 2.32

Utgiven: 13 maj 2018
 
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 

## <a name="azure-atp-release-231"></a>Azure ATP-versionen 2.31

Gavs ut den 6 maj 2018
 
- Förbättringar har gjorts för namnmatchning. Som en del av det, förutom active upplösning RPC- och NetBIOS-sensorn kan utfärda ett TLS klientens Hello-paket till RDP-slutpunkten porten (port 3389). 
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 

## <a name="azure-atp-release-230"></a>Azure ATP-versionen 2.30

Gavs ut den 29 April 2018
 
- Kryptering nedgradering av misstänkta aktiviteter innehåller nu ett bevis avsnitt som beskriver de problem som identifieras av Azure ATP som orsakar den att tro att en aktivitet för nedgradering av kryptering har förflutit. 
-   Azure ATP använder nu Azure e-Orchestrator för alla e-postmeddelanden som skickas från Azure ATP, inklusive misstänkta aktiviteter, övervakning, aviseringar och rapporter. Du ser att dessa e-postmeddelanden enligt ett konsekvent format för enkel användning och Excel-filer som kommer att länkas till från e-post som ska hämtas från konsolen.
 
 

## <a name="azure-atp-release-229"></a>Azure ATP-versionen 2.29

Gavs ut den 22 April 2018
 
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP-versionen 2.28

Gavs ut den 15 April 2018
 
-   Användare som är medlemmar i rollgrupperna Azure ATP-användare och Azure ATP-visningsprogram nu har behörighet att se övervakningsaviseringar.
- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 


## <a name="azure-atp-release-227"></a>Azure ATP-versionen 2,27

Gavs ut den 8 April 2018

- Nu har du möjlighet att tillhandahålla feedback från användare från det övre navigeringsfältet. Klicka på smileyn på menyraden kan du skicka ett e-postmeddelande till Azure Advanced Threat Protection-teamet med din feedback.

- Den här versionen innehåller korrigeringar och förbättringar för flera problem. 
 

## <a name="azure-atp-release-226"></a>Azure ATP-versionen 2,26

Publicerad 25 mars 2018

- När Azure ATP varnar dig för en misstänkt aktivitet som du identifierar som en ofarliga positiva (en giltig åtgärd som inte är en misstänkt aktivitet) du möjlighet att undanta datorer och IP-adresser för flera identifieringar, inklusive: nedgradering av kryptering, LDAP Brute force, förfalskat PAC, Brute force och Pass-the-hash.
-   Prestanda för Azure ATP-sensorn har förbättrats.
-   En ny region har lagts till för arbetsyta för distribution, du kan nu distribuera en arbetsyta i Asien. 


## <a name="azure-atp-release-225"></a>Azure ATP-versionen 2,25

Publicerad 18 mars 2018

- Multifaktorautentisering (MFA) stöds nu i Azure ATP. Klienter som använder MFA nu kan du ange Azure ATP-portalen.
- Azure ATP har nu en [ **systemstatus** ](https://health.atp.azure.com/) att förse dig med information om huruvida arbetsytehanteringsportalen är igång och aktiv, om det finns problem med identifieringar och om sensorn kan skicka trafik till molnet. Du kan komma åt den **systemstatus** Azure ATP-menyraden.


## <a name="azure-atp-release-224"></a>Azure ATP-versionen 2.24

Gavs ut den 11 mars 2018

**Nya och uppdaterade identifieringar**
  - Misstänkt skapande av tjänst – angripare försöker köra misstänkta tjänster i nätverket. Azure ATP nu genererar en avisering när den identifierar att någon på en specifik dator körs en ny tjänst som verkar misstänkt. Den här identifieringen baseras på händelser (inte nätverkstrafik) och har upptäckts på alla domänkontrollanter i nätverket som vidarebefordrar händelse 7045 till Azure ATP. Mer information finns i den [guide för misstänkt aktivitet](suspicious-activity-guide.md).

**Förbättrad undersökning**
  - Azure ATP innehåller en avancerad och [entitetsprofilen](entity-profiles.md). Entitetsprofilen ger dig en plattform som är utformad för djupgående undersökning av användaraktiviteter detta inkluderar de resurser de använde, datorer som de har loggat in på och många fler. Entitetsprofilen också ger katalogdata och hjälper dig att identifiera potentiella laterala rörelsebanor till eller från entiteten, vilket gör att du vill veta mer om potentiella överträdelser i din organisation.

  - ATP gör att du kan manuellt taggen entiteter som *känsliga* att förbättra identifieringar och övervakning. Den här taggningen påverkar många Azure ATP-identifieringar, till exempel känsliga grupp ändring av identifiering och [lateral rörelsesökväg](use-case-lateral-movement-path.md), som förlitar sig på entiteter som betraktas som känslig.

**Nya rapporter som hjälper dig att undersöka**
  - Den [lösenord som exponerats i klartext rapporten](reports.md) kan du identifiera när tjänster skickar autentiseringsuppgifter skickas i klartext. På så sätt kan du undersöka tjänster och förbättra din nivå för nätverkssäkerhet. Den här rapporten ersätter aviseringarna som klartext misstänkt aktivitet.
  - Den [laterala rörelsebanor till känsliga konton rapport](reports.md) visar en lista över känsliga konton som exponeras via lateral förflyttning. På så sätt kan du minska dessa sökvägar och förstärka nätverket för att minimera risken attack surface. Detta gör att du kan förhindra lateral förflyttning så att angripare inte kan flytta över nätverket mellan användare och datorer tills de når virtual Secure högsta vinsten: dina känsliga administratörsautentiseringsuppgifter för kontot.

- Du kan nu enkelt ge åtkomst i dokumentationen från en länk i en avisering om misstänkt aktivitet för att kunna visa [undersökningssteg som du kan vidta](suspicious-activity-guide.md). 

**Prestandaförbättringar**
 -  Infrastruktur för Azure ATP-sensorn har fått förbättrad prestanda: aggregerade vyn av trafik möjliggör optimering av pipeline för CPU och paket och återanvänder sockets till domänkontrollanterna för att minimera SSL-sessioner till domänkontrollanten.

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)