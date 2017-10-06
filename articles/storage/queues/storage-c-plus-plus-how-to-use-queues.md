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
# <a name="how-toouse-queue-storage-from-c"></a>Come toouse l'archiviazione delle code da C++
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure. esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.

> [!NOTE]
> Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive. Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creazione di un’applicazione C++
In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.

toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.

tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:

* **Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.
* **Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**. Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurare il tooaccess applicazione l'archiviazione delle code
Aggiungere il seguente hello includere hello C++ file in cui le code tooaccess toouse hello archiviazione Azure API cima toohello istruzioni:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Impostare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire stringa di connessione di archiviazione hello in hello seguente formato, utilizzando il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso di account di archiviazione hello elencato nella hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori. Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json). In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest l'applicazione nel computer locale di Windows, è possibile utilizzare Microsoft Azure hello [emulatore di archiviazione](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulatore di archiviazione Hello è un'utilità che simula hello Blob, coda e tabella servizi disponibili in Azure nel computer di sviluppo locale. Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello emulatore di archiviazione Azure, seleziona hello **avviare** hello o preme **Windows** chiave. Iniziare a digitare **emulatore di archiviazione Azure**e selezionare **emulatore di archiviazione di Microsoft Azure** elenco hello di applicazioni.

Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.

## <a name="retrieve-your-connection-string"></a>Recuperare la stringa di connessione
È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'Account di archiviazione. tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile usare hello **analizzare** metodo.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Procedura: creare una coda
L'oggetto **cloud_queue_client** consente di ottenere oggetti di riferimento per le code. Hello codice seguente viene creata una **cloud_queue_client** oggetto.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Hello utilizzare **cloud_queue_client** tooget una coda di toohello di riferimento che si desidera toouse dell'oggetto. È possibile creare la coda hello se non esiste.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedura: inserire un messaggio in una coda
tooinsert un messaggio in una coda esistente, creare innanzitutto un nuovo **cloud_queue_message**. Successivamente, chiamare hello **add_message** metodo. È possibile creare un oggetto **cloud_queue_message** da una stringa o da una matrice di **byte**. Ecco il codice che crea una coda (se non esiste) e il messaggio hello inserimenti "Hello, World":

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

## <a name="how-to-peek-at-hello-next-message"></a>Procedura: leggere il messaggio hello successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek_message** metodo.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedura: modificare hello contenuto di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello. Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello. Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e set hello tooextend timeout di visibilità di un altro 60 secondi. Questo consente di salvare lo stato di hello del lavoro associata al messaggio hello e assegna il client di hello un'altra toocontinue minuto lavorando messaggio hello. È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software. In genere, è consigliabile mantenere un numero di tentativi anche, e se il messaggio hello viene ritentato più di n volte, è possibile eliminare. In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.

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

## <a name="how-to-de-queue-hello-next-message"></a>Procedura: annullare l'accodamento messaggio successivo hello
Il codice consente di rimuovere un messaggio da una coda in due passaggi. Quando si chiama **get_message**, si messaggio hello successivo in una coda. Un messaggio restituito da **get_message** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **delete_message**. Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. Il codice chiama **delete_message** subito dopo il messaggio hello è stato elaborato.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Procedura: usufruire di opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi. In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. esempio di codice seguente Hello utilizza hello **get_messages** messaggi tooget 20 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **for** . Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio. Si noti che hello 5 minuti inizia per tutti i messaggi in hello stesso tempo, quindi dopo 5 minuti passati dal chiamata hello troppo**get_messages**, eventuali messaggi di cui non sono stati eliminati verrà visualizzati nuovamente.

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

## <a name="how-to-get-hello-queue-length"></a>Procedura: ottenere la lunghezza coda di hello
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Hello **download_attributes** metodo chiede hello coda servizio tooretrieve hello coda gli attributi, inclusi il numero di messaggi hello. Hello **approximate_message_count** metodo ottiene il numero approssimativo di messaggi hello nella coda di hello.

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

## <a name="how-to-delete-a-queue"></a>Procedura: eliminare una coda
una coda e tutti i messaggi hello contenuti al suo interno, chiamata hello toodelete **delete_queue_if_exists** metodo hello dell'oggetto di coda.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure.

* [Come toouse archiviazione Blob da C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Come toouse archiviazione tabelle da C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Elenco delle risorse di archiviazione di Azure in C++](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Informazioni di riferimento sulla libreria client di archiviazione per C++](http://azure.github.io/azure-storage-cpp)
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)