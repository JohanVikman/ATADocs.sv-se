---
title: Installera Azure Advanced Threat Protection – steg 5 | Microsoft Docs
description: Steg fem för att installera Azure ATP kan du konfigurera inställningar för din fristående Azure ATP-sensorn.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 15e3639aa08e48a40ae65bf229964ae589ce1ba8
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454079"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-5"></a>Installera Azure ATP - steg 5

> [!div class="step-by-step"]
> [« Steg 4](install-atp-step4.md)
> [Steg 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Steg 5. Konfigurera inställningar för Azure ATP-sensorn
När du har installerat Azure ATP-sensorn utför du följande steg för att konfigurera inställningar för Azure ATP-sensorn.

1.  I Azure ATP-arbetsyteportalen, går du till **Configuration** och under **System**väljer **sensor**.
   
     ![Konfigurera bild för inställning av sensor](media/atp-sensor-config.png)


2.  Klicka på sensorn som du vill konfigurera och ange följande information:

    ![Konfigurera bild för inställning av sensor](media/atp-sensor-config-2.png)

  - **Beskrivning av**: Ange en beskrivning för Azure ATP-sensorn (valfritt).
  - **Domänkontrollanter (FQDN)** (krävs för fristående Azure ATP-sensorn, detta kan inte ändras för Azure ATP-sensorn): Ange fullständig FQDN för domänkontrollanten och klicka på plustecknet för att lägga till den i listan. Till exempel  **dc01.contoso.com**

      Följande information gäller servrar som du anger i listan **Domänkontrollanter**:
      - Alla domänkontrollanter vars trafik övervakas via portspegling av fristående Azure ATP-sensorn måste anges i den **domänkontrollanter** lista. Om en domänkontrollant inte visas i listan **Domänkontrollanter** kan det hända att identifiering av misstänkta aktiviteter inte fungerar som förväntat.
      - Minst en domänkontrollant i listan bör vara en global katalog. Detta gör Azure ATP att lösa dator- och användarobjekt i andra domäner i skogen.

  - **Avbilda nätverkskort** (krävs):
   
     - Det bör vara alla nätverkskort som används för kommunikation med andra datorer i din organisation för en Azure ATP-sensorn.
    - Välj de nätverkskort som är konfigurerade som målspegelport för en Azure ATP fristående sensorn på en dedikerad server. Dessa ta emot speglad domain controller-trafik.

    - **Kandidat för domänsynkronisering**: som standard Azure ATP-sensorer som är inte kandidater för domänsynkronisering, medan Azure ATP fristående sensorer är. För att manuellt välja ett Azure ATP-sensorn som en domän syncronizer kandidat, växla den **kandidat för domänsynkronisering** växla möjlighet att **på** på skärm för konfiguration. 
    
        Domänsynkroniseraren ansvarar för synkronisering mellan Azure ATP- och Active Directory-domänen. Beroende på domänens storlek på den första synkroniseringen kan ta lite tid och är resurskrävande. 
   Vi rekommenderar att du inaktiverar eventuella fjärranslutna Azure ATP givare från att domänen kandidater för domänsynkronisering.
   Om domänkontrollanten är skrivskyddad ska den inte anges som kandidat för domänsynkronisering. Läs mer om Azure ATP-domänsynkronisering [Azure ATP-arkitektur](atp-architecture.md#azure-atp-sensor-features)
  
4. Klicka på **Spara**.


## <a name="validate-installations"></a>Verifiera installationer
För att verifiera att Azure ATP-sensorn har distribuerats kan du kontrollera följande:

1.  Kontrollera att tjänsten **Azure Advanced Threat Protection sensor** körs. När du har sparat inställningarna för Azure ATP-sensorn, kan det ta några sekunder för tjänsten att starta.

2.  Om tjänsten inte startar, kontrollerar du filen ”Microsoft.Tri.sensor-Errors.log” som finns i följande standardmapp, ”%programfiles%\Azure Avancerat skydd sensor\Version X\Logs”.
 
 >[!NOTE]
 > Versionen av Azure ATP-uppdateringar ofta att kontrollera den senaste versionen på arbetsplatsen Azure ATP-portalen går du till **Configuration** och sedan **om**. 

3.  Gå till din arbetsyta-URL. Sök efter något i sökfältet, t.ex en användare eller grupp på din domän i arbetsytans portal.



> [!div class="step-by-step"]
> [« Steg 4](install-atp-step4.md)
> [Steg 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
