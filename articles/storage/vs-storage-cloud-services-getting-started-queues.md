---
title: aaaGet avviato con Visual Studio e l'archiviazione delle code di servizi connessi (servizi cloud) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzando l'archiviazione delle code di Azure in un progetto di servizio cloud in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
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
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introduzione all’archiviazione di accodamento di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questo articolo descrive la modalità di avvio con l'archiviazione delle code di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto di servizi cloud con Visual Studio hello tooget **aggiungere servizi connessi** finestra di dialogo .

Vi mostreremo come toocreate una coda nel codice. È inoltre mostreremo come tooperform basic coda operazioni, ad esempio aggiunta, modifica, lettura e la rimozione messaggi in coda. esempi di Hello vengono scritti in codice c# e usano hello [Microsoft Azure Storage Client Library per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.

* Per altre informazioni sulla modifica delle code a livello di codice, vedere [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md) .
* Vedere [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.
* Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.
* Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.

Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.

## <a name="access-queues-in-code"></a>Code di accesso nel codice
le code tooaccess nei progetti di Visual Studio Cloud Services, è necessario seguente hello tooinclude file di origine c# tooany gli elementi che l'archiviazione delle code di Azure di accedere.

1. Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Ottenere un **CloudQueueClient** tooreference hello coda oggetti nell'account di archiviazione di oggetti.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Ottenere un **CloudQueue** tooreference una coda specifica dell'oggetto.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Nota:** utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.

## <a name="create-a-queue-in-code"></a>Creare una coda in codice
coda di hello toocreate nel codice, è sufficiente aggiungere una chiamata troppo**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Aggiungere una coda di messaggi tooa
tooinsert un messaggio in una coda esistente, creare un nuovo **CloudQueueMessage** oggetto, quindi chiamata hello **AddMessage** metodo.

È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.

Di seguito è riportato un esempio che inserisce il messaggio hello "Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Leggere un messaggio in una coda
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessage** metodo.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Leggere e rimuovere un messaggio in una coda
Il codice può rimuovere un messaggio da una coda in due passaggi.

1. Chiamare **GetMessage** tooget hello successivo messaggio della coda. Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.
2. messaggio hello di rimozione dalla coda di hello, chiamata toofinish **DeleteMessage**.

Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. codice Hello seguente chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Utilizzare le opzioni aggiuntive tooprocess e rimuovere i messaggi in coda
È possibile personalizzare il recupero di messaggi da una coda in due modi.

* È possibile ottenere un batch di messaggi (in alto too32).
* È possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **foreach** . Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio. Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.

Ad esempio:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Ottiene la lunghezza della coda hello
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello. Hello **ApproximateMethodCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Utilizzare hello modello Async-Await con API comuni coda di Azure
Questo esempio mostra come serie di hello toouse Async-Await con API comuni coda di Azure. esempio Hello chiama versione asincrona di hello di ogni dato metodi hello, può essere visto da hello **Async** post-correzione di ogni metodo. Quando un metodo asincrono è usato hello async-await modello sospende l'esecuzione locale fino al completamento hello chiamata. Questo comportamento consente hello corrente thread toodo altro lavoro che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello. Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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

## <a name="delete-a-queue"></a>Eliminare una coda
una coda e tutti i messaggi hello contenuti al suo interno, chiamata hello toodelete **eliminare** metodo hello dell'oggetto di coda.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

