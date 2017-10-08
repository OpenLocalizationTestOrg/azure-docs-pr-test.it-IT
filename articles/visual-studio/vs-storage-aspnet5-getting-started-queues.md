---
title: aaaGet avviato con l'archiviazione delle code e Visual Studio (ASP.NET Core) di servizi connessi | Documenti Microsoft
description: "La modalità di avvio tooget utilizzando l'archiviazione delle code di Azure in un progetto ASP.NET Core in Visual Studio"
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
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="ece7f-103">Introduzione all'archiviazione code e ai servizi connessi di Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="ece7f-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="ece7f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ece7f-104">Overview</span></span>
<span data-ttu-id="ece7f-105">Questo articolo descrive la modalità di avvio con l'archiviazione delle code di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando Visual Studio hello tooget **aggiungere servizi connessi** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ece7f-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="ece7f-106">Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.</span><span class="sxs-lookup"><span data-stu-id="ece7f-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="ece7f-107">L'archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ece7f-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="ece7f-108">Può essere un messaggio nella coda singolo backup too64 kilobyte (KB) e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ece7f-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="ece7f-109">tooget avviato, è necessario innanzitutto toocreate una coda di Azure nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ece7f-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="ece7f-110">Vi mostreremo come toocreate una coda nel codice.</span><span class="sxs-lookup"><span data-stu-id="ece7f-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="ece7f-111">È inoltre mostreremo come tooperform basic coda operazioni, ad esempio aggiunta, modifica, lettura e la rimozione di messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="ece7f-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="ece7f-112">Hello esempi sono scritti in C\# del codice e utilizzare hello Azure Storage Client Library per .NET.</span><span class="sxs-lookup"><span data-stu-id="ece7f-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="ece7f-113">Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="ece7f-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="ece7f-114">**Nota:** alcune delle API che eseguono chiamate tooAzure archiviazione in ASP.NET Core hello sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="ece7f-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="ece7f-115">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ece7f-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="ece7f-116">codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.</span><span class="sxs-lookup"><span data-stu-id="ece7f-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="ece7f-117">Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="ece7f-117">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="ece7f-118">Vedere la [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ece7f-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="ece7f-119">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="ece7f-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="ece7f-120">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ece7f-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="ece7f-121">Code di accesso nel codice</span><span class="sxs-lookup"><span data-stu-id="ece7f-121">Access queues in code</span></span>
<span data-ttu-id="ece7f-122">le code tooaccess nei progetti ASP.NET Core, è necessario seguente hello tooinclude file di origine elementi tooany c# che accede all'archiviazione di coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="ece7f-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="ece7f-123">Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ece7f-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="ece7f-124">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ece7f-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ece7f-125">Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="ece7f-126">Ottenere un **CloudQueueClient** tooreference hello coda oggetti nell'account di archiviazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="ece7f-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="ece7f-127">Ottenere un **CloudQueue** tooreference una coda specifica dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ece7f-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="ece7f-128">**Nota:** utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="ece7f-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="ece7f-129">Creare una coda in codice</span><span class="sxs-lookup"><span data-stu-id="ece7f-129">Create a queue in code</span></span>
<span data-ttu-id="ece7f-130">hello toocreate coda di Azure nel codice, è sufficiente aggiungere una chiamata troppo**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="ece7f-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="ece7f-131">Aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="ece7f-131">Add a message tooa queue</span></span>
<span data-ttu-id="ece7f-132">tooinsert un messaggio in una coda esistente, creare un nuovo **CloudQueueMessage** oggetto, quindi chiamata hello **AddMessageAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="ece7f-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="ece7f-133">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="ece7f-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="ece7f-134">Di seguito è riportato un esempio che inserisce il messaggio hello "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="ece7f-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="ece7f-135">Leggere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="ece7f-135">Read a message in a queue</span></span>
<span data-ttu-id="ece7f-136">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessageAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="ece7f-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="ece7f-137">Leggere e rimuovere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="ece7f-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="ece7f-138">Il codice può rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="ece7f-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="ece7f-139">Chiamare **GetMessageAsync** tooget hello successivo messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="ece7f-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="ece7f-140">Un messaggio restituito da **GetMessageAsync** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="ece7f-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="ece7f-141">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="ece7f-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="ece7f-142">messaggio hello di rimozione dalla coda di hello, chiamata toofinish **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="ece7f-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="ece7f-143">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="ece7f-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="ece7f-144">codice Hello seguente chiama **DeleteMessageAsync** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="ece7f-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="ece7f-145">Utilizzare opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="ece7f-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="ece7f-146">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="ece7f-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="ece7f-147">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="ece7f-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="ece7f-148">In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="ece7f-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="ece7f-149">codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="ece7f-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="ece7f-150">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="ece7f-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="ece7f-151">Imposta inoltre hello invisibilità timeout too5 in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="ece7f-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="ece7f-152">Si noti che hello iniziale di 5 minuti per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti trascorsi dopo la chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati nuovamente visibile.</span><span class="sxs-lookup"><span data-stu-id="ece7f-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="ece7f-153">Ottiene la lunghezza della coda hello</span><span class="sxs-lookup"><span data-stu-id="ece7f-153">Get hello queue length</span></span>
<span data-ttu-id="ece7f-154">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="ece7f-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="ece7f-155">Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="ece7f-156">Hello **ApproximateMethodCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="ece7f-157">Usare il modello di hello Async-Await comune coda API</span><span class="sxs-lookup"><span data-stu-id="ece7f-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="ece7f-158">Questo esempio mostra come toouse hello Async-Await modello con le API di coda comuni.</span><span class="sxs-lookup"><span data-stu-id="ece7f-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="ece7f-159">versione di async hello per le chiamate di esempio Hello di ogni dato metodi hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="ece7f-160">Può essere considerato dalla post-correzione di Async hello di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="ece7f-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="ece7f-161">Quando viene utilizzato un metodo asincrono, modello Async-Await hello sospende l'esecuzione locale finché non viene completata la chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="ece7f-162">Questo comportamento consente hello corrente thread toodo altro lavoro che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ece7f-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="ece7f-163">Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET, vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="ece7f-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="ece7f-164">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="ece7f-164">Delete a queue</span></span>
<span data-ttu-id="ece7f-165">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="ece7f-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="ece7f-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ece7f-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

