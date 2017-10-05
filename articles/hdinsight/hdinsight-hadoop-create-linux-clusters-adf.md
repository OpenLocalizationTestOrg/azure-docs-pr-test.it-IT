---
title: Creare cluster Hadoop on demand con Data Factory - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare cluster Hadoop on demand in HDInsight con Azure Data Factory.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="b2fee-103">Creare cluster Hadoop on demand in HDInsight con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2fee-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="b2fee-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) è un servizio di integrazione delle informazioni basato sul cloud che consente di automatizzare lo spostamento e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="b2fee-105">È possibile creare un cluster Hadoop di HDInsight JIT per elaborare una sezione dati di input ed eliminare il cluster al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="b2fee-106">Ecco alcuni dei vantaggi offerti dall'uso di un cluster Hadoop di HDInsight su richiesta:</span><span class="sxs-lookup"><span data-stu-id="b2fee-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="b2fee-107">Si paga solo per il tempo in cui il processo è in esecuzione nel cluster Hadoop di HDInsight, più un breve tempo di inattività configurabile.</span><span class="sxs-lookup"><span data-stu-id="b2fee-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="b2fee-108">La fatturazione dei cluster HDInsight viene calcolata al minuto, indipendentemente dal fatto che siano in uso o meno.</span><span class="sxs-lookup"><span data-stu-id="b2fee-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="b2fee-109">Quando si usa un servizio collegato HDInsight su richiesta in Data Factory, i cluster vengono creati su richiesta.</span><span class="sxs-lookup"><span data-stu-id="b2fee-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="b2fee-110">I cluster vengono eliminati automaticamente quando i processi vengono completati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="b2fee-111">Di conseguenza, si paga solo per il tempo di esecuzione del processo e il breve tempo di inattività (impostazione timeToLive).</span><span class="sxs-lookup"><span data-stu-id="b2fee-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="b2fee-112">È possibile creare un flusso di lavoro usando una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="b2fee-113">Ad esempio, è possibile usare la pipeline per copiare dati da un'istanza locale di SQL Server a un archivio BLOB di Azure, elaborare i dati eseguendo uno script Hive e uno script Pig in un cluster Hadoop di HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="b2fee-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b2fee-114">e quindi copiare i dati dei risultati in Azure SQL Data Warehouse perché vengano utilizzati da applicazioni di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="b2fee-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="b2fee-115">È possibile pianificare l'esecuzione periodica (oraria, giornaliera, settimanale, mensile e così via) del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b2fee-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="b2fee-116">In Azure Data Factory, una data factory può includere una o più pipeline di dati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="b2fee-117">Una pipeline di dati include una o più attività.</span><span class="sxs-lookup"><span data-stu-id="b2fee-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="b2fee-118">Esistono due tipi di attività: [attività di spostamento dei dati](../data-factory/data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="b2fee-119">Le attività di spostamento dei dati (che attualmente includono solo l'attività di copia) vengono usate per spostare dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="b2fee-120">Le attività di trasformazione dei dati vengono usate per trasformare/elaborare i dati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="b2fee-121">L'attività Hive di HDInsight è una delle attività di trasformazione supportate da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="b2fee-122">L'attività di trasformazione Hive verrà usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="b2fee-123">È possibile configurare un'attività Hive in modo da usare il cluster Hadoop di HDInsight dell'utente oppure un cluster Hadoop di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="b2fee-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b2fee-124">In questa esercitazione, l'attività Hive nella pipeline della data factory viene configurata per usare un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="b2fee-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b2fee-125">Ecco quindi cosa accade quando l'attività viene eseguita per elaborare una sezione dati:</span><span class="sxs-lookup"><span data-stu-id="b2fee-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="b2fee-126">Viene creato automaticamente un cluster Hadoop di HDInsight JIT per elaborare la sezione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="b2fee-127">I dati di input vengono elaborati eseguendo uno script HiveQL nel cluster.</span><span class="sxs-lookup"><span data-stu-id="b2fee-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="b2fee-128">Il cluster Hadoop di HDInsight viene eliminato al termine dell'elaborazione ed è inattivo per l'intervallo di tempo configurato (impostazione timeToLive).</span><span class="sxs-lookup"><span data-stu-id="b2fee-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="b2fee-129">Se la sezione dati successiva è disponibile per l'elaborazione entro il tempo di inattività di timeToLive, per l'elaborazione della sezione viene usato lo stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="b2fee-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="b2fee-130">In questa esercitazione, lo script HiveQL associato all'attività Hive esegue queste azioni:</span><span class="sxs-lookup"><span data-stu-id="b2fee-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="b2fee-131">Crea una tabella esterna che fa riferimento ai dati di blog non elaborati contenuti in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="b2fee-132">Partiziona i dati non elaborati per anno e per mese.</span><span class="sxs-lookup"><span data-stu-id="b2fee-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="b2fee-133">Archivia i dati partizionati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="b2fee-134">In questa esercitazione, lo script HiveQL associato all'attività Hive crea una tabella esterna che fa riferimento ai dati di blog non elaborati contenuti nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="b2fee-135">Ecco le righe di esempio per ogni mese nel file di input.</span><span class="sxs-lookup"><span data-stu-id="b2fee-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="b2fee-136">Lo script HiveQL partiziona i dati non elaborati per anno e per mese</span><span class="sxs-lookup"><span data-stu-id="b2fee-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="b2fee-137">e crea tre cartelle di output in base all'input precedente.</span><span class="sxs-lookup"><span data-stu-id="b2fee-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="b2fee-138">Ogni cartella contiene un file con le voci di ogni mese.</span><span class="sxs-lookup"><span data-stu-id="b2fee-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="b2fee-139">Per vedere un elenco delle attività di trasformazione dei dati di Data Factory oltre alle attività Hive, vedere [Trasformazione e analisi tramite Data Factory di Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b2fee-140">Attualmente, da Azure Data Factory è possibile creare solo cluster HDInsight versione 3.2.</span><span class="sxs-lookup"><span data-stu-id="b2fee-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2fee-141">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b2fee-141">Prerequisites</span></span>
<span data-ttu-id="b2fee-142">Per poter eseguire le istruzioni descritte nell'articolo è necessario disporre dei seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b2fee-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="b2fee-143">[Sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b2fee-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b2fee-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2fee-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="b2fee-145">Preparare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b2fee-145">Prepare storage account</span></span>
<span data-ttu-id="b2fee-146">In questo scenario, è possibile usare fino a tre account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b2fee-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="b2fee-147">account di archiviazione predefinito per il cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="b2fee-148">account di archiviazione per i dati di input</span><span class="sxs-lookup"><span data-stu-id="b2fee-148">storage account for the input data</span></span>
- <span data-ttu-id="b2fee-149">account di archiviazione per i dati di output</span><span class="sxs-lookup"><span data-stu-id="b2fee-149">storage account for the output data</span></span>

<span data-ttu-id="b2fee-150">Per semplificare l'esercitazione, si usa un solo account di archiviazione per tutti e tre gli scopi.</span><span class="sxs-lookup"><span data-stu-id="b2fee-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="b2fee-151">Lo script di esempio di Azure PowerShell di questa sezione consente di eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="b2fee-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="b2fee-152">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-152">Log in to Azure.</span></span>
2. <span data-ttu-id="b2fee-153">Creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="b2fee-154">Creare un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="b2fee-155">Creare un contenitore BLOB nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="b2fee-156">Copiare i due file seguenti nel contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="b2fee-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="b2fee-157">File di dati di input: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="b2fee-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="b2fee-158">Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="b2fee-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="b2fee-159">Entrambi i file vengono archiviati in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="b2fee-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="b2fee-160">**Per preparare l'archiviazione e copiare i file con Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="b2fee-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b2fee-161">Specificare i nomi del gruppo di risorse di Azure e dell'account di archiviazione di Azure che verranno creati dallo script.</span><span class="sxs-lookup"><span data-stu-id="b2fee-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="b2fee-162">Prendere nota del **nome del gruppo di risorse**, del **nome dell'account di archiviazione** e della **chiave dell'account di archiviazione** restituiti dallo script.</span><span class="sxs-lookup"><span data-stu-id="b2fee-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="b2fee-163">Saranno necessari nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="b2fee-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="b2fee-164">Per altre informazioni sullo script di PowerShell, vedere [Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="b2fee-165">Se invece si vuole usare l'interfaccia della riga di comando di Azure, vedere lo script corrispondente nella sezione [Appendice](#appendix).</span><span class="sxs-lookup"><span data-stu-id="b2fee-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="b2fee-166">**Per esaminare l'account di archiviazione e il suo contenuto**</span><span class="sxs-lookup"><span data-stu-id="b2fee-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="b2fee-167">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2fee-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2fee-168">Fare clic su **Gruppi di risorse** nel pannello di sinistra.</span><span class="sxs-lookup"><span data-stu-id="b2fee-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="b2fee-169">Fare doppio clic sul nome del gruppo di risorse creato con lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2fee-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="b2fee-170">Se sono presenti troppi gruppi di risorse elencati, usare il filtro.</span><span class="sxs-lookup"><span data-stu-id="b2fee-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="b2fee-171">Nel riquadro **Risorse** dovrebbe essere elencata una sola risorsa, a meno che il gruppo di risorse non sia condiviso con altri progetti.</span><span class="sxs-lookup"><span data-stu-id="b2fee-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="b2fee-172">Tale risorsa è l'account di archiviazione con il nome specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b2fee-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="b2fee-173">Fare clic sul nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-173">Click the storage account name.</span></span>
5. <span data-ttu-id="b2fee-174">Fare clic sui riquadri **BLOB** .</span><span class="sxs-lookup"><span data-stu-id="b2fee-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="b2fee-175">Fare clic sul contenitore **adfgetstarted** .</span><span class="sxs-lookup"><span data-stu-id="b2fee-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="b2fee-176">Vengono visualizzate due cartelle: **inputdata** e **script**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="b2fee-177">Aprire le cartelle e controllare i file al loro interno.</span><span class="sxs-lookup"><span data-stu-id="b2fee-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="b2fee-178">La cartella inputdata contiene il file input.log con i dati di input, mentre la cartella script contiene il file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="b2fee-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="b2fee-179">Creare una data factory usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2fee-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="b2fee-180">Con l'account di archiviazione, i dati di input e lo script HiveQL preparato, si è pronti per creare un'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="b2fee-181">Esistono diversi metodi per creare un'istanza di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="b2fee-182">In questa esercitazione si crea una data factory distribuendo un modello di Azure Resource Manager con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="b2fee-183">È possibile distribuire un modello di Resource Manager anche con l'[interfaccia della riga di comando di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="b2fee-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="b2fee-184">Per altri metodi di creazione di un'istanza di Data Factory, vedere [l'esercitazione per creare la prima istanza di Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="b2fee-185">Fare clic sull'immagine seguente per accedere ad Azure e aprire il modello di Resource Manager nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="b2fee-186">Il modello si trova all'indirizzo https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="b2fee-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="b2fee-187">Per informazioni dettagliate sulle entità definite nel modello, vedere la sezione [Entità di Data Factory nel modello](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="b2fee-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="b2fee-188">Selezionare l'opzione **Usa esistente** per l'impostazione **Gruppo di risorse** e quindi selezionare il nome del gruppo di risorse creato nel passaggio precedente (con lo script di PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b2fee-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="b2fee-189">Immettere un nome per la data factory in **Nome data factory**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="b2fee-190">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="b2fee-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="b2fee-191">Immettere il **nome dell'account di archiviazione** e la **chiave dell'account di archiviazione** di cui si è preso nota nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b2fee-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="b2fee-192">Dopo aver letto le **condizioni**, selezionare **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="b2fee-193">Selezionare l'opzione **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="b2fee-194">Fare clic su **Acquista/Crea**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="b2fee-195">Nel Dashboard è presente il riquadro **Distribuzione modello**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="b2fee-196">Attendere che venga visualizzato il pannello **Gruppo di risorse** per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b2fee-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="b2fee-197">Per aprire il pannello del gruppo di risorse è anche possibile fare clic sul riquadro con il nome del gruppo di risorse come titolo.</span><span class="sxs-lookup"><span data-stu-id="b2fee-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="b2fee-198">Se il pannello del gruppo di risorse non è visualizzato, fare clic sul riquadro per aprire il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b2fee-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="b2fee-199">Ora sarà visibile un'altra risorsa Data Factory oltre alla risorsa dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="b2fee-200">Fare clic sul nome della data factory, ossia sul valore specificato per il parametro **Nome data factory**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="b2fee-201">Nel pannello Data Factory fare clic sul riquadro **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="b2fee-202">Il diagramma mostra un'attività con un set di dati di input e un set di dati di output:</span><span class="sxs-lookup"><span data-stu-id="b2fee-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagramma della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="b2fee-204">I nomi sono definiti nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2fee-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="b2fee-205">Fare doppio clic su **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="b2fee-206">Tra le **sezioni aggiornate di recente**verrà visualizzata una sezione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="b2fee-207">Se lo stato è **In corso**, attendere finché non diventa **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="b2fee-208">Per creare un cluster HDInsight sono in genere necessari circa **20 minuti**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="b2fee-209">Controllare l'output della data factory</span><span class="sxs-lookup"><span data-stu-id="b2fee-209">Check the data factory output</span></span>

1. <span data-ttu-id="b2fee-210">Per controllare il contenuto dei contenitori adfgetstarted, usare la stessa procedura dell'ultima sessione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="b2fee-211">Oltre a **adfgetsarted**sono disponibili due nuovi contenitori:</span><span class="sxs-lookup"><span data-stu-id="b2fee-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="b2fee-212">Un contenitore il cui nome segue il modello `adf<yourdatafactoryname>-linkedservicename-datetimestamp`</span><span class="sxs-lookup"><span data-stu-id="b2fee-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="b2fee-213">e che è il contenitore predefinito per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2fee-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="b2fee-214">adfjobs, il contenitore per i log dei processi di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="b2fee-215">L'output della data factory viene archiviato in **adfgetstarted**, in base alla configurazione definita nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2fee-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="b2fee-216">Fare clic su **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="b2fee-217">Fare doppio clic su **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="b2fee-218">Verrà visualizzata una cartella **year=2014** perché tutti i blog sono datati 2014.</span><span class="sxs-lookup"><span data-stu-id="b2fee-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="b2fee-220">Eseguendo il drill-down dell'elenco si vedranno tre cartelle relative a gennaio, febbraio e marzo.</span><span class="sxs-lookup"><span data-stu-id="b2fee-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="b2fee-221">È presente un log per ogni mese.</span><span class="sxs-lookup"><span data-stu-id="b2fee-221">And there is a log for each month.</span></span>

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="b2fee-223">Entità di Data Factory nel modello</span><span class="sxs-lookup"><span data-stu-id="b2fee-223">Data Factory entities in the template</span></span>
<span data-ttu-id="b2fee-224">Il modello di Resource Manager di livello principale per una data factory si presenta come segue:</span><span class="sxs-lookup"><span data-stu-id="b2fee-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="b2fee-225">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="b2fee-225">Define data factory</span></span>
<span data-ttu-id="b2fee-226">È possibile definire una data factory nel modello di Resource Manager come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b2fee-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="b2fee-227">dataFactoryName è il nome della data factory specificato quando si distribuisce il modello.</span><span class="sxs-lookup"><span data-stu-id="b2fee-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="b2fee-228">Il servizio Data Factory è attualmente supportato solo negli Stati Uniti occidentali, negli Stati Uniti orientali e in Europa settentrionale.</span><span class="sxs-lookup"><span data-stu-id="b2fee-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="b2fee-229">Definizione delle entità nella data factory</span><span class="sxs-lookup"><span data-stu-id="b2fee-229">Defining entities within the data factory</span></span>
<span data-ttu-id="b2fee-230">Le entità di Data Factory seguenti vengono definite nel modello JSON:</span><span class="sxs-lookup"><span data-stu-id="b2fee-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="b2fee-231">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="b2fee-232">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="b2fee-233">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="b2fee-234">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="b2fee-235">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="b2fee-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b2fee-236">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-236">Azure Storage linked service</span></span>
<span data-ttu-id="b2fee-237">Il servizio collegato Archiviazione di Azure collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="b2fee-238">In questa esercitazione lo stesso account di archiviazione viene usato come account di Archiviazione HDInsight predefinito, come archivio dati di input e come archivio dati di output.</span><span class="sxs-lookup"><span data-stu-id="b2fee-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="b2fee-239">Di conseguenza, si definisce un solo servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="b2fee-240">Nella definizione del servizio collegato si specificano il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="b2fee-241">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Archiviazione di Azure, vedere [Servizio collegato Archiviazione di Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b2fee-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="b2fee-242">**connectionString** usa i parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="b2fee-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="b2fee-243">I valori per questi parametri vengono specificati durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="b2fee-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="b2fee-244">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="b2fee-245">Nella definizione del servizio collegato HDInsight su richiesta si specificano i valori per i parametri di configurazione usati dal servizio Data Factory per creare un cluster Hadoop di HDInsight in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="b2fee-246">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato su richiesta HDInsight, vedere [Servizi collegati di calcolo](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b2fee-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="b2fee-247">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b2fee-247">Note the following points:</span></span>

* <span data-ttu-id="b2fee-248">Data Factory crea automaticamente un cluster HDInsight **basato su Linux**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="b2fee-249">Il cluster Hadoop di HDInsight viene creato nella stessa area dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="b2fee-250">Si noti l'impostazione di *timeToLive* .</span><span class="sxs-lookup"><span data-stu-id="b2fee-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="b2fee-251">Data Factory elimina automaticamente il cluster dopo un periodo di inattività di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="b2fee-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="b2fee-252">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="b2fee-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="b2fee-253">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="b2fee-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="b2fee-254">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-254">This behavior is by design.</span></span> <span data-ttu-id="b2fee-255">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che è necessario elaborare una sezione, a meno che non esista un cluster attivo (**timeToLive**) che viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="b2fee-256">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="b2fee-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2fee-257">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="b2fee-258">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="b2fee-259">I nomi dei contenitori seguono questo schema: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="b2fee-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="b2fee-260">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="b2fee-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="b2fee-261">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-261">Azure blob input dataset</span></span>
<span data-ttu-id="b2fee-262">Nella definizione del set di dati di input si specificano i nomi del contenitore BLOB, della cartella e del file contenente i dati di input.</span><span class="sxs-lookup"><span data-stu-id="b2fee-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="b2fee-263">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b2fee-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="b2fee-264">Nella definizione JSON, si notino le impostazioni specifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2fee-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b2fee-265">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-265">Azure Blob output dataset</span></span>
<span data-ttu-id="b2fee-266">Nella definizione del set di dati di output si specificano i nomi del contenitore BLOB e della cartella contenente i dati di output.</span><span class="sxs-lookup"><span data-stu-id="b2fee-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="b2fee-267">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b2fee-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="b2fee-268">folderPath specifica il percorso della cartella contenente i dati di output:</span><span class="sxs-lookup"><span data-stu-id="b2fee-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="b2fee-269">L'impostazione [disponibilità dei set di dati](../data-factory/data-factory-create-datasets.md#dataset-availability) è la seguente:</span><span class="sxs-lookup"><span data-stu-id="b2fee-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="b2fee-270">In Azure Data Factory, la disponibilità dei set di dati di output attiva la pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2fee-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="b2fee-271">In questo esempio, la sezione viene prodotta mensilmente l'ultimo giorno del mese (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="b2fee-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="b2fee-272">Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="b2fee-273">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="b2fee-273">Data pipeline</span></span>
<span data-ttu-id="b2fee-274">Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta.</span><span class="sxs-lookup"><span data-stu-id="b2fee-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="b2fee-275">Per le descrizioni degli elementi JSON usati per definire una pipeline in questo esempio, vedere [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="b2fee-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="b2fee-276">La pipeline contiene un'attività, HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="b2fee-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="b2fee-277">Poiché sia la data di inizio che la data di fine sono nel mese di gennaio 2016, vengono elaboratori i dati per un solo mese (una sezione).</span><span class="sxs-lookup"><span data-stu-id="b2fee-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="b2fee-278">Le date di *inizio* e di *fine* dell'attività sono entrambe già passate, quindi Data Factory elabora i dati del mese immediatamente.</span><span class="sxs-lookup"><span data-stu-id="b2fee-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="b2fee-279">Se la data finale è futura, Data Factory crea un'altra sezione a tempo debito.</span><span class="sxs-lookup"><span data-stu-id="b2fee-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="b2fee-280">Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="b2fee-281">Eseguire la pulizia dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b2fee-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="b2fee-282">Eliminare i contenitori BLOB creati dal cluster HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="b2fee-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="b2fee-283">Con il servizio collegato HDInsight on demand viene creato un cluster HDInsight ogni volta che è necessario elaborare una sezione, a meno che non esista un cluster attivo, timeToLive, che viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="b2fee-284">Per ogni cluster, Azure Data Factory crea un contenitore BLOB nell'archivio BLOB di Azure usato come account di archiviazione predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="b2fee-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="b2fee-285">Anche se il cluster HDInsight viene eliminato, il contenitore di archiviazione BLOB predefinito e l'account di archiviazione associato non vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="b2fee-286">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-286">This behavior is by design.</span></span> <span data-ttu-id="b2fee-287">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fee-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="b2fee-288">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2fee-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="b2fee-289">I nomi dei contenitori seguono il modello `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="b2fee-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="b2fee-290">Eliminare le cartelle **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="b2fee-291">Il contenitore adfjobs contiene i log dei processi di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="b2fee-292">Eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b2fee-292">Delete the resource group</span></span>
<span data-ttu-id="b2fee-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) viene usato per distribuire, gestire e monitorare la soluzione come gruppo.</span><span class="sxs-lookup"><span data-stu-id="b2fee-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="b2fee-294">Eliminando un gruppo di risorse vengono eliminati tutti i componenti all'interno del gruppo.</span><span class="sxs-lookup"><span data-stu-id="b2fee-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="b2fee-295">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2fee-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2fee-296">Fare clic su **Gruppi di risorse** nel pannello di sinistra.</span><span class="sxs-lookup"><span data-stu-id="b2fee-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="b2fee-297">Fare clic sul nome del gruppo di risorse creato con lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2fee-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="b2fee-298">Se sono presenti troppi gruppi di risorse elencati, usare il filtro.</span><span class="sxs-lookup"><span data-stu-id="b2fee-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="b2fee-299">Viene aperto il gruppo di risorse in un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="b2fee-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="b2fee-300">Nel riquadro **Risorse** dovrebbe essere indicato l'account di archiviazione predefinito e l'istanza Data Factory, a meno che il gruppo di risorse non sia condiviso con altri progetti.</span><span class="sxs-lookup"><span data-stu-id="b2fee-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="b2fee-301">Fare clic su **Elimina** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="b2fee-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="b2fee-302">In questo modo si eliminano l'account di archiviazione e i dati in esso archiviati.</span><span class="sxs-lookup"><span data-stu-id="b2fee-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="b2fee-303">Immettere il nome del gruppo di risorse per confermare l'eliminazione e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="b2fee-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="b2fee-304">Se non si vuole eliminare l'account di archiviazione quando si elimina il gruppo di risorse, prendere in considerazione l'architettura seguente in modo da separare i dati aziendali dall'account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="b2fee-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="b2fee-305">In questo caso, si ha un gruppo di risorse per l'account di archiviazione con i dati aziendali e un secondo gruppo di risorse per l'account di archiviazione predefinito per il servizio collegato HDInsight e la data factory.</span><span class="sxs-lookup"><span data-stu-id="b2fee-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="b2fee-306">L'eliminazione del secondo gruppo di risorse non influisce sull'account di archiviazione dei dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="b2fee-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="b2fee-307">A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="b2fee-307">To do so:</span></span>

* <span data-ttu-id="b2fee-308">Aggiungere quanto segue al gruppo di risorse di livello principale insieme alla risorsa Microsoft.DataFactory/datafactories nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2fee-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="b2fee-309">Viene creato un account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b2fee-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="b2fee-310">Aggiungere un nuovo punto di servizio collegato al nuovo account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b2fee-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="b2fee-311">Configurare il servizio collegato HDInsight on demand con un dependsOn e un additionalLinkedServiceNames aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="b2fee-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="b2fee-312">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2fee-312">Next steps</span></span>
<span data-ttu-id="b2fee-313">Questo articolo ha descritto come usare Azure Data Factory per creare il cluster HDInsight on demand per l'elaborazione dei processi Hive.</span><span class="sxs-lookup"><span data-stu-id="b2fee-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="b2fee-314">Altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="b2fee-314">To read more:</span></span>

* [<span data-ttu-id="b2fee-315">Esercitazione di Hadoop: Introduzione all'uso di Hadoop basato su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="b2fee-316">Creare cluster Hadoop basati su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="b2fee-317">Documentazione relativa a HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2fee-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="b2fee-318">Documentazione di Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2fee-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="b2fee-319">Appendice</span><span class="sxs-lookup"><span data-stu-id="b2fee-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="b2fee-320">Script dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b2fee-320">Azure CLI script</span></span>
<span data-ttu-id="b2fee-321">Per eseguire l'esercitazione è possibile usare l'interfaccia della riga di comando di Azure anziché Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2fee-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="b2fee-322">Per usare l'interfaccia della riga di comando di Azure, per prima cosa installarla seguendo queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b2fee-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="b2fee-323">Usare l'interfaccia della riga di comando di Azure per preparare l'archiviazione e copiare i file</span><span class="sxs-lookup"><span data-stu-id="b2fee-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="b2fee-324">Il nome del contenitore è *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="b2fee-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="b2fee-325">Mantenerlo invariato,</span><span class="sxs-lookup"><span data-stu-id="b2fee-325">Keep it as it is.</span></span> <span data-ttu-id="b2fee-326">altrimenti sarebbe necessario aggiornare il modello di modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2fee-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="b2fee-327">Se occorre assistenza per questo script dell'interfaccia della riga di comando, vedere [Utilizzo dell'interfaccia della riga di comando di Azure con archiviazione di Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b2fee-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
