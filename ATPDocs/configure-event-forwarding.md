---
title: Konfigurera vidarebefordran av Windows-händelser i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver alternativen för att konfigurera vidarebefordran av Windows-händelser med Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 08/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4adae00e0985a831cddf1d9b5276c937e82523d3
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126050"
---
*Gäller för: Azure Avancerat skydd*



# <a name="configuring-windows-event-forwarding"></a>Konfigurera vidarebefordran av Windows-händelser

> [!NOTE]
> Azure ATP-sensorn läser automatiskt händelser lokalt, utan att behöva konfigurera vidarebefordran av händelser.


För att förbättra identifieringsfunktionerna behöver Azure ATP följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045. Dessa kan antingen läsas automatiskt av Azure ATP-sensorn eller om Azure ATP-sensorn inte har distribuerats, vidarebefordras till Azure ATP-sensorn för fristående i ett av två sätt, genom att konfigurera Azure ATP-sensorn för fristående för att lyssna efter SIEM-händelser eller genom att configuri NG vidarebefordran av Windows-händelser.

> [!NOTE]
> Kontrollera att domänkontrollanten är korrekt konfigurerad för att samla in nödvändiga händelser.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>WEF-konfiguration för Azure ATP fristående sensorns med portspegling

När du konfigurerat portspegling från domänkontrollanterna till fristående Azure ATP-sensorn, följer du instruktionerna för att konfigurera vidarebefordran av Windows-händelse med Källinitierad konfiguration. Detta är ett sätt att konfigurera vidarebefordran av Windows-händelse. 

**Steg 1: Lägg till konto för nätverkstjänst i domänens händelselogg för läsargrupp** 

I det här scenariot förutsätter att den fristående Azure ATP-sensorn är medlem i domänen.

1.  Öppna Active Directory-användare och datorer, navigera till den **BuiltIn** mappen och dubbelklickar på **Händelseloggläsare**. 
2.  Välj **medlemmar**.
4.  Om **Nätverkstjänst** inte visas klicka på **Lägg till**, skriv **Nätverkstjänst** i fältet **Ange de objektnamn som ska väljas**. Klicka på **Kontrollera namn** och klicka på **OK**. 

När du lägger till den **nätverkstjänst** till den **Händelseloggläsare** och starta om domänkontrollanterna för att ändringen ska börja gälla.

**Steg 2: Skapa en princip på domänkontrollanterna för att ställa in inställningen Konfigurera målprenumerationshanterare.** 
> [!Note] 
> Du kan skapa en grupprincip för de här inställningarna och använda grupprincipen till varje domänkontrollant som övervakas av fristående Azure ATP-sensorn. Följande steg ändra den lokala principen på domänkontrollanten.     

1.  Kör följande kommando på varje domänkontrollant: *winrm quickconfig*
2.  Från en kommandotolk, ange *gpedit.msc*.
3.  Expandera **Datorkonfiguration > Administrativa mallar > Windows-komponenter > Vidarebefordran av händelse**

 ![Bild av gruppredigerare för lokal princip](media/wef%201%20local%20group%20policy%20editor.png)

4.  Dubbelklicka på **konfigurera målprenumerationshanterare**.
   
    1.  Välj **Aktiverad**.
    2.  Under **alternativ**, klickar du på **visa**.
    3.  Under **SubscriptionManagers**, anger du följande värde och klickar på **OK**: * Server =`http://<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10*` (till exempel: Server =`http://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)
    
    ![Konfigurera målprenumerationsbild](media/wef%202%20config%20target%20sub%20manager.png)
    
5.  Klicka på **OK**.
6.  Från en upphöjd kommandotolk skriver du: *gpupdate/force*. 

**Steg 3: Utför följande steg på den fristående Azure ATP-sensorn** 

1.  Öppna en upphöjd kommandotolk och skriv *wecutil qc*
2.  Öppna **Loggboken**. 
3.  Högerklicka på **prenumerationer** och välj **skapa prenumeration**. 

   1.   Ange namn och beskrivning för prenumerationen. 
   2.   För **Målloggen**, bekräftar du att **vidarebefordrade händelser** har valts. Azure ATP ska läsa händelser måste målloggen vara **vidarebefordrade händelser**. 
   3.   Välj **Källdatorn initierad** och klicka på **Välj datorgrupper**.
        1.  Klicka på **Lägg till domändator**.
        2.  Ange namnet på domänkontrollanten i fältet **Ange ett objektnamn du vill markera**. Klicka sedan på **Kontrollera namn** och klicka på **OK**. 
       
        ![Loggboksbild](media/wef3%20event%20viewer.png)
   
        
        3.  Klicka på **OK**.
   4.   Klicka på **Välj händelser**.

        1. Klicka på **Av logg** och välj **Säkerhet**.
        2. Skriv händelsenumret i fältet **Includes/Excludes Event ID** (Med/utan händelse-ID) och klicka på **OK**. Skriv exempelvis 4776, som i följande exempel:

        ![Frågefilterbild](media/wef-4-query-filter.png)

   5.   Högerklicka på den skapade prenumerationen och välj **Körningsstatus** att se om det finns några problem med statusen. 
   6.   Efter några minuter visas Kontrollera att händelserna har du konfigurerat för vidarebefordran i vidarebefordrade händelser på den fristående Azure ATP-sensorn.


Mer information finns i: [konfigurera datorerna att vidarebefordra och samla in händelser](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Se även

- [Installera Azure ATP](install-atp-step1.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
