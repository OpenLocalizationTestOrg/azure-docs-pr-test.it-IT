---
title: dati aaaUpload per i processi di Hadoop in HDInsight | Documenti Microsoft
description: Informazioni su come tooupload e accedere ai dati per i processi di Hadoop in HDInsight mediante hello CLI di Azure, Azure Storage Explorer, Azure PowerShell, riga di comando hello Hadoop o Sqoop.
keywords: hadoop etl, recupero dati in hadoop, caricare dati in hadoop
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="48205-104">Caricare dati per processi Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="48205-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="48205-105">Azure HDInsight include un'interfaccia completa per il file system HDFS (Hadoop Distributed File System) sull'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="48205-106">È progettato come un'estensione HDFS per tooprovide una perfetta riscontrare toocustomers.</span><span class="sxs-lookup"><span data-stu-id="48205-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="48205-107">Abilita set completo di hello dei componenti in hello Hadoop ecosistema toooperate direttamente sui dati di hello che gestisce.</span><span class="sxs-lookup"><span data-stu-id="48205-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="48205-108">L'archivio BLOB di Azure e HDFS sono file system distinti, ottimizzati per l'archiviazione di dati e per l'esecuzione di calcoli su di essi.</span><span class="sxs-lookup"><span data-stu-id="48205-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="48205-109">Per informazioni sui vantaggi di hello di utilizzo dell'archiviazione Blob di Azure, vedere [archiviazione Blob di Azure usare con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="48205-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="48205-110">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="48205-110">**Prerequisites**</span></span>

<span data-ttu-id="48205-111">Si noti hello seguente requisito prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="48205-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="48205-112">Disporre di un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="48205-113">Per istruzioni, vedere [Introduzione ad Azure HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster Hadoop in HDInsight con opzioni personalizzate][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="48205-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="48205-114">Informazioni sull'archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="48205-114">Why blob storage?</span></span>
<span data-ttu-id="48205-115">Azure HDInsight cluster sono in genere distribuiti i processi MapReduce toorun e cluster hello vengono eliminati dopo il completamento di tali processi.</span><span class="sxs-lookup"><span data-stu-id="48205-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="48205-116">Conservazione dei dati hello nel cluster HDFS hello al termine di calcoli sarebbe un toostore costoso questi dati.</span><span class="sxs-lookup"><span data-stu-id="48205-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="48205-117">Archiviazione Blob di Azure è un'elevata disponibilità, estremamente scalabile e ad alta capacità, l'opzione di archiviazione basso costo e condivisibile per i dati che viene elaborato tramite HDInsight toobe.</span><span class="sxs-lookup"><span data-stu-id="48205-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="48205-118">L'archiviazione dei dati in un blob consente cluster HDInsight hello che vengono utilizzati per toobe calcolo rilasciato in modo sicuro senza perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="48205-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="48205-119">Directory</span><span class="sxs-lookup"><span data-stu-id="48205-119">Directories</span></span>
<span data-ttu-id="48205-120">I contenitori di archiviazione BLOB archiviano i dati come coppie chiave-valore e non esiste una gerarchia di directory.</span><span class="sxs-lookup"><span data-stu-id="48205-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="48205-121">Tuttavia hello "/" carattere può essere utilizzato all'interno di hello nome della chiave toomake appare come se un file viene archiviato in una struttura di directory.</span><span class="sxs-lookup"><span data-stu-id="48205-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="48205-122">HDInsight le rileva come directory effettive.</span><span class="sxs-lookup"><span data-stu-id="48205-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="48205-123">Ad esempio, la chiave di un BLOB potrebbe essere *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="48205-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="48205-124">Nessuna directory "input" effettiva esiste, ma a causa di presenza di toohello di hello carattere "/" nel nome della chiave hello sia aspetto hello di un percorso di file.</span><span class="sxs-lookup"><span data-stu-id="48205-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="48205-125">Per questo motivo, se si usano gli strumenti di esplorazione di Azure, è possibile notare la presenza di file da 0 byte.</span><span class="sxs-lookup"><span data-stu-id="48205-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="48205-126">Questi file servono a due scopi:</span><span class="sxs-lookup"><span data-stu-id="48205-126">These files serve two purposes:</span></span>

* <span data-ttu-id="48205-127">Se sono presenti le cartelle vuote, contrassegnate dell'esistenza di hello della cartella hello.</span><span class="sxs-lookup"><span data-stu-id="48205-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="48205-128">Archiviazione Blob di Azure è sufficientemente appositamente tooknow che se esiste un blob denominato foo/barra, vi sia una cartella denominata **foo**.</span><span class="sxs-lookup"><span data-stu-id="48205-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="48205-129">Ma solo toosignify modo una cartella vuota denominata hello **foo** consiste nel disporre di questo file speciale 0 byte sul posto.</span><span class="sxs-lookup"><span data-stu-id="48205-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="48205-130">Contengono metadati speciale che sono necessario per hello Hadoop file system, in particolare le autorizzazioni di hello e proprietari per le cartelle di hello.</span><span class="sxs-lookup"><span data-stu-id="48205-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="48205-131">Utilità della riga di comando</span><span class="sxs-lookup"><span data-stu-id="48205-131">Command-line utilities</span></span>
<span data-ttu-id="48205-132">Microsoft fornisce hello seguente utilità toowork con archiviazione Blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="48205-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="48205-133">Strumento</span><span class="sxs-lookup"><span data-stu-id="48205-133">Tool</span></span> | <span data-ttu-id="48205-134">Linux</span><span class="sxs-lookup"><span data-stu-id="48205-134">Linux</span></span> | <span data-ttu-id="48205-135">OS X</span><span class="sxs-lookup"><span data-stu-id="48205-135">OS X</span></span> | <span data-ttu-id="48205-136">Windows</span><span class="sxs-lookup"><span data-stu-id="48205-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="48205-137">[Interfaccia della riga di comando di Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="48205-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="48205-138">✔</span><span class="sxs-lookup"><span data-stu-id="48205-138">✔</span></span> |<span data-ttu-id="48205-139">✔</span><span class="sxs-lookup"><span data-stu-id="48205-139">✔</span></span> |<span data-ttu-id="48205-140">✔</span><span class="sxs-lookup"><span data-stu-id="48205-140">✔</span></span> |
| <span data-ttu-id="48205-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="48205-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="48205-142">✔</span><span class="sxs-lookup"><span data-stu-id="48205-142">✔</span></span> |
| <span data-ttu-id="48205-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="48205-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="48205-144">✔</span><span class="sxs-lookup"><span data-stu-id="48205-144">✔</span></span> |
| [<span data-ttu-id="48205-145">Comando Hadoop</span><span class="sxs-lookup"><span data-stu-id="48205-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="48205-146">✔</span><span class="sxs-lookup"><span data-stu-id="48205-146">✔</span></span> |<span data-ttu-id="48205-147">✔</span><span class="sxs-lookup"><span data-stu-id="48205-147">✔</span></span> |<span data-ttu-id="48205-148">✔</span><span class="sxs-lookup"><span data-stu-id="48205-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="48205-149">Mentre hello CLI di Azure, Azure PowerShell e AzCopy possono tutti essere usato da all'esterno di Azure, hello Hadoop comando è disponibile solo in cluster di HDInsight hello e consente solo il caricamento dei dati da hello file system locale nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="48205-150"><a id="xplatcli"></a></span><span class="sxs-lookup"><span data-stu-id="48205-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="48205-151">Hello CLI di Azure è uno strumento multipiattaforma consente toomanage Azure servizi.</span><span class="sxs-lookup"><span data-stu-id="48205-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="48205-152">Utilizzare hello archiviazione di Blob tooAzure dati tooupload i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="48205-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="48205-153">[Installare e configurare hello CLI di Azure per Mac, Linux e Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="48205-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="48205-154">Aprire un prompt dei comandi, bash o altre shell, utilizzare hello seguente tooauthenticate tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="48205-155">Quando richiesto, immettere nome utente hello e una password per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="48205-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="48205-156">Immettere hello comando toolist hello gli account di archiviazione per la sottoscrizione seguente:</span><span class="sxs-lookup"><span data-stu-id="48205-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="48205-157">Selezionare l'account di archiviazione hello che contiene il blob hello desiderato toowork con, quindi utilizzare hello chiave hello tooretrieve di comando per l'account di seguito:</span><span class="sxs-lookup"><span data-stu-id="48205-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="48205-158">Il comando dovrebbe restituire le chiavi **Primary** e **Secondary**.</span><span class="sxs-lookup"><span data-stu-id="48205-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="48205-159">Hello copia **primario** valore della chiave poiché verrà utilizzato in passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="48205-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="48205-160">Utilizzare hello comando tooretrieve un elenco di contenitori di blob nell'account di archiviazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="48205-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="48205-161">Utilizzare hello tooupload i comandi seguenti e scaricare file toohello blob:</span><span class="sxs-lookup"><span data-stu-id="48205-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="48205-162">tooupload un file:</span><span class="sxs-lookup"><span data-stu-id="48205-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="48205-163">toodownload un file:</span><span class="sxs-lookup"><span data-stu-id="48205-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="48205-164">Se è sempre possibile lavorare con hello stesso account di archiviazione, è possibile impostare hello seguenti variabili di ambiente invece di specificare account hello e la chiave per ogni comando:</span><span class="sxs-lookup"><span data-stu-id="48205-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="48205-165">**AZURE\_archiviazione\_ACCOUNT**: nome account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="48205-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="48205-166">**AZURE\_archiviazione\_accesso\_chiave**: chiave account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="48205-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="48205-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48205-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="48205-168">Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="48205-169">Per informazioni sulla configurazione del toorun workstation Azure PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48205-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="48205-170">**tooupload tooAzure un file locale nell'archiviazione Blob**</span><span class="sxs-lookup"><span data-stu-id="48205-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="48205-171">Console di Azure PowerShell hello aperta come descritto in [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48205-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="48205-172">Impostare i valori hello di hello primi cinque variabili nel hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="48205-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="48205-173">Hello Incolla in hello Azure PowerShell console toorun è toocopy hello file script.</span><span class="sxs-lookup"><span data-stu-id="48205-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="48205-174">Ad esempio PowerShell script creati toowork con HDInsight, vedere [strumenti HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="48205-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="48205-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="48205-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="48205-176">AzCopy è uno strumento da riga di comando progettata attività hello toosimplify di trasferimento dei dati in e da un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="48205-177">Può essere usato come strumento autonomo o può essere incorporato in un'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="48205-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="48205-178">[Download di AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="48205-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="48205-179">sintassi di AzCopy Hello è:</span><span class="sxs-lookup"><span data-stu-id="48205-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="48205-180">Per altre informazioni, vedere [AzCopy: caricamento/download di file per BLOB di Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="48205-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="48205-181"><a id="commandline"></a>Riga di comando di Hadoop</span><span class="sxs-lookup"><span data-stu-id="48205-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="48205-182">riga di comando Hadoop Hello è utile solo per l'archiviazione dei dati nell'archiviazione blob quando i dati di hello sono già presenti nel nodo head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="48205-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="48205-183">Hello toouse ordine comando Hadoop, è innanzitutto necessario connettere il nodo head toohello utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="48205-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="48205-184">**HDInsight basato su Windows**: [connettersi tramite Desktop remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="48205-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="48205-185">**HDInsight basati su Linux**: connettersi tramite SSH ([hello comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) o [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="48205-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="48205-186">Una volta connessi, è possibile utilizzare hello seguente tooupload sintassi toostorage un file.</span><span class="sxs-lookup"><span data-stu-id="48205-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="48205-187">Ad esempio, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="48205-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="48205-188">Poiché hello predefinito file system per HDInsight nell'archiviazione Blob di Azure, /example/data.txt è effettivamente in archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="48205-189">È inoltre possibile consultare il file toohello come:</span><span class="sxs-lookup"><span data-stu-id="48205-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="48205-190">oppure</span><span class="sxs-lookup"><span data-stu-id="48205-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="48205-191">Per un elenco di altri comandi Hadoop che funzionano con i file, vedere [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="48205-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="48205-192">Nei cluster HBase, dimensione del blocco predefinita hello utilizzato durante la scrittura dei dati è di 256KB.</span><span class="sxs-lookup"><span data-stu-id="48205-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="48205-193">Mentre funziona correttamente quando si utilizza HBase APIs o le API REST, utilizzando hello `hadoop` o `hdfs dfs` dati toowrite comandi superiori a circa 12 GB genera un errore.</span><span class="sxs-lookup"><span data-stu-id="48205-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="48205-194">Vedere hello [eccezione di archiviazione per la scrittura nel blob](#storageexception) sezione riportata di seguito per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="48205-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="48205-195">Client con interfaccia grafica</span><span class="sxs-lookup"><span data-stu-id="48205-195">Graphical clients</span></span>
<span data-ttu-id="48205-196">Esistono diverse applicazioni che forniscono un'interfaccia grafica per usare Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="48205-197">Hello seguito è riportato un elenco di alcune di queste applicazioni:</span><span class="sxs-lookup"><span data-stu-id="48205-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="48205-198">Client</span><span class="sxs-lookup"><span data-stu-id="48205-198">Client</span></span> | <span data-ttu-id="48205-199">Linux</span><span class="sxs-lookup"><span data-stu-id="48205-199">Linux</span></span> | <span data-ttu-id="48205-200">OS X</span><span class="sxs-lookup"><span data-stu-id="48205-200">OS X</span></span> | <span data-ttu-id="48205-201">Windows</span><span class="sxs-lookup"><span data-stu-id="48205-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="48205-202">Microsoft Visual Studio Tools per HDInsight</span><span class="sxs-lookup"><span data-stu-id="48205-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="48205-203">✔</span><span class="sxs-lookup"><span data-stu-id="48205-203">✔</span></span> |<span data-ttu-id="48205-204">✔</span><span class="sxs-lookup"><span data-stu-id="48205-204">✔</span></span> |<span data-ttu-id="48205-205">✔</span><span class="sxs-lookup"><span data-stu-id="48205-205">✔</span></span> |
| [<span data-ttu-id="48205-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="48205-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="48205-207">✔</span><span class="sxs-lookup"><span data-stu-id="48205-207">✔</span></span> |<span data-ttu-id="48205-208">✔</span><span class="sxs-lookup"><span data-stu-id="48205-208">✔</span></span> |<span data-ttu-id="48205-209">✔</span><span class="sxs-lookup"><span data-stu-id="48205-209">✔</span></span> |
| [<span data-ttu-id="48205-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="48205-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="48205-211">✔</span><span class="sxs-lookup"><span data-stu-id="48205-211">✔</span></span> |
| [<span data-ttu-id="48205-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="48205-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="48205-213">✔</span><span class="sxs-lookup"><span data-stu-id="48205-213">✔</span></span> |
| [<span data-ttu-id="48205-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="48205-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="48205-215">✔</span><span class="sxs-lookup"><span data-stu-id="48205-215">✔</span></span> |
| [<span data-ttu-id="48205-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="48205-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="48205-217">✔</span><span class="sxs-lookup"><span data-stu-id="48205-217">✔</span></span> |<span data-ttu-id="48205-218">✔</span><span class="sxs-lookup"><span data-stu-id="48205-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="48205-219">Visual Studio Tools per HDInsight</span><span class="sxs-lookup"><span data-stu-id="48205-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="48205-220">Per ulteriori informazioni, vedere [risorse collegate Naviga hello](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="48205-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="48205-221"><a id="storageexplorer"></a>Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="48205-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="48205-222">*Azure Storage Explorer* è uno strumento utile per analizzare e modificare dati hello nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="48205-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="48205-223">Si tratta di uno strumento gratuito open-source che è possibile scaricare da [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="48205-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="48205-224">codice sorgente Hello è disponibile anche in questo collegamento.</span><span class="sxs-lookup"><span data-stu-id="48205-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="48205-225">Prima di utilizzare lo strumento di hello, è necessario conoscere la chiave account e nome dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="48205-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="48205-226">Per istruzioni su come ottenere queste informazioni, vedere hello "procedura: visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso" sezione di [creare, gestire o eliminare un account di archiviazione][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="48205-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="48205-227">Eseguire Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="48205-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="48205-228">Se è hello prima volta che è stato eseguito hello Esplora archivi, verrà richiesto di hello **nome dell'account _Storage** e **chiave account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="48205-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="48205-229">Se è stata eseguita in precedenza, utilizzare hello **Aggiungi** pulsante tooadd un nuovo nome di account di archiviazione e la chiave.</span><span class="sxs-lookup"><span data-stu-id="48205-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="48205-230">Immettere hello nome e chiave per l'account di archiviazione hello utilizzato dal cluster HDInsight e quindi seleziona **Salva e Apri**.</span><span class="sxs-lookup"><span data-stu-id="48205-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="48205-232">Nell'elenco di hello di sinistra toohello contenitori dell'interfaccia hello, fare clic sul nome hello del contenitore di hello associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="48205-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="48205-233">Per impostazione predefinita, questo è il nome di hello del cluster HDInsight hello, ma potrebbe essere diverso se è stato immesso un nome specifico durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="48205-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="48205-234">Dalla barra degli strumenti hello, selezionare l'icona del caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="48205-234">From hello tool bar, select hello upload icon.</span></span>

    ![Barra degli strumenti con icona di caricamento evidenziata](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="48205-236">Specificare un tooupload di file e quindi fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="48205-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="48205-237">Quando richiesto, selezionare **caricare** radice toohello del file hello tooupload hello del contenitore dell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="48205-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="48205-238">Se si desidera tooupload hello tooa specifico percorso, immettere il percorso di hello hello **destinazione** campo, quindi selezionare **caricare**.</span><span class="sxs-lookup"><span data-stu-id="48205-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Finestra di dialogo di caricamento file](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="48205-240">Al termine il caricamento di file hello, è possibile utilizzarlo dai processi nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="48205-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="48205-241">Montare l'archiviazione BLOB di Azure come unità locale</span><span class="sxs-lookup"><span data-stu-id="48205-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="48205-242">Vedere [Montaggio dell’archiviazione BLOB di Azure come unità locale](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="48205-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="48205-243">Servizi</span><span class="sxs-lookup"><span data-stu-id="48205-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="48205-244">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="48205-244">Azure Data Factory</span></span>
<span data-ttu-id="48205-245">Hello servizio Data Factory di Azure è un servizio completamente gestito per la composizione di servizi dello spostamento dei dati, l'elaborazione dati e archiviazione dati in una pipeline di produzione di dati semplificato, scalabile e affidabile.</span><span class="sxs-lookup"><span data-stu-id="48205-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="48205-246">Azure Data Factory può essere utilizzato toomove dati nell'archiviazione Blob di Azure o toocreate pipeline di dati che utilizzano direttamente le funzionalità di HDInsight, ad esempio Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="48205-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="48205-247">Per ulteriori informazioni, vedere hello [documentazione di Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="48205-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="48205-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="48205-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="48205-249">Sqoop è di tipo data tootransfer strumento progettato tra Hadoop e database relazionali.</span><span class="sxs-lookup"><span data-stu-id="48205-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="48205-250">È possibile utilizzarlo tooimport dati da un sistema di gestione di database relazionali (RDBMS), ad esempio SQL Server, MySQL o Oracle in hello distributed file system Hadoop (HDFS), la trasformazione dei dati di hello in Hadoop MapReduce o Hive e quindi esportare i dati hello in un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="48205-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="48205-251">Per altre informazioni, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="48205-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="48205-252">SDK di sviluppo</span><span class="sxs-lookup"><span data-stu-id="48205-252">Development SDKs</span></span>
<span data-ttu-id="48205-253">Archiviazione Blob di Azure è possibile accedere utilizzando un SDK di Azure da hello seguenti linguaggi di programmazione:</span><span class="sxs-lookup"><span data-stu-id="48205-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="48205-254">.NET</span><span class="sxs-lookup"><span data-stu-id="48205-254">.NET</span></span>
* <span data-ttu-id="48205-255">Java</span><span class="sxs-lookup"><span data-stu-id="48205-255">Java</span></span>
* <span data-ttu-id="48205-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="48205-256">Node.js</span></span>
* <span data-ttu-id="48205-257">PHP</span><span class="sxs-lookup"><span data-stu-id="48205-257">PHP</span></span>
* <span data-ttu-id="48205-258">Python</span><span class="sxs-lookup"><span data-stu-id="48205-258">Python</span></span>
* <span data-ttu-id="48205-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="48205-259">Ruby</span></span>

<span data-ttu-id="48205-260">Per ulteriori informazioni sull'installazione hello Azure SDK, vedere [download di Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="48205-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="48205-261">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="48205-261">Troubleshooting</span></span>
### <span data-ttu-id="48205-262"><a id="storageexception"></a>Eccezione di archiviazione per la scrittura nel BLOB</span><span class="sxs-lookup"><span data-stu-id="48205-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="48205-263">**Sintomi**: quando si utilizza hello `hadoop` o `hdfs dfs` comandi toowrite i file che sono ~ 12 GB o superiore in un cluster HBase, che possono verificarsi hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="48205-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="48205-264">**Causa**: HBase in HDInsight cluster dimensione del blocco predefinita tooa di 256 KB durante la scrittura di archiviazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="48205-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="48205-265">Quando questo viene utilizzato per HBase APIs o le API REST, si verificherà un errore quando si utilizza hello `hadoop` o `hdfs dfs` utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="48205-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="48205-266">**Risoluzione**: utilizzare `fs.azure.write.request.size` toospecify dimensioni maggiori del blocco.</span><span class="sxs-lookup"><span data-stu-id="48205-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="48205-267">È possibile farlo in base all'utilizzo tramite hello `-D` parametro.</span><span class="sxs-lookup"><span data-stu-id="48205-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="48205-268">Hello seguito è riportato un esempio di utilizzo di questo parametro con hello `hadoop` comando:</span><span class="sxs-lookup"><span data-stu-id="48205-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="48205-269">È inoltre possibile aumentare il valore di hello di `fs.azure.write.request.size` a livello globale tramite Ambari.</span><span class="sxs-lookup"><span data-stu-id="48205-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="48205-270">Hello procedura seguente può essere utilizzato il valore di hello toochange nell'interfaccia utente Web Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="48205-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="48205-271">Nel browser passare toohello Ambari Web UI per il cluster.</span><span class="sxs-lookup"><span data-stu-id="48205-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="48205-272">Si tratta di https://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="48205-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="48205-273">Quando richiesto, immettere il nome di amministratore hello e una password per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="48205-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="48205-274">Hello il lato sinistro di schermata ciao, selezionare **HDFS**, quindi selezionare hello **configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="48205-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="48205-275">In hello **filtro...**  immettere `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="48205-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="48205-276">Campo hello e il valore corrente verrà visualizzato al centro hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="48205-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="48205-277">Modificare il valore di hello 262144 (256KB) toohello nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="48205-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="48205-278">ad esempio 4194304 (4 MB).</span><span class="sxs-lookup"><span data-stu-id="48205-278">For example, 4194304 (4MB).</span></span>

![Immagine della modifica valore hello tramite interfaccia utente Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="48205-280">Per ulteriori informazioni sull'utilizzo Ambari, vedere [gestione dei cluster HDInsight tramite hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="48205-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48205-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48205-281">Next steps</span></span>
<span data-ttu-id="48205-282">Ora che la modalità di lettura dei dati di tooget in HDInsight, hello seguenti come articoli toolearn tooperform analisi:</span><span class="sxs-lookup"><span data-stu-id="48205-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="48205-283">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="48205-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="48205-284">[Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="48205-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="48205-285">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="48205-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="48205-286">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="48205-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
