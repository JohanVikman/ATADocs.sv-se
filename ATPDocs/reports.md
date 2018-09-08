---
title: Arbeta med Azure ATP-rapporter | Microsoft Docs
description: Beskriver hur du kan generera rapporter i Azure ATP att övervaka ditt nätverk.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: eb1a29038d8afb47328970ff7179f0e1ff01614d
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165940"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-reports"></a>Azure ATP-rapporter

Azure ATP-rapportavsnittet i arbetsytans portal kan du generera rapporter som ger dig information om systemstatus, både systemhälsa och en rapport över misstänkta aktiviteter har identifierats i din miljö.


Du kommer åt rapportsidan genom att klicka på rapportikonen på menyraden: ![rapportikon](./media/atp-report-icon.png).
Följande rapporter är tillgängliga: 

- **Sammanfattningsrapport**: sammanfattningsrapporten innehåller en instrumentpanel över systemets status i systemet. Du kan se tre flikar: en för en **sammanfattning** av vad som har identifierats i nätverket, **öppna misstänkta aktiviteter** som visar en lista över misstänkta aktiviteter som du bör ta hand om, och **öppna hälsotillstånd problem med** listor Azure ATP hälsoproblem du bör ta hand om. Både misstänkta aktiviteter och hälsorelaterade problem är uppdelade efter typ. 

- **Ändring av känsliga grupper**: den här rapporten visar varje gång en ändring görs känsliga grupper (till exempel Administratörer, eller manuellt märkt konton eller grupper). Om du använder Azure ATP fristående sensorer, för att få en fullständig rapport om dina känsliga grupper, är det nödvändigt att se till att [händelser vidarebefordras från domänkontrollanterna till fristående sensorer](configure-event-forwarding.md). 

- **Lösenord som exponerats i klartext**: vissa tjänster använder icke-säker LDAP-protokollet för att skicka autentiseringsuppgifter i klartext. Detta kan även inträffa för känsliga konton. Angripare som övervakar nätverkstrafiken kan fånga upp och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. Den här rapporten listar alla käll- och lösenord som Azure ATP har identifierats som skickas i klartext. 

- **Laterala rörelsebanor till känsliga konton**: den här rapporten Listar de känsliga konton som exponeras via lateral förflyttning. Mer information finns i [Lateral förflyttning](use-case-lateral-movement-path.md). Den här rapporten samlar in sökvägar som har skapats under de senaste 60 dagarna, till skillnad från informationen som visas i arbetsytan-portalen, som representerar två dagar.

Du kan generera en rapport på två sätt: antingen på begäran eller genom att schemalägga en rapport så att den med jämna mellanrum skickas till din e-postadress.

Så här genererar du en rapport på begäran:

1. Klicka på rapportikonen på menyraden i fältet Azure ATP-arbetsyta – meny på portalen: ![rapportikon](./media/atp-report-icon.png).

2. Under den valda rapporten-typ, ange den **från** och **till** datum och klicka på **hämta**. 
 ![rapporter](./media/reports.png)

Så här genererar du en schemalagd rapport:
 
1. I den **rapporter** klickar du på **Ställ in schemalagda rapporter**, eller i Azure ATP arbetsytan Portalkonfiguration sidan under meddelanden och rapporter, klickar du på **schemalagda rapporter**.

   ![Schemalägga rapporter](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Rapporter för daglig är utformade för att skickas strax efter midnatt UTC-tid.

2. Klicka på **schema** bredvid din valda rapporttyp att frekvens och e-postadress för leverans av rapporter och klicka på plustecknet bredvid e-postadressen att lägga till dem och klicka på **spara**.

   ![Frekvens och e-postadress för schemalagda rapporter](./media/sched-report1.png)


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)