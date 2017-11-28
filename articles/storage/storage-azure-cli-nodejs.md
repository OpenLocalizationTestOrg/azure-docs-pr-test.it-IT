---
title: aaaUsing hello Azure CLI 1.0 con archiviazione di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello interfaccia della riga di comando di Azure (Azure CLI) 1.0 con toocreate di archiviazione di Azure e gestire gli account di archiviazione e utilizzo di BLOB di Azure e i file. Hello CLI di Azure è uno strumento multipiattaforma"
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
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="4517d-104">Utilizzo di hello Azure CLI 1.0 con archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4517d-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="4517d-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4517d-105">Overview</span></span>

<span data-ttu-id="4517d-106">Hello CLI di Azure fornisce un set di open source, multipiattaforma comandi per l'utilizzo con hello piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="4517d-107">Fornisce gran parte delle stesse funzionalità, vedere hello hello [portale di Azure](https://portal.azure.com) funzionalità di accesso ai dati e avanzati.</span><span class="sxs-lookup"><span data-stu-id="4517d-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="4517d-108">In questa Guida, si esamineranno come toouse [interfaccia della riga di comando di Azure (Azure CLI)](../cli-install-nodejs.md) tooperform un'ampia gamma di attività di sviluppo e amministrazione con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="4517d-109">È consigliabile scaricare e installare o aggiornare toohello CLI di Azure più recenti prima di usare questa Guida.</span><span class="sxs-lookup"><span data-stu-id="4517d-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="4517d-110">Questa guida presuppone la conoscenza dei concetti di base hello dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="4517d-111">Guida di Hello fornisce un numero di script utilizzo hello toodemonstrate di hello CLI di Azure con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="4517d-112">Essere tooupdate che le variabili dello script hello in base alla configurazione prima di eseguire ogni script.</span><span class="sxs-lookup"><span data-stu-id="4517d-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="4517d-113">Guida di Hello fornisce esempi di script e comando CLI di Azure di hello per gli account di archiviazione classico.</span><span class="sxs-lookup"><span data-stu-id="4517d-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="4517d-114">Vedere [Using hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) per i comandi CLI di Azure per gli account di archiviazione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4517d-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="4517d-115">Introduzione all'archiviazione di Azure e hello CLI di Azure in 5 minuti</span><span class="sxs-lookup"><span data-stu-id="4517d-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="4517d-116">In questa guida utilizza Ubuntu per gli esempi, ma altre piattaforme del sistema operativo devono eseguire in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="4517d-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="4517d-117">**Nuovo tooAzure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato a tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4517d-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="4517d-118">Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).</span><span class="sxs-lookup"><span data-stu-id="4517d-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="4517d-119">Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4517d-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="4517d-120">**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="4517d-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="4517d-121">Scaricare e installare hello Azure CLI hello alle istruzioni descritte nella [installazione hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4517d-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="4517d-122">Una volta hello CLI di Azure è stato installato, sarà in grado di toouse hello azure comando i comandi di Azure CLI hello tooaccess interfaccia della riga di comando (Bash, Terminal, prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="4517d-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="4517d-123">Hello tipo _azure_ comando e si dovrebbe essere hello output seguente.</span><span class="sxs-lookup"><span data-stu-id="4517d-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Output del comando di esempio:][Image1]
3. <span data-ttu-id="4517d-125">Nell'interfaccia della riga di comando hello, digitare `azure storage` toolist tutte hello i comandi di archiviazione di azure e ottenere una visione prima di hello funzionalità hello CLI di Azure fornisce.</span><span class="sxs-lookup"><span data-stu-id="4517d-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="4517d-126">È possibile digitare il nome di comando con **-h** parametro (ad esempio, `azure storage share create -h`) toosee dettagli della sintassi del comando.</span><span class="sxs-lookup"><span data-stu-id="4517d-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="4517d-127">A questo punto, verrà fornita è un semplice script che mostra tooaccess di comandi CLI di Azure basic di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="4517d-128">script Hello verrà innanzitutto richiesto tooset due variabili per l'account di archiviazione e la chiave.</span><span class="sxs-lookup"><span data-stu-id="4517d-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="4517d-129">Quindi, hello script creare un nuovo contenitore in questo nuovo account di archiviazione e caricare un contenitore toothat (blob) di file di immagine esistente.</span><span class="sxs-lookup"><span data-stu-id="4517d-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="4517d-130">Dopo aver hello script permette di elencare tutti i BLOB nel contenitore, verrà scaricato hello immagine toohello destinazione directory del file esistente sul computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="4517d-131">Nel computer locale, aprire l'editor di testo preferito (vim ad esempio).</span><span class="sxs-lookup"><span data-stu-id="4517d-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="4517d-132">Digitare hello sopra script nell'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="4517d-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="4517d-133">A questo punto, è necessario tooupdate hello scripting di variabili in base alle impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="4517d-134">**< Storage_account_name >** utilizzare hello dato nome nello script hello o immettere un nuovo nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="4517d-135">**Importante:** nome hello hello dell'account di archiviazione deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="4517d-136">Utilizzare caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="4517d-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="4517d-137">**< storage_account_key >** chiave di accesso hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="4517d-138">**< Container_name >** utilizzare hello dato nome nello script hello o immettere un nuovo nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="4517d-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="4517d-139">**< Image_to_upload >** immettere un'immagine di tooa percorso sul computer locale, ad esempio: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="4517d-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="4517d-140">**< Destination_folder >** immettere un percorso tooa directory locale toostore scaricare i file dall'archiviazione di Azure, ad esempio: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="4517d-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="4517d-141">Dopo aver aggiornato le variabili necessarie hello in vim, premere le combinazioni di tasti `ESC`, `:`, `wq!` script hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4517d-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="4517d-142">toorun questo script, semplicemente tipo hello nome del file script nella console di hello bash.</span><span class="sxs-lookup"><span data-stu-id="4517d-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="4517d-143">Quando si esegue questo script, è una cartella di destinazione locale che include i file di immagine scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="4517d-144">Hello seguente schermata mostra un esempio dell'output:</span><span class="sxs-lookup"><span data-stu-id="4517d-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="4517d-145">Dopo l'esecuzione di script hello è una cartella di destinazione locale che include i file di immagine scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="4517d-146">Gestire gli account di archiviazione con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="4517d-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="4517d-147">Connettersi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="4517d-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="4517d-148">Anche se la maggior parte dei comandi di archiviazione hello funzionerà senza una sottoscrizione di Azure, è consigliabile tooconnect tooyour sottoscrizione hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="4517d-149">tooconfigure hello Azure CLI toowork con la sottoscrizione, seguire i passaggi hello [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4517d-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="4517d-150">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-150">Create a new storage account</span></span>
<span data-ttu-id="4517d-151">toouse archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="4517d-152">Dopo aver configurato la sottoscrizione di tooyour tooconnect computer, è possibile creare un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="4517d-153">nome di Hello dell'account di archiviazione deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare i numeri e lettere minuscole solo.</span><span class="sxs-lookup"><span data-stu-id="4517d-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="4517d-154">Impostare un account di archiviazione Azure predefinito nelle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="4517d-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="4517d-155">È possibile avere più account di archiviazione nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4517d-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="4517d-156">È possibile scegliere uno di essi e impostate nel hello le variabili di ambiente per l'archiviazione hello tutti i comandi hello stessa sessione.</span><span class="sxs-lookup"><span data-stu-id="4517d-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="4517d-157">Ciò consente l'archiviazione di Azure CLI hello toorun comandi senza specificare archiviazione hello account e la chiave in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="4517d-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="4517d-158">Stringa di connessione utilizza un altro modo tooset un account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="4517d-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="4517d-159">Prima di tutto ottenere la stringa di connessione hello dal comando:</span><span class="sxs-lookup"><span data-stu-id="4517d-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="4517d-160">Copiare la stringa di connessione di output di hello e impostarlo tooenvironment variabile:</span><span class="sxs-lookup"><span data-stu-id="4517d-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="4517d-161">Creare e gestire gli account di accesso</span><span class="sxs-lookup"><span data-stu-id="4517d-161">Create and manage blobs</span></span>
<span data-ttu-id="4517d-162">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4517d-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="4517d-163">In questa sezione si presuppone che si ha già familiarità con i concetti di archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="4517d-164">Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="4517d-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="4517d-165">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="4517d-165">Create a container</span></span>
<span data-ttu-id="4517d-166">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4517d-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="4517d-167">È possibile creare un contenitore privato utilizzando hello `azure storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="4517d-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="4517d-168">Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**.</span><span class="sxs-lookup"><span data-stu-id="4517d-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="4517d-169">tooprevent anonimo accesso troppo accedere tooblobs, il parametro di autorizzazione del set di hello**Off**.</span><span class="sxs-lookup"><span data-stu-id="4517d-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="4517d-170">Per impostazione predefinita, hello nuovo contenitore è privato e accessibile solo dal proprietario dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="4517d-171">in lettura pubblico anonimo tooallow tooblob di accedere alle risorse, ma non toocontainer metadati o toohello elenco di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**Blob**.</span><span class="sxs-lookup"><span data-stu-id="4517d-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="4517d-172">in lettura pubblico completo tooallow tooblob di accedere alle risorse e i metadati del contenitore elenco hello di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**contenitore**.</span><span class="sxs-lookup"><span data-stu-id="4517d-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="4517d-173">Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4517d-173">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4517d-174">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="4517d-174">Upload a blob into a container</span></span>
<span data-ttu-id="4517d-175">Nell'archivio BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="4517d-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="4517d-176">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="4517d-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="4517d-177">i BLOB nel contenitore tooa tooupload, è possibile utilizzare hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="4517d-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="4517d-178">Per impostazione predefinita, questo comando Carica blob in blocchi tooa hello file locali.</span><span class="sxs-lookup"><span data-stu-id="4517d-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="4517d-179">tipo di hello toospecify per blob hello, è possibile utilizzare hello `--blobtype` parametro.</span><span class="sxs-lookup"><span data-stu-id="4517d-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="4517d-180">Come scaricare i BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="4517d-180">Download blobs from a container</span></span>
<span data-ttu-id="4517d-181">Hello di esempio seguente viene illustrato come toodownload BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4517d-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="4517d-182">Copiare i BLOB</span><span class="sxs-lookup"><span data-stu-id="4517d-182">Copy blobs</span></span>
<span data-ttu-id="4517d-183">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="4517d-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="4517d-184">Hello esempio seguente viene illustrato come toocopy BLOB da un archivio account tooanother.</span><span class="sxs-lookup"><span data-stu-id="4517d-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="4517d-185">In questo esempio è possibile creare un contenitore in cui i BLOB sono pubblicamente, accessibile in forma anonima.</span><span class="sxs-lookup"><span data-stu-id="4517d-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="4517d-186">Nell'esempio viene eseguita una copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="4517d-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="4517d-187">È possibile monitorare lo stato di hello di ogni operazione di copia eseguendo hello `azure storage blob copy show` operazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="4517d-188">Si noti che hello origine URL fornito per l'operazione di copia hello deve essere accessibile pubblicamente o includono un token di firma di accesso condiviso (firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="4517d-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="4517d-189">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="4517d-189">Delete a blob</span></span>
<span data-ttu-id="4517d-190">toodelete un blob, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4517d-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="4517d-191">Creare e gestire condivisioni di file</span><span class="sxs-lookup"><span data-stu-id="4517d-191">Create and manage file shares</span></span>
<span data-ttu-id="4517d-192">Archiviazione di File di Azure offre archiviazione condivisa per applicazioni che utilizzano il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="4517d-193">Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate.</span><span class="sxs-lookup"><span data-stu-id="4517d-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="4517d-194">È possibile gestire condivisioni file e dati di file tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="4517d-195">Per ulteriori informazioni sull'archiviazione di File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](storage-dotnet-how-to-use-files.md) o [come archiviazione di File di Azure con Linux toouse](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4517d-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="4517d-196">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="4517d-196">Create a file share</span></span>
<span data-ttu-id="4517d-197">Una condivisione di archiviazione file è una condivisione file SMB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="4517d-198">Tutte le directory e i file devono essere creati in una condivisione padre.</span><span class="sxs-lookup"><span data-stu-id="4517d-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="4517d-199">Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, i limiti di capacità toohello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4517d-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="4517d-200">esempio Hello crea una condivisione file denominata **myshare**.</span><span class="sxs-lookup"><span data-stu-id="4517d-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="4517d-201">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="4517d-201">Create a directory</span></span>
<span data-ttu-id="4517d-202">Una directory fornisce una struttura gerarchica facoltativa per una condivisione di file di Azure.</span><span class="sxs-lookup"><span data-stu-id="4517d-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="4517d-203">esempio Hello crea una directory denominata **myDir** nella condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="4517d-204">Si noti che tale percorso di directory può includere più livelli, *ad esempio*, **un / b**.</span><span class="sxs-lookup"><span data-stu-id="4517d-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="4517d-205">Tuttavia è necessario assicurarsi che tutte le directory padre esistano.</span><span class="sxs-lookup"><span data-stu-id="4517d-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="4517d-206">Ad esempio, per il percorso **a/b**, è necessario creare prima la directory **a** e poi la directory **b**.</span><span class="sxs-lookup"><span data-stu-id="4517d-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="4517d-207">Caricare un file locale di toodirectory</span><span class="sxs-lookup"><span data-stu-id="4517d-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="4517d-208">esempio Hello carica un file da **~/temp/samplefile.txt** toohello **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="4517d-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="4517d-209">Modificare il percorso del file hello in modo che punti tooa file valido sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="4517d-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="4517d-210">Si noti che può essere un file nella condivisione di hello backup too1 TB nella dimensione.</span><span class="sxs-lookup"><span data-stu-id="4517d-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="4517d-211">Elencare i file hello nella radice di hello condivisione o directory</span><span class="sxs-lookup"><span data-stu-id="4517d-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="4517d-212">È possibile elencare i file hello e le sottodirectory in una radice di condivisione o una directory tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4517d-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="4517d-213">Si noti che il nome directory hello sia facoltativo per l'operazione di elenco hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="4517d-214">Se omesso, il comando hello Elenca il contenuto di hello della directory radice hello della condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="4517d-215">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="4517d-215">Copy files</span></span>
<span data-ttu-id="4517d-216">A partire dalla versione 0.9.8 di CLI di Azure, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa.</span><span class="sxs-lookup"><span data-stu-id="4517d-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="4517d-217">Di seguito viene illustrato come questi tooperform copiare operazioni utilizzando i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="4517d-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="4517d-218">toocopy una nuova directory toohello di file:</span><span class="sxs-lookup"><span data-stu-id="4517d-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="4517d-219">una directory del file blob tooa toocopy:</span><span class="sxs-lookup"><span data-stu-id="4517d-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="4517d-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4517d-220">Next Steps</span></span>

<span data-ttu-id="4517d-221">È possibile trovare riferimenti ai comandi dell'interfaccia della riga di comando 1.0 di Azure da usare con le risorse di Archiviazione qui:</span><span class="sxs-lookup"><span data-stu-id="4517d-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="4517d-222">Comandi dell'interfaccia della riga di comando Azure in modalità Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4517d-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="4517d-223">Comandi dell'interfaccia della riga di comando di Azure in modalità Gestione servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="4517d-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="4517d-224">Anche desiderato hello tootry [CLI di Azure 2.0](storage-azure-cli.md), la CLI di prossima generazione scritti in Python, per l'utilizzo con modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="4517d-224">You may also like tootry hello [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
