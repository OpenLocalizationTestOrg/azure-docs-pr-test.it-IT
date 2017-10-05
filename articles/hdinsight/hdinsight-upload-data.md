---
title: Caricare dati per processi Hadoop in HDInsight | Documentazione Microsoft
description: Informazioni su come caricare i dati per processi Hadoop e accedervi in HDInsight con Interfaccia della riga di comando di Azure, Azure Storage Explorer, Azure PowerShell, la riga di comando di Hadoop o Sqoop.
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="d1390-104">Caricare dati per processi Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1390-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="d1390-105">Azure HDInsight include un'interfaccia completa per il file system HDFS (Hadoop Distributed File System) sull'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="d1390-106">Tale interfaccia è stata progettata come estensione HDFS per offrire un'esperienza lineare ai clienti</span><span class="sxs-lookup"><span data-stu-id="d1390-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="d1390-107">tramite l'abilitazione del set completo di componenti nell'ecosistema Hadoop, con possibilità di agire direttamente sui dati gestiti da Hadoop stesso.</span><span class="sxs-lookup"><span data-stu-id="d1390-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="d1390-108">L'archivio BLOB di Azure e HDFS sono file system distinti, ottimizzati per l'archiviazione di dati e per l'esecuzione di calcoli su di essi.</span><span class="sxs-lookup"><span data-stu-id="d1390-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="d1390-109">Per i vantaggi dell'uso dell'archivio BLOB di Azure, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d1390-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d1390-110">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="d1390-110">**Prerequisites**</span></span>

<span data-ttu-id="d1390-111">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="d1390-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="d1390-112">Disporre di un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="d1390-113">Per istruzioni, vedere [Introduzione ad Azure HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster Hadoop in HDInsight con opzioni personalizzate][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d1390-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="d1390-114">Informazioni sull'archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="d1390-114">Why blob storage?</span></span>
<span data-ttu-id="d1390-115">In genere i cluster HDInsight di Azure vengono distribuiti per l'esecuzione di processi MapReduce e rimossi dopo il completamento di questi ultimi.</span><span class="sxs-lookup"><span data-stu-id="d1390-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="d1390-116">Mantenere i dati nei cluster HDFS dopo il completamento dei calcoli rappresenterebbe una soluzione di archiviazione dei dati molto costosa.</span><span class="sxs-lookup"><span data-stu-id="d1390-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="d1390-117">L'archivio BLOB di Azure offre un'opzione di archiviazione con caratteristiche di scalabilità e capacità elevata, a basso costo e condivisibile per i dati che devono essere elaborati mediante HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1390-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="d1390-118">L'archiviazione dei dati in un BLOB consente l'eliminazione sicura dei cluster HDInsight usati per i calcoli, senza perdita di dati utente.</span><span class="sxs-lookup"><span data-stu-id="d1390-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="d1390-119">Directory</span><span class="sxs-lookup"><span data-stu-id="d1390-119">Directories</span></span>
<span data-ttu-id="d1390-120">I contenitori di archiviazione BLOB archiviano i dati come coppie chiave-valore e non esiste una gerarchia di directory.</span><span class="sxs-lookup"><span data-stu-id="d1390-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="d1390-121">È tuttavia possibile usare il carattere "/" all'interno del nome della chiave, in modo che un file sembri archiviato in una struttura di directory.</span><span class="sxs-lookup"><span data-stu-id="d1390-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="d1390-122">HDInsight le rileva come directory effettive.</span><span class="sxs-lookup"><span data-stu-id="d1390-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="d1390-123">Ad esempio, la chiave di un BLOB potrebbe essere *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="d1390-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="d1390-124">Non esiste realmente una directory "input" ma, grazie alla presenza del carattere "/", il nome della chiave ha l'aspetto di un percorso di file.</span><span class="sxs-lookup"><span data-stu-id="d1390-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="d1390-125">Per questo motivo, se si usano gli strumenti di esplorazione di Azure, è possibile notare la presenza di file da 0 byte.</span><span class="sxs-lookup"><span data-stu-id="d1390-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="d1390-126">Questi file servono a due scopi:</span><span class="sxs-lookup"><span data-stu-id="d1390-126">These files serve two purposes:</span></span>

* <span data-ttu-id="d1390-127">In caso di cartelle vuote, fungono da indicatore dell'esistenza della cartella.</span><span class="sxs-lookup"><span data-stu-id="d1390-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="d1390-128">L'archivio BLOB è in grado di comprendere che, se esiste un BLOB denominato foo/bar, esiste una cartella denominata **foo**.</span><span class="sxs-lookup"><span data-stu-id="d1390-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="d1390-129">La presenza di una cartella vuota denominata **foo** , tuttavia, è indicata esclusivamente da questo speciale file da 0 byte.</span><span class="sxs-lookup"><span data-stu-id="d1390-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="d1390-130">Questi file contengono metadati speciali, in particolare relativi alle autorizzazioni e ai proprietari delle cartelle, necessari per il file system Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1390-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="d1390-131">Utilità della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d1390-131">Command-line utilities</span></span>
<span data-ttu-id="d1390-132">Microsoft fornisce le utilità seguenti da usare con l'archivio BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="d1390-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="d1390-133">Strumento</span><span class="sxs-lookup"><span data-stu-id="d1390-133">Tool</span></span> | <span data-ttu-id="d1390-134">Linux</span><span class="sxs-lookup"><span data-stu-id="d1390-134">Linux</span></span> | <span data-ttu-id="d1390-135">OS X</span><span class="sxs-lookup"><span data-stu-id="d1390-135">OS X</span></span> | <span data-ttu-id="d1390-136">Windows</span><span class="sxs-lookup"><span data-stu-id="d1390-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="d1390-137">[Interfaccia della riga di comando di Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="d1390-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="d1390-138">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-138">✔</span></span> |<span data-ttu-id="d1390-139">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-139">✔</span></span> |<span data-ttu-id="d1390-140">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-140">✔</span></span> |
| <span data-ttu-id="d1390-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="d1390-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="d1390-142">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-142">✔</span></span> |
| <span data-ttu-id="d1390-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="d1390-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="d1390-144">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-144">✔</span></span> |
| [<span data-ttu-id="d1390-145">Comando Hadoop</span><span class="sxs-lookup"><span data-stu-id="d1390-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="d1390-146">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-146">✔</span></span> |<span data-ttu-id="d1390-147">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-147">✔</span></span> |<span data-ttu-id="d1390-148">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="d1390-149">Mentre l'interfaccia della riga di comando di Azure, Azure PowerShell e AzCopy possono tutti essere usati all'esterno di Azure, il comando Hadoop è disponibile solo nei cluster HDInsight e consente solo il caricamento dei dati dal file system locale nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="d1390-150"><a id="xplatcli"></a></span><span class="sxs-lookup"><span data-stu-id="d1390-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="d1390-151">L'interfaccia della riga di comando di Azure è uno strumento multipiattaforma che consente di gestire i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="d1390-152">Per caricare dati nell'archivio BLOB di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d1390-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="d1390-153">[Installare e configurare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d1390-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="d1390-154">Aprire un prompt dei comandi, una sessione Bash o un'altra shell e usare quanto riportato di seguito per eseguire l'autenticazione alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="d1390-155">Quando richiesto, immettere il nome utente e la password per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d1390-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="d1390-156">Immettere il comando seguente per elencare gli account di archiviazione per la sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="d1390-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="d1390-157">Selezionare l'account di archiviazione contenente il BLOB che si desidera usare, quindi usare il comando seguente per recuperare la chiave per tale account:</span><span class="sxs-lookup"><span data-stu-id="d1390-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="d1390-158">Il comando dovrebbe restituire le chiavi **Primary** e **Secondary**.</span><span class="sxs-lookup"><span data-stu-id="d1390-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="d1390-159">Copiare il valore della chiave **Primary** poiché varrà usato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="d1390-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="d1390-160">Usare il comando seguente per recuperare un elenco di contenitori BLOB all'interno dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="d1390-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="d1390-161">Per caricare e scaricare i file dal BLOB, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1390-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="d1390-162">Per caricare un file:</span><span class="sxs-lookup"><span data-stu-id="d1390-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="d1390-163">Per scaricare un file:</span><span class="sxs-lookup"><span data-stu-id="d1390-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="d1390-164">Se si userà sempre lo stesso account di archiviazione, anziché specificare l'account e la chiave per ogni comando è possibile impostare le variabili di ambiente seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1390-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="d1390-165">**AZURE\_STORAGE\_ACCOUNT**: nome dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d1390-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="d1390-166">**AZURE\_STORAGE\_ACCESS\_KEY**: chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d1390-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="d1390-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1390-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="d1390-168">Azure PowerShell è un ambiente di scripting che può essere usato per controllare e automatizzare la distribuzione e la gestione dei carichi di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="d1390-169">Per informazioni sulla configurazione della workstation per l'esecuzione di Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1390-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="d1390-170">**Per caricare un file locale nell'archivio BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="d1390-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="d1390-171">Aprire la console di Azure PowerShell come illustrato in [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1390-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="d1390-172">Impostare i valori delle prime cinque variabili nello script seguente:</span><span class="sxs-lookup"><span data-stu-id="d1390-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="d1390-173">Incollare lo script nella console di Azure PowerShell per eseguirlo e copiare il file.</span><span class="sxs-lookup"><span data-stu-id="d1390-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="d1390-174">Per script di PowerShell di esempio creati per funzionare con HDInsight, vedere [Strumenti HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="d1390-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="d1390-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="d1390-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="d1390-176">AzCopy è un strumento della riga di comando progettato per semplificare l'attività di trasferimento dati in entrata e in uscita da un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="d1390-177">Può essere usato come strumento autonomo o può essere incorporato in un'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="d1390-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="d1390-178">[Download di AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="d1390-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="d1390-179">La sintassi di AzCopy è:</span><span class="sxs-lookup"><span data-stu-id="d1390-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="d1390-180">Per altre informazioni, vedere [AzCopy: caricamento/download di file per BLOB di Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="d1390-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="d1390-181"><a id="commandline"></a>Riga di comando di Hadoop</span><span class="sxs-lookup"><span data-stu-id="d1390-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="d1390-182">La riga di comando di Hadoop è utile solo per archiviare i dati nell'archivio BLOB quando i dati sono già presenti nel nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="d1390-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="d1390-183">Per usare il comando Hadoop, è innanzitutto necessario connettersi nel nodo head mediante uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1390-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="d1390-184">**HDInsight basato su Windows**: [connettersi tramite Desktop remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="d1390-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="d1390-185">**HDInsight basato su Linux**: connettersi tramite SSH ([comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) r [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="d1390-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="d1390-186">Dopo essersi connessi, è possibile usare la sintassi seguente per caricare un file nell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d1390-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="d1390-187">Ad esempio, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="d1390-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="d1390-188">Poiché il file system predefinito per HDInsight si trova nell'archivio BLOB di Azure, /example/datadavinci.txt si trova in effetti nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="d1390-189">È inoltre possibile fare riferimento al file come segue:</span><span class="sxs-lookup"><span data-stu-id="d1390-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="d1390-190">oppure</span><span class="sxs-lookup"><span data-stu-id="d1390-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="d1390-191">Per un elenco di altri comandi Hadoop che funzionano con i file, vedere [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="d1390-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="d1390-192">Nei cluster HBase la dimensione di blocco predefinita usata per la scrittura dei dati è 256 KB.</span><span class="sxs-lookup"><span data-stu-id="d1390-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="d1390-193">Questa impostazione non costituisce un problema quando si usano API HBase o API REST, ma l'uso dei comandi `hadoop` o `hdfs dfs` per scrivere dati di dimensioni superiori a ~12 GB provoca un errore.</span><span class="sxs-lookup"><span data-stu-id="d1390-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="d1390-194">Per altre informazioni, vedere la sezione [Eccezione di archiviazione per la scrittura nel BLOB](#storageexception) più avanti.</span><span class="sxs-lookup"><span data-stu-id="d1390-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="d1390-195">Client con interfaccia grafica</span><span class="sxs-lookup"><span data-stu-id="d1390-195">Graphical clients</span></span>
<span data-ttu-id="d1390-196">Esistono diverse applicazioni che forniscono un'interfaccia grafica per usare Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="d1390-197">Di seguito è riportato un elenco di alcune di queste applicazioni:</span><span class="sxs-lookup"><span data-stu-id="d1390-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="d1390-198">Client</span><span class="sxs-lookup"><span data-stu-id="d1390-198">Client</span></span> | <span data-ttu-id="d1390-199">Linux</span><span class="sxs-lookup"><span data-stu-id="d1390-199">Linux</span></span> | <span data-ttu-id="d1390-200">OS X</span><span class="sxs-lookup"><span data-stu-id="d1390-200">OS X</span></span> | <span data-ttu-id="d1390-201">Windows</span><span class="sxs-lookup"><span data-stu-id="d1390-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="d1390-202">Microsoft Visual Studio Tools per HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1390-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="d1390-203">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-203">✔</span></span> |<span data-ttu-id="d1390-204">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-204">✔</span></span> |<span data-ttu-id="d1390-205">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-205">✔</span></span> |
| [<span data-ttu-id="d1390-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="d1390-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="d1390-207">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-207">✔</span></span> |<span data-ttu-id="d1390-208">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-208">✔</span></span> |<span data-ttu-id="d1390-209">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-209">✔</span></span> |
| [<span data-ttu-id="d1390-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="d1390-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="d1390-211">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-211">✔</span></span> |
| [<span data-ttu-id="d1390-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="d1390-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="d1390-213">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-213">✔</span></span> |
| [<span data-ttu-id="d1390-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="d1390-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="d1390-215">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-215">✔</span></span> |
| [<span data-ttu-id="d1390-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="d1390-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="d1390-217">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-217">✔</span></span> |<span data-ttu-id="d1390-218">✔</span><span class="sxs-lookup"><span data-stu-id="d1390-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="d1390-219">Visual Studio Tools per HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1390-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="d1390-220">Per altre informazioni, vedere [Esplorare le risorse collegate](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="d1390-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="d1390-221"><a id="storageexplorer"></a>Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="d1390-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="d1390-222">*Azure Storage Explorer* è uno strumento utile per l'esame e la modifica dei dati nei BLOB.</span><span class="sxs-lookup"><span data-stu-id="d1390-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="d1390-223">Si tratta di uno strumento gratuito open-source che è possibile scaricare da [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d1390-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="d1390-224">Anche il codice sorgente è disponibile da questo collegamento.</span><span class="sxs-lookup"><span data-stu-id="d1390-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="d1390-225">Prima di usare lo strumento è necessario conoscere il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="d1390-226">Per istruzioni sull'acquisizione di queste informazioni, vedere la sezione "Procedura: Visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione" dell'articolo [Creare, gestire o eliminare un account di archiviazione][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="d1390-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="d1390-227">Eseguire Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="d1390-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="d1390-228">Se è la prima volta che si esegue Storage Explorer, sarà necessario specificare il **nome account di archiviazione** e la **chiave account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="d1390-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="d1390-229">Se questo strumento è stato eseguito prima, usare il pulsante **Aggiungi** per aggiungere un nuovo nome e una nuova chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d1390-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="d1390-230">Immettere il nome e la chiave dell'account di archiviazione usati dal cluster HDInsight e quindi selezionare **SALVA E APRI**.</span><span class="sxs-lookup"><span data-stu-id="d1390-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="d1390-232">Nell'elenco dei contenitori a sinistra dell'interfaccia, fare clic sul nome del contenitore associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1390-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="d1390-233">Per impostazione predefinita, questo è il nome del cluster HDInsight, ma potrebbe essere diverso se è stato immesso un nome specifico durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d1390-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="d1390-234">Sulla barra degli strumenti, selezionare l'icona di caricamento.</span><span class="sxs-lookup"><span data-stu-id="d1390-234">From the tool bar, select the upload icon.</span></span>

    ![Barra degli strumenti con icona di caricamento evidenziata](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="d1390-236">Specificare un file da caricare e quindi fare clic su **Open**.</span><span class="sxs-lookup"><span data-stu-id="d1390-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="d1390-237">Quando richiesto, selezionare **Carica** per caricare il file nella directory principale del contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d1390-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="d1390-238">Se si vuole caricare il file in un percorso specifico, immettere il percorso nel campo **Destinazione**, quindi selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="d1390-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Finestra di dialogo di caricamento file](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="d1390-240">Dopo che il file ha terminato il caricamento, è possibile utilizzarlo dai processi nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1390-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="d1390-241">Montare l'archiviazione BLOB di Azure come unità locale</span><span class="sxs-lookup"><span data-stu-id="d1390-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="d1390-242">Vedere [Montaggio dell’archiviazione BLOB di Azure come unità locale](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1390-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="d1390-243">Servizi</span><span class="sxs-lookup"><span data-stu-id="d1390-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="d1390-244">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="d1390-244">Azure Data Factory</span></span>
<span data-ttu-id="d1390-245">Data factory di Azure è un servizio completamente gestito per la composizione di servizi di archiviazione, elaborazione e spostamento dei dati in pipeline di produzione dei dati ottimizzate, scalabili e affidabili.</span><span class="sxs-lookup"><span data-stu-id="d1390-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="d1390-246">Data factory di Azure può essere usato per spostare i dati nell'archivio BLOB di Azure o per creare pipeline di dati che usano direttamente le funzionalità di HDInsight, ad esempio Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="d1390-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="d1390-247">Per altre informazioni, vedere [Documentazione di Data factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="d1390-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="d1390-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="d1390-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="d1390-249">Sqoop è uno strumento progettato per il trasferimento di dati tra Hadoop e i database relazionali.</span><span class="sxs-lookup"><span data-stu-id="d1390-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="d1390-250">Può essere usato per importare dati in HDFS (Hadoop Distributed File System) da un sistema di gestione di database relazionali (RDBMS), ad esempio SQL, MySQL oppure Oracle, trasformare i dati in Hadoop con MapReduce o Hive e quindi esportarli nuovamente in un sistema RDBMS.</span><span class="sxs-lookup"><span data-stu-id="d1390-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="d1390-251">Per altre informazioni, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="d1390-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="d1390-252">SDK di sviluppo</span><span class="sxs-lookup"><span data-stu-id="d1390-252">Development SDKs</span></span>
<span data-ttu-id="d1390-253">È possibile accedere all'archivio BLOB di Azure anche tramite un SDK di Azure dai linguaggi di programmazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1390-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="d1390-254">.NET</span><span class="sxs-lookup"><span data-stu-id="d1390-254">.NET</span></span>
* <span data-ttu-id="d1390-255">Java</span><span class="sxs-lookup"><span data-stu-id="d1390-255">Java</span></span>
* <span data-ttu-id="d1390-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="d1390-256">Node.js</span></span>
* <span data-ttu-id="d1390-257">PHP</span><span class="sxs-lookup"><span data-stu-id="d1390-257">PHP</span></span>
* <span data-ttu-id="d1390-258">Python</span><span class="sxs-lookup"><span data-stu-id="d1390-258">Python</span></span>
* <span data-ttu-id="d1390-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="d1390-259">Ruby</span></span>

<span data-ttu-id="d1390-260">Per altre informazioni sull'installazione di SDK di Azure, vedere [Download di Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d1390-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d1390-261">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d1390-261">Troubleshooting</span></span>
### <span data-ttu-id="d1390-262"><a id="storageexception"></a>Eccezione di archiviazione per la scrittura nel BLOB</span><span class="sxs-lookup"><span data-stu-id="d1390-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="d1390-263">**Sintomi**: quando si usa il comando `hadoop` o `hdfs dfs` per scrivere file di dimensioni pari o superiori a ~12 GB in un cluster HBase, è possibile che si verifichi l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="d1390-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="d1390-264">**Causa**: i cluster HBase in HDInsight usano per impostazione predefinita dimensioni di blocco pari a 256 KB per la scrittura nelle risorse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1390-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="d1390-265">Benché questa impostazione sia ottimale per le API HBase o le API REST, provocherà un errore se si usano le utilità da riga di comando `hadoop` o `hdfs dfs`.</span><span class="sxs-lookup"><span data-stu-id="d1390-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="d1390-266">**Risoluzione**: usare `fs.azure.write.request.size` per specificare dimensioni maggiori per i blocchi.</span><span class="sxs-lookup"><span data-stu-id="d1390-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="d1390-267">È possibile eseguire questa operazione per i singoli utenti usando il parametro `-D`.</span><span class="sxs-lookup"><span data-stu-id="d1390-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="d1390-268">L'esempio seguente usa questo parametro con il comando `hadoop`:</span><span class="sxs-lookup"><span data-stu-id="d1390-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="d1390-269">È anche possibile aumentare globalmente il valore di `fs.azure.write.request.size` usando Ambari.</span><span class="sxs-lookup"><span data-stu-id="d1390-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="d1390-270">La procedura seguente consente di cambiare il valore nell'interfaccia utente Web di Ambari:</span><span class="sxs-lookup"><span data-stu-id="d1390-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="d1390-271">Nel browser passare all'interfaccia utente Web di Ambari per il cluster,</span><span class="sxs-lookup"><span data-stu-id="d1390-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="d1390-272">ovvero https://CLUSTERNAME.azurehdinsight.net, dove **CLUSTERNAME** è il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="d1390-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="d1390-273">Quando richiesto, immettere il nome dell'amministratore e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d1390-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="d1390-274">Sul lato sinistro dello schermo selezionale **HDFS** e quindi fare clic sulla scheda **Configs** (Configurazioni).</span><span class="sxs-lookup"><span data-stu-id="d1390-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="d1390-275">Nel campo **Filter** (Filtro) immettere `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="d1390-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="d1390-276">Il campo e il valore corrente verranno visualizzati al centro della pagina.</span><span class="sxs-lookup"><span data-stu-id="d1390-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="d1390-277">Modificare il valore da 262144 (256 KB) al nuovo valore,</span><span class="sxs-lookup"><span data-stu-id="d1390-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="d1390-278">ad esempio 4194304 (4 MB).</span><span class="sxs-lookup"><span data-stu-id="d1390-278">For example, 4194304 (4MB).</span></span>

![Immagine della modifica del valore tramite l'interfaccia utente Web di Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="d1390-280">Per altre informazioni sull'uso di Ambari, vedere [Gestire i cluster HDInsight mediante l'utilizzo dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="d1390-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1390-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1390-281">Next steps</span></span>
<span data-ttu-id="d1390-282">Dopo aver appreso come importare dati in HDInsight, leggere gli articoli seguenti per informazioni sull'esecuzione di analisi:</span><span class="sxs-lookup"><span data-stu-id="d1390-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="d1390-283">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d1390-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d1390-284">[Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="d1390-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="d1390-285">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d1390-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d1390-286">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d1390-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
