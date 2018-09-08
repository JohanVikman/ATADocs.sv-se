---
title: Installera Azure Advanced Threat Protection – steg 1 | Microsoft Docs
description: Första steget för att installera Azure ATP innebär att du skapar instansen för din Azure ATP-distribution.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6f44bbf50cff2e983a7ddb1ef1cf54ebaf928741
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126237"
---
*Gäller för: Azure Avancerat skydd*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Skapa en arbetsyta i Azure ATP arbetsytehanteringsportalen – steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-atp-step2.md)

Den här installationsproceduren innehåller anvisningar för att skapa och hantera din Azure ATP-instans. Information om Azure ATP-arkitekturen finns i [Azure ATP-arkitektur](atp-architecture.md).

I Azure ATP får du en enda arbetsyta eller en instans så att du kan hantera flera skogar från en enda glasruta. 

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

2. I den **Skapa ny arbetsyta** dialogrutan namnge din arbetsyta och välj en **Geoplats** för ditt datacenter. Endast en arbetsyta kan anges som primär. Ange en arbetsyta som primär påverkar integreringar – du kan bara integrera Azure ATP med Windows Defender ATP för den primära arbetsytan. Du kan ändra vilken arbetsyta är primär senare, men för att kunna göra det behöver du måste ta bort alla integreringar som redan angetts för den aktuella primära arbetsytan.
 > [!NOTE]
 > När du har valt en geografisk plats, kan du inte ändra den.
    ![Azure ATP-arbetsyta](media/create-workspace.png)

3. Du kan klicka på den **hantera Azure ATP-användarroller** länk för direkt åtkomst till den [Azure Active Directory Administrationscenter](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) och hantera dina rollgrupper.

 > [!NOTE]
 > Du måste logga in med en användare som har tilldelats rätt Azure ATP-roll att komma åt Azure ATP-arbetsyteportalen för att du har loggat in till Azure ATP. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP-rollgrupper](atp-role-groups.md).

4. Klicka på namnet på den nya arbetsytan för att komma åt Azure ATP-arbetsyteportalen för den arbetsytan.

    ![Azure ATP-arbetsytor](media/atp-workspaces.png)

- Endast den primära arbetsytan kan redigeras. Om du vill göra ändringar i andra arbetsytor, kan du ta bort dem och lägga till dem igen. Om du vill ta bort den primära arbetsytan kan du först inaktivera integreringar och ange arbetsytan ska inte **primära** innan den kan tas bort.
- Om du vill redigera en primär arbetsyta, måste du först inaktivera befintliga integreringar på arbetsytan.

- Kvarhållning av data – borttagna arbetsytor syns inte i Användargränssnittet. Läs mer på Azure ATP-datakvarhållning [Aure ATP datasäkerhet och sekretess](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[«Förinstallation](configure-port-mirroring.md)
[steg 2»](install-atp-step2.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
