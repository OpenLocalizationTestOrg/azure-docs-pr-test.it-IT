---
title: aaaAzure servizio App e sul suo impatto sui servizi di Azure esistenti
description: "Viene illustrato come hello nuovo servizio App di Azure e le funzionalità di influire sulle servizi esistenti in Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Servizio app di Azure e i servizi di Azure esistenti
Questo articolo vengono illustrati hello modifiche tooexisting servizi di Azure come parte dell'insieme di hello modifica toobring diversi servizi di Azure in [Azure App Service](https://azure.microsoft.com/services/app-service/), una nuova offerta integrata.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Panoramica
[Servizio App di Azure](https://azure.microsoft.com/services/app-service/) è un servizio cloud nuovi ed esclusivi che consente agli sviluppatori toocreate App web e dispositivi mobili per qualsiasi piattaforma e con qualsiasi dispositivo. Servizio App è che toostreamline una soluzione integrata progettata ripetuto funzioni codifica, integrazione con sistemi di SaaS ed enterprise e automatizzare i processi di business mentre soddisfa le esigenze di sicurezza, affidabilità e la scalabilità.

Servizio App riunisce hello Azure esistenti seguenti servizi - [siti Web](https://azure.microsoft.com/services/websites/), [servizi mobili](https://azure.microsoft.com/services/mobile-services/), e [servizi Biztalk](https://azure.microsoft.com/services/biztalk-services/) in un'unica combinazione servizio, mentre aggiunta di nuove funzionalità.  Servizio App consente hello toohost seguenti tipi di app:

* App Web
* App per dispositivi mobili
* App per le API
* App per la logica

Hello nella tabella seguente vengono illustrati Azure esistenti come servizi mapping tooApp hello e servizio app tipi disponibili in esso contenuti.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Servizio di Azure esistente</th>
<th align="left", style="width:10%">Servizio app di Azure</th>
<th align="left", style="width:80%">Cosa è cambiato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Siti Web di Azure</td>
<td align="left">App Web</td>
<td align="left"><li>Per i siti Web di Azure, servizio App è limitato esclusivamente toochanging hello Nome siti Web tooWeb app.
<p><li>Tutte le istanze esistenti di Siti Web sono ora app Web nel servizio app.</p>
<p><li>È possibile accedere ai siti Web inclusi esistenti tramite hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">portale Azure</a>, quale è possibile trovare tutti i siti esistenti in <em>App Web</em>.</p>
<p><li><em>Web piano di Hosting</em> è ora <em>piano di servizio App</em>. Un <em>piano di servizio app</em> può ospitare qualsiasi tipo di servizio app, ad esempio app Web, per dispositivi mobili, per la logica o per le API.</p>
<p><li>App Web del servizio app di Azure si trova ora in stato di disponibilità generale.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Altre informazioni sulle App Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Servizi mobili di Azure</td>
<td align="left">App per dispositivi mobili</td>
<td align="left"><p><li>Servizi mobili continuare toobe disponibile come servizio autonomo e rimangono completamente supportati.</p>
<p><li>App per dispositivi mobili è un tipo di app nel servizio App, che integra le funzionalità di hello di servizi mobili e altro ancora.</p>
<p><li>È facile troppo<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">esegue la migrazione da servizi mobili tooMobile app</a>.</p>
<p><li>Come parte del servizio app, App per dispositivi mobili offre nuove funzionalità oltre a quelle di Servizi mobili, come l'integrazione con sistemi locali e SaaS, slot di gestione temporanea, Processi Web, opzioni di scalabilità migliorate e altro ancora.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Altre informazioni sulle App per dispositivi mobili</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">App per le API</td>
<td align="left">
<p><li>App per le API è un nuovo tipo di app nel servizio App che consente di compilare facilmente e utilizzare le API in cloud hello.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Altre informazioni sulle API app</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">App per la logica</td>
<td align="left">
<p><li>App per la logica è un nuovo tipo di app nel servizio app, che consente di automatizzare i processi aziendali con estrema facilità.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Altre informazioni sulle App logica</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Servizi BizTalk di Azure</td>
<td align="left">App per le API di BizTalk</td>
<td align="left">
<li><p>Servizi BizTalk continuare toobe disponibile come servizio autonomo e rimangono completamente supportati.</p>
<li><p>Tutte le funzionalità di hello dei servizi BizTalk vengono integrate nel servizio App come App per le API abilitazione utenti tooperform enterprise application integration e scenari di integrazione B2B con uno qualsiasi dei tipi di app hello nel servizio App.</p>
<li><p>Logica App consentono di automatizzare i processi di business utilizzando un flussi di lavoro di progettazione visiva esperienza toocreate.</p></td>
</tr>
</tbody>
</table>

toolearn, visitare [documentazione del servizio App](https://azure.microsoft.com/documentation/services/app-service/).

