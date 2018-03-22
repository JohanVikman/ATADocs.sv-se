---
title: "Tagga känsliga konton med ATA | Microsoft Docs"
description: "Beskriver hur du tagga känsliga konton med hjälp av Advanced Threat Analytics (ATA)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d9666c0a4fb3aad027ac1f85719bc533e919d75a
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="tag-sensitive-accounts"></a>Taggen känsliga konton

Du kan manuellt lägga till märkord grupper eller konton som känslig för att förbättra identifieringar. Det är viktigt att se till att detta uppdateras eftersom vissa ATA-identifieringar, till exempel känsliga grupp ändring identifiering och lateral förflyttning sökväg förlitar sig på vilka grupper och konton anses vara känslig. Tidigare ATA automatiskt anses vara en entitet *känsliga* om den var medlem i en viss lista över grupper. Du kan nu manuellt tagga andra användare eller grupper som skiftlägeskänslig, till exempel styrelsemedlemmar, chefer, försäljning, etc.-chef och ATA ska anses vara känslig.

1.  I ATA-konsolen klickar du på den **Configuration** kugge i menyraden.

2.  Under **identifiering,** klickar du på **entitetstaggar**.

    ![ATA-entitetstaggar](media/entity-tags.png)

3.  I den **känsliga** avsnittet, skriver du namnet på den **känsliga konton** och **känsliga grupper** och klicka sedan på  **+**  Logga lägga till dem.

    ![ATA känsligt konto exempel](media/sensitive-account-sample.png)

4. Klicka på **Spara**.

5. Gå till sidan entitet profil genom att klicka på enhetsnamnet. Här kommer du att kunna se varför entiteten betraktas som känslig - om det är på grund av medlemskap i en grupp eller på grund av manuell taggning som känsliga.

     
## <a name="see-also"></a>Se även
[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
