---
title: Installera Advanced Threat Analytics steg 1 | Microsoft Docs
description: Första steget för att installera ATA omfattar att hämta och installera ATA Center på den valda servern.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 028b27b36ed483338f73c30551b9f0296731a87e
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126220"
---
*Gäller för: Advanced Threat Analytics version 1.9*


# <a name="install-ata---step-1"></a>Installera ATA – Steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-ata-step2.md)

Den här installationsproceduren innehåller anvisningar som beskriver hur du utför en helt ny installation av ATA 1.8. Information om hur du uppdaterar en befintlig ATA-distribution från en tidigare version finns i [ATA-Migreringsguide för version 1.9](ata-update-1.9-migration-guide.md).

> [!IMPORTANT] 
> Om du använder Windows 2012 R2 kan du installera KB2934520 på ATA Center-servern och på ATA-gatewayservrarna innan du påbörjar installationen, annars ATA-installationen installerar uppdateringen och kräver en omstart mitt i ATA-installationen.

## <a name="step-1-download-and-install-the-ata-center"></a>Steg 1. Hämta och installera ATA Center
När du har kontrollerat att servern uppfyller kraven kan du fortsätta med installationen av ATA Center.
    
> [!NOTE]
>Om du har köpt en licens för Enterprise Mobility + Security (EMS) direkt via Office 365-portalen eller via licensieringsmodellen för molnlösningspartner och du inte har åtkomst till ATA via Microsoft Volume Licensing Center (VLSC), kontaktar du Microsoft Support för hjälp med att aktivera Advanced Threat Analytics (ATA).

På ATA Center-servern utför du följande steg.

1.  Hämta ATA från [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) eller [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Logga in på datorn som du installerar ATA Center som en användare som är medlem i gruppen lokala administratörer.

3.  Kör **Microsoft ATA Center Setup.EXE** och följ installationsguiden.

> [!NOTE]   
> Se till att köra installationsfilen från en lokal enhet och inte från en monterad ISO-fil för att undvika problem om en omstart krävs som en del av installationen.   

4.  Om Microsoft .net Framework inte är installerat uppmanas du att installera det när du startar installationen. Du kan uppmanas att starta om efter installationen av .NET Framework.
5.  På sidan **Välkommen** väljer du det språk som ska användas för ATA-installationsskärmarna och klickar på **Nästa**.

6.  Läs licensvillkoren för programvara från Microsoft och om du accepterar villkoren markerar du kryssrutan och klicka sedan på **nästa**.

7.  Vi rekommenderar att du konfigurerar ATA för att uppdateras automatiskt. Om Windows inte är inställt på att göra detta på datorn, får du den **Använd Microsoft Update för att hålla datorn säker och uppdaterad** skärmen. 
    ![Bild om att håll ATA uppdaterat](media/ata_ms_update.png)

8. Markera **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**. Detta justerar Windows-inställningar för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), som visas här. 

    ![Bild för automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

8.  Ange följande information på sidan **Configure the Center** (Konfigurera Center) baserat på din miljö:

    |Fält|Description|Kommentar|
    |---------|---------------|------------|
    |Installationssökväg|Det här är den plats där ATA Center är installerat. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center|Låt standardvärdet vara kvar|
    |Datasökväg för databasen|Det här är den plats där MongoDB-databasfilerna finns. Detta är som standard %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Ändra platsen till en plats där det finns utrymme att växa, baserat på storleken. **Obs:** <ul><li>I produktionsmiljöer bör du använda en enhet som har tillräckligt med utrymme baserat på kapacitetsplaneringen.</li><li>Vid stora distributioner bör databasen finnas på en separat fysisk enhet.</li></ul>Storleksinformation finns i [ATA-kapacitetsplanering](ata-capacity-planning.md).|
    |SSL-certifikat för Center-tjänsten|Det här är det certifikat som används av ATA-konsolen och ATA Center-tjänsten.|Klicka på nyckelikonen om du vill välja ett installerat certifikat eller kontrollera ett självsignerat certifikat vid distribution i en labbmiljö. Du har möjlighet att skapa ett självsignerat certifikat.|
        
    ![Bild för konfiguration av ATA center](media/ATA-Center-Configuration.png)

10.  Klicka på **Installera** för att installera ATA Center och dess komponenter.
    Följande komponenter installeras och konfigureras under installationen av ATA Center:

    -   ATA Center-tjänsten

    -   MongoDB

    -   Anpassad datasamlingsuppsättning för Prestandaövervakaren

    -   Självsignerade certifikat (om detta valdes under installationen)

11.  När installationen är klar klickar du på **Starta** för att öppna ATA-konsolen och slutföra konfigurationen på sidan **Konfiguration**.
Nu kommer du automatiskt till den **Allmänt** inställningssidan för att fortsätta konfigurationen och distributionen av ATA-gatewayer.
Eftersom du loggar in på platsen med en IP-adress, du får en varning relaterad till certifikatet, detta är normalt och du på **Fortsätt till denna webbplats**.

### <a name="validate-installation"></a>Verifiera installationen

1.  Kontrollera att tjänsten **Microsoft Advanced Threat Analytics Center** körs.
2.  På skrivbordet klickar du på genvägen för **Microsoft Advanced Threat Analytics** för att ansluta till ATA-konsolen. Logga in med samma autentiseringsuppgifter som du använde för att installera ATA Center.

### <a name="set-anti-virus-exclusions"></a>Ange ett virusskyddsprogram undantag

När du har installerat ATA Center ska du undanta databaskatalogen MongoDB från att genomsökas kontinuerligt av ditt antivirusprogram. Standardplatsen måltabeller är: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**.



>[!div class="step-by-step"]
[«Förinstallation](configure-port-mirroring.md)
[steg 2»](install-ata-step2.md)

## <a name="related-videos"></a>Relaterade videor
- [Välja rätt typ av ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Översikt över ATA-distribution](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Se även
- [ATA POC-Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

