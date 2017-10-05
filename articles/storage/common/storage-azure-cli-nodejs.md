---
title: Uso dell'interfaccia della riga di comando 1.0 di Azure con Archiviazione di Azure | Documentazione Microsoft
description: "Informazioni su come usare l'interfaccia della riga di comando 1.0 di Azure con Archiviazione di Azure per creare e gestire gli account di archiviazione e usare file e BLOB di Azure. La CLI di Azure è uno strumento multipiattaforma"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 837cf0f2b8db011b38de795339560574027030f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="1b15f-104">Uso dell'interfaccia della riga di comando 1.0 di Azure con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1b15f-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="1b15f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1b15f-105">Overview</span></span>

<span data-ttu-id="1b15f-106">L'interfaccia della riga di comando di Azure fornisce un insieme di comandi open source e multipiattaforma per utilizzare la piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="1b15f-107">Fornisce gran parte delle funzionalità disponibili nel [portale di Azure](https://portal.azure.com) , nonché funzionalità di accesso ai dati complessi.</span><span class="sxs-lookup"><span data-stu-id="1b15f-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="1b15f-108">In questa guida verrà illustrato come usare l'[interfaccia della riga di comando di Azure (Azure CLI)](../../cli-install-nodejs.md) per eseguire una serie di attività di sviluppo e amministrazione con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="1b15f-109">Si consiglia di scaricare e installare oppure di aggiornare il modulo alla versione di Azure PowerShell più recente prima di usare questa guida.</span><span class="sxs-lookup"><span data-stu-id="1b15f-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="1b15f-110">Questa guida si presuppone che si conoscano i concetti di base dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="1b15f-111">La guida fornisce diversi script che mostrano come usare PowerShell con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="1b15f-112">Prima di eseguire gli script, è necessario aggiornarne le variabili in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="1b15f-113">La guida fornisce esempi di comandi e script dell'interfaccia della riga di comando di Azure per gli account di archiviazione della versione classica.</span><span class="sxs-lookup"><span data-stu-id="1b15f-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="1b15f-114">Vedere [Uso dell'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) per i comandi dell'interfaccia della riga di comando di Azure per gli account di archiviazione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b15f-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="1b15f-115">Iniziare a utilizzare archiviazione di Azure e Azure CLI in 5 minuti</span><span class="sxs-lookup"><span data-stu-id="1b15f-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="1b15f-116">In questa guida utilizza Ubuntu per gli esempi, ma altre piattaforme del sistema operativo devono eseguire in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="1b15f-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="1b15f-117">**Novità in Azure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="1b15f-118">Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1b15f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="1b15f-119">Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1b15f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="1b15f-120">**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="1b15f-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="1b15f-121">Scaricare e installare CLI Azure seguendo le istruzioni riportate nel [installare CLI Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1b15f-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="1b15f-122">Dopo l'installazione dell'interfaccia della riga di comando di Azure, sarà possibile utilizzare il comando azure dall'interfaccia della riga di comando (Bash, terminale, prompt dei comandi) per accedere ai relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="1b15f-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="1b15f-123">Digitare il comando _azure_. Verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="1b15f-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Output del comando di esempio:](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="1b15f-125">Nell'interfaccia della riga di comando, digitare `azure storage` per elencare tutti i comandi di archiviazione di azure e ottenere una panoramica delle funzionalità offerte dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="1b15f-126">È possibile digitare il nome del comando con parametro **-h** (ad esempio, `azure storage share create -h`) per visualizzare i dettagli della sintassi del comando.</span><span class="sxs-lookup"><span data-stu-id="1b15f-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="1b15f-127">A questo punto viene fornito uno script semplice che mostra i comandi di base dell'interfaccia della riga di comando di Azure per accedere ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="1b15f-128">Lo script prima verrà chiesto di impostare due variabili per l'account di archiviazione e la chiave.</span><span class="sxs-lookup"><span data-stu-id="1b15f-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="1b15f-129">Lo script crea un nuovo contenitore in questo nuovo account di archiviazione e carica un file di immagine esistente (BLOB) in tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b15f-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="1b15f-130">Dopo aver elencato tutti i BLOB nel contenitore, lo script crea una nuova directory di destinazione nel computer locale e scarica il file di immagine.</span><span class="sxs-lookup"><span data-stu-id="1b15f-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="1b15f-131">Nel computer locale, aprire l'editor di testo preferito (vim ad esempio).</span><span class="sxs-lookup"><span data-stu-id="1b15f-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="1b15f-132">Digitare lo script precedente nell'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="1b15f-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="1b15f-133">A questo punto, è necessario aggiornare le variabili dello script in base alle impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="1b15f-134">**<storage_account_name>**: usare il nome specificato nello script oppure immettere un nuovo nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="1b15f-135">**Importante:** il nome dell'account di archiviazione deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="1b15f-136">Utilizzare caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="1b15f-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="1b15f-137">**<storage_account_key>**: la chiave di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="1b15f-138">**<container_name>**: usare il nome specificato nello script oppure immettere un nuovo nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b15f-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="1b15f-139">**<image_to_upload>**: immettere il percorso di un'immagine nel computer locale, ad esempio "~/images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="1b15f-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="1b15f-140">**<destination_folder>**: immettere il percorso di una directory locale per archiviare i file scaricati da Archiviazione di Azure, ad esempio "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="1b15f-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="1b15f-141">Dopo avere aggiornato le variabili necessarie in vim, premere le combinazioni di tasti `ESC`, `:`, `wq!` per salvare lo script.</span><span class="sxs-lookup"><span data-stu-id="1b15f-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="1b15f-142">Per eseguire questo script, è sufficiente digitare il nome del file script nella console di bash.</span><span class="sxs-lookup"><span data-stu-id="1b15f-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="1b15f-143">Dopo l'esecuzione dello script è necessario disporre di una cartella di destinazione locale che includa il file di immagine scaricato.</span><span class="sxs-lookup"><span data-stu-id="1b15f-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="1b15f-144">La schermata seguente mostra un output di esempio:</span><span class="sxs-lookup"><span data-stu-id="1b15f-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="1b15f-145">Dopo l'esecuzione dello script è necessario disporre di una cartella di destinazione locale che includa il file di immagine scaricato.</span><span class="sxs-lookup"><span data-stu-id="1b15f-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="1b15f-146">Gestione degli account di archiviazione con Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b15f-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="1b15f-147">Connettersi alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="1b15f-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="1b15f-148">Sebbene la maggior parte dei comandi di archiviazione funzioni senza una sottoscrizione di Azure, è consigliabile connettersi alla sottoscrizione dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="1b15f-149">Per configurare l'interfaccia della riga di comando di Azure per l'uso con la sottoscrizione, seguire la procedura nell'argomento [Connessione a una sottoscrizione di Azure dall'interfaccia della riga di comando di Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1b15f-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="1b15f-150">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-150">Create a new storage account</span></span>
<span data-ttu-id="1b15f-151">Per usare Archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="1b15f-152">Dopo aver configurato il computer per connettersi alla sottoscrizione, è possibile creare un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="1b15f-153">Il nome dell'account di archiviazione deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare numeri e lettere minuscole solo.</span><span class="sxs-lookup"><span data-stu-id="1b15f-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="1b15f-154">Impostare un account di archiviazione Azure predefinito nelle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="1b15f-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="1b15f-155">È possibile avere più account di archiviazione nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="1b15f-156">È possibile scegliere uno di essi e impostarlo in variabili di ambiente per tutti i comandi di archiviazione nella stessa sessione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="1b15f-157">Questo consente di eseguire i comandi di archiviazione di Azure PowerShell senza specificare in modo esplicito il contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="1b15f-158">Un altro modo per impostare un account di archiviazione predefinito utilizza stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="1b15f-159">In primo luogo per ottenere la stringa di connessione comando:</span><span class="sxs-lookup"><span data-stu-id="1b15f-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="1b15f-160">Quindi copiare la stringa di connessione di output e impostare alla variabile di ambiente:</span><span class="sxs-lookup"><span data-stu-id="1b15f-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="1b15f-161">Creare e gestire gli account di accesso</span><span class="sxs-lookup"><span data-stu-id="1b15f-161">Create and manage blobs</span></span>
<span data-ttu-id="1b15f-162">Archivio BLOB di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binari, a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b15f-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="1b15f-163">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="1b15f-164">Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b15f-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="1b15f-165">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15f-165">Create a container</span></span>
<span data-ttu-id="1b15f-166">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b15f-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="1b15f-167">È possibile creare un contenitore privato utilizzando il `azure storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="1b15f-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="1b15f-168">Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="1b15f-169">Per impedire l'accesso anonimo ai BLOB, impostare il parametro di autorizzazione su **Disattivato**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="1b15f-170">Per impostazione predefinita, il nuovo contenitore è privato ed è accessibile solo al proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="1b15f-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="1b15f-171">Per consentire l'accesso in lettura pubblico anonimo alle risorse BLOB, ma non ai metadati del contenitore o all'elenco dei BLOB nel contenitore, impostare il parametro di autorizzazione su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="1b15f-172">Per consentire l'accesso in lettura pubblico completo alle risorse BLOB, ai metadati del contenitore e all'elenco dei BLOB nel contenitore, impostare il parametro di autorizzazione **su Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="1b15f-173">Per altre informazioni, vedere [Gestire l'accesso in lettura anonimo a contenitori e BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1b15f-173">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="1b15f-174">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15f-174">Upload a blob into a container</span></span>
<span data-ttu-id="1b15f-175">Nell'archivio BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="1b15f-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1b15f-176">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b15f-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="1b15f-177">Per caricare BLOB in un contenitore, è possibile utilizzare il `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="1b15f-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="1b15f-178">Per impostazione predefinita, questo comando carica i file locali in un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="1b15f-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="1b15f-179">Per specificare il tipo per il BLOB, è possibile usare il parametro `--blobtype` .</span><span class="sxs-lookup"><span data-stu-id="1b15f-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="1b15f-180">Come scaricare i BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15f-180">Download blobs from a container</span></span>
<span data-ttu-id="1b15f-181">Nell'esempio seguente viene mostrato come scaricare i BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="1b15f-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="1b15f-182">Copiare i BLOB</span><span class="sxs-lookup"><span data-stu-id="1b15f-182">Copy blobs</span></span>
<span data-ttu-id="1b15f-183">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="1b15f-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="1b15f-184">Nell'esempio seguente viene illustrato come copiare BLOB da un account di archiviazione a un altro.</span><span class="sxs-lookup"><span data-stu-id="1b15f-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="1b15f-185">In questo esempio è possibile creare un contenitore in cui i BLOB sono pubblicamente, accessibile in forma anonima.</span><span class="sxs-lookup"><span data-stu-id="1b15f-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="1b15f-186">Nell'esempio viene eseguita una copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="1b15f-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="1b15f-187">È possibile monitorare lo stato di ogni operazione di copia eseguendo il `azure storage blob copy show` operazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="1b15f-188">Si noti che l'URL di origine fornito per l'operazione di copia devono essere accessibile pubblicamente o includere un token SAS (firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="1b15f-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="1b15f-189">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="1b15f-189">Delete a blob</span></span>
<span data-ttu-id="1b15f-190">Per eliminare un blob, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b15f-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="1b15f-191">Creare e gestire condivisioni di file</span><span class="sxs-lookup"><span data-stu-id="1b15f-191">Create and manage file shares</span></span>
<span data-ttu-id="1b15f-192">L'archiviazione file di Azure offre un'archiviazione condivisa per le applicazioni che usano il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="1b15f-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="1b15f-193">Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate.</span><span class="sxs-lookup"><span data-stu-id="1b15f-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="1b15f-194">È possibile gestire condivisioni di file e dati di file tramite la CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="1b15f-195">Per altre informazioni su Archiviazione file di Azure, vedere [Introduzione ad Archiviazione file di Azure in Windows](../storage-dotnet-how-to-use-files.md) o [Come usare Archiviazione file di Azure con Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1b15f-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="1b15f-196">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="1b15f-196">Create a file share</span></span>
<span data-ttu-id="1b15f-197">Una condivisione di archiviazione file è una condivisione file SMB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="1b15f-198">Tutte le directory e i file devono essere creati in una condivisione padre.</span><span class="sxs-lookup"><span data-stu-id="1b15f-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="1b15f-199">Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, fino ai limiti di capacità dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="1b15f-200">Nell'esempio seguente viene creata una condivisione file denominata **myshare**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="1b15f-201">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="1b15f-201">Create a directory</span></span>
<span data-ttu-id="1b15f-202">Una directory fornisce una struttura gerarchica facoltativa per una condivisione di file di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15f-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="1b15f-203">Nell'esempio seguente viene creata una directory denominata **myDir** nella condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="1b15f-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="1b15f-204">Si noti che tale percorso di directory può includere più livelli, *ad esempio*, **un / b**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="1b15f-205">Tuttavia è necessario assicurarsi che tutte le directory padre esistano.</span><span class="sxs-lookup"><span data-stu-id="1b15f-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="1b15f-206">Ad esempio, per il percorso **a/b**, è necessario creare prima la directory **a** e poi la directory **b**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="1b15f-207">Caricare un file locale nella directory</span><span class="sxs-lookup"><span data-stu-id="1b15f-207">Upload a local file to directory</span></span>
<span data-ttu-id="1b15f-208">Nell'esempio seguente viene caricato un file dalla directory **~/temp/samplefile.txt** to the **myDir**.</span><span class="sxs-lookup"><span data-stu-id="1b15f-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="1b15f-209">Modificare il percorso del file in modo che punti a un file valido nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="1b15f-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="1b15f-210">Si noti che un file nella condivisione può essere fino a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="1b15f-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="1b15f-211">Elenco dei file nella directory principale della condivisione o directory</span><span class="sxs-lookup"><span data-stu-id="1b15f-211">List the files in the share root or directory</span></span>
<span data-ttu-id="1b15f-212">È possibile elencare i file e sottodirectory nella directory principale della condivisione o una directory utilizzando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b15f-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="1b15f-213">Si noti che il nome della directory è facoltativo per l'operazione di elenco.</span><span class="sxs-lookup"><span data-stu-id="1b15f-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="1b15f-214">Se omesso, il comando Elenca il contenuto della directory radice della condivisione.</span><span class="sxs-lookup"><span data-stu-id="1b15f-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="1b15f-215">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="1b15f-215">Copy files</span></span>
<span data-ttu-id="1b15f-216">A partire dalla versione 0.9.8.CLI di Azure, è possibile copiare un file in un altro file, un file in un BLOB o un BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="1b15f-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="1b15f-217">Di seguito viene illustrato come eseguire queste operazioni di copia utilizzando i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="1b15f-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="1b15f-218">Copiare un file nella nuova directory:</span><span class="sxs-lookup"><span data-stu-id="1b15f-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="1b15f-219">Copiare un BLOB in una directory del file:</span><span class="sxs-lookup"><span data-stu-id="1b15f-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="1b15f-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b15f-220">Next Steps</span></span>

<span data-ttu-id="1b15f-221">È possibile trovare riferimenti ai comandi dell'interfaccia della riga di comando 1.0 di Azure da usare con le risorse di Archiviazione qui:</span><span class="sxs-lookup"><span data-stu-id="1b15f-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="1b15f-222">Comandi dell'interfaccia della riga di comando Azure in modalità Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b15f-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="1b15f-223">Comandi dell'interfaccia della riga di comando di Azure in modalità Gestione servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="1b15f-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="1b15f-224">È anche possibile provare l'[interfaccia della riga di comando di Azure 2.0](../storage-azure-cli.md), ovvero l'interfaccia della riga di comando di nuova generazione scritta in Python per il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b15f-224">You may also like to try the [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>
