---
title: aaaGet avviato con Visual Studio e l'archiviazione delle code di servizi connessi (servizi cloud) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzando l'archiviazione delle code di Azure in un progetto di servizio cloud in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="20b79-103">Introduzione all’archiviazione di accodamento di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="20b79-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="20b79-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="20b79-104">Overview</span></span>
<span data-ttu-id="20b79-105">Questo articolo descrive la modalità di avvio con l'archiviazione delle code di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto di servizi cloud con Visual Studio hello tooget **aggiungere servizi connessi** finestra di dialogo .</span><span class="sxs-lookup"><span data-stu-id="20b79-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="20b79-106">Vi mostreremo come toocreate una coda nel codice.</span><span class="sxs-lookup"><span data-stu-id="20b79-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="20b79-107">È inoltre mostreremo come tooperform basic coda operazioni, ad esempio aggiunta, modifica, lettura e la rimozione messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="20b79-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="20b79-108">esempi di Hello vengono scritti in codice c# e usano hello [Microsoft Azure Storage Client Library per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="20b79-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="20b79-109">Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.</span><span class="sxs-lookup"><span data-stu-id="20b79-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="20b79-110">Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="20b79-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="20b79-111">Vedere [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="20b79-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="20b79-112">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="20b79-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="20b79-113">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="20b79-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="20b79-114">Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="20b79-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="20b79-115">Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="20b79-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="20b79-116">Code di accesso nel codice</span><span class="sxs-lookup"><span data-stu-id="20b79-116">Access queues in code</span></span>
<span data-ttu-id="20b79-117">le code tooaccess nei progetti di Visual Studio Cloud Services, è necessario seguente hello tooinclude file di origine c# tooany gli elementi che l'archiviazione delle code di Azure di accedere.</span><span class="sxs-lookup"><span data-stu-id="20b79-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="20b79-118">Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.</span><span class="sxs-lookup"><span data-stu-id="20b79-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="20b79-119">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="20b79-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="20b79-120">Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="20b79-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="20b79-121">Ottenere un **CloudQueueClient** tooreference hello coda oggetti nell'account di archiviazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="20b79-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="20b79-122">Ottenere un **CloudQueue** tooreference una coda specifica dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="20b79-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="20b79-123">**Nota:** utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="20b79-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="20b79-124">Creare una coda in codice</span><span class="sxs-lookup"><span data-stu-id="20b79-124">Create a queue in code</span></span>
<span data-ttu-id="20b79-125">coda di hello toocreate nel codice, è sufficiente aggiungere una chiamata troppo**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="20b79-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="20b79-126">Aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="20b79-126">Add a message tooa queue</span></span>
<span data-ttu-id="20b79-127">tooinsert un messaggio in una coda esistente, creare un nuovo **CloudQueueMessage** oggetto, quindi chiamata hello **AddMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="20b79-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="20b79-128">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="20b79-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="20b79-129">Di seguito è riportato un esempio che inserisce il messaggio hello "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="20b79-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="20b79-130">Leggere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="20b79-130">Read a message in a queue</span></span>
<span data-ttu-id="20b79-131">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="20b79-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="20b79-132">Leggere e rimuovere un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="20b79-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="20b79-133">Il codice può rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="20b79-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="20b79-134">Chiamare **GetMessage** tooget hello successivo messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="20b79-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="20b79-135">Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="20b79-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="20b79-136">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="20b79-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="20b79-137">messaggio hello di rimozione dalla coda di hello, chiamata toofinish **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="20b79-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="20b79-138">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="20b79-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="20b79-139">codice Hello seguente chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="20b79-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="20b79-140">Utilizzare le opzioni aggiuntive tooprocess e rimuovere i messaggi in coda</span><span class="sxs-lookup"><span data-stu-id="20b79-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="20b79-141">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="20b79-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="20b79-142">È possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="20b79-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="20b79-143">È possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="20b79-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="20b79-144">codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="20b79-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="20b79-145">Quindi, ogni messaggio viene elaborato con un ciclo **foreach** .</span><span class="sxs-lookup"><span data-stu-id="20b79-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="20b79-146">Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="20b79-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="20b79-147">Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="20b79-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="20b79-148">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="20b79-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="20b79-149">Ottiene la lunghezza della coda hello</span><span class="sxs-lookup"><span data-stu-id="20b79-149">Get hello queue length</span></span>
<span data-ttu-id="20b79-150">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="20b79-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="20b79-151">Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="20b79-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="20b79-152">Hello **ApproximateMethodCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="20b79-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="20b79-153">Utilizzare hello modello Async-Await con API comuni coda di Azure</span><span class="sxs-lookup"><span data-stu-id="20b79-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="20b79-154">Questo esempio mostra come serie di hello toouse Async-Await con API comuni coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="20b79-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="20b79-155">esempio Hello chiama versione asincrona di hello di ogni dato metodi hello, può essere visto da hello **Async** post-correzione di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="20b79-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="20b79-156">Quando un metodo asincrono è usato hello async-await modello sospende l'esecuzione locale fino al completamento hello chiamata.</span><span class="sxs-lookup"><span data-stu-id="20b79-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="20b79-157">Questo comportamento consente hello corrente thread toodo altro lavoro che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="20b79-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="20b79-158">Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="20b79-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="20b79-159">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="20b79-159">Delete a queue</span></span>
<span data-ttu-id="20b79-160">una coda e tutti i messaggi hello contenuti al suo interno, chiamata hello toodelete **eliminare** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="20b79-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="20b79-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20b79-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

