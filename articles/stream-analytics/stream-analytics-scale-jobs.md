---
title: "velocità effettiva tooincrease i processi di flusso Analitica aaaScale | Documenti Microsoft"
description: "Informazioni su come i processi di flusso Analitica tooscale per la configurazione delle partizioni di input, l'ottimizzazione di definizione della query hello e impostazione processo unità di streaming."
keywords: flusso di dati, elaborazione del flusso di dati, ottimizzare analisi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Velocità effettiva di elaborazione dei dati di scala Analitica di flusso di Azure processi tooincrease flusso
In questo articolo viene illustrato come eseguire una query tooincrease velocità effettiva per i processi di Streaming Analitica tootune Analitica un flusso. Si apprenderà come tooscale Analitica di flusso dei processi tramite la configurazione di input di partizioni, definizione di query di ottimizzazione analitica hello e processo di calcolo e l'impostazione *unità di streaming* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Quali sono le parti di un processo di flusso Analitica hello?
Una definizione del processo di Analisi di flusso include input, query e output. Gli input sono in cui il processo di hello legge il flusso di dati hello da. query Hello è usato tootransform hello dati flusso di input e output di hello è quale processo hello invia i risultati del processo hello per.  

Un processo richiede almeno un'origine di input per il flusso dei dati. Hello origine di input flusso di dati può essere archiviati in un hub di eventi di Azure o nell'archiviazione blob di Azure. Per ulteriori informazioni, vedere [tooAzure introduzione Analitica flusso](stream-analytics-introduction.md) e [iniziare a usare Azure flusso Analitica](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partizioni negli hub eventi e nell'archiviazione di Azure
Ridimensionamento di un processo di flusso Analitica si avvale di partizioni hello input o output. Il partizionamento consente di suddividere i dati in subset in base a una chiave di partizione. Un processo che utilizza dati hello (ad esempio, un processo di Streaming Analitica) può utilizzare e scrivere le varie partizioni in parallelo, con conseguente aumento della velocità effettiva. Quando si usa Analisi di flusso, è possibile sfruttare il partizionamento negli hub eventi e nell'archiviazione BLOB. 

Per ulteriori informazioni sulle partizioni, vedere hello seguenti articoli:

* [Panoramica delle funzionalità di Hub eventi](../event-hubs/event-hubs-features.md#partitions)
* [Partizionamento dei dati](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Unità di streaming
Unità (SUs) rappresentano hello risorse di flusso e di elaborazione necessarie in ordine tooexecute un processo Analitica di flusso di Azure. SUs forniscono un modo toodescribe hello relativo evento basata su una misura combinata di CPU, memoria, capacità di elaborazione, leggere e scrivere tariffe. Ogni SU corrisponde tooroughly 1 MB al secondo di velocità effettiva. 

Scelta di SUs quanti sono necessari per un determinato processo dipende dalla configurazione della partizione per gli input hello hello e hello query definita per il processo di hello. È possibile selezionare le quote tooyour in SUs per un processo. Per impostazione predefinita, ogni sottoscrizione di Azure prevede una quota di backup SUs too50 per tutti i processi di hello analitica in un'area specifica. tooincrease SUs per le sottoscrizioni oltre questa quota, contattare [supporto Microsoft](http://support.microsoft.com). I valori validi di unità di streaming per processo sono 1, 3, 6 e poi a salire, con incrementi di 6.

## <a name="embarrassingly-parallel-jobs"></a>Processi perfettamente paralleli
Un *imbarazzantemente parallele* processo è uno scenario di hello più scalabile in Azure flusso Analitica è disponibile. Si connette una partizione di istanza di input tooone hello della partizione di tooone hello query di output di hello. Il parallelismo è hello seguenti requisiti:

1. Se la logica di query dipende dalla stessa chiave in fase di elaborazione hello da hello stessa istanza di query, è necessario assicurarsi che gli eventi di hello vanno toohello stessa partizione dell'input. Per gli hub di eventi, ciò significa che i dati di evento hello devono disporre di hello **PartitionKey** valore impostato. In alternativa, è possibile usare mittenti partizionati. Per l'archiviazione blob, ciò significa che gli eventi di hello vengono inviati toohello stessa cartella della partizione. Se la logica di query non richiede la stessa chiave toobe elaborati hello da hello stessa istanza di query, è possibile ignorare questo requisito. Un esempio di questa logica è offerto da una query semplice select-project-filter.  

2. Una volta dati hello sono disposto sul lato di input hello, è necessario assicurarsi che la query è partizionata. Questa operazione richiede il toouse **Partition By** in tutte le fasi di hello. Sono consentiti più passaggi, ma essi devono essere partizionati da hello stessa chiave. Attualmente, hello chiave di partizionamento deve essere impostato troppo**PartitionId** affinché hello processo toobe completamente parallelo.  

3. Solo gli hub eventi e l'archiviazione BLOB supportano attualmente l'output partizionato. Per l'output di hub eventi, è necessario configurare toobe chiave di partizione hello **PartitionId**. Per l'output di archiviazione blob, non è necessario toodo nulla.  

4. numero di Hello di partizioni di input deve essere uguale hello numero di partizioni di output. L'output dell'archiviazione BLOB attualmente non supporta le partizioni, Ma che non costituisce un problema, perché eredita hello schema della query a monte hello di partizionamento. Ecco alcuni esempi di valori di partizioni che consentono un processo perfettamente parallelo:  

   * 8 partizioni di input di hub eventi e 8 partizioni di output di hub eventi
   * 8 partizioni di input di hub eventi e output di archiviazione BLOB  
   * 8 partizioni di input di archiviazione BLOB e output di archiviazione BLOB  
   * 8 partizioni di input di archiviazione BLOB e 8 partizioni di output di hub eventi  

Hello nelle sezioni seguenti vengono illustrano alcuni scenari di esempio imbarazzantemente parallele.

### <a name="simple-query"></a>Query semplice

* Input: hub eventi con 8 partizioni
* Output: hub eventi con 8 partizioni

Query:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Questa query è un filtro semplice. Pertanto, non è necessario tooworry sul partizionamento input hello inviato toohello hub di eventi. Sono incluse query hello **partizione da PartitionId**, in modo che soddisfi i requisiti #2 precedenti. Per l'output di hello, dobbiamo output di hub di eventi tooconfigure hello in hello processo toohave hello partizione set di chiavi troppo**PartitionId**. Ultimo uno controllo è toomake assicurarsi che il numero di hello delle partizioni di input sia uguale toohello numero di partizioni di output.

### <a name="query-with-a-grouping-key"></a>Query con chiave di raggruppamento

* Input: hub eventi con 8 partizioni
* Output: archiviazione BLOB

Query:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Questa query include una chiave di raggruppamento. Pertanto, hello stesso toobe esigenze chiave elaborati dalla stessa query di istanza, il che significa che gli eventi devono essere inviati toohello hub di eventi in modo partizionato hello. Ma quale chiave è necessario usare? **PartitionId** corrisponde a un concetto della logica di processo. chiave Hello interessante effettivamente **TollBoothId**, pertanto hello **PartitionKey** valore dei dati di evento hello deve essere **TollBoothId**. Prepariamo queste query hello impostando **Partition By** troppo**PartitionId**. Poiché l'output di hello nell'archiviazione blob, non è necessario tooworry sulla configurazione di un valore di chiave di partizione, in base ai requisiti #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Query a più passaggi con chiave di raggruppamento
* Input: hub eventi con 8 partizioni
* Output: istanza di hub eventi con 8 partizioni

Query:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

La query contiene una chiave di raggruppamento, pertanto hello stesso toobe esigenze chiave elaborata hello stessa istanza di query. È possibile utilizzare hello stessa strategia esempio hello precedente. In questo caso, query hello prevede diversi passaggi. Per ogni passaggio è presente la clausola **Partition By PartitionID**? Sì, in modo da query hello soddisfa requisito #3. Per l'output di hello, dobbiamo chiave di partizione hello tooset troppo**PartitionId**, come descritto in precedenza. È inoltre possibile notare che hello stesso numero di partizioni come input hello.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Esempi di scenari *non* perfettamente paralleli

Nella sezione precedente hello, abbiamo anche mostrato alcuni scenari imbarazzantemente parallele. In questa sezione sono illustrati scenari che non soddisfano tutti hello requisiti toobe imbarazzantemente parallele. 

### <a name="mismatched-partition-count"></a>Numero di partizioni non corrispondente
* Input: hub eventi con 8 partizioni
* Output: hub eventi con 32 partizioni

In questo caso, non è importante è la query che hello. Se il numero di partizioni di input di hello non corrisponde a numero di partizioni di output di hello, non è una topologia hello imbarazzantemente parallela.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Uso di un output diverso da hub eventi o archiviazione BLOB
* Input: hub eventi con 8 partizioni
* Output: Power BI

L'output Power BI attualmente non supporta il partizionamento. Pertanto, questo scenario non è perfettamente parallelo.

### <a name="multi-step-query-with-different-partition-by-values"></a>Query a più passaggi con valori diversi per Partition By
* Input: hub eventi con 8 partizioni
* Output: hub eventi con 8 partizioni

Query:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Come si può notare, secondo passaggio hello Usa **TollBoothId** come chiave di partizionamento hello. Questo passaggio è non hello stesso come primo passaggio hello e pertanto richiede ci toodo una casuale. 

Hello esempi precedenti alcuni processi di flusso Analitica conformi troppo (o non) una topologia imbarazzantemente parallela. Se devono essere conformi, hanno potenziale hello per la massima scalabilità. Per i processi che non rientrano in nessuno di questi profili, in futuro saranno disponibili aggiornamenti con le linee guida per il ridimensionamento. Per il momento, utilizzare indicazioni generali hello hello le sezioni seguenti.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Unità di streaming massimo hello di un processo di calcolo
numero totale di Hello di unità di streaming che può essere utilizzato da un processo di flusso Analitica dipende dal numero di hello dei passaggi in query hello è definito per il processo di hello e numero di hello di partizioni per ogni passaggio.

### <a name="steps-in-a-query"></a>Passaggi in una query
Una query può includere uno o più passaggi. Ogni passaggio è una sottoquery definita da hello **WITH** (parola chiave). query di Hello di fuori di hello **WITH** (parola chiave) (solo per una query) è anch'essa conteggiata come un passaggio, ad esempio hello **selezionare** istruzione hello seguente query:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Questa query include due passaggi.

> [!NOTE]
> Questa query viene illustrata in dettaglio più avanti in articolo hello.
>  

### <a name="partition-a-step"></a>Partizionamento di un passaggio
Partizionamento di un passaggio necessario hello seguenti condizioni:

* origine di input Hello deve essere partizionato. 
* Hello **selezionare** istruzione di query hello deve leggere da un'origine di input partizionata.
* query di Hello all'interno di passaggio hello deve avere hello **Partition By** (parola chiave).

Quando una query è partizionata, gli eventi di input hello sono partizione separata elaborati e aggregati in gruppi e gli eventi di output vengono generati per ognuno dei gruppi di hello. Se si desidera una funzione di aggregazione combinato, è necessario creare un secondo tooaggregate passaggio non partizionata.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Calcolare il numero massimo hello unità per un processo di streaming
Tutti i passaggi non partizionata insieme possono scalare in verticale toosix unità (SUs) per un processo di flusso Analitica di streaming. SUs tooadd, un passaggio devono essere partizionati. Ogni partizione può includere sei unità di streaming.

<table border="1">
<tr><th>Query</th><th>SUs Max per processo hello</th></td>

<tr><td>
<ul>
<li>query Hello contiene un unico passaggio.</li>
<li>passaggio di Hello non è partizionata.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flusso di dati di input Hello viene partizionata in base a 3.</li>
<li>query Hello contiene un unico passaggio.</li>
<li>passaggio di Hello è partizionata.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>query Hello contiene due passi.</li>
<li>Nessuno dei passaggi di hello è partizionata.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flusso di dati di input Hello viene partizionata in base a 3.</li>
<li>query Hello contiene due passi. passaggio di input Hello è partizionata e secondo passaggio hello non lo è.</li>
<li>Hello <strong>selezionare</strong> istruzione legge da un input hello partizionata.</li>
</ul>
</td>
<td>24 (18 per i passaggi partizionati + 6 per i passaggi non partizionati)</td></tr>
</table>

### <a name="examples-of-scaling"></a>Esempi di ridimensionamento

Hello nella query seguente calcola il numero di hello di automobili in una finestra di tre minuti passando un casello con tre tollbooths. Questa query può essere ridimensionato verso l'alto toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

toouse più SUs per hello query, entrambi hello flusso dati di input e query hello devono essere partizionati. Poiché la partizione di flusso di dati hello è impostata too3, hello query modificata seguente può essere ridimensionato verso l'alto too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Quando una query è partizionata, gli eventi di input hello vengono elaborati e aggregati in gruppi di una partizione separata. Gli eventi di output vengono inoltre generati per ognuno dei gruppi di hello. Partizionamento può causare alcuni risultati imprevisti quando hello **GROUP BY** campo non è una chiave di partizione hello nel flusso di dati di input hello. Ad esempio, hello **TollBoothId** campo nella query precedente hello non è una chiave di partizione hello di **Input1**. il risultato di Hello è tale hello dati da casello #1 possono essere distribuiti in più partizioni.

Ognuno di hello **Input1** partizioni saranno elaborate separatamente dal flusso Analitica. Di conseguenza, più record del numero di automobili hello per hello stesso casello in hello stessa finestra a cascata verrà creato. Se non è possibile modificare la chiave di partizione input hello, questo problema può essere risolto aggiungendo un passaggio non partizione, come in hello di esempio seguente:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Questa query può essere scalato too24 SUs.

> [!NOTE]
> Se si siano unendo in join due flussi, assicurarsi che i flussi di hello vengono partizionati dalla chiave di partizione hello della colonna hello utilizzare toocreate hello join. Assicurarsi inoltre di aver hello stesso numero di partizioni in entrambi i flussi.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Configurare le unità di streaming di Analisi di flusso

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nell'elenco di hello delle risorse, trovare il processo di flusso Analitica di hello tooscale desiderati e quindi aprirlo.
3. In hello processo pannello in **configura**, fare clic su **scala**.

    ![Configurazione del processo di Analisi di flusso nel portale di Azure][img.stream.analytics.preview.portal.settings.scale]

4. Utilizzare hello dispositivo di scorrimento tooset hello SUs per processo hello. Si noti che le impostazioni SU toospecific limitato.


## <a name="monitor-job-performance"></a>Monitorare le prestazioni del processo
Utilizza hello portale di Azure, è possibile tenere traccia della velocità effettiva hello di un processo:

![Processi di monitoraggio di Analisi dei flussi di Azure][img.stream.analytics.monitor.job]

Calcolare la velocità effettiva hello previsto del carico di lavoro hello. Se la velocità effettiva hello è inferiore al previsto, ottimizzare partizione input hello, ottimizzare la query hello e aggiungere SUs tooyour processo.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Visualizzare la velocità effettiva Analitica flusso a livello di scalabilità: scenario Pi Raspberry hello
toohelp che è comprendere le modalità di scalabilità dei processi di flusso Analitica, è stata eseguita un esperimento in base all'input da un dispositivo Raspberry Pi. Questo esperimento farci vedere hello effetto sulla velocità effettiva di più unità di streaming e partizioni.

In questo scenario, il dispositivo hello invia hub di eventi tooan sensore dati (client). Streaming Analitica elabora dati hello e invia un avviso o nelle statistiche come un hub di eventi di output tooanother. 

client Hello invia i dati del sensore in formato JSON. anche l'output di Hello dati è in formato JSON. dati Hello sono simile al seguente:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Hello seguente query è toosend usato un avviso quando una luce è disattivata:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Misurare la velocità effettiva

In questo contesto, velocità effettiva è quantità hello dei dati di input elaborati dal flusso Analitica in un periodo di tempo stabilito. (È misurato per 10 minuti). dati di input tooachieve hello migliore elaborazione velocità effettiva per hello, sia i dati hello flusso di input e sono stati partizionati query hello. Sono inclusi **Count ()** in hello query toomeasure sono stati elaborati come molti eventi di input. processo hello che toomake non semplicemente attendendo toocome gli eventi di input, ogni partizione dell'hub di eventi di input hello è stato precaricato con circa 300 MB di dati di input.

Hello nella tabella seguente sono illustrati i risultati di hello che è stato illustrato quando è stato aumentato il numero di hello di unità di streaming e partizione corrispondente hello conteggi nell'hub eventi.  

<table border="1">
<tr><th>Partizioni di input</th><th>Partizioni di output</th><th>Unità di streaming</th><th>Velocità effettiva sostenuta
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4,06 MB/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8,06 MB/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38,32 MB/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172,67 MB/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454,27 MB/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609,69 MB/s</td>
</tr>
</table>

E hello grafico seguente viene illustrata una visualizzazione della relazione hello tra SUs e la velocità effettiva.

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

