---
title: Konfigurera vidarebefordran av Windows-händelser i Azure Advanced Threat Protection | Microsoft Docs
description: Beskriver alternativen för att konfigurera vidarebefordran av Windows-händelse med Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: df06235de3a29051f9ffcd889bb95936ed9fc27d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446094"
---
*Gäller för: Azure Advanced Threat Protection version 1.9.*



# <a name="configuring-windows-event-forwarding"></a>Konfigurera vidarebefordran av Windows-händelser

> [!NOTE]
> Azure ATP-sensor läser automatiskt händelser lokalt, utan att behöva konfigurera vidarebefordran av händelser.


För att förbättra identifieringsfunktionerna Azure ATP måste följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045. Dessa kan antingen läsas automatiskt av Azure ATP-sensor eller om Azure ATP-sensor inte har distribuerats, den kan vidarebefordras till Azure ATP fristående sensor i ett av två sätt, genom att konfigurera fristående Azure ATP sensorn så att den lyssnar efter SIEM-händelser eller genom att configuri NG vidarebefordran av Windows-händelser.

> [!NOTE]
> Kontrollera att domänkontrollanten är korrekt konfigurerad för att samla in händelser som krävs.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>WEF konfigurationen för Azure ATP fristående sensor's med portspegling

När du har konfigurerat portspegling från domänkontrollanterna till Azure ATP fristående sensor följer du följande instruktioner för att konfigurera vidarebefordran av Windows-händelse med källan initierade konfiguration. Detta är ett sätt att konfigurera vidarebefordran av Windows-händelse. 

**Steg 1: Lägg till konto för nätverkstjänst i domänens händelselogg för läsargrupp** 

I det här scenariot förutsätter att Azure ATP fristående sensor är medlem i domänen.

1.  Öppna Active Directory-användare och datorer, navigera till den **BuiltIn** mappen och dubbelklickar på **Händelseloggläsare**. 
2.  Välj **medlemmar**.
4.  Om **Nätverkstjänst** inte visas klicka på **Lägg till**, skriv **Nätverkstjänst** i fältet **Ange de objektnamn som ska väljas**. Klicka på **Kontrollera namn** och klicka på **OK**. 

När du lägger till den **nätverkstjänsten** till den **Händelseloggläsare** och starta om domänkontrollanterna för att ändringarna ska börja gälla.

**Steg 2: Skapa en princip på domänkontrollanterna för att ställa in inställningen Konfigurera målprenumerationshanterare.** 
> [!Note] 
> Du kan skapa en grupprincip för dessa inställningar och tillämpa grupprincipen på alla domänkontrollanter som övervakas av Azure ATP fristående sensorn. Följande steg ändra den lokala principen på domänkontrollanten.     

1.  Kör följande kommando på varje domänkontrollant: *winrm quickconfig*
2.  Från en kommandotolk, ange *gpedit.msc*.
3.  Expandera **Datorkonfiguration > Administrativa mallar > Windows-komponenter > Vidarebefordran av händelse**

 ![Bild av gruppredigerare för lokal princip](media/wef 1 local group policy editor.png)

4.  Dubbelklicka på **konfigurera mål prenumeration Manager**.
   
    1.  Välj **Aktiverad**.
    2.  Under **alternativ**, klickar du på **visa**.
    3.  Under **SubscriptionManagers**, anger följande värde och klickar på **OK**: *Server = http: / /<fqdnATPSensor>: 5985/wsman/SubscriptionManager/WEC, uppdatera = 10* () Till exempel: Server = http://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC, uppdatera = 10)
 
   ![Konfigurera målprenumerationsbild](media/wef 2 config target sub manager.png)
   
    5.  Klicka på **OK**.
    6.  Från en upphöjd kommandotolk skriver du: *gpupdate/force*. 

**Steg 3: Utför följande steg på Azure ATP fristående sensor** 

1.  Öppna en upphöjd kommandotolk och skriv *wecutil qc*
2.  Öppna **Loggboken**. 
3.  Högerklicka på **prenumerationer** och välj **skapa prenumeration**. 

   1.   Ange namn och beskrivning för prenumerationen. 
   2.   För **mål loggen**, bekräftar du att **vidarebefordrade händelser** är markerad. För Azure ATP att läsa händelser, mål-loggen måste vara **vidarebefordrade händelser**. 
   3.   Välj **Källdatorn initierad** och klicka på **Välj datorgrupper**.
        1.  Klicka på **Lägg till domändator**.
        2.  Ange namnet på domänkontrollanten i fältet **Ange ett objektnamn du vill markera**. Klicka sedan på **Kontrollera namn** och klicka på **OK**. 
       
        ![Loggboksbild](media/wef3 event viewer.png)
   
        
        3.  Klicka på **OK**.
   4.   Klicka på **Välj händelser**.

        1. Klicka på **Av logg** och välj **Säkerhet**.
        2. Skriv händelsenumret i fältet **Includes/Excludes Event ID** (Med/utan händelse-ID) och klicka på **OK**. Skriv till exempel 4776, som i följande exempel:

 ![Frågefilterbild](media/wef-4-query-filter.png)

   5.   Högerklicka på den skapade prenumerationen och välj **Körningsstatus** att se om det uppstår några problem med status. 
   6.   Efter några minuter, se till att händelserna som du anger som ska vidarebefordras visas i händelser som vidarebefordras på Azure ATP fristående sensor.


Mer information finns: [konfigurera datorerna att vidarebefordra och samla händelser](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Se även

- [Installera Azure ATP](install-atp-step1.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)