---
title: Azure Advanced Threat Protection-integrering med Windows Defender ATP | Microsoft Docs
description: Integrera Azure Advanced Threat Protection med Windows Defender ATP för fullständig threat detection täckning
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 17ade33a55039eaf8abc98901cdab9ebeef850c5
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/16/2018
---
*Gäller för: Azure Advanced Threat Protection*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrera Azure ATP med Windows Defender ATP

Azure Advanced Threat Protection kan du integrera Azure ATP med Windows Defender ATP för en ännu mer komplett lösning för skydd av hot. Medan Azure ATP övervakar trafiken på domänkontrollanterna, övervakar Windows Defender ATP dina slutpunkter tillsammans ger ett enda gränssnitt som du kan använda för att skydda din miljö.

> [!NOTE]
> Integrering är aktiverat endast om du är en privat förhandsversion Windows Defender ATP-kund.
 
Genom att integrera Windows Defender ATP i Azure ATP, du kan utnyttja alla fördelar med båda tjänsterna och skydda din miljö, inklusive:

- Azure ATP sensorer och fristående sensorer: kan sitta direkt på domänkontrollanter eller port spegling från domänkontrollanterna till ATP att samla in och analysera nätverkstrafik för flera protokoll (till exempel Kerberos, DNS, RPC, NTLM och andra) för autentisering auktorisering och insamling av information. 

-   Slutpunkten beteendebaserade sensorer: inbäddat i Windows 10 dessa sensorer samla in och bearbeta beteendebaserade signaler från operativsystemet (till exempel process, registret, fil och nätverkskommunikation) och skickar informationen sensor till ditt privata, isolerade, moln Windows Defender ATP-instans.

- Cloud security analytics: utnyttja big data, machine learning och unikt Microsoft vy över Windows-ekosystemet (som den [Microsoft verktyget](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), enterprise cloud-produkter (till exempel Office 365), och online-resurser (till exempel Bing och SmartScreen-URL: en rykte), beteendebaserade signaler översättas till insights, identifieringar, och rekommenderas svar för avancerade hot.

- Hot intelligence: genereras av Microsoft jägare, security team och förstärkta av hotinformation som tillhandahålls av partner, hot intelligence kan Windows Defender ATP identifiera angripare verktyg, tekniker och procedurer och generera aviseringar när Dessa observeras i insamlade sensordata.

Azure ATP teknik identifierar flera misstänkta aktiviteter som fokuserar på flera faser cyber attack kill kedjan inklusive:

- Rekognosering, då angripare samla in information om hur miljön skapas, vilka de olika tillgångarna är och vilka entiteter finns. De bygger vanligtvis deras plan för nästa faser för angrepp.

- Lateral rörelsecykel då en angripare investerar tid och möda i spridning av sin angreppsyta i nätverket.

- Domändominans (beständiga) under vilka en angripare fångar information så att de kan återuppta sina kampanj med olika uppsättningar med startpunkter, autentiseringsuppgifter och tekniker.

På samma gång utnyttjar Windows Defender ATP Microsoft-teknik och expertis för att identifiera avancerade cyber-attacker, tillhandahåller:

- Beteende-baserad moln påslagen, avancerade angreppsidentifiering<br></br>Söker efter attacker som gjorts efter andra försvar (Bokför intrång identifiering), ger tillämplig, korrelerade aviseringar för kända och okända motståndare försöker dölja deras aktiviteter slutpunkter.

- Omfattande tidslinje för kriminaltekniska undersökningar och minskning<br></br>Undersök enkelt omfattning överträdelse eller misstänkt beteende på en dator via en omfattande datorn tidslinje. Filen, URL: er och nätverk anslutning inventering över nätverket. Få mer information med hjälp av djup insamling och analys (”detonation”) för en fil eller URL: er.

- Inbyggda unika hot kunskapsbas<br></br>Enastående hot optik innehåller aktören information och avsiktshantering kontext för varje intel-baserade hotidentifiering – kombinera första och tredje parts intelligence källor.

## <a name="prerequisites"></a>Krav

Om du vill aktivera den här funktionen måste du ha en licens för både Azure ATP och Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Integrera Azure ATP med Windows Defender ATP

1. Ange arbetsytan som du vill integrera som **primära**. Endast en arbetsyta kan vara den primära arbetsytan och endast en primär arbetsyta kan integreras med andra tjänster. Om du någon gång i framtiden, du bör vill göra den här arbetsytan inte längre den primära arbetsytan, måste du först ta bort integrationen innan du kan ange som icke-primär.

 ![primära arbetsytan](./media/primary-workspace.png)

2. Klicka på **Configuration**, och under **datakällor** Välj **Windows Defender ATP**. Klicka på länken till **arbetsytan management**. Detta är endast tillgängligt om du har en licens för Windows Defender ATP och du redan har utfört-boarding processen för Windows Defender ATP. 

3. Klicka på inställningskuggen i din primära arbetsytan.

 ![arbetsytan integrering](./media/edit-workspace.png)
 
3. Ange integrationen till **på**. 

 ![aktivera integrering](./media/enable-integration.png)

4. I den [Windows Defender ATP-portalen](https://beta.securitycenter.windows.com/preferences/advanced), gå till **inställningar**, **avancerade funktioner** och ange **Azure ATP integration** till  **ON**. 

 ![Windows Defender ATP aktivera integrering](./media/wd-atp-enable.png)

5. Om du vill kontrollera status för integrering i Azure ATP arbetsytan portal, gå till **inställningar** och sedan **Windows Defender ATP-integration**. Du kan se status för integration. ett felmeddelande visas om det är något fel. Du kan också se vilken arbetsyta är integrerad med Windows Defender ATP.

## <a name="how-it-works"></a>Så här fungerar det

När Azure ATP och Windows Defender ATP är helt integrerade i Azure ATP arbetsytan portal Mini profil popup-fönstret och profilsida entitet innehåller varje entitet som finns i Windows Defender ATP en Aktivitetsikon för att visa att det är integrerat med Windows Defender ATP. 

 ![Windows Defender ATP-aviseringar](./media/profile-alerts-wd.png)

Om entiteten innehåller aviseringar i Windows Defender ATP, är det ett tal bredvid Aktivitetsikon så att du vet hur många aviseringar har aktiverats.

 ![Azure ATP-aviseringar](./media/atp-integrated-wd-icon-alerts.png)

Om du klickar på skylt förs till Windows Defender ATP-portalen där du kan visa och minska aviseringarna. Om enheten inte kan identifieras av Windows Defender ATP nedtonade Aktivitetsikon. 

 ![Windows Defender ATP grå](./media/wd-grey.png)

När du klickar på en slutpunkt i Windows Defender ATP-portalen kan du visa Azure ATP aviseringar. Om du klickar på aviseringar för den här entiteten i Windows Defender ATP öppnas entitetens profilen i Azure ATP. 
 
 > ! [OBS] För närvarande Azure ATP integrering med Windows Defender ATP stöder endast användare och datorer från lokalt AD. Användare från Azure AD och virtuella datorer som hanteras i Azure visas inte som en del av integrering 

![Windows Defender ATP-aviseringar](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Se även

- [Undersöka lateral förflyttning sökvägar med Azure ATP](use-case-lateral-movement-path.md)
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Azure ATP-arkitektur](atp-architecture.md)
- [Installera ATP](install-atp-step1.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)

