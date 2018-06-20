---
title: Vanliga frågor och svar om Azure Advanced Threat Protection | Microsoft Docs
description: Visar en lista med vanliga frågor och svar om Azure ATP och tillhörande svar
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/13/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7f7f4841c40fb78dc06bae1c06e3c57d2e7f7ee
ms.sourcegitcommit: c77e378d18e654bea4b4af4f24cc941a6659ce99
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/15/2018
ms.locfileid: "29883958"
---
*Gäller för: Azure Advanced Threat Protection*

# <a name="azure-atp-frequently-asked-questions"></a>Vanliga och frågor svar om Azure ATP
Den här artikeln innehåller en lista med vanliga frågor och svar om Azure ATP och ger insikt och svar.


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Var hittar jag en licens för Azure Advanced Threat Protection (ATP)?

Du kan skaffa en licens för Enterprise Mobility + Security 5 (EMS E5) direkt via den [Office 365-portalen](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) eller via molnet lösning Partner (CSP) licensieringsmodell.                  

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Vad gör jag om Azure ATP-sensor eller fristående sensor inte startar?
Titta på det senaste fel i den aktuella felloggen (där Azure ATP är installerat under mappen ”loggar”).

## <a name="how-can-i-test-azure-atp"></a>Hur kan jag testa Azure ATP?
Du kan simulera misstänkta aktiviteter som ett test slutpunkt till slutpunkt, genom att köra följande kommando:

-  DNS-rekognosering med hjälp av Nslookup.exe


Detta måste fjärrköras mot domänkontrollanten som övervakas och inte från Azure ATP fristående sensorn.


## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Fungerar Azure ATP med krypterad trafik?
Azure ATP beroende analysera flera nätverksprotokoll, samt händelser som samlas in från SIEM eller via vidarebefordran av Windows-händelser. Identifieringar baserat på nätverksprotokoll med krypterad trafik (till exempel LDAPS och IPSEC) har inte analyserats.


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Fungerar Azure ATP med Kerberos-skydd?
Aktivera Kerberos-skydd, kallas även Flexible Authentication Secure Tunneling (FAST), stöds av ATP, med undantag för over-pass hash-identifiering fungerar inte med Kerberos-skydd.

## <a name="how-many-azure-atp-sensors-do-i-need"></a>Hur många Azure ATP sensorer behöver jag?

Alla domänkontrollanter i miljön bör omfattas av en ATP-sensor eller fristående sensor. Mer information finns i [Azure ATP sensor storleksanpassa](atp-capacity-planning.md#sizing). 


## <a name="why-are-certain-accounts-considered-sensitive"></a>Varför anses vissa konton känsliga?
Detta inträffar när ett konto är medlem i grupper som är avsedda som känslig (till exempel: ”Domänadministratörer”).

Om du vill förstå varför ett konto är känsligt kan du granska dess gruppmedlemskap för att förstå vilka känsliga grupper det tillhör (den grupp det tillhör kan också vara känslig till följd av en annan grupp, så samma process bör utföras tills du hittar den känsliga grupp som har högst nivå). Du kan också [taggen konton som känsliga manuellt](sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Hur övervakar jag en virtuell domänkontrollant med hjälp av Azure ATP?
De flesta virtuella domänkontrollanter kan omfattas av Azure ATP sensor, att fastställa om Azure ATP sensor är lämplig för din miljö finns [Azure ATP kapacitetsplanering](atp-capacity-planning.md).

Om en virtuell domänkontrollant inte kan omfattas av Azure ATP sensorn, du kan ha antingen en virtuell eller fysisk Azure ATP fristående sensor enligt beskrivningen i [konfigurera portspegling](configure-port-mirroring.md).  <br />Det enklaste sättet är att ha en virtuell Azure-ATP fristående sensor på varje värd där det finns en virtuell domänkontrollant.<br />Om de virtuella domänkontrollanterna flyttas mellan olika värdar, måste du göra något av följande steg:

-   När den virtuella domänkontrollanten flyttar till en annan värd förkonfigurera Azure ATP fristående sensor i som är värdar för att ta emot trafik från den virtuella domänkontrollanten som precis har flyttats.
-   Kontrollera att du kopplar den virtuella Azure-ATP fristående sensorn med den virtuella domänkontrollanten, så att om den flyttas Azure ATP fristående sensor med.
-   Det finns några virtuella växlar som kan skicka trafik mellan värdar.


## <a name="what-can-azure-atp-detect"></a>Vad kan Azure ATP identifiera?

Azure ATP identifierar kända skadliga attacker och tekniker, säkerhetsproblem och risker.
En fullständig lista över Azure ATP-identifieringar finns [vilka identifieringar Azure ATP utför?](suspicious-activity-guide.md).

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Hur många nätverkskort kräver Azure ATP fristående sensor?
Azure ATP fristående sensor måste ha minst två nätverkskort:<br>1. Ett nätverkskort för att ansluta till det interna nätverket och tjänsten Azure ATP moln<br>2. Ett nätverkskort som används för att avbilda domänkontrollantens nätverkstrafik via portspegling.<br>* Det här gäller inte för Azure ATP sensor, som internt använder alla nätverkskort som domänkontrollanten använder.

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Vilken typ av integrering har Azure ATP med Siem?
Azure ATP har en dubbelriktad integrering med Siem enligt följande:

1. Azure ATP kan konfigureras för att skicka en Syslog-avisering till valfri SIEM-server som använder CEF-formatet för health-aviseringar och när en misstänkt aktivitet har identifierats.
2. Azure ATP kan konfigureras för att ta emot Syslog-meddelanden för Windows-händelser från [dessa siem-servrar](configure-event-collection.md).

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Hur konfigurerar Azure ATP sensorer att kommunicera med Azure ATP molntjänst när jag har en proxy?

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna: *. atp.azure.com port 443 i din brandvägg/proxyserver. Instruktioner om hur du gör detta finns [konfigurera proxyservern eller brandväggen för att aktivera kommunikation med Azure ATP sensorer](configure-proxy.md).
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Övervakar Azure ATP domänkontrollanter virtualiserade på IaaS-lösningen?
Ja, du kan använda Azure ATP-sensor övervakar domänkontrollanter som finns i valfri IaaS-lösning.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Kommer det här att vara en del av Azure Active Directory eller lokal Active Directory?
Den här lösningen är för närvarande ett fristående erbjudande. Det är inte en del av Azure Active Directory eller lokal Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Måste man skriva sina egna regler och skapa en tröskel/baslinje?
Det finns inget behov av att skapa regler, trösklar eller baslinjer och sedan finjustera med Azure Advanced Threat Protection. Azure ATP analyserar beteende hos användare, enheter och resurser, samt deras relation till varandra, och kan identifiera misstänkt beteende och kända attacker snabbt. Tre veckor efter distributionen börjar Azure ATP identifiera beteendebaserade misstänkta aktiviteter. Å andra sidan startar Azure ATP Identifiera kända skadliga attacker och säkerhetsproblem direkt efter distributionen.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Använder detta endast trafik från Active Directory?
Förutom att analysera Active Directory-trafik med teknik för djup paketinspektion Azure ATP också samlar in relevanta händelser från Security Information and Event Management (SIEM) och skapar entitetsprofiler baserat på information från Active Directory Domain Services. Om du använder Azure ATP-sensor extraherar händelserna automatiskt. Du kan använda vidarebefordran av Windows-händelser för att skicka dessa händelser till Azure ATP fristående sensorn. Azure ATP stöder även ta emot RADIUS-redovisning VPN-loggar från olika leverantörer (Microsoft, Cisco, F5 eller kontrollpunkt).

## <a name="what-is-port-mirroring"></a>Vad är portspegling?
Portspegling kallas även SPAN (Switched Port Analyzer) och är en metod för att övervaka nätverkstrafik. När portspegling är aktiverat skickar växeln en kopia av alla nätverkspaket som syns på en port (eller ett helt VLAN) till en annan port där paketet kan analyseras.

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Övervakar Azure ATP domänanslutna enheter?
Nej. Azure ATP övervakar alla enheter i nätverket som utför autentisering och auktorisering förfrågningar mot Active Directory, inklusive icke-Windows och mobila enheter.

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Övervakar Azure ATP datorkonton samt användarkonton?
Ja. Eftersom datorn konton (samt eventuella andra entiteter) kan användas för att utföra skadliga aktiviteter, övervakar Azure ATP alla datorn konton beteende och alla andra entiteter i miljön.

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP kan stödja flera domäner och flera skogar?
Azure Advanced Threat Protection har stöd för miljöer med flera domäner inom samma skogsgräns. Flera skogar kräver en arbetsyta för Azure ATP för varje skog.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Går det att se den övergripande hälsan för distributionen?
Ja, du kan visa den övergripande hälsan för distributionen samt specifika problem relaterade till konfiguration, anslutning osv., och du meddelas när de inträffar.

## <a name="what-data-does-azure-atp-collect"></a>Vilka data samlar Azure ATP? 
Azure ATP samlar in och lagrar information från din konfigurerade servrar (domänkontrollanter, medlemsservrar osv.) i en databas som är specifika för tjänsten för administration, spårning och rapportering. Den insamlade informationen omfattar nätverkstrafik till och från domänkontrollanterna (till exempel Kerberos-autentisering, NTLM-autentisering, DNS-frågor), säkerhetsloggar (till exempel Windows säkerhetshändelser), Active Directory-information (struktur, undernät, platser) entitetsinformation om och (till exempel namn, e-postadresser och telefonnummer). 

Microsoft använder dessa data till: 

-   Proaktivt identifiera indikatorer för attack (IOAs) i din organisation 
-   Generera aviseringar om möjligt attack upptäcktes 
-   Ange din säkerhetsåtgärder med en överblick över enheter som är relaterade till hot signaler från nätverket, så att du kan undersöka och utforska förekomst av hot mot säkerheten i nätverket. 

Microsoft inte min data för reklam eller för andra syften än tillhandahåller tjänsten. 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Måste jag möjlighet att välja var du vill lagra Mina data? 

När du skapar Azure ATP arbetsytan kan du lagra data, kan du lagra data i Microsoft Azure-datacenter i USA och Europa. När du konfigurerat, kan du inte ändra den plats där dina data lagras. Microsoft kommer inte att överföra data från den angivna platsen. 

## <a name="is-my-data-isolated-from-other-customer-data"></a>Är Mina data som de isoleras från andra kundinformation? 

Ja, dina data är isolerade via autentisering och logiska särskiljning utifrån kundens identifierare. Varje kund kan endast komma åt data som samlas in från sin egen organisation och allmänna data som Microsoft tillhandahåller. 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Hur Microsoft att intern aktiviteter och missbruk av Privilegierade roller? 

Microsoft-utvecklare och administratörer, avsiktligt får behörighet att utföra sina uppgifter att driva och utvecklas tjänsten. Microsoft distribuerar kombinationer av förebyggande Detektiv och reaktiv kontroller till exempel följande metoder för att skydda mot obehörig utvecklare och/eller administrativ aktivitet: 

-   Nära åtkomstkontroll till känsliga data 
-   Kombinationer av kontroller som används för att avsevärt förbättrar oberoende upptäcka skadlig programvara 
-   Flera nivåer av övervakning, loggning och rapportering 

Dessutom Microsoft utför verifieringen bakgrundskontroller på vissa åtgärder personal och begränsar åtkomst till program, system och nätverksinfrastruktur i förhållande till nivån för verifiering i bakgrunden. Operations personal följa en formell process när de krävs för att en kunds konto eller relaterad information i sina uppgifter. 

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
