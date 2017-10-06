---
title: l'archiviazione delle code toouse aaaHow (C++) | Documenti Microsoft
description: Informazioni su come toouse hello servizio di archiviazione delle code in Azure. Gli esempi sono scritti in C++.
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
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="be707-104">Come toouse l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="be707-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="be707-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="be707-105">Overview</span></span>
<span data-ttu-id="be707-106">Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="be707-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="be707-107">esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="be707-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="be707-108">Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="be707-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="be707-109">Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="be707-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="be707-110">Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="be707-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="be707-111">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="be707-111">Create a C++ application</span></span>
<span data-ttu-id="be707-112">In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="be707-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="be707-113">toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be707-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="be707-114">tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="be707-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="be707-115">**Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="be707-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="be707-116">**Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="be707-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="be707-117">Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="be707-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="be707-118">Configurare il tooaccess applicazione l'archiviazione delle code</span><span class="sxs-lookup"><span data-stu-id="be707-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="be707-119">Aggiungere il seguente hello includere hello C++ file in cui le code tooaccess toouse hello archiviazione Azure API cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="be707-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="be707-120">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="be707-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="be707-121">Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="be707-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="be707-122">Quando si esegue un'applicazione client, è necessario fornire stringa di connessione di archiviazione hello in hello seguente formato, utilizzando il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso di account di archiviazione hello elencato nella hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori.</span><span class="sxs-lookup"><span data-stu-id="be707-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="be707-123">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be707-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="be707-124">In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:</span><span class="sxs-lookup"><span data-stu-id="be707-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="be707-125">tootest l'applicazione nel computer locale di Windows, è possibile utilizzare Microsoft Azure hello [emulatore di archiviazione](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="be707-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="be707-126">emulatore di archiviazione Hello è un'utilità che simula hello Blob, coda e tabella servizi disponibili in Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="be707-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="be707-127">Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:</span><span class="sxs-lookup"><span data-stu-id="be707-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="be707-128">toostart hello emulatore di archiviazione Azure, seleziona hello **avviare** hello o preme **Windows** chiave.</span><span class="sxs-lookup"><span data-stu-id="be707-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="be707-129">Iniziare a digitare **emulatore di archiviazione Azure**e selezionare **emulatore di archiviazione di Microsoft Azure** elenco hello di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="be707-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="be707-130">Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="be707-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="be707-131">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="be707-131">Retrieve your connection string</span></span>
<span data-ttu-id="be707-132">È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="be707-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="be707-133">tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile usare hello **analizzare** metodo.</span><span class="sxs-lookup"><span data-stu-id="be707-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="be707-134">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="be707-134">How to: Create a queue</span></span>
<span data-ttu-id="be707-135">L'oggetto **cloud_queue_client** consente di ottenere oggetti di riferimento per le code.</span><span class="sxs-lookup"><span data-stu-id="be707-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="be707-136">Hello codice seguente viene creata una **cloud_queue_client** oggetto.</span><span class="sxs-lookup"><span data-stu-id="be707-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="be707-137">Hello utilizzare **cloud_queue_client** tooget una coda di toohello di riferimento che si desidera toouse dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="be707-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="be707-138">È possibile creare la coda hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="be707-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="be707-139">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="be707-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="be707-140">tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="be707-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="be707-141">Successivamente, chiamare hello **add_message** metodo.</span><span class="sxs-lookup"><span data-stu-id="be707-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="be707-142">È possibile creare un oggetto **cloud_queue_message** da una stringa o da una matrice di **byte**.</span><span class="sxs-lookup"><span data-stu-id="be707-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="be707-143">Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World":</span><span class="sxs-lookup"><span data-stu-id="be707-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="be707-144">Procedura: leggere il messaggio hello successivo</span><span class="sxs-lookup"><span data-stu-id="be707-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="be707-145">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek_message** metodo.</span><span class="sxs-lookup"><span data-stu-id="be707-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="be707-146">Procedura: modificare hello contenuto di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="be707-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="be707-147">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="be707-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="be707-148">Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="be707-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="be707-149">Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="be707-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="be707-150">Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="be707-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="be707-151">È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="be707-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="be707-152">In genere, è consigliabile mantenere un numero di tentativi anche, e se il messaggio hello viene ritentato più di n volte, è possibile eliminare.</span><span class="sxs-lookup"><span data-stu-id="be707-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="be707-153">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="be707-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="be707-154">Procedura: annullare l'accodamento messaggio successivo hello</span><span class="sxs-lookup"><span data-stu-id="be707-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="be707-155">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="be707-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="be707-156">Quando si chiama **get_message**, si messaggio hello successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="be707-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="be707-157">Un messaggio restituito da **get_message** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="be707-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="be707-158">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="be707-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="be707-159">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="be707-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="be707-160">Il codice chiama **delete_message** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="be707-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="be707-161">Procedura: usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="be707-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="be707-162">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="be707-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="be707-163">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="be707-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="be707-164">In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="be707-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="be707-165">esempio di codice seguente Hello utilizza hello **get_messages** messaggi tooget 20 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="be707-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="be707-166">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="be707-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="be707-167">Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="be707-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="be707-168">Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**get_messages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="be707-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="be707-169">Procedura: ottenere la lunghezza coda di hello</span><span class="sxs-lookup"><span data-stu-id="be707-169">How to: Get hello queue length</span></span>
<span data-ttu-id="be707-170">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="be707-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="be707-171">Hello **download_attributes** metodo chiede hello coda servizio tooretrieve hello coda gli attributi, inclusi il numero di messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="be707-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="be707-172">Hello **approximate_message_count** metodo ottiene il numero approssimativo di messaggi hello nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="be707-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="be707-173">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="be707-173">How to: Delete a queue</span></span>
<span data-ttu-id="be707-174">una coda e tutti i messaggi hello contenuti al suo interno, chiamata hello toodelete **delete_queue_if_exists** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="be707-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="be707-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be707-175">Next steps</span></span>
<span data-ttu-id="be707-176">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be707-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="be707-177">Come toouse archiviazione Blob da C++</span><span class="sxs-lookup"><span data-stu-id="be707-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="be707-178">Come toouse archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="be707-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="be707-179">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="be707-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="be707-180">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="be707-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="be707-181">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="be707-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)