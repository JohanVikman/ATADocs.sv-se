---
title: "Konfigurera vidarebefordran av Windows-händelser i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver alternativen för att konfigurera vidarebefordran av Windows-händelse med ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6469f602d2da833e96bba72003aad3fe2b67eb48
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="configuring-windows-event-forwarding"></a>Konfigurera vidarebefordran av Windows-händelser

För att kunna förbättra identifieringsfunktionerna behöver ATA följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Dessa kan antingen läsas automatiskt av ATA Lightweight Gateway eller, om ATA Lightweight Gateway inte har distribuerats, vidarebefordras till ATA-gatewayen på något av två sätt, genom att ATA Gateway konfigureras att lyssna efter SIEM-händelser eller genom att [vidarebefordran av Windows-händelser konfigureras](#configuring-windows-event-forwarding).

> [!NOTE]
> För ATA versions 1.8 och senare behövs inte längre konfiguration av händelseinsamling för ATA Lightweight-gatewayer. ATA Lightweight Gateway kan nu läsa händelser lokalt, utan att du behöver konfigurera vidarebefordran av händelser.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>WEF-konfiguration för ATA-gatewayar med portspegling

När du konfigurerat portspegling från domänkontrollanter till ATA Gateway, följ anvisningarna nedan för att konfigurera vidarebefordran av Windows-händelse med källinitierad konfiguration. Detta är ett sätt att konfigurera vidarebefordran av Windows-händelse. 

**Steg 1: Lägg till konto för nätverkstjänst i domänens händelselogg för läsargrupp** 

I det här scenariot antar vi att ATA-gatewayen är medlem i domänen.

1.  Öppna Active Directory-användare och -datorer, navigera till mappen **BuiltIn** och dubbelklicka på **händelseloggläsare**. 
2.  Välj **medlemmar**.
4.  Om **Nätverkstjänst** inte visas klicka på **Lägg till**, skriv **Nätverkstjänst** i fältet **Ange de objektnamn som ska väljas**. Klicka på **Kontrollera namn** och klicka på **OK**. 

Observera att du efter att ha lagt till **nätverkstjänsten** i gruppen **Händelseloggläsare** måste starta om domänkontrollanterna för att ändringen ska börja gälla.

**Steg 2: Skapa en princip på domänkontrollanterna för att ställa in inställningen Konfigurera målprenumerationshanterare.** 
> [!Note] 
> Du kan skapa en grupprincip för de här inställningarna och använda grupprincipen till varje domänkontrollant som övervakas av ATA Gateway. Stegen nedan ändrar den lokala principen på domänkontrollanten.     

1.  Kör följande kommando på varje domänkontrollant: *winrm quickconfig*
2.  Från en kommandotolk, ange *gpedit.msc*.
3.  Expandera **Datorkonfiguration > Administrativa mallar > Windows-komponenter > Vidarebefordran av händelse**

 ![Bild av gruppredigerare för lokal princip](media/wef 1 local group policy editor.png)

4.  Dubbelklicka på **Konfigurera målprenumerationshanterare**.
   
    1.  Välj **Aktiverad**.
    2.  Under **Alternativ** klickar du på **Visa**.
    3.  Under **SubscriptionManagers** anger du följande värde och klickar på **OK**:  *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (Exempel: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Konfigurera målprenumerationsbild](media/wef 2 config target sub manager.png)
   
    5.  Klicka på **OK**.
    6.  Från en upphöjd kommandotolk skriver du: *gpupdate/force*. 

**Steg 3: Utför följande steg på ATA-Gateway** 

1.  Öppna en upphöjd kommandotolk och skriv *wecutil qc*
2.  Öppna **Loggboken**. 
3.  Högerklicka på **Prenumerationer** och välj **Skapa prenumeration**. 

   1.   Ange namn och beskrivning för prenumerationen. 
   2.   För **Målloggen**, bekräfta att **Vidarebefordrade händelser** har valts. För att ATA ska läsa händelser måste målloggen vara **Vidarebefordrade händelser**. 
   3.   Välj **Källdatorn initierad** och klicka på **Välj datorgrupper**.
        1.  Klicka på **Lägg till domändator**.
        2.  Ange namnet på domänkontrollanten i fältet **Ange ett objektnamn du vill markera**. Klicka sedan på **Kontrollera namn** och klicka på **OK**. 
       
        ![Loggboksbild](media/wef3 event viewer.png)
   
        
        3.  Klicka på **OK**.
   4.   Klicka på **Välj händelser**.

        1. Klicka på **Av logg** och välj **Säkerhet**.
        2. Skriv händelsenumret i fältet **Includes/Excludes Event ID** (Med/utan händelse-ID) och klicka på **OK**. 

 ![Frågefilterbild](media/wef 4 query filter.png)

   5.   Högerklicka på den skapade prenumerationen och välj **Körningsstatus** för att se om det finns problem med statusen. 
   6.   Efter några minuter kontrollerar du att de händelser som du har konfigurerat för vidarebefordran visas i Vidarebefordrade händelser på ATA-gatewayen.


Mer information finns i: [Konfigurera datorerna att vidarebefordra och samla in händelser](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Se även
- [Installera ATA](install-ata-step1.md)
- [Ta en titt i ATA-forumet!!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)