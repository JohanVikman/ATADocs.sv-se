---
title: "Undersöka rekognosering med DNS | Microsoft Docs"
description: "Den här artikeln beskriver rekognosering med DNS och innehåller instruktioner för hur du hanterar det här hotet när det identifieras av ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4455be4f300b698b2ba8b53529e894700a282147
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/06/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*

# <a name="investigating-reconnaissance-using-dns"></a>Undersöka rekognosering med DNS

Om ATA identifierar **rekognosering med DNS** i ditt nätverk och aviserar dig om det, kan du använda informationen i den här artikeln för att undersöka aviseringen och se hur du åtgärdar problemet.

## <a name="what-is-reconnaissance-using-dns"></a>Vad är rekognosering med DNS?

Aviseringen om **rekognosering med DNS** anger att misstänkta DNS-frågor (Domain Name System) görs från en ovanlig värd för att rekognosera ditt interna nätverk.

DNS (Domain Name System) är en tjänst som implementeras som en hierarkisk, distribuerad databas som kan matcha värdnamn och domännamn. Namnen i en DNS-databas bildar en hierarkisk trädstruktur kallad domänens namnområde.
För en angripare innehåller ditt DNS-system värdefull information om mappningen i ett internt nätverk, inklusive en lista över alla servrar och ofta alla klienter och deras mappningar till IP-adresser. Den här informationen är dessutom värdefull eftersom den anger värdnamn som ofta är beskrivande i en viss nätverksmiljö. Genom att samla in den här informationen kan en angripare bättre prioritera sitt arbete på relevanta entiteter under en attack. Verktyg som [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce) och inbyggda verktyg som [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) innehåller funktioner för värdidentifiering med DNS-rekognosering.
Identifieringen av rekognosering med DNS-frågor från en intern värd bör inte tas lättvindigt eftersom det kan vara tecken på att en befintlig värd eller ett större nätverk har komprometterats, eller tyda på ett insiderhot.

## <a name="dns-query-types"></a>DNS-frågetyper

Det finns flera frågetyper i DNS-protokollet. ATA identifierar AXFR-förfrågningarna (Transfer) och skapar en avisering när de observeras. Den här typen av fråga bör endast komma från DNS-servrar.

## <a name="discovering-the-attack"></a>Identifiera angreppet

När en angripare försöker utföra rekognosering med DNS identifieras detta av ATA och märks med medelhög allvarlighetsgrad.

![ATA identifierar DNS-rekognosering](./media/dns-recon.png)
 
ATA visar namnet på källdatorn samt ytterligare information om själva DNS-frågan som kördes. Det kan till exempel hända att flera försök görs från samma värd.

## <a name="investigating"></a>Undersöka

För att undersöka rekognosering med DNS måste du först ta reda på orsaken till frågorna. Dessa kan identifieras i någon av följande kategorier: 
-   Korrekta positiva identifieringar – Det finns en angripare eller skadlig kod i ditt nätverk. Detta kan antingen vara en angripare som har gjort intrång i nätverket, eller ett insiderhot.
-   Harmlösa korrekta positiva identifieringar – Dessa identifieringar kan vara aviseringar som har utlösts av penetrationstestning, aktiviteter av granskningsteamet, säkerhetsgenomsökningar, en nästa generations brandvägg eller IT-administratörer som utför sanktionerade aktiviteter.
-   Falska positiva identifieringar – Du kan få aviseringar som beror på en felkonfiguration, t.ex. om UDP-port 53 är blockerad mellan ATA-gatewayen och din DNS-server (eller ett annat nätverksproblem).

Följande diagram gör det enklare att avgöra vilka undersökningssteg du bör vidta:

![Matcha DNS-rekognosering med ATA](./media/dns-recon-diagram.png)
 
1.  Det första steget är att identifiera den dator som aviseringen kommer från, som du ser nedan:
 
    ![Visa misstänkt aktivitet med DNS-rekognosering i ATA](./media/dns-recon.png)
2.  Fastställ vad det är för typ av dator. Är det en arbetsstation, server, arbetsstation, penetrationstestningsstation eller liknande?
3.  Om datorn är en DNS-server och har behörighet att begära en sekundär kopia av zonen, så är det en falsk positiv identifiering. När du hittar en falsk positiv identifiering kan du använda alternativet **Undanta** så att du inte får den här specifika aviseringen för den här datorn mer.
4. Kontrollera att UDP-port 53 är öppen mellan ATA-gatewayen och din DNS-server.
4.  Om datorn används för administrativt arbete eller penetrationstestning rör det sig om en harmlös korrekt positiv identifiering, och datorn i fråga kan konfigureras som ett undantag.
5.  Om datorn inte används för penetrationstestning kontrollerar du om den kör en säkerhetsgenomsökning eller en nästa generations brandvägg, vilket kan involvera DNS-förfrågningar med AXFR-typen.
6.  Om inga av dessa kriterier är uppfyllda är det möjligt att datorn har komprometterats, vilket i så fall måste utredas noggrant. 
7.  Om frågorna är begränsade till specifika datorer och du avgör att de inte är harmlösa, bör du utföra följande steg:
    1.  Granska tillgängliga loggkällor. 
    2.  Genomför värdbaserade analyser. 
    3.  Om aktiviteten inte är från en misstänkt användare bör en kriminalteknisk analys utföras på datorn för att avgöra om den har komprometterats med skadlig kod.

## <a name="post-investigation"></a>Efter undersökningen

Skadlig kod som används för att kompromettera värden kan innehålla trojaner med bakdörrar. I de fall då lyckade laterala förflyttningar har identifierats från den komprometterade värden bör reparationsåtgärderna även omfatta dessa värdar, och alla lösenord och autentiseringsuppgifter som används på värden och på alla värdar i den laterala förflyttningen bör ändras. 

Om den komprometterade värden inte kan bekräftas som ren efter reparationsåtgärderna, eller om rotorsaken till intrånget inte kan identifieras, rekommenderar Microsoft att du säkerhetskopierar viktiga data och återskapar värddatorn. Nya eller ombyggda värdar bör även härdas innan de läggs till i nätverket igen för att förhindra att de komprometteras igen. 

Microsoft rekommenderar att du använder ett professionellt team för incidentsvar och återställning, som kan nås via ditt Microsoft-kontoteam, för att få hjälp med att identifiera om en angripare har distribuerat ihållande metoder i nätverket.

## <a name="mitigation"></a>Lösningar

Du kan skydda en intern DNS-server för att förhindra rekognosering med DNS genom att inaktivera eller begränsa zonöverföringar till endast angivna IP-adresser. Mer information om hur du begränsar zonöverföringar finns i Windows Server Technet-artikeln [Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (Begränsa zonöverföringar). Du kan ytterligare begränsa begränsade zonöverföringar genom att [skydda zonöverföringar med IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx). Ändringar av zonöverföringar är en av uppgifterna i en checklista som bör utföras för att [skydda DNS-servrar från både interna och externa attacker](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).



## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
