---
title: "aaaWhat è Analitica di Log in Operations Management Suite (OMS)? | Microsoft Docs"
description: "Log Analytics è un servizio di Operations Management Suite (OMS) che consente di raccogliere e analizzare i dati operativi generati dalle risorse nel cloud e nell'ambiente locale.  Questo articolo fornisce una breve panoramica dei diversi componenti di hello di Log Analitica e contenuto toodetailed collegamenti."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Cos'è Log Analytics?
Log Analitica è un servizio in [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) che monitora il toomaintain ambienti cloud e locali loro disponibilità e prestazioni.  Vengono raccolti i dati generati dalle risorse negli ambienti di cloud e locali e da altre analisi di tooprovide strumenti monitoraggio in più origini.  Questo articolo fornisce una breve descrizione del valore di hello che Log Analitica, una panoramica di come funziona, e i collegamenti toomore dettagliati contenuto in modo è possibile esaminare ulteriormente.

## <a name="is-log-analytics-for-you"></a>Log Analytics è la scelta giusta?
Se l'ambiente Azure non è attualmente monitorato, è consigliabile iniziare con [Monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview.md), che raccoglie e analizza i dati di monitoraggio per le risorse di Azure.  Log Analitica può [raccogliere i dati da Azure monitoraggio](log-analytics-azure-storage.md) toocorrelate con altri dati e fornire un'ulteriore analisi.

Se si desidera toomonitor l'ambiente locale o si dispone di monitoraggio esistente mediante i servizi, ad esempio monitoraggio di Azure o System Center Operations Manager, quindi Log Analitica possibile aggiungere un valore significativo.  Può raccogliere dati direttamente dagli agenti e da altri strumenti in un unico archivio.  Gli strumenti di analisi in Log Analytics, come le ricerche nei log, le visualizzazioni e le soluzioni, vengono applicati a tutti i dati raccolti per offrire un'analisi centralizzata dell'intero ambiente.


## <a name="using-log-analytics"></a>Uso di Log Analytics
È possibile accedere Analitica Log tramite il portale di OMS hello o hello portale di Azure che vengono eseguite in qualsiasi browser e fornire con le impostazioni di accesso tooconfiguration di più strumenti tooanalyze e agire sui dati raccolti.  Dal portale hello è possibile sfruttare [log ricerche](log-analytics-log-searches.md) in cui si creano query tooanalyze raccolti dati, [dashboard](log-analytics-dashboards.md) che è possibile personalizzare grafici, le ricerche utili, e [soluzioni](log-analytics-add-solutions.md) che forniscono gli strumenti di analisi e funzionalità aggiuntivi.

immagine di Hello riportata di seguito è dal portale OMS hello dashboard hello in cui viene mostrato che visualizza le informazioni di riepilogo per hello [soluzioni](#add-functionality-with-management-solutions) installate nell'area di lavoro hello.  È possibile fare clic su qualsiasi toodrill riquadro ulteriormente in dati hello per tale soluzione.

![Portale OMS](media/log-analytics-overview/portal.png)

Log Analitica include un recupero tooquickly linguaggio di query e consolida i dati nel repository di hello.  È possibile creare e salvare [ricerche nei Log](log-analytics-log-searches.md) toodirectly analizzare i dati nel portale di hello o ricerche nei log eseguiti automaticamente toocreate un avviso se i risultati hello di query di hello indicano una condizione di importanti.

![Ricerca log](media/log-analytics-overview/log-search.png)

tooget una visualizzazione grafica rapida dell'integrità hello dell'ambiente globale, è possibile aggiungere visualizzazioni per tooyour ricerche log salvate [dashboard](log-analytics-dashboards.md).   

![Dashboard](media/log-analytics-overview/dashboard.png)

Dati tooanalyze degli ordini di fuori di Log Analitica, è possibile esportare dati hello dal repository OMS hello in strumenti, ad esempio [Power BI](log-analytics-powerbi.md) o Excel.  È anche possibile sfruttare hello [API di ricerca Log](log-analytics-log-search-api.md) toobuild le soluzioni personalizzate che sfruttano i dati di Log Analitica o toointegrate con altri sistemi.

## <a name="add-functionality-with-management-solutions"></a>Aggiungere funzionalità con soluzioni di gestione
[Soluzioni di gestione](log-analytics-add-solutions.md) aggiungere funzionalità tooOMS, che forniscono dati aggiuntivi e strumenti di analisi tooLog Analitica.  Possono anche definire raccolti nuovo toobe tipi di record che può essere analizzati con ricerche nei Log o tramite l'interfaccia utente aggiuntive fornite dalla soluzione hello nel dashboard di hello.  immagine di esempio Hello riportata di seguito viene illustrato hello [soluzione Change Tracking](log-analytics-change-tracking.md)

![Soluzione di Rilevamento modifiche](media/log-analytics-overview/change-tracking.png)

Sono disponibili soluzioni per numerose funzioni e vengono aggiunte continuamente altre soluzioni.  È possibile esplorare con facilità le soluzioni disponibili e [aggiungerli come area di lavoro OMS tooyour](log-analytics-add-solutions.md) dalla raccolta di soluzioni hello o da Azure Marketplace.  Molte vengono distribuite automaticamente e iniziano a funzionare immediatamente, mentre altre possono richiedere qualche attività di configurazione.

![Raccolta soluzioni](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Componenti di Log Analytics
Centro di Log Analitica hello è repository OMS hello che è ospitato in hello cloud di Azure.  Raccolta dei dati nel repository di hello dai origini connesse, la configurazione delle origini dati e Aggiunta sottoscrizione tooyour di soluzioni.  Origini dati e soluzioni ogni creare tipi di record diversi possono ancora essere analizzati insieme nel repository di query toohello ma il proprio set di proprietà.  In questo modo hello toouse stesso toowork strumenti e i metodi con diversi tipi di dati raccolti da diverse origini.

![Repository OMS](media/log-analytics-overview/overview.png)

Origini collegate sono computer hello e altre risorse che generano dati raccolti da Log Analitica.  Sono inclusi gli agenti installati nei computer [Windows](log-analytics-windows-agents.md) e [Linux](log-analytics-linux-agents.md) che si connettono direttamente o gli agenti in un [gruppo di gestione di System Center Operations Manager connesso](log-analytics-om-agents.md).  Per le risorse di Azure, Log Analytics raccoglie dati da [Monitoraggio di Azure e Diagnostica di Azure](log-analytics-azure-storage.md).

[Origini dati](log-analytics-data-sources.md) sono hello diversi tipi di dati raccolti da ogni origine connessa.  Sono inclusi [eventi](log-analytics-data-sources-windows-events.md) e [dati sulle prestazioni](log-analytics-data-sources-performance-counters.md) da [Windows](log-analytics-data-sources-windows-events.md) e gli agenti Linux in toosources aggiunta, ad esempio [registri IIS](log-analytics-data-sources-iis-logs.md)e [registri di testo personalizzato](log-analytics-data-sources-custom-logs.md).  Configurare ogni origine dati che si desidera toocollect e configurazione di hello è origine connessa tooeach recapitato automaticamente.

Se si dispone di requisiti personalizzati, è quindi possibile utilizzare hello [API dell'agente di raccolta dati di HTTP](log-analytics-data-collector-api.md) toowrite repository toohello dei dati da un client di API REST.

## <a name="log-analytics-architecture"></a>Architettura di Log Analytics
requisiti di distribuzione Hello di Log Analitica sono minimi, poiché componenti centrali hello ospitati nel cloud di Azure hello.  Questo include hello in servizi di toohello aggiunta che consentono di toocorrelate e analizzare i dati raccolti.  portale Hello è accessibile da qualsiasi browser, pertanto non c'è Nessun requisito per il software client.

È necessario installare gli agenti nei computer [Windows](log-analytics-windows-agents.md) e [Linux](log-analytics-linux-agents.md), ma non sono richiesti agenti aggiuntivi per i computer che fanno già parte di un [gruppo di gestione SCOM connesso](log-analytics-om-agents.md).  Agenti SCOM continuerà toocommunicate con i server di gestione che inoltra i relativi tooLog dati Analitica.  Alcune soluzioni, tuttavia, saranno necessario toocommunicate agenti direttamente con Log Analitica.  documentazione di Hello per ogni soluzione verrà specificati i requisiti di comunicazione.

Quando ci si [iscrive a Log Analytics](log-analytics-get-started.md), verrà creata un'area di lavoro OMS.  È possibile considerare dell'area di lavoro hello come un ambiente Analitica Log univoco con il proprio archivio dati, origini dati e soluzioni. È possibile creare più aree di lavoro in toosupport la sottoscrizione più ambienti, ad esempio produzione e di test.

![Architettura di Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Passaggi successivi
* [Iscriversi a un account gratuito di Log Analitica](log-analytics-get-started.md) tootest nel proprio ambiente.
* Hello visualizza diversi [origini dati](log-analytics-data-sources.md) dati toocollect disponibile nel repository OMS hello.
* [Cercare hello soluzioni disponibili in hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità tooLog Analitica.

