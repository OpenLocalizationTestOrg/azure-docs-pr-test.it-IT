---
title: aaaHow toouse archiviazione tabelle di Azure con hello WebJobs SDK
description: "Informazioni su come toouse Azure tabella archiviazione con hello WebJobs SDK. Creare tabelle, aggiungere entità tootables e leggere le tabelle esistenti."
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="e002c-104">La modalità di archiviazione con tabelle di Azure toouse hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="e002c-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="e002c-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e002c-105">Overview</span></span>
<span data-ttu-id="e002c-106">Questa guida fornisce esempi di codice c# che mostrano come tooread e scrittura di archiviazione Azure tabelle utilizzando [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.</span><span class="sxs-lookup"><span data-stu-id="e002c-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="e002c-107">Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o troppo[più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="e002c-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="e002c-108">Alcuni dei frammenti di codice hello mostrano hello `Table` attributo utilizzato nelle funzioni che sono [chiamato manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), vale a dire, non tramite uno degli attributi di hello trigger.</span><span class="sxs-lookup"><span data-stu-id="e002c-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="e002c-109"><a id="ingress"></a>La tabella di tooa tooadd entità</span><span class="sxs-lookup"><span data-stu-id="e002c-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="e002c-110">tabella tooa tooadd entità hello utilizzare `Table` attributo con un `ICollector<T>` o `IAsyncCollector<T>` parametro dove `T` specifica dello schema di hello di entità hello desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="e002c-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="e002c-111">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello della tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="e002c-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="e002c-112">Hello nell'esempio di codice seguente consente di aggiungere `Person` tabella tooa entità denominata *in ingresso*.</span><span class="sxs-lookup"><span data-stu-id="e002c-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="e002c-113">In genere hello tipo da utilizzare con `ICollector` deriva da `TableEntity` o implementa `ITableEntity`, ma non è necessario.</span><span class="sxs-lookup"><span data-stu-id="e002c-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="e002c-114">Uno dei seguenti hello `Person` le classi di lavoro con codice di hello di hello precedente `Ingress` metodo.</span><span class="sxs-lookup"><span data-stu-id="e002c-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="e002c-115">Se si desidera toowork direttamente con hello API di archiviazione di Azure, è possibile aggiungere un `CloudStorageAccount` firma del metodo toohello parametro.</span><span class="sxs-lookup"><span data-stu-id="e002c-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="e002c-116"><a id="monitor"></a> Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="e002c-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="e002c-117">Poiché le funzioni in ingresso dei dati spesso elaborano grandi volumi di dati, hello dashboard WebJobs SDK fornisce i dati di monitoraggio in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="e002c-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="e002c-118">Hello **chiamata Log** sezione viene indicato se la funzione hello è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e002c-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="e002c-120">Hello **chiamata dettagli** pagina report hello lo stato di avanzamento della funzione (numero di entità scritta) durante l'esecuzione e offre un tooabort opportunità è.</span><span class="sxs-lookup"><span data-stu-id="e002c-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="e002c-122">Quando la funzione hello viene completata, hello **chiamata dettagli** pagina viene indicato il numero di hello di righe scritte.</span><span class="sxs-lookup"><span data-stu-id="e002c-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Funzione Ingress completata](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="e002c-124"><a id="multiple"></a>Come tooread più entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="e002c-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="e002c-125">tooread una tabella, utilizzare hello `Table` attributo con un `IQueryable<T>` parametro in cui digitare `T` deriva da `TableEntity` o implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e002c-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="e002c-126">legge Hello nell'esempio di codice seguente e i log di tutte le righe da hello `Ingress` tabella:</span><span class="sxs-lookup"><span data-stu-id="e002c-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="e002c-127"><a id="readone"></a>Come tooread una singola entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="e002c-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="e002c-128">È presente un `Table` costruttore di attributo con due parametri aggiuntivi che consentono di specificare la chiave di partizione hello e chiave di riga quando si desidera toobind tooa tabella singola entità.</span><span class="sxs-lookup"><span data-stu-id="e002c-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="e002c-129">esempio di codice seguente Hello legge una riga della tabella per un `Person` entità in base a partizione chiave e riga di valori di chiave ricevuti in un messaggio nella coda:</span><span class="sxs-lookup"><span data-stu-id="e002c-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="e002c-130">Hello `Person` classe in questo esempio non dispone di tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e002c-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="e002c-131"><a id="storageapi"></a>Come toouse hello API di archiviazione .NET direttamente toowork con una tabella</span><span class="sxs-lookup"><span data-stu-id="e002c-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="e002c-132">È inoltre possibile utilizzare hello `Table` attributo con un `CloudTable` oggetto per una maggiore flessibilità durante l'utilizzo di una tabella.</span><span class="sxs-lookup"><span data-stu-id="e002c-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="e002c-133">codice Hello seguente viene utilizzata una `CloudTable` tooadd toohello una singola entità dell'oggetto *in ingresso* tabella.</span><span class="sxs-lookup"><span data-stu-id="e002c-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="e002c-134">Per ulteriori informazioni su come hello toouse `CloudTable` , vedere [come toouse archiviazione tabelle da .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e002c-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="e002c-135"><a id="queues"></a>Argomenti correlati coperti da hello code come-tooarticle</span><span class="sxs-lookup"><span data-stu-id="e002c-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="e002c-136">Per informazioni su come l'elaborazione tabella toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non è l'elaborazione, vedere specifiche tootable [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="e002c-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="e002c-137">Gli argomenti trattati in tale articolo includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e002c-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="e002c-138">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="e002c-138">Async functions</span></span>
* <span data-ttu-id="e002c-139">Più istanze</span><span class="sxs-lookup"><span data-stu-id="e002c-139">Multiple instances</span></span>
* <span data-ttu-id="e002c-140">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="e002c-140">Graceful shutdown</span></span>
* <span data-ttu-id="e002c-141">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="e002c-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="e002c-142">Impostare le stringhe di connessione SDK hello nel codice</span><span class="sxs-lookup"><span data-stu-id="e002c-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="e002c-143">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="e002c-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="e002c-144">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="e002c-144">Trigger a function manually</span></span>
* <span data-ttu-id="e002c-145">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="e002c-145">Write logs</span></span>

## <span data-ttu-id="e002c-146"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e002c-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="e002c-147">Questa guida è fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e002c-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="e002c-148">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="e002c-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

