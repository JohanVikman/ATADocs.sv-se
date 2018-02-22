---
title: Installera Azure Advanced Threat Protection - steg 5 | Microsoft Docs
description: "Steg fem för att installera Azure ATP hjälper dig att konfigurera inställningar för din Azure ATP fristående sensor."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2e61758e06aedfe607afc0d3365227af872fe20
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-5"></a>Installera Azure ATP - steg 5

>[!div class="step-by-step"]
[« Steg 4](install-atp-step4.md)
[Steg 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Steg 5. Konfigurera inställningar för Azure ATP-temperatursensor
Utför följande steg om du vill konfigurera inställningarna för Azure ATP-sensor när Azure ATP sensorn har installerats.

1.  I arbetsytan ATP Azure-portalen går du till **Configuration** och under **System**väljer **sensor**.
   
     ![Konfigurera sensor inställningar avbildningen](media/atp-sensor-config.png)


2.  Klicka på den sensor som du vill konfigurera och ange följande information:

    ![Konfigurera sensor inställningar avbildningen](media/atp-sensor-config-2.png)

  - **Beskrivning**: Ange en beskrivning för Azure ATP sensorn (valfritt).
  - **Domänkontrollanter (FQDN)** (krävs för Azure ATP fristående sensor detta kan inte ändras för Azure ATP-sensor): Ange det fullständiga FQDN för domänkontrollanten och klicka på plustecknet för att lägga till den i listan. Till exempel  **dc01.contoso.com**

      Följande information gäller servrar som du anger i listan **Domänkontrollanter**:
      - Alla domänkontrollanter vars trafik övervakas via portspegling av Azure ATP fristående sensor måste anges i den **domänkontrollanter** lista. Om en domänkontrollant inte visas i listan **Domänkontrollanter** kan det hända att identifiering av misstänkta aktiviteter inte fungerar som förväntat.
      - Minst en domänkontrollant i listan bör vara en global katalog. Detta gör att Azure ATP att lösa dator- och användarobjekt i andra domäner i skogen.

  - **Avbilda nätverkskort** (krävs):
     - Välj vilka nätverkskort som är konfigurerade som målspegelport för en Azure ATP fristående sensor på en dedikerad server. Dessa ta emot speglad domain controller trafik.
     - För en Azure ATP-sensor vara detta alla nätverkskort som används för kommunikation med andra datorer i din organisation.


  - **Kandidat för domänsynkronisering**: alla Azure ATP fristående sensor är en kandidat för domänsynkronisering kan ansvara för synkronisering mellan Azure ATP och Active Directory-domänen. Beroende på domänens storlek på den första synkroniseringen kan ta lite tid och är resurskrävande. Som standard konfigureras endast Azure ATP fristående sensorer som kandidater för domänsynkronisering.
   Det rekommenderas att du inaktiverar en fjärrplats Azure ATP sensor från att vara kandidater för domänsynkronisering.
   Om domänkontrollanten är skrivskyddad ska den inte anges som kandidat för domänsynkronisering. Mer information finns i [Azure ATP arkitektur](atp-architecture.md#azure-atp-sensor-features).
  
4. Klicka på **Spara**.


## <a name="validate-installations"></a>Verifiera installationer
Om du vill verifiera att Azure ATP sensorn har distribuerats, kontrollerar du följande steg:

1.  Kontrollera att tjänsten **Azure Advanced Threat Protection sensor** körs. När du har sparat inställningarna Azure ATP sensor kan det ta några sekunder för tjänsten att starta.

2.  Om tjänsten inte startar kontrollerar du filen ”Microsoft.Tri.sensor-Errors.log” som finns i följande standardmapp, ”%programfiles%\Azure avancerade Threat Protection sensor\Version X\Logs”.
 
 >[!NOTE]
 > Versionen av Azure ATP uppdateringar ofta att kontrollera den senaste versionen i Azure ATP arbetsplats portal, gå till **Configuration** och sedan **om**. 

3.  Gå till arbetsytan URL: en. I arbetsytan-portalen, söka efter något i sökfältet, t.ex en användare eller en grupp på din domän.



>[!div class="step-by-step"]
[« Steg 4](install-atp-step4.md)
[Steg 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Se även

- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
