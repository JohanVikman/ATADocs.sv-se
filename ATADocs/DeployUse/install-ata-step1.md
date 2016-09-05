---
title: "Installera ATA – Steg 1 | Microsoft ATA"
description: "Första steget för att installera ATA omfattar att hämta och installera ATA Center på den valda servern."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d89f6c5e0ac9712ce2fde057c9ef8e4025e8a144
ms.openlocfilehash: 41d538039a8fa0511a74dd6cd5d840a1dea516e8


---

# Installera ATA – Steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-ata-step2.md)

Den här installationsproceduren innehåller anvisningar för att utföra en helt ny installation av ATA 1.6. Information om hur du uppdaterar en befintlig ATA-distribution från en tidigare version finns i [ATA-migreringsguide för version 1.6](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide).

> [!IMPORTANT] 
> Installera KB2934520 på ATA Center-servern och på ATA-gatewayservrarna innan du påbörjar installationen, annars kommer ATA-installationen att installera denna uppdatering och kräva en omstart mitt i ATA-installationen.

## Steg 1. Hämta och installera ATA Center
När du har kontrollerat att servern uppfyller kraven kan du fortsätta med installationen av ATA Center.

På ATA Center-servern utför du följande steg.

1.  Hämta ATA från [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) eller [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Logga in på datorn där du installerar ATA Center som en användare som är medlem i den lokala administratörsgruppen.

3.  Kör **Microsoft ATA Center Setup.EXE** och följ installationsguiden.

4.  Om Microsoft .Net Framework inte är installerat uppmanas du att installera det när du startar installationen. Du kan uppmanas att starta om efter installationen av .NET Framework.
5.  På sidan **Välkommen** väljer du det språk som ska användas för ATA-installationsskärmarna och klickar på **Nästa**.

6.  Läs igenom Licensvillkor för programvara från Microsoft och om du godkänner villkoren markerar du kryssrutan och klickar sedan på **Nästa**.

7.  Vi rekommenderar att du konfigurerar ATA för att uppdateras automatiskt. Om Windows inte är inställt på att göra detta på datorn visas skärmen **Använd Microsoft Update så hjälper du till att hålla datorn säker och uppdaterad**. 
    ![Bild för håll ATA uppdaterat](media/ata_ms_update.png)

8. Markera **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**. Detta justerar Windows-inställningarna för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), på det sätt som visas här. 
    ![Bild för automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

8.  På sidan **ATA Center-konfiguration** anger du följande information baserat på miljön:

    |Fält|Beskrivning|Kommentar|
    |---------|---------------|------------|
    |Installationssökväg|Det här är den plats där ATA Center kommer att installeras. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center|Låt standardvärdet vara kvar|
    |Datasökväg för databasen|Det här är den plats där MongoDB-databasfilerna kommer att finnas. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Ändra platsen till en plats där det finns utrymme att växa, baserat på storleken. **Obs!** <ul><li>I produktionsmiljöer bör du använda en enhet som har tillräckligt med utrymme baserat på kapacitetsplaneringen.</li><li>Vid stora distributioner bör databasen finnas på en separat fysisk enhet.</li></ul>Storleksinformation finns i [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |IP-adress för ATA Center-tjänsten: Port|Det här är den IP-adress som ATA Center-tjänsten kommer att lyssna på för kommunikation från ATA-gatewayerna.<br /><br />**Standardport:** 443|Klicka på nedåtpilen för att välja den IP-adress som ska användas av ATA Center-tjänsten.<br /><br />IP-adressen och porten för ATA Center-tjänsten får inte vara samma som IP-adressen och porten för ATA-konsolen. Tänk på att ändra porten för ATA-konsolen.|
    |SSL-certifikat för ATA Center-tjänsten|Det här är det certifikat som kommer att användas av ATA Center-tjänsten.|Klicka på nyckelikonen om du vill välja ett installerat certifikat eller kontrollera ett självsignerat certifikat vid distribution i en labbmiljö.|
    |ATA-konsolens IP-adress|Det här är den IP-adress som ska användas av IIS för ATA-konsolen.|Klicka på nedåtpilen för att välja den IP-adress som används av ATA-konsolen. **Obs!** Anteckna denna IP-adress för att göra det enklare att komma åt ATA-konsolen från ATA Gateway.|
    |SSL-certifikat för ATA-konsolen|Det här är certifikatet som ska användas av IIS.|Klicka på nyckelikonen om du vill välja ett installerat certifikat eller kontrollera ett självsignerat certifikat vid distribution i en labbmiljö.|

    ![Bild för konfiguration av ATA center](media/ATA-Center-Configuration.JPG)

10.  Klicka på **Installera** för att installera ATA Center och dess komponenter.
    Följande komponenter installeras och konfigureras under installationen av ATA Center:

    -   IIS (Internet Information Services)

    -   ATA Center-tjänsten och ATA-konsolens IIS-plats

    -   MongoDB

    -   Anpassad datasamlingsuppsättning för Prestandaövervakaren

    -   Självsignerade certifikat (om detta valdes under installationen)

11.  När installationen är klar klickar du på **Starta** för att ansluta till ATA-konsolen.
Du kommer nu automatiskt till inställningssidan **Allmänt** där du fortsätter med konfigurationen och distributionen av ATA-gatewayer.
Eftersom du loggar in på platsen med en IP-adress får du en varning relaterad till certifikatet, detta är normalt och du ska klicka på **Fortsätt till denna webbplats**.

### Verifiera installationen

1.  Kontrollera att tjänsten **Microsoft Advanced Threat Analytics Center** körs.
2.  På skrivbordet klickar du på genvägen för **Microsoft Advanced Threat Analytics** för att ansluta till ATA-konsolen. Logga in med samma autentiseringsuppgifter som du använde för att installera ATA Center.



>[!div class="step-by-step"]
[«Förinstallation](preinstall-ata.md)
[steg 2»](install-ata-step2.md)

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Aug16_HO3-->


