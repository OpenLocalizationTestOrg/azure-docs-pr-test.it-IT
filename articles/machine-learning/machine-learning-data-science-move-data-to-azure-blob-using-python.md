---
title: Spostamento dei dati da e verso l'archiviazione BLOB di Azure utilizzando Python | Documentazione Microsoft
description: Spostamento dei dati da e verso l'archiviazione BLOB di Azure utilizzando Python.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="ddbc7-103">Spostamento dei dati da e verso l'archivio BLOB di Azure tramite Python</span><span class="sxs-lookup"><span data-stu-id="ddbc7-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="ddbc7-104">Questo argomento descrive come elencare, caricare e scaricare BLOB usando l'API Python.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="ddbc7-105">Con l'API Python fornita in Azure SDK, è possibile:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="ddbc7-106">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="ddbc7-106">Create a container</span></span>
* <span data-ttu-id="ddbc7-107">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="ddbc7-107">Upload a blob into a container</span></span>
* <span data-ttu-id="ddbc7-108">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="ddbc7-108">Download blobs</span></span>
* <span data-ttu-id="ddbc7-109">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="ddbc7-109">List the blobs in a container</span></span>
* <span data-ttu-id="ddbc7-110">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="ddbc7-110">Delete a blob</span></span>

<span data-ttu-id="ddbc7-111">Per ulteriori informazioni sull'utilizzo dell’API di Python, vedere [Come utilizzare il servizio di archiviazione BLOB da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ddbc7-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="ddbc7-112">Se si utilizza una macchina virtuale che è stata impostata con gli script forniti da [Macchine virtuali della scienza dei dati in Azure](machine-learning-data-science-virtual-machines.md), allora AzCopy è già installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ddbc7-113">Per un'introduzione completa all'archiviazione BLOB di Azure, vedere [Introduzione all'archivio BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [Servizio BLOB di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddbc7-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ddbc7-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ddbc7-114">Prerequisites</span></span>
<span data-ttu-id="ddbc7-115">In questo documento si presuppone di avere una sottoscrizione di Azure, un account di archiviazione e chiavi di archiviazione corrispondenti per quell'account.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="ddbc7-116">Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="ddbc7-117">Per configurare una sottoscrizione di Azure, vedere [Versione di prova gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddbc7-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ddbc7-118">Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddbc7-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="ddbc7-119">Caricamento di dati BLOB</span><span class="sxs-lookup"><span data-stu-id="ddbc7-119">Upload Data to Blob</span></span>
<span data-ttu-id="ddbc7-120">Aggiungere lo snippet seguente vicino all'inizio di ogni codice Python in cui si desidera accedere all'archiviazione di Azure a livello di programmazione:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="ddbc7-121">L'oggetto **BlobService** consente di lavorare con contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ddbc7-122">Il codice seguente crea un oggetto BlobService usando il nome e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="ddbc7-123">Sostituire nome e chiave dell'account con la chiave e l'account effettivi.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="ddbc7-124">Per caricare dati in un BLOB, utilizzare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="ddbc7-125">put\_block\_blob\_from\_path (consente di caricare il contenuto di un file dal percorso specificato)</span><span class="sxs-lookup"><span data-stu-id="ddbc7-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="ddbc7-126">put\_block_blob\_from\_file (consente di caricare il contenuto da un flusso/file già aperto)</span><span class="sxs-lookup"><span data-stu-id="ddbc7-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="ddbc7-127">put\_block\_blob\_from\_bytes (consente di caricare una matrice di byte)</span><span class="sxs-lookup"><span data-stu-id="ddbc7-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="ddbc7-128">put\_block\_blob\_from\_text (consente di caricare il valore di testo specificato mediante la codifica specificata)</span><span class="sxs-lookup"><span data-stu-id="ddbc7-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="ddbc7-129">Il seguente codice di esempio consente di caricare un file locale in un contenitore:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ddbc7-130">Il seguente codice di esempio consente di caricare tutti i file (a esclusione delle directory) in una directory locale in un'archiviazione BLOB:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="ddbc7-131">Download dei dati dal BLOB</span><span class="sxs-lookup"><span data-stu-id="ddbc7-131">Download Data from Blob</span></span>
<span data-ttu-id="ddbc7-132">Per scaricare dati da un BLOB, utilizzare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="ddbc7-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="ddbc7-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="ddbc7-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="ddbc7-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="ddbc7-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="ddbc7-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="ddbc7-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="ddbc7-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="ddbc7-137">Questi sono metodi che eseguono il blocco dei dati necessario quando le dimensioni superano i 64 MB.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="ddbc7-138">Il seguente codice di esempio consente di scaricare i contenuti di un BLOB in un contenitore in un file locale:</span><span class="sxs-lookup"><span data-stu-id="ddbc7-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ddbc7-139">Il seguente codice di esempio consente di scaricare tutti i BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="ddbc7-140">Usa list\_blobs per ottenere un elenco di BLOB disponibili nel contenitore e li scarica in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="ddbc7-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading the data %s"%blob.name
