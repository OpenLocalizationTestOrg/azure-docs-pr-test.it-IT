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
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="66a4f-103">Eseguire lo sviluppo per l'archiviazione file di Azure con C++</span><span class="sxs-lookup"><span data-stu-id="66a4f-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="66a4f-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="66a4f-104">About this tutorial</span></span>

<span data-ttu-id="66a4f-105">In questa esercitazione si apprenderà come operazioni di base tooperform sull'archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="66a4f-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="66a4f-106">Attraverso esempi scritti in C++, si apprenderà come toocreate condivide e directory, caricare, elencare ed eliminare i file.</span><span class="sxs-lookup"><span data-stu-id="66a4f-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="66a4f-107">Nel caso di nuove risorse di archiviazione tooAzure File, il passando concetti hello in sezioni hello seguenti saranno utile per capire gli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="66a4f-108">Creare ed eliminare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="66a4f-109">Creare ed eliminare directory</span><span class="sxs-lookup"><span data-stu-id="66a4f-109">Create and delete directories</span></span>
* <span data-ttu-id="66a4f-110">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="66a4f-111">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="66a4f-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="66a4f-112">Impostare la quota di hello (dimensione massima) per una condivisione di File di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="66a4f-113">Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che utilizza un criterio di accesso condiviso definito nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="66a4f-114">Poiché l'archiviazione di File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le funzioni e classi C++ dei / o standard hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="66a4f-115">In questo articolo descrive come le applicazioni che usano toowrite hello C++ Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.</span><span class="sxs-lookup"><span data-stu-id="66a4f-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="66a4f-116">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="66a4f-116">Create a C++ application</span></span>
<span data-ttu-id="66a4f-117">esempi di hello toobuild, sarà necessario tooinstall hello Azure Storage Client Library 2.4.0 per C++.</span><span class="sxs-lookup"><span data-stu-id="66a4f-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="66a4f-118">È inoltre necessario aver creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="66a4f-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="66a4f-119">tooinstall hello del Client di archiviazione Azure 2.4.0 per C++, è possibile utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="66a4f-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="66a4f-120">**Linux:** seguire istruzioni hello hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="66a4f-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="66a4f-121">**Windows:** in Visual Studio fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="66a4f-122">Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="66a4f-123">Configurare l'archiviazione di File di Azure di toouse applicazione</span><span class="sxs-lookup"><span data-stu-id="66a4f-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="66a4f-124">Aggiungere i seguenti hello includono file di origine C++ hello il percorso di archiviazione di File di Azure toomanipulate cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="66a4f-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="66a4f-125">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="66a4f-126">toouse archiviazione di File, è necessario tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="66a4f-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="66a4f-127">Hello primo passaggio potrebbe essere una stringa di connessione, che verrà usato tooconfigure tooconnect tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="66a4f-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="66a4f-128">È pertanto possibile definire un toodo variabile statica che.</span><span class="sxs-lookup"><span data-stu-id="66a4f-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="66a4f-129">Connessione tooan account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="66a4f-130">È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="66a4f-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="66a4f-131">tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile usare hello **analizzare** metodo.</span><span class="sxs-lookup"><span data-stu-id="66a4f-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="66a4f-132">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-132">Create an Azure File share</span></span>
<span data-ttu-id="66a4f-133">Tutti i file e le directory nell'archiviazione file di Azure si trovano in un contenitore denominato **Share**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="66a4f-134">L'account di archiviazione può disporre del numero di condivisioni consentite dalla capacità dell'account.</span><span class="sxs-lookup"><span data-stu-id="66a4f-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="66a4f-135">condivisione di tooa tooobtain accesso e il relativo contenuto, è necessario toouse un client di archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="66a4f-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="66a4f-136">Client di archiviazione Azure File hello è quindi possibile ottenere una condivisione di tooa di riferimento.</span><span class="sxs-lookup"><span data-stu-id="66a4f-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="66a4f-137">condivisione di hello toocreate, utilizzare hello **create_if_not_exists** metodo hello **cloud_file_share** oggetto.</span><span class="sxs-lookup"><span data-stu-id="66a4f-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="66a4f-138">A questo punto, **condividere** contiene una condivisione di tooa di riferimento denominata **my-esempio-share**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="66a4f-139">Eliminare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-139">Delete an Azure File share</span></span>
<span data-ttu-id="66a4f-140">Eliminazione di una condivisione di viene eseguita dal chiamante hello **delete_if_exists** metodo su un oggetto cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="66a4f-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="66a4f-141">Ecco il codice di esempio che esegue tale operazione.</span><span class="sxs-lookup"><span data-stu-id="66a4f-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="66a4f-142">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="66a4f-142">Create a directory</span></span>
<span data-ttu-id="66a4f-143">È possibile organizzare archiviazione inserendo i file all'interno di sottodirectory anziché tutti gli elementi nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="66a4f-144">Archiviazione di File di Azure consente toocreate come consentire molte directory come l'account.</span><span class="sxs-lookup"><span data-stu-id="66a4f-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="66a4f-145">codice Hello seguente verrà creata una directory denominata **directory di esempio my** nella directory radice di hello, nonché una sottodirectory denominata **my sottodirectory-esempio**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="66a4f-146">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="66a4f-146">Delete a directory</span></span>
<span data-ttu-id="66a4f-147">Eliminare una directory è un'attività semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.</span><span class="sxs-lookup"><span data-stu-id="66a4f-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="66a4f-148">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="66a4f-149">Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **list_files_and_directories** in un riferimento **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="66a4f-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="66a4f-150">set completo di proprietà e metodi per un tipo restituito di hello tooaccess **list_file_and_directory_item**, è necessario chiamare hello **list_file_and_directory_item.as_file** metodo tooget un **cloud_ file** oggetto o hello **list_file_and_directory_item.as_directory** metodo tooget un **cloud_file_directory** oggetto.</span><span class="sxs-lookup"><span data-stu-id="66a4f-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="66a4f-151">Hello di codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nella directory radice hello della condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

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

## <a name="upload-a-file"></a><span data-ttu-id="66a4f-152">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="66a4f-152">Upload a file</span></span>
<span data-ttu-id="66a4f-153">Hello molto, almeno una condivisione di File di Azure contiene una directory radice in cui i file possono trovarsi.</span><span class="sxs-lookup"><span data-stu-id="66a4f-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="66a4f-154">In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="66a4f-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="66a4f-155">Hello caricando un file è innanzitutto tooobtain una directory toohello di riferimento in cui risiede.</span><span class="sxs-lookup"><span data-stu-id="66a4f-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="66a4f-156">A tale scopo, chiamata hello **get_root_directory_reference** metodo dell'oggetto condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="66a4f-157">Dopo aver creato una directory radice toohello di riferimento della condivisione di hello, è possibile caricare un file su di esso.</span><span class="sxs-lookup"><span data-stu-id="66a4f-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="66a4f-158">Questo esempio esegue il caricamento da un file, da testo e da un flusso.</span><span class="sxs-lookup"><span data-stu-id="66a4f-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="66a4f-159">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="66a4f-159">Download a file</span></span>
<span data-ttu-id="66a4f-160">file toodownload, recuperare innanzitutto un riferimento a file e quindi chiamare hello **download_to_stream** metodo tootransfer hello file contenuto tooa oggetto flusso, che è quindi possibile mantenere tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="66a4f-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="66a4f-161">In alternativa, è possibile utilizzare hello **download_to_file** contenuto hello toodownload di metodo di un file locale tooa di file.</span><span class="sxs-lookup"><span data-stu-id="66a4f-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="66a4f-162">È possibile utilizzare hello **download_text** contenuto hello toodownload di metodo di un file come una stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="66a4f-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="66a4f-163">esempio Hello utilizza hello **download_to_stream** e **download_text** toodemonstrate metodi download file hello, che sono stati creati nelle sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="66a4f-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="66a4f-164">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="66a4f-164">Delete a file</span></span>
<span data-ttu-id="66a4f-165">Un'altra operazione comunemente eseguita nell'archiviazione file di Azure è l'eliminazione dei file.</span><span class="sxs-lookup"><span data-stu-id="66a4f-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="66a4f-166">Hello codice seguente elimina un file denominato my-esempio-file-3 archiviato nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

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

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="66a4f-167">Impostare la quota di hello (dimensione massima) per una condivisione di File di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="66a4f-168">È possibile impostare una quota di hello (o dimensioni massime) per una condivisione di file, in gigabyte.</span><span class="sxs-lookup"><span data-stu-id="66a4f-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="66a4f-169">È inoltre possibile verificare la quantità di dati è attualmente archiviati nella condivisione di hello toosee.</span><span class="sxs-lookup"><span data-stu-id="66a4f-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="66a4f-170">Dalla quota hello impostazione per una condivisione, è possibile limitare hello totale dimensioni hello file archiviati nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="66a4f-171">Se hello dimensioni totali dei file nella condivisione di hello superano quota hello impostato nella condivisione di hello, il client verrà tooincrease Impossibile hello dimensioni dei file esistenti o creare nuovi file, a meno che tali file sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="66a4f-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="66a4f-172">esempio di Hello seguente mostra come toocheck hello utilizzo corrente per una condivisione e la modalità tooset hello quota per la condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="66a4f-173">Generare la firma di accesso condiviso per un file o una condivisione file</span><span class="sxs-lookup"><span data-stu-id="66a4f-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="66a4f-174">È possibile generare una firma di accesso condiviso per una condivisione file o un singolo file.</span><span class="sxs-lookup"><span data-stu-id="66a4f-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="66a4f-175">È anche possibile creare un criterio di accesso condiviso per un accesso condiviso toomanage di condivisione file firme.</span><span class="sxs-lookup"><span data-stu-id="66a4f-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="66a4f-176">È consigliabile creare un criterio di accesso condiviso, in quanto forniscono un mezzo di revoca hello SAS se questa deve essere compromessa.</span><span class="sxs-lookup"><span data-stu-id="66a4f-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="66a4f-177">Hello di esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi utilizza che condividono tooprovide hello i vincoli dei criteri per una firma di accesso condiviso in un file hello.</span><span class="sxs-lookup"><span data-stu-id="66a4f-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="66a4f-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66a4f-178">Next steps</span></span>
<span data-ttu-id="66a4f-179">toolearn più sull'archiviazione di Azure, è esplorare queste risorse:</span><span class="sxs-lookup"><span data-stu-id="66a4f-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="66a4f-180">Libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="66a4f-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="66a4f-181">[Esempi del servizio di archiviazione file di Azure scritti in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="66a4f-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="66a4f-182">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="66a4f-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="66a4f-183">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="66a4f-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)