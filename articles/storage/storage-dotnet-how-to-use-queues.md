---
title: aaaGet avviato con l'archiviazione delle code di Azure usando .NET | Documenti Microsoft
description: Le code di Azure forniscono una messaggistica asincrona affidabile tra i componenti dell'applicazione. Cloud della messaggistica consentono il tooscale componenti dell'applicazione in modo indipendente.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="d409c-104">Introduzione all'archiviazione code di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="d409c-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="d409c-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d409c-105">Overview</span></span>
<span data-ttu-id="d409c-106">L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d409c-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="d409c-107">Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="d409c-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="d409c-108">L'archiviazione delle code recapita la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, se sono in esecuzione nel cloud hello, sul desktop di hello, in un server locale o in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="d409c-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="d409c-109">Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.</span><span class="sxs-lookup"><span data-stu-id="d409c-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="d409c-110">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="d409c-110">About this tutorial</span></span>
<span data-ttu-id="d409c-111">Questa esercitazione viene illustrato come toowrite .NET codice in alcuni scenari comuni tramite l'archiviazione delle code di Azure.</span><span class="sxs-lookup"><span data-stu-id="d409c-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="d409c-112">Gli scenari presentati includono creazione ed eliminazione di code, nonché aggiunta, lettura ed eliminazione di messaggi nella coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="d409c-113">**Toocomplete tempo stimato:** 45 minuti</span><span class="sxs-lookup"><span data-stu-id="d409c-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="d409c-114">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="d409c-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="d409c-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d409c-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="d409c-116">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="d409c-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="d409c-117">Gestione configurazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="d409c-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="d409c-118">Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d409c-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="d409c-119">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="d409c-119">Add using directives</span></span>
<span data-ttu-id="d409c-120">Aggiungere il seguente hello `using` hello cima toohello direttive `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="d409c-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="d409c-121">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="d409c-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="d409c-122">Creare hello client del servizio coda</span><span class="sxs-lookup"><span data-stu-id="d409c-122">Create hello Queue service client</span></span>
<span data-ttu-id="d409c-123">Hello **CloudQueueClient** classe consente di tooretrieve code archiviate in archiviazione di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="d409c-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="d409c-124">Ecco un modo toocreate client del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="d409c-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="d409c-125">Si è ora pronto toowrite codice che legge i dati da e scrive tooQueue archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="d409c-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="d409c-126">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="d409c-126">Create a queue</span></span>
<span data-ttu-id="d409c-127">Questo esempio viene illustrato come toocreate una coda se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="d409c-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="d409c-128">Inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="d409c-128">Insert a message into a queue</span></span>
<span data-ttu-id="d409c-129">tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="d409c-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="d409c-130">Successivamente, chiamare hello **AddMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="d409c-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="d409c-131">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di **byte**.</span><span class="sxs-lookup"><span data-stu-id="d409c-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="d409c-132">Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World":</span><span class="sxs-lookup"><span data-stu-id="d409c-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="d409c-133">Leggere il messaggio hello successivo</span><span class="sxs-lookup"><span data-stu-id="d409c-133">Peek at hello next message</span></span>
<span data-ttu-id="d409c-134">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="d409c-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="d409c-135">Modificare il contenuto di hello di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="d409c-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="d409c-136">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="d409c-137">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questo tooupdate funzionalità lo stato dell'attività di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="d409c-138">Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="d409c-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="d409c-139">Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="d409c-140">È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="d409c-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="d409c-141">In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare.</span><span class="sxs-lookup"><span data-stu-id="d409c-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d409c-142">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d409c-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="d409c-143">Annullato l'accodamento messaggio successivo hello</span><span class="sxs-lookup"><span data-stu-id="d409c-143">De-queue hello next message</span></span>
<span data-ttu-id="d409c-144">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="d409c-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="d409c-145">Quando si chiama **GetMessage**, si messaggio hello successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="d409c-146">Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="d409c-147">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="d409c-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="d409c-148">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d409c-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="d409c-149">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="d409c-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="d409c-150">Il codice chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="d409c-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="d409c-151">Utilizzare il modello Async-Await modello con API comuni di archiviazione coda</span><span class="sxs-lookup"><span data-stu-id="d409c-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="d409c-152">Questo esempio mostra come hello toouse Async-Await criterio con le API comuni di archiviazione della coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="d409c-153">esempio Hello chiama versione asincrona di hello di ogni hello ha metodi, come indicato dal hello *Async* suffisso di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="d409c-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="d409c-154">Quando viene utilizzato un metodo asincrono, hello async-await modello sospende l'esecuzione locale fino al completamento hello chiamata.</span><span class="sxs-lookup"><span data-stu-id="d409c-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="d409c-155">Questo comportamento consente hello corrente thread toodo altro lavoro, che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="d409c-156">Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="d409c-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="d409c-157">Usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="d409c-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="d409c-158">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="d409c-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="d409c-159">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="d409c-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="d409c-160">In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="d409c-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="d409c-161">codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="d409c-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="d409c-162">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="d409c-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="d409c-163">Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="d409c-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="d409c-164">Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d409c-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="d409c-165">Ottiene la lunghezza della coda hello</span><span class="sxs-lookup"><span data-stu-id="d409c-165">Get hello queue length</span></span>
<span data-ttu-id="d409c-166">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="d409c-167">Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="d409c-168">Hello **ApproximateMessageCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="d409c-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="d409c-169">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="d409c-169">Delete a queue</span></span>
<span data-ttu-id="d409c-170">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="d409c-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="d409c-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d409c-171">Next steps</span></span>
<span data-ttu-id="d409c-172">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="d409c-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="d409c-173">Visualizzare la documentazione di riferimento di hello coda del servizio per informazioni dettagliate sulle API disponibili:</span><span class="sxs-lookup"><span data-stu-id="d409c-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="d409c-174">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="d409c-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="d409c-175">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="d409c-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="d409c-176">Informazioni su come codice hello toosimplify scrivere toowork con archiviazione di Azure tramite hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d409c-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="d409c-177">Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="d409c-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="d409c-178">[Introduzione all'archiviazione tabelle di Azure usando .NET](storage-dotnet-how-to-use-tables.md) toostore dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="d409c-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) toostore structured data.</span></span>
  * <span data-ttu-id="d409c-179">[Introduzione all'archiviazione Blob di Azure usando .NET](storage-dotnet-how-to-use-blobs.md) toostore dati non strutturati.</span><span class="sxs-lookup"><span data-stu-id="d409c-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="d409c-180">[Connettersi con .NET (c#) tooSQL Database](../sql-database/sql-database-develop-dotnet-simple.md) toostore di dati relazionali.</span><span class="sxs-lookup"><span data-stu-id="d409c-180">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
