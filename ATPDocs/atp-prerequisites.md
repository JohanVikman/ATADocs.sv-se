---
title: Krav för Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver kraven för en lyckad distribution av Azure ATP i din miljö
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1fc2b3656701ee5db54a4f918ab617a2ad487780
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="azure-atp-prerequisites"></a>Krav för Azure ATP
Den här artikeln beskrivs kraven för en lyckad distribution av Azure ATP i din miljö.

>[!NOTE]
> Information om hur du planerar resurser och kapacitet finns [Azure ATP kapacitetsplanering](atp-capacity-planning.md).


Azure ATP består av Azure ATP-Molntjänsten, som består av hanteringsportalen arbetsyta och arbetsytan-portalen, Azure ATP fristående sensor och/eller Azure ATP-sensor. Mer information om Azure ATP-komponenterna finns [Azure ATP arkitektur](atp-architecture.md).

Varje arbetsyta i Azure ATP stöder en gräns för Active Directory-skog och skogens funktionella nivå (FFL) av Windows 2003 och senare. En separat Azure ATP-arbetsyta krävs för distributioner med flera skogar för varje skog.


[Innan du börjar](#before-you-start): det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera Azure ATP.

[Azure-hanteringsportalen för ATP arbetsytan](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): det här avsnittet beskrivs webbläsarkrav arbetsytan management portal.

[Azure portal för ATP arbetsytan](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): det här avsnittet beskrivs Webbläsarkrav för att köra Azure ATP arbetsytan portal.

[Azure ATP fristående sensor](#azure-atp-sensor-requirements): det här avsnittet innehåller Azure ATP fristående sensor maskinvara, programvarukrav samt inställningar du behöver konfigurera på Azure ATP fristående sensor-servrar.

[Azure ATP sensor](#azure-atp-lightweight-sensor-requirements): det här avsnittet innehåller Azure ATP sensor maskin- och programvarukrav.

![Arkitekturdiagram för Azure ATP](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Innan du börjar
Det här avsnittet innehåller information som du bör samla in och konton och nätverksentiteter som du bör ha innan du börjar installera Azure ATP.


-   En **lokalt** AD användarkonto och lösenord med läsbehörighet till alla objekt i de övervakade domänerna.

    > [!NOTE]
    > Om du har angett anpassade ACL:er på olika organisationsenheter i domänen ska du se till att den valda användaren har läsbehörighet till de organisationsenheterna.

-   Om du kör Wireshark på Azure ATP fristående sensor kommer du måste starta om Azure Advanced Threat Protection-sensor tjänsten när du har stoppat Wireshark avbildningen. Om inte, sensorn slutar att fånga in trafik.

- Om du försöker installera ATP-sensor på en dator som har konfigurerats med ett NIC-Teamindelning kort får ett fel vid installation. Om du vill installera ATP-sensor på en dator som har konfigurerats med NIC-teamindelning, se [Azure ATP sensor NIC-teamindelning problemet](troubleshooting-atp-known-issues.md#nic-teaming).

-    Rekommenderat: Användare ska ha läsbehörighet till behållaren för borttagna objekt. Detta gör att Azure ATP kan identifiera massborttagning av objekt i domänen. Information om hur du konfigurerar läsbehörigheter för behållaren för borttagna objekt finns i **ändra behörigheter för en behållare för borttagna objekt** under den [vy eller ange behörigheter för ett katalogobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) artikel.

-   Valfritt: Ett användarkonto för en användare utan nätverksaktiviteter. Det här kontot har konfigurerats som Azure ATP honeytokenanvändaren. Mer information finns i [konfigurera undantag och honeytokenanvändaren](install-atp-step7.md).

-   Valfritt: Vid distribution av fristående sensor, är det nödvändigt att vidarebefordra Windows-händelser 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045 till ATP att ytterligare förbättra Azure ATP Pass-the-Hash, Brute Force, ändring av känsliga grupper, honung token identifieringar och skapa skadliga tjänster. I Azure ATP-sensor emot händelserna automatiskt. I den fristående sensorn Azure ATP kan dessa händelser fås från SIEM eller genom att ange vidarebefordran av Windows-händelser från domänkontrollanten. Insamlade händelser ger Azure ATP med ytterligare information som inte är tillgänglig via domänkontrollantens nätverkstrafik.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>ATP arbetsytan management portal och arbetsytan portal krav för Azure
Åtkomst till Azure ATP arbetsytan portalen och Azure ATP arbetsytan management portal sker via en webbläsare som stöder följande webbläsare och inställningar:
-   Microsoft Edge
-   Internet Explorer version 10 och senare
-   Google Chrome 4.0 och senare
-   Minsta bredd för skärmupplösning på 1 700 bildpunkter
-   Brandvägg/proxy – öppna - att kommunicera med Azure ATP-Molntjänsten, som är öppna: *. atp.azure.com port 443 i din brandvägg/proxyserver. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Krav för Azure sensor för ATP fristående
Det här avsnittet innehåller kraven för Azure ATP fristående sensorn.
### <a name="general"></a>Allmänt
Azure ATP fristående sensorn har stöd för installation på en server som kör Windows Server 2012 R2 eller Windows Server 2016 (inkludera server core).
Azure ATP fristående sensor kan installeras på en server som är medlem i en domän eller arbetsgrupp.
Azure ATP fristående sensor kan användas för att övervaka domänkontrollanter med domänens funktionsnivå nivå av Windows 2003 och senare.

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna port 443 i dina brandväggar och proxyservrar till *. atp.azure.com.


Information om hur du använder virtuella datorer med Azure ATP fristående sensor finns [konfigurera portspegling](configure-port-mirroring.md).

> [!NOTE]
> Minst 5 GB ledigt diskutrymme krävs och 10 GB rekommenderas. Detta inkluderar utrymme som krävs för Azure ATP binärfiler, Azure ATP loggar och prestanda loggar.

### <a name="server-specifications"></a>Serverspecifikationer
För optimala prestanda ställer du in den **Energialternativ** av Azure ATP fristående sensor till **högpresterande**.<br>
En fristående Azure ATP-sensor har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik till och från domänkontrollanterna.

>[!NOTE] 
> När du kör som en virtuell dator stöds inte dynamiskt minne eller någon annan minne ballooning funktion.

Mer information om maskinvarukrav för Azure ATP fristående sensor finns [Azure ATP kapacitetsplanering](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering

Servrar och domänkontrollanter som sensorn har installerats måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.


### <a name="network-adapters"></a>Nätverkskort
Azure ATP fristående sensor kräver minst ett hanteringskort och minst ett avbildningskort:

-   **Hanteringskortet** – används för kommunikation i företagsnätverket. Sensorn använder det här nätverkskortet för att fråga DC den skyddar och matchning till datorkonton. <br>Det här kortet ska konfigureras med följande inställningar:

    -   Statisk IP-adress, inklusive standardgateway

    -   Primära och sekundära DNS-servrar

    -   **DNS-suffix för den här anslutningen** ska vara domänens DNS-namn för varje domän som övervakas.

        ![Konfigurera DNS-suffix i avancerade TCP/IP-inställningar](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Om Azure ATP fristående sensor är medlem i domänen, kan det konfigureras automatiskt.

-   **Avbildningskort** – används för att avbilda trafik till och från domänkontrollanterna.

    > [!IMPORTANT]
    > -   Konfigurera portspegling för avbildningskortet som mål för domänkontrollantens nätverkstrafik. Mer information finns i [konfigurera portspegling](configure-port-mirroring.md). Normalt behöver arbeta med nätverks- eller -teamet för att konfigurera portspegling.
    > -   Konfigurera en statisk icke-dirigerbara IP-adress för din miljö med ingen standard sensor och ingen DNS-serveradresser. Exempel: 1.1.1.1/32. Detta garanterar att avbildningsnätverkskortet kan avbilda maximal mängd trafik och att hanteringsnätverkskortet används för att skicka och ta emot nödvändig nätverkstrafik.

### <a name="ports"></a>Portar
I följande tabell visas de portar som minst kräver Azure ATP fristående sensor konfigurerade på Hanteringskortet:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|**Internet-portar**|||||
|SSL (*.atp.azure.com)|TCP|443|Molntjänsten Azure ATP|Utgående|
|**Interna portar**|||||
|LDAP|TCP och UDP|389|Domänkontrollanter|Utgående|
|Säkert LDAP (LDAPS)|TCP|636|Domänkontrollanter|Utgående|
|LDAP till global katalog|TCP|3268|Domänkontrollanter|Utgående|
|LDAPS till global katalog|TCP|3269|Domänkontrollanter|Utgående|
|Kerberos|TCP och UDP|88|Domänkontrollanter|Utgående|
|Netlogon (SMB, CIFS, SAM-R)|TCP och UDP|445|Alla enheter på nätverket|Utgående|
|Windows Time|UDP|123|Domänkontrollanter|Utgående|
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Utgående|
|NetBIOS|UDP|137|Alla enheter i nätverket|Utgående|
|Syslog (valfritt)|TCP/UDP|514, beroende på konfiguration|SIEM-server|Inkommande|
|RADIUS|UDDP|1813|RADIUS|Inkommande|
|RDP|TCP|3389|Alla enheter på nätverket|Utgående|

> [!NOTE]
> - Med Directory service-användarkonto sensorn frågar slutpunkter i din organisation för lokala administratörer använda SAM-R (nätverksinloggning) för att skapa den [lateral förflyttning sökväg diagram](use-case-lateral-movement-path.md). Mer information finns i [konfigurera SAM-R nödvändiga behörigheter](install-atp-step8-samr.md).
> - Följande portar måste vara öppna för inkommande på enheter i nätverket från Azure ATP fristående sensorer:
>   -   NTLM över RPC (TCP-Port 135) för framtida bruk
>   -   NetBIOS (UDP-port 137) för framtida bruk
>   -   RDP (TCP-port 3389), bara första paketet av *klientens hälsning*, för framtida bruk<br> Observera att ingen autentisering utförs på någon av portarna.

## <a name="azure-atp-sensor-requirements"></a>Krav för Azure ATP-temperatursensor
Det här avsnittet innehåller kraven för Azure ATP sensorn.
### <a name="general"></a>Allmänt
Azure ATP sensorn har stöd för installation på en domänkontrollant som kör Windows Server 2008 R2 SP1 (inklusive inte Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (inklusive Core men inte Nano).

Domänkontrollanten kan vara en skrivskyddad domänkontrollant (RODC).

För domänkontrollanterna att kommunicera med Molntjänsten, måste du öppna port 443 i dina brandväggar och proxyservrar till *. atp.azure.com.

Under installationen av .net Framework 4.7 har installerats och kan kräva en omstart av domänkontrollanten om en omstart pågår redan.


> [!NOTE]
> Minst 5 GB ledigt diskutrymme krävs och 10 GB rekommenderas. Detta inkluderar utrymme som krävs för Azure ATP binärfiler, Azure ATP loggar och prestanda loggar.

### <a name="server-specifications"></a>Serverspecifikationer

Azure ATP-sensor kräver minst två kärnor och 6 GB RAM-minne på domänkontrollanten.
För optimala prestanda ställer du in den **Energialternativ** av Azure ATP sensor till **högpresterande**.
Azure ATP-sensor kan distribueras på domänkontrollanter med olika belastningar och storlekar, beroende på mängden nätverkstrafik till och från domänkontrollanterna och mängden resurser som finns installerade på domänkontrollanten.

>[!NOTE] 
> När du kör som en virtuell dator stöds inte dynamiskt minne eller någon annan minne ballooning funktion.

Mer information om maskinvarukrav för Azure ATP sensor finns [Azure ATP kapacitetsplanering](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Tidssynkronisering

Servrar och domänkontrollanter som sensorn har installerats måste ha tidsinställningen synkroniserad högst 5 minuter från varandra.

### <a name="network-adapters"></a>Nätverkskort

Azure ATP-sensor övervakar lokal trafik på alla nätverkskort för domänkontrollanten. <br>
Efter distributionen kan använda du Azure ATP arbetsytan portal om du vill ändra vilka nätverkskort som ska övervakas.

Sensorn stöds inte på domän aktiverad för domänkontrollanter som kör Windows 2008 R2 med Broadcom kombination för nätverkskort.

### <a name="ports"></a>Portar
I följande tabell visas de portar som Azure ATP-sensor kräver minst:

|Protokoll|Transport|Port|Till/från|Riktning|
|------------|-------------|--------|-----------|-------------|
|**Internet-portar**|||||
|SSL (*.atp.azure.com)|TCP|443|Molntjänsten Azure ATP|Utgående|
|**Interna portar**|||||
|DNS|TCP och UDP|53|DNS-servrar|Utgående|
|NTLM över RPC|TCP|135|Alla enheter i nätverket|Utgående|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Alla enheter på nätverket|Utgående|
|NetBIOS|UDP|137|Alla enheter i nätverket|Utgående|
|Syslog (valfritt)|TCP/UDP|514, beroende på konfiguration|SIEM-server|Inkommande|
|RADIUS|UDDP|1813|RADIUS|Inkommande|
|TLS ska RDP-porten|TCP|3389|Alla enheter på nätverket|Utgående|

> [!NOTE]
> - Med Directory service-användarkonto sensorn frågar slutpunkter i din organisation för lokala administratörer använda SAM-R (nätverksinloggning) för att skapa den [lateral förflyttning sökväg diagram](use-case-lateral-movement-path.md). Mer information finns i [konfigurera SAM-R nödvändiga behörigheter](install-atp-step8-samr.md).
> - Följande portar måste vara öppna för inkommande på enheter i nätverket från Azure ATP fristående sensorer:
>   -   NTLM över RPC (TCP-Port 135) för framtida bruk
>   -   NetBIOS (UDP-port 137) för framtida bruk
>   -   RDP (TCP-port 3389), bara första paketet av *klientens hälsning*, för framtida bruk<br> Observera att ingen autentisering utförs på någon av portarna.




## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Azure ATP-arkitektur](atp-architecture.md)
- [Installera ATP](install-atp-step1.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)

