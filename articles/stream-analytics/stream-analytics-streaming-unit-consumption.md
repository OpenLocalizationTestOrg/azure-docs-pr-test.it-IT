---
title: "Azure flusso Analitica: Ottimizzare il toouse processo unità di Streaming in modo efficiente | Documenti Microsoft"
description: "Procedure consigliate di query per la scalabilità e le prestazioni in Analisi di flusso di Azure."
keywords: "unità di streaming, prestazioni delle query"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Ottimizzare in modo efficiente il toouse processo unità di Streaming

Azure flusso Analitica aggrega prestazioni hello "peso" dell'esecuzione di un processo in unità di Streaming (SUs). SUs rappresentano hello risorse elaborazione tooexecute utilizzato un processo. SUs forniscono un modo toodescribe hello relativo evento basata su una misura combinata di CPU, memoria, capacità di elaborazione, leggere e scrivere tariffe. Questo consente di capacità di concentrarsi sulla logica della query hello e rimuove la necessità di considerazioni sulle prestazioni di livello archiviazione tooknow, allocare memoria per il processo manualmente e approssimativo toorun core-numero necessario di hello CPU del processo in modo tempestivo.

## <a name="how-many-sus-are-required-for-a-job"></a>Quante unità di streaming sono necessarie per un processo?

Scegliere il numero di hello di SUs necessari per un determinato processo dipende dalla configurazione di partizione hello per input hello e query hello è definito all'interno del processo di hello. Hello **scala** pannello consente hello tooset numeri a destra di SUs. È una procedura consigliata tooallocate SUs più del necessario. il motore di elaborazione Analitica flusso Hello Ottimizza per la latenza e velocità effettiva al costo di hello di allocazione di memoria aggiuntiva.

In generale, consigliata hello è toostart con 6 SUs per le query che non usano *PARTITION BY*. Determinare quindi ideale hello utilizzando un metodo di prove ed errori nel quale si modifica il numero di hello di SUs dopo è passare rappresentativo quantità di dati ed esaminare metrica di utilizzo % SU hello.

Azure Analitica flusso mantiene gli eventi in una finestra denominata hello "Riordina buffer" prima di avviare qualsiasi elaborazione. Gli eventi vengono ordinati nella finestra di riordino hello tempo e operazioni successive vengono eseguite sugli eventi hello temporaneamente ordinato. Riordinare gli eventi da tempo garantisce che l'operatore hello dispone della visibilità in tutti gli eventi di hello in hello stipulata intervallo di tempo. Consente inoltre operatore hello elaborazione necessarie hello e produrre un output. Un effetto collaterale di questo meccanismo è che l'elaborazione viene ritardata per la durata della finestra di riordino hello hello. footprint di memoria Hello del processo di hello (che influisce su consumo SU) è una funzione della dimensione hello di questo numero di finestra e hello riordino degli eventi in esso contenuti.

> [!NOTE]
> Quando il numero di hello di lettori cambia durante gli aggiornamenti di processi, avvisi temporanei vengono scritti tooaudit log. I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Cause comuni di memoria elevata per l'utilizzo elevato delle unità di streaming per i processi in esecuzione

### <a name="high-cardinality-for-group-by"></a>Elevata cardinalità di GROUP BY

utilizzo della memoria per il processo di hello determina la cardinalità Hello di eventi in entrata.

Ad esempio, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello numero associato **cluster** è cardinalità hello di query hello.

toomitigate problemi causati dalla cardinalità elevata, scalabilità query hello aumentando partizioni utilizzando **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

numero di Hello *cluster* è cardinalità hello del gruppo da qui.

Dopo che la query hello è partizionata, viene ripartito su più nodi. Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello. È inoltre consigliabile partizionare le partizioni dell'hub eventi in base all'ID partizione.

### <a name="high-unmatched-event-count-for-join"></a>Elevata quantità di eventi senza corrispondenza per JOIN

numero di Hello di eventi non corrispondenti in un JOIN influisce hello quantità di memoria utilizzata query hello. Ad esempio, eseguire una query che esegue la ricerca toofind hello svariate impressioni ad che genera l'errore clic:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

In questo scenario è possibile che vengano visualizzati molti annunci e siano generati pochi clic. Questo errore richiederebbe hello processo tookeep tutti gli eventi di hello in hello intervallo di tempo. quantità di Hello di memoria utilizzata è di tipo tasso di dimensioni e di eventi finestra toohello proporzionale. 

toomitigate questa situazione, la scalabilità orizzontale query hello aumentando partizioni tramite PARTITION BY. 

Dopo che la query hello è partizionata, viene ripartito su più nodi di elaborazione. Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello.

### <a name="large-number-of-out-of-order-events"></a>Quantità elevata di eventi fuori sequenza 

Un numero elevato di eventi non in ordine all'interno di un intervallo di tempo di grandi dimensioni comporta dimensioni hello di hello "riordinare buffer" toobe più grande. toomitigate questa situazione, query hello scala aumentando partizioni tramite PARTITION BY. Dopo che la query hello è partizionata, viene ripartito su più nodi. Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello. 


## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
