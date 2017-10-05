---
title: Come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK
description: "Informazioni su come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK. Creare tabelle, aggiungere entità alle tabelle e leggere le tabelle esistenti."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="de751-104">Come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="de751-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="de751-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="de751-105">Overview</span></span>
<span data-ttu-id="de751-106">In questa guida sono forniti esempi di codice C# che illustrano come leggere e scrivere le tabelle di archiviazione di Azure usando [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="de751-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="de751-107">Nella guida si presuppone che si sappia come [creare un progetto processo Web in Visual Studio con stringhe di connessione che puntano all'account di archiviazione](websites-dotnet-webjobs-sdk-get-started.md) o a [più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="de751-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="de751-108">Alcuni dei frammenti di codice illustrano l'attributo `Table` usato nelle funzioni [chiamate manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)e non mediante uno degli attributi del trigger.</span><span class="sxs-lookup"><span data-stu-id="de751-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="de751-109"><a id="ingress"></a> Come aggiungere entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="de751-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="de751-110">Per aggiungere entità a una tabella, utilizzare l’attributo `Table` con un parametro `ICollector<T>` o `IAsyncCollector<T>` dove `T` specifica lo schema delle entità da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="de751-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="de751-111">Il costruttore dell'attributo accetta un parametro di stringa che specifica il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="de751-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="de751-112">L’esempio di codice seguente aggiunge le entità `Person` a una tabella denominata *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="de751-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="de751-113">In genere il tipo usato con `ICollector` deriva da `TableEntity` o implementa `ITableEntity`, anche se non necessariamente.</span><span class="sxs-lookup"><span data-stu-id="de751-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="de751-114">Una delle seguenti classi `Person` usa il codice illustrato nel precedente metodo `Ingress`.</span><span class="sxs-lookup"><span data-stu-id="de751-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="de751-115">Se si desidera usare direttamente l'API di archiviazione di Azure, è possibile aggiungere un parametro `CloudStorageAccount` alla firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="de751-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="de751-116"><a id="monitor"></a> Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="de751-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="de751-117">Poiché spesso le funzioni di ingresso ai dati (Ingress) elaborano volumi elevati di informazioni, il dashboard di WebJobs SDK fornisce dati di monitoraggio in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="de751-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="de751-118">La sezione **Invocation Log** indica se la funzione è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="de751-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="de751-120">La pagina **Invocation Details** restituisce lo stato di avanzamento della funzione (numero di entità scritte) mentre è in esecuzione e offre la possibilità di interromperla.</span><span class="sxs-lookup"><span data-stu-id="de751-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="de751-122">Al termine della funzione, la pagina **Invocation Details** indica il numero di righe scritte.</span><span class="sxs-lookup"><span data-stu-id="de751-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Funzione Ingress completata](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="de751-124"><a id="multiple"></a> Come leggere più entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="de751-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="de751-125">Per leggere una tabella, usare l’attributo `Table` con un parametro `IQueryable<T>` dove il tipo `T` deriva da `TableEntity` o implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="de751-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="de751-126">Il seguente esempio di codice legge e registra tutte le righe dalla tabella `Ingress`:</span><span class="sxs-lookup"><span data-stu-id="de751-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="de751-127"><a id="readone"></a> Come leggere una singola entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="de751-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="de751-128">È disponibile un costruttore dell'attributo `Table` con due parametri aggiuntivi che consentono di specificare la chiave di partizione e la chiave di riga quando si desidera l'associazione a un'entità di tabella singola.</span><span class="sxs-lookup"><span data-stu-id="de751-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="de751-129">Il seguente esempio di codice legge una riga della tabella per un'entità `Person` basata sui valori della chiave di partizione e della chiave di riga ricevuti in un messaggio di coda:</span><span class="sxs-lookup"><span data-stu-id="de751-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="de751-130">La classe `Person` in questo esempio non deve implementare `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="de751-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="de751-131"><a id="storageapi"></a> Come usare l'API di archiviazione .NET direttamente con una tabella</span><span class="sxs-lookup"><span data-stu-id="de751-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="de751-132">È possibile usare l'attributo `Table` anche con un oggetto `CloudTable` per una maggiore flessibilità nell'uso di una tabella.</span><span class="sxs-lookup"><span data-stu-id="de751-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="de751-133">Il seguente esempio di codice usa un oggetto `CloudTable` per aggiungere una singola entità alla tabella *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="de751-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="de751-134">Per altre informazioni su come usare l'oggetto `CloudTable` , vedere l'argomento relativo [all'uso dell'archiviazione tabelle da .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="de751-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="de751-135"><a id="queues"></a>Argomenti correlati trattati nell'articolo delle procedure sulle code</span><span class="sxs-lookup"><span data-stu-id="de751-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="de751-136">Per informazioni su come gestire l'elaborazione di tabelle attivata da un messaggio di coda o per scenari di WebJobs SDK non specifici dell'elaborazione di tabelle, vedere [Come usare il servizio di archiviazione code di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="de751-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="de751-137">Gli argomenti trattati in questo articolo includono quanto segue:</span><span class="sxs-lookup"><span data-stu-id="de751-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="de751-138">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="de751-138">Async functions</span></span>
* <span data-ttu-id="de751-139">Più istanze</span><span class="sxs-lookup"><span data-stu-id="de751-139">Multiple instances</span></span>
* <span data-ttu-id="de751-140">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="de751-140">Graceful shutdown</span></span>
* <span data-ttu-id="de751-141">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="de751-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="de751-142">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="de751-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="de751-143">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="de751-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="de751-144">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="de751-144">Trigger a function manually</span></span>
* <span data-ttu-id="de751-145">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="de751-145">Write logs</span></span>

## <span data-ttu-id="de751-146"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de751-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="de751-147">Questa guida ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="de751-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="de751-148">Per altre informazioni su come usare i processi Web di Azure e su WebJobs SDK, vedere le [risorse consigliate per i processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="de751-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

