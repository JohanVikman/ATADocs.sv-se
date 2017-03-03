---
title: Installera Advanced Threat Analytics steg 5 | Microsoft Docs
description: "Steg fem för att installera ATA hjälper dig att konfigurera inställningar för ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 5856a5e658ed18cbf82d25247f8c39e48ccd2185


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-5"></a>Installera ATA – Steg 5

>[!div class="step-by-step"]
[« Steg 4](install-ata-step4.md)
[Steg 6 »](install-ata-step6.md)


## <a name="step-5-configure-the-ata-gateway-settings"></a>Steg 5. Konfigurera inställningar för ATA Gateway
När ATA Gateway har installerats gör du följande för att konfigurera inställningarna för ATA Gateway.

1.  I ATA-konsolen, gå till **Konfiguration** och under **System**, väljer du **Gateways**.
   
     ![Bild för konfigurering av gateway-inställningar](media/ATA-Gateways-config-1.png)


2.  Välj en Gateway som du vill konfigurera och ange följande information:

    ![Bild för konfigurering av gateway-inställningar](media/ATA-Gateways-config-2.png)

  - **Beskrivning**: Ange en beskrivning av ATA Gateway (valfritt).
  - **Portspeglade domänkontrollanter (FQDN)** (krävs för ATA Gateway, detta kan inte ändras för ATA Lightweight Gateway): Ange fullständig FQDN för domänkontrollanten och klicka på plustecknet för att lägga till den i listan. Till exempel  **dc01.contoso.com**

      Följande information gäller servrar som du anger i listan **Domänkontrollanter**:
      - Alla domänkontrollanter vars trafik övervakas via portspegling av ATA Gateway måste anges i listan **Domänkontrollanter**. Om en domänkontrollant inte visas i listan **Domänkontrollanter** kan det hända att identifiering av misstänkta aktiviteter inte fungerar som förväntat.
      - Minst en domänkontrollant i listan bör vara en global katalog. Det gör det möjligt för ATA att lösa dator- och användarobjekt i andra domäner i skogen.

- **Avbilda nätverkskort** (krävs):
  - Välj de nätverkskort som har konfigurerats som målspeglingskort för en ATA Gateway på en dedikerad server. Dessa tar emot trafiken för den speglade domänkontrollanten.
  - För en ATA Lightweight Gateway bör detta vara alla nätverkskort som används för kommunikation med andra datorer i organisationen.


 - **Kandidat för domänsynkronisering**: Eventuell ATA Gateway som har konfigurerats som kandidat för domänsynkronisering kan ansvara för synkronisering mellan ATA och Active Directory-domänen. Den första synkroniseringen kan ta en stund beroende på storleken på domänen och är resurskrävande. Som standard anges endast ATA-gatewayar som kandidater för domänsynkronisering.
   Vi rekommenderar att du inaktiverar eventuella fjärranslutna ATA-gatewayer från att vara kandidater för domänsynkronisering.
   Om domänkontrollanten är skrivskyddad ska den inte anges som kandidat för domänsynkronisering. Mer information finns i [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features).

> [!NOTE] 
> Det tar några minuter för ATA Gateway-tjänsten att startas första gången efter installation eftersom den bygger upp cache för tolkar för nätverksavbildning.
> Konfigurationsändringarna verkställs på ATA Gateway vid nästa schemalagda synkronisering mellan ATA Gateway och ATA Center.

3. Du kan välja att ange [Syslog listener och Windows Event Forwarding Collection](configure-event-collection.md). 
4. Aktivera **Uppdatera ATA Gateway automatiskt** så att denna ATA Gateway uppdateras automatiskt när du uppdaterar ATA Center med kommande versioner.
3. Klicka på **Spara**.


## <a name="validate-installations"></a>Verifiera installationer
Kontrollera följande om du vill verifiera att ATA-gatewayen har distribuerats:

1.  Kontrollera att tjänsten **Microsoft Advanced Threat Analytics Gateway** körs. Det kan ta några minuter innan tjänsten startar efter att du har sparat inställningarna för ATA Gateway.

2.  Om tjänsten inte startar kontrollerar du filen ”Microsoft.Tri.Gateway-Errors.log” som finns i följande standardmapp, ”%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs” och markerar [ATA-felsökning](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) för hjälp.

3.  Om detta är den första ATA Gateway som installeras bör du efter några minuter logga in på ATA-konsolen och öppna meddelandefönstret genom att svepa på höger sida av skärmen. En lista bör visas med **Senaste inlärda entiteter** i meddelandefältet på höger sida av konsolen.

4.  På skrivbordet klickar du på genvägen för **Microsoft Advanced Threat Analytics** för att ansluta till ATA-konsolen. Logga in med samma autentiseringsuppgifter som du använde för att installera ATA Center.
5.  I konsolen söker du efter något i sökfältet, t.ex. en användare eller grupp på domänen.
6.  Öppna Prestandaövervakaren. I trädet Prestanda klickar du på **Prestandaövervakare** och klickar sedan på plusikonen för att **Lägga till en räknare**. Expandera **Microsoft ATA Gateway** och bläddra ned till **Meddelanden/sek som inhämtats av nätverkslyssnare PEF** och lägg till den. Kontrollera sedan att aktiviteten visas i diagrammet.

    ![Bild av hur du lägger till prestandaräknare](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Steg 4](install-ata-step4.md)
[Steg 6 »](install-ata-step6.md)

## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Feb17_HO1-->


