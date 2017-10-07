---
title: aaaDevelop per l'archiviazione di File di Azure con C++ | Documenti Microsoft
description: Informazioni su come toodevelop C++ applicazioni e servizi che usano File di Azure storage toostore dati dei file.
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Eseguire lo sviluppo per l'archiviazione file di Azure con C++
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Informazioni sull'esercitazione

In questa esercitazione si apprenderà come operazioni di base tooperform sull'archiviazione di File di Azure. Attraverso esempi scritti in C++, si apprenderà come toocreate condivide e directory, caricare, elencare ed eliminare i file. Nel caso di nuove risorse di archiviazione tooAzure File, il passando concetti hello in sezioni hello seguenti saranno utile per capire gli esempi di hello.


* Creare ed eliminare condivisioni file di Azure
* Creare ed eliminare directory
* Enumerare file e directory in una condivisione file di Azure
* Caricare, scaricare ed eliminare un file
* Impostare la quota di hello (dimensione massima) per una condivisione di File di Azure
* Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che utilizza un criterio di accesso condiviso definito nella condivisione di hello.

> [!Note]  
> Poiché l'archiviazione di File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le funzioni e classi C++ dei / o standard hello. In questo articolo descrive come le applicazioni che usano toowrite hello C++ Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.

## <a name="create-a-c-application"></a>Creazione di un’applicazione C++
esempi di hello toobuild, sarà necessario tooinstall hello Azure Storage Client Library 2.4.0 per C++. È inoltre necessario aver creato un account di archiviazione di Azure.

tooinstall hello del Client di archiviazione Azure 2.4.0 per C++, è possibile utilizzare uno dei seguenti metodi hello:

* **Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.
* **Windows:** in Visual Studio fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**. Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurare l'archiviazione di File di Azure di toouse applicazione
Aggiungere i seguenti hello includono file di origine C++ hello il percorso di archiviazione di File di Azure toomanipulate cima toohello istruzioni:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Impostare una stringa di connessione di archiviazione di Azure
toouse archiviazione di File, è necessario tooconnect tooyour account di archiviazione Azure. Hello primo passaggio potrebbe essere una stringa di connessione, che verrà usato tooconfigure tooconnect tooyour account di archiviazione. È pertanto possibile definire un toodo variabile statica che.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Connessione tooan account di archiviazione di Azure
È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'Account di archiviazione. tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile usare hello **analizzare** metodo.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Creare una condivisione file di Azure
Tutti i file e le directory nell'archiviazione file di Azure si trovano in un contenitore denominato **Share**. L'account di archiviazione può disporre del numero di condivisioni consentite dalla capacità dell'account. condivisione di tooa tooobtain accesso e il relativo contenuto, è necessario toouse un client di archiviazione di File di Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Client di archiviazione Azure File hello è quindi possibile ottenere una condivisione di tooa di riferimento.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

condivisione di hello toocreate, utilizzare hello **create_if_not_exists** metodo hello **cloud_file_share** oggetto.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

A questo punto, **condividere** contiene una condivisione di tooa di riferimento denominata **my-esempio-share**.

## <a name="delete-an-azure-file-share"></a>Eliminare una condivisione file di Azure
Eliminazione di una condivisione di viene eseguita dal chiamante hello **delete_if_exists** metodo su un oggetto cloud_file_share. Ecco il codice di esempio che esegue tale operazione.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Creare una directory
È possibile organizzare archiviazione inserendo i file all'interno di sottodirectory anziché tutti gli elementi nella directory radice hello. Archiviazione di File di Azure consente toocreate come consentire molte directory come l'account. codice Hello seguente verrà creata una directory denominata **directory di esempio my** nella directory radice di hello, nonché una sottodirectory denominata **my sottodirectory-esempio**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Eliminare una directory
Eliminare una directory è un'attività semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerare file e directory in una condivisione file di Azure
Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **list_files_and_directories** in un riferimento **cloud_file_directory**. set completo di proprietà e metodi per un tipo restituito di hello tooaccess **list_file_and_directory_item**, è necessario chiamare hello **list_file_and_directory_item.as_file** metodo tooget un **cloud_ file** oggetto o hello **list_file_and_directory_item.as_directory** metodo tooget un **cloud_file_directory** oggetto.

Hello di codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nella directory radice hello della condivisione hello.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Caricare un file
Hello molto, almeno una condivisione di File di Azure contiene una directory radice in cui i file possono trovarsi. In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.

Hello caricando un file è innanzitutto tooobtain una directory toohello di riferimento in cui risiede. A tale scopo, chiamata hello **get_root_directory_reference** metodo dell'oggetto condivisione hello.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Dopo aver creato una directory radice toohello di riferimento della condivisione di hello, è possibile caricare un file su di esso. Questo esempio esegue il caricamento da un file, da testo e da un flusso.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Scaricare un file
file toodownload, recuperare innanzitutto un riferimento a file e quindi chiamare hello **download_to_stream** metodo tootransfer hello file contenuto tooa oggetto flusso, che è quindi possibile mantenere tooa file locale. In alternativa, è possibile utilizzare hello **download_to_file** contenuto hello toodownload di metodo di un file locale tooa di file. È possibile utilizzare hello **download_text** contenuto hello toodownload di metodo di un file come una stringa di testo.

esempio Hello utilizza hello **download_to_stream** e **download_text** toodemonstrate metodi download file hello, che sono stati creati nelle sezioni precedenti.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Eliminare un file
Un'altra operazione comunemente eseguita nell'archiviazione file di Azure è l'eliminazione dei file. Hello codice seguente elimina un file denominato my-esempio-file-3 archiviato nella directory radice hello.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Impostare la quota di hello (dimensione massima) per una condivisione di File di Azure
È possibile impostare una quota di hello (o dimensioni massime) per una condivisione di file, in gigabyte. È inoltre possibile verificare la quantità di dati è attualmente archiviati nella condivisione di hello toosee.

Dalla quota hello impostazione per una condivisione, è possibile limitare hello totale dimensioni hello file archiviati nella condivisione di hello. Se hello dimensioni totali dei file nella condivisione di hello superano quota hello impostato nella condivisione di hello, il client verrà tooincrease Impossibile hello dimensioni dei file esistenti o creare nuovi file, a meno che tali file sono vuoti.

esempio di Hello seguente mostra come toocheck hello utilizzo corrente per una condivisione e la modalità tooset hello quota per la condivisione di hello.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generare la firma di accesso condiviso per un file o una condivisione file
È possibile generare una firma di accesso condiviso per una condivisione file o un singolo file. È anche possibile creare un criterio di accesso condiviso per un accesso condiviso toomanage di condivisione file firme. È consigliabile creare un criterio di accesso condiviso, in quanto forniscono un mezzo di revoca hello SAS se questa deve essere compromessa.

Hello di esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi utilizza che condividono tooprovide hello i vincoli dei criteri per una firma di accesso condiviso in un file hello.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'archiviazione di Azure, è esplorare queste risorse:

* [Libreria client di archiviazione per C++](https://github.com/Azure/azure-storage-cpp)
* [Esempi del servizio di archiviazione file di Azure scritti in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Storage Explorer](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)