---
title: "Installera ATA – Steg 5 | Microsoft Advanced Threat Analytics"
description: "Steg fem för att installera ATA hjälper dig att konfigurera inställningar för ATA Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 6400a0eabefac91b418e00eb670b1329fa1b5fb5


---

# Installera ATA – Steg 5

>[!div class="step-by-step"]
[« Steg 4](install-ata-step4.md)
[Steg 6 »](install-ata-step6.md)


## Steg 5. Konfigurera inställningar för ATA Gateway
När ATA Gateway har installerats gör du följande för att konfigurera inställningarna för ATA Gateway.

1.  På ATA-konsolen klickar du på **Konfiguration** och väljer sidan **ATA Gateways**.

2.  Ange följande information.

  - **Beskrivning**: <br>Ange en beskrivning av ATA Gateway (valfritt).
  - **Portspeglade domänkontrollanter (FQDN)** (krävs för ATA Gateway, detta kan inte konfigureras för ATA Lightweight Gateway): <br>Ange fullständig FQDN för domänkontrollanten och klicka på plustecknet för att lägga till den i listan. Till exempel  **dc01.contoso.com**<br /><br />![Bild med exempel på FDQN](media/ATAGWDomainController.png)

Följande information gäller för alla servrar du anger i listan **Domänkontrollanter**: Alla domänkontrollanter vars trafik övervakas via portspegling av ATA Gateway måste anges i listan **Domänkontrollanter**. Om en domänkontrollant inte visas i listan **Domänkontrollanter** kan det hända att identifiering av misstänkta aktiviteter inte fungerar som förväntat.
- Minst en domänkontrollant i listan måste vara en global katalogserver. Det gör det möjligt för ATA att lösa dator- och användarobjekt i andra domäner i skogen.

 - **Avbilda nätverkskort** (krävs):<br>
     - Välj de nätverkskort som har konfigurerats som målspeglingskort för en ATA Gateway på en dedikerad server. Dessa tar emot trafiken för den speglade domänkontrollanten.
     - För en ATA Lightweight Gateway bör detta vara alla nätverkskort som används för kommunikation med andra datorer i organisationen.

![Bild för konfigurering av gateway-inställningar](media/ATA-Config-GW-Settings.jpg)

 - **Kandidat för domänsynkronisering**<br>
Eventuell ATA Gateway som har konfigurerats som kandidat för domänsynkronisering kan ansvara för synkronisering mellan ATA och Active Directory-domänen. Beroende på domänens storlek kan den första synkroniseringen ta lite tid och vara resurskrävande. Som standard konfigureras endast ATA-gatewayer som kandidater för domänsynkronisering. <br>Vi rekommenderar att du inaktiverar eventuella fjärranslutna ATA-gatewayer från att vara kandidater för domänsynkronisering.<br>Om domänkontrollanten är skrivskyddad ska den inte anges som kandidat för domänsynkronisering. Mer information finns i [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features).

> [!NOTE] 
> Det tar några minuter för ATA Gateway-tjänsten att startas första gången eftersom den bygger upp cache för tolkar för nätverksavbildning.<br>
> Konfigurationsändringarna verkställs på ATA Gateway vid nästa schemalagda synkronisering mellan ATA Gateway och ATA Center.



    

3. Du kan välja att ange [Syslog listener och Windows Event Forwarding Collection](configure-event-collection.md). 
4. Aktivera **Uppdatera ATA Gateway automatiskt** så att denna ATA Gateway uppdateras automatiskt när du uppdaterar ATA Center med kommande versioner.
3.  Klicka på **Spara**.


## Verifiera installationer
Kontrollera följande om du vill verifiera att ATA-gatewayen har distribuerats:

1.  Kontrollera att tjänsten **Microsoft Advanced Threat Analytics Gateway** körs. Det kan ta några minuter innan tjänsten startar efter att du har sparat inställningarna för ATA Gateway.

2.  Om tjänsten inte startar kontrollerar du filen ”Microsoft.Tri.Gateway-Errors.log” som finns i följande standardmapp, ”%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs”.

3.  Kontrollera [Felsökning av ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) för att få hjälp.

4.  Om detta är den första ATA Gateway som installeras bör du efter några minuter logga in på ATA-konsolen och öppna meddelandefönstret genom att svepa på höger sida av skärmen. En lista bör visas med **Senaste inlärda entiteter** i meddelandefältet på höger sida av konsolen.

5.  På skrivbordet klickar du på genvägen för **Microsoft Advanced Threat Analytics** för att ansluta till ATA-konsolen. Logga in med samma autentiseringsuppgifter som du använde för att installera ATA Center.
6.  I konsolen söker du efter något i sökfältet, t.ex. en användare eller grupp på domänen.
7.  Öppna Prestandaövervakaren. I trädet Prestanda klickar du på **Prestandaövervakare** och klickar sedan på plusikonen för att **Lägga till en räknare**. Expandera **Microsoft ATA Gateway** och bläddra ned till **Meddelanden/sek som inhämtats av nätverkslyssnare PEF** och lägg till den. Kontrollera sedan att aktiviteten visas i diagrammet.

    ![Bild av hur du lägger till prestandaräknare](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Steg 4](install-ata-step4.md)
[Steg 6 »](install-ata-step6.md)

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


