---
title: Nyheter i ATA version 1.8 | Microsoft Docs
description: "Innehåller en lista med nyheter i ATA version 1.8 tillsammans med kända problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/14/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 1ec9308e046a228ac1276eb1aace58eec47e95d0
ms.sourcegitcommit: 8b622fa5457cf1a540504899c8c98e860b946e01
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/14/2017
---
# <a name="whats-new-in-ata-version-18"></a>Nyheter i ATA version 1.8

Den senast uppdaterade versionen av ATA går att [ladda ned från Download Center](https://www.microsoft.com/download/details.aspx?id=55536). Det går också att ladda ned den fullständig versionen från [utvärderingscentret](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Den här versionsinformationen innehåller information om uppdateringar, nya funktioner, felkorrigeringar och kända problem i den här versionen av Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Nya och uppdaterade identifieringar

- Onormal protokollimplementering har förbättrats för att kunna identifiera skadlig WannaCry-kod.

- Nytt! **Onormal modifiering av känsliga grupper** – Som en del av behörighetseskaleringsfasen ändrar angripare grupper med höga privilegier för att få åtkomst till känsliga resurser. Nu identifierar ATA onormala ändringar i grupper med höga privilegier.
- Nytt! **Misstänkta misslyckade autentiseringar** (beteendebaserad brute force) – Angripare försöker utföra en råstyrkeattack mot autentiseringsuppgifter för att kompromettera konton. Nu genererar ATA en avisering när onormalt beteende vid misslyckade autentiseringar identifieras.   

- **Fjärrkörningsförsök – WMI-exekvering** – Angripare kan försöka få kontroll över nätverket genom att fjärrköra kod på din domänkontrollant. Identifieringen av fjärrkörning har förbättrats i ATA och omfattar nu även WMI-metoder för fjärrkörning av kod.

- Rekognosering med katalogtjänstfrågor – Den här identifieringen har förbättrats för att kunna fånga frågor mot en enskild känslig entitet och för att minska antalet falska positiva identifieringar som genererades i den förra versionen. Om du har inaktiverat den här identifieringen i version 1.7 aktiveras den automatiskt när du installerar version 1.8.

- Kerberos Golden ticket-aktivitet – ATA 1.8 innehåller en till teknik för att identifiera Golden ticket-attacker.
    - Nu identifierar ATA misstänkta aktiviteter där Golden ticket-biljettens livslängd har gått ut. Om en Kerberos-biljett används under längre tid än den tillåtna livslängden identifierar ATA detta som en misstänkt aktivitet som indikerar att en Golden ticket-biljett troligen har skapats.
- Förbättringar har gjorts i följande identifieringar för att minska antalet kända falska positiva identifieringar:  
    - Identifiering av behörighetseskalering (förfalskat PAC) 
    - Aktivitet för nedgradering av kryptering (Skeleton Key)
    - Onormal protokollimplementering
    - Brutet förtroende

## <a name="improved-triage-of-suspicious-activities"></a>Förbättrad prioritering av misstänkta aktiviteter

-   Nytt! I ATA 1.8 kan du köra följande åtgärder för misstänkta aktiviteter under prioriteringsprocessen: 
    - **Undanta entiteter** så att ATA inte aviserar om misstänkta aktiviteter som i själva verket utgör harmlösa korrekta positiva identifieringar (t.ex. en administratör som kör fjärrkod eller identifiering av säkerhetsgenomsökningar).
    - **Ignorera återkommande** misstänkta aktiviteter så att de inte utlöser aviseringar.
    - **Ta bort misstänkta aktiviteter** från tidslinjen för attacker.
-   Processen för uppföljning av aviseringar om misstänkta aktiviteter har effektiviserats. Tidslinjen för misstänkta aktiviteter har omarbetats. I ATA 1.8 kan du se många fler misstänkta aktiviteter på samma skärm, som innehåller bättre information om prioriteringar och undersökningar. 

## <a name="new-reports-to-help-you-investigate"></a>Nya rapporter som underlättar dina undersökningar 
-   Nytt! En **sammanfattningsrapport** har lagts till så att du kan se alla sammanfattade data från ATA, inklusive misstänkta aktiviteter, problem med hälsotillstånd och mer. Du kan även definiera en anpassad rapport som genereras automatiskt och regelbundet.
-   Nytt! En **rapport för känsliga grupper** har lagts till så att du kan se alla ändringar som gjorts i känsliga grupper under en viss tidsperiod.


## <a name="infrastructure-improvements"></a>Förbättringar i infrastrukturen

-   ATA Centers prestanda har förbättrats. I ATA 1.8 kan ATA Center hantera över 1 miljon paket per sekund.
-   ATA Lightweight Gateway kan nu läsa händelser lokalt, utan att du behöver konfigurera vidarebefordran av händelser.
-   Nu kan du konfigurera e-post för övervakningsaviseringar och misstänkta aktiviteter separat.

## <a name="security-improvements"></a>Förbättringar av säkerhet

-   Nytt! **Enkel inloggning för ATA-hantering**. ATA har stöd för enkel inloggning integrerat med Windows-autentisering. Om du redan har loggat in på datorn använder ATA den token för att logga in dig i ATA-konsolen. Du kan också logga in med ett smartkort. Nu använder skripten för obevakade installationer för ATA Gateway och ATA Lightweight Gateway den inloggade användarens kontext, och inga autentiseringsuppgifter behöver uppges.
-   Privilegierna för lokalt system har tagits bort från ATA Gateway-processen, vilket betyder att du nu kan använda virtuella konton (endast tillgängligt på fristående ATA-gatewayer), hanterade tjänstkonton och grupphanterade tjänstkonton för att köra ATA Gateway-processen.   
-   Granskningsloggar för ATA Center och ATA-gatewayer har lagts till och alla åtgärder loggas nu i Windows-händelseloggen.
-   Stöd har lagts till för KSP-certifikat för ATA Center.

## <a name="additional-changes"></a>Ytterligare ändringar

- Alternativet att lägga till anteckningar har tagits bort från misstänkta aktiviteter
- Rekommendationer för hur du minimerar misstänkta aktiviteter har tagits bort från i tidslinjen för misstänkta aktiviteter.
- Från och med ATA version 1.8 ATA-gatewayer och Lightweight-gatewayer hanterar sina egna certifikat och behöver ingen åtgärd av administratör ska kunna hanteras.

## <a name="known-issues"></a>Kända problem

> [!WARNING]
> För att undvika kända problem du uppdateringen eller distribueras med hjälp av uppdatering 1.8 1.

### <a name="ata-gateway-on-windows-server-core"></a>ATA Gateway på Windows Server Core

**Symptom**: Uppgradering av en ATA Gateway till 1.8 på Windows Server 2012 R2 Core med .Net framework 4.7 kan misslyckas med felet: *Microsoft Advanced Threat Analytics Gateway har slutat fungera*. 

![Gateway-kärnfel](./media/gateway-core-error.png)

Felet kanske inte visas i Windows Server 2016 Core, men processen kommer att misslyckas när du försöker installera, och händelserna 1000 och 1001 (processkrasch) kommer att loggas i programmets händelselogg på servern.

**Beskrivning**: Det är problem med .NET Framework 4.7 som gör att program som använder WPF-teknik (till exempel ATA) inte kan läsas in. Mer information finns i [KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on) . 

**Lösning**: Avinstallera .Net 4.7 [KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) för att återställa .NET-versionen till .NET 4.6.2 och sedan uppdatera ATA Gateway till version 1.8. När ATA har uppgraderats kan du installera .NET 4.7 på nytt.  En framtida version kommer att innehålla en uppdatering för att åtgärda det här problemet.

### <a name="lightweight-gateway-event-log-permissions"></a>Lightweight Gateway-händelseloggbehörigheter

**Symptom**: När du uppgraderar ATA till version 1.8 kan appar eller tjänster som tidigare beviljats åtkomst till säkerhetshändelseloggen förlora behörigheterna. 

**Beskrivning**: För att underlätta distributionen av ATA får ATA 1.8 åtkomst till din säkerhetshändelselogg direkt, utan att konfiguration av Windows Event Forwarding krävs. Samtidigt körs ATA som en lokal tjänst med låg behörighet för att upprätthålla bättre säkerhet. ATA-tjänsten beviljar sig själv behörighet till säkerhetshändelseloggen för att ge åtkomst till ATA att läsa händelserna. Då kan behörigheter som tidigare angetts för andra tjänster inaktiveras.

**Lösning**: Kör följande Windows PowerShell-skript. Då tas behörigheterna som felaktigt lagts till i registret bort från ATA och läggs till via ett annat API. Då kan behörigheter för andra appar återställas. Om det inte sker måste de återställas manuellt. En framtida version kommer att innehålla en uppdatering för att åtgärda det här problemet. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Proxygränssnitt

**Symptom**: Efter uppgradering till ATA 1.8 kanske det inte går att starta ATA Gateway-tjänsten. I ATA-felloggen visas följande undantag: *System.Net.Http.HttpRequestException: Ett fel inträffade när begäran skickades. ---> System.Net.WebException: Fjärrservern returnerade ett fel: (407) Proxyautentisering krävs.*

**Beskrivning**: Från och med ATA 1.8 kommunicerar ATA Gateway med ATA Center med hjälp av HTTP-protokollet. Om datorn där du installerade ATA Gateway använder en proxyserver för att ansluta till ATA Center kan kommunikationen avbrytas. 

**Lösning**: Inaktivera användningen av en proxyserver på ATA Gateway-tjänstkontot. En framtida version kommer att innehålla en uppdatering för att åtgärda det här problemet.


## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.8 – migreringsguide](ata-update-1.8-migration-guide.md)

