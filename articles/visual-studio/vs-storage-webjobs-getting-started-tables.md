---
title: aaaGetting avviato con l'archiviazione di Azure e servizi di Visual Studio connesso (processo Web progetti)
description: "La modalità di avvio tooget utilizzando l'archiviazione tabelle di Azure in un progetto processi Web di Azure in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
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
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="9ba30-103">Introduzione all'Archiviazione di Azure (progetti Azure WebJob)</span><span class="sxs-lookup"><span data-stu-id="9ba30-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="9ba30-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9ba30-104">Overview</span></span>
<span data-ttu-id="9ba30-105">Questo articolo fornisce esempi di codice c# che mostrano mostrano come toouse hello Azure WebJobs SDK versione 1. x con il servizio di archiviazione tabelle di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ba30-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="9ba30-106">esempi di codice Hello utilizzano hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versione 1. x.</span><span class="sxs-lookup"><span data-stu-id="9ba30-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="9ba30-107">servizio di archiviazione tabelle Azure Hello consente toostore grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="9ba30-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="9ba30-108">servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba30-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="9ba30-109">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="9ba30-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="9ba30-110">Per altre informazioni, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) .</span><span class="sxs-lookup"><span data-stu-id="9ba30-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="9ba30-111">Alcuni dei frammenti di codice hello mostrano hello **tabella** attributo utilizzato nelle funzioni che vengono chiamate manualmente, vale a dire non utilizzando uno degli attributi di hello trigger.</span><span class="sxs-lookup"><span data-stu-id="9ba30-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="9ba30-112">La tabella di tooa tooadd entità</span><span class="sxs-lookup"><span data-stu-id="9ba30-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="9ba30-113">tabella tooa tooadd entità utilizzare hello **tabella** attributo con un **ICollector<T>**  o **IAsyncCollector<T>**  parametro dove **T** specifica dello schema hello di entità hello desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="9ba30-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="9ba30-114">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello della tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="9ba30-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="9ba30-115">Hello nell'esempio di codice seguente consente di aggiungere **persona** tabella tooa entità denominata *in ingresso*.</span><span class="sxs-lookup"><span data-stu-id="9ba30-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="9ba30-116">In genere hello tipo da utilizzare con **ICollector** deriva da **TableEntity** o implementa **ITableEntity**, ma non è necessario.</span><span class="sxs-lookup"><span data-stu-id="9ba30-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="9ba30-117">Uno dei seguenti hello **persona** le classi di lavoro con codice di hello di hello precedente **in ingresso** metodo.</span><span class="sxs-lookup"><span data-stu-id="9ba30-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="9ba30-118">Se si desidera toowork direttamente con hello API di archiviazione di Azure, è possibile aggiungere un **CloudStorageAccount** firma del metodo toohello parametro.</span><span class="sxs-lookup"><span data-stu-id="9ba30-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="9ba30-119">Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9ba30-119">Real-time monitoring</span></span>
<span data-ttu-id="9ba30-120">Poiché le funzioni in ingresso dei dati spesso elaborano grandi volumi di dati, hello dashboard WebJobs SDK fornisce i dati di monitoraggio in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="9ba30-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="9ba30-121">Hello **chiamata Log** sezione viene indicato se la funzione hello è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9ba30-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="9ba30-123">Hello **chiamata dettagli** pagina report hello lo stato di avanzamento della funzione (numero di entità scritta) durante l'esecuzione e offre un tooabort opportunità è.</span><span class="sxs-lookup"><span data-stu-id="9ba30-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="9ba30-125">Quando la funzione hello viene completata, hello **chiamata dettagli** pagina viene indicato il numero di hello di righe scritte.</span><span class="sxs-lookup"><span data-stu-id="9ba30-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Funzione Ingress completata](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="9ba30-127">Come tooread più entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="9ba30-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="9ba30-128">tooread una tabella, utilizzare hello **tabella** attributo con un **IQueryable<T>**  parametro in cui digitare **T** deriva da **TableEntity**o implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="9ba30-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="9ba30-129">legge Hello nell'esempio di codice seguente e i log di tutte le righe da hello **in ingresso** tabella:</span><span class="sxs-lookup"><span data-stu-id="9ba30-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="9ba30-130">Come tooread una singola entità da una tabella</span><span class="sxs-lookup"><span data-stu-id="9ba30-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="9ba30-131">È presente un **tabella** costruttore di attributo con due parametri aggiuntivi che consentono di specificare la chiave di partizione hello e chiave di riga quando si desidera toobind tooa tabella singola entità.</span><span class="sxs-lookup"><span data-stu-id="9ba30-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="9ba30-132">esempio di codice seguente Hello legge una riga della tabella per un **persona** entità in base a partizione chiave e riga di valori di chiave ricevuti in un messaggio nella coda:</span><span class="sxs-lookup"><span data-stu-id="9ba30-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="9ba30-133">Hello **persona** classe in questo esempio non dispone di tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="9ba30-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="9ba30-134">Come toouse hello API di archiviazione .NET direttamente toowork con una tabella</span><span class="sxs-lookup"><span data-stu-id="9ba30-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="9ba30-135">È inoltre possibile utilizzare hello **tabella** attributo con un **CloudTable** oggetto per una maggiore flessibilità durante l'utilizzo di una tabella.</span><span class="sxs-lookup"><span data-stu-id="9ba30-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="9ba30-136">codice Hello seguente viene utilizzata una **CloudTable** tooadd toohello una singola entità dell'oggetto *in ingresso* tabella.</span><span class="sxs-lookup"><span data-stu-id="9ba30-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="9ba30-137">Per ulteriori informazioni su come hello toouse **CloudTable** , vedere [Introduzione all'archiviazione tabelle di Azure usando .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9ba30-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="9ba30-138">Argomenti correlati coperti da hello code come-tooarticle</span><span class="sxs-lookup"><span data-stu-id="9ba30-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="9ba30-139">Per informazioni su come l'elaborazione tabella toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non è l'elaborazione, vedere specifiche tootable [Guida introduttiva a Visual Studio e l'archiviazione delle code di Azure connessa servizi (processo Web progetti) ](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="9ba30-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ba30-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ba30-140">Next steps</span></span>
<span data-ttu-id="9ba30-141">In questo articolo ha fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba30-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="9ba30-142">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse della documentazione di processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="9ba30-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

