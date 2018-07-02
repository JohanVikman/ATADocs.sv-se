---
title: Uppdatera din Azure ATP-sensorer | Microsoft Docs
description: Det beskriver hur du uppdaterar sensorer i Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/24/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b6a9cbb203068e1318425631f9f83c796bb26aa8
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2018
ms.locfileid: "36949030"
---
*Gäller för: Azure Avancerat skydd*


# <a name="update-azure-atp-sensors"></a>Uppdatera Azure ATP-sensorer
Det är viktigt att hålla Azure Advanced Threat Protection uppdaterade för att aktivera bästa möjliga skydd för din organisation.

Azure ATP-tjänsten uppdateras några gånger i månaden med felkorrigeringar, prestandaförbättringar av och nya identifieringar. Ibland kräver dessa uppdateringar en motsvarande uppdatering sensorerna. 

Om du inte uppdaterar din sensorer, kan de inte kan kommunicera med Azure ATP-Molntjänsten, vilket kan resultera i ett degraderat tjänst.

Varje uppdatering har testats och godkänts för alla operativsystem som stöds kan orsaka minimal påverkan på ditt nätverk och åtgärder.

### <a name="azure-atp-sensor-update-types"></a>Uppdateringstyperna för Azure ATP-sensorn   

Azure ATP-sensorer stöder två typer av uppdateringar:
- Lägre versionuppdateringar: 
  - Frekventa 
  - Kräv ingen MSI-installation och inga ändringar i registret
  - Azure ATP-sensorn tjänsten startas om
  - Domänkontrollanter och servern behöver inte startas om

- Stora versionsuppdateringar:
 - Sällsynta
 - Kan kräva en omstart av domänkontrollanter och servrar
 - Innehåller viktiga ändringar 

> [!NOTE]
>- Automatisk omstart av sensorer (i stora uppdateringar) kan styras på konfigurationssida. 
> - Azure ATP-sensorn bevarar alltid minst 15% av minne och CPU som är tillgänglig. Om tjänsten förbrukar för mycket minne som den startas automatiskt av uppdateringstjänsten för Azure ATP-sensorn.

## <a name="delayed-sensor-update"></a>Fördröjd sensor update
Om du vill tillåta en mer gradvis uppdateringsprocess Azure ATP kan du ange en sensor som en **fördröjd update** kandidat. 

Normalt uppdateras sensorer automatiskt när Azure ATP-Molntjänsten har uppdaterats. Sensorer inställd **fördröjd update** uppdateras 24 timmar efter tjänstuppdateringen inledande molnet.

På så sätt kan du välja specifika sensorer där uppdateringen distribueras automatiskt och uppdatera resten av dina sensorer på fördröjning, endast efter att du ser att den första uppdateringen gick smidigt.

> [!NOTE]
> Om ett fel och en sensor uppdateras inte kan öppna ett supportärende.

För att ange en sensor för fördröjd uppdatering:

1. Från Azure ATP-arbetsyteportalen, klicka på ikonen för inställningar och välj **Configuration**.
2. Klicka på den **uppdateringar** fliken.
3. I tabellrad bredvid varje sensor som du vill fördröja, ställer du in den **fördröjd update** skjutreglaget till **på**.
4. Klicka på **Spara**.
 
## <a name="sensor-update-process"></a>Sensorns uppdateringsprocess

Några minuters mellanrum, kontrollera Azure ATP-sensorer om de har den senaste versionen. När Molntjänsten Azure ATP uppdateras till en nyare version, startar tjänsten Azure ATP-sensorn uppdateringsprocessen:

1. Azure ATP cloud service uppdateringarna till den senaste versionen.
2. Uppdateringstjänsten för Azure ATP-sensorn lär sig att det finns en uppdaterad version.
3. Sensorer som är inställda på att **fördröjd update** uppdatering:
  1. Uppdateringstjänsten för Azure ATP-sensorn hämtar den uppdaterade versionen från Molntjänsten (i formatet cab-fil).
  2. Azure ATP-sensorn updater verifierar filens signatur.
  3. Uppdateringstjänsten för Azure ATP-sensorn extrahera cab-filen till en ny mapp i installationsmappen för den sensorn. Som standard kommer den att extraheras till *c:\Program\Microsoft Files\Azure Advanced Threat Protection Sensor\<versionsnummer >*
  4. Uppdateringstjänsten för Azure ATP-sensorn startar om tjänsten Azure ATP-sensorn.
  5. Tjänsten Azure ATP-sensorn pekar på de nya filerna som extraheras från cab-filen.
  > [!NOTE]
  >En mindre uppdatering av sensorerna inte installera en MSI eller ändra alla registervärden eller systemfiler. Även en väntande omstart påverkar inte uppdatering av sensorerna. 
  6. Sensorerna körs baserat på den nyligen uppdaterade versionen.
  7. En sensor tar emot clearance från Azure-molntjänst. Detta kan verifieras i den **uppdateringar** sidan.
  8. Nästa sensorn börjar uppdateringsprocessen. 

4. 24 timmar efter Azure ATP-molntjänst uppdateras, sensorer som valts för ** fördröjd uppdateringen börjar uppdateringsprocessen.

![sensorn update](./media/sensor-update.png)


I händelse av fel, om sensorn inte kunde slutföra uppdateringsprocessen, en relevanta övervakningsavisering utlöses och skickas som ett meddelande.

![sensorn är inaktuell](./media/sensor-outdated.png)


## <a name="see-also"></a>Se även

- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)