---
title: aaaMove tooand di dati dall'archiviazione Blob di Azure usando Python | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure Usa Python
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
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="105a8-103">Spostare dati tooand dall'archiviazione Blob di Azure Usa Python</span><span class="sxs-lookup"><span data-stu-id="105a8-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="105a8-104">In questo argomento viene descritto come toolist, caricare e scaricare BLOB utilizzando hello API Python.</span><span class="sxs-lookup"><span data-stu-id="105a8-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="105a8-105">Con hello API Python fornito in Azure SDK, è possibile:</span><span class="sxs-lookup"><span data-stu-id="105a8-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="105a8-106">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="105a8-106">Create a container</span></span>
* <span data-ttu-id="105a8-107">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="105a8-107">Upload a blob into a container</span></span>
* <span data-ttu-id="105a8-108">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="105a8-108">Download blobs</span></span>
* <span data-ttu-id="105a8-109">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="105a8-109">List hello blobs in a container</span></span>
* <span data-ttu-id="105a8-110">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="105a8-110">Delete a blob</span></span>

<span data-ttu-id="105a8-111">Per ulteriori informazioni sull'utilizzo di hello Python API, vedere [come tooUse hello servizio di archiviazione Blob da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="105a8-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="105a8-112">Se si utilizza macchina virtuale che è stato configurato con gli script hello disponibili in [macchine virtuali di analisi scientifica dei dati in Azure](machine-learning-data-science-virtual-machines.md), quindi AzCopy è già installata nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="105a8-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="105a8-113">Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="105a8-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="105a8-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="105a8-114">Prerequisites</span></span>
<span data-ttu-id="105a8-115">Questo documento si presuppone la presenza di una sottoscrizione di Azure, un account di archiviazione e chiave di archiviazione per l'account corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="105a8-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="105a8-116">Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="105a8-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="105a8-117">tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="105a8-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="105a8-118">Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="105a8-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="105a8-119">Caricare dati tooBlob</span><span class="sxs-lookup"><span data-stu-id="105a8-119">Upload Data tooBlob</span></span>
<span data-ttu-id="105a8-120">Aggiungere hello seguente frammento di codice superiore hello del codice Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="105a8-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="105a8-121">Hello **BlobService** oggetto consente di collaborare con i contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="105a8-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="105a8-122">Hello di codice seguente crea un oggetto di BlobService tramite hello archiviazione nome account e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="105a8-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="105a8-123">Sostituire nome e chiave dell'account con la chiave e l'account effettivi.</span><span class="sxs-lookup"><span data-stu-id="105a8-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="105a8-124">Utilizzare hello blob tooa di metodi tooupload dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="105a8-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="105a8-125">inserire\_blocco\_blob\_da\_percorso (carica il contenuto di hello di un file dal percorso specificato hello)</span><span class="sxs-lookup"><span data-stu-id="105a8-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="105a8-126">inserire\_block_blob\_da\_file (carica il contenuto di hello dal flusso file già aperto)</span><span class="sxs-lookup"><span data-stu-id="105a8-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="105a8-127">put\_block\_blob\_from\_bytes (consente di caricare una matrice di byte)</span><span class="sxs-lookup"><span data-stu-id="105a8-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="105a8-128">inserire\_blocco\_blob\_da\_testo (Carica hello specificato il valore di testo utilizzando hello specificato codifica)</span><span class="sxs-lookup"><span data-stu-id="105a8-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="105a8-129">Hello seguente codice di esempio carica un contenitore di tooa file locale:</span><span class="sxs-lookup"><span data-stu-id="105a8-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="105a8-130">Hello codice di esempio seguente consente di caricare tutti i file hello (escluse le directory) in un archivio tooblob directory locale:</span><span class="sxs-lookup"><span data-stu-id="105a8-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="105a8-131">Download dei dati dal BLOB</span><span class="sxs-lookup"><span data-stu-id="105a8-131">Download Data from Blob</span></span>
<span data-ttu-id="105a8-132">Utilizzare hello seguente dati toodownload metodi da un blob:</span><span class="sxs-lookup"><span data-stu-id="105a8-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="105a8-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="105a8-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="105a8-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="105a8-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="105a8-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="105a8-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="105a8-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="105a8-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="105a8-137">Questi metodi che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.</span><span class="sxs-lookup"><span data-stu-id="105a8-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="105a8-138">Hello codice di esempio seguente consente di scaricare contenuto hello di un blob in un file locale tooa di contenitore:</span><span class="sxs-lookup"><span data-stu-id="105a8-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="105a8-139">Hello codice di esempio seguente Scarica tutti i BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="105a8-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="105a8-140">Usa elenco\_BLOB elenco hello tooget di BLOB disponibili nel contenitore hello e li scarica tooa directory locale.</span><span class="sxs-lookup"><span data-stu-id="105a8-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
            print "something wrong happened when downloading hello data %s"%blob.name
