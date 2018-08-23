---
title: Tagga känsliga konton med Azure ATP | Microsoft Docs
description: Beskriver hur du tagga känsliga konton med Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8f1a78e8ce6005c58dc98171a4bf4d049ff60d8f
ms.sourcegitcommit: dc56b9e9533db1a2dc314b199e90191bb25adaba
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/14/2018
ms.locfileid: "41734776"
---
*Gäller för: Azure Avancerat skydd*



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


## <a name="tagging-sensitive-accounts"></a>Tagga känsliga konton

Förutom dessa grupper kan du tagga grupper eller känsliga konton för att förbättra identifieringarna manuellt. Detta är viktigt eftersom vissa Azure ATP-identifieringar, till exempel känsliga grupp ändring av identifiering och lateral rörelsesökväg är beroende av vilka grupper och konton betraktas som känslig. Manuellt kan du tagga andra användare eller grupper som känsliga, till exempel styrelsemedlemmar, chefer, chef för försäljning, etc. och Azure ATP kan identifiera känslig.

1.  I Azure ATP-arbetsyteportalen, klickar du på den **Configuration** kugghjulet på menyraden.

2.  Under **identifiering** klickar du på **entitetstaggar**.

    ![Azure ATP-entitetstaggar](media/entity-tags.png)

3.  I den **känsliga** Skriv namnet på den **känsliga konton** och **känsliga grupper** och klicka sedan på **+** logga in att lägga till dem.

    ![Exempel på Azure ATP känsligt konto](media/sensitive-account-sample.png)

4. Klicka på **Spara**.

    
## <a name="see-also"></a>Se även

- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)