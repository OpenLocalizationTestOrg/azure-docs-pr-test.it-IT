---
title: 'Progettare query di tipo elenco efficienti: Azure Batch | Documentazione Microsoft'
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
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="b59cb-103">Creare query per elencare le risorse di Batch in modo efficiente</span><span class="sxs-lookup"><span data-stu-id="b59cb-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="b59cb-104">Viene illustrato come migliorare le prestazioni dell'applicazione Azure Batch, riducendo la quantità di dati restituiti dal servizio quando si eseguono query su processi, attività e nodi di calcolo con la libreria [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="b59cb-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="b59cb-105">Quasi tutte le applicazioni Batch devono eseguire un tipo di monitoraggio o un'altra operazione che esegue query sul servizio Batch, spesso a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="b59cb-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="b59cb-106">Per determinare ad esempio se sono ancora presenti attività in coda in un processo, è necessario ottenere dati per ogni attività nel processo.</span><span class="sxs-lookup"><span data-stu-id="b59cb-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="b59cb-107">Per determinare lo stato dei nodi nel pool è necessario ottenere dati in ogni nodo nel pool.</span><span class="sxs-lookup"><span data-stu-id="b59cb-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="b59cb-108">Questo articolo illustra come eseguire queste query nel modo più efficiente.</span><span class="sxs-lookup"><span data-stu-id="b59cb-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="b59cb-109">Il servizio Batch fornisce supporto speciale delle API per lo scenario comune di conteggio delle attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="b59cb-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="b59cb-110">Invece di usare una query di tipo elenco a questo scopo, è possibile chiamare l'operazione di [recupero del conteggio delle attività][rest_get_task_counts].</span><span class="sxs-lookup"><span data-stu-id="b59cb-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="b59cb-111">Questa operazione restituisce il numero di attività in sospeso, in esecuzione o completate, nonché di quelle riuscite e non riuscite.</span><span class="sxs-lookup"><span data-stu-id="b59cb-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="b59cb-112">L'operazione di recupero dei conteggi delle attività è più efficiente di una query di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="b59cb-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="b59cb-113">Per altre informazioni, vedere [Conteggiare le attività per un processo in base allo stato (anteprima)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="b59cb-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="b59cb-114">Questa operazione non è disponibile nelle versioni del servizio Batch precedenti alla 2017-06-01.5.1.</span><span class="sxs-lookup"><span data-stu-id="b59cb-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="b59cb-115">Se si usa una versione meno recente del servizio, usare una query di tipo elenco per conteggiare le attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="b59cb-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="b59cb-116">Definire livelli di dettaglio</span><span class="sxs-lookup"><span data-stu-id="b59cb-116">Meet the DetailLevel</span></span>
<span data-ttu-id="b59cb-117">In un'applicazione Batch di produzione, le entità da elaborare, ad esempio processi, attività e nodi di calcolo, possono essere migliaia.</span><span class="sxs-lookup"><span data-stu-id="b59cb-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="b59cb-118">Quando si richiedono informazioni su queste risorse, una grande quantità di dati deve "transitare" dal servizio Batch all'applicazione in ogni query.</span><span class="sxs-lookup"><span data-stu-id="b59cb-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="b59cb-119">Limitando il numero di elementi e il tipo di informazioni restituiti da una query, è possibile aumentarne la velocità e quindi migliorare le prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b59cb-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="b59cb-120">Questo frammento di codice dell'API [Batch .NET][api_net] elenca *ogni* attività associata a un processo, insieme a *tutte* le proprietà dell'attività:</span><span class="sxs-lookup"><span data-stu-id="b59cb-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="b59cb-121">È possibile eseguire una query di tipo elenco molto più efficiente, tuttavia, applicando un "livello di dettaglio" alla query.</span><span class="sxs-lookup"><span data-stu-id="b59cb-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="b59cb-122">A questo scopo, indicare un oggetto [ODATADetailLevel][odata] al metodo [JobOperations.ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="b59cb-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="b59cb-123">Questo frammento restituisce solo l'ID, la riga di comando e informazioni sulle proprietà del nodo di calcolo delle attività completate:</span><span class="sxs-lookup"><span data-stu-id="b59cb-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="b59cb-124">Se in questo scenario di esempio il processo include migliaia di attività, il risultato della seconda query viene in genere restituito molto più rapidamente della prima.</span><span class="sxs-lookup"><span data-stu-id="b59cb-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="b59cb-125">[Di seguito](#efficient-querying-in-batch-net)sono disponibili altre informazioni sull'uso di ODATADetailLevel quando si elencano elementi con l'API Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="b59cb-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b59cb-126">È consigliabile specificare *sempre* un oggetto ODATADetailLevel per le chiamate di tipo elenco all'API .NET, per assicurare il massimo livello di efficienza e prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b59cb-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="b59cb-127">Specificando un livello di dettaglio è possibile ridurre i tempi di risposta del servizio Batch, migliorare l'utilizzo della rete e ridurre l'utilizzo di memoria da parte delle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="b59cb-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="b59cb-128">Filtro, selezione ed espansione</span><span class="sxs-lookup"><span data-stu-id="b59cb-128">Filter, select, and expand</span></span>
<span data-ttu-id="b59cb-129">Le API [Batch .NET][api_net] e [Batch REST][api_rest] consentono di ridurre sia il numero di elementi restituiti in un elenco sia la quantità di informazioni restituite per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="b59cb-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="b59cb-130">A questo scopo, specificare stringhe di **filtro**, **selezione** ed **espansione** quando si eseguono query di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="b59cb-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="b59cb-131">Filtro</span><span class="sxs-lookup"><span data-stu-id="b59cb-131">Filter</span></span>
<span data-ttu-id="b59cb-132">La stringa di filtro è un'espressione che riduce il numero di elementi restituiti.</span><span class="sxs-lookup"><span data-stu-id="b59cb-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="b59cb-133">Ad esempio, elencare solo le attività in esecuzione per un processo o solo i nodi di calcolo pronti per eseguire attività.</span><span class="sxs-lookup"><span data-stu-id="b59cb-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="b59cb-134">Una stringa di filtro è costituita da una o più espressioni, ciascuna delle quali è composta da un nome di proprietà, un operatore e un valore.</span><span class="sxs-lookup"><span data-stu-id="b59cb-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="b59cb-135">Le proprietà che è possibile immettere sono specifiche di ogni tipo di entità su cui viene eseguita la query, come lo sono gli operatori supportati per ogni proprietà.</span><span class="sxs-lookup"><span data-stu-id="b59cb-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="b59cb-136">È possibile combinare più espressioni usando gli operatori logici `and` e `or`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="b59cb-137">Questo esempio di stringa di filtro indica solo le attività di "rendering" in esecuzione: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="b59cb-138">Selezionare</span><span class="sxs-lookup"><span data-stu-id="b59cb-138">Select</span></span>
<span data-ttu-id="b59cb-139">La stringa di selezione limita i valori della proprietà restituiti per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="b59cb-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="b59cb-140">Si specifica un elenco di nomi di proprietà e vengono restituiti solo i valori di quelle proprietà per gli elementi nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="b59cb-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="b59cb-141">La stringa di selezione è costituita da un elenco con valori delimitati da virgole di nomi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="b59cb-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="b59cb-142">È possibile specificare qualsiasi proprietà per il tipo di entità su cui si esegue la query.</span><span class="sxs-lookup"><span data-stu-id="b59cb-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="b59cb-143">Questa stringa di selezione di esempio specifica che dovranno essere restituiti solo i valori di tre proprietà per ogni attività: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="b59cb-144">Espandere</span><span class="sxs-lookup"><span data-stu-id="b59cb-144">Expand</span></span>
<span data-ttu-id="b59cb-145">La stringa di espansione riduce il numero di chiamate API richieste per ottenere determinate informazioni.</span><span class="sxs-lookup"><span data-stu-id="b59cb-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="b59cb-146">Quando si usa una stringa di espansione, si possono ottenere altre informazioni su ogni elemento con una singola chiamata API.</span><span class="sxs-lookup"><span data-stu-id="b59cb-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="b59cb-147">Invece di ottenere prima l'elenco delle entità e quindi richiedere informazioni per ogni elemento nell'elenco, usare una stringa di espansione per ottenere le stesse informazioni in una singola chiamata API.</span><span class="sxs-lookup"><span data-stu-id="b59cb-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="b59cb-148">Meno chiamate API significano prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="b59cb-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="b59cb-149">Analogamente alla stringa di selezione, la stringa di espansione controlla se determinati dati sono inclusi nei risultati di una query di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="b59cb-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="b59cb-150">La stringa di espansione è supportata solo quando viene usata nell'elenco di processi, pianificazioni di processi, attività e pool.</span><span class="sxs-lookup"><span data-stu-id="b59cb-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="b59cb-151">Attualmente supporta solo informazioni statistiche.</span><span class="sxs-lookup"><span data-stu-id="b59cb-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="b59cb-152">Quando tutte le proprietà sono obbligatorie e non è stata specificata alcuna stringa di selezione, è *necessario* usare la stringa di espansione per ottenere informazioni statistiche.</span><span class="sxs-lookup"><span data-stu-id="b59cb-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="b59cb-153">Se si usa una stringa di selezione per ottenere un subset di proprietà, è possibile specificare `stats` nella stringa di selezione e non è necessario specificare la stringa di espansione.</span><span class="sxs-lookup"><span data-stu-id="b59cb-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="b59cb-154">Questo esempio di stringa di espansione specifica che dovranno essere restituite informazioni statistiche per ogni elemento nell'elenco: `stats`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="b59cb-155">Quando si costruisce uno qualsiasi dei tre tipi di stringhe di query, ovvero filtro, selezione ed espansione, è necessario assicurarsi che i nomi delle proprietà e le lettere maiuscole/minuscole corrispondano alle relative controparti nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="b59cb-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="b59cb-156">Ad esempio, quando si usa la classe [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) .NET, è necessario specificare **state** invece di **State**, anche se la proprietà .NET è [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="b59cb-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="b59cb-157">Per i mapping delle proprietà tra le API .NET e REST, vedere le tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="b59cb-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="b59cb-158">Regole per le stringhe di filtro, selezione ed espansione</span><span class="sxs-lookup"><span data-stu-id="b59cb-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="b59cb-159">I nomi delle proprietà nelle stringhe di filtro, selezione ed espansione devono corrispondere a quelli presenti nell'API [Batch REST][api_rest] anche quando si usa [Batch .NET][api_net] o uno degli altri SDK di Batch.</span><span class="sxs-lookup"><span data-stu-id="b59cb-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="b59cb-160">Per tutti i nomi di proprietà viene fatta distinzione tra maiuscole e minuscole, al contrario di quanto avviene per i valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="b59cb-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="b59cb-161">Le stringhe relative a data/ora possono essere indicate in uno dei due formati seguenti e devono essere precedute da `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="b59cb-162">Esempio di formato W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="b59cb-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="b59cb-163">Esempio di formato RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="b59cb-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="b59cb-164">Le stringhe booleane sono `true` o `false`.</span><span class="sxs-lookup"><span data-stu-id="b59cb-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="b59cb-165">Se si specifica una proprietà o un operatore non valido, viene generato un errore `400 (Bad Request)` .</span><span class="sxs-lookup"><span data-stu-id="b59cb-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="b59cb-166">Esecuzione efficiente di query in Batch .NET</span><span class="sxs-lookup"><span data-stu-id="b59cb-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="b59cb-167">Nell'API [Batch .NET][api_net] viene usata la classe [ODATADetailLevel][odata] per specificare le stringhe di filtro, selezione ed espansione alle operazioni di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="b59cb-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="b59cb-168">La classe ODataDetailLevel presenta tre proprietà pubbliche di tipo stringa che possono essere specificate nel costruttore o impostate direttamente:</span><span class="sxs-lookup"><span data-stu-id="b59cb-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="b59cb-169">L'oggetto ODataDetailLevel viene quindi passato come parametro alle diverse operazioni di tipo elenco, ad esempio [ListPools][net_list_pools], [ListJobs][net_list_jobs] e [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="b59cb-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="b59cb-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: limita il numero di elementi restituiti.</span><span class="sxs-lookup"><span data-stu-id="b59cb-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="b59cb-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: specifica i valori della proprietà restituiti con ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="b59cb-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="b59cb-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: recupera i dati per tutti gli elementi in una singola chiamata all'API anziché con chiamate separate per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="b59cb-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="b59cb-173">Il frammento di codice seguente usa l'API Batch .NET per eseguire query efficienti sul servizio Batch per ottenere le statistiche di un set di pool specificato.</span><span class="sxs-lookup"><span data-stu-id="b59cb-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="b59cb-174">In questo scenario l'utente Batch ha pool di test e di produzione.</span><span class="sxs-lookup"><span data-stu-id="b59cb-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="b59cb-175">Gli ID del pool di test sono preceduti da "test", mentre quelli del pool di produzione sono preceduti da "prod".</span><span class="sxs-lookup"><span data-stu-id="b59cb-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="b59cb-176">Nel frammento di codice *myBatchClient* è un'istanza della classe [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) inizializzata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b59cb-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="b59cb-177">È anche possibile passare un'istanza di [ODATADetailLevel][odata] configurata con le clausole Select ed Expand ai metodi Get appropriati, ad esempio [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), per limitare la quantità di dati restituiti.</span><span class="sxs-lookup"><span data-stu-id="b59cb-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="b59cb-178">Mapping di API Batch REST a API .NET</span><span class="sxs-lookup"><span data-stu-id="b59cb-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="b59cb-179">I nomi delle proprietà nelle stringhe di filtro, selezione ed espansione *devono* riflettere le rispettive controparti dell'API REST, sia a livello di nome che di lettere maiuscole/minuscole.</span><span class="sxs-lookup"><span data-stu-id="b59cb-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="b59cb-180">Le tabelle seguenti forniscono i mapping tra l'API .NET e le relative controparti dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="b59cb-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="b59cb-181">Mapping per le stringhe di filtro</span><span class="sxs-lookup"><span data-stu-id="b59cb-181">Mappings for filter strings</span></span>
* <span data-ttu-id="b59cb-182">**Metodi list .NET**: ogni metodo dell'API .NET in questa colonna accetta un oggetto [ODATADetailLevel][odata] come parametro.</span><span class="sxs-lookup"><span data-stu-id="b59cb-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="b59cb-183">**Richieste list REST**: ogni pagina dell'API REST collegata in questa colonna contiene una tabella che specifica le proprietà e le operazioni consentite nelle stringhe di *filtro* .</span><span class="sxs-lookup"><span data-stu-id="b59cb-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="b59cb-184">Questi nomi di proprietà e queste operazioni verranno usati per costruire una stringa [ODATADetailLevel.FilterClause][odata_filter].</span><span class="sxs-lookup"><span data-stu-id="b59cb-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="b59cb-185">Metodi list .NET</span><span class="sxs-lookup"><span data-stu-id="b59cb-185">.NET list methods</span></span> | <span data-ttu-id="b59cb-186">Richieste list REST</span><span class="sxs-lookup"><span data-stu-id="b59cb-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="b59cb-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="b59cb-188">[Elencare i certificati in un account][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="b59cb-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="b59cb-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="b59cb-190">[Elencare i file associati a un'attività][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="b59cb-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="b59cb-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="b59cb-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="b59cb-192">[Elencare lo stato della preparazione e le attività di rilascio per un processo specifico][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="b59cb-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="b59cb-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="b59cb-194">[Elencare i processi in un account][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="b59cb-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="b59cb-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="b59cb-196">[Elencare i file in un nodo][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="b59cb-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="b59cb-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="b59cb-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="b59cb-198">[Elencare le attività associate a un processo][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="b59cb-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="b59cb-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="b59cb-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="b59cb-200">[Elencare le pianificazioni di processi in un account][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="b59cb-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="b59cb-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="b59cb-202">[Elencare i processi associati a una pianificazione di processi][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="b59cb-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="b59cb-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="b59cb-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="b59cb-204">[Elencare i nodi di calcolo in un pool][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="b59cb-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="b59cb-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="b59cb-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="b59cb-206">[Elencare i pool in un account][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="b59cb-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="b59cb-207">Mapping per le stringhe di selezione</span><span class="sxs-lookup"><span data-stu-id="b59cb-207">Mappings for select strings</span></span>
* <span data-ttu-id="b59cb-208">**Tipi di Batch .NET**: tipi di API Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="b59cb-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="b59cb-209">**Entità di API REST**: ogni pagina di questa colonna contiene una o più tabelle che indicano i nomi delle proprietà dell'API REST per il tipo.</span><span class="sxs-lookup"><span data-stu-id="b59cb-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="b59cb-210">Questi nomi di proprietà vengono usati per la costruzione di stringhe di *selezione* .</span><span class="sxs-lookup"><span data-stu-id="b59cb-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="b59cb-211">Questi stessi nomi di proprietà verranno usati per costruire una stringa [ODATADetailLevel.SelectClause][odata_select].</span><span class="sxs-lookup"><span data-stu-id="b59cb-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="b59cb-212">Tipi di Batch .NET</span><span class="sxs-lookup"><span data-stu-id="b59cb-212">Batch .NET types</span></span> | <span data-ttu-id="b59cb-213">Entità di API REST</span><span class="sxs-lookup"><span data-stu-id="b59cb-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="b59cb-214">[Certificate][net_cert]</span><span class="sxs-lookup"><span data-stu-id="b59cb-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="b59cb-215">[Ottenere informazioni su un certificato][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="b59cb-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="b59cb-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="b59cb-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="b59cb-217">[Ottenere informazioni su un processo][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="b59cb-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="b59cb-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="b59cb-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="b59cb-219">[Ottenere informazioni su una pianificazione di processi][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="b59cb-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="b59cb-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="b59cb-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="b59cb-221">[Ottenere informazioni su un nodo][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="b59cb-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="b59cb-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="b59cb-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="b59cb-223">[Ottenere informazioni su un pool][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="b59cb-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="b59cb-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="b59cb-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="b59cb-225">[Ottenere informazioni su un'attività][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="b59cb-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="b59cb-226">Esempio: costruire una stringa di filtro</span><span class="sxs-lookup"><span data-stu-id="b59cb-226">Example: construct a filter string</span></span>
<span data-ttu-id="b59cb-227">Quando si costruisce una stringa di filtro per un oggetto [ODATADetailLevel.FilterClause][odata_filter], vedere la tabella in "Mapping per le stringhe di filtro" per trovare la pagina di documentazione dell'API REST corrispondente all'operazione di tipo elenco da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b59cb-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="b59cb-228">Le proprietà filtrabili e gli operatori supportati sono disponibili nella prima tabella con più righe in quella pagina.</span><span class="sxs-lookup"><span data-stu-id="b59cb-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="b59cb-229">Per recuperare ad esempio tutte le attività il cui codice di uscita non è pari a zero, questa riga in [Elencare le attività associate a un processo][rest_list_tasks] specifica la stringa della proprietà applicabile e gli operatori consentiti:</span><span class="sxs-lookup"><span data-stu-id="b59cb-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="b59cb-230">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b59cb-230">Property</span></span> | <span data-ttu-id="b59cb-231">Operazioni consentite</span><span class="sxs-lookup"><span data-stu-id="b59cb-231">Operations allowed</span></span> | <span data-ttu-id="b59cb-232">Tipo</span><span class="sxs-lookup"><span data-stu-id="b59cb-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="b59cb-233">La stringa di filtro per elencare tutte le attività con un codice di uscita non pari a zero sarà:</span><span class="sxs-lookup"><span data-stu-id="b59cb-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="b59cb-234">Esempio: costruire una stringa di selezione</span><span class="sxs-lookup"><span data-stu-id="b59cb-234">Example: construct a select string</span></span>
<span data-ttu-id="b59cb-235">Per costruire una stringa [ODATADetailLevel.SelectClause][odata_select], vedere la tabella in "Mapping per le stringhe di selezione" e passare alla pagina dell'API REST che corrisponde al tipo di entità da specificare.</span><span class="sxs-lookup"><span data-stu-id="b59cb-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="b59cb-236">Le proprietà selezionabili e gli operatori supportati sono disponibili nella prima tabella con più righe in quella pagina.</span><span class="sxs-lookup"><span data-stu-id="b59cb-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="b59cb-237">Se ad esempio si desidera recuperare solo l'ID e la riga di comando per ogni attività in un elenco, queste righe si trovano nella tabella applicabile in [Ottenere informazioni su un'attività][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="b59cb-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="b59cb-238">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b59cb-238">Property</span></span> | <span data-ttu-id="b59cb-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="b59cb-239">Type</span></span> | <span data-ttu-id="b59cb-240">Note</span><span class="sxs-lookup"><span data-stu-id="b59cb-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="b59cb-241">La stringa di selezione per includere solo l'ID e la riga di comando con ogni attività elencata sarà:</span><span class="sxs-lookup"><span data-stu-id="b59cb-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="b59cb-242">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="b59cb-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="b59cb-243">Esempio di codice per query di elenco efficienti</span><span class="sxs-lookup"><span data-stu-id="b59cb-243">Efficient list queries code sample</span></span>
<span data-ttu-id="b59cb-244">Per verificare il modo in cui una query di tipo elenco può influire efficacemente sulle prestazioni in un'applicazione, vedere il progetto di esempio [EfficientListQueries][efficient_query_sample] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b59cb-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="b59cb-245">Questa applicazione console C# crea e aggiunge un numero elevato di attività a un processo.</span><span class="sxs-lookup"><span data-stu-id="b59cb-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="b59cb-246">Esegue quindi più chiamate al metodo [JobOperations.ListTasks][net_list_tasks] e passa gli oggetti [ODATADetailLevel][odata] configurati con valori di proprietà diversi per variare la quantità di dati da restituire.</span><span class="sxs-lookup"><span data-stu-id="b59cb-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="b59cb-247">L'output generato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b59cb-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="b59cb-248">Come illustrato nelle informazioni sul tempo trascorso, è possibile ridurre notevolmente i tempi di risposta della query limitando le proprietà e il numero di elementi restituiti.</span><span class="sxs-lookup"><span data-stu-id="b59cb-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="b59cb-249">Questo e altri progetti di esempio sono disponibili nel repository [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b59cb-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="b59cb-250">Libreria BatchMetrics ed esempio di codice</span><span class="sxs-lookup"><span data-stu-id="b59cb-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="b59cb-251">Oltre all'esempio di codice EfficientListQueries precedente, è possibile trovare il progetto [BatchMetrics][batch_metrics] nel repository [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b59cb-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="b59cb-252">Il progetto di esempio BatchMetrics illustra come monitorare in modo efficiente lo stato dei processi di Azure Batch con l'API di Batch.</span><span class="sxs-lookup"><span data-stu-id="b59cb-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="b59cb-253">L'esempio [BatchMetrics][batch_metrics] include un progetto di libreria di classi .NET che è possibile incorporare nei propri progetti e un semplice programma della riga di comando per apprendere l'uso della libreria.</span><span class="sxs-lookup"><span data-stu-id="b59cb-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="b59cb-254">L'applicazione di esempio nel progetto illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b59cb-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="b59cb-255">Selezione degli attributi specifici per scaricare solo le proprietà necessarie</span><span class="sxs-lookup"><span data-stu-id="b59cb-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="b59cb-256">Filtro delle ore di transizione allo stato per scaricare solo le modifiche apportate dopo l'ultima query</span><span class="sxs-lookup"><span data-stu-id="b59cb-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="b59cb-257">Ad esempio, il metodo seguente è presente nella libreria BatchMetrics.</span><span class="sxs-lookup"><span data-stu-id="b59cb-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="b59cb-258">Restituisce un elemento ODATADetailLevel che specifica che dovranno essere ottenute solo le proprietà `id` e `state` per le entità sulle quali viene eseguita una query.</span><span class="sxs-lookup"><span data-stu-id="b59cb-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="b59cb-259">Specifica anche che dovranno essere restituite solo le entità il cui stato è stato modificato dopo il parametro `DateTime` specificato.</span><span class="sxs-lookup"><span data-stu-id="b59cb-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="b59cb-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b59cb-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="b59cb-261">Attività parallele sui nodi</span><span class="sxs-lookup"><span data-stu-id="b59cb-261">Parallel node tasks</span></span>
<span data-ttu-id="b59cb-262">[Ottimizzare l'utilizzo delle risorse di calcolo di Azure Batch con attività dei nodi simultanee](batch-parallel-node-tasks.md) è un altro articolo correlato alle prestazioni per l'applicazione Batch.</span><span class="sxs-lookup"><span data-stu-id="b59cb-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="b59cb-263">Alcuni tipi di carichi di lavoro possono trarre vantaggio dall'esecuzione di attività in parallelo su nodi di calcolo più grandi, ma in numero inferiore.</span><span class="sxs-lookup"><span data-stu-id="b59cb-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="b59cb-264">Vedere lo [scenario di esempio](batch-parallel-node-tasks.md#example-scenario) nell'articolo per informazioni dettagliate su questo scenario.</span><span class="sxs-lookup"><span data-stu-id="b59cb-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="b59cb-265">Forum di Batch</span><span class="sxs-lookup"><span data-stu-id="b59cb-265">Batch Forum</span></span>
<span data-ttu-id="b59cb-266">Il [forum di Azure Batch][forum] su MSDN consente di seguire discussioni su Batch e inviare domande sul servizio.</span><span class="sxs-lookup"><span data-stu-id="b59cb-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="b59cb-267">Leggere i post contrassegnati e inviare domande durante le procedure di sviluppo delle soluzioni Batch.</span><span class="sxs-lookup"><span data-stu-id="b59cb-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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