---
title: aaaGet avviato con l'archiviazione delle code di Azure usando .NET | Documenti Microsoft
description: Le code di Azure forniscono una messaggistica asincrona affidabile tra i componenti dell'applicazione. Cloud della messaggistica consentono il tooscale componenti dell'applicazione in modo indipendente.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Introduzione all'archiviazione code di Azure con .NET
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Overview
L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione. Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente. L'archiviazione delle code recapita la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, se sono in esecuzione nel cloud hello, sul desktop di hello, in un server locale o in un dispositivo mobile. Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.

### <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
Questa esercitazione viene illustrato come toowrite .NET codice in alcuni scenari comuni tramite l'archiviazione delle code di Azure. Gli scenari presentati includono creazione ed eliminazione di code, nonché aggiunta, lettura ed eliminazione di messaggi nella coda.

**Toocomplete tempo stimato:** 45 minuti

**Prerequisiti:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestione configurazione di Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Aggiungere le direttive using
Aggiungere il seguente hello `using` hello cima toohello direttive `Program.cs` file:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Analizzare la stringa di connessione hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Creare hello client del servizio coda
Hello **CloudQueueClient** classe consente di tooretrieve code archiviate in archiviazione di Accodamento. Ecco un modo toocreate client del servizio hello:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Si è ora pronto toowrite codice che legge i dati da e scrive tooQueue archiviazione dei dati.

## <a name="create-a-queue"></a>Creare una coda
Questo esempio viene illustrato come toocreate una coda se non esiste già:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Inserire un messaggio in una coda
tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **CloudQueueMessage**. Successivamente, chiamare hello **AddMessage** metodo. È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di **byte**. Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World":

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Leggere il messaggio hello successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **PeekMessage** metodo.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>Modificare il contenuto di hello di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello. Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questo tooupdate funzionalità lo stato dell'attività di lavoro hello. Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi. Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello. È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software. In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare. In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>Annullato l'accodamento messaggio successivo hello
Il codice consente di rimuovere un messaggio da una coda in due passaggi. Quando si chiama **GetMessage**, si messaggio hello successivo in una coda. Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **DeleteMessage**. Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. Il codice chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Utilizzare il modello Async-Await modello con API comuni di archiviazione coda
Questo esempio mostra come hello toouse Async-Await criterio con le API comuni di archiviazione della coda. esempio Hello chiama versione asincrona di hello di ogni hello ha metodi, come indicato dal hello *Async* suffisso di ogni metodo. Quando viene utilizzato un metodo asincrono, hello async-await modello sospende l'esecuzione locale fino al completamento hello chiamata. Questo comportamento consente hello corrente thread toodo altro lavoro, che consente di evitare colli di bottiglia delle prestazioni e consente di migliorare le prestazioni complessive dell'applicazione hello. Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET vedere [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi.
In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. codice Hello seguente viene utilizzata la **GetMessages** messaggi tooget 20 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **foreach** . Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio. Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**GetMessages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Ottiene la lunghezza della coda hello
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Il **FetchAttributes** metodo richiede il servizio di Accodamento hello per recuperare gli attributi di coda hello, incluso il numero di messaggio hello. Hello **ApproximateMessageCount** proprietà restituisce l'ultimo valore hello recuperati tramite il **FetchAttributes** metodo, senza chiamare il servizio di Accodamento di hello.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare** metodo hello dell'oggetto di coda.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* Visualizzare la documentazione di riferimento di hello coda del servizio per informazioni dettagliate sulle API disponibili:
  * [Informazioni di riferimento sulla libreria client di archiviazione per .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Informazioni di riferimento sulle API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Informazioni su come codice hello toosimplify scrivere toowork con archiviazione di Azure tramite hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).
* Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.
  * [Introduzione all'archiviazione tabelle di Azure usando .NET](storage-dotnet-how-to-use-tables.md) toostore dati strutturati.
  * [Introduzione all'archiviazione Blob di Azure usando .NET](storage-dotnet-how-to-use-blobs.md) toostore dati non strutturati.
  * [Connettersi con .NET (c#) tooSQL Database](../sql-database/sql-database-develop-dotnet-simple.md) toostore di dati relazionali.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
