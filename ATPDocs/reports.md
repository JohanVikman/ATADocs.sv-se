---
title: Arbeta med Azure ATP rapporter | Microsoft Docs
description: "Beskriver hur du kan generera rapporter i Azure ATP att övervaka nätverket."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2ebc0d9bb860bd93f14c4c511b034c740b59dffb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="azure-atp-reports"></a>Azure ATP rapporter

Avsnittet Azure ATP rapporter på arbetsytan portalen kan du generera rapporter som ger dig information om systemstatus, både systemhälsa och en rapport med misstänkta aktiviteter som identifierats i din miljö.

Du kommer åt rapportsidan genom att klicka på rapportikonen på menyraden: ![rapportikon](./media/atp-report-icon.png).
Följande rapporter är tillgängliga: 

- **Översiktsrapport**: I sammanfattningsrapporten presenterar en instrumentpanel status i systemet. Du kan visa tre flikar - en för en **sammanfattning** av vad som har identifierats i nätverket, **öppna misstänkta aktiviteter** som visar misstänkta aktiviteter som du bör ta hand om, och **öppna hälsa problem** att listor Azure ATP hälsa problem som du bör ta hand om. Både misstänkta aktiviteter och hälsorelaterade problem är uppdelade efter typ. 

- **Ändring av känsliga grupper**: den här rapporten visar varje gång en ändring görs till känsliga grupper (till exempel Administratörer, eller manuellt taggade konton eller grupper). Om du använder Azure ATP fristående sensorer, få en fullständig rapport om känsliga grupper det är nödvändigt att se till att [händelser som vidarebefordras från domänkontrollanterna till fristående sensorer](configure-event-forwarding.md). 

- **Lösenord i klartext**: vissa tjänster använder LDAP-protokollet inte är säkra för att skicka autentiseringsuppgifter i klartext. Detta kan även bero på känsliga konton. Övervaka nätverkstrafik angripare kan fånga och sedan återanvända dessa autentiseringsuppgifter för skadliga syften. Den här rapporten visar en lista över alla käll- och lösenord som Azure ATP identifieras som skickas i klartext. 

- **Lateral förflyttning sökvägar till känsliga konton**: den här rapporten visar de känsliga konton som är tillgängliga via lateral förflyttning sökvägar. Mer information finns i [Lateral förflyttning sökvägar](use-case-lateral-movement-path.md). Den här rapporten samlar in sökvägar som skapades under de senaste 60 dagarna, och den information som visas i arbetsytan-portalen som representerar två dagar.

Du kan generera en rapport på två sätt: antingen på begäran eller genom att schemalägga en rapport så att den med jämna mellanrum skickas till din e-postadress.

Så här genererar du en rapport på begäran:

1. Klicka på ikonen rapporten i menyraden i Azure ATP arbetsytan portal menyraden: ![rapportikon](./media/atp-report-icon.png).

2. Under den valda rapporttyp, ange den **från** och **till** datum och klicka på **hämta**. 
 ![rapporter](./media/reports.png)

Så här genererar du en schemalagd rapport:
 
1. I den **rapporter** klickar du på **ange schemalagda rapporter**, eller i Azure ATP arbetsytan Portalkonfiguration sidan under meddelanden och rapporter, klickar du på **schemalagda rapporter**.

   ![Schemalägga rapporter](./media/atp-sched-reports.png)

2. Klicka på **schema** bredvid ditt valda rapporttyp Ange frekvens och e-postadress för leverans av rapporterna Klicka på plustecknet för att lägga till dem och klicka på e-postadresser **spara**.

   ![Frekvens och e-postadress för schemalagda rapporter](./media/sched-report1.png)


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)