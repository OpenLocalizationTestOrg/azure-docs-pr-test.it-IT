---
title: aaaHow toocreate una condivisione di File di Azure | Documenti Microsoft
description: Toocreate come un file di Azure condividere in archiviazione di File di Azure utilizzando hello portale di Azure, PowerShell e hello CLI di Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="c6d83-103">Creare una condivisione file in Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d83-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="c6d83-104">È possibile creare condivisioni di File di Azure utilizzando [portale di Azure](https://portal.azure.com/), hello cmdlet PowerShell di archiviazione di Azure, hello librerie client di archiviazione di Azure o hello API REST di archiviazione di Azure. In questa esercitazione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="c6d83-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="c6d83-105">Come toocreate un File di Azure condividono utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d83-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="c6d83-106">Come toocreate un File di Azure condividono con Powershell</span><span class="sxs-lookup"><span data-stu-id="c6d83-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="c6d83-107">Come toocreate un File di Azure condividono utilizzando CLI</span><span class="sxs-lookup"><span data-stu-id="c6d83-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="c6d83-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6d83-108">Prerequisites</span></span>
<span data-ttu-id="c6d83-109">toocreate una condivisione di File di Azure, è possibile utilizzare un account di archiviazione già esistente, o [creare un nuovo account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6d83-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="c6d83-110">toocreate una condivisione di File di Azure con PowerShell, è necessario hello account chiave e il nome dell'account di archiviazione...</span><span class="sxs-lookup"><span data-stu-id="c6d83-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="c6d83-111">Chiave dell'account di archiviazione è necessario se si prevede di toouse Powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="c6d83-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="c6d83-112">Creare la condivisione di file tramite hello portale</span><span class="sxs-lookup"><span data-stu-id="c6d83-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="c6d83-113">**Pannello Account tooStorage andare nel portale di Azure**:</span><span class="sxs-lookup"><span data-stu-id="c6d83-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="c6d83-114">![Pannello Account di archiviazione](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="c6d83-115">**Fare clic sul pulsante Aggiungi condivisione file**:</span><span class="sxs-lookup"><span data-stu-id="c6d83-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="c6d83-116">![Fare clic su hello aggiungere il pulsante di condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="c6d83-117">**Specificare il nome e la quota. La quota attualmente non può essere superiore a 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="c6d83-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="c6d83-118">![Specificare un nome e una quota desiderata per la nuova condivisione di file hello](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="c6d83-119">**Visualizzare la nuova condivisione file**: ![Visualizzare la nuova condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="c6d83-120">**Caricare un file**: ![Caricare un file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="c6d83-121">**Esplorare la condivisione file e gestire le directory e i file**: ![Esplorare la condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="c6d83-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="c6d83-122">Creare la condivisione file tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d83-122">Create file share through PowerShell</span></span>
<span data-ttu-id="c6d83-123">tooprepare toouse PowerShell, scaricare e installare i cmdlet di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c6d83-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c6d83-124">Vedere [come tooinstall e configurare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) per hello installare istruzioni sull'installazione e punto.</span><span class="sxs-lookup"><span data-stu-id="c6d83-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="c6d83-125">È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello.</span><span class="sxs-lookup"><span data-stu-id="c6d83-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="c6d83-126">**Creare un contesto per l'account di archiviazione e la chiave** contesto hello incapsula hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="c6d83-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="c6d83-127">Per istruzioni sulla copia della chiave dell'account dal [portale di Azure](https://portal.azure.com/), vedere [Visualizzare e copiare le chiavi di accesso alle risorse di archiviazione](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="c6d83-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="c6d83-128">**Creare una nuova condivisione file**:</span><span class="sxs-lookup"><span data-stu-id="c6d83-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="c6d83-129">nome Hello della condivisione file deve essere tutti in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="c6d83-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="c6d83-130">Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6d83-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="c6d83-131">Creare una condivisione file tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="c6d83-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="c6d83-132">**tooprepare toouse interfaccia della riga di comando (CLI), scaricare e installare hello CLI di Azure.**</span><span class="sxs-lookup"><span data-stu-id="c6d83-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="c6d83-133">Vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2.md) e [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6d83-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="c6d83-134">**Creare un account di archiviazione toohello di stringa di connessione in cui si desidera condivisione hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="c6d83-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="c6d83-135">Sostituire ```<storage-account>``` e ```<resource_group>``` con l'account nome e la risorsa gruppo di archiviazione nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="c6d83-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="c6d83-136">**Creare la condivisione file**</span><span class="sxs-lookup"><span data-stu-id="c6d83-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="c6d83-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6d83-137">Next steps</span></span>
* [<span data-ttu-id="c6d83-138">Connettersi e montare una condivisione file: Windows</span><span class="sxs-lookup"><span data-stu-id="c6d83-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="c6d83-139">Connettersi e montare una condivisione file: Linux</span><span class="sxs-lookup"><span data-stu-id="c6d83-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="c6d83-140">Connettersi e montare una condivisione file: macOS</span><span class="sxs-lookup"><span data-stu-id="c6d83-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="c6d83-141">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d83-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="c6d83-142">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="c6d83-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="c6d83-143">Risoluzione dei problemi in Windows</span><span class="sxs-lookup"><span data-stu-id="c6d83-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="c6d83-144">Risoluzione dei problemi in Linux</span><span class="sxs-lookup"><span data-stu-id="c6d83-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   