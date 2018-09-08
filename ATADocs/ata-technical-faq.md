---
title: Vanliga frågor och svar om Advanced Threat Analytics | Microsoft Docs
description: Visar en lista med vanliga frågor om ATA och tillhörande svar
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c28783170764c117a07fa19946c83638f24dc1a6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166501"
---
*Gäller för: Advanced Threat Analytics version 1.9*

# <a name="ata-frequently-asked-questions"></a>Vanliga frågor och svar om ATA
Den här artikeln innehåller en lista med vanliga frågor om ATA och ger insikt och svar.


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>Var kan jag skaffa en licens för Advanced Threat Analytics (ATA)?

Om du har ett aktivt Enterprise-avtal kan du ladda ned programvaran från Microsoft Volume Licensing Center (VLSC).

Om du har köpt en licens för Enterprise Mobility + Security (EMS) direkt via Office 365-portalen eller via licensieringsmodellen för molnlösningspartner och du inte har åtkomst till ATA via Microsoft Volume Licensing Center (VLSC), kontaktar du Microsoft Support för hjälp med att aktivera Advanced Threat Analytics (ATA).

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Vad gör jag om ATA-gatewayen inte startar?
Titta på det senaste felet i den aktuella felloggen (där ATA är installerat under mappen "Loggar").

## <a name="how-can-i-test-ata"></a>Hur kan jag testa ATA?
Du kan simulera misstänkta aktiviteter som är ett test slutpunkt till slutpunkt på något av följande sätt:

1.  DNS-rekognosering med hjälp av Nslookup.exe
2.  Fjärrkörning med hjälp av psexec.exe


Detta måste fjärrköras mot domänkontrollanten som övervakas och inte från ATA-gatewayen.

## <a name="which-ata-build-corresponds-to-each-version"></a>Vilken build-version av ATA motsvarar varje version?

Version uppgradera information finns i [ATA uppgraderingssökväg](upgrade-path.md).

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>Vilken version ska jag använda för att uppgradera min aktuella ATA-distribution till den senaste versionen?

Uppgradera matrisen ATA version Se [ATA uppgraderingssökväg](upgrade-path.md).


## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>Hur uppdaterar dess senaste signaturerna i ATA Center?

ATA-identifieringen utökas när en ny version är installerad på ATA Center. Du kan uppgradera till Center genom att använda Microsoft Update (MU) eller genom att manuellt hämta den nya versionen från Download Center eller Volume License-plats.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Hur kan jag bekräfta vidarebefordran av Windows-händelser?
Du kan placera följande kod i en fil och sedan köra den från Kommandotolken i katalogen:  **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** enligt följande:

mongo.exe ATA-filnamn

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>Fungerar ATA med krypterad trafik?
ATA förlitar sig på analysen av flera nätverksprotokoll och även händelser som samlas in från SIEM eller via vidarebefordran av Windows-händelser. Identifieringar baserat på nätverksprotokoll med krypterad trafik (till exempel LDAPS och IPSEC) analyseras inte.


## <a name="does-ata-work-with-kerberos-armoring"></a>Fungerar ATA med Kerberos Armoring?
Aktivering av Kerberos Armoring, som även kallas Flexible Authentication Secure Tunneling (FAST), stöds av ATA, med undantag för identifiering av ”over-pass the hash” som inte fungerar.

## <a name="how-many-ata-gateways-do-i-need"></a>Hur många ATA-gatewayer behöver jag?

Antalet ATA-gatewayer beror på nätverkslayout, volym av paket och volym av händelser som avbildas av ATA. För att avgöra exakt antal, se [Storlek för ATA Lightweight Gateway](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Hur mycket lagringsutrymme måste jag ha för ATA?
För varje hel dag med i genomsnitt 1 000 paket/sek behöver du 0,3 GB lagring.<br /><br />Mer information om storlek för ATA Center finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Varför anses vissa konton känsliga?
Detta inträffar när ett konto är medlem i vissa grupper som vi anser vara känsliga (t.ex. "Domänadministratörer").

Om du vill förstå varför ett konto är känsligt kan du granska dess gruppmedlemskap för att förstå vilka känsliga grupper det tillhör (den grupp det tillhör kan också vara känslig till följd av en annan grupp, så samma process bör utföras tills du hittar den känsliga grupp som har högst nivå). 

Du kan också manuellt tagga en användare, grupp eller dator som känslig. Mer information finns i [tagga känsliga konton](tag-sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Hur övervakar jag en virtuell domänkontrollant med ATA?
De flesta virtuella domänkontrollanter kan omfattas av ATA Lightweight Gateway. Information för att fastställa om ATA Lightweight Gateway är lämpligt för din miljö finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).

Om en virtuell domänkontrollant inte kan omfattas av ATA Lightweight Gateway, kan du använda antingen en virtuell eller fysisk ATA-Gateway enligt beskrivningen i [konfigurera portspegling](configure-port-mirroring.md).  <br />Det enklaste sättet är att ha en virtuell ATA-gateway på varje värd där det finns en virtuell domänkontrollant.<br />Om de virtuella domänkontrollanterna flyttas mellan olika värdar, måste du göra något av följande steg:

-   När den virtuella domänkontrollanten flyttar till en annan värd ska ATA-gatewayen på den värden förkonfigureras för att ta emot trafiken från den virtuella domänkontrollant som precis har flyttats.
-   Se till att du kopplar den virtuella ATA-gatewayen till den virtuella domänkontrollanten, så att om den flyttas följer ATA-gatewayen med.
-   Det finns några virtuella växlar som kan skicka trafik mellan värdar.

## <a name="how-do-i-back-up-ata"></a>Hur säkerhetskopierar jag ATA?

Mer information finns i avsnittet om [haveriberedskap för ATA](disaster-recovery.md)



## <a name="what-can-ata-detect"></a>Vad kan ATA identifiera?

ATA identifierar kända skadliga attacker och tekniker, säkerhetsproblem och risker.
En fullständig lista över ATA-identifieringar finns i [Vilka identifieringar utför ATA?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Vilken typ av lagring behöver jag för ATA?
Vi rekommenderar snabb lagring (diskar med 7 200 RPM rekommenderas inte) med åtkomst till disken med låg latens (mindre än 10 ms). RAID-konfigurationen ska ha stöd för tung skrivbelastning (RAID-5/6 och tillhörande produkter rekommenderas inte).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>Hur många nätverkskort kräver ATA-gatewayen?
ATA-gatewayen måste ha minst två nätverkskort:<br>1. Ett nätverkskort för att ansluta till det interna nätverket och ATA Center<br>2. Ett nätverkskort som används för att avbilda domänkontrollantens nätverkstrafik via portspegling.<br>* Det här gäller inte för ATA Lightweight Gateway, som internt använder alla nätverkskort som domänkontrollanten använder.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Vilken typ av integrering har ATA med SIEM?
ATA har en dubbelriktad integrering med SIEM enligt följande:

1. ATA kan konfigureras för att skicka en Syslog-avisering till valfri SIEM-server som använder CEF-formatet när en misstänkt aktivitet har identifierats.
2. ATA kan konfigureras att ta emot Syslog-meddelanden för Windows-händelser från [dessa SIEM-servrar](install-ata-step6.md).

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Kan ATA övervaka domänkontrollanter som är visualiserade på IaaS-lösningen?
Ja, du kan använda ATA Lightweight Gateway för att övervaka domänkontrollanter som finns i valfri IaaS-lösning.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Är detta ett lokalt eller molnbaserat erbjudande?
Microsoft Advanced Threat Analytics är en lokal produkt.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Kommer det här att vara en del av Azure Active Directory eller lokal Active Directory?
Den här lösningen är för närvarande ett fristående erbjudande, det är inte en del av Azure Active Directory eller lokal Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Måste man skriva sina egna regler och skapa en tröskel/baslinje?
Med Microsoft Advanced Threat Analytics behöver du inte skapa regler, trösklar eller baslinjer och sedan finjustera. ATA analyserar beteende hos användare, enheter och resurser, samt deras förhållande till varandra, och kan identifiera misstänkt beteende och kända attacker snabbt. Tre veckor efter distributionen börjar ATA att identifiera misstänkta aktiviteter baserat på beteende. ATA börjar dock identifiera kända skadliga attacker och säkerhetsproblem direkt efter distributionen.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>Om du är ett brott mot, kan Microsoft Advanced Threat Analytics identifiera onormalt beteende?
Ja, även om ATA installeras efter att ett intrång har skett kan ATA identifiera misstänkta aktiviteter hos hackaren. ATA tittar inte bara på användarens beteenden utan jämför också med andra användare på organisationens säkerhetskarta. Under den inledande analystiden identifieras angriparens beteende, om det är onormalt, som en ”avvikare” och ATA fortsätter att rapportera det onormala beteendet. Dessutom kan ATA identifiera en misstänkt aktivitet om hackaren försöker stjäla en annan användares autentiseringsuppgifter, t.ex. vid Pass-the-Ticket, eller försök att utföra en fjärrkörning av en av domänkontrollanterna.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Använder detta endast trafik från Active Directory?
Förutom att analysera Active Directory-trafik med teknik för djup paketinspektion kan ATA också samla in relevanta händelser från SIEM (Security Information and Event Management) och skapa entitetsprofiler baserat på information från Active Directory Domain Services. ATA kan också samla in händelser från händelseloggarna om organisationen konfigurerar vidarebefordran av Windows-händelseloggar.

## <a name="what-is-port-mirroring"></a>Vad är portspegling?
Portspegling kallas även SPAN (Switched Port Analyzer) och är en metod för att övervaka nätverkstrafik. När portspegling är aktiverat skickar växeln en kopia av alla nätverkspaket som syns på en port (eller ett helt VLAN) till en annan port där paketet kan analyseras.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>Övervakar ATA endast domänanslutna enheter?
Nej. ATA övervakar alla enheter i nätverket som utför autentiserings- och auktoriseringsförfrågningar mot Active Directory, inklusive enheter som inte har Windows och mobila enheter.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>Övervakar ATA både datorkonton och användarkonton?
Ja. Eftersom datorn konton (samt eventuella andra entiteter) kan användas för att utföra skadliga aktiviteter, övervakar ATA alla datorn konton beteende och alla andra entiteter i miljön.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>ATA kan stödja flera domäner och flera skogar?
Microsoft Advanced Threat Analytics stöder miljöer med flera domäner i samma skogsgräns. Flera skogar kräver en ATA-distribution för varje skog.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Går det att se den övergripande hälsan för distributionen?
Ja, du kan visa den övergripande hälsan för den distribution och specifika problem som rör konfiguration, anslutning osv. du informeras när de inträffar.


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

