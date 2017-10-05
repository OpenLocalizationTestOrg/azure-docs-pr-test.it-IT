---
title: Introduzione all'archiviazione code e ai Servizi connessi di Visual Studio (servizi cloud) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione di coda in un progetto di servizio di cloud in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio.
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: d0e6e3eab312f169b1d05ba16e2e293e103df1ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="813f4-103">Introduzione all’archiviazione di accodamento di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="813f4-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="813f4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="813f4-104">Overview</span></span>
<span data-ttu-id="813f4-105">Questo articolo descrive come iniziare a usare l'archiviazione code di Azure in Visual Studio dopo aver creato o fatto riferimento a un account di archiviazione di Azure in un progetto servizio cloud usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="813f4-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="813f4-106">Verrà mostrato come creare una coda nel codice.</span><span class="sxs-lookup"><span data-stu-id="813f4-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="813f4-107">Infine verrà mostrato come eseguire operazioni relative alle code di base, come l'aggiunta, la modifica, la lettura e la rimozione di messaggi delle code.</span><span class="sxs-lookup"><span data-stu-id="813f4-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="813f4-108">Negli esempi, scritti in codice C#, viene usata la [libreria client di Archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="813f4-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="813f4-109">L'operazione **Aggiungi servizi connessi** consente di installare i pacchetti NuGet appropriati per accedere all'archiviazione di Azure nel progetto e di aggiungere la stringa di connessione per l'account di archiviazione ai file di configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="813f4-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="813f4-110">Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="813f4-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="813f4-111">Vedere [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="813f4-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="813f4-112">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="813f4-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="813f4-113">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="813f4-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="813f4-114">Il servizio di archiviazione di accodamento di Azure consente di archiviare grandi quantità di messaggi ai quali è possibile accedere da qualsiasi parte del mondo mediante chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="813f4-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="813f4-115">La dimensione massima di un singolo messaggio della coda è di 64 KB e una coda può contenere milioni di messaggi, nei limiti della capacità complessiva di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="813f4-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="813f4-116">Code di accesso nel codice</span><span class="sxs-lookup"><span data-stu-id="813f4-116">Access queues in code</span></span>
<span data-ttu-id="813f4-117">Per accedere alle code nei progetti Servizi cloud di Visual Studio, è necessario aggiungere i seguenti elementi a un file di origine C# che accede all’archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="813f4-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="813f4-118">Assicurarsi che le dichiarazioni dello spazio dei nomi all'inizio del file C# includano queste istruzioni **using** .</span><span class="sxs-lookup"><span data-stu-id="813f4-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="813f4-119">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="813f4-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="813f4-120">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="813f4-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="813f4-121">Ottenere un oggetto **CloudQueueClient** per fare riferimento agli oggetti delle code nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="813f4-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="813f4-122">Ottenere un oggetto **CloudQueue** per fare riferimento a una coda specifica.</span><span class="sxs-lookup"><span data-stu-id="813f4-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="813f4-123">**NOTA:** utilizzare tutto il codice riportato in precedenza prima del codice indicato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="813f4-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="813f4-124">Creare una coda in codice</span><span class="sxs-lookup"><span data-stu-id="813f4-124">Create a queue in code</span></span>
<span data-ttu-id="813f4-125">Per creare la coda nel codice, è sufficiente aggiungere una chiamata a **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="813f4-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="813f4-126">Aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="813f4-126">Add a message to a queue</span></span>
<span data-ttu-id="813f4-127">Per inserire un messaggio in una coda esistente, creare un nuovo oggetto **CloudQueueMessage**, quindi chiamare il metodo **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="813f4-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="813f4-128">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="813f4-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="813f4-129">Di seguito è riportato un esempio che inserisce il messaggio "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="813f4-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="813f4-130">Leggere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="813f4-130">Read a message in a queue</span></span>
<span data-ttu-id="813f4-131">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="813f4-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="813f4-132">Leggere e rimuovere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="813f4-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="813f4-133">Il codice può rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="813f4-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="813f4-134">Chiamare **GetMessage** per ottenere il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="813f4-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="813f4-135">Un messaggio restituito da **GetMessage** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="813f4-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="813f4-136">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="813f4-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="813f4-137">Per completare la rimozione del messaggio dalla coda, chiamare **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="813f4-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="813f4-138">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="813f4-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="813f4-139">Il codice seguente chiama **DeleteMessage** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="813f4-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="813f4-140">Utilizzare opzioni aggiuntive per elaborare e rimuovere i messaggi in coda</span><span class="sxs-lookup"><span data-stu-id="813f4-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="813f4-141">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="813f4-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="813f4-142">È possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="813f4-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="813f4-143">È possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="813f4-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="813f4-144">Nell'esempio di codice seguente viene utilizzato il metodo **GetMessages** per recuperare 20 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="813f4-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="813f4-145">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="813f4-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="813f4-146">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="813f4-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="813f4-147">Si noti che i cinque minuti iniziano per tutti i messaggi contemporaneamente, quindi dopo che sono trascorsi cinque minuti dalla chiamata a **GetMessages**, tutti i messaggi che non sono stati eliminati diventano nuovamente visibili.</span><span class="sxs-lookup"><span data-stu-id="813f4-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="813f4-148">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="813f4-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="813f4-149">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="813f4-149">Get the queue length</span></span>
<span data-ttu-id="813f4-150">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="813f4-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="813f4-151">Il metodo **FetchAttributes** chiede al servizio di accodamento di recuperare gli attributi della coda, incluso il numero di messaggi.</span><span class="sxs-lookup"><span data-stu-id="813f4-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="813f4-152">La proprietà **ApproximateMethodCount** restituisce l'ultimo valore recuperato dal metodo **FetchAttributes**, senza chiamare il servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="813f4-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="813f4-153">Utilizzare il modello Async-Await con le API comuni di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="813f4-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="813f4-154">In questo esempio viene illustrato come utilizzare il modello Async-Await con API di accodamento di Azure comuni.</span><span class="sxs-lookup"><span data-stu-id="813f4-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="813f4-155">Nell'esempio viene chiamata la versione asincrona di ogni metodo specificato. Ciò può essere osservato dal suffisso **Async** di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="813f4-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="813f4-156">Quando un metodo asincrono viene utilizzato, il modello async-await sospende l'esecuzione locale fino al completamento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="813f4-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="813f4-157">Questo comportamento consente al thread corrente di eseguire altre attività per evitare colli di bottiglia delle prestazioni e migliora la velocità di risposta complessiva dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="813f4-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="813f4-158">Per ulteriori informazioni sull'utilizzo del modello Async-Await in .NET, vedere [Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="813f4-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="813f4-159">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="813f4-159">Delete a queue</span></span>
<span data-ttu-id="813f4-160">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **Elimina** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="813f4-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="813f4-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="813f4-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

