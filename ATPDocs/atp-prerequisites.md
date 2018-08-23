---
title: Krav för Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver kraven för en lyckad distribution av Azure ATP i din miljö
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fea95d0cfdcca96eba1f77b6dbd81a101b3782
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734820"
---
*Gäller för: Azure Avancerat skydd*



# <a name="azure-atp-prerequisites"></a>Azure ATP-krav
Den här artikeln beskrivs kraven för en lyckad distribution av Azure ATP i din miljö.

>[!NOTE]
> Information om hur du planerar resurser och kapacitet finns i [Azure ATP-kapacitetsplanering](atp-capacity-planning.md).


Azure ATP består av Azure ATP-Molntjänsten, som består av hanteringsportalen, arbetsytans portal, Azure ATP-sensorn eller fristående Azure ATP-sensorn. Mer information om var och en av de Azure ATP-komponenterna finns i [Azure ATP-arkitektur](atp-architecture.md).

Varje Azure ATP-instans har stöd för en gräns för flera Active Directory-skog och skogens funktionella nivå (FFL) av Windows 2003 och senare. 


[Innan du börjar](#before-you-start): det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera Azure ATP.

[Azure ATP-hanteringsportalen](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): det här avsnittet beskrivs Webbläsarkrav för Azure ATP management portal.

[Azure ATP-arbetsyteportalen](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): det här avsnittet beskrivs Webbläsarkrav för att köra Azure ATP-arbetsyteportalen.

[Azure ATP-sensorn](#azure-atp-lightweight-sensor-requirements): det här avsnittet innehåller Azure ATP-sensorn maskin- och programvarukrav.

[Azure ATP fristående sensorn](#azure-atp-sensor-requirements): det här avsnittet innehåller Azure ATP fristående sensorn maskinvara, programvarukrav samt inställningar du måste konfigurera på din Azure ATP fristående sensor-servrar.

![Azure ATP-arkitekturdiagrammet](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Innan du börjar
Det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera Azure ATP.


-   En **lokala** AD-användarkonto och lösenord med läsbehörighet till alla objekt i de övervakade domänerna.

    > [!NOTE]
    > Om du har angett anpassade ACL:er på olika organisationsenheter i domänen ska du se till att den valda användaren har läsbehörighet till de organisationsenheterna.

-   Om du kör Wireshark i Azure ATP fristående sensorn behöver starta om tjänsten Azure Advanced Threat Protection sensor när du har stoppat Wireshark-insamlingen. Om inte, sensorn slutar att fånga in trafik.

- Om du försöker installera ATP-sensorn på en dator som konfigureras med en NIC-teamindelningsadapter, får du ett fel vid installation. Om du vill installera ATP-sensorn på en dator som konfigureras med NIC teaming kan du läsa [Azure ATP-sensorn NIC teaming problemet](troubleshooting-atp-known-issues.md#nic-teaming).

-    Rekommenderat: Ska användaren ha läsbehörighet för behållaren borttagna objekt. På så sätt kan Azure ATP kan identifiera massborttagning av objekt i domänen. Information om hur du konfigurerar läsbehörigheter för behållaren för borttagna objekt finns i den **ändring av behörigheter i en behållare för borttagna objekt** i avsnittet den [visa eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) artikeln.

-   Valfritt: Ett användarkonto för en användare utan nätverksaktiviteter. Det här kontot har konfigurerats som Azure ATP Honeytoken-användare. Mer information finns i [konfigurera undantag och Honeytoken-användare](install-atp-step7.md).

-   Valfritt: Om du distribuerar den fristående sensorn, är det nödvändigt att vidarebefordra Windows-händelserna 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045 till ATP att förbättra Azure ATP-Pass-the-Hash, Brute Force, ändring av känsliga grupper, Honey token-identifieringar och skapa skadliga tjänster. Azure ATP-sensorn tar emot dessa händelser automatiskt. I Azure ATP fristående sensorn tas händelserna emot från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger Azure ATP med ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Azure ATP-arbetsyta-portalen och arbetsytan portal hanteringskrav
Åtkomst till Azure ATP-arbetsyteportalen och hanteringsportalen för Azure ATP-arbetsytan är via en webbläsare som stöder följande webbläsare och inställningar:
-   Microsoft Edge
-   Internet Explorer version 10 och senare
-   Google Chrome 4.0 och senare
-   Minsta bredd för skärmupplösning på 1 700 bildpunkter
-   Öppna brandvägg/proxy – för att kommunicera med Molntjänsten Azure ATP *. atp.azure.com port 443 måste vara öppna i din brandväggsproxy. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Azure ATP fristående sensor-krav
Det här avsnittet innehåller kraven för fristående Azure ATP-sensorn.
### <a name="general"></a>Allmänt
Fristående Azure ATP-sensorn har stöd för installation på en server som kör Windows Server 2012 R2 eller Windows Server 2016 (inkludera server core).
Fristående Azure ATP-sensorn kan installeras på en server som är medlem i en domän eller arbetsgrupp.
Fristående Azure ATP-sensorn kan användas för att övervaka domänkontrollanter med domän funktionella nivån för Windows 2003 och senare.

Port 443 i brandväggar och proxyservrar till för din fristående sensorn att kommunicera med Molntjänsten *. atp.azure.com måste vara öppna.


Information om hur du använder virtuella datorer med Azure ATP-sensorn fristående finns i [konfigurera portspegling](configure-port-mirroring.md).

> [!NOTE]
> Minst 5 GB utrymme krävs och 10 GB rekommenderas. Detta inkluderar utrymmet som krävs för Azure ATP-binärfiler, Azure ATP-loggar och prestanda loggar.

### <a name="server-specifications"></a>Serverspecifikationer
För optimala prestanda ställer du in den **Energialternativ** för Azure ATP fristående sensor till **högpresterande**.<br>
En fristående Azure ATP-sensorn har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik till och från domänkontrollanterna.

>[!NOTE] 
> När du kör som en virtuell dator stöds inte dynamiskt minne eller någon annan minne ballooning-funktion.

Mer information om maskinvarukraven för Azure ATP fristående sensor finns [Azure ATP-kapacitetsplanering](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering

Servrar och domänkontrollanter på vilka sensorn installeras måste ha tidsinställningen synkroniserad högst fem minuter från varandra.


### <a name="network-adapters"></a>Nätverkskort
Fristående Azure ATP-sensorn kräver minst ett hanteringskort och minst ett avbildningskort:

-   **Hanteringskortet** – används för kommunikation i företagsnätverket. Sensorn använder det här nätverkskortet för att fråga DC den skyddar och matchning till datorkonton. <br>Det här kortet ska konfigureras med följande inställningar:

    -   Statisk IP-adress, inklusive standardgateway

    -   Primära och sekundära DNS-servrar

    -   **DNS-suffix för den här anslutningen** ska vara domänens DNS-namn för varje domän som övervakas.

        ![Konfigurera DNS-suffix i avancerade TCP/IP-inställningar](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Om den fristående Azure ATP-sensorn är medlem i domänen kan konfigureras den automatiskt.

-   **Avbildningskort** – används för att avbilda trafik till och från domänkontrollanterna.

    > [!IMPORTANT]
    > -   Konfigurera portspegling för avbildningskortet som mål för domänkontrollantens nätverkstrafik. Mer information finns i [konfigurera portspegling](configure-port-mirroring.md). Vanligtvis måste du arbeta med nätverks- eller -teamet att konfigurera portspegling.
    > -   Konfigurera en statisk icke-dirigerbara IP-adress för din miljö med någon standard-sensor och ingen DNS-serveradresser. Exempel: 1.1.1.1/32. Detta garanterar att avbildningsnätverkskortet kan avbilda maximal mängd trafik och att hanteringsnätverkskortet används för att skicka och ta emot nödvändig nätverkstrafik.

### <a name="ports"></a>Portar
I följande tabell visas de portar som minst kräver fristående Azure ATP-sensorn konfigurerade på Hanteringskortet:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|**Internet-portar**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP-molntjänst|Utgående|
|**Interna portar**|||||
|LDAP|TCP och UDP|389|Domänkontrollanter|Utgående|
|Säkert LDAP (LDAPS)|TCP|636|Domänkontrollanter|Utgående|
|LDAP till global katalog|TCP|3268|Domänkontrollanter|Utgående|
|LDAPS till global katalog|TCP|3269|Domänkontrollanter|Utgående|
|Kerberos|TCP och UDP|88|Domänkontrollanter|Utgående|
|Netlogon (SMB/CIFS, SAM-R)|TCP och UDP|445|Alla enheter i nätverket|Utgående|
|Windows Time|UDP|123|Domänkontrollanter|Utgående|
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Båda|
|NetBIOS|UDP|137|Alla enheter i nätverket|Båda|
|Syslog (valfritt)|TCP/UDP|514, beroende på konfiguration|SIEM-server|Inkommande|
|RADIUS|UDP|1813|RADIUS|Inkommande|
|TLS för RDP|TCP|3389|Alla enheter i nätverket|Båda|

> [!NOTE]
> - Använder användarkontot för Directory service, sensorn frågar slutpunkter i din organisation för lokala administratörer med SAM-R (nätverksinloggning) för att skapa den [laterala sökväg graph](use-case-lateral-movement-path.md). Mer information finns i [behörigheter som krävs för Konfigurera SAM-R](install-atp-step8-samr.md).
> - Följande portar måste vara öppna för inkommande på enheter i nätverket från Azure ATP fristående sensorer:
>   -   NTLM över RPC (TCP-Port 135) för framtida bruk
>   -   NetBIOS (UDP-port 137) för framtida bruk
>   -   RDP (TCP-port 3389), endast första paketet i *klientens hälsning*, för framtida bruk<br> Observera att ingen autentisering utförs på någon av portarna.

## <a name="azure-atp-sensor-requirements"></a>Krav för Azure ATP-sensorn
Det här avsnittet innehåller kraven för Azure ATP-sensorn.
### <a name="general"></a>Allmänt
Azure ATP-sensorn har stöd för installation på en domänkontrollant som kör Windows Server 2008 R2 SP1 (inkluderar inte Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (inkluderar Core men inte Nano).

Domänkontrollanten kan vara en skrivskyddad domänkontrollant (RODC).

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna port 443 i brandväggar och proxyservrar till *. atp.azure.com.

Under installationen, .net Framework 4.7 har installerats och kan kräva en omstart av domänkontrollanten om en omstart väntar redan.


> [!NOTE]
> Minst 5 GB utrymme krävs och 10 GB rekommenderas. Detta inkluderar utrymmet som krävs för Azure ATP-binärfiler, Azure ATP-loggar och prestanda loggar.

### <a name="server-specifications"></a>Serverspecifikationer

Azure ATP-sensorn kräver minst två kärnor och 6 GB RAM-minne på domänkontrollanten.
För optimala prestanda ställer du in den **Energialternativ** för Azure ATP-sensorn till **högpresterande**.
Azure ATP-sensorn kan distribueras på domänkontrollanter med olika belastningar och storlekar, beroende på mängden nätverkstrafik till och från domänkontrollanterna och mängden resurser som finns installerade på domänkontrollanten.

>[!NOTE] 
> När du kör som en virtuell dator stöds inte dynamiskt minne eller någon annan minne ballooning-funktion.

Mer information om maskinvarukraven för Azure ATP-sensorn finns [Azure ATP-kapacitetsplanering](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering

Servrar och domänkontrollanter på vilka sensorn installeras måste ha tidsinställningen synkroniserad högst fem minuter från varandra.

### <a name="network-adapters"></a>Nätverkskort

Azure ATP-sensorn övervakar lokal trafik på alla nätverkskort för domänkontrollanten. <br>
Efter distributionen kan använda du Azure ATP-arbetsyteportalen om du vill ändra vilka nätverkskort som ska övervakas.

Sensorn stöds inte på domän aktiverad för domänkontrollanter som kör Windows 2008 R2 med Broadcom Teamindelade nätverkskort.

### <a name="ports"></a>Portar
I följande tabell visas de portar som Azure ATP-sensorn kräver minst:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|**Internet-portar**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP-molntjänst|Utgående|
|**Interna portar**|||||
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|Netlogon (SMB/CIFS, SAM-R)|TCP/UDP|445|Alla enheter i nätverket|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Båda|
|NetBIOS|UDP|137|Alla enheter i nätverket|Båda|
|Syslog (valfritt)|TCP/UDP|514, beroende på konfiguration|SIEM-server|Inkommande|
|RADIUS|UDP|1813|RADIUS|Inkommande|
|TLS för att RDP-porten|TCP|3389|Alla enheter i nätverket|Båda|

> [!NOTE]
> - Använder användarkontot för Directory service, sensorn frågar slutpunkter i din organisation för lokala administratörer med SAM-R (nätverksinloggning) för att skapa den [laterala sökväg graph](use-case-lateral-movement-path.md). Mer information finns i [behörigheter som krävs för Konfigurera SAM-R](install-atp-step8-samr.md).
> - Följande portar måste vara öppna för inkommande på enheter i nätverket från Azure ATP fristående sensorer:
>   -   NTLM över RPC (TCP-Port 135) för framtida bruk
>   -   NetBIOS (UDP-port 137) för framtida bruk
>   -   RDP (TCP-port 3389), endast första paketet i *klientens hälsning*, för framtida bruk<br> Observera att ingen autentisering utförs på någon av portarna.




## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Azure ATP-arkitektur](atp-architecture.md)
- [Installera ATP](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)

