---
title: Nyheter i ATA version 1.8 | Microsoft Docs
description: "Innehåller en lista med nyheter i ATA version 1.8 tillsammans med kända problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/16/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 63dd37548dbf4e150f32880543c3bf421bf3fe71
ms.sourcegitcommit: 3cd268cf353ff8bc3d0b8f9a8c10a34353d1fcf1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/16/2017
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
-   Processen för uppföljning av aviseringar om misstänkta aktiviteter har effektiviserats. Tidslinjen för misstänkta aktiviteter har omarbetats. I ATA 1.8 kan du hantera många fler misstänkta aktiviteter på samma skärm, som innehåller bättre information om prioriteringar och undersökningar. 

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



## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Uppdatera ATA till version 1.8 – migreringsguide](ata-update-1.8-migration-guide.md)

