---
title: Spostare i dati da e verso l'archiviazione BLOB di Azure usando AzCopy | Documentazione Microsoft
description: Spostamento dei dati da e verso l'archiviazione BLOB di Azure utilizzando AzCopy.
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
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="94abf-103">Spostamento dei dati da e verso l'archivio BLOB di Azure tramite AzCopy</span><span class="sxs-lookup"><span data-stu-id="94abf-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="94abf-104">AzCopy è un'utilità della riga di comando progettata per le operazioni di caricamento, download e copia dei dati in e da servizi di archiviazione BLOB, file e tabelle di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94abf-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="94abf-105">Per istruzioni sull'installazione di AzCopy e informazioni aggiuntive sull'utilizzo della piattaforma Azure, vedere [Introduzione all’utilità della riga di comando di AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="94abf-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="94abf-106">Se si utilizza una macchina virtuale che è stata impostata con gli script forniti da [Macchine virtuali della scienza dei dati in Azure](machine-learning-data-science-virtual-machines.md), allora AzCopy è già installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="94abf-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="94abf-107">Per un'introduzione completa all'archiviazione BLOB di Azure, vedere [Introduzione all'archivio BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [Servizio BLOB di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="94abf-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="94abf-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94abf-108">Prerequisites</span></span>
<span data-ttu-id="94abf-109">In questo documento si presuppone di avere una sottoscrizione di Azure, un account di archiviazione e delle chiavi di archiviazione corrispondenti per quell'account.</span><span class="sxs-lookup"><span data-stu-id="94abf-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="94abf-110">Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94abf-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="94abf-111">Per configurare una sottoscrizione di Azure, vedere [Versione di prova gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94abf-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="94abf-112">Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="94abf-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="94abf-113">Eseguire i comandi di AzCopy</span><span class="sxs-lookup"><span data-stu-id="94abf-113">Run AzCopy commands</span></span>
<span data-ttu-id="94abf-114">Per eseguire i comandi di AzCopy, aprire una finestra di comando e passare alla directory di installazione di AzCopy contenente il file eseguibile AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="94abf-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="94abf-115">La sintassi di base per i comandi di AzCopy è la seguente:</span><span class="sxs-lookup"><span data-stu-id="94abf-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="94abf-116">È possibile aggiungere il percorso di installazione di AzCopy al percorso di sistema ed eseguire i comandi da qualsiasi directory.</span><span class="sxs-lookup"><span data-stu-id="94abf-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="94abf-117">Per impostazione predefinita, AzCopy viene installato in *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* o in *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="94abf-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="94abf-118">Caricare file in un BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="94abf-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="94abf-119">Per caricare un file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="94abf-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="94abf-120">Scaricare file da un BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="94abf-120">Download files from an Azure blob</span></span>
<span data-ttu-id="94abf-121">Per scaricare un file da un BLOB di Azure, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="94abf-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="94abf-122">Trasferire i BLOB tra contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="94abf-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="94abf-123">Per trasferire i BLOB tra i contenitori di Azure, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="94abf-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="94abf-124">Suggerimenti per l'utilizzo di AzCopy</span><span class="sxs-lookup"><span data-stu-id="94abf-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="94abf-125">Quando si **caricano** file, */S* caricherà i file in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="94abf-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="94abf-126">Senza questo parametro, i file nelle sottodirectory non vengono caricati.</span><span class="sxs-lookup"><span data-stu-id="94abf-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="94abf-127">Durante il **download** di file, */S* cerca il contenitore in modo ricorsivo fino a quando non vengono scaricati tutti i file nella directory specificata e nelle relative sottodirectory o tutti i file corrispondenti al criterio specificato nella directory data e nelle relative sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="94abf-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="94abf-128">Non è possibile specificare un **file BLOB specifico** da scaricare utilizzando il parametro */Source* .</span><span class="sxs-lookup"><span data-stu-id="94abf-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="94abf-129">Per scaricare un file specifico, specificare il nome del file BLOB per il download utilizzando il parametro */Pattern* .</span><span class="sxs-lookup"><span data-stu-id="94abf-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="94abf-130">**/S** può essere utilizzato per fare in modo che AzCopy cerchi il nome del file in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="94abf-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="94abf-131">Senza il parametro pattern, AzCopy scarica tutti i file nella directory.</span><span class="sxs-lookup"><span data-stu-id="94abf-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

