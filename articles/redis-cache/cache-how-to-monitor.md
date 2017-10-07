---
title: aaaHow toomonitor Cache Redis di Azure | Documenti Microsoft
description: "Informazioni su come toomonitor hello integrità e le prestazioni le istanze di Cache Redis di Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>La modalità di Cache Redis di Azure di toomonitor
Cache Redis di Azure Usa [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide diverse opzioni per il monitoraggio delle istanze di cache. È possibile visualizzare le metriche, aggiungere metriche grafici toohello schermata iniziale, personalizzare l'intervallo di data e ora hello di grafici di monitoraggio, aggiungere e rimuovere metriche dai grafici hello e impostare gli avvisi quando vengono soddisfatte determinate condizioni. Questi strumenti consentono di toomonitor hello integrità delle istanze di Cache Redis di Azure e consentono di gestire le applicazioni di memorizzazione nella cache.

Le metriche per le istanze di Cache Redis di Azure vengono raccolti tramite hello Redis [INFO](http://redis.io/commands/info) comando circa due volte al minuto e archiviati automaticamente per 30 giorni (vedere [esportare le metriche di cache](#export-cache-metrics) tooconfigure un criteri di conservazione diversi) pertanto possono essere visualizzati nei grafici di metriche hello e valutati per le regole di avviso. Per ulteriori informazioni sui valori INFO diversi hello usati per ogni metrica della cache, vedere [disponibili metriche e intervalli di reporting](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

le metriche di cache, tooview [Sfoglia](cache-configure.md#configure-redis-cache-settings) tooyour istanza di cache di hello [portale di Azure](https://portal.azure.com).  Cache Redis di Azure fornisce alcuni grafici incorporati su hello **Panoramica** blade e hello **Redis metriche** blade. Ogni grafico può essere personalizzato aggiungendo o rimuovendo metriche e la modifica di hello intervallo di reporting.

![Metriche Redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Visualizzare i grafici preconfigurati relativi alle metriche

Hello **Panoramica** pannello è hello seguenti grafici di monitoraggio configurati in precedenza.

* [Grafici di monitoraggio](#monitoring-charts)
* [Grafici di utilizzo](#usage-charts)

### <a name="monitoring-charts"></a>Grafici di monitoraggio
Hello **monitoraggio** sezione hello **Panoramica** pannello è **riscontri e mancati riscontri**, **Ottiene e imposta**, **connessioni**, e **comandi totali** grafici.

![Grafici di monitoraggio](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Grafici di utilizzo
Hello **utilizzo** sezione hello **Panoramica** pannello è **carico del Server Redis**, **utilizzo della memoria**, **larghezza di banda di rete** , e **l'utilizzo della CPU** grafici e visualizza anche hello **tariffario** per l'istanza di cache di hello.

![Grafici di utilizzo](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Hello **tariffario** prezzi di cache di hello Visualizza livello, quindi è possibile utilizzare anche[scala](cache-how-to-scale.md) hello tooa cache diverso livello di prezzo.

## <a name="view-metrics-with-azure-monitor"></a>Visualizzare le metriche con Monitoraggio di Azure
tooview Redis metriche e creare grafici personalizzati tramite Monitor di Azure, fare clic su **metriche** da hello **menu Resource**e personalizzare il grafico utilizzando la metrica di hello desiderato, intervallo, il tipo di grafico di reporting e altre.

![Metriche Redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Per altre informazioni sull'uso delle metriche con Monitoraggio di Azure, vedere [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Esportare le metriche della cache
Per impostazione predefinita, le metriche relative alla cache in Monitoraggio di Azure vengono [archiviate per 30 giorni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e quindi vengono eliminate. toopersist le metriche di cache per più di 30 giorni, è possibile [designare un account di archiviazione](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) e specificare un **conservazione (giorni)** criteri per le metriche della cache. 

tooconfigure un account di archiviazione per le metriche della cache:

1. Fare clic su **diagnostica** da hello **menu Resource** in hello **Cache Redis** blade.
2. Fare clic su **Sì**.
3. Controllare **archiviare l'account di archiviazione tooa**.
4. Selezionare l'account di archiviazione hello in cui le metriche della cache di hello toostore.
5. Controllare hello **1 minuto** casella di controllo e specificare un **conservazione (giorni)** criteri. Se non si desidera tooapply eventuali criteri di conservazione e mantenere sempre i dati, impostare **conservazione (giorni)** troppo**0**.
6. Fare clic su **Salva**.

![Diagnostica di Redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>In aggiunta tooarchiving toostorage le metriche di cache, è anche possibile [trasmessi tooan hub di eventi o inviare loro tooLog Analitica](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess le metriche, è possibile visualizzarli nel portale di Azure come descritto in precedenza in questo articolo hello ed è anche possibile accedervi utilizzando hello [API REST di metriche di monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Se si modificano l'account di archiviazione, dati hello nell'account di archiviazione hello configurato in precedenza rimangono disponibili per il download, ma che non è visualizzata nel portale di Azure hello.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Metriche disponibili e intervalli di report
Le metriche della cache vengono segnalate usando diversi intervalli di report, tra cui **Ultima ora**, **Oggi**, **Ultima settimana** e **Personalizza**. Hello **metrica** pannello per ogni grafico delle metriche Visualizza i valori medio, minimo e massimo hello per ogni metrica grafico hello e alcune metriche viene mostrato un totale per l'intervallo di reporting hello. 

In ogni metrica sono incluse due versioni. Misure di una metrica delle prestazioni per l'intera cache di hello e per le cache che usano [clustering](cache-how-to-premium-clustering.md), una seconda versione di metrica hello che include `(Shard 0-9)` hello Nome misure delle prestazioni per una singola partizione in una cache. Se ad esempio una cache è 4 partizioni, `Cache Hits` hello quantità totale di riscontri per l'intera cache hello, e `Cache Hits (Shard 3)` è semplicemente i riscontri hello per tale partizionamento della cache di hello.

> [!NOTE]
> Anche quando la cache di hello è inattiva e non le applicazioni client attive connesse, è possibile visualizzare alcune attività di cache, ad esempio, i client connessi, utilizzo della memoria e le operazioni eseguite. Questa attività è normale durante l'operazione di hello di un'istanza di Cache Redis di Azure.
> 
> 

| Metrica | Descrizione |
| --- | --- |
| Riscontri cache |numero di Hello di ricerche chiave riuscite durante l'intervallo di reporting specificato hello. Esegue il mapping troppo`keyspace_hits` da hello Redis [INFO](http://redis.io/commands/info) comando. |
| Mancati riscontri nella cache |numero di Hello di ricerche chiave non riuscite durante l'intervallo di reporting specificato hello. Esegue il mapping troppo`keyspace_misses` dal comando Redis INFO hello. Mancati riscontri nella cache non indicano necessariamente che un problema con la cache di hello. Ad esempio, quando si utilizza hello modello di programmazione cache-aside, un'applicazione prima Cerca nella cache di hello per un elemento. Se hello elemento non è presente (mancato riscontro nella cache), elemento hello viene recuperato dal database hello e aggiunto toohello cache per la volta successiva. Mancati riscontri nella cache sono un comportamento normale per modello di programmazione cache-aside hello. Se il numero di mancati riscontri nella cache di hello è supera al previsto, esaminare la logica dell'applicazione hello che popola e letture dalla cache di hello. Se la rimozione di elementi dalla cache di hello a causa di pressione toomemory quindi potrebbero essere presenti alcuni mancati riscontri nella cache, ma un migliore toomonitor metrica per l'utilizzo della memoria sarebbe `Used Memory` o `Evicted Keys`. |
| Client connessi |numero di Hello della cache di toohello le connessioni client durante l'intervallo di reporting specificato hello. Esegue il mapping troppo`connected_clients` dal comando Redis INFO hello. Una volta hello [limite di connessioni](cache-configure.md#default-redis-server-configuration) viene raggiunto successivi tentativi di connessione della cache toohello avrà esito negativo. Si noti che anche se sono non presenti applicazioni nessun client attive, si possono comunque essere presenti alcune istanze di client connessi a causa di connessioni e processi toointernal. |
| Chiavi rimosse |numero di elementi rimossi dalla cache di hello durante hello Hello specificato intervallo di reporting toohello scadenza `maxmemory` limite. Esegue il mapping troppo`evicted_keys` dal comando Redis INFO hello. |
| Chiavi scadute |numero di Hello di elementi scaduti dalla cache di hello durante l'intervallo di reporting specificato hello. Questo valore esegue il mapping troppo`expired_keys` dal comando Redis INFO hello. |
| Totale chiavi  | numero massimo di Hello di chiavi nella cache di hello durante hello oltre il periodo di tempo di reporting. Esegue il mapping troppo`keyspace` dal comando Redis INFO hello. A causa di limitazione tooa di hello sottostante sistema metriche, per la cache con il servizio cluster attivato, Totale chiavi restituisce numero massimo di hello delle chiavi di partizione hello con hello il numero massimo di chiavi durante l'intervallo di reporting hello.  |
| Operazioni Get |numero di Hello di operazioni get dalla cache di hello durante l'intervallo di reporting specificato hello. Questo valore è seguito hello hello somma i valori da hello Redis INFO comando tutto: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, e `cmdstat_getrange`, ed è la somma toohello equivalente di riscontri nella cache e Mancati riscontri durante l'intervallo di reporting hello. |
| Carico server Redis |percentuale di Hello di cicli in cui hello server Redis è impegnato nell'elaborazione e non è in attesa inattiva per i messaggi. Se il contatore raggiunge 100 che indica che il server di Redis hello ha raggiunto un limite massimo delle prestazioni e hello CPU non è in grado di elaborare funzionare uno più velocemente. Se si verifica carico del Server Redis elevato si vedranno le eccezioni di timeout nel client hello. In tal caso, è necessario prendere in considerazione il dimensionamento o il partizionamento dei dati in più cache. |
| Operazioni Set |numero di Hello della cache di toohello set di operazioni durante hello specificato intervallo di reporting. Questo valore è seguito hello hello somma i valori da hello Redis INFO comando tutto: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , e `cmdstat_setnx`. |
| Totale operazioni |numero totale di Hello di comandi elaborati dal server di cache di hello hello specifica l'intervallo di reporting. Questo valore esegue il mapping troppo`total_commands_processed` dal comando Redis INFO hello. Si noti che quando la Cache Redis di Azure vengono utilizzata esclusivamente per pubblicazione/sottoscrizione non vi sarà alcuna metrica per `Cache Hits`, `Cache Misses`, `Gets`, o `Sets`, saranno presenti `Total Operations` metriche che riflettono l'uso della cache di hello per le operazioni di pubblicazione/sottoscrizione. |
| Memoria utilizzata |quantità di Hello di memoria cache usata per le coppie chiave/valore nella cache di hello in MB durante hello specificato intervallo di reporting. Questo valore esegue il mapping troppo`used_memory` dal comando Redis INFO hello. Non include i metadati o la frammentazione. |
| Memoria utilizzata RSS |Hello memoria cache utilizzata in MB hello reporting intervallo specificato, inclusi la frammentazione e metadati. Questo valore esegue il mapping troppo`used_memory_rss` dal comando Redis INFO hello. |
| CPU |utilizzo della CPU del server di Cache Redis di Azure hello come percentuale durante hello Hello specificato intervallo di reporting. Questo valore viene eseguito il mapping del sistema operativo toohello `\Processor(_Total)\% Processor Time` contatore delle prestazioni. |
| Lettura da cache |quantità di Hello dei dati letti dalla cache di hello in megabyte al secondo (MB/s) durante hello specificato intervallo di reporting. Questo valore è derivato da hello schede di rete che supportano la macchina virtuale hello che ospita la cache di hello ed è non Redis specifico. **Questo valore corrisponde toohello larghezza di banda utilizzata da questa cache. Se si desidera tooset di avvisi per i limiti della larghezza di banda di rete sul lato server, quindi creare utilizzando questo `Cache Read` contatore. Vedere [questa tabella](cache-faq.md#cache-performance) per hello osservato i limiti di larghezza di banda per vari cache prezzi livelli e dimensioni.** |
| Scrittura nella cache |Hello quantità di dati scritti toohello cache in megabyte al secondo (MB/s) durante l'intervallo di reporting specificato hello. Questo valore è derivato da hello schede di rete che supportano la macchina virtuale hello che ospita la cache di hello ed è non Redis specifico. Questo valore corrisponde toohello larghezza di banda di dati inviati toohello cache dal client hello. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Avvisi
È possibile configurare avvisi tooreceive in base alle metriche e attività di log. Monitoraggio di Azure consente tooconfigure un avviso toodo hello seguenti attiva:

* Inviare una notifica via posta elettronica
* Chiamare un webhook
* Richiamare un'app per la logica di Azure

le regole di avviso tooconfigure per la cache, fare clic su **regole di avviso** da hello **menu risorse**.

![Monitoraggio](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Per altre informazioni sulla configurazione e sull'uso degli avvisi, vedere [Panoramica degli avvisi](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Log attività
Log attività forniscono informazioni sulle operazioni hello eseguite sulle istanze Cache Redis di Azure. In precedenza erano noti come "log di controllo" o "log operativi". Utilizzo di log di attività, è possibile determinare hello "cosa, chi e quando" per le operazioni (PUT, POST, DELETE) eseguite sulle istanze Cache Redis di Azure di scrittura. 

> [!NOTE]
> I log attività non includono le operazioni di lettura (GET).
>
>

log attività tooview per la cache, fare clic su **log attività** da hello **menu risorse**.

Per ulteriori informazioni sui log di attività, vedere [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











