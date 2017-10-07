---
title: aaaHow toouse blob archiviazione (oggetto) da C++ | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Come toouse archiviazione Blob da C++
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione Blob di Azure. esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB.  

> [!NOTE]
> Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive. Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creazione di un’applicazione C++
In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.  

toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.   

tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:

* **Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.  
* **Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**. Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.  
  
     Install-Package knockoutjs

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurare l'archiviazione Blob di tooaccess applicazione
Aggiungere i seguenti hello includono i file di C++ hello in cui si desidera toouse hello archiviazione di Azure API tooaccess BLOB cima toohello istruzioni:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire stringa di connessione di archiviazione hello in hello seguente formato, utilizzando il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso di account di archiviazione hello elencato nella hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori. Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest l'applicazione nel computer locale di Windows, è possibile utilizzare Microsoft Azure hello [emulatore di archiviazione](../storage-use-emulator.md) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulatore di archiviazione Hello è un'utilità che simula hello Blob, coda e tabella servizi disponibili in Azure nel computer di sviluppo locale. Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:

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

Quindi, ottenere un riferimento tooa **cloud_blob_client** classe in quanto consente tooretrieve oggetti che rappresentano i contenitori e BLOB archiviati all'interno di hello servizio di archiviazione Blob. Hello codice seguente viene creata una **cloud_blob_client** oggetto utilizzando l'oggetto account di archiviazione hello è recuperato in precedenza:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Procedura: creare un contenitore
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Questo esempio viene illustrato come toocreate un contenitore, se non esiste già:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Per impostazione predefinita, il nuovo contenitore di hello è privata ed è necessario specificare i BLOB toodownload chiave di accesso di archiviazione da questo contenitore. Se si desidera che il file di hello toomake (BLOB) all'interno di hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblico utilizzando hello seguente codice:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Chiunque sia connesso a Internet hello possa vedere i BLOB in un contenitore pubblico, ma è possibile modificarli o eliminarli solo se si dispone di hello chiave di accesso appropriati.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Procedura: caricare un BLOB in un contenitore
In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine. Nella maggior parte delle hello blob in blocchi è consigliata toouse tipo hello.  

tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco. Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **upload_from_stream** metodo. Questa operazione consente di creare blob hello se non è stata precedentemente esiste, o sovrascrivere il file se esiste. Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

In alternativa, è possibile utilizzare hello **upload_from_file** tooupload metodo un blob in blocchi tooa file.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Procedura: elencare i BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore. È quindi possibile utilizzare del contenitore hello **list_blobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso. set completo di proprietà e metodi per un tipo restituito di hello tooaccess **list_blob_item**, è necessario chiamare hello **list_blob_item.as_blob** tooget metodo un **cloud_blob** oggetto, hello o **list_blob.as_directory** tooget metodo un oggetto cloud_blob_directory. Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello **risorse del contenitore di esempio** contenitore:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Per ulteriori informazioni sull'elenco di operazioni, vedere [elenco risorse di archiviazione Azure in C++](../storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Procedura: scaricare i BLOB
BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **download_to_stream** metodo. esempio Hello utilizza hello **download_to_stream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

In alternativa, è possibile utilizzare hello **download_to_file** contenuto hello toodownload di metodo di un file tooa blob.
Inoltre, è possibile utilizzare anche hello **download_text** contenuto hello toodownload di metodo di un blob come una stringa di testo.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Procedura: eliminare i BLOB
un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare hello **delete_blob** metodo su di esso.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello dell'archiviazione blob, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure.  

* [Come toouse l'archiviazione delle code da C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Come toouse archiviazione tabelle da C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Elenco delle risorse di archiviazione di Azure in C++](../storage-c-plus-plus-enumeration.md)
* [Informazioni di riferimento sulla libreria client di archiviazione per C++](http://azure.github.io/azure-storage-cpp)
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Trasferimento dati con hello utilità della riga di comando AzCopy](../storage-use-azcopy.md)

