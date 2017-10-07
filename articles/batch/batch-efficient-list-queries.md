---
title: query di elenco efficiente aaaDesign - Azure Batch | Documenti Microsoft
description: "Migliorare le prestazioni filtrando le query quando si chiedono informazioni su risorse di Batch, ad esempio pool, processi, attività e nodi di calcolo."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Creare query in modo efficiente le risorse di Batch toolist

Questo articolo si apprenderà come tooincrease prestazioni dell'applicazione Azure Batch riducendo hello di dati restituiti dal servizio hello quando si eseguono query processi, attività e i nodi di calcolo con hello [.NET per Batch] [ api_net] libreria.

Quasi tutte le applicazioni di Batch necessario tooperform qualche tipo di monitoraggio o un'altra operazione che una query nel servizio Batch hello, spesso a intervalli regolari. Toodetermine, ad esempio, se sono presenti tutte le attività in coda rimanente in un processo, è necessario ottenere dati per ogni attività nel processo di hello. stato di hello toodetermine dei nodi del pool, è necessario ottenere dati in ogni nodo nel pool di hello. Questo articolo viene illustrato come tooexecute ad una query in hello modo più efficiente.

> [!NOTE]
> Hello servizio Batch offre uno speciale supporto API per uno scenario comune di hello del conteggio delle attività in un processo. Anziché utilizzare una query di elenco per questi, è possibile chiamare hello [Ottieni conteggio attività] [ rest_get_task_counts] operazione. Questa operazione restituisce il numero di attività in sospeso, in esecuzione o completate, nonché di quelle riuscite e non riuscite. L'operazione di recupero dei conteggi delle attività è più efficiente di una query di tipo elenco. Per altre informazioni, vedere [Conteggiare le attività per un processo in base allo stato (anteprima)](batch-get-task-counts.md). 
>
> in precedenza 2017-06-01.5.1 Hello operazione Ottieni conteggio attività non è disponibile nelle versioni del servizio Batch. Se si utilizza una versione precedente del servizio di hello, quindi utilizzare un'attività di toocount query di elenco in un processo.
>
> 

## <a name="meet-hello-detaillevel"></a>Soddisfare hello DetailLevel
In un ambiente di produzione dell'applicazione di Batch, hello migliaia possibile numerare entità quali processi, attività e i nodi di calcolo. Quando si richiedono informazioni su queste risorse, una grande quantità di dati deve "attraversare transito hello" da un'applicazione hello Batch servizio tooyour per ogni query. Limitando il numero di hello di elementi e il tipo di informazioni restituite da una query, è possibile aumentare la velocità delle query hello e pertanto hello prestazioni dell'applicazione.

Questo [.NET per Batch] [ api_net] elenchi frammento di codice API *ogni* attività associata a un processo, insieme a *tutti* di proprietà hello di ogni attività:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

È possibile eseguire una query di elenco molto più efficiente, tuttavia, tramite l'applicazione di una query di tooyour "livello di dettaglio". A tale scopo, fornire un [ODATADetailLevel] [ odata] oggetto toohello [JobOperations.ListTasks] [ net_list_tasks] metodo. Questo frammento restituisce solo ID hello, riga di comando e proprietà delle informazioni di nodo di calcolo delle attività completate:

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

In questo scenario di esempio, se sono presenti migliaia di attività nel processo di hello, hello risultati dalla seconda query hello in genere saranno restituite molto più rapidamente rispetto a hello prima. Ulteriori informazioni sull'utilizzo ODATADetailLevel quando si elencano gli elementi con hello API .NET di Batch vengono incluse [sotto](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> È consigliabile si *sempre* specificare un elenco di API .NET ODATADetailLevel tooyour oggetto chiama tooensure della massima efficienza e prestazioni dell'applicazione. Se si specifica un livello di dettaglio, consentono di toolower Batch tempi di risposta del servizio, migliorare l'utilizzo della rete e ridurre l'utilizzo di memoria dalle applicazioni client.
> 
> 

## <a name="filter-select-and-expand"></a>Filtro, selezione ed espansione
Hello [.NET per Batch] [ api_net] e [Batch REST] [ api_rest] API forniscono hello possibilità tooreduce sia il numero di elementi che vengono restituiti in un elenco, hello nonché hello quantità di informazioni restituite per ogni. A questo scopo, specificare stringhe di **filtro**, **selezione** ed **espansione** quando si eseguono query di tipo elenco.

### <a name="filter"></a>Filtro
stringa di filtro Hello è un'espressione che consente di ridurre il numero di hello di elementi restituiti. Ad esempio, elenco solo hello in esecuzione di attività per un processo o elenco solo nodi di calcolo che sono attività toorun pronto.

* stringa di filtro Hello è costituita da una o più espressioni, con un'espressione costituita da un nome di proprietà, un operatore e un valore. proprietà Hello che è possibile specificare sono tooeach specifico tipo di entità che si esegue una query, come gli operatori di hello che sono supportati per ogni proprietà.
* Più espressioni possono essere combinate utilizzando operatori logici hello `and` e `or`.
* In questo esempio filtrare gli elenchi di stringa solo hello in esecuzione "eseguire il rendering" attività: `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Selezionare
Selezionare stringa Hello limita i valori delle proprietà hello restituiti per ogni elemento. Si specifica un elenco di nomi di proprietà e vengono restituiti solo i valori di proprietà per gli elementi di hello nei risultati della query hello.

* stringa selezionare Hello è costituita da un elenco delimitato da virgole di nomi di proprietà. È possibile specificare qualsiasi proprietà hello per il tipo di entità hello che si esegue la query.
* Questa stringa di selezione di esempio specifica che dovranno essere restituiti solo i valori di tre proprietà per ogni attività: `id, state, stateTransitionTime`.

### <a name="expand"></a>Espandere
Hello espandere stringa riduce il numero di hello di chiamate API tooobtain necessarie alcune informazioni. Quando si usa una stringa di espansione, si possono ottenere altre informazioni su ogni elemento con una singola chiamata API. Anziché primo recupero hello elenco di entità, quindi la richiesta di informazioni per ogni elemento nell'elenco di hello è utilizzare una stringa di espansione tooobtain hello stesse informazioni in una singola chiamata API. Meno chiamate API significano prestazioni migliori.

* Stringa selezionare toohello simile, hello espandere i controlli di stringa se determinati dati sono inclusa nei risultati di query di elenco.
* stringa di espandere Hello è supportato solo quando viene utilizzato nell'elenco di processi, le pianificazioni dei processi, attività e i pool. Attualmente supporta solo informazioni statistiche.
* Quando tutte le proprietà e viene specificata alcuna stringa seleziona, hello espandere stringa *deve* essere tooget utilizzate le informazioni statistiche. Se una stringa di selezione è tooobtain usato un subset delle proprietà, quindi `stats` può essere specificato nella stringa selezionare hello e hello espandere stringa non è necessario toobe specificato.
* In questo esempio espandere stringa specifica che devono essere restituite le informazioni statistiche per ogni elemento nell'elenco di hello: `stats`.

> [!NOTE]
> Quando si crea uno qualsiasi dei hello tre tipi di stringa di query (filtrare, selezionare ed espandere), è necessario assicurarsi che i nomi delle proprietà hello e case corrisponde a quello delle controparti elemento API REST. Ad esempio, quando si lavora con hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) (classe), è necessario specificare **stato** anziché **stato**, anche se è di proprietà .NET hello [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Vedere tabelle hello seguenti per i mapping di proprietà tra hello .NET e le API REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Regole per le stringhe di filtro, selezione ed espansione
* I nomi di proprietà nel filtro, selezionare ed espandere le stringhe dovrebbe essere visualizzata come avviene in hello [Batch REST] [ api_rest] API, anche quando si utilizza [.NET per Batch] [ api_net] o uno degli altri SDK di Batch di hello.
* Per tutti i nomi di proprietà viene fatta distinzione tra maiuscole e minuscole, al contrario di quanto avviene per i valori delle proprietà.
* Le stringhe relative a data/ora possono essere indicate in uno dei due formati seguenti e devono essere precedute da `DateTime`.
  
  * Esempio di formato W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Esempio di formato RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Le stringhe booleane sono `true` o `false`.
* Se si specifica una proprietà o un operatore non valido, viene generato un errore `400 (Bad Request)` .

## <a name="efficient-querying-in-batch-net"></a>Esecuzione efficiente di query in Batch .NET
All'interno di hello [.NET per Batch] [ api_net] API, hello [ODATADetailLevel] [ odata] classe viene utilizzata per fornire filtro, selezionare ed espandere le stringhe operazioni toolist. classe ODataDetailLevel Hello ha tre proprietà pubbliche di stringa che può essere specificata nel costruttore hello o impostare direttamente sull'oggetto hello. Oggetto viene quindi passato hello ODataDetailLevel come un parametro toohello varie operazioni di elenco, ad esempio [ListPools][net_list_pools], [ListJobs][net_list_jobs], e [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: limitare il numero di hello di elementi restituiti.
* [ODATADetailLevel][odata].[SelectClause][odata_select]: specifica i valori della proprietà restituiti con ogni elemento.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]: recupera i dati per tutti gli elementi in una singola chiamata all'API anziché con chiamate separate per ogni elemento.

Hello frammento di codice seguente Usa servizio di Batch hello per la query tooefficiently hello API .NET di Batch per le statistiche di un set specifico di pool di hello. In questo scenario, hello Batch utente dispone di pool di test e di produzione. il pool di test hello gli ID sono precedute dal prefisso "test" e il pool di produzione hello gli ID sono precedute dal prefisso "produzione". Nel frammento di codice hello *myBatchClient* è un'istanza di hello inizializzata correttamente [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) classe.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Un'istanza di [ODATADetailLevel] [ odata] che viene configurato con l'istruzione Select e clausole di espansione è anche possibile passare metodi Get tooappropriate, ad esempio [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , quantità di hello toolimit di dati restituiti.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Mapping REST too.NET API batch
I nomi delle proprietà nelle stringhe di filtro, selezione ed espansione *devono* riflettere le rispettive controparti dell'API REST, sia a livello di nome che di lettere maiuscole/minuscole. tabelle di Hello riportate di seguito forniscono i mapping tra hello .NET e relative controparti di API REST.

### <a name="mappings-for-filter-strings"></a>Mapping per le stringhe di filtro
* **Metodi di elenco .NET**: ognuno dei metodi dell'API .NET hello in questa colonna accetta un [ODATADetailLevel] [ odata] oggetto come parametro.
* **Richieste REST di elenco**: API REST di ogni pagina tooin collegato, questa colonna contiene una tabella che specifica le proprietà di hello e le operazioni che sono consentiti in *filtro* stringhe. Questi nomi di proprietà e queste operazioni verranno usati per costruire una stringa [ODATADetailLevel.FilterClause][odata_filter].

| Metodi list .NET | Richieste list REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Elenco dei certificati hello in un account][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Elencare i file hello associati a un'attività][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Elenca stato hello di preparazione del processo hello e attività di processo di rilascio per un processo][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Elencare i processi di hello in un account][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Elenco di file hello in un nodo][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Elencare le attività di hello associate a un processo][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Pianificazioni dei processi hello elenco in un account][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Elencare i processi di hello associati a una pianificazione di processo][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Hello elenco nodi di calcolo in un pool][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Elenco hello pool in un account][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Mapping per le stringhe di selezione
* **Tipi di Batch .NET**: tipi di API Batch .NET.
* **Entità API REST**: ogni pagina in questa colonna contiene una o più tabelle in cui sono elencati i nomi delle proprietà di hello API REST per il tipo di hello. Questi nomi di proprietà vengono usati per la costruzione di stringhe di *selezione* . Questi stessi nomi di proprietà verranno usati per costruire una stringa [ODATADetailLevel.SelectClause][odata_select].

| Tipi di Batch .NET | Entità di API REST |
| --- | --- |
| [Certificate][net_cert] |[Ottenere informazioni su un certificato][rest_get_cert] |
| [CloudJob][net_job] |[Ottenere informazioni su un processo][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Ottenere informazioni su una pianificazione di processi][rest_get_schedule] |
| [ComputeNode][net_node] |[Ottenere informazioni su un nodo][rest_get_node] |
| [CloudPool][net_pool] |[Ottenere informazioni su un pool][rest_get_pool] |
| [CloudTask][net_task] |[Ottenere informazioni su un'attività][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Esempio: costruire una stringa di filtro
Quando si costruisce una stringa di filtro per [ODATADetailLevel.FilterClause][odata_filter], consultare la tabella hello in precedenza nella sezione "Mapping per le stringhe di filtro" toofind hello API REST documentazione pagina corrispondente operazione di elenco toohello che si desidera tooperform. Sono disponibili proprietà filtrabili hello e i relativi operatori supportati nella prima tabella più righe di hello in tale pagina. Se si desiderano tooretrieve tutte le attività il cui codice di uscita è diverso da zero, ad esempio, questa riga in [elenco attività hello associata a un processo] [ rest_list_tasks] specifica stringa della proprietà applicabile hello e operatori consentiti:

| Proprietà | Operazioni consentite | Tipo |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Di conseguenza, la stringa di filtro hello per elencare tutte le attività con un codice di uscita diverso da zero sarebbe:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Esempio: costruire una stringa di selezione
tooconstruct [ODATADetailLevel.SelectClause][odata_select], consultare la tabella hello sopra in "Mapping per le stringhe selezionare" e passare i codici di API REST di toohello corrispondente toohello tipo di entità che si elencare. Sono disponibili proprietà selezionabile hello e i relativi operatori supportati nella prima tabella più righe di hello in tale pagina. Se si desidera tooretrieve solo hello ID e la riga di comando per ogni attività in un elenco, ad esempio, si troverà queste righe nella tabella applicabile hello in [ottenere informazioni su un'attività][rest_get_task]:

| Proprietà | Tipo | Note |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

Selezionare stringa per includere solo hello ID e la riga di comando con ogni attività elencata di Hello sarà quindi:

`id, commandLine`

## <a name="code-samples"></a>Esempi di codice
### <a name="efficient-list-queries-code-sample"></a>Esempio di codice per query di elenco efficienti
Estrarre hello [EfficientListQueries] [ efficient_query_sample] progetto di esempio in GitHub toosee modo efficiente l'esecuzione di query di elenco in termini di prestazioni in un'applicazione. Questa applicazione console c# Crea e aggiunge un numero elevato di processi tooa di attività. Quindi, rende più chiamate toohello [JobOperations.ListTasks] [ net_list_tasks] metodo e passa [ODATADetailLevel] [ odata] gli oggetti configurato con una quantità di proprietà diversi valori toovary hello di toobe di dati restituito. Produce il seguente toohello simili di output:

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Come illustrato in ore trascorso hello, è possibile ridurre notevolmente i tempi di risposta query limitando proprietà hello e numero di hello di elementi restituiti. È possibile trovare questo e altri progetti di esempio in hello [esempi di azure batch] [ github_samples] repository in GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>Libreria BatchMetrics ed esempio di codice
Inoltre toohello EfficientListQueries codice di esempio precedente, è possibile trovare hello [BatchMetrics] [ batch_metrics] progetto in hello [esempi di azure batch] [ github_samples] Repository di GitHub. progetto di esempio Hello BatchMetrics viene illustrato come tooefficiently monitorare lo stato del processo Batch di Azure utilizzando hello API Batch.

Hello [BatchMetrics] [ batch_metrics] esempio include un progetto libreria di classi .NET che è possibile incorporare in progetti e una semplice riga di comando tooexercise di programma e illustrare l'utilizzo di hello di hello libreria.

applicazione di esempio Hello all'interno di progetto hello illustra hello seguenti operazioni:

1. Selezione attributi specifici in ordine toodownload solo hello le proprietà necessarie
2. Il filtro sui tempi di transizione di stato in toodownload ordine solo modifiche dall'ultima query hello

Ad esempio, hello al metodo nella libreria BatchMetrics hello. Restituisce un ODATADetailLevel che specifica che solo hello `id` e `state` devono ottenere le proprietà per le entità hello che vengono eseguita una query. Specifica inoltre che solo le entità il cui stato è stato modificato dall'hello specificato `DateTime` parametro deve essere restituito.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Passaggi successivi
### <a name="parallel-node-tasks"></a>Attività parallele sui nodi
[Ottimizzare l'utilizzo delle risorse di calcolo di Azure Batch con le attività simultanee nodo](batch-parallel-node-tasks.md) un altro articolo correlato tooBatch le prestazioni dell'applicazione. Alcuni tipi di carichi di lavoro possono trarre vantaggio dall'esecuzione di attività in parallelo su nodi di calcolo più grandi, ma in numero inferiore. Estrarre hello [nello scenario di esempio](batch-parallel-node-tasks.md#example-scenario) nell'articolo hello per informazioni dettagliate su questo scenario.

### <a name="batch-forum"></a>Forum di Batch
Hello [Forum di Azure Batch] [ forum] su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello. Leggere i post contrassegnati e inviare domande durante le procedure di sviluppo delle soluzioni Batch.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job