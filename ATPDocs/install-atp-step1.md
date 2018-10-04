---
title: Installera Azure Advanced Threat Protection – steg 1 | Microsoft Docs
description: Första steget för att installera Azure ATP innebär att du skapar instansen för din Azure ATP-distribution.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a6238b6d3cd05c3896b88701c15d17404db43cf
ms.sourcegitcommit: 04ed0b9faf72d82cd10bf84efd9dc5aa525be212
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/03/2018
ms.locfileid: "48245357"
---
*Gäller för: Azure Avancerat skydd*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Skapa en arbetsyta i Azure ATP arbetsytehanteringsportalen – steg 1

> [!div class="step-by-step"]
> [Steg 2 »](install-atp-step2.md)

Den här installationsproceduren innehåller anvisningar för att skapa och hantera din Azure ATP-instans. Information om Azure ATP-arkitekturen finns i [Azure ATP-arkitektur](atp-architecture.md).

I Azure ATP får du en enda arbetsyta eller så att du kan hantera flera skogar från en enda glasruta-instans. 

> [!NOTE]
> För närvarande distribueras Azure ATP-datacenter i Europa, Nordamerika/centrala America/Karibien och Asien.

## <a name="step-1-enter-the-management-portal"></a>Steg 1. Ange hanteringsportalen

När du har kontrollerat att ditt nätverk uppfyller kraven för sensorn, kan du fortsätta med skapa Azure ATP-arbetsyta.

> [!NOTE]
>Du måste vara en global administratör eller säkerhetsadministratör på den klienten för att komma åt hanteringsportalen.


1.  Ange [Azure ATP-portal](https://portal.atp.azure.com).

2.  Logga in med ditt Azure Active Directory-användarkonto.

## <a name="step-2-create-your-workspace"></a>Steg 2. Skapa din arbetsyta

1. Klicka på **Skapa arbetsyta**.

2. I den **Skapa ny arbetsyta** dialogrutan namnge din arbetsyta och välj en **Geoplats** för ditt datacenter. Din arbetsyta är **primära** som standard. 
 > [!NOTE]
 > När du har valt en geografisk plats, kan du inte ändra den.
    ![Azure ATP-arbetsyta](media/create-workspace.png)

3. Du kan klicka på den **hantera Azure ATP-användarroller** länk för direkt åtkomst till den [Azure Active Directory Administrationscenter](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) och hantera dina rollgrupper.

 > [!NOTE]
 > Du måste logga in med en användare som har tilldelats rätt Azure ATP-roll att komma åt Azure ATP-arbetsyteportalen för att du har loggat in till Azure ATP. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP-rollgrupper](atp-role-groups.md).

4. Klicka på namnet på din arbetsyta för att få åtkomst till arbetsytan Azure ATP-portalen.

    ![Azure ATP-arbetsytor](media/atp-workspaces.png)

- Endast den primära arbetsytan kan redigeras. Om du vill ta bort din aktiva arbetsyta måste du först inaktivera integreringar innan den kan tas bort.

- Kvarhållning av data – tidigare borttagna arbetsytor syns inte i Användargränssnittet. Läs mer på Azure ATP-datakvarhållning [Aure ATP datasäkerhet och sekretess](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[«Förinstallation](atp-prerequisites.md)
[steg 2»](install-atp-step2.md)



## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
