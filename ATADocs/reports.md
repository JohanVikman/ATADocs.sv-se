---
title: Arbeta med ATA-rapporter | Microsoft Docs
description: Beskriver hur du kan generera rapporter i ATA för att övervaka ditt nätverk.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eaa579a6b82bab27bba0ddb79b39f06bd495debc
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133233"
---
*Gäller för: Advanced Threat Analytics version 1.9*


# <a name="ata-reports"></a>ATA-rapporter

I avsnittet för ATA-rapporter i konsolen kan du generera rapporter som ger dig information om systemstatus, både systemhälsa och en rapport över misstänkta aktiviteter som har identifierats i din miljö.

Du kommer åt rapportsidan genom att klicka på rapportikonen på menyraden: ![rapportikon](./media/ata-report-icon.png).
Följande rapporter är tillgängliga: 

- **Sammanfattningsrapport**: sammanfattningsrapporten innehåller en instrumentpanel över systemets status i systemet. Det finns tre flikar: **Sammanfattning**, som visar vad som har identifierats i nätverket, **Open suspicious activities** (Öppna misstänkta aktiviteter), som visar en lista över misstänkta aktiviteter som du bör ta hand om, och **Open health issues** (Öppna problem med hälsotillstånd), som visar problem med systemhälsan i ATA som du bör åtgärda. Både misstänkta aktiviteter och hälsorelaterade problem är uppdelade efter typ. 

- **Ändring av känsliga grupper**: den här rapporten visar varje gång en ändring görs känsliga grupper (till exempel Administratörer).

- **Lösenord som exponerats i klartext**: vissa tjänster använder icke-säker LDAP-protokollet för att skicka autentiseringsuppgifter i klartext. Detta kan även inträffa för känsliga konton. Angripare som övervakar nätverkstrafiken kan fånga upp och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. Den här rapporten listar alla källa dator och kontonamn lösenord som ATA har identifierats som skickas i klartext. 

- **Laterala rörelsebanor till känsliga konton**: den här rapporten Listar de känsliga konton som exponeras via lateral förflyttning. Mer information finns i [Lateral förflyttning](use-case-lateral-movement-path.md)

Du kan generera en rapport på två sätt: antingen på begäran eller genom att schemalägga en rapport så att den med jämna mellanrum skickas till din e-postadress.

Så här genererar du en rapport på begäran:

1. Klicka på rapportikonen på menyraden i ATA-konsolen: ![rapportikon](./media/ata-report-icon.png).

2. Under den valda rapporten-typ, ange den **från** och **till** datum och klicka på **hämta**. 
 ![rapporter](./media/reports.png)

Så här genererar du en schemalagd rapport:
 
1. På sidan **Rapporter** klickar du på **Set scheduled reports** (Skapa schemalagda rapporter). Du kan också klicka på **Schemalagda rapporter** under Notifications and Reports (Meddelanden och rapporter) på konfigurationssidan i ATA-konsolen.

   ![Schemalägga rapporter](./media/ata-sched-reports.png)

  > [!NOTE]
  > Rapporter för daglig är utformade för att skickas strax efter midnatt UTC-tid.

2. Klicka på **schema** bredvid din valda rapporttyp att frekvens och e-postadress för leverans av rapporter och klicka på plustecknet bredvid e-postadressen att lägga till dem och klicka på **spara**.

   ![Frekvens och e-postadress för schemalagda rapporter](./media/sched-report1.png)


> [!NOTE]
> Schemalagda rapporter levereras via e-post och kan endast skickas om du redan har konfigurerat en e-postserver under **Configuration** och under **meddelanden och rapporter**väljer **e-post Server**.


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
