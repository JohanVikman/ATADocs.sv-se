---
title: Ändra Azure Advanced Threat Protection-konfigurationen – lösenord för domänanslutning | Microsoft Docs
description: Beskriver hur du ändrar lösenordet för domänanslutning på fristående Azure ATP-sensorn.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e5b3fd544fb52cd2979ab95d34918ffba3f56541
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166195"
---
*Gäller för: Azure Avancerat skydd*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Ändra Azure ATP arbetsytan portalen-konfiguration – lösenord för domänanslutning



## <a name="change-the-domain-connectivity-password"></a>Ändra lösenord för domänanslutning
Om du vill ändra lösenordet för domänanslutning, se till att är lösenordet korrekt. Om du inte stoppar tjänsten Azure ATP-sensorn för alla distribuerade sensorer.

Om du misstänker att det har inträffat på den fristående sensorn Azure ATP tittar du på filen Microsoft.Tri.sensor-Errors.log för följande fel: `The supplied credential is invalid.`

Följ den här proceduren för att uppdatera lösenordet för domänanslutning på Azure ATP-arbetsyteportalen:

> [!NOTE]
> Detta är det användarnamn och lösenord från den lokala Active Directory-distributionen och inte från Azure AD.

1.  Öppna Azure ATP-arbetsyteportalen på den genom att gå till URL: en för arbetsytan.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Azure ATP ikon för konfigurationsinställningar](media/atp-config-menu.png)

3.  Välj **Katalogtjänster**.

    ![Azure ATP fristående sensorn ändra lösenord](media/directory-services.png)

4.  Under **Lösenord**, ändrar du lösenordet.

 > [!NOTE]
 > Ange ett Active Directory-användare och lösenord här, inte Azure Active Directory.

5.  Klicka på **Spara**.

6.  När du har ändrat lösenordet manuellt kan kontrollera att Azure ATP fristående sensorn tjänst körs på Azure ATP fristående sensorn servrar.

7. I arbetsyteportalen under **Configuration**går du till den **Sensor** sidan och kontrollera status för sensorerna.

## <a name="see-also"></a>Se även

- [Integrering med Windows Defender ATP](integrate-wd-atp.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)