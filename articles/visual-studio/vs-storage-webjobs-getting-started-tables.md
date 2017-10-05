---
title: Introduzione all'archiviazione di Azure e ai servizi relativi a Visual Studio (progetti WebJob)
description: "Informazioni su come iniziare a usare l’archiviazione tabella di Azure in un progetto WebJobs di Azure in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 0bf51f9113c45c747cd4fd3f76bdabd4a4c1f8e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="08e81-103">Introduzione all'Archiviazione di Azure (progetti Azure WebJob)</span><span class="sxs-lookup"><span data-stu-id="08e81-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="08e81-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="08e81-104">Overview</span></span>
<span data-ttu-id="08e81-105">Questo articolo fornisce esempi di codice C# che illustrano come usare Azure WebJobs SDK versione 1.x con il servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="08e81-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="08e81-106">Gli esempi di codice usano [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="08e81-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="08e81-107">Il servizio di archiviazione tabelle di Azure consente di archiviare grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="08e81-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="08e81-108">Il servizio è un datastore NoSQL che accetta chiamate autenticate dall'interno e dall'esterno del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="08e81-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="08e81-109">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="08e81-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="08e81-110">Per altre informazioni, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) .</span><span class="sxs-lookup"><span data-stu-id="08e81-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="08e81-111">Alcuni dei frammenti di codice illustrano l'attributo **Tabella** usato nelle funzioni chiamate manualmente e non mediante uno degli attributi del trigger.</span><span class="sxs-lookup"><span data-stu-id="08e81-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="08e81-112">Come aggiungere entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="08e81-112">How to add entities to a table</span></span>
<span data-ttu-id="08e81-113">Per aggiungere entità a una tabella, usare l'attributo **Table** con un parametro **ICollector<T>** o **IAsyncCollector<T>** dove **T** specifica lo schema delle entità da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="08e81-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="08e81-114">Il costruttore dell'attributo accetta un parametro di stringa che specifica il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="08e81-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="08e81-115">L’esempio di codice seguente aggiunge le entità **Persona** a una tabella denominata *Ingresso*.</span><span class="sxs-lookup"><span data-stu-id="08e81-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="08e81-116">In genere il tipo usato con **ICollector** deriva da **TableEntity** o implementa **ITableEntity**, ma non obbligatoriamente.</span><span class="sxs-lookup"><span data-stu-id="08e81-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="08e81-117">Ognuna delle seguenti classi **Person** funziona con il codice illustrato nel precedente metodo **Ingress**.</span><span class="sxs-lookup"><span data-stu-id="08e81-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="08e81-118">Se si desidera usare direttamente l’API dell'account di archiviazione di Azure, è anche possibile aggiungere un parametro **CloudStorageAccount** alla firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="08e81-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="08e81-119">Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="08e81-119">Real-time monitoring</span></span>
<span data-ttu-id="08e81-120">Poiché spesso le funzioni di ingresso ai dati (Ingress) elaborano volumi elevati di informazioni, il dashboard di WebJobs SDK fornisce dati di monitoraggio in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="08e81-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="08e81-121">La sezione **Invocation Log** indica se la funzione è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="08e81-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="08e81-123">La pagina **Invocation Details** restituisce lo stato di avanzamento della funzione (numero di entità scritte) mentre è in esecuzione e offre la possibilità di interromperla.</span><span class="sxs-lookup"><span data-stu-id="08e81-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="08e81-125">Al termine della funzione, la pagina **Invocation Details** indica il numero di righe scritte.</span><span class="sxs-lookup"><span data-stu-id="08e81-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Funzione Ingress completata](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="08e81-127">Come leggere più entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="08e81-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="08e81-128">Per leggere una tabella, usare l'attributo **Tabella** con un parametro **IQueryable<T>** in cui il tipo **T** deriva da **TableEntity** o implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="08e81-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="08e81-129">Il seguente esempio di codice legge e registra tutte le righe dalla tabella **Ingresso** :</span><span class="sxs-lookup"><span data-stu-id="08e81-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="08e81-130">Come leggere una singola entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="08e81-130">How to read a single entity from a table</span></span>
<span data-ttu-id="08e81-131">È disponibile un costruttore dell'attributo **Tabella** con due parametri aggiuntivi che consentono di specificare la chiave di partizione e la chiave di riga quando si desidera l'associazione a un'entità di tabella singola.</span><span class="sxs-lookup"><span data-stu-id="08e81-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="08e81-132">Il seguente esempio di codice legge una riga della tabella per un'entità **Persona** basata sui valori della chiave di partizione e della chiave di riga ricevuti in un messaggio di coda:</span><span class="sxs-lookup"><span data-stu-id="08e81-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="08e81-133">La classe **Person** in questo esempio non deve implementare **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="08e81-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="08e81-134">Come usare l'API di archiviazione .NET direttamente con una tabella</span><span class="sxs-lookup"><span data-stu-id="08e81-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="08e81-135">È possibile usare l'attributo **Tabella** anche con un oggetto **CloudTable** per una maggiore flessibilità nell'uso di una tabella.</span><span class="sxs-lookup"><span data-stu-id="08e81-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="08e81-136">Il seguente esempio di codice usa un oggetto **CloudTable** per aggiungere una singola entità alla tabella *Ingresso* .</span><span class="sxs-lookup"><span data-stu-id="08e81-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="08e81-137">Per altre informazioni su come usare l'oggetto **CloudTable** , vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="08e81-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="08e81-138">Argomenti correlati trattati nell'articolo delle procedure sulle code</span><span class="sxs-lookup"><span data-stu-id="08e81-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="08e81-139">Per informazioni su come gestire l'elaborazione di tabelle attivata da un messaggio di coda o per scenari di WebJobs SDK non legati all'elaborazione di tabelle, vedere [Introduzione all'archiviazione di accodamento di Azure e ai servizi relativi a Visual Studio (progetti WebJob)](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="08e81-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08e81-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08e81-140">Next steps</span></span>
<span data-ttu-id="08e81-141">Questo articolo ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="08e81-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="08e81-142">Per altre informazioni su come usare Processi Web di Azure e WebJobs SDK, vedere le [risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="08e81-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

