---
title: aaaHow toouse l'archiviazione delle code da Java | Documenti Microsoft
description: Informazioni su come toouse hello Azure coda servizio toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in Java.
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="f1e06-104">Come toouse l'archiviazione delle code da Java</span><span class="sxs-lookup"><span data-stu-id="f1e06-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="f1e06-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f1e06-105">Overview</span></span>
<span data-ttu-id="f1e06-106">Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e06-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="f1e06-107">esempi di Hello sono scritti in Java e usano hello [Azure Storage SDK per Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="f1e06-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="f1e06-108">Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **creazione di** e **eliminazione** code.</span><span class="sxs-lookup"><span data-stu-id="f1e06-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="f1e06-109">Per ulteriori informazioni sulle code, vedere hello [passaggi successivi](#Next-Steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="f1e06-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="f1e06-110">Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico.</span><span class="sxs-lookup"><span data-stu-id="f1e06-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="f1e06-111">Per ulteriori informazioni, vedere hello [Azure Storage SDK per Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="f1e06-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="f1e06-112">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="f1e06-112">Create a Java application</span></span>
<span data-ttu-id="f1e06-113">In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e06-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="f1e06-114">toodo in tal caso, sarà necessario tooinstall hello Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e06-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="f1e06-115">Dopo aver eseguito questa operazione, sarà necessario tooverify che il sistema di sviluppo soddisfi i requisiti minimi di hello e le dipendenze sono elencate in hello [Azure Storage SDK per Java] [ Azure Storage SDK for Java] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="f1e06-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="f1e06-116">Se il sistema soddisfi tali requisiti, è possibile seguire le istruzioni di hello per scaricare e installare le librerie di archiviazione di Azure hello for Java nel sistema da quel repository.</span><span class="sxs-lookup"><span data-stu-id="f1e06-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="f1e06-117">Dopo aver completato queste attività, sarà in grado di toocreate un'applicazione Java che utilizza esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f1e06-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="f1e06-118">Configurare l'archiviazione delle code dell'applicazione tooaccess</span><span class="sxs-lookup"><span data-stu-id="f1e06-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="f1e06-119">Aggiungere hello dopo l'inizio di toohello di istruzioni di importazione del file di Java hello in cui si desidera code tooaccess le API di archiviazione di Azure toouse:</span><span class="sxs-lookup"><span data-stu-id="f1e06-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="f1e06-120">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f1e06-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="f1e06-121">Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f1e06-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f1e06-122">Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello in hello seguente formato, utilizzando nome hello dell'account di archiviazione e chiave di accesso primaria per l'account di archiviazione hello elencati in hello hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori.</span><span class="sxs-lookup"><span data-stu-id="f1e06-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f1e06-123">In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:</span><span class="sxs-lookup"><span data-stu-id="f1e06-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="f1e06-124">In un'applicazione in esecuzione all'interno di un ruolo in Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio hello *ServiceConfiguration. cscfg*ed è possibile accedervi con una chiamata toohello  **RoleEnvironment.getConfigurationSettings** metodo.</span><span class="sxs-lookup"><span data-stu-id="f1e06-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="f1e06-125">Di seguito è riportato un esempio di recupero della stringa di connessione hello da un **impostazione** elemento denominato *StorageConnectionString* nel file di configurazione del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="f1e06-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="f1e06-126">Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f1e06-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f1e06-127">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="f1e06-127">How to: Create a queue</span></span>
<span data-ttu-id="f1e06-128">Per ottenere oggetti di riferimento per le code, è possibile usare un oggetto **CloudQueueClient**.</span><span class="sxs-lookup"><span data-stu-id="f1e06-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="f1e06-129">Hello codice seguente viene creata una **CloudQueueClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="f1e06-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="f1e06-130">(Nota: esistono altri modi toocreate **CloudStorageAccount** oggetti; per ulteriori informazioni, vedere **CloudStorageAccount** in hello [Azure Storage Client SDK riferimento].)</span><span class="sxs-lookup"><span data-stu-id="f1e06-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="f1e06-131">Hello utilizzare **CloudQueueClient** tooget una coda di toohello di riferimento che si desidera toouse dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="f1e06-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="f1e06-132">È possibile creare la coda hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="f1e06-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="f1e06-133">Procedura: aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="f1e06-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="f1e06-134">tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="f1e06-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="f1e06-135">Successivamente, chiamare hello **addMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="f1e06-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="f1e06-136">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="f1e06-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="f1e06-137">Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="f1e06-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="f1e06-138">Procedura: leggere il messaggio hello successivo</span><span class="sxs-lookup"><span data-stu-id="f1e06-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="f1e06-139">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello chiamando **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="f1e06-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="f1e06-140">Procedura: modificare hello contenuto di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="f1e06-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="f1e06-141">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e06-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="f1e06-142">Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="f1e06-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="f1e06-143">Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="f1e06-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="f1e06-144">Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="f1e06-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="f1e06-145">È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="f1e06-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="f1e06-146">In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare.</span><span class="sxs-lookup"><span data-stu-id="f1e06-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="f1e06-147">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="f1e06-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="f1e06-148">esempio Hello le ricerche tramite coda hello dei messaggi di esempio di codice, individua primo messaggio hello che corrisponde a "Hello, World" per il contenuto di hello, quindi modifica il contenuto del messaggio hello e viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="f1e06-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="f1e06-149">In alternativa, hello nell'esempio di codice seguente aggiorna solo hello prima visibile messaggio nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e06-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="f1e06-150">Procedura: ottenere la lunghezza coda di hello</span><span class="sxs-lookup"><span data-stu-id="f1e06-150">How to: Get hello queue length</span></span>
<span data-ttu-id="f1e06-151">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="f1e06-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="f1e06-152">Hello **downloadAttributes** metodo richiede il servizio di Accodamento hello per diversi valori correnti, incluso un conteggio del numero di messaggi è in una coda.</span><span class="sxs-lookup"><span data-stu-id="f1e06-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="f1e06-153">conteggio Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo hello servizio di Accodamento risponde tooyour richiesta.</span><span class="sxs-lookup"><span data-stu-id="f1e06-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="f1e06-154">Hello **getApproximateMessageCount** metodo restituisce l'ultimo valore hello recuperati dalla chiamata hello troppo**downloadAttributes**, senza chiamare il servizio di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e06-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="f1e06-155">Procedura: rimozione dalla coda il messaggio hello successivo</span><span class="sxs-lookup"><span data-stu-id="f1e06-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="f1e06-156">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="f1e06-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="f1e06-157">Quando si chiama **retrieveMessage**, si messaggio hello successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="f1e06-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="f1e06-158">Un messaggio restituito da **retrieveMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f1e06-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="f1e06-159">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="f1e06-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f1e06-160">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="f1e06-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="f1e06-161">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="f1e06-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="f1e06-162">Il codice chiama **deleteMessage** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="f1e06-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="f1e06-163">Opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="f1e06-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="f1e06-164">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="f1e06-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="f1e06-165">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="f1e06-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="f1e06-166">In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="f1e06-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="f1e06-167">esempio di codice seguente Hello utilizza hello **retrieveMessages** messaggi tooget 20 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="f1e06-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="f1e06-168">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="f1e06-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="f1e06-169">Imposta inoltre hello invisibilità timeout toofive minuti (300 secondi per ogni messaggio).</span><span class="sxs-lookup"><span data-stu-id="f1e06-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="f1e06-170">Si noti che hello cinque minuti viene avviato per tutti i messaggi in hello stesso tempo, pertanto quando cinque minuti passati dal chiamata hello troppo**retrieveMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f1e06-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="f1e06-171">Procedura: elencare code hello</span><span class="sxs-lookup"><span data-stu-id="f1e06-171">How to: List hello queues</span></span>
<span data-ttu-id="f1e06-172">un elenco di code corrente hello, chiamata hello tooobtain **CloudQueueClient.listQueues()** metodo, che restituisce una raccolta di **CloudQueue** oggetti.</span><span class="sxs-lookup"><span data-stu-id="f1e06-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f1e06-173">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="f1e06-173">How to: Delete a queue</span></span>
<span data-ttu-id="f1e06-174">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamata hello **deleteIfExists** metodo hello **CloudQueue** oggetto.</span><span class="sxs-lookup"><span data-stu-id="f1e06-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="f1e06-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1e06-175">Next steps</span></span>
<span data-ttu-id="f1e06-176">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="f1e06-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="f1e06-177">[Azure Storage SDK per Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="f1e06-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="f1e06-178">[Azure Storage Client SDK riferimento][Azure Storage Client SDK riferimento]</span><span class="sxs-lookup"><span data-stu-id="f1e06-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="f1e06-179">[API REST dei servizi di archiviazione di Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="f1e06-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="f1e06-180">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="f1e06-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK riferimento]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
