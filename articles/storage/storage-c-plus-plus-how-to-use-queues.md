---
title: Come usare l'archiviazione code (C++) | Microsoft Docs
description: Informazioni su come usare il servizio di archiviazione delle code in Azure. Gli esempi sono scritti in C++.
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 85e4d95549ca5edd375f3b15971634e032a3962a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="9f749-104">Come usare l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="9f749-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9f749-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9f749-105">Overview</span></span>
<span data-ttu-id="9f749-106">In questa guida verranno illustrati diversi scenari comuni di utilizzo del servizio di archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f749-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="9f749-107">Gli esempi sono scritti in C++ e utilizzano la [libreria client di Archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="9f749-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="9f749-108">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre a **creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="9f749-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="9f749-109">Questa guida fa riferimento alla libreria client di Archiviazione di Azure per C++ versione 1.0.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="9f749-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="9f749-110">La versione consigliata per la libreria client di archiviazione è la 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="9f749-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="9f749-111">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="9f749-111">Create a C++ application</span></span>
<span data-ttu-id="9f749-112">In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="9f749-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="9f749-113">A tal fine, sarà necessario installare la libreria client di Archiviazione di Azure per C++ e creare un account di archiviazione Azure nella propria sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="9f749-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="9f749-114">Per installare la libreria client di Archiviazione di Azure per C++, è possibile utilizzare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9f749-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="9f749-115">**Linux:** seguire le istruzioni fornite nella pagina [README della libreria client di Archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="9f749-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="9f749-116">**Windows:** in Visual Studio, fare clic su **Strumenti > Gestione pacchetti NuGet > console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="9f749-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="9f749-117">Digitare il seguente comando nella [console Gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="9f749-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="9f749-118">Configurazione dell'applicazione per l’accesso ad Archiviazione di accodamento</span><span class="sxs-lookup"><span data-stu-id="9f749-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="9f749-119">Aggiungere le istruzioni include seguenti all'inizio del file C++ in cui si desidera utilizzare le API di archiviazione di Azure per accedere alle code:</span><span class="sxs-lookup"><span data-stu-id="9f749-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="9f749-120">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9f749-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="9f749-121">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="9f749-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9f749-122">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente, usando il nome dell'account di archiviazione e la chiave di accesso alle risorse di archiviazione per l'account di archiviazione elencato nel [portale di Azure](https://portal.azure.com) per i valori di *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="9f749-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9f749-123">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9f749-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="9f749-124">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="9f749-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="9f749-125">Per eseguire il test dell'applicazione nel computer Windows locale, è possibile usare l'[emulatore di archiviazione](storage-use-emulator.md) di Microsoft Azure installato con [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9f749-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="9f749-126">L'emulatore di archiviazione è un'utilità che simula i servizi BLOB, tabelle e di accodamento, disponibile in Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="9f749-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="9f749-127">Nell’esempio seguente viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione all’emulatore di archiviazione locale:</span><span class="sxs-lookup"><span data-stu-id="9f749-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="9f749-128">Per avviare l'emulatore di archiviazione di Azure, selezionare il pulsante **Start** o premere **WINDOWS** sulla tastiera.</span><span class="sxs-lookup"><span data-stu-id="9f749-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="9f749-129">Digitare **Emulatore di archiviazione di Azure** e selezionare **Emulatore di archiviazione di Microsoft Azure** nell'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9f749-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="9f749-130">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9f749-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="9f749-131">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="9f749-131">Retrieve your connection string</span></span>
<span data-ttu-id="9f749-132">Per visualizzare le informazioni dell'account di archiviazione, è possibile usare la classe **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="9f749-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="9f749-133">Per recuperare le informazioni sull'account di archiviazione dalla stringa di connessione alla risorsa di archiviazione, è possibile utilizzare il metodo **parse** .</span><span class="sxs-lookup"><span data-stu-id="9f749-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9f749-134">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="9f749-134">How to: Create a queue</span></span>
<span data-ttu-id="9f749-135">L'oggetto **cloud_queue_client** consente di ottenere oggetti di riferimento per le code.</span><span class="sxs-lookup"><span data-stu-id="9f749-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="9f749-136">Il codice seguente crea un oggetto **cloud_queue_client**.</span><span class="sxs-lookup"><span data-stu-id="9f749-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="9f749-137">Usare l'oggetto **cloud_queue_client** per ottenere un riferimento alla coda che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="9f749-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="9f749-138">È possibile creare la coda se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="9f749-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="9f749-139">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="9f749-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="9f749-140">Per inserire un messaggio in una coda esistente, creare prima un nuovo oggetto **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="9f749-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="9f749-141">Chiamare successivamente il metodo **add_message**.</span><span class="sxs-lookup"><span data-stu-id="9f749-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="9f749-142">È possibile creare un oggetto **cloud_queue_message** da una stringa o da una matrice di **byte**.</span><span class="sxs-lookup"><span data-stu-id="9f749-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="9f749-143">Di seguito è riportato il codice che consente di creare una coda (se non esiste già) e di inserire il messaggio 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="9f749-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="9f749-144">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="9f749-144">How to: Peek at the next message</span></span>
<span data-ttu-id="9f749-145">È possibile visualizzare il messaggio in testa a una coda senza rimuoverlo dalla coda chiamando il metodo **peek_message**.</span><span class="sxs-lookup"><span data-stu-id="9f749-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="9f749-146">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="9f749-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="9f749-147">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="9f749-148">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questa funzionalità per aggiornarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="9f749-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="9f749-149">Il codice seguente consente di aggiornare il messaggio in coda con nuovo contenuto e di impostarne il timeout di visibilità per prolungarlo di altri 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="9f749-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="9f749-150">In questo modo lo stato del lavoro associato al messaggio viene salvato e il client ha a disposizione un altro minuto per continuare l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="9f749-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="9f749-151">È possibile usare questa tecnica per tenere traccia di flussi di lavoro composti da più passaggi nei messaggi in coda, senza la necessità di ricominciare dall'inizio se un passaggio di elaborazione non riesce a causa di errori hardware o software.</span><span class="sxs-lookup"><span data-stu-id="9f749-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="9f749-152">In genere, è consigliabile mantenere anche un conteggio dei tentativi, in modo da eliminare i messaggi per cui vengono effettuati più di n tentativi.</span><span class="sxs-lookup"><span data-stu-id="9f749-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="9f749-153">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="9f749-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="9f749-154">Procedura: rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="9f749-154">How to: De-queue the next message</span></span>
<span data-ttu-id="9f749-155">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="9f749-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="9f749-156">Quando si chiama **get_message**, si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="9f749-157">Un messaggio restituito da **get_message** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="9f749-158">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="9f749-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="9f749-159">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="9f749-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="9f749-160">Il codice chiama **delete_message** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="9f749-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="9f749-161">Procedura: usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="9f749-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="9f749-162">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="9f749-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="9f749-163">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="9f749-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="9f749-164">In secondo luogo, è possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="9f749-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="9f749-165">Nell'esempio di codice seguente viene usato il metodo **get_messages** per recuperare 20 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="9f749-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="9f749-166">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="9f749-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="9f749-167">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="9f749-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="9f749-168">Si noti che il conteggio di 5 minuti viene iniziato per tutti i messaggi allo stesso tempo, per cui, dopo 5 minuti dalla chiamata a **get_messages**, tutti i messaggi che non sono stati eliminati diventano nuovamente visibili.</span><span class="sxs-lookup"><span data-stu-id="9f749-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="9f749-169">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="9f749-169">How to: Get the queue length</span></span>
<span data-ttu-id="9f749-170">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="9f749-171">Il metodo **download_attributes** chiede al servizio di accodamento di recuperare gli attributi della coda, incluso il numero di messaggi.</span><span class="sxs-lookup"><span data-stu-id="9f749-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="9f749-172">Il metodo **approximate_message_count** ottiene il numero approssimativo di messaggi nella coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9f749-173">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="9f749-173">How to: Delete a queue</span></span>
<span data-ttu-id="9f749-174">Per eliminare una coda e tutti i messaggi inclusi, chiamare il metodo **delete_queue_if_exists** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="9f749-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="9f749-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f749-175">Next steps</span></span>
<span data-ttu-id="9f749-176">A questo punto, dopo aver appreso le nozioni di base di Archiviazione accodamento, visitare i collegamenti seguenti per altre informazioni su Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f749-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="9f749-177">Come usare l’archiviazione BLOB da C++</span><span class="sxs-lookup"><span data-stu-id="9f749-177">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="9f749-178">Come usare l’archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="9f749-178">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="9f749-179">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="9f749-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="9f749-180">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="9f749-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="9f749-181">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9f749-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)