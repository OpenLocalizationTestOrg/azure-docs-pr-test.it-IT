---
title: Eseguire lo sviluppo per Archiviazione file di Azure con Python | Microsoft Docs
description: Informazioni su come sviluppare applicazioni e servizi Python che usano Archiviazione file di Azure per archiviare i dati dei file.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3dd14e8d3ea7d1e50f41633a7920a6d36becf789
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="528a5-103">Eseguire lo sviluppo per Archiviazione file di Azure con Python</span><span class="sxs-lookup"><span data-stu-id="528a5-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="528a5-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="528a5-104">About this tutorial</span></span>
<span data-ttu-id="528a5-105">Questa esercitazione illustra le nozioni base per l'uso di Python per sviluppare applicazioni o servizi che usano Archiviazione file di Azure per archiviare i dati dei file.</span><span class="sxs-lookup"><span data-stu-id="528a5-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="528a5-106">In questa esercitazione verrà creata una semplice applicazione console e verrà mostrato come eseguire le azioni di base con Python e Archiviazione file di Azure:</span><span class="sxs-lookup"><span data-stu-id="528a5-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="528a5-107">Creare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-107">Create Azure File shares</span></span>
* <span data-ttu-id="528a5-108">Creare directory</span><span class="sxs-lookup"><span data-stu-id="528a5-108">Create directories</span></span>
* <span data-ttu-id="528a5-109">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="528a5-110">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="528a5-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="528a5-111">Poiché Archiviazione file di Azure è accessibile tramite SMB, è possibile scrivere semplici applicazioni che accedono alla condivisione file di Azure usando le classi e le funzioni standard I/O di Python.</span><span class="sxs-lookup"><span data-stu-id="528a5-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="528a5-112">Questo articolo descrive come scrivere applicazioni che usano Azure Storage Python SDK, che usa l'[API REST di archiviazione file Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) per comunicare con Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="528a5-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="528a5-113">Configurare l'applicazione per usare Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="528a5-114">Aggiungere il codice seguente vicino all'inizio del file di origine Python da cui si desidera accedere all'archiviazione di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="528a5-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="528a5-115">Configurare una connessione all'archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="528a5-116">L'oggetto `FileService` consente di usare condivisioni, directory e file.</span><span class="sxs-lookup"><span data-stu-id="528a5-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="528a5-117">Il codice seguente crea un oggetto `FileService` usando il nome e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="528a5-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="528a5-118">Sostituire `<myaccount>` e `<mykey>` con il nome e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="528a5-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="528a5-119">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-119">Create an Azure File share</span></span>
<span data-ttu-id="528a5-120">Nell'esempio di codice seguente, è possibile usare un oggetto `FileService` per creare la condivisione, se non esiste.</span><span class="sxs-lookup"><span data-stu-id="528a5-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="528a5-121">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="528a5-121">Create a directory</span></span>
<span data-ttu-id="528a5-122">È inoltre possibile organizzare l'archiviazione inserendo i file all'interno di sottodirectory anziché inserirli tutti nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="528a5-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="528a5-123">L'archiviazione file di Azure permette di creare tutte le directory consentite dall'account.</span><span class="sxs-lookup"><span data-stu-id="528a5-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="528a5-124">Il codice riportato di seguito creerà una sottodirectory denominata **sampledir** nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="528a5-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="528a5-125">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="528a5-126">Per elencare i file e le directory di una condivisione, usare il metodo **list\_directories\_and\_files**.</span><span class="sxs-lookup"><span data-stu-id="528a5-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="528a5-127">Questo metodo restituisce un generatore.</span><span class="sxs-lookup"><span data-stu-id="528a5-127">This method returns a generator.</span></span> <span data-ttu-id="528a5-128">Il codice seguente consente di inviare alla console il valore **name** di ogni file e directory in una condivisione.</span><span class="sxs-lookup"><span data-stu-id="528a5-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="528a5-129">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="528a5-129">Upload a file</span></span> 
<span data-ttu-id="528a5-130">Una condivisione file di Azure contiene almeno una directory radice in cui possono risiedere i file.</span><span class="sxs-lookup"><span data-stu-id="528a5-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="528a5-131">In questa sezione verrà illustrato come caricare un file dall'archiviazione locale nella directory radice di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="528a5-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="528a5-132">Per creare un file e caricare dati, usare i metodi `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text`.</span><span class="sxs-lookup"><span data-stu-id="528a5-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="528a5-133">Questi sono metodi di carattere generale che eseguono il blocco dei dati necessario quando le dimensioni superano i 64 MB.</span><span class="sxs-lookup"><span data-stu-id="528a5-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="528a5-134">`create_file_from_path` carica i contenuti di un file dal percorso specificato, mentre `create_file_from_stream` carica i contenuti da un file/flusso già aperto.</span><span class="sxs-lookup"><span data-stu-id="528a5-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="528a5-135">`create_file_from_bytes` carica un array di byte, mentre `create_file_from_text` carica il valore di testo specificato usando la codifica specificata (l'impostazione predefinita è UTF-8).</span><span class="sxs-lookup"><span data-stu-id="528a5-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="528a5-136">Nell'esempio seguente viene caricato il contenuto del file **sunset.png** nel file **myfile**.</span><span class="sxs-lookup"><span data-stu-id="528a5-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="528a5-137">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="528a5-137">Download a file</span></span>
<span data-ttu-id="528a5-138">Per scaricare i dati da un file, usare `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` o `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="528a5-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="528a5-139">Questi sono metodi di carattere generale che eseguono il blocco dei dati necessario quando le dimensioni superano i 64 MB.</span><span class="sxs-lookup"><span data-stu-id="528a5-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="528a5-140">Nell'esempio seguente viene illustrato l'uso di `get_file_to_path` per scaricare il contenuto del file **myfile** e archiviarlo nel file **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="528a5-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="528a5-141">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="528a5-141">Delete a file</span></span>
<span data-ttu-id="528a5-142">Per eliminare un file, infine, chiamare `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="528a5-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="528a5-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="528a5-143">Next steps</span></span>
<span data-ttu-id="528a5-144">Dopo aver appreso come interagire con l'archiviazione di File di Azure con Python, seguire i collegamenti seguenti per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="528a5-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="528a5-145">Centro per sviluppatori di Python</span><span class="sxs-lookup"><span data-stu-id="528a5-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="528a5-146">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="528a5-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="528a5-147">Microsoft Azure Storage SDK per Python</span><span class="sxs-lookup"><span data-stu-id="528a5-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)