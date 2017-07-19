---
title: Installera Advanced Threat Analytics steg 1 | Microsoft Docs
description: "Första steget för att installera ATA omfattar att hämta och installera ATA Center på den valda servern."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 97fa1522ca43cf92416ac845b8886f2905e9981b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# <a name="install-ata---step-1"></a>Installera ATA – Steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-ata-step2.md)

Den här installationsproceduren innehåller anvisningar som beskriver hur du utför en helt ny installation av ATA 1.8. Information om hur du uppdaterar en befintlig ATA-distribution från en tidigare version finns i [ATA-migreringsguide för version 1.8](ata-update-1.8-migration-guide.md).

> [!IMPORTANT] 
> Om du använder Windows 2012 R2 kan du installera KB2934520 på ATA Center-servern och på ATA-gatewayservrarna innan du påbörjar installationen, annars kommer ATA-installationen att installera denna uppdatering och kräva en omstart mitt i ATA-installationen.

## <a name="step-1-download-and-install-the-ata-center"></a>Steg 1. Hämta och installera ATA Center
När du har kontrollerat att servern uppfyller kraven kan du fortsätta med installationen av ATA Center.
    
> [!NOTE]
>Om du har köpt en licens för Enterprise Mobility + Security (EMS) direkt via Office 365-portalen eller via licensieringsmodellen för molnlösningspartner och du inte har åtkomst till ATA via Microsoft Volume Licensing Center (VLSC), kontaktar du Microsoft Support för hjälp med att aktivera Advanced Threat Analytics (ATA).

På ATA Center-servern utför du följande steg.

1.  Hämta ATA från [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) eller [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Logga in på datorn där du installerar ATA Center som en användare som är medlem i den lokala administratörsgruppen.

3.  Kör **Microsoft ATA Center Setup.EXE** och följ installationsguiden.

> [!NOTE]   
> Se till att köra installationsfilen från en lokal enhet och inte från en monterad ISO-fil för att undvika problem om en omstart krävs som en del av installationen.   

4.  Om Microsoft .Net Framework inte är installerat uppmanas du att installera det när du startar installationen. Du kan uppmanas att starta om efter installationen av .NET Framework.
5.  På sidan **Välkommen** väljer du det språk som ska användas för ATA-installationsskärmarna och klickar på **Nästa**.

6.  Läs igenom Licensvillkor för programvara från Microsoft och om du godkänner villkoren markerar du kryssrutan och klickar sedan på **Nästa**.

7.  Vi rekommenderar att du konfigurerar ATA för att uppdateras automatiskt. Om Windows inte är inställt på att göra detta på datorn visas skärmen **Använd Microsoft Update så hjälper du till att hålla datorn säker och uppdaterad**. 
    ![Bild om att håll ATA uppdaterat](media/ata_ms_update.png)

8. Markera **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**. Detta justerar Windows-inställningarna för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), på det sätt som visas här. 

    ![Bild för automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

8.  Ange följande information på sidan **Configure the Center** (Konfigurera Center) baserat på din miljö:

    |Fält|Beskrivning|Kommentar|
    |---------|---------------|------------|
    |Installationssökväg|Det här är den plats där ATA Center kommer att installeras. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center|Låt standardvärdet vara kvar|
    |Datasökväg för databasen|Det här är den plats där MongoDB-databasfilerna kommer att finnas. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Ändra platsen till en plats där det finns utrymme att växa, baserat på storleken. **Obs:** <ul><li>I produktionsmiljöer bör du använda en enhet som har tillräckligt med utrymme baserat på kapacitetsplaneringen.</li><li>Vid stora distributioner bör databasen finnas på en separat fysisk enhet.</li></ul>Storleksinformation finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).|
    |SSL-certifikat för Center-tjänsten|Det här är det certifikat som kommer att användas av ATA-konsolen och ATA Center-tjänsten.|Klicka på nyckelikonen om du vill välja ett installerat certifikat eller kontrollera ett självsignerat certifikat vid distribution i en labbmiljö. Observera att du har möjlighet att skapa ett självsignerat certifikat.|
        
    ![Bild för konfiguration av ATA center](media/ATA-Center-Configuration.png)

10.  Klicka på **Installera** för att installera ATA Center och dess komponenter.
    Följande komponenter installeras och konfigureras under installationen av ATA Center:

    -   ATA Center-tjänsten

    -   MongoDB

    -   Anpassad datasamlingsuppsättning för Prestandaövervakaren

    -   Självsignerade certifikat (om detta valdes under installationen)

11.  När installationen är klar klickar du på **Starta** för att öppna ATA-konsolen och slutföra konfigurationen på sidan **Konfiguration**.
Du kommer nu automatiskt till inställningssidan **Allmänt** där du fortsätter med konfigurationen och distributionen av ATA-gatewayer.
Eftersom du loggar in på platsen med en IP-adress får du en varning relaterad till certifikatet, detta är normalt och du ska klicka på **Fortsätt till denna webbplats**.

### <a name="validate-installation"></a>Verifiera installationen

1.  Kontrollera att tjänsten **Microsoft Advanced Threat Analytics Center** körs.
2.  På skrivbordet klickar du på genvägen för **Microsoft Advanced Threat Analytics** för att ansluta till ATA-konsolen. Logga in med samma autentiseringsuppgifter som du använde för att installera ATA Center.



>[!div class="step-by-step"]
[«Förinstallation](configure-port-mirroring.md)
[steg 2»](install-ata-step2.md)

## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

