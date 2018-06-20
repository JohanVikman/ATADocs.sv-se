---
title: Installera Azure Advanced Threat Protection - steg 1 | Microsoft Docs
description: Första steget för att installera Azure ATP innebär att du skapar en arbetsyta för Azure ATP-distribution.
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
ms.openlocfilehash: a4c2f03955eddb4615b347fa8a211501546e6f4a
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/16/2018
ms.locfileid: "31007278"
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Skapa en arbetsyta i Azure ATP arbetsytan hanteringsportalen – steg 1

>[!div class="step-by-step"]
[Steg 2 »](install-atp-step2.md)

Den här installationsproceduren innehåller anvisningar för att skapa och hantera en arbetsyta i hanteringsportalen för Azure ATP-arbetsytan. Mer information om Azure ATP arkitektur finns [Azure ATP arkitektur](atp-architecture.md).

Du har möjlighet att hantera och övervaka flera arbetsytor i Azure ATP. Detta är särskilt användbart om du vill skapa en demo-arbetsyta och en test-arbetsyta där du kan POC Azure ATP innan den distribueras ut till hela organisationen. Det krävs också stöd för distributioner med flera skogar. En enda arbetsyta kan endast övervaka flera domäner från en enda skog. 

> [!NOTE]
> - Du kan ha högst två aktiva arbetsytor. När du har tagit bort en arbetsyta kan du kontakta supporten om du vill återaktivera den. Du en högst bestå av tre borttagna arbetsytor. Kontakta Azure ATP-supporten om du vill öka antalet sparade, borttagna arbetsytor.
> - För närvarande har Azure ATP Datacenter distribuerats i Europa, Nordamerika/centrala Nordamerika/Västindien och Asien.

## <a name="step-1-enter-the-workspace-management-portal"></a>Steg 1. Ange arbetsytan management portal

När du har kontrollerat att nätverket uppfyller kraven för sensorn, kan du fortsätta med att skapa Azure ATP-arbetsytan.

> [!NOTE]
>Du måste vara en global administratör eller säkerhetsadministratör på den klienten för att komma åt hanteringsportalen arbetsytan.


1.  Ange [Azure ATP arbetsytan portal](https://portal.atp.azure.com).

2.  Logga in med ditt Azure Active Directory-användarkonto.

## <a name="step-2-create-a-workspace"></a>Steg 2. Skapa en arbetsyta

1. Klicka på **Skapa arbetsyta**.

2. I den **Skapa ny arbetsyta** dialogrutan namnge din arbetsyta, bestämma om den primära arbetsytan eller inte och väljer en **Geolokalisering** för ditt datacenter. Endast en arbetsyta kan anges som primär. Ange en arbetsyta som primär påverkar integreringar – du kan endast integrera Azure ATP med Windows Defender ATP för den primära arbetsytan. Du kan ändra vilken arbetsyta är primära senare, men för att kunna göra så du måste ta bort alla integreringar som redan angetts för den aktuella primära arbetsytan.
 > [!NOTE]
 > När du har valt en Geolokalisering kan du inte ändra den.
    ![Azure ATP-arbetsytan](media/create-workspace.png)

3. Du kan klicka på den **hantera Azure ATP användarroller** länk för direkt åtkomst till den [Azure Active Directory Administrationscenter](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) och hantera dina rollgrupper.

 > [!NOTE]
 > Du måste logga in med en användare som har tilldelats rollen rätt Azure ATP åt Azure ATP arbetsytan portalen för att kunna logga in på Azure ATP. Mer information om rollbaserad åtkomstkontroll (RBAC) i Azure ATP finns [arbeta med Azure ATP rollgrupper](atp-role-groups.md).

4. Klicka på namnet på arbetsytan nya åtkomst Azure ATP arbetsytan portal för arbetsytan.

    ![Azure ATP arbetsytor](media/atp-workspaces.png)

- Endast den primära arbetsytan kan redigeras. Om du vill göra ändringar i andra arbetsytor, kan du ta bort dem och lägga till dem igen. Om du vill ta bort den primära arbetsytan du först inaktivera integreringar och arbetsyta får inte vara **primära** innan den kan tas bort.
- Om du vill redigera en primär arbetsyta, måste du först inaktivera befintliga integreringar i arbetsytan.

- Datalagring – borttagna arbetsytor visas inte i Användargränssnittet, men deras data sparas enligt [Microsoft databevarandeprincip](https://www.microsoft.com/trustcenter/privacy/you-own-your-data).


>[!div class="step-by-step"]
[«Förinstallation](configure-port-mirroring.md)
[steg 2»](install-atp-step2.md)


## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
