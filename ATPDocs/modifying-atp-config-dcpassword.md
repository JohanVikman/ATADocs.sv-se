---
title: Ändra Azure Advanced Threat Protection config - lösenord för domänanslutning | Microsoft Docs
description: Beskriver hur du ändrar lösenordet för domänanslutning på Azure ATP fristående sensorn.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 369f00b1b33fe509850bc331b0d5b45ae161f91c
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445968"
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Ändra Azure ATP arbetsytan portal-konfiguration – lösenord för domänanslutning



## <a name="change-the-domain-connectivity-password"></a>Ändra lösenord för domänanslutning
Om du behöver ändra lösenordet för domänanslutning, kontrollera att lösenordet är korrekt. Om det inte stoppar tjänsten Azure ATP sensor för alla distribuerade sensorer.

Om du misstänker att det har inträffat på Azure ATP fristående sensor, titta på filen Microsoft.Tri.sensor-Errors.log för följande fel: `The supplied credential is invalid.`

Så här om du vill uppdatera lösenordet för domänanslutning på Azure ATP arbetsytan portal:

> [!NOTE]
> Detta är det användarnamn och lösenord från den lokala Active Directory-distributionen och inte från Azure AD.

1.  Öppna Azure ATP arbetsytan portal på den genom att öppna URL: en för arbetsytan.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Azure ATP ikon för konfigurationsinställningar](media/atp-config-menu.png)

3.  Välj **Katalogtjänster**.

    ![Azure ATP fristående sensor ändra lösenord](media/directory-services.png)

4.  Under **Lösenord**, ändrar du lösenordet.

 > [!NOTE]
 > Ange en Active Directory-användare och lösenord här inte Azure Active Directory.

5.  Klicka på **Spara**.

6.  När du har ändrat lösenordet ska du manuellt kontrollera att Azure ATP fristående sensor-tjänsten körs på Azure ATP fristående sensor-servrar.

7. I arbetsytan-portal under **Configuration**, gå till den **Sensor** sidan och kontrollera status för sensorerna.

## <a name="see-also"></a>Se även

- [Integrering med Windows Defender ATP](integrate-wd-atp.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)