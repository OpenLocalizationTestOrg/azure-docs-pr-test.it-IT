---
title: Introduzione all'archiviazione code di Azure con .NET | Documentazione Microsoft
description: Le code di Azure forniscono una messaggistica asincrona affidabile tra i componenti dell'applicazione. La messaggistica cloud consente di ridimensionare i componenti dell'applicazione in modo indipendente.
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
ms.openlocfilehash: 7f88aa9c50e669d1be7248346c7b1176bce61249
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="17d27-104">Introduzione all'archiviazione code di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="17d27-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="17d27-105">Overview</span><span class="sxs-lookup"><span data-stu-id="17d27-105">Overview</span></span>
<span data-ttu-id="17d27-106">L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17d27-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="17d27-107">Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="17d27-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="17d27-108">L'archivio code fornisce la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, che possono essere eseguiti nel cloud, in un desktop, in un server locale o in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="17d27-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="17d27-109">Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.</span><span class="sxs-lookup"><span data-stu-id="17d27-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="17d27-110">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="17d27-110">About this tutorial</span></span>
<span data-ttu-id="17d27-111">Questa esercitazione illustra come scrivere codice .NET per alcuni scenari comuni dell'archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="17d27-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="17d27-112">Gli scenari presentati includono creazione ed eliminazione di code, nonché aggiunta, lettura ed eliminazione di messaggi nella coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="17d27-113">**Tempo previsto per il completamento:** 45 minuti</span><span class="sxs-lookup"><span data-stu-id="17d27-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="17d27-114">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="17d27-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="17d27-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17d27-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="17d27-116">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="17d27-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="17d27-117">Gestione configurazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="17d27-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="17d27-118">Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="17d27-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="17d27-119">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="17d27-119">Add using directives</span></span>
<span data-ttu-id="17d27-120">Aggiungere le direttive `using` seguenti all'inizio del file `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="17d27-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="17d27-121">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="17d27-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="17d27-122">Creare il client del servizio di accodamento</span><span class="sxs-lookup"><span data-stu-id="17d27-122">Create the Queue service client</span></span>
<span data-ttu-id="17d27-123">La classe **CloudQueueClient** consente di recuperare le code archiviate nell'archivio code.</span><span class="sxs-lookup"><span data-stu-id="17d27-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="17d27-124">Ecco come creare il client del servizio:</span><span class="sxs-lookup"><span data-stu-id="17d27-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="17d27-125">A questo punto si è pronti a scrivere codice che legge e scrive i dati nell'archivio code.</span><span class="sxs-lookup"><span data-stu-id="17d27-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="17d27-126">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="17d27-126">Create a queue</span></span>
<span data-ttu-id="17d27-127">Questo esempio illustra come creare una coda, se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="17d27-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="17d27-128">Inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="17d27-128">Insert a message into a queue</span></span>
<span data-ttu-id="17d27-129">Per inserire un messaggio in una coda esistente, creare innanzitutto un nuovo oggetto **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="17d27-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="17d27-130">Quindi, chiamare il metodo **AddMessage** .</span><span class="sxs-lookup"><span data-stu-id="17d27-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="17d27-131">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di **byte**.</span><span class="sxs-lookup"><span data-stu-id="17d27-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="17d27-132">Di seguito è riportato il codice che consente di creare una coda (se non esiste già) e di inserire il messaggio 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="17d27-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="17d27-133">Visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="17d27-133">Peek at the next message</span></span>
<span data-ttu-id="17d27-134">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="17d27-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="17d27-135">Cambiare il contenuto di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="17d27-135">Change the contents of a queued message</span></span>
<span data-ttu-id="17d27-136">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="17d27-137">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questa funzionalità per aggiornarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="17d27-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="17d27-138">Il codice seguente consente di aggiornare il messaggio in coda con nuovo contenuto e di impostarne il timeout di visibilità per prolungarlo di altri 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="17d27-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="17d27-139">In questo modo lo stato del lavoro associato al messaggio viene salvato e il client ha a disposizione un altro minuto per continuare l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="17d27-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="17d27-140">È possibile usare questa tecnica per tenere traccia di flussi di lavoro composti da più passaggi nei messaggi in coda, senza la necessità di ricominciare dall'inizio se un passaggio di elaborazione non riesce a causa di errori hardware o software.</span><span class="sxs-lookup"><span data-stu-id="17d27-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="17d27-141">In genere, è consigliabile mantenere anche un conteggio dei tentativi, in modo da eliminare i messaggi per cui vengono effettuati più di *n* tentativi.</span><span class="sxs-lookup"><span data-stu-id="17d27-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="17d27-142">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="17d27-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="17d27-143">Rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="17d27-143">De-queue the next message</span></span>
<span data-ttu-id="17d27-144">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="17d27-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="17d27-145">Chiamando **GetMessage**, si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="17d27-146">Un messaggio restituito da **GetMessage** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="17d27-147">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="17d27-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="17d27-148">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="17d27-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="17d27-149">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="17d27-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="17d27-150">Il codice chiama **DeleteMessage** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="17d27-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="17d27-151">Utilizzare il modello Async-Await modello con API comuni di archiviazione coda</span><span class="sxs-lookup"><span data-stu-id="17d27-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="17d27-152">In questo esempio viene illustrato come utilizzare il modello Async-Await con API comuni di archiviazione coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="17d27-153">Nell'esempio viene chiamata la versione asincrona di ogni metodo specificato, come indicato dal suffisso *Async* di ciascun metodo.</span><span class="sxs-lookup"><span data-stu-id="17d27-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="17d27-154">Quando un metodo asincrono viene utilizzato, il modello async-await sospende l'esecuzione locale fino al completamento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="17d27-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="17d27-155">Questo comportamento consente al thread corrente di eseguire altre attività per evitare colli di bottiglia delle prestazioni e migliora la velocità di risposta complessiva dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17d27-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="17d27-156">Per ulteriori informazioni sull'utilizzo del modello Async-Await in .NET, vedere [Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="17d27-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="17d27-157">Usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="17d27-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="17d27-158">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="17d27-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="17d27-159">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="17d27-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="17d27-160">In secondo luogo, è possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="17d27-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="17d27-161">Nell'esempio di codice seguente viene utilizzato il metodo **GetMessages** per recuperare 20 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="17d27-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="17d27-162">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="17d27-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="17d27-163">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="17d27-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="17d27-164">Si noti che i cinque minuti iniziano per tutti i messaggi contemporaneamente, quindi dopo che sono trascorsi cinque minuti dalla chiamata a **GetMessages**, tutti i messaggi che non sono stati eliminati diventano nuovamente visibili.</span><span class="sxs-lookup"><span data-stu-id="17d27-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="17d27-165">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="17d27-165">Get the queue length</span></span>
<span data-ttu-id="17d27-166">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="17d27-167">Il metodo **FetchAttributes** chiede al servizio di accodamento di recuperare gli attributi della coda, incluso il numero di messaggi.</span><span class="sxs-lookup"><span data-stu-id="17d27-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="17d27-168">La proprietà **ApproximateMessageCount** restituisce l'ultimo valore recuperato dal metodo **FetchAttributes**, senza chiamare il servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="17d27-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="17d27-169">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="17d27-169">Delete a queue</span></span>
<span data-ttu-id="17d27-170">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **Elimina** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="17d27-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="17d27-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17d27-171">Next steps</span></span>
<span data-ttu-id="17d27-172">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione di accodamento, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="17d27-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="17d27-173">Per informazioni dettagliate sulle API disponibili, vedere la documentazione di riferimento del servizio di accodamento:</span><span class="sxs-lookup"><span data-stu-id="17d27-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="17d27-174">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="17d27-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="17d27-175">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="17d27-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="17d27-176">Per altre informazioni su come semplificare il codice scritto da usare con Archiviazione di Azure, vedere [Informazioni su Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="17d27-177">Per ulteriori opzioni di archiviazione dei dati in Azure, consultare altre guide alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="17d27-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="17d27-178">[Introduzione all'archiviazione tabelle di Azure con .NET](storage-dotnet-how-to-use-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="17d27-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="17d27-179">[Introduzione all'archivio BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="17d27-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="17d27-180">Per archiviare i dati relazionali, vedere [Connettersi al database SQL tramite .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
