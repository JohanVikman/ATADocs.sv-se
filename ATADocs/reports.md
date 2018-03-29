---
title: Arbeta med ATA-rapporter | Microsoft Docs
description: Beskriver hur du kan generera rapporter i ATA för att övervaka ditt nätverk.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9a113d8d090c5a90a07043a0ef75e1be0fc840c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/28/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*


# <a name="ata-reports"></a>ATA-rapporter

I avsnittet för ATA-rapporter i konsolen kan du generera rapporter som ger dig information om systemstatus, både systemhälsa och en rapport över misstänkta aktiviteter som har identifierats i din miljö.

Du kommer åt rapportsidan genom att klicka på rapportikonen på menyraden: ![rapportikon](./media/ata-report-icon.png).
Följande rapporter är tillgängliga: 

- **Översiktsrapport**: I sammanfattningsrapporten presenterar en instrumentpanel status i systemet. Det finns tre flikar: **Sammanfattning**, som visar vad som har identifierats i nätverket, **Open suspicious activities** (Öppna misstänkta aktiviteter), som visar en lista över misstänkta aktiviteter som du bör ta hand om, och **Open health issues** (Öppna problem med hälsotillstånd), som visar problem med systemhälsan i ATA som du bör åtgärda. Både misstänkta aktiviteter och hälsorelaterade problem är uppdelade efter typ. 

- **Ändring av känsliga grupper**: den här rapporten visar varje gång en ändring görs till känsliga grupper (till exempel Administratörer).

- **Lösenord i klartext**: vissa tjänster använder LDAP-protokollet inte är säkra för att skicka autentiseringsuppgifter i klartext. Detta kan även bero på känsliga konton. Övervaka nätverkstrafik angripare kan fånga och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. Den här rapporten visar en lista över alla källa datorn och kontoinformation lösenord som ATA som identifierats som skickas i klartext. 

- **Lateral förflyttning sökvägar till känsliga konton**: den här rapporten visar de känsliga konton som är tillgängliga via lateral förflyttning sökvägar. Mer information finns i [Lateral förflyttning sökvägar](use-case-lateral-movement-path.md)

Du kan generera en rapport på två sätt: antingen på begäran eller genom att schemalägga en rapport så att den med jämna mellanrum skickas till din e-postadress.

Så här genererar du en rapport på begäran:

1. Klicka på rapportikonen på menyraden i ATA-konsolen: ![rapportikon](./media/ata-report-icon.png).

2. Under den valda rapporttyp, ange den **från** och **till** datum och klicka på **hämta**. 
 ![rapporter](./media/reports.png)

Så här genererar du en schemalagd rapport:
 
1. På sidan **Rapporter** klickar du på **Set scheduled reports** (Skapa schemalagda rapporter). Du kan också klicka på **Schemalagda rapporter** under Notifications and Reports (Meddelanden och rapporter) på konfigurationssidan i ATA-konsolen.

   ![Schemalägga rapporter](./media/ata-sched-reports.png)

  > [!NOTE]
  > De dagliga rapporterna som är utformade för att skickas strax efter midnatt UTC-tid.

2. Klicka på **schema** bredvid ditt valda rapporttyp Ange frekvens och e-postadress för leverans av rapporterna Klicka på plustecknet för att lägga till dem och klicka på e-postadresser **spara**.

   ![Frekvens och e-postadress för schemalagda rapporter](./media/sched-report1.png)


> [!NOTE]
> Schemalagda rapporter levereras via e-post och kan bara skickas om du redan har konfigurerat en e-postserver under **Configuration** och under **meddelanden och rapporter**väljer **e-post Server**.


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
