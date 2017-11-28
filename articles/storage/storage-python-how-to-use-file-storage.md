---
title: aaaDevelop per l'archiviazione di File di Azure con Python | Documenti Microsoft
description: Informazioni su come toodevelop Python applicazioni e servizi che utilizzano i File di Azure storage toostore dati dei file.
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="64d86-103">Eseguire lo sviluppo per Archiviazione file di Azure con Python</span><span class="sxs-lookup"><span data-stu-id="64d86-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="64d86-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="64d86-104">About this tutorial</span></span>
<span data-ttu-id="64d86-105">Questa esercitazione verrà illustrato l'utilizzo di Python toodevelop applicazioni o servizi che utilizzano i File di Azure storage toostore file dati di base di hello.</span><span class="sxs-lookup"><span data-stu-id="64d86-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="64d86-106">In questa esercitazione verrà creata una semplice applicazione console e Mostra come tooperform azioni di base con l'archiviazione di Python e File di Azure:</span><span class="sxs-lookup"><span data-stu-id="64d86-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="64d86-107">Creare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="64d86-107">Create Azure File shares</span></span>
* <span data-ttu-id="64d86-108">Creare directory</span><span class="sxs-lookup"><span data-stu-id="64d86-108">Create directories</span></span>
* <span data-ttu-id="64d86-109">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="64d86-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="64d86-110">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="64d86-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="64d86-111">Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le funzioni e classi dei / o Python standard hello.</span><span class="sxs-lookup"><span data-stu-id="64d86-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="64d86-112">In questo articolo descrive come le applicazioni che usano toowrite hello Python Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.</span><span class="sxs-lookup"><span data-stu-id="64d86-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="64d86-113">Configurare l'archiviazione di File di Azure di toouse applicazione</span><span class="sxs-lookup"><span data-stu-id="64d86-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="64d86-114">Aggiungere il seguente hello superiore hello di qualsiasi file di origine di Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="64d86-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="64d86-115">Impostare un tooAzure connessione archiviazione File</span><span class="sxs-lookup"><span data-stu-id="64d86-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="64d86-116">Hello `FileService` oggetto consente di lavorare con file, directory e condivisioni.</span><span class="sxs-lookup"><span data-stu-id="64d86-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="64d86-117">Hello codice seguente viene creata una `FileService` oggetto utilizzando hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="64d86-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="64d86-118">Sostituire `<myaccount>` e `<mykey>` con il nome e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="64d86-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="64d86-119">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="64d86-119">Create an Azure File share</span></span>
<span data-ttu-id="64d86-120">Nell'esempio di codice seguente di hello, è possibile utilizzare un `FileService` condivisione di hello toocreate oggetto se non esiste.</span><span class="sxs-lookup"><span data-stu-id="64d86-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="64d86-121">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="64d86-121">Create a directory</span></span>
<span data-ttu-id="64d86-122">È anche possibile organizzare archiviazione inserendo i file all'interno di sottodirectory, anziché tutti gli elementi nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="64d86-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="64d86-123">Archiviazione di File di Azure consente toocreate come consentire molte directory come l'account.</span><span class="sxs-lookup"><span data-stu-id="64d86-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="64d86-124">codice Hello seguente verrà creata una sottodirectory denominata **sampledir** nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="64d86-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="64d86-125">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="64d86-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="64d86-126">toolist hello file e directory in una condivisione, utilizzare hello **elenco\_directory\_e\_file** metodo.</span><span class="sxs-lookup"><span data-stu-id="64d86-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="64d86-127">Questo metodo restituisce un generatore.</span><span class="sxs-lookup"><span data-stu-id="64d86-127">This method returns a generator.</span></span> <span data-ttu-id="64d86-128">il codice seguente Hello restituisce hello **nome** di ogni file e directory in una console toohello condivisione.</span><span class="sxs-lookup"><span data-stu-id="64d86-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="64d86-129">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="64d86-129">Upload a file</span></span> 
<span data-ttu-id="64d86-130">File di Azure condivisione contiene in hello molto meno, una directory radice in cui i file possono trovarsi.</span><span class="sxs-lookup"><span data-stu-id="64d86-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="64d86-131">In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="64d86-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="64d86-132">toocreate un file e caricare i dati, utilizzare hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text` metodi.</span><span class="sxs-lookup"><span data-stu-id="64d86-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="64d86-133">Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.</span><span class="sxs-lookup"><span data-stu-id="64d86-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="64d86-134">`create_file_from_path`caricamenti hello contenuto di un file dal percorso specificato hello, e `create_file_from_stream` caricamenti hello contenuto dal flusso file già aperto.</span><span class="sxs-lookup"><span data-stu-id="64d86-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="64d86-135">`create_file_from_bytes`Carica una matrice di byte, e `create_file_from_text` caricamenti hello specificato il valore di testo utilizzando hello codifica (impostazioni predefinite tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="64d86-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="64d86-136">esempio Hello carica il contenuto di hello di hello **sunset.png** file hello **myfile** file.</span><span class="sxs-lookup"><span data-stu-id="64d86-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="64d86-137">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="64d86-137">Download a file</span></span>
<span data-ttu-id="64d86-138">toodownload dati da un file, utilizzare `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, o `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="64d86-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="64d86-139">Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.</span><span class="sxs-lookup"><span data-stu-id="64d86-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="64d86-140">Hello seguente viene illustrato l'utilizzo `get_file_to_path` contenuto hello toodownload di hello **myfile** file e archiviarlo toohello **out sunset.png** file.</span><span class="sxs-lookup"><span data-stu-id="64d86-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="64d86-141">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="64d86-141">Delete a file</span></span>
<span data-ttu-id="64d86-142">Chiamare infine toodelete un file, `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="64d86-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="64d86-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64d86-143">Next steps</span></span>
<span data-ttu-id="64d86-144">Ora che si è appreso come toomanipulate archiviazione di File di Azure con Python, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="64d86-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="64d86-145">Centro per sviluppatori di Python</span><span class="sxs-lookup"><span data-stu-id="64d86-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="64d86-146">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="64d86-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="64d86-147">Microsoft Azure Storage SDK per Python</span><span class="sxs-lookup"><span data-stu-id="64d86-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)