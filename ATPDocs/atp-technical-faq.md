---
title: Vanliga frågor och svar om Azure Advanced Threat Protection | Microsoft Docs
description: Innehåller en lista över vanliga frågor och svar om Azure ATP och tillhörande svar
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ce3c41f1cca7e3f621ea2afbf89565e7d6009f28
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166824"
---
*Gäller för: Azure Avancerat skydd*

# <a name="azure-atp-frequently-asked-questions"></a>Vanliga och frågor svar om Azure ATP
Den här artikeln innehåller en lista över vanliga frågor och svar om Azure ATP och ger insikt och svar.


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Var hittar jag en licens för Azure Advanced Threat Protection (ATP)?

Du kan skaffa en licens för Enterprise Mobility + Security 5 (EMS E5) direkt via den [Office 365-portalen](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) eller via licensieringsmodellen för Cloud Solution Partner (CSP).                  

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Vad gör jag om Azure ATP-sensorn eller fristående sensorn inte startar?
Titta på det senaste felet i det aktuella felet [log](troubleshooting-atp-using-logs.md) (där Azure ATP är installerat under mappen ”loggar”).

## <a name="how-can-i-test-azure-atp"></a>Hur kan jag testa Azure ATP?
Du kan simulera misstänkta aktiviteter som ett test för slutpunkt till slutpunkt. DNS-rekognosering simuleras i följande scenario:

1.  Verifiera Azure ATP sensorer installeras och konfigureras på domänkontrollanter (eller fristående sensorer och relaterade portspegling är installerade och konfigurerade)
2.  Öppna CMD
3.  Kör följande kommando: nslookup -<DC iP address>
    1.  Tryck på RETUR
    2.  Typ: Är -d <FQDN>
    3.  Beroende på hur din miljö varierar svar från ”fråga nekade” till en lista över dina DNS-poster. 
4. Visa aviseringar som rör simulerade DNS-rekognosering i Azure ATP-konsolen. 

## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Fungerar Azure ATP med krypterad trafik?
Azure ATP förlitar sig på analysen av flera nätverksprotokoll och även händelser som samlas in från SIEM eller via vidarebefordran av Windows-händelser.  Nätverksprotokoll med krypterad trafik (till exempel LDAPS och IPSEC) dekryptera inte, men har analyserats.


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Fungerar Azure ATP med Kerberos-skydd?
Aktivering av Kerberos Armoring, även kallat Flexible Authentication Secure Tunneling (FAST), stöds av ATP, med undantag för over-pass hash-identifiering, vilket inte fungerar med Kerberos-skydd.

## <a name="how-many-azure-atp-sensors-do-i-need"></a>Hur många Azure ATP-sensorer behöver jag?

Alla domänkontrollanter i miljön bör omfattas av en ATP-sensorn eller fristående sensorn. Mer information finns i [Azure ATP-sensorn ändrar storlek på](atp-capacity-planning.md#sizing). 


## <a name="why-are-certain-accounts-considered-sensitive"></a>Varför anses vissa konton känsliga?
Det här inträffar när ett konto är medlem i grupper som är tilldelade som känsliga (till exempel: ”Domänadministratörer”).

Om du vill förstå varför ett konto är känsligt kan du granska dess gruppmedlemskap för att förstå vilka känsliga grupper det tillhör (den grupp det tillhör kan också vara känslig till följd av en annan grupp, så samma process bör utföras tills du hittar den känsliga grupp som har högst nivå). Du kan också [tagg som känsliga konton manuellt](sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Hur övervakar jag en virtuell domänkontrollant med hjälp av Azure ATP?
De flesta virtuella domänkontrollanter kan omfattas av Azure ATP-sensorn att avgöra om Azure ATP sensorn är lämplig för din miljö, se [kapacitetsplanering för Azure ATP](atp-capacity-planning.md).

Om en virtuell domänkontrollant inte kan omfattas av Azure ATP-sensorn, kan du använda antingen en virtuell eller fysisk Azure ATP fristående sensor enligt beskrivningen i [konfigurera portspegling](configure-port-mirroring.md).  <br />Det enklaste sättet är att ha en virtuell Azure ATP fristående sensor på varje värd där det finns en virtuell domänkontrollant.<br />Om de virtuella domänkontrollanterna flyttas mellan olika värdar, måste du göra något av följande steg:

-   När den virtuella domänkontrollanten flyttar till en annan värd, kan du förkonfigurera Azure ATP-sensorn för fristående på den värden att ta emot trafiken från den virtuella domänkontrollanten som har flyttats.
-   Se till att du kopplar följer den virtuella Azure ATP fristående sensorn med den virtuella domänkontrollanten, så att om den flyttas fristående Azure ATP-sensorn med den.
-   Det finns några virtuella växlar som kan skicka trafik mellan värdar.


## <a name="what-can-azure-atp-detect"></a>Vad kan Azure ATP identifiera?

Azure ATP identifierar kända skadliga attacker och tekniker, säkerhetsproblem och risker.
En fullständig lista över Azure ATP-identifieringar finns [vilka identifieringar Azure ATP utför?](suspicious-activity-guide.md).

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Hur många nätverkskort kräver fristående Azure ATP-sensorn?
Fristående Azure ATP-sensorn måste ha minst två nätverkskort:<br>1. Ett nätverkskort för att ansluta till det interna nätverket och Azure ATP-Molntjänsten<br>2. Ett nätverkskort som används för att avbilda domänkontrollantens nätverkstrafik via portspegling.<br>* Detta gäller inte för Azure ATP-sensorn som internt använder alla nätverkskort som domänkontrollanten använder.

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Vilken typ av integrering har Azure ATP med Siem?
Azure ATP har en dubbelriktad integrering med Siem enligt följande:

1. Azure ATP kan konfigureras för att skicka en Syslog-avisering till valfri SIEM-server som använder CEF-formatet för hälsovarningar och när en misstänkt aktivitet har identifierats.
2. Azure ATP kan konfigureras för att ta emot Syslog-meddelanden för Windows-händelser från [dessa siem-servrar](configure-event-collection.md).

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Hur konfigurerar jag Azure ATP-sensorer för att kommunicera med Azure ATP-Molntjänsten när jag har en proxy?

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna: *. atp.azure.com port 443 i din brandväggsproxy. Anvisningar för hur du gör detta finns i [konfigurera proxyservern eller brandväggen för att aktivera kommunikation med Azure ATP-sensorer](configure-proxy.md).
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Azure ATP kan övervaka domänkontrollanter som är visualiserade på IaaS-lösningen?
Ja, du kan använda Azure ATP-sensorn för att övervaka domänkontrollanter som finns i valfri IaaS-lösning.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Kommer det här att vara en del av Azure Active Directory eller lokal Active Directory?
Den här lösningen är för närvarande ett fristående erbjudande. Det är inte en del av Azure Active Directory eller lokal Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Måste man skriva sina egna regler och skapa en tröskel/baslinje?
Med Azure Advanced Threat Protection finns kan du skapa regler, trösklar eller baslinjer och sedan finjustera. Azure ATP analyserar beteende hos användare, enheter och resurser, samt deras relation till varandra, och kan identifiera misstänkt beteende och kända attacker snabbt. Tre veckor efter distributionen startar Azure ATP att identifiera beteendeanalys misstänkta aktiviteter. Å andra sidan startar Azure ATP Identifiera kända skadliga attacker och säkerhetsproblem direkt efter distributionen.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Använder detta endast trafik från Active Directory?
Förutom att analysera Active Directory-trafik med teknik för djup paketinspektion Azure ATP också samlar in relevanta händelser från din säkerhetsinformation och händelsehantering (SIEM) och skapar entitetsprofiler baserat på information från Active Directory Domain Services. Om du använder Azure ATP-sensorn extraherar händelserna automatiskt. Du kan använda vidarebefordran av Windows-händelser för att skicka dessa händelser till fristående Azure ATP-sensorn. Azure ATP stöder också mottagande RADIUS-redovisning för VPN-loggar från olika leverantörer (Microsoft, Cisco, F5 och kontrollpunkt).

## <a name="what-is-port-mirroring"></a>Vad är portspegling?
Portspegling kallas även SPAN (Switched Port Analyzer) och är en metod för att övervaka nätverkstrafik. När portspegling är aktiverat skickar växeln en kopia av alla nätverkspaket som syns på en port (eller ett helt VLAN) till en annan port där paketet kan analyseras.

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Övervakar Azure ATP-domänanslutna enheter?
Nej. Azure ATP övervakar alla enheter i nätverket som utför autentisering och auktorisering förfrågningar mot Active Directory, inklusive icke-Windows och mobila enheter.

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Övervakar Azure ATP-datorkonton, samt användarkonton?
Ja. Eftersom datorn konton (samt eventuella andra entiteter) kan användas för att utföra skadliga aktiviteter, övervakar Azure ATP allationsbeteende för dator-konton och alla andra entiteter i miljön.

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP kan stödja flera domäner och flera skogar?
Azure Advanced Threat Protection har stöd för miljöer med flera domäner och skogar. Den här funktionen är för närvarande i offentlig förhandsversion. Mer information och kända begränsningar finns i [stöd för flera skogar](atp-multi-forest.md).

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Går det att se den övergripande hälsan för distributionen?
Ja, du kan visa den övergripande hälsan för den distribution och specifika problem som rör konfiguration, anslutning osv. du informeras när de inträffar.

## <a name="what-data-does-azure-atp-collect"></a>Vilka data samlar Azure ATP? 
Azure ATP samlar in och lagrar information från dina konfigurerade servrar (domänkontrollanter, medlemsservrar osv.) i en databas som är specifika för tjänsten för administration, spårning och rapportering. Information som samlas in omfattar nätverkstrafik till och från domänkontrollanterna (till exempel Kerberos-autentisering, NTLM-autentisering, DNS-frågor), säkerhetsloggar (till exempel Windows säkerhetshändelser), Active Directory-information (struktur, undernät, platser) och entitetsinformation (till exempel namn, e-postadresser och telefonnummer). 

Microsoft använder dessa data till: 

-   Proaktivt identifiera indikatorer för attack (IOAs) i din organisation 
-   Generera aviseringar om en möjlig attack upptäcktes 
-   Ange dina säkerhetsåtgärder med en översikt över enheter som hör till threat signaler från ditt nätverk, så att du kan undersöka och utforska förekomsten av säkerhetshot på nätverket. 

Microsoft inte min dina data i reklamsyfte eller för något annat syfte än att ge dig till tjänsten. 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Måste jag flexibiliteten att välja var du vill lagra Mina data? 

När du skapar Azure ATP-arbetsytan som du kan välja att lagra dina data, kan du lagra data i Microsoft Azure-datacenter i USA eller Europa. När du konfigurerat, kan du inte ändra den plats där dina data lagras. Microsoft kommer inte att överföra data från den angivna platsen. 

## <a name="is-my-data-isolated-from-other-customer-data"></a>Är Mina data isolerade från andra kunddata? 

Ja, dina data är isolerade genom autentisering och logisk uppdelning baserat på kundernas identifierare. Varje kund kan endast komma åt data som samlas in från sin egen organisation och allmänna data som Microsoft tillhandahåller. 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Hur Microsoft förhindra skadliga insiderattacker aktiviteter och missbruk av Privilegierade roller? 

Microsoft-utvecklare och administratörer har, avsiktligt fått behörighet att utföra sina uppgifter att driva och utvecklas tjänsten. Microsoft distribuerar kombinationer av förebyggande Detektiv och reaktiv kontroller, inklusive följande metoder för att skydda mot obehörig utvecklare och/eller den administrativa aktiviteten: 

-   Nära åtkomstkontroll till känsliga data 
-   Kombinationer av kontroller som avsevärt förbättrar oberoende upptäcka skadlig programvara 
-   Flera nivåer av övervakning, loggning och rapportering 

Dessutom Microsoft utför bakgrundsundersökningar verifiering på vissa anställda och begränsar åtkomsten till program, system och nätverksinfrastruktur i förhållande till nivån för verifiering i bakgrunden. Anställda följer en formell process när de krävs för åtkomst till en kunds konto eller relaterad information i prestandan för sina uppgifter. 

## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
