---
title: Eseguire lo sviluppo per l'archiviazione file di Azure con C++ | Microsoft Docs
description: Informazioni su come sviluppare applicazioni e servizi C++ che usano l'archiviazione file di Azure per archiviare i dati dei file.
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
ms.openlocfilehash: 86c3714327074f5576e535f67a0a2a8e761ffb46
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="e436b-103">Eseguire lo sviluppo per l'archiviazione file di Azure con C++</span><span class="sxs-lookup"><span data-stu-id="e436b-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="e436b-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e436b-104">About this tutorial</span></span>

<span data-ttu-id="e436b-105">In questa esercitazione verrà illustrato come eseguire operazioni di base nell'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="e436b-105">In this tutorial, you'll learn how to perform basic operations on Azure File storage.</span></span> <span data-ttu-id="e436b-106">Gli esempi scritti in C++ consentono di apprendere come creare condivisioni e directory, caricare, elencare ed eliminare file.</span><span class="sxs-lookup"><span data-stu-id="e436b-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="e436b-107">Se non si ha familiarità con l'archiviazione file di Azure, leggere le sezioni seguenti per comprendere gli esempi.</span><span class="sxs-lookup"><span data-stu-id="e436b-107">If you are new to Azure File storage , going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>


* <span data-ttu-id="e436b-108">Creare ed eliminare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="e436b-109">Creare ed eliminare directory</span><span class="sxs-lookup"><span data-stu-id="e436b-109">Create and delete directories</span></span>
* <span data-ttu-id="e436b-110">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="e436b-111">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="e436b-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="e436b-112">Impostare la quota (dimensione massima) per la condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-112">Set the quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="e436b-113">Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che usa criteri di accesso condiviso definiti nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>

> [!Note]  
> <span data-ttu-id="e436b-114">Poiché l'archiviazione file di Azure è accessibile tramite SMB, è possibile scrivere semplici applicazioni che accedono alla condivisione file di Azure usando le classi e le funzioni standard I/O di C++.</span><span class="sxs-lookup"><span data-stu-id="e436b-114">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard C++ I/O classes and functions.</span></span> <span data-ttu-id="e436b-115">Questo articolo descrive come scrivere applicazioni basate su Azure Storage .NET SDK, che usa l'[API REST dell'archiviazione file Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) per comunicare con l'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="e436b-115">This article will describe how to write applications that use the Azure Storage C++ SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="e436b-116">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="e436b-116">Create a C++ application</span></span>
<span data-ttu-id="e436b-117">Per compilare gli esempi, è necessario installare la libreria client di archiviazione di Azure 2.4.0 per C++.</span><span class="sxs-lookup"><span data-stu-id="e436b-117">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="e436b-118">È inoltre necessario aver creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e436b-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="e436b-119">Per installare il client di archiviazione di Azure 2.4.0 per C++, è possibile usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e436b-119">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="e436b-120">**Linux:** seguire le istruzioni fornite nella pagina [README della libreria client di Archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="e436b-120">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="e436b-121">**Windows:** in Visual Studio fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="e436b-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="e436b-122">Digitare il seguente comando nella [console Gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="e436b-122">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="e436b-123">Configurare l'applicazione per usare l'archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-123">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="e436b-124">Aggiungere le istruzioni include seguenti all'inizio del file di origine C++ in cui si vuole modificare l'archiviazione file di Azure:</span><span class="sxs-lookup"><span data-stu-id="e436b-124">Add the following include statements to the top of the C++ source file where you want to manipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e436b-125">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e436b-126">Per utilizzare la condivisione di file, è necessario connettersi all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e436b-126">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="e436b-127">Il primo passaggio consiste nel configurare una stringa di connessione che verrà usata per connettersi all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e436b-127">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="e436b-128">È importante definire una variabile statica a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="e436b-128">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="e436b-129">Connessione a un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-129">Connecting to an Azure storage account</span></span>
<span data-ttu-id="e436b-130">Per visualizzare le informazioni dell'account di archiviazione, è possibile usare la classe **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="e436b-130">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="e436b-131">Per recuperare le informazioni sull'account di archiviazione dalla stringa di connessione alla risorsa di archiviazione, è possibile utilizzare il metodo **parse** .</span><span class="sxs-lookup"><span data-stu-id="e436b-131">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="e436b-132">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-132">Create an Azure File share</span></span>
<span data-ttu-id="e436b-133">Tutti i file e le directory nell'archiviazione file di Azure si trovano in un contenitore denominato **Share**.</span><span class="sxs-lookup"><span data-stu-id="e436b-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="e436b-134">L'account di archiviazione può disporre del numero di condivisioni consentite dalla capacità dell'account.</span><span class="sxs-lookup"><span data-stu-id="e436b-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="e436b-135">Per ottenere l'accesso a una condivisione e ai suoi contenuti, è necessario usare un client per l'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="e436b-135">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```cpp
// Create the Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="e436b-136">In questo modo è possibile ottenere un riferimento a una condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-136">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="e436b-137">Per creare la condivisione, usare il metodo **create_if_not_exists** dell'oggetto **cloud_file_share**.</span><span class="sxs-lookup"><span data-stu-id="e436b-137">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="e436b-138">A questo punto, **share** contiene un riferimento a una condivisione denominata **my-sample-share**.</span><span class="sxs-lookup"><span data-stu-id="e436b-138">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="e436b-139">Eliminare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-139">Delete an Azure File share</span></span>
<span data-ttu-id="e436b-140">L'eliminazione di una condivisione viene eseguita chiamando il metodo **delete_if_exists** in un oggetto cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="e436b-140">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="e436b-141">Ecco il codice di esempio che esegue tale operazione.</span><span class="sxs-lookup"><span data-stu-id="e436b-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="e436b-142">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="e436b-142">Create a directory</span></span>
<span data-ttu-id="e436b-143">È possibile organizzare l'archiviazione inserendo i file all'interno di sottodirectory anziché inserirli tutti nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="e436b-143">You can organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="e436b-144">L'archiviazione file di Azure consente di creare tutte le directory consentite dall'account.</span><span class="sxs-lookup"><span data-stu-id="e436b-144">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="e436b-145">Il codice seguente creerà una directory denominata **my-sample-directory** sotto la directory radice e una sottodirectory denominata **my-sample-subdirectory**.</span><span class="sxs-lookup"><span data-stu-id="e436b-145">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="e436b-146">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="e436b-146">Delete a directory</span></span>
<span data-ttu-id="e436b-147">Eliminare una directory è un'attività semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.</span><span class="sxs-lookup"><span data-stu-id="e436b-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="e436b-148">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="e436b-149">Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **list_files_and_directories** in un riferimento **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="e436b-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="e436b-150">Per accedere al set completo di proprietà e metodi per un **list_file_and_directory_item** restituito, è necessario chiamare il metodo **list_file_and_directory_item.as_file** per ottenere un oggetto **cloud_file** oppure il metodo **list_file_and_directory_item.as_directory** per ottenere un oggetto **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="e436b-150">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="e436b-151">Il codice seguente illustra come recuperare e visualizzare l'URI di ogni elemento della directory radice della condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-151">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
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

## <a name="upload-a-file"></a><span data-ttu-id="e436b-152">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="e436b-152">Upload a file</span></span>
<span data-ttu-id="e436b-153">Una condivisione file di Azure contiene almeno una directory radice in cui possono risiedere i file.</span><span class="sxs-lookup"><span data-stu-id="e436b-153">At the very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="e436b-154">In questa sezione verrà illustrato come caricare un file dall'archiviazione locale nella directory radice di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-154">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="e436b-155">Il primo passaggio del caricamento di un file consiste nell'ottenere un riferimento alla directory in cui risiederà.</span><span class="sxs-lookup"><span data-stu-id="e436b-155">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="e436b-156">È possibile eseguire questa operazione chiamando il metodo **get_root_directory_reference** dell'oggetto condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-156">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="e436b-157">Ora che si dispone di un riferimento alla directory radice della condivisione, è possibile caricarvi un file.</span><span class="sxs-lookup"><span data-stu-id="e436b-157">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="e436b-158">Questo esempio esegue il caricamento da un file, da testo e da un flusso.</span><span class="sxs-lookup"><span data-stu-id="e436b-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="e436b-159">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="e436b-159">Download a file</span></span>
<span data-ttu-id="e436b-160">Per scaricare i file, recuperare prima un riferimento al file e quindi chiamare il metodo **download_to_stream** per trasferire il contenuto del file in un oggetto flusso che è possibile memorizzare in modo permanente in un file locale.</span><span class="sxs-lookup"><span data-stu-id="e436b-160">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="e436b-161">In alternativa, è possibile usare il metodo **download_to_file** per scaricare il contenuto di un file in un file locale.</span><span class="sxs-lookup"><span data-stu-id="e436b-161">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="e436b-162">È possibile usare il metodo **download_text** per scaricare il contenuto di un file come stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="e436b-162">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="e436b-163">L'esempio seguente usa i metodi **download_to_stream** e **download_text** per illustrare il download dei file creati nelle sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e436b-163">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="e436b-164">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="e436b-164">Delete a file</span></span>
<span data-ttu-id="e436b-165">Un'altra operazione comunemente eseguita nell'archiviazione file di Azure è l'eliminazione dei file.</span><span class="sxs-lookup"><span data-stu-id="e436b-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="e436b-166">Il codice seguente elimina un file denominato my-sample-file-3 archiviato nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="e436b-166">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="e436b-167">Impostare la quota (dimensione massima) per la condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-167">Set the quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="e436b-168">È possibile impostare la quota o dimensione massima per una condivisione file in gigabyte.</span><span class="sxs-lookup"><span data-stu-id="e436b-168">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="e436b-169">È anche possibile controllare la quantità di dati archiviata attualmente nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-169">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="e436b-170">Impostando la quota per una condivisione, è possibile limitare la dimensione totale dei file archiviati nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-170">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="e436b-171">Se la dimensione totale dei file nella condivisione supera la quota impostata per la condivisione, i client non saranno in grado di aumentare le dimensioni dei file esistenti o creare nuovi file, a meno che tali file non siano vuoti.</span><span class="sxs-lookup"><span data-stu-id="e436b-171">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="e436b-172">L'esempio seguente illustra come controllare l'uso corrente per una condivisione e come impostare la quota per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-172">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="e436b-173">Generare la firma di accesso condiviso per un file o una condivisione file</span><span class="sxs-lookup"><span data-stu-id="e436b-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="e436b-174">È possibile generare una firma di accesso condiviso per una condivisione file o un singolo file.</span><span class="sxs-lookup"><span data-stu-id="e436b-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="e436b-175">È inoltre possibile creare un criterio di accesso condiviso in una condivisione file per gestire le firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="e436b-175">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="e436b-176">È consigliabile creare un criterio di accesso condiviso, in quanto fornisce un modo per revocare la firma SAS se necessario.</span><span class="sxs-lookup"><span data-stu-id="e436b-176">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="e436b-177">Nell'esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi viene usato tale criterio per fornire i vincoli per una firma di accesso condiviso su un file della condivisione.</span><span class="sxs-lookup"><span data-stu-id="e436b-177">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
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

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="e436b-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e436b-178">Next steps</span></span>
<span data-ttu-id="e436b-179">Per altre informazioni su Archiviazione di Azure, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="e436b-179">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="e436b-180">Libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="e436b-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="e436b-181">[Esempi del servizio di archiviazione file di Azure scritti in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="e436b-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="e436b-182">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e436b-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="e436b-183">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e436b-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)