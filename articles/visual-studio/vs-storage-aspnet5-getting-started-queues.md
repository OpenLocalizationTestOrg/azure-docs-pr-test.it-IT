---
title: Introduzione all'archiviazione code e ai servizi connessi di Visual Studio (ASP.NET Core) | Microsoft Docs
description: Informazioni su come iniziare a usare l'archiviazione code di Azure in un progetto ASP.NET Core in Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 394344c0e126472b97c2e8f721c8c8d6514a17dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="45be6-103">Introduzione all'archiviazione code e ai servizi connessi di Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="45be6-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="45be6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="45be6-104">Overview</span></span>
<span data-ttu-id="45be6-105">In questo articolo viene descritto come iniziare a usare l'archiviazione code di Azure in Visual Studio dopo aver creato o fatto riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45be6-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="45be6-106">L'operazione **Aggiungi servizi connessi** consente di installare i pacchetti NuGet appropriati per accedere all'archiviazione di Azure nel progetto e di aggiungere la stringa di connessione per l'account di archiviazione ai file di configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="45be6-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="45be6-107">Il servizio di archiviazione di accodamento di Azure consente di archiviare grandi quantità di messaggi ai quali è possibile accedere da qualsiasi parte del mondo mediante chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="45be6-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="45be6-108">La dimensione massima di un singolo messaggio della coda è di 64 KB e una coda può contenere milioni di messaggi, nei limiti della capacità complessiva di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45be6-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="45be6-109">Per iniziare, è innanzitutto necessario creare una coda di Azure nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45be6-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="45be6-110">Verrà mostrato come creare una coda nel codice.</span><span class="sxs-lookup"><span data-stu-id="45be6-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="45be6-111">Infine verrà mostrato come eseguire operazioni relative alle code di base, come l'aggiunta, la modifica, la lettura e la rimozione di messaggi delle code.</span><span class="sxs-lookup"><span data-stu-id="45be6-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="45be6-112">Negli esempi, scritti in codice C\# viene usata la libreria client di Archiviazione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="45be6-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="45be6-113">Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="45be6-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="45be6-114">**NOTA:** alcune API che eseguono chiamate ad Archiviazione di Azure in ASP.NET Core sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="45be6-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="45be6-115">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="45be6-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="45be6-116">Nel codice riportato di seguito si presuppone vengano utilizzati i metodi di programmazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="45be6-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="45be6-117">Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="45be6-117">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="45be6-118">Vedere la [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45be6-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="45be6-119">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="45be6-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="45be6-120">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="45be6-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="45be6-121">Code di accesso nel codice</span><span class="sxs-lookup"><span data-stu-id="45be6-121">Access queues in code</span></span>
<span data-ttu-id="45be6-122">Per accedere alle code nei progetti ASP.NET Core, è necessario includere gli elementi seguenti ai file di origine C# che consentono di accedere all'archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="45be6-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="45be6-123">Assicurarsi che le dichiarazioni dello spazio dei nomi all'inizio del file C# includano queste istruzioni **using** .</span><span class="sxs-lookup"><span data-stu-id="45be6-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="45be6-124">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45be6-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="45be6-125">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="45be6-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="45be6-126">Ottenere un oggetto **CloudQueueClient** per fare riferimento agli oggetti delle code nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45be6-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="45be6-127">Ottenere un oggetto **CloudQueue** per fare riferimento a una coda specifica.</span><span class="sxs-lookup"><span data-stu-id="45be6-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="45be6-128">**NOTA:** utilizzare tutto il codice riportato in precedenza prima del codice indicato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="45be6-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="45be6-129">Creare una coda in codice</span><span class="sxs-lookup"><span data-stu-id="45be6-129">Create a queue in code</span></span>
<span data-ttu-id="45be6-130">Per creare la coda nel codice, è sufficiente aggiungere una chiamata a **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="45be6-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="45be6-131">Aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="45be6-131">Add a message to a queue</span></span>
<span data-ttu-id="45be6-132">Per inserire un messaggio in una coda esistente, creare un nuovo oggetto **CloudQueueMessage**, quindi chiamare il metodo **AddMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="45be6-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="45be6-133">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="45be6-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="45be6-134">Di seguito è riportato un esempio che inserisce il messaggio "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="45be6-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="45be6-135">Leggere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="45be6-135">Read a message in a queue</span></span>
<span data-ttu-id="45be6-136">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **PeekMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="45be6-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="45be6-137">Leggere e rimuovere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="45be6-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="45be6-138">Il codice può rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="45be6-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="45be6-139">Chiamare **GetMessageAsync** per ottenere il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="45be6-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="45be6-140">Un messaggio restituito da **GetMessageAsync** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="45be6-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="45be6-141">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="45be6-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="45be6-142">Per completare la rimozione del messaggio dalla coda, chiamare **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="45be6-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="45be6-143">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="45be6-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="45be6-144">Il codice seguente chiama **DeleteMessageAsync** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="45be6-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="45be6-145">Utilizzare opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="45be6-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="45be6-146">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="45be6-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="45be6-147">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="45be6-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="45be6-148">In secondo luogo, è possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="45be6-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="45be6-149">Nell'esempio di codice seguente viene utilizzato il metodo **GetMessages** per recuperare 20 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="45be6-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="45be6-150">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="45be6-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="45be6-151">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="45be6-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="45be6-152">Si noti che i 5 minuti iniziano per tutti i messaggi contemporaneamente, quindi dopo che sono trascorsi 5 minuti dalla chiamata a **GetMessages**tutti i messaggi che non sono stati eliminati diventano nuovamente visibili.</span><span class="sxs-lookup"><span data-stu-id="45be6-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="45be6-153">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="45be6-153">Get the queue length</span></span>
<span data-ttu-id="45be6-154">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="45be6-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="45be6-155">Il metodo **FetchAttributes** chiede al servizio di accodamento di recuperare gli attributi della coda, incluso il numero di messaggi.</span><span class="sxs-lookup"><span data-stu-id="45be6-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="45be6-156">La proprietà **ApproximateMethodCount** restituisce l'ultimo valore recuperato dal metodo **FetchAttributes**, senza chiamare il servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="45be6-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="45be6-157">Utilizzare il modello Async-Await con API delle code comuni</span><span class="sxs-lookup"><span data-stu-id="45be6-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="45be6-158">In questo esempio viene illustrato come utilizzare il modello Async-Await con API delle code comuni.</span><span class="sxs-lookup"><span data-stu-id="45be6-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="45be6-159">L'esempio chiama la versione asincrona di ogni metodo specificato.</span><span class="sxs-lookup"><span data-stu-id="45be6-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="45be6-160">Può essere visto dalla post-correzione di Async di ciascun metodo.</span><span class="sxs-lookup"><span data-stu-id="45be6-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="45be6-161">Quando un metodo asincrono viene utilizzato, il modello async-await sospende l'esecuzione locale fino al completamento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="45be6-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="45be6-162">Questo comportamento consente al thread corrente di eseguire altre attività per evitare colli di bottiglia delle prestazioni e migliora la velocità di risposta complessiva dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45be6-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="45be6-163">Per ulteriori informazioni sull'utilizzo del modello Async-Await in .NET, vedere [Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="45be6-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="45be6-164">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="45be6-164">Delete a queue</span></span>
<span data-ttu-id="45be6-165">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **Elimina** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="45be6-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="45be6-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45be6-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

