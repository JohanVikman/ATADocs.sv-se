---
title: Tagga känsliga konton med ATA | Microsoft Docs
description: Beskriver hur du tagga känsliga konton med hjälp av Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e30e4d2085be460432be131b10beb067020c5959
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166518"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="tag-sensitive-accounts"></a>Tagga känsliga konton

Du kan manuellt tagga grupper eller känsliga konton för att förbättra identifieringar. Det är viktigt att se till att detta uppdateras eftersom vissa ATA-identifieringar, till exempel känsliga grupp ändring av identifiering och lateral rörelsesökväg är beroende av vilka grupper och konton betraktas som känslig. Tidigare ATA automatiskt vara en entitet *känsliga* om den var medlem i en specifik lista över grupper. Du kan nu manuellt tagga andra användare eller grupper som känsliga, till exempel styrelsemedlemmar, chefer, chef för försäljning, etc. och ATA ska anses vara känslig.

1.  I ATA-konsolen klickar du på den **Configuration** kugghjulet på menyraden.

2.  Under **identifiering,** klickar du på **entitetstaggar**.

    ![ATA-entitetstaggar](media/entity-tags.png)

3.  I den **känsliga** Skriv namnet på den **känsliga konton** och **känsliga grupper** och klicka sedan på **+** logga in att lägga till dem.

    ![ATA känsligt konto exemplet](media/sensitive-account-sample.png)

4. Klicka på **Spara**.

5. Gå till profilsidan entitet genom att klicka på enhetens namn. Här kommer du att kunna se varför entiteten betraktas som känslig – oavsett om den på grund av medlemskap i en grupp eller på grund av manuell taggning som känsliga.


## <a name="sensitive-groups"></a>Känsliga grupper

Följande lista över grupper betraktas som känslig av ATA. En entitet som är medlem i dessa grupper betraktas som känslig:

-   Administratörer
-   Privilegierade användare
-   Kontoansvariga
-   Serveransvariga
-   Skrivaransvariga
-   Ansvariga för säkerhetskopiering
-   Ansvariga för replikering
-   Användare av fjärrskrivbord 
-   Ansvariga för nätverkskonfigurering 
-   Incoming Forest Trust Builders
-   Domänadministratörer
-   Domänkontrollanter
-   Skapare och ägare av grupprincip 
-   skrivskyddade domänkontrollanter 
-   Företagets skrivskyddade domänkontrollanter 
-   Schemaadministratörer 
-   Företagsadministratörer
     
## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
