---
# required metadata

title: Krav för ATA | Microsoft Advanced Threat Analytics
description: Beskriver kraven för en lyckad distribution av ATA i din miljö
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Krav för ATA
Den här artikeln beskriver kraven för en lyckad distribution av ATA i din miljö.

>[!NOTE] Mer information om hur du planerar resurser och kapacitet finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).


ATA består av ATA Center, ATA Gateway och/eller ATA Lightweight Gateway. Mer information om ATA-komponenterna finns i [ATA-arkitektur](ata-architecture.md).


[Innan du börjar](#before-you-start): Det här avsnittet innehåller information som du bör samla in samt konton och nätverksentiteter som du bör ha innan du börjar installera ATA.

[ATA Center](#ata-center-requirements): Det här avsnittet innehåller maskin- och programvarukrav för ATA Center samt inställningar du måste konfigurera på ATA Center-servern.

[ATA Gateway](#ata-gateway-requirements): Det här avsnittet innehåller maskinvaru- och programvarukrav för ATA Gateway samt inställningar du måste konfigurera på ATA Gateway-servrarna.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): Det här avsnittet innehåller maskinvaru- och programvarukrav för ATA Lightweight Gateway.

[ATA-konsolen](#ata-console): Det här avsnittet innehåller webbläsarkrav för att köra ATA-konsolen.

![Diagram över ATA-arkitektur](media/ATA-architecture-topology.jpg)

## Innan du börjar
Det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera ATA.


-   Användarkonto och lösenord med läsbehörighet till alla objekt i de domäner som ska övervakas.

    > [!NOTE] Om du har angett anpassade ACL:er på olika organisationsenheter i domänen ska du se till att den valda användaren har läsbehörighet till de organisationsenheterna.

-   Ha en lista över alla undernät som används i nätverket för VPN och Wi-Fi, som omtilldelar IP-adresser mellan enheter inom en mycket kort tidsperiod (sekunder eller minuter).  Du bör identifiera de här undernäten med kortsiktiga lån så att ATA kan minska cachelivstiden för snabb omtilldelning mellan enheter. Information om konfiguration av undernät med kortsiktiga lån finns i [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata).
-   Kontrollera att Message Analyzer och Wire Shark inte är installerade på ATA Gateway eller ATA Center.
-    Valfritt: Användaren bör ha läsbehörighet till behållaren Borttagna objekt. Det gör att ATA kan identifiera massborttagning av objekt i domänen. Information om hur du konfigurerar läsbehörigheter för behållaren för borttagna objekt finns i avsnittet **Ändra behörigheter för en behållare för borttagna objekt ** i artikeln [Visa eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Valfritt: Ett användarkonto för en användare utan nätverksaktiviteter. Det här kontot konfigureras som ATA-honeytokenanvändaren. Om du vill konfigurera honeytoken-användaren behöver du användarkontots SID, inte användarnamnet.

-   Valfritt: Förutom att samla in och analysera nätverkstrafik till och från domänkontrollanterna kan ATA använda Windows-händelse 4776 för att förbättra ATA Pass-the-Hash-identifiering ytterligare. Den kan fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger ATA ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.


## Krav för ATA Center
Det här avsnittet innehåller kraven för ATA Center.
### Allmänt
ATA Center har stöd för installation på en server med Windows Server 2012 R2. ATA Center kan installeras på en server som är medlem i en domän eller arbetsgrupp.

Installation av ATA Center som en virtuell dator stöds. 

Om du kör ATA Center som en virtuell dator ska du stänga av servern innan du skapar en ny kontrollpunkt för att undvika att databasen skadas.
### Serverspecifikationer
ATA-databasen kräver att du **inaktiverar** NUMA (Non-Uniform Memory Access) i BIOS. NUMA kan kallas Node Interleaving i systemet. I så fall måste du **aktivera** Node Interleaving för att inaktivera NUMA. Mer information finns i BIOS-dokumentationen.<br>
För optimala prestanda ställer du in **Energialternativ** för ATA Center på **Höga prestanda**.<br>
Antalet domänkontrollanter som du övervakar och belastningen på var och en av domänkontrollanterna avgör serverspecifikationerna som krävs, mer information finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).

### Tidssynkronisering
ATA Center-servern, ATA Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.


### Nätverkskort
Du bör ha följande:
-   Minst ett nätverkskort

-   Två IP-adresser (rekommenderas men krävs inte)

Kommunikation mellan ATA Center och ATA Gateway krypteras med SSL på port 443. Dessutom körs ATA-konsolen på IIS och skyddas med SSL på port 443. **Två IP-adresser** rekommenderas. ATA Center-tjänsten binder port 443 till den första IP-adressen och IIS binder port 443 till den andra IP-adressen.

> [!NOTE] En enda IP-adress med två olika portar kan användas, men två IP-adresser rekommenderas.

### Portar
I följande tabell visas de portar som minst måste öppnas för att ATA Center ska fungera korrekt.

I den här tabellen är IP-adress 1 bunden till ATA Center-tjänsten och IP-adress 2 är bunden till IIS-tjänsten för ATA-konsolen:

|Protokoll|Transport|Port|Till/från|Riktning|IP-adress|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (ATA-kommunikation)|TCP|443, eller konfigurerbar|ATA Gateway|Inkommande|IP-adress 1|
|**HTTP**|TCP|80|Företagsnätverk|Inkommande|IP-adress 2|
|**HTTPS**|TCP|443|Företagsnätverk och ATA Gateway|Inkommande|IP-adress 2|
|**SMTP** (valfritt)|TCP|25|SMTP-server|Utgående|IP-adress 2|
|**SMTPS** (valfritt)|TCP|465|SMTP-server|Utgående|IP-adress 2|
|**Syslog** (valfritt)|TCP|514|Syslog-server|Utgående|IP-adress 2|

### Certifikat
Kontrollera att ATA Center har åtkomst till CRL-distributionsplatsen. Om ATA-gatewayerna inte har Internetåtkomst följer du [proceduren för att importera en CRL manuellt](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx), och ser till att installera alla CRL-distributionsplatser för hela kedjan.

För att underlätta installationen av ATA Center kan du installera självsignerade certifikat under installationen av ATA Center. Efter distributionen kan du ersätta de självsignerade certifikaten med ett certifikat från en intern certifikatutfärdare som ska användas av ATA Gateway.<br>
> [!NOTE] Certifikatets providertyp måste vara kryptografiprovider (CSP).


ATA Center kräver certifikat för följande tjänster:

-   IIS (Internet Information Services) – webbservercertifikat

-   ATA Center-tjänst – certifikat för serverautentisering

> [!NOTE] Om du kommer att ansluta till ATA-konsolen från andra datorer ska du se till att de datorerna litar på certifikatet som används av IIS. Annars visas en varningssida om att det finns ett problem med webbplatsens säkerhetscertifikat innan du kommer till inloggningssidan.

## Krav för ATA Gateway
Det här avsnittet innehåller kraven för ATA Gateway.
### Allmänt
ATA Gateway har stöd för installation på en server med Windows Server 2012 R2.
ATA Gateway kan installeras på en server som är medlem i en domän eller arbetsgrupp.

Innan du installerar ATA Gateway ska du kontrollera att följande uppdatering har installerats: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/).

Du kan kontrollera genom att köra följande Windows PowerShell-cmdlet: `[Get-HotFix -Id kb2919355]`.

Information om hur du använder virtuella datorer med ATA Gateway finns i [Konfigurera portspegling](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

### Serverspecifikationer
För bästa prestanda ställer du in **Energialternativ** för ATA Gateway på **Höga prestanda**.<br>
En ATA-gateway har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik till och från domänkontrollanterna.


### Tidssynkronisering
ATA Center-servern, ATA Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.

### Nätverkskort
ATA- gatewayen kräver minst ett hanteringskort och minst ett avbildningskort:

-   **Hanteringskort** – används för kommunikation i företagsnätverket. Kortet ska konfigureras med följande:

    -   Statisk IP-adress, inklusive standardgateway

    -   Primära och sekundära DNS-servrar

    -   **DNS-suffix för den här anslutningen** ska vara domänens DNS-namn för varje domän som övervakas.

        ![Konfigurera DNS-suffix i avancerade TCP/IP-inställningar](media/ATA-DNS-Suffix.png)

        > [!NOTE] Om ATA-gatewayen är medlem i domänen konfigureras det automatiskt.

-   **Avbildningskort** – används för att avbilda trafik till och från domänkontrollanterna.

    > [!IMPORTANT]
    > -   Konfigurera portspegling för avbildningskortet som mål för domänkontrollantens nätverkstrafik. Mer information finns i [Konfigurera portspegling](/advanced-threat-analytics/deploy-use/configure-port-mirroring). Vanligtvis behöver du samarbeta med nätverks- eller virtualiseringsteamet när du vill konfigurera portspegling.
    > -   Konfigurera en statisk icke-dirigerbar IP-adress för miljön utan standardgateway och utan DNS-serveradresser. Exempel: 1.1.1.1/32. Det garanterar att avbildningsnätverkskortet kan avbilda maximal mängd trafik och att hanteringsnätverkskortet används för att skicka och ta emot nödvändig nätverkstrafik.

### Portar
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
|SSL|TCP|443 eller enligt konfiguration för Center-tjänsten|ATA Center:<br /><br />–   IP-adress för Center-tjänsten<br />–   IP-adress för IIS|Utgående|
|Syslog (valfritt)|UDP|514|SIEM-server|Inkommande|

> [!NOTE] Som en del av lösningsprocessen som utförs av ATA Gateway måste följande portar vara öppna för inkommande på enheter i nätverket från ATA-gatewayerna.
>
> -   NTLM över RPC
> -   NetBIOS

### Certifikat
Kontrollera att ATA Center har åtkomst till CRL-distributionsplatsen. Om ATA-gatewayerna inte har Internetåtkomst följer du proceduren för att importera en CRL manuellt, och ser till att installera alla CRL-distributionsplatser för hela kedjan.<br>
För att underlätta installationen av ATA Center kan du installera självsignerade certifikat under installationen av ATA Center. Efter distributionen kan du ersätta de självsignerade certifikaten med ett certifikat från en intern certifikatutfärdare som ska användas av ATA Gateway.

> [!NOTE]
Certifikatets providertyp måste vara kryptografiprovider (CSP).<br>

Ett certifikat med stöd för **serverautentisering** måste vara installerat i datorarkivet för ATA Gateway i det lokala datorarkivet. Certifikatet måste vara betrott av ATA Center.

## Krav för ATA Lightweight Gateway
Det här avsnittet innehåller kraven för ATA Lightweight Gateway.
### Allmänt
ATA Lightweight Gateway har stöd för installation på en domänkontrollant som kör Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.

Domänkontrollanten kan vara en skrivskyddad domänkontrollant (RODC).

Domänkontrollanten kan inte vara Server Core.

### Serverspecifikationer

ATA Lightweight Gateway kräver att minst 2 kärnor och 6 GB RAM är installerat på domänkontrollanten.
För bästa prestanda ställer du in **Energialternativ** för ATA Lightweight Gateway på **Höga prestanda**.
ATA Lightweight Gateway kan distribueras på domänkontrollanter med olika belastningar och storlekar, beroende på mängden nätverkstrafik till och från domänkontrollanterna och mängden resurser som finns installerade på den domänkontrollanten.

### Tidssynkronisering
ATA Center-servern, ATA Lightweight Gateway-servrarna och domänkontrollanterna måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.
### Nätverkskort
ATA Lightweight Gateway övervakar lokal trafik på alla nätverkskort för domänkontrollanten. <br>
Efter distributionen kan använda du ATA-konsolen om du vill ändra vilka nätverkskort som ska övervakas.

### Portar
I följande tabell visas de portar som ATA Lightweight Gateway som minst kräver:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Utgående|
|NetBIOS|UDP|137|Alla enheter i nätverket|Utgående|
|SSL|TCP|443 eller enligt konfiguration för Center-tjänsten|ATA Center:<br /><br />–   IP-adress för Center-tjänsten<br />–   IP-adress för IIS|Utgående|
|Syslog (valfritt)|UDP|514|SIEM-server|Inkommande|

> [!NOTE] Som en del av lösningsprocessen som utförs av ATA Gateway måste följande portar vara öppna för inkommande på enheter i nätverket från ATA Lightweight-gatewayerna.
>
> -   NTLM över RPC
> -   NetBIOS

### Certifikat
Kontrollera att ATA Center har åtkomst till CRL-distributionsplatsen. Om ATA Lightweight-gatewayerna inte har Internetåtkomst följer du proceduren för att importera en CRL manuellt, och ser till att installera alla CRL-distributionsplatser för hela kedjan.
För att underlätta installationen av ATA Center kan du installera självsignerade certifikat under installationen av ATA Center. Efter distributionen kan du ersätta de självsignerade certifikaten med ett certifikat från en intern certifikatutfärdare som ska användas av ATA Lightweight Gateway.
> [!NOTE]
Certifikatets providertyp måste vara kryptografiprovider (CSP).

Ett certifikat med stöd för serverautentisering måste vara installerat i datorarkivet för ATA Lightweight Gateway i det lokala datorarkivet. Certifikatet måste vara betrott av ATA Center.

## ATA-konsolen
Åtkomst till ATA-konsolen sker via en webbläsare. Följande stöds:

-   Internet Explorer version 10 och senare

-   Google Chrome 40 och senare

-   Minsta bredd för skärmupplösning på 1 700 bildpunkter

## Se även

- [ATA-arkitektur](ata-architecture.md)
- [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO4-->

