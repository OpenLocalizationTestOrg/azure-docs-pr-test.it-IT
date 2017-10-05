---
title: Servizio app di Azure e impatto sui servizi di Azure esistenti
description: "Viene illustrato come il nuovo servizio app di Azure e le relative funzionalità influiscono sui servizi esistenti in Azure."
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
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Servizio app di Azure e i servizi di Azure esistenti
Questo articolo illustra le modifiche ai servizi di Azure esistenti come parte delle modifiche introdotte al fine di raggruppare vari servizi di Azure nel [servizio app di Azure](https://azure.microsoft.com/services/app-service/), una nuova offerta integrata.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Panoramica
[servizio app di Azure](https://azure.microsoft.com/services/app-service/) è un servizio cloud nuovo ed esclusivo che consente agli sviluppatori di creare app per dispositivi mobili e Web per qualsiasi piattaforma e dispositivo. Il servizio app viene offerto come soluzione integrata progettata per snellire le ripetitive procedure di scrittura del codice, integrarsi con i sistemi aziendali e SaaS e automatizzare i processi aziendali, adattandosi al contempo alle esigenze di sicurezza, affidabilità e scalabilità.

Il servizio app riunisce i servizi di Azure esistenti [Siti Web](https://azure.microsoft.com/services/websites/), [Servizi mobili](https://azure.microsoft.com/services/mobile-services/) e [Servizi Biztalk](https://azure.microsoft.com/services/biztalk-services/) in un unico servizio combinato a cui sono state aggiunte nuove funzionalità avanzate.  Il servizio app consente di ospitare i seguenti tipi di app:

* App Web
* App per dispositivi mobili
* App per le API
* App per la logica

La tabella seguente illustra la corrispondenza tra i servizi di Azure esistenti e il nuovo servizio app, nonché i tipi di app disponibili al suo interno.

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
<td align="left"><li>Per quanto riguarda Siti Web di Azure, le modifiche si riducono esclusivamente al cambio di nome da Siti Web ad App Web.
<p><li>Tutte le istanze esistenti di Siti Web sono ora app Web nel servizio app.</p>
<p><li>È possibile accedere ai siti web esistenti tramite il <a href="http://go.microsoft.com/fwlink/?LinkId=529715">portale di Azure</a>, in cui tutti i siti Web esistenti saranno visualizzati sotto <em>App Web</em>.</p>
<p><li><em>Web piano di Hosting</em> è ora <em>piano di servizio App</em>. Un <em>piano di servizio app</em> può ospitare qualsiasi tipo di servizio app, ad esempio app Web, per dispositivi mobili, per la logica o per le API.</p>
<p><li>App Web del servizio app di Azure si trova ora in stato di disponibilità generale.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Altre informazioni sulle App Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Servizi mobili di Azure</td>
<td align="left">App per dispositivi mobili</td>
<td align="left"><p><li>Servizi mobili continua ad essere disponibile come servizio autonomo e rimane completamente supportato.</p>
<p><li>App per dispositivi mobili è un tipo di app nel servizio app che integra tutte le funzionalità di Servizi mobili e altre.</p>
<p><li>La <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrazione da Servizi mobili ad App per dispositivi mobili</a> è molto semplice.</p>
<p><li>Come parte del servizio app, App per dispositivi mobili offre nuove funzionalità oltre a quelle di Servizi mobili, come l'integrazione con sistemi locali e SaaS, slot di gestione temporanea, Processi Web, opzioni di scalabilità migliorate e altro ancora.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Altre informazioni sulle App per dispositivi mobili</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">App per le API</td>
<td align="left">
<p><li>App per le API è un nuovo tipo di app nel servizio app, che consente di creare e usare API nel cloud con estrema facilità.</p>
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
<li><p>Servizi BizTalk continua a essere disponibile come servizio autonomo e rimane completamente supportato.</p>
<li><p>Tutte le funzionalità di Servizi BizTalk sono integrate nel servizio app come app per le API, consentendo agli utenti di eseguire l'integrazione di applicazioni aziendali e di scenari B2B con qualsiasi tipo di app del servizio app.</p>
<li><p>Con App per la logica è ora possibile automatizzare i processi aziendali usando un'esperienza di progettazione visiva per la creazione di flussi di lavoro.</p></td>
</tr>
</tbody>
</table>

Per altre informazioni, vedere la [documentazione relativa al servizio app](https://azure.microsoft.com/documentation/services/app-service/).

