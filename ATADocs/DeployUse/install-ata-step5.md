---
title: "Installera ATA – Steg 5 | Microsoft ATA"
description: "Steg fem för att installera ATA hjälper dig att konfigurera inställningar för ATA Gateway."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 168a41182128a1fc91d92a4ef11b873c04ecc6b7


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Installera ATA – Steg 5

>[!div class="step-by-step"]
[« Steg 4](install-ata-step4.md)
[Steg 6 »](install-ata-step6.md)


## Steg 5. Konfigurera inställningar för ATA Gateway
När ATA Gateway har installerats gör du följande för att konfigurera inställningarna för ATA Gateway.

1.  I ATA-konsolen, gå till **Konfiguration** och under **System**, väljer du **Gateways**.
   
     ![Bild för konfigurering av gateway-inställningar](media/ATA-Gateways-config-1.png)


2.  Välj en Gateway som du vill konfigurera och ange följande information:

    ![Bild för konfigurering av gateway-inställningar](media/ATA-Gateways-config-2.png)

  - **Beskrivning**: Ange en beskrivning av ATA Gateway (valfritt).
  - **Portspeglade domänkontrollanter (FQDN)** (krävs för ATA Gateway, detta kan inte ändras för ATA Lightweight Gateway): Ange fullständig FQDN för domänkontrollanten och klicka på plustecknet för att lägga till den i listan. Till exempel  **dc01.contoso.com**

        The following information applies to the servers you enter in the **Domain Controllers** list:
        - All domain controllers whose traffic is being monitored via port mirroring by the ATA Gateway must be listed in the **Domain Controllers** list. If a domain controller is not listed in the **Domain Controllers** list, detection of suspicious activities might not function as expected.
        - At least one domain controller in the list should be a global catalog. This will enable ATA to resolve computer and user objects in other domains in the forest.

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


## Verifiera installationer
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

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Aug16_HO5-->


