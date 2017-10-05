---
title: Come usare l'archiviazione BLOB (archiviazione di oggetti) da C++ | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
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
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="5a1b6-103">Come usare l'archiviazione BLOB da C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5a1b6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5a1b6-104">Overview</span></span>
<span data-ttu-id="5a1b6-105">L'archiviazione BLOB di Azure è un servizio che archivia dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="5a1b6-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5a1b6-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="5a1b6-108">In questa guida verranno illustrati diversi scenari comuni di utilizzo del servizio di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="5a1b6-109">Gli esempi sono scritti in C++ e utilizzano la [libreria client di Archiviazione di Azure per C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5a1b6-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="5a1b6-110">Gli scenari illustrati includono **caricamento**, **visualizzazione in elenchi**, **download** e **eliminazione** di BLOB.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="5a1b6-111">Questa guida fa riferimento alla libreria client di Archiviazione di Azure per C++ versione 1.0.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="5a1b6-112">La versione consigliata per la libreria client di archiviazione è la 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="5a1b6-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="5a1b6-113">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-113">Create a C++ application</span></span>
<span data-ttu-id="5a1b6-114">In questa guida verranno utilizzate le funzionalità di archiviazione che è possibile eseguire all’interno di un’applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="5a1b6-115">A tal fine, sarà necessario installare la libreria client di Archiviazione di Azure per C++ e creare un account di archiviazione Azure nella propria sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="5a1b6-116">Per installare la libreria client di Archiviazione di Azure per C++, è possibile utilizzare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="5a1b6-117">**Linux:** seguire le istruzioni fornite nella pagina [README della libreria client di Archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="5a1b6-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="5a1b6-118">**Windows:** in Visual Studio, fare clic su **Strumenti > Gestione pacchetti NuGet > console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="5a1b6-119">Digitare il seguente comando nella [console Gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="5a1b6-120">Install-Package knockoutjs</span><span class="sxs-lookup"><span data-stu-id="5a1b6-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="5a1b6-121">Configurazione dell'applicazione per l'accesso all'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="5a1b6-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="5a1b6-122">Aggiungere le istruzioni include seguenti all'inizio del file C++ in cui si desidera utilizzare le API di archiviazione di Azure per accedere ai BLOB:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="5a1b6-123">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5a1b6-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="5a1b6-124">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="5a1b6-125">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente, usando il nome dell'account di archiviazione e la chiave di accesso alle risorse di archiviazione per l'account di archiviazione elencato nel [portale di Azure](https://portal.azure.com) per i valori di *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="5a1b6-126">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a1b6-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="5a1b6-127">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="5a1b6-128">Per eseguire il test dell'applicazione nel computer Windows locale, è possibile usare l'[emulatore di archiviazione](../storage-use-emulator.md) di Microsoft Azure installato con [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5a1b6-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="5a1b6-129">L'emulatore di archiviazione è un'utilità che simula i servizi BLOB, tabelle e di accodamento, disponibile in Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="5a1b6-130">Nell’esempio seguente viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione all’emulatore di archiviazione locale:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="5a1b6-131">Per avviare l'emulatore di archiviazione di Azure, selezionare il pulsante **Start** o premere **WINDOWS** sulla tastiera.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="5a1b6-132">Digitare **Emulatore di archiviazione di Azure** e selezionare **Emulatore di archiviazione di Microsoft Azure** nell'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="5a1b6-133">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="5a1b6-134">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="5a1b6-134">Retrieve your connection string</span></span>
<span data-ttu-id="5a1b6-135">Per visualizzare le informazioni dell'account di archiviazione, è possibile usare la classe **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="5a1b6-136">Per recuperare le informazioni sull'account di archiviazione dalla stringa di connessione alla risorsa di archiviazione, è possibile utilizzare il metodo **parse** .</span><span class="sxs-lookup"><span data-stu-id="5a1b6-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="5a1b6-137">Ottenere successivamente un riferimento alla classe **cloud_blob_client**, perché consente di recuperare oggetti che rappresentano contenitori e BLOB archiviati nel servizio di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="5a1b6-138">Il codice seguente crea un oggetto **cloud_blob_client** usando l'oggetto account di archiviazione recuperato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="5a1b6-139">Procedura: creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="5a1b6-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5a1b6-140">In questo esempio viene creato un contenitore, nel caso in cui non esista già:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="5a1b6-141">Per impostazione predefinita, il nuovo contenitore è privato ed è necessario specificare la chiave di accesso alle risorse di archiviazione per scaricare BLOB da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="5a1b6-142">Se si desidera rendere i file all'interno del contenitore disponibili per tutti, è possibile impostare il contenitore come pubblico utilizzando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5a1b6-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="5a1b6-143">I BLOB in un contenitore pubblico sono visibili a tutti gli utenti di Internet, tuttavia è possibile modificarli o eliminarli solo se si dispone della chiave di accesso appropriata.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="5a1b6-144">Procedura: caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="5a1b6-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="5a1b6-145">In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="5a1b6-146">Nella maggior parte dei casi è consigliabile utilizzare il tipo di BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="5a1b6-147">Per caricare un file in un BLOB in blocchi, ottenere un riferimento a un contenitore e utilizzarlo per ottenere un riferimento a un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="5a1b6-148">Dopo aver ottenuto un riferimento al BLOB, è possibile caricarvi qualsiasi flusso di dati chiamando il metodo **upload_from_stream**.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="5a1b6-149">Questa operazione consentirà di creare il BLOB se non già esistente o di sovrascriverlo se già esistente.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="5a1b6-150">Nell'esempio seguente viene illustrato come caricare un BLOB in un contenitore e si presuppone che il contenitore sia già stato creato.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="5a1b6-151">In alternativa, è possibile usare il metodo **upload_from_file** per caricare un file in un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="5a1b6-152">Procedura: elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="5a1b6-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="5a1b6-153">Per elencare i BLOB in un contenitore, ottenere prima un riferimento al contenitore.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="5a1b6-154">Sarà successivamente possibile usare il metodo **list_blobs** del contenitore per recuperare i BLOB e/o le directory in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="5a1b6-155">Per accedere al set completo di proprietà e metodi per un **list_blob_item** restituito, è necessario chiamare il metodo **list_blob_item.as_blob** per ottenere un oggetto **cloud_blob** oppure il metodo **list_blob.as_directory** per ottenere un oggetto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="5a1b6-156">Nel codice seguente viene illustrato come recuperare e visualizzare l'URI di ciascun elemento del contenitore **my-sample-container** :</span><span class="sxs-lookup"><span data-stu-id="5a1b6-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
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

<span data-ttu-id="5a1b6-157">Per ulteriori informazioni sull'elenco di operazioni, vedere [elenco risorse di archiviazione Azure in C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="5a1b6-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="5a1b6-158">Procedura: scaricare i BLOB</span><span class="sxs-lookup"><span data-stu-id="5a1b6-158">How to: Download blobs</span></span>
<span data-ttu-id="5a1b6-159">Per scaricare BLOB, recuperare prima un riferimento al BLOB e chiamare il metodo **download_to_stream**.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="5a1b6-160">Nell'esempio seguente viene usato il metodo **download_to_stream** per trasferire il contenuto del BLOB in un oggetto stream per poterlo mentenere in un file locale.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="5a1b6-161">In alternativa, è possibile usare il metodo **download_to_file** per scaricare il contenuto di un BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="5a1b6-162">È anche possibile usare il metodo **download_text** per scaricare il contenuto di un BLOB come stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="5a1b6-163">Procedura: eliminare i BLOB</span><span class="sxs-lookup"><span data-stu-id="5a1b6-163">How to: Delete blobs</span></span>
<span data-ttu-id="5a1b6-164">Per eliminare un BLOB, ottenere prima un riferimento al BLOB e chiamare il metodo **delete_blob** sul riferimento.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="5a1b6-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a1b6-165">Next steps</span></span>
<span data-ttu-id="5a1b6-166">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione BLOB, visitare i collegamenti seguenti per ulteriori informazioni su Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a1b6-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="5a1b6-167">Come usare l’archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="5a1b6-168">Come usare l’archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="5a1b6-169">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="5a1b6-170">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="5a1b6-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="5a1b6-171">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5a1b6-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="5a1b6-172">Trasferire dati con l'utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="5a1b6-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

