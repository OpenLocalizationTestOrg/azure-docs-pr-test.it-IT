---
title: aaaMove tooand di dati dall'archiviazione Blob di Azure tramite AzCopy | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure tramite AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="534c2-103">Spostare dati tooand dall'archiviazione Blob di Azure tramite AzCopy</span><span class="sxs-lookup"><span data-stu-id="534c2-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="534c2-104">AzCopy è un'utilità della riga di comando progettata per il caricamento, download e copia tooand dati dal blob, file e archiviazione tabelle di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="534c2-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="534c2-105">Per istruzioni sull'installazione di AzCopy e informazioni aggiuntive sull'utilizzo con hello piattaforma Azure, vedere [introduzione hello utilità della riga di comando di AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="534c2-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="534c2-106">Se si utilizza macchina virtuale che è stato configurato con gli script hello disponibili in [macchine virtuali di analisi scientifica dei dati in Azure](machine-learning-data-science-virtual-machines.md), quindi AzCopy è già installata nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="534c2-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="534c2-107">Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="534c2-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="534c2-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="534c2-108">Prerequisites</span></span>
<span data-ttu-id="534c2-109">Questo documento presuppone di disporre di una sottoscrizione di Azure, un account di archiviazione e hello chiave di archiviazione corrispondente per tale account.</span><span class="sxs-lookup"><span data-stu-id="534c2-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="534c2-110">Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534c2-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="534c2-111">tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="534c2-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="534c2-112">Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="534c2-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="534c2-113">Eseguire i comandi di AzCopy</span><span class="sxs-lookup"><span data-stu-id="534c2-113">Run AzCopy commands</span></span>
<span data-ttu-id="534c2-114">comandi AzCopy toorun, aprire una finestra di comando e passare toohello AzCopy directory di installazione nel computer in cui si trova l'eseguibile AzCopy.exe hello.</span><span class="sxs-lookup"><span data-stu-id="534c2-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="534c2-115">sintassi di base per i comandi AzCopy Hello è:</span><span class="sxs-lookup"><span data-stu-id="534c2-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="534c2-116">È possibile aggiungere hello AzCopy tooyour sistema percorso di installazione e quindi eseguire i comandi di hello da qualsiasi directory.</span><span class="sxs-lookup"><span data-stu-id="534c2-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="534c2-117">Per impostazione predefinita, AzCopy è installato troppo*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* o *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="534c2-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="534c2-118">Caricare file tooan blob di Azure</span><span class="sxs-lookup"><span data-stu-id="534c2-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="534c2-119">tooupload un file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="534c2-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="534c2-120">Scaricare file da un BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="534c2-120">Download files from an Azure blob</span></span>
<span data-ttu-id="534c2-121">toodownload un file da un blob di Azure, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="534c2-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="534c2-122">Trasferire i BLOB tra contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="534c2-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="534c2-123">BLOB tootransfer tra i contenitori di Azure, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="534c2-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="534c2-124">Suggerimenti per l'utilizzo di AzCopy</span><span class="sxs-lookup"><span data-stu-id="534c2-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="534c2-125">Quando si **caricano** file, */S* caricherà i file in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="534c2-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="534c2-126">Senza questo parametro, i file nelle sottodirectory non vengono caricati.</span><span class="sxs-lookup"><span data-stu-id="534c2-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="534c2-127">Quando **download** file */S* ricerche hello contenitore in modo ricorsivo fino a quando tutti i file nella directory specificata hello e nelle relative sottodirectory, o tutti i file corrispondenti hello modello specificato in hello specificato Directory e nelle relative sottodirectory, vengono scaricati.</span><span class="sxs-lookup"><span data-stu-id="534c2-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="534c2-128">Non è possibile specificare un **file blob specifico** toodownload utilizzando hello */origine* parametro.</span><span class="sxs-lookup"><span data-stu-id="534c2-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="534c2-129">toodownload un file specifico, specificare toodownload nome file blob di hello utilizzando hello *modello/* parametro.</span><span class="sxs-lookup"><span data-stu-id="534c2-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="534c2-130">**/S** parametro può essere utilizzato toohave AzCopy cercare un nome di file modello in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="534c2-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="534c2-131">Senza il parametro di modello hello, AzCopy di scaricare tutti i file in tale directory.</span><span class="sxs-lookup"><span data-stu-id="534c2-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

