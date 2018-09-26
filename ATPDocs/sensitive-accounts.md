---
title: Tagga känsliga konton med Azure ATP | Microsoft Docs
description: Beskriver hur du tagga känsliga konton med Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ccb87ab6b3fabed5edaf7c32324701c74259f098
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750445"
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
-   Ansvariga för nätverkskonfigurering 
-   Incoming Forest Trust Builders
-   Domänadministratörer
-   Domänkontrollanter
-   Skapare och ägare av grupprincip 
-   skrivskyddade domänkontrollanter 
-   Företagets skrivskyddade domänkontrollanter 
-   Schemaadministratörer 
-   Företagsadministratörer

 > [!NOTE]
 > Till September 2018 användare av fjärrskrivbord har också automatiskt anses vara känsliga med Azure ATP. Remote Desktop entiteter eller grupper har lagts till det här datumet är inte längre automatiskt markerats som känsliga när Remote Desktop-enheter och grupper som har lagts till innan detta datum förbli markerat som känsliga. Den här inställningen för känsliga kan nu ändras manuellt.  

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