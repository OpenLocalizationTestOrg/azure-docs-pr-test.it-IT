---
title: Come usare l'archiviazione code da Java | Microsoft Docs
description: Informazioni su come usare il servizio di accodamento di Azure per creare ed eliminare code e per inserire, visualizzare ed eliminare messaggi. Gli esempi sono scritti in Java.
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
ms.openlocfilehash: 03faea986221453d1862ff0f0d6d1ec21f92f3bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="9c639-104">Come usare l'archiviazione di accodamento da Java</span><span class="sxs-lookup"><span data-stu-id="9c639-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="9c639-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9c639-105">Overview</span></span>
<span data-ttu-id="9c639-106">In questa guida verranno illustrati diversi scenari comuni di utilizzo del servizio di archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c639-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="9c639-107">Gli esempi sono scritti in Java e usano [Azure Storage SDK per Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="9c639-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="9c639-108">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre alla **creazione** ed **eliminazione** di code.</span><span class="sxs-lookup"><span data-stu-id="9c639-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="9c639-109">Per altre informazioni sulle code, vedere la sezione [Passaggi successivi](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="9c639-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="9c639-110">Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico.</span><span class="sxs-lookup"><span data-stu-id="9c639-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="9c639-111">Per altre informazioni, vedere [Azure Storage SDK per Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="9c639-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="9c639-112">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="9c639-112">Create a Java application</span></span>
<span data-ttu-id="9c639-113">In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.</span><span class="sxs-lookup"><span data-stu-id="9c639-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="9c639-114">A questo scopo, è necessario installare Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c639-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="9c639-115">Dopo avere eseguito questa operazione, sarà necessario verificare che il sistema di sviluppo in uso soddisfi i requisiti minimi e le dipendenze elencate nel repository [Azure Storage SDK per Java][Azure Storage SDK for Java] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c639-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="9c639-116">Se il sistema soddisfa i requisiti, è possibile seguire le istruzioni per scaricare e installare le librerie di archiviazione di Azure per Java nel sistema dall'archivio indicato.</span><span class="sxs-lookup"><span data-stu-id="9c639-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="9c639-117">Dopo avere completato queste attività, sarà possibile creare un'applicazione Java che usa gli esempi illustrati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9c639-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="9c639-118">Configurazione dell'applicazione per l'accesso all'archiviazione di accodamento</span><span class="sxs-lookup"><span data-stu-id="9c639-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="9c639-119">Aggiungere le istruzioni import seguenti all'inizio del file Java in cui si desidera usare le API di archiviazione di Azure per accedere alle code:</span><span class="sxs-lookup"><span data-stu-id="9c639-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="9c639-120">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9c639-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="9c639-121">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="9c639-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9c639-122">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente, usando il nome dell'account di archiviazione e la chiave di accesso primaria relativa all'account di archiviazione riportata nel [portale di Azure](https://portal.azure.com) per i valori *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="9c639-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9c639-123">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="9c639-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="9c639-124">In un'applicazione in esecuzione in un ruolo di Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio *ServiceConfiguration.cscfg*ed è accessibile con una chiamata al metodo **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="9c639-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="9c639-125">Nell'esempio seguente viene recuperata la stringa di connessione da un elemento **Setting** denominato *StorageConnectionString* nel file di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="9c639-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="9c639-126">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9c639-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9c639-127">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="9c639-127">How to: Create a queue</span></span>
<span data-ttu-id="9c639-128">Per ottenere oggetti di riferimento per le code, è possibile usare un oggetto **CloudQueueClient**.</span><span class="sxs-lookup"><span data-stu-id="9c639-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="9c639-129">Il codice seguente consente di creare un oggetto **CloudQueueClient**.</span><span class="sxs-lookup"><span data-stu-id="9c639-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="9c639-130">(Nota: esistono altri modi per creare oggetti **CloudStorageAccount**. Per altre informazioni, vedere **CloudStorageAccount** nel [Riferimento all'SDK del client di archiviazione di Azure]).</span><span class="sxs-lookup"><span data-stu-id="9c639-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="9c639-131">Usare l'oggetto **CloudQueueClient** t per ottenere un riferimento alla coda da usare.</span><span class="sxs-lookup"><span data-stu-id="9c639-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="9c639-132">È possibile creare la coda se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="9c639-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="9c639-133">Procedura: aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="9c639-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="9c639-134">Per inserire un messaggio in una coda esistente, creare innanzitutto un nuovo oggetto **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="9c639-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="9c639-135">Quindi, chiamare il metodo **addMessage** .</span><span class="sxs-lookup"><span data-stu-id="9c639-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="9c639-136">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="9c639-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="9c639-137">Di seguito è riportato il codice che consente di creare una coda (se non esiste già) e di inserire il messaggio "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="9c639-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="9c639-138">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="9c639-138">How to: Peek at the next message</span></span>
<span data-ttu-id="9c639-139">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="9c639-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="9c639-140">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="9c639-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="9c639-141">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="9c639-142">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questa funzionalità per aggiornarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="9c639-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="9c639-143">Il codice seguente consente di aggiornare il messaggio in coda con nuovo contenuto e di impostarne il timeout di visibilità per prolungarlo di altri 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="9c639-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="9c639-144">In questo modo lo stato del lavoro associato al messaggio viene salvato e il client ha a disposizione un altro minuto per continuare l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="9c639-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="9c639-145">È possibile usare questa tecnica per tenere traccia di flussi di lavoro composti da più passaggi nei messaggi in coda, senza la necessità di ricominciare dall'inizio se un passaggio di elaborazione non riesce a causa di errori hardware o software.</span><span class="sxs-lookup"><span data-stu-id="9c639-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="9c639-146">In genere, è consigliabile mantenere anche un conteggio dei tentativi, in modo da eliminare i messaggi per cui vengono effettuati più di *n* tentativi.</span><span class="sxs-lookup"><span data-stu-id="9c639-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="9c639-147">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="9c639-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="9c639-148">L'esempio di codice seguente consente di eseguire una ricerca nella coda di messaggi, individuare il primo messaggio con una corrispondenza di "Hello, World" per il contenuto, di modificare il contenuto del messaggio e infine di uscire.</span><span class="sxs-lookup"><span data-stu-id="9c639-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="9c639-149">In alternativa, l'esempio di codice seguente consente di aggiornare solo il primo messaggio visibile nella coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="9c639-150">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="9c639-150">How to: Get the queue length</span></span>
<span data-ttu-id="9c639-151">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="9c639-152">Il metodo **downloadAttributes** richiede al servizio di accodamento diversi valori correnti, incluso un conteggio dei messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="9c639-153">Il conteggio è solo approssimativo, poiché è possibile aggiungere o rimuovere messaggi dopo la risposta del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="9c639-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="9c639-154">Il metodo **getApproximateMessageCount** restituisce l'ultimo valore recuperato dalla chiamata a **downloadAttributes**, senza chiamare il servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="9c639-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="9c639-155">Procedura: rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="9c639-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="9c639-156">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="9c639-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="9c639-157">Chiamando il metodo **retrieveMessage**, si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="9c639-158">Un messaggio restituito da **retrieveMessage** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="9c639-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="9c639-159">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="9c639-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="9c639-160">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="9c639-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="9c639-161">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="9c639-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="9c639-162">Il codice chiama **deleteMessage** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="9c639-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="9c639-163">Opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="9c639-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="9c639-164">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="9c639-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="9c639-165">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="9c639-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="9c639-166">In secondo luogo, è possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="9c639-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="9c639-167">Nell'esempio di codice seguente viene usato il metodo **retrieveMessages** per recuperare 20 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="9c639-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="9c639-168">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="9c639-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="9c639-169">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti (300 secondi).</span><span class="sxs-lookup"><span data-stu-id="9c639-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="9c639-170">Si noti che i cinque minuti iniziano per tutti i messaggi contemporaneamente, quindi dopo che sono trascorsi cinque minuti dalla chiamata a **retrieveMessages**, tutti i messaggi che non sono stati eliminati diventano nuovamente visibili.</span><span class="sxs-lookup"><span data-stu-id="9c639-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="9c639-171">Procedura: elencare le code</span><span class="sxs-lookup"><span data-stu-id="9c639-171">How to: List the queues</span></span>
<span data-ttu-id="9c639-172">Per ottenere un elenco delle code correnti, chiamare il metodo **CloudQueueClient.listQueues()** che restituisce una raccolta di oggetti **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="9c639-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9c639-173">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="9c639-173">How to: Delete a queue</span></span>
<span data-ttu-id="9c639-174">Per eliminare una coda e tutti i messaggi in essa contenuti, chiamare il metodo **deleteIfExists** sull'oggetto **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="9c639-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="9c639-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c639-175">Next steps</span></span>
<span data-ttu-id="9c639-176">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione di accodamento, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="9c639-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="9c639-177">[Azure Storage SDK per Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="9c639-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="9c639-178">[Riferimento all'SDK del client di archiviazione di Azure][Riferimento all'SDK del client di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="9c639-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="9c639-179">[API REST dei servizi di archiviazione di Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="9c639-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="9c639-180">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="9c639-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="9c639-181">[Riferimento all'SDK del client di archiviazione di Azure]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="9c639-181">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
