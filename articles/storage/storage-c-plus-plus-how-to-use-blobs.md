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
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="a1a0d-103">Come toouse archiviazione Blob da C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a1a0d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a1a0d-104">Overview</span></span>
<span data-ttu-id="a1a0d-105">Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="a1a0d-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a1a0d-107">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="a1a0d-108">Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="a1a0d-109">esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="a1a0d-110">Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="a1a0d-111">Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="a1a0d-112">Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="a1a0d-113">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-113">Create a C++ application</span></span>
<span data-ttu-id="a1a0d-114">In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="a1a0d-115">toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="a1a0d-116">tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="a1a0d-117">**Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="a1a0d-118">**Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="a1a0d-119">Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="a1a0d-120">Install-Package knockoutjs</span><span class="sxs-lookup"><span data-stu-id="a1a0d-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="a1a0d-121">Configurare l'archiviazione Blob di tooaccess applicazione</span><span class="sxs-lookup"><span data-stu-id="a1a0d-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="a1a0d-122">Aggiungere i seguenti hello includono i file di C++ hello in cui si desidera toouse hello archiviazione di Azure API tooaccess BLOB cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="a1a0d-123">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a1a0d-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="a1a0d-124">Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="a1a0d-125">Quando si esegue un'applicazione client, è necessario fornire stringa di connessione di archiviazione hello in hello seguente formato, utilizzando il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso di account di archiviazione hello elencato nella hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="a1a0d-126">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="a1a0d-127">In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="a1a0d-128">tootest l'applicazione nel computer locale di Windows, è possibile utilizzare Microsoft Azure hello [emulatore di archiviazione](storage-use-emulator.md) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="a1a0d-129">emulatore di archiviazione Hello è un'utilità che simula hello Blob, coda e tabella servizi disponibili in Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="a1a0d-130">Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="a1a0d-131">toostart hello emulatore di archiviazione Azure, seleziona hello **avviare** hello o preme **Windows** chiave.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="a1a0d-132">Iniziare a digitare **emulatore di archiviazione Azure**e selezionare **emulatore di archiviazione di Microsoft Azure** elenco hello di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="a1a0d-133">Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="a1a0d-134">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="a1a0d-134">Retrieve your connection string</span></span>
<span data-ttu-id="a1a0d-135">È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="a1a0d-136">tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile usare hello **analizzare** metodo.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="a1a0d-137">Quindi, ottenere un riferimento tooa **cloud_blob_client** classe in quanto consente tooretrieve oggetti che rappresentano i contenitori e BLOB archiviati all'interno di hello servizio di archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="a1a0d-138">Hello codice seguente viene creata una **cloud_blob_client** oggetto utilizzando l'oggetto account di archiviazione hello è recuperato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="a1a0d-139">Procedura: creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="a1a0d-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a1a0d-140">Questo esempio viene illustrato come toocreate un contenitore, se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-140">This example shows how toocreate a container if it does not already exist:</span></span>  

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

<span data-ttu-id="a1a0d-141">Per impostazione predefinita, il nuovo contenitore di hello è privata ed è necessario specificare i BLOB toodownload chiave di accesso di archiviazione da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="a1a0d-142">Se si desidera che il file di hello toomake (BLOB) all'interno di hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblico utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="a1a0d-143">Chiunque sia connesso a Internet hello possa vedere i BLOB in un contenitore pubblico, ma è possibile modificarli o eliminarli solo se si dispone di hello chiave di accesso appropriati.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="a1a0d-144">Procedura: caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="a1a0d-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="a1a0d-145">In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="a1a0d-146">Nella maggior parte delle hello blob in blocchi è consigliata toouse tipo hello.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="a1a0d-147">tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="a1a0d-148">Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **upload_from_stream** metodo.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="a1a0d-149">Questa operazione consente di creare blob hello se non è stata precedentemente esiste, o sovrascrivere il file se esiste.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="a1a0d-150">Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

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

<span data-ttu-id="a1a0d-151">In alternativa, è possibile utilizzare hello **upload_from_file** tooupload metodo un blob in blocchi tooa file.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="a1a0d-152">Procedura: elencare i BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="a1a0d-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="a1a0d-153">BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="a1a0d-154">È quindi possibile utilizzare del contenitore hello **list_blobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="a1a0d-155">set completo di proprietà e metodi per un tipo restituito di hello tooaccess **list_blob_item**, è necessario chiamare hello **list_blob_item.as_blob** tooget metodo un **cloud_blob** oggetto, hello o **list_blob.as_directory** tooget metodo un oggetto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="a1a0d-156">Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello **risorse del contenitore di esempio** contenitore:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

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

<span data-ttu-id="a1a0d-157">Per ulteriori informazioni sull'elenco di operazioni, vedere [elenco risorse di archiviazione Azure in C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="a1a0d-158">Procedura: scaricare i BLOB</span><span class="sxs-lookup"><span data-stu-id="a1a0d-158">How to: Download blobs</span></span>
<span data-ttu-id="a1a0d-159">BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **download_to_stream** metodo.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="a1a0d-160">esempio Hello utilizza hello **download_to_stream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

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

<span data-ttu-id="a1a0d-161">In alternativa, è possibile utilizzare hello **download_to_file** contenuto hello toodownload di metodo di un file tooa blob.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="a1a0d-162">Inoltre, è possibile utilizzare anche hello **download_text** contenuto hello toodownload di metodo di un blob come una stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

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

## <a name="how-to-delete-blobs"></a><span data-ttu-id="a1a0d-163">Procedura: eliminare i BLOB</span><span class="sxs-lookup"><span data-stu-id="a1a0d-163">How to: Delete blobs</span></span>
<span data-ttu-id="a1a0d-164">un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare hello **delete_blob** metodo su di esso.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="a1a0d-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1a0d-165">Next steps</span></span>
<span data-ttu-id="a1a0d-166">Ora che si è appreso i concetti di base di hello dell'archiviazione blob, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="a1a0d-167">Come toouse l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-167">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="a1a0d-168">Come toouse archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-168">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="a1a0d-169">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="a1a0d-170">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="a1a0d-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="a1a0d-171">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a1a0d-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="a1a0d-172">Trasferimento dati con hello utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="a1a0d-172">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

