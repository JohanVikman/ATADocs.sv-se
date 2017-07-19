---
title: Arbeta med ATA-rapporter | Microsoft Docs
description: "Beskriver hur du kan generera rapporter i ATA för att övervaka ditt nätverk."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# <a name="ata-reports"></a>ATA-rapporter

I avsnittet för ATA-rapporter i konsolen kan du generera rapporter som ger dig information om systemstatus, både systemhälsa och en rapport över misstänkta aktiviteter som har identifierats i din miljö.

Du kommer åt rapportsidan genom att klicka på rapportikonen på menyraden: ![rapportikon](./media/ata-report-icon.png).
Följande rapporter är tillgängliga: 
- Sammanfattningsrapport: Sammanfattningsrapporten innehåller en instrumentpanel över systemets status. Det finns tre flikar: **Sammanfattning**, som visar vad som har identifierats i nätverket, **Open suspicious activities** (Öppna misstänkta aktiviteter), som visar en lista över misstänkta aktiviteter som du bör ta hand om, och **Open health issues** (Öppna problem med hälsotillstånd), som visar problem med systemhälsan i ATA som du bör åtgärda. Både misstänkta aktiviteter och hälsorelaterade problem är uppdelade efter typ. 
- Modification to sensitive groups (Ändring av känsliga grupper): Den här rapporten visar varje gång en ändring av känsliga grupper (till exempel Administratörer) gjorts.

Du kan generera en rapport på två sätt: antingen på begäran eller genom att schemalägga en rapport så att den med jämna mellanrum skickas till din e-postadress.

Så här genererar du en rapport på begäran:

1. Klicka på rapportikonen på menyraden i ATA-konsolen: ![rapportikon](./media/ata-report-icon.png).
2. Under **Sammanfattning** eller **Modification to sensitive groups** (Ändring av känsliga grupper) anger du datum för **Från** och **Till** och klickar på **Ladda ned**. 
![rapporter](./media/reports.png)

Så här genererar du en schemalagd rapport:
 
1. På sidan **Rapporter** klickar du på **Set scheduled reports** (Skapa schemalagda rapporter). Du kan också klicka på **Schemalagda rapporter** under Notifications and Reports (Meddelanden och rapporter) på konfigurationssidan i ATA-konsolen.

   ![Schemalägga rapporter](./media/ata-sched-reports.png)

2. Klicka på **Schema** bredvid **Sammanfattning** eller **Modification to sensitive groups** (Ändring av känsliga grupper) för att ange e-postadressen som rapporterna ska skickas till och hur ofta du vill få dem. Lägg sedan till dem genom att klicka plustecknet bredvid e-postadressen och klicka slutligen på **Spara**.

   ![Frekvens och e-postadress för schemalagda rapporter](./media/sched-report1.png)


> [!NOTE]
> Schemalagda rapporter levereras via e-post och kan endast skickas om du redan har konfigurerat en e-postserver under **Konfiguration** och sedan väljer **E-postserver** under Notifications and Reports (Meddelanden och rapporter).


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
