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
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Introduzione all'archiviazione code e ai servizi connessi di Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questo articolo descrive la modalità di avvio con l'archiviazione delle code di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando Visual Studio hello tooget **aggiungere servizi connessi** finestra di dialogo. Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.

L'archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. Può essere un messaggio nella coda singolo backup too64 kilobyte (KB) e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.

tooget avviato, è necessario innanzitutto toocreate una coda di Azure nell'account di archiviazione. Vi mostreremo come toocreate una coda nel codice. È inoltre mostreremo come tooperform basic coda operazioni, ad esempio aggiunta, modifica, lettura e la rimozione di messaggi in coda. Hello esempi sono scritti in C\# del codice e utilizzare hello Azure Storage Client Library per .NET. Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).

**Nota:** alcune delle API che eseguono chiamate tooAzure archiviazione in ASP.NET Core hello sono asincrone. Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) . codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.

* Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .
* Vedere la [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.
* Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.
* Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.

## <a name="access-queues-in-code"></a>Code di accesso nel codice
le code tooaccess nei progetti ASP.NET Core, è necessario seguente hello tooinclude file di origine elementi tooany c# che accede all'archiviazione di coda di Azure.

1. Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Ottenere un **CloudQueueClient** tooreference hello coda oggetti nell'account di archiviazione di oggetti.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Ottenere un **CloudQueue** tooreference una coda specifica dell'oggetto.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Nota:** utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.

### <a name="create-a-queue-in-code"></a>Creare una coda in codice
hello toocreate coda di Azure nel codice, è sufficiente aggiungere una chiamata troppo**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Aggiungere una coda di messaggi tooa
tooinsert un messaggio in una coda esistente, creare un nuovo **CloudQueueMessage** oggetto, quindi chiamata hello **AddMessageAsync** metodo.

È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.

Di seguito è riportato un esempio che inserisce il messaggio hello "Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Leggere un messaggio in una coda
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessageAsync** metodo.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Leggere e rimuovere un messaggio in una coda
Il codice può rimuovere un messaggio da una coda in due passaggi.

1. Chiamare **GetMessageAsync** tooget hello successivo messaggio della coda. Un messaggio restituito da **GetMessageAsync** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.
2. messaggio hello di rimozione dalla coda di hello, chiamata toofinish **DeleteMessageAsync**.

Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. codice Hello seguente chiama **DeleteMessageAsync** subito dopo il messaggio hello è stato elaborato.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>Utilizzare opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi.
In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **foreach** . Imposta inoltre hello invisibilità timeout too5 in minuti per ogni messaggio. Si noti che hello iniziale di 5 minuti per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti trascorsi dopo la chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati nuovamente visibile.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Ottiene la lunghezza della coda hello
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello. Hello **ApproximateMethodCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Usare il modello di hello Async-Await comune coda API
Questo esempio mostra come toouse hello Async-Await modello con le API di coda comuni. versione di async hello per le chiamate di esempio Hello di ogni dato metodi hello. Può essere considerato dalla post-correzione di Async hello di ogni metodo. Quando viene utilizzato un metodo asincrono, modello Async-Await hello sospende l'esecuzione locale finché non viene completata la chiamata hello. Questo comportamento consente hello corrente thread toodo altro lavoro che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello. Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET, vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
## <a name="delete-a-queue"></a>Eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare** metodo hello dell'oggetto di coda.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

