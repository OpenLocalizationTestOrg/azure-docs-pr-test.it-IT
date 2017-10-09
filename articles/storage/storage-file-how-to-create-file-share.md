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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="6bf6f-103">Creare una condivisione file in Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="6bf6f-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="6bf6f-104">È possibile creare condivisioni di File di Azure utilizzando [portale di Azure](https://portal.azure.com/), hello cmdlet PowerShell di archiviazione di Azure, hello librerie client di archiviazione di Azure o hello API REST di archiviazione di Azure. In questa esercitazione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="6bf6f-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="6bf6f-105">Come toocreate un File di Azure condividono utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bf6f-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="6bf6f-106">Come toocreate un File di Azure condividono con Powershell</span><span class="sxs-lookup"><span data-stu-id="6bf6f-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="6bf6f-107">Come toocreate un File di Azure condividono utilizzando CLI</span><span class="sxs-lookup"><span data-stu-id="6bf6f-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="6bf6f-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6bf6f-108">Prerequisites</span></span>
<span data-ttu-id="6bf6f-109">toocreate una condivisione di File di Azure, è possibile utilizzare un account di archiviazione già esistente, o [creare un nuovo account di archiviazione di Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6bf6f-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="6bf6f-110">toocreate una condivisione di File di Azure con PowerShell, è necessario hello account chiave e il nome dell'account di archiviazione...</span><span class="sxs-lookup"><span data-stu-id="6bf6f-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="6bf6f-111">Chiave dell'account di archiviazione è necessario se si prevede di toouse Powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="6bf6f-112">Creare la condivisione di file tramite hello portale</span><span class="sxs-lookup"><span data-stu-id="6bf6f-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="6bf6f-113">**Pannello Account tooStorage andare nel portale di Azure**:</span><span class="sxs-lookup"><span data-stu-id="6bf6f-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="6bf6f-114">![Pannello Account di archiviazione](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="6bf6f-115">**Fare clic sul pulsante Aggiungi condivisione file**:</span><span class="sxs-lookup"><span data-stu-id="6bf6f-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="6bf6f-116">![Fare clic su hello aggiungere il pulsante di condivisione file](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="6bf6f-117">**Specificare il nome e la quota. La quota attualmente non può essere superiore a 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="6bf6f-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="6bf6f-118">![Specificare un nome e una quota desiderata per la nuova condivisione di file hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="6bf6f-119">**Visualizzare la nuova condivisione file**: ![Visualizzare la nuova condivisione file](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="6bf6f-120">**Caricare un file**: ![Caricare un file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="6bf6f-121">**Esplorare la condivisione file e gestire le directory e i file**: ![Esplorare la condivisione file](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="6bf6f-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="6bf6f-122">Creare la condivisione file tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bf6f-122">Create file share through PowerShell</span></span>
<span data-ttu-id="6bf6f-123">tooprepare toouse PowerShell, scaricare e installare i cmdlet di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6bf6f-124">Vedere [come tooinstall e configurare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) per hello installare istruzioni sull'installazione e punto.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="6bf6f-125">È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="6bf6f-126">**Creare un contesto per l'account di archiviazione e la chiave** contesto hello incapsula hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="6bf6f-127">Per istruzioni sulla copia della chiave dell'account dal [portale di Azure](https://portal.azure.com/), vedere [Visualizzare e copiare le chiavi di accesso alle risorse di archiviazione](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="6bf6f-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="6bf6f-128">**Creare una nuova condivisione file**:</span><span class="sxs-lookup"><span data-stu-id="6bf6f-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="6bf6f-129">nome Hello della condivisione file deve essere tutti in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="6bf6f-130">Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bf6f-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="6bf6f-131">Creare una condivisione file tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="6bf6f-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="6bf6f-132">**tooprepare toouse interfaccia della riga di comando (CLI), scaricare e installare hello CLI di Azure.**</span><span class="sxs-lookup"><span data-stu-id="6bf6f-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="6bf6f-133">Vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2.md) e [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6bf6f-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="6bf6f-134">**Creare un account di archiviazione toohello di stringa di connessione in cui si desidera condivisione hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="6bf6f-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="6bf6f-135">Sostituire ```<storage-account>``` e ```<resource_group>``` con l'account nome e la risorsa gruppo di archiviazione nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="6bf6f-136">**Creare la condivisione file**</span><span class="sxs-lookup"><span data-stu-id="6bf6f-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="6bf6f-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bf6f-137">Next steps</span></span>
* [<span data-ttu-id="6bf6f-138">Connettersi e montare una condivisione file: Windows</span><span class="sxs-lookup"><span data-stu-id="6bf6f-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="6bf6f-139">Connettersi e montare una condivisione file: Linux</span><span class="sxs-lookup"><span data-stu-id="6bf6f-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="6bf6f-140">Connettersi e montare una condivisione file: macOS</span><span class="sxs-lookup"><span data-stu-id="6bf6f-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="6bf6f-141">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="6bf6f-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="6bf6f-142">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="6bf6f-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="6bf6f-143">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6bf6f-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)