---
title: "Krav för Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver kraven för en lyckad distribution av ATA i din miljö"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 14b0d68ce797eeaa99c9e067f7f8caacee1a7b74
ms.sourcegitcommit: 3cd268cf353ff8bc3d0b8f9a8c10a34353d1fcf1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/16/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="ata-prerequisites"></a>Krav för ATA
Den här artikeln beskriver kraven för en lyckad distribution av ATA i din miljö.

>[!NOTE]
> Mer information om hur du planerar resurser och kapacitet finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).


ATA består av ATA Center, ATA Gateway och/eller ATA Lightweight Gateway. Mer information om ATA-komponenterna finns i [ATA-arkitektur](ata-architecture.md).

ATA-systemet fungerar på Active Directory-skogens gränser och stöder skogens funktionella nivå (FFL) för Windows 2003 och högre.


[Innan du börjar](#before-you-start): Det här avsnittet innehåller information som du bör samla in samt konton och nätverksentiteter som du bör ha innan du börjar installera ATA.

[ATA Center](#ata-center-requirements): Det här avsnittet innehåller maskin- och programvarukrav för ATA Center samt inställningar du måste konfigurera på ATA Center-servern.

[ATA Gateway](#ata-gateway-requirements): Det här avsnittet innehåller maskinvaru- och programvarukrav för ATA Gateway samt inställningar du måste konfigurera på ATA Gateway-servrarna.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): Det här avsnittet innehåller maskinvaru- och programvarukrav för ATA Lightweight Gateway.

[ATA-konsolen](#ata-console): Det här avsnittet innehåller webbläsarkrav för att köra ATA-konsolen.

![Diagram över ATA-arkitektur](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Innan du börjar
Det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera ATA.


-   Användarkonto och lösenord med läsbehörighet till alla objekt i de domäner som ska övervakas.

    > [!NOTE]
    > Om du har angett anpassade ACL:er på olika organisationsenheter i domänen ska du se till att den valda användaren har läsbehörighet till de organisationsenheterna.

-   Installera inte Analysverktyg för meddelanden på en ATA-gateway eller ATA Lightweight-gateway. Drivrutinen för Analysverktyg för meddelanden är inte kompatibel med drivrutinerna för ATA Gateway och ATA Lightweight Gateway. Om du kör Wireshark i ATA Gateway måste du starta om Microsoft Advanced Threat Analytics Gateway-tjänsten när du har stoppat Wireshark-insamlingen. Annars kommer gatewayen inte längre att samla in någon trafik. Observera att ATA Lightweight Gateway inte påverkas om du kör Wireshark på en ATA Lightweight-gateway.

-    Rekommenderat: Användaren bör ha läsbehörighet till behållaren Borttagna objekt. Det gör att ATA kan identifiera massborttagning av objekt i domänen. Information om hur du konfigurerar läsbehörigheter för behållaren för borttagna objekt finns i avsnittet **Ändra behörigheter för en behållare för borttagna objekt**  i artikeln [Visa eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Valfritt: Ett användarkonto för en användare utan nätverksaktiviteter. Det här kontot konfigureras som ATA-honeytokenanvändaren. Om du vill konfigurera honeytoken-användaren behöver du användarkontots SID, inte användarnamnet. Mer information finns i ämnet [Arbeta med identifieringsinställningar i ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings).

-   Valfritt: Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan ATA använda Windows-händelserna 4776, 4732, 4733, 4728, 4729, 4756 och 4757 för att ytterligare förbättra identifieringar av typen Pass-the-Hash, Brute Force, Ändring av känsliga grupper och Honey Token i ATA. Dessa kan hämtas från din SIEM-server eller genom vidarebefordran av Windows-händelser från din domänkontrollant. Insamlade händelser ger ATA ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.


## <a name="ata-center-requirements"></a>Krav för ATA Center
Det här avsnittet innehåller kraven för ATA Center.
### <a name="general"></a>Allmänt
ATA Center har stöd för installation på en server med Windows Server 2012 R2 eller Windows Server 2016. ATA Center kan installeras på en server som är medlem i en domän eller arbetsgrupp.

Innan du installerar ATA Center med Windows 2012 R2, ska du kontrollera att följande uppdatering har installerats: [KB2919355](https://support.microsoft.com/kb/2919355/).

Du kan kontrollera genom att köra följande Windows PowerShell-cmdlet: `[Get-HotFix -Id kb2919355]`.

Installation av ATA Center som en virtuell dator stöds. 

>[!NOTE] 
> Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.

Om du kör ATA Center som en virtuell dator ska du stänga av servern innan du skapar en ny kontrollpunkt för att undvika att databasen skadas.
### <a name="server-specifications"></a>Serverspecifikationer
När du arbetar på en fysisk server kräver ATA-databasen att du **inaktiverar** NUMA (Non-Uniform Memory Access) i BIOS. NUMA kan kallas Node Interleaving i systemet. I så fall måste du **aktivera** Node Interleaving för att inaktivera NUMA. Mer information finns i BIOS-dokumentationen. Obs! Det här gäller inte när ATA Center körs på en virtuell server.<br>
För optimala prestanda ställer du in **Energialternativ** för ATA Center på **Höga prestanda**.<br>
Antalet domänkontrollanter som du övervakar och belastningen på var och en av domänkontrollanterna avgör serverspecifikationerna som krävs, mer information finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Tidssynkronisering
ATA Center-servern, ATA Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.


### <a name="network-adapters"></a>Nätverkskort
Du bör ha följande:
-   Minst ett nätverkskort (om fysisk server i VLAN-miljö används, rekommenderar vi att två nätverkskort används)

-   En IP-adress för kommunikation mellan ATA Center och ATA Gateway har krypterats med SSL på port 443. 

### <a name="ports"></a>Portar
I följande tabell visas de portar som minst måste öppnas för att ATA Center ska fungera korrekt.

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|**SSL** (ATA-kommunikation)|TCP|443, eller konfigurerbar|ATA Gateway|Inkommande|
|**HTTP** (valfritt)|TCP|80|Företagsnätverk|Inkommande|
|**HTTPS**|TCP|443|Företagsnätverk och ATA Gateway|Inkommande|
|**SMTP** (valfritt)|TCP|25|SMTP-server|Utgående|
|**SMTPS** (valfritt)|TCP|465|SMTP-server|Utgående|
|**Syslog** (valfritt)|TCP|514|Syslog-server|Utgående|
|**LDAP**|TCP och UDP|389|Domänkontrollanter|Utgående|
|**LDAPS** (valfritt)|TCP|636|Domänkontrollanter|Utgående|
|**DNS**|TCP och UDP|53|DNS-servrar|Utgående|
|**Kerberos** (valfritt om domänansluten)|TCP och UDP|88|Domänkontrollanter|Utgående|
|**Netlogon** (valfritt om domänansluten)|TCP och UDP|445|Domänkontrollanter|Utgående|
|**Windows Time** (valfritt om domänansluten)|UDP|123|Domänkontrollanter|Utgående|

### <a name="certificates"></a>Certifikat
Kontrollera att ATA Center har åtkomst till CRL-distributionsplatsen. Om ATA-gatewayerna inte har internetåtkomst följer du [proceduren för att importera en CRL manuellt](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), och ser till att installera alla CRL-distributionsplatser för hela kedjan.

För att underlätta installationen av ATA kan du installera självsignerade certifikat under installationen. Efter distributionen kan du ersätta de självsignerade certifikaten med ett certifikat från en intern certifikatutfärdare som ska användas av ATA Gateway.<br>
> [!NOTE]
> Certifikatets providertyp kan vara Kryptografiprovider (CSP) eller Nyckellagringsprovider (KSP).


> Användning av automatisk certifikatförnyelse stöds inte.


> [!NOTE]
> Om du kommer att ansluta till ATA-konsolen från andra datorer ska du se till att de datorerna litar på certifikatet som används av ATA Center. Annars visas en varningssida om att det finns ett problem med webbplatsens säkerhetscertifikat innan du kommer till inloggningssidan.

## <a name="ata-gateway-requirements"></a>Krav för ATA Gateway
Det här avsnittet innehåller kraven för ATA Gateway.
### <a name="general"></a>Allmänt
ATA Gateway stöder installation på en server som kör Windows Server 2012 R2 eller Windows Server 2016 (inkludera server core).
ATA Gateway kan installeras på en server som är medlem i en domän eller arbetsgrupp.
ATA Gateway kan användas för att övervaka domänkontrollanter i domänens funktionella nivå för Windows 2003 och högre.

Innan du installerar ATA Gateway med Windows 2012 R2, ska du kontrollera att följande uppdatering har installerats: [KB2919355](https://support.microsoft.com/kb/2919355/).

Du kan kontrollera genom att köra följande Windows PowerShell-cmdlet: `[Get-HotFix -Id kb2919355]`.


Information om hur du använder virtuella datorer med ATA Gateway finns i [Konfigurera portspegling](configure-port-mirroring.md).

> [!NOTE]
> Det krävs minst 5 GB utrymme och 10 GB rekommenderas. Detta inkluderar utrymmet som krävs för ATA-binärfiler, [ATA-loggar](troubleshooting-ata-using-logs.md) och [prestandaloggar](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Serverspecifikationer
För bästa prestanda ställer du in **Energialternativ** för ATA Gateway på **Höga prestanda**.<br>
En ATA-gateway har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik till och från domänkontrollanterna.

>[!NOTE] 
> Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.

Mer information om ATA Gateways maskinvarukrav finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering
ATA Center-servern, ATA Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.

### <a name="network-adapters"></a>Nätverkskort
ATA- gatewayen kräver minst ett hanteringskort och minst ett avbildningskort:

-   **Hanteringskort** – används för kommunikation i företagsnätverket. Kortet ska konfigureras med följande:

    -   Statisk IP-adress, inklusive standardgateway

    -   Primära och sekundära DNS-servrar

    -   **DNS-suffix för den här anslutningen** ska vara domänens DNS-namn för varje domän som övervakas.

        ![Konfigurera DNS-suffix i avancerade TCP/IP-inställningar](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Om ATA Gateway är medlem i domänen kan den konfigureras automatiskt.

-   **Avbildningskort** – används för att avbilda trafik till och från domänkontrollanterna.

    > [!IMPORTANT]
    > -   Konfigurera portspegling för avbildningskortet som mål för domänkontrollantens nätverkstrafik. Mer information finns i [Konfigurera portspegling](configure-port-mirroring.md). Vanligtvis behöver du samarbeta med nätverks- eller virtualiseringsteamet när du vill konfigurera portspegling.
    > -   Konfigurera en statisk icke-dirigerbar IP-adress för miljön utan standardgateway och utan DNS-serveradresser. Exempel: 1.1.1.1/32. Det garanterar att avbildningsnätverkskortet kan avbilda maximal mängd trafik och att hanteringsnätverkskortet används för att skicka och ta emot nödvändig nätverkstrafik.

### <a name="ports"></a>Portar
I följande tabell visas de portar som ATA Gateway som minst kräver är konfigurerade på hanteringskortet:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP och UDP|389|Domänkontrollanter|Utgående|
|Säkert LDAP (LDAPS)|TCP|636|Domänkontrollanter|Utgående|
|LDAP till global katalog|TCP|3268|Domänkontrollanter|Utgående|
|LDAPS till global katalog|TCP|3269|Domänkontrollanter|Utgående|
|Kerberos|TCP och UDP|88|Domänkontrollanter|Utgående|
|Netlogon|TCP och UDP|445|Domänkontrollanter|Utgående|
|Windows Time|UDP|123|Domänkontrollanter|Utgående|
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Utgående|
|NetBIOS|UDP|137|Alla enheter i nätverket|Utgående|
|SSL|TCP|443 eller enligt konfiguration för Center-tjänsten|ATA Center:<br /><br />–   IP-adress för Center-tjänsten<br />- Konsolens IP-adress|Utgående|
|Syslog (valfritt)|UDP|514|SIEM-server|Inkommande|

> [!NOTE]
> Som en del av lösningsprocessen som utförs av ATA Gateway måste följande portar vara öppna för inkommande på enheter i nätverket från ATA-gatewayerna.
>
> -   NTLM över RPC (TCP-Port 135)
> -   NetBIOS (UDP-port 137)

## <a name="ata-lightweight-gateway-requirements"></a>Krav för ATA Lightweight Gateway
Det här avsnittet innehåller kraven för ATA Lightweight Gateway.
### <a name="general"></a>Allmänt
ATA Lightweight Gateway har stöd för installation på en domänkontrollant som kör Windows Server 2008 R2 SP1 (inkluderar inte Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (inkluderar Core men inte Nano).

Domänkontrollanten kan vara en skrivskyddad domänkontrollant (RODC).

Innan du installerar ATA Lightweight Gateway på en domänkontrollant som kör Windows Server 2012 R2, måste du bekräfta att följande uppdatering har installerats: [KB2919355](https://support.microsoft.com/kb/2919355/).

Du kan kontrollera genom att köra följande Windows PowerShell-cmdlet: `[Get-HotFix -Id kb2919355]`

Om installationen är för Windows Server 2012 R2 Server Core, måste följande uppdatering också installeras: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Du kan kontrollera genom att köra följande Windows PowerShell-cmdlet: `[Get-HotFix -Id kb3000850]`


Under installationen installeras .Net Framework 4.6.1 och det kan göra att domänkontrollanten startas om.


> [!NOTE]
> Det krävs minst 5 GB utrymme och 10 GB rekommenderas. Detta inkluderar utrymmet som krävs för ATA-binärfiler, [ATA-loggar](troubleshooting-ata-using-logs.md) och [prestandaloggar](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Serverspecifikationer

ATA Lightweight Gateway kräver att minst 2 kärnor och 6 GB RAM är installerat på domänkontrollanten.
För bästa prestanda ställer du in **Energialternativ** för ATA Lightweight Gateway på **Höga prestanda**.
ATA Lightweight Gateway kan distribueras på domänkontrollanter med olika belastningar och storlekar, beroende på mängden nätverkstrafik till och från domänkontrollanterna och mängden resurser som finns installerade på den domänkontrollanten.

>[!NOTE] 
> Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.

Mer information om ATA Lightweight Gateways maskinvarukrav finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering
ATA Center-servern, ATA Lightweight Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.
### <a name="network-adapters"></a>Nätverkskort
ATA Lightweight Gateway övervakar lokal trafik på alla nätverkskort för domänkontrollanten. <br>
Efter distributionen kan använda du ATA-konsolen om du vill ändra vilka nätverkskort som ska övervakas.

### <a name="ports"></a>Portar
I följande tabell visas de portar som ATA Lightweight Gateway som minst kräver:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Utgående|
|NetBIOS|UDP|137|Alla enheter i nätverket|Utgående|
|SSL|TCP|443 eller enligt konfiguration för Center-tjänsten|ATA Center:<br /><br />–   IP-adress för Center-tjänsten<br />- Konsolens IP-adress|Utgående|
|Syslog (valfritt)|UDP|514|SIEM-server|Inkommande|

> [!NOTE]
> Som en del av lösningsåtgärden som utförs av ATA Gateway måste följande portar vara öppna för inkommande på enheter i nätverket från ATA Lightweight-gatewayerna.
>
> -   NTLM över RPC
> -   NetBIOS

## <a name="ata-console"></a>ATA-konsolen
Åtkomst till ATA-konsolen sker via en webbläsare. Följande stöds:

-   Internet Explorer version 10 och senare

-   Microsoft Edge

-   Google Chrome 40 och senare

-   Minsta bredd för skärmupplösning på 1 700 bildpunkter

## <a name="see-also"></a>Se även

- [ATA-arkitektur](ata-architecture.md)
- [Installera ATA](install-ata-step1.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


