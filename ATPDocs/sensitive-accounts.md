---
title: "Tagga känsliga konton med Azure ATP | Microsoft Docs"
description: "Beskriver hur du tagga känsliga konton med hjälp av Azure Advanced Threat Protection (ATP)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4270ebda76309e19518f9d49b72bbce7f9bb5f32
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection version 1.9.*



# <a name="working-with-sensitive-accounts"></a>Arbeta med känsliga konton

## <a name="sensitive-groups"></a>Känsliga grupper

Följande lista över grupper betraktas som känslig genom Azure ATP. En entitet som är medlem i dessa grupper betraktas som känslig:

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


## <a name="tagging-sensitive-accounts"></a>Taggning känsliga konton

Förutom dessa grupper kan du tagga grupper eller konton som känslig för att förbättra identifieringar manuellt. Detta är viktigt eftersom vissa Azure ATP identifieringar, till exempel känsliga grupp ändring identifiering och lateral förflyttning sökväg förlitar sig på vilka grupper och konton anses vara känslig. Manuellt kan du tagga andra användare eller grupper som skiftlägeskänslig, till exempel styrelsemedlemmar, chefer, försäljning, etc.-chef och Azure ATP anser dem känslig.

1.  I arbetsytan ATP Azure-portalen klickar du på den **Configuration** kugge i menyraden.

2.  Under **identifiering** klickar du på **entitetstaggar**.

    ![Azure ATP-entitetstaggar](media/entity-tags.png)

3.  I den **känsliga** avsnittet, skriver du namnet på den **känsliga konton** och **känsliga grupper** och klicka sedan på  **+**  Logga lägga till dem.

    ![Azure ATP känsligt konto-exempel](media/sensitive-account-sample.png)

4. Klicka på **Spara**.

    
## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)