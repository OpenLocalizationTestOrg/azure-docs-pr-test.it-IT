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
# <a name="how-toouse-queue-storage-from-java"></a>Come toouse l'archiviazione delle code da Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure. esempi di Hello sono scritti in Java e usano hello [Azure Storage SDK per Java][Azure Storage SDK for Java]. Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **creazione di** e **eliminazione** code. Per ulteriori informazioni sulle code, vedere hello [passaggi successivi](#Next-Steps) sezione.

Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico. Per ulteriori informazioni, vedere hello [Azure Storage SDK per Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creare un'applicazione Java
In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.

toodo in tal caso, sarà necessario tooinstall hello Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure. Dopo aver eseguito questa operazione, sarà necessario tooverify che il sistema di sviluppo soddisfi i requisiti minimi di hello e le dipendenze sono elencate in hello [Azure Storage SDK per Java] [ Azure Storage SDK for Java] repository in GitHub. Se il sistema soddisfi tali requisiti, è possibile seguire le istruzioni di hello per scaricare e installare le librerie di archiviazione di Azure hello for Java nel sistema da quel repository. Dopo aver completato queste attività, sarà in grado di toocreate un'applicazione Java che utilizza esempi hello in questo articolo.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurare l'archiviazione delle code dell'applicazione tooaccess
Aggiungere hello dopo l'inizio di toohello di istruzioni di importazione del file di Java hello in cui si desidera code tooaccess le API di archiviazione di Azure toouse:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello in hello seguente formato, utilizzando nome hello dell'account di archiviazione e chiave di accesso primaria per l'account di archiviazione hello elencati in hello hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori. In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In un'applicazione in esecuzione all'interno di un ruolo in Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio hello *ServiceConfiguration. cscfg*ed è possibile accedervi con una chiamata toohello  **RoleEnvironment.getConfigurationSettings** metodo. Di seguito è riportato un esempio di recupero della stringa di connessione hello da un **impostazione** elemento denominato *StorageConnectionString* nel file di configurazione del servizio hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.

## <a name="how-to-create-a-queue"></a>Procedura: creare una coda
Per ottenere oggetti di riferimento per le code, è possibile usare un oggetto **CloudQueueClient**. Hello codice seguente viene creata una **CloudQueueClient** oggetto. (Nota: esistono altri modi toocreate **CloudStorageAccount** oggetti; per ulteriori informazioni, vedere **CloudStorageAccount** in hello [Azure Storage Client SDK riferimento].)

Hello utilizzare **CloudQueueClient** tooget una coda di toohello di riferimento che si desidera toouse dell'oggetto. È possibile creare la coda hello se non esiste.

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

## <a name="how-to-add-a-message-tooa-queue"></a>Procedura: aggiungere una coda di messaggi tooa
tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **CloudQueueMessage**. Successivamente, chiamare hello **addMessage** metodo. È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte. Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World".

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

## <a name="how-to-peek-at-hello-next-message"></a>Procedura: leggere il messaggio hello successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello chiamando **peekMessage**.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedura: modificare hello contenuto di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello. Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello. Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi. Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello. È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software. In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare. In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.

esempio Hello le ricerche tramite coda hello dei messaggi di esempio di codice, individua primo messaggio hello che corrisponde a "Hello, World" per il contenuto di hello, quindi modifica il contenuto del messaggio hello e viene chiuso.

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

In alternativa, hello nell'esempio di codice seguente aggiorna solo hello prima visibile messaggio nella coda di hello.

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

## <a name="how-to-get-hello-queue-length"></a>Procedura: ottenere la lunghezza coda di hello
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Hello **downloadAttributes** metodo richiede il servizio di Accodamento hello per diversi valori correnti, incluso un conteggio del numero di messaggi è in una coda. conteggio Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo hello servizio di Accodamento risponde tooyour richiesta. Hello **getApproximateMessageCount** metodo restituisce l'ultimo valore hello recuperati dalla chiamata hello troppo**downloadAttributes**, senza chiamare il servizio di Accodamento di hello.

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

## <a name="how-to-dequeue-hello-next-message"></a>Procedura: rimozione dalla coda il messaggio hello successivo
Il codice consente di rimuovere un messaggio da una coda in due passaggi. Quando si chiama **retrieveMessage**, si messaggio hello successivo in una coda. Un messaggio restituito da **retrieveMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **deleteMessage**. Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. Il codice chiama **deleteMessage** subito dopo il messaggio hello è stato elaborato.

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

## <a name="additional-options-for-dequeuing-messages"></a>Opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi. In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.

esempio di codice seguente Hello utilizza hello **retrieveMessages** messaggi tooget 20 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **for** . Imposta inoltre hello invisibilità timeout toofive minuti (300 secondi per ogni messaggio). Si noti che hello cinque minuti viene avviato per tutti i messaggi in hello stesso tempo, pertanto quando cinque minuti passati dal chiamata hello troppo**retrieveMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.

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

## <a name="how-to-list-hello-queues"></a>Procedura: elencare code hello
un elenco di code corrente hello, chiamata hello tooobtain **CloudQueueClient.listQueues()** metodo, che restituisce una raccolta di **CloudQueue** oggetti.

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

## <a name="how-to-delete-a-queue"></a>Procedura: eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamata hello **deleteIfExists** metodo hello **CloudQueue** oggetto.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* [Azure Storage SDK per Java][Azure Storage SDK for Java]
* [Azure Storage Client SDK riferimento][Azure Storage Client SDK riferimento]
* [API REST dei servizi di archiviazione di Azure][Azure Storage Services REST API]
* [Blog del team di Archiviazione di Azure][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK riferimento]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
