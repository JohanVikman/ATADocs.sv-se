---
title: Installera Azure Advanced Threat Protection – steg 1 | Microsoft Docs
description: Första steget för att installera Azure ATP innebär att du skapar en arbetsyta för din Azure ATP-distribution.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cadd708c20733324b939db1e35d12aae3f2d80f2
ms.sourcegitcommit: 40dbce8045f689376a50275fb12e3c5c32ca8092
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/04/2018
ms.locfileid: "37799084"
---
*Gäller för: Azure Avancerat skydd*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Skapa en arbetsyta i Azure ATP arbetsytehanteringsportalen – steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-atp-step2.md)

Den här installationsproceduren innehåller anvisningar för att skapa och hantera en arbetsyta i hanteringsportalen för Azure ATP-arbetsytan. Information om Azure ATP-arkitekturen finns i [Azure ATP-arkitektur](atp-architecture.md).

I Azure ATP har du möjlighet att hantera och övervaka flera arbetsytor. Detta är särskilt användbart om du vill skapa en demo-arbetsyta och en test-arbetsyta där du kan POC Azure ATP innan den distribueras ut till hela organisationen. Detta krävs också stöd för distributioner med flera skogar. En enda arbetsyta kan endast övervaka flera domäner från en enda skog. 

> [!NOTE]
> För närvarande distribueras Azure ATP-datacenter i Europa, Nordamerika/centrala America/Karibien och Asien.

## <a name="step-1-enter-the-workspace-management-portal"></a>Steg 1. Ange arbetsytehanteringsportalen

När du har kontrollerat att ditt nätverk uppfyller kraven för sensorn, kan du fortsätta med skapa Azure ATP-arbetsyta.

> [!NOTE]
>Du måste vara en global administratör eller säkerhetsadministratör på den klienten för att komma åt arbetsytehanteringsportalen.


1.  Ange [Azure ATP-arbetsyteportalen](https://portal.atp.azure.com).

2.  Logga in med ditt Azure Active Directory-användarkonto.

## <a name="step-2-create-a-workspace"></a>Steg 2. Skapa en arbetsyta

1. Klicka på **Skapa arbetsyta**.

2. I den **Skapa ny arbetsyta** dialogrutan namnge din arbetsyta, bestämmer om det är din primära arbetsytan eller inte och väljer en **Geoplats** för ditt datacenter. Endast en arbetsyta kan anges som primär. Ange en arbetsyta som primär påverkar integreringar – du kan bara integrera Azure ATP med Windows Defender ATP för den primära arbetsytan. Du kan ändra vilken arbetsyta är primär senare, men för att kunna göra det behöver du måste ta bort alla integreringar som redan angetts för den aktuella primära arbetsytan.
 > [!NOTE]
 > När du har valt en geografisk plats, kan du inte ändra den.
    ![Azure ATP-arbetsyta](media/create-workspace.png)

3. Du kan klicka på den **hantera Azure ATP-användarroller** länk för direkt åtkomst till den [Azure Active Directory Administrationscenter](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) och hantera dina rollgrupper.

 > [!NOTE]
 > Du måste logga in med en användare som har tilldelats rätt Azure ATP-roll att komma åt Azure ATP-arbetsyteportalen för att du har loggat in till Azure ATP. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP-rollgrupper](atp-role-groups.md).

4. Klicka på namnet på den nya arbetsyteåtkomst Azure ATP-arbetsyteportalen för den arbetsytan.

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
