---
title: cluster di Hadoop su richiesta utilizzando Data Factory - Azure HDInsight aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate cluster su richiesta Hadoop in HDInsight mediante la Data Factory di Azure.
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
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="8f35b-103">Creare cluster Hadoop on demand in HDInsight con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8f35b-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="8f35b-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="8f35b-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="8f35b-105">È possibile creare un tooprocess just-in-time di cluster HDInsight Hadoop una sezione di dati di input ed eliminare cluster hello termine dell'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="8f35b-106">Alcuni dei vantaggi di hello dell'utilizzo di un cluster HDInsight Hadoop su richiesta sono:</span><span class="sxs-lookup"><span data-stu-id="8f35b-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="8f35b-107">Si pagare solo per il processo ora hello è in esecuzione hello del cluster HDInsight Hadoop (più un tempo di inattività configurabile breve).</span><span class="sxs-lookup"><span data-stu-id="8f35b-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="8f35b-108">la fatturazione per i cluster HDInsight Hello è proporzionale al minuto, sia che si utilizzi o non.</span><span class="sxs-lookup"><span data-stu-id="8f35b-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="8f35b-109">Quando si utilizza un servizio collegato di HDInsight su richiesta in Data Factory, i cluster hello vengono creati su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="8f35b-110">E i cluster hello vengono eliminati automaticamente quando vengono completati i processi di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="8f35b-111">Pertanto, si paga solo per il processo di hello esegue ora e tempo di inattività breve hello (impostazione di time-to-live).</span><span class="sxs-lookup"><span data-stu-id="8f35b-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="8f35b-112">È possibile creare un flusso di lavoro usando una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8f35b-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="8f35b-113">Ad esempio, è possibile disporre hello pipeline toocopy di dati da un tooan di SQL Server on-premise archiviazione blob di Azure, dati hello processo eseguendo uno script Hive e uno script Pig in un cluster HDInsight Hadoop su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="8f35b-114">Copiare quindi hello risultato dati tooan Azure SQL Data Warehouse per tooconsume applicazioni di Business Intelligence.</span><span class="sxs-lookup"><span data-stu-id="8f35b-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="8f35b-115">È possibile pianificare hello del flusso di lavoro toorun periodicamente (oraria, giornaliera, settimanale, mensile, ecc.).</span><span class="sxs-lookup"><span data-stu-id="8f35b-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="8f35b-116">In Azure Data Factory, una data factory può includere una o più pipeline di dati.</span><span class="sxs-lookup"><span data-stu-id="8f35b-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="8f35b-117">Una pipeline di dati include una o più attività.</span><span class="sxs-lookup"><span data-stu-id="8f35b-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="8f35b-118">Esistono due tipi di attività: [attività di spostamento dei dati](../data-factory/data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="8f35b-119">Utilizzare dati toomove di attività (attualmente solo attività di copia) lo spostamento di dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="8f35b-120">Utilizzare i dati o il processo tootransform attività di trasformazione dati.</span><span class="sxs-lookup"><span data-stu-id="8f35b-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="8f35b-121">Attività Hive di HDInsight è una delle attività di trasformazione hello è supportata da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8f35b-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="8f35b-122">Utilizzare l'attività di trasformazione Hive hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="8f35b-123">È possibile configurare un toouse attività hive cluster HDInsight Hadoop personale o un cluster HDInsight Hadoop su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="8f35b-124">In questa esercitazione, hello attività Hive nella pipeline di hello data factory è toouse configurato un cluster di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="8f35b-125">Pertanto, quando viene eseguita attività hello tooprocess una sezione di dati, ecco cosa succede:</span><span class="sxs-lookup"><span data-stu-id="8f35b-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="8f35b-126">-In-time tooprocess hello suddividere viene creato automaticamente un cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8f35b-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="8f35b-127">dati di input Hello viene elaborati eseguendo uno script HiveQL nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="8f35b-128">cluster HDInsight Hadoop Hello viene eliminato dopo l'elaborazione di hello e cluster hello è inattivo per hello configurato di tempo (impostazione timeToLive).</span><span class="sxs-lookup"><span data-stu-id="8f35b-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="8f35b-129">Se è disponibile per l'elaborazione con il tempo di inattività timeToLive sezione di dati successiva hello, hello dello stesso cluster è sezione hello tooprocess utilizzato.</span><span class="sxs-lookup"><span data-stu-id="8f35b-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="8f35b-130">In questa esercitazione, hello script HiveQL associato all'attività hive hello esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="8f35b-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="8f35b-131">Crea una tabella esterna che riferimenti hello dati di log web non elaborato archiviati in una risorsa di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="8f35b-132">Dati non elaborati hello di partizioni per anno e mese.</span><span class="sxs-lookup"><span data-stu-id="8f35b-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="8f35b-133">Archivi hello dati partizionati in hello archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="8f35b-134">In questa esercitazione, hello script HiveQL associato all'attività hive hello crea una tabella esterna che riferimenti hello dati di registro non elaborati web archiviati in hello archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="8f35b-135">Di seguito sono le righe di esempio hello per ogni mese nel file di input hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="8f35b-136">le partizioni di script HiveQL Hello hello dati non elaborati per anno e mese.</span><span class="sxs-lookup"><span data-stu-id="8f35b-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="8f35b-137">Vengono create tre cartelle di output in base all'input precedente hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="8f35b-138">Ogni cartella contiene un file con le voci di ogni mese.</span><span class="sxs-lookup"><span data-stu-id="8f35b-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="8f35b-139">Per un elenco delle attività di trasformazione di dati di Data Factory in attività tooHive aggiunta, vedere [trasformare e analizzare l'utilizzo di Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8f35b-140">Attualmente, da Azure Data Factory è possibile creare solo cluster HDInsight versione 3.2.</span><span class="sxs-lookup"><span data-stu-id="8f35b-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f35b-141">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f35b-141">Prerequisites</span></span>
<span data-ttu-id="8f35b-142">Prima di iniziare hello istruzioni in questo articolo, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8f35b-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="8f35b-143">[Sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8f35b-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8f35b-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f35b-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="8f35b-145">Preparare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8f35b-145">Prepare storage account</span></span>
<span data-ttu-id="8f35b-146">È possibile utilizzare gli account di archiviazione toothree in questo scenario:</span><span class="sxs-lookup"><span data-stu-id="8f35b-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="8f35b-147">account di archiviazione predefinito per il cluster HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="8f35b-148">account di archiviazione per i dati di input hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-148">storage account for hello input data</span></span>
- <span data-ttu-id="8f35b-149">account di archiviazione per i dati di output di hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-149">storage account for hello output data</span></span>

<span data-ttu-id="8f35b-150">esercitazione di hello toosimplify, utilizzare un account tooserve hello tre scopi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="8f35b-151">script di esempio Hello Azure PowerShell riportati in questa sezione vengono eseguite hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="8f35b-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="8f35b-152">Accedi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="8f35b-153">Creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="8f35b-154">Creare un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="8f35b-155">Creare un contenitore Blob nell'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="8f35b-156">Copiare hello contenitore Blob di due file toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f35b-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="8f35b-157">File di dati di input: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="8f35b-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="8f35b-158">Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="8f35b-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="8f35b-159">Entrambi i file vengono archiviati in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="8f35b-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="8f35b-160">**tooprepare hello archiviazione e copiare hello file tramite Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="8f35b-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f35b-161">Specificare i nomi per il gruppo di risorse di Azure hello e hello account di archiviazione Azure che verrà creato dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="8f35b-162">Annotare **nome gruppo di risorse**, **nome account di archiviazione**, e **chiave account di archiviazione** restituite dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="8f35b-163">È necessario nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="8f35b-164">Per assistenza con script di PowerShell hello, vedere [hello tramite Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="8f35b-165">Se si desidera toouse CLI di Azure, vedere hello [appendice](#appendix) sezione per hello script CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="8f35b-166">**tooexamine hello storage account e hello contenuto**</span><span class="sxs-lookup"><span data-stu-id="8f35b-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="8f35b-167">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f35b-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f35b-168">Fare clic su **gruppi di risorse** hello riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8f35b-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="8f35b-169">Fare doppio clic sul nome del gruppo di risorse hello che è stato creato nello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f35b-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="8f35b-170">Se si dispone di un numero eccessivo di gruppi di risorse elencati, utilizzare il filtro di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="8f35b-171">In hello **risorse** riquadro, si deve essere presente una risorsa elencata, a meno che il gruppo di risorse hello è condividere con altri progetti.</span><span class="sxs-lookup"><span data-stu-id="8f35b-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="8f35b-172">Questa risorsa è l'account di archiviazione hello con nome hello specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8f35b-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="8f35b-173">Fare clic su nome account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="8f35b-174">Fare clic su hello **BLOB** riquadri.</span><span class="sxs-lookup"><span data-stu-id="8f35b-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="8f35b-175">Fare clic su hello **adfgetstarted** contenitore.</span><span class="sxs-lookup"><span data-stu-id="8f35b-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="8f35b-176">Vengono visualizzate due cartelle: **inputdata** e **script**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="8f35b-177">Aprire la cartella hello e controllare i file nelle cartelle hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="8f35b-178">cartella script hello contiene file di script HiveQL hello inputdata Hello contiene file input.log hello con dati di input.</span><span class="sxs-lookup"><span data-stu-id="8f35b-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="8f35b-179">Creare una data factory usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f35b-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="8f35b-180">Con account di archiviazione hello, dati di input hello e hello script HiveQL preparato, si è pronti toocreate una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="8f35b-181">Esistono diversi metodi per creare un'istanza di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8f35b-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="8f35b-182">In questa esercitazione creerai una data factory tramite la distribuzione di un modello di gestione risorse di Azure tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="8f35b-183">È possibile distribuire un modello di Resource Manager anche con l'[interfaccia della riga di comando di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="8f35b-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="8f35b-184">Per altri metodi di creazione di un'istanza di Data Factory, vedere [l'esercitazione per creare la prima istanza di Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="8f35b-185">Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="8f35b-186">modello Hello si trova in https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="8f35b-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="8f35b-187">Vedere hello [entità Data Factory nel modello hello](#data-factory-entities-in-the-template) sezione per informazioni dettagliate sulle entità definite nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="8f35b-188">Selezionare **Usa esistente** opzione per hello **gruppo di risorse** , impostazione e il nome di hello selezionare hello del gruppo di risorse creato nel passaggio precedente di hello (tramite script di PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8f35b-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="8f35b-189">Immettere un nome per data factory di hello (**nome della Data Factory**).</span><span class="sxs-lookup"><span data-stu-id="8f35b-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="8f35b-190">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="8f35b-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="8f35b-191">Immettere hello **nome account di archiviazione** e **chiave account di archiviazione** annotate nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="8f35b-192">Selezionare **accetto le condizioni toohello** indicati sopra la a **termini e condizioni**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="8f35b-193">Selezionare **toodashboard Pin** opzione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="8f35b-194">Fare clic su **Acquista/Crea**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="8f35b-195">Viene visualizzato un riquadro nel Dashboard chiamato hello **distribuzione del modello di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="8f35b-196">Attendere hello **gruppo di risorse** apre pannello per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f35b-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="8f35b-197">È anche possibile fare clic su riquadro hello denominato come il pannello di gruppo di risorse gruppo nome tooopen hello risorsa.</span><span class="sxs-lookup"><span data-stu-id="8f35b-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="8f35b-198">Fare clic su gruppo di risorse di hello riquadro tooopen hello pannello della risorsa gruppo hello non è già aperto.</span><span class="sxs-lookup"><span data-stu-id="8f35b-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="8f35b-199">Ora verrà visualizzata una risorsa di ulteriori dati factory inoltre toohello archiviazione account risorsa indicata.</span><span class="sxs-lookup"><span data-stu-id="8f35b-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="8f35b-200">Fare clic sul nome di una factory di dati hello (valore specificato per hello **nome della Data Factory** parametro).</span><span class="sxs-lookup"><span data-stu-id="8f35b-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="8f35b-201">Nel Pannello di Data Factory hello, fare clic su hello **diagramma** riquadro.</span><span class="sxs-lookup"><span data-stu-id="8f35b-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="8f35b-202">Hello è illustrata un'attività con un set di dati di input e un set di dati di output:</span><span class="sxs-lookup"><span data-stu-id="8f35b-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagramma della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="8f35b-204">i nomi di Hello vengono definiti nel modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="8f35b-205">Fare doppio clic su **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="8f35b-206">In hello **recenti aggiornato sezioni**, verrà visualizzata un'unica sezione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="8f35b-207">Se è stato hello **In corso**, attendere fino a quando non è stato modificato anche**pronto**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="8f35b-208">In genere richiede circa **20 minuti** toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8f35b-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="8f35b-209">Controllare l'output di hello data factory</span><span class="sxs-lookup"><span data-stu-id="8f35b-209">Check hello data factory output</span></span>

1. <span data-ttu-id="8f35b-210">Utilizzare hello stessa procedura in hello ultima sessione toocheck hello contenitori del contenitore adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="8f35b-211">Esistono due nuovi contenitori inoltre troppo**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="8f35b-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="8f35b-212">Un contenitore con nome che segue il modello di hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="8f35b-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="8f35b-213">Questo contenitore è il contenitore predefinito hello per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="8f35b-214">adfjobs: questo contenitore è il contenitore di hello hello ADF dei log dei processi.</span><span class="sxs-lookup"><span data-stu-id="8f35b-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="8f35b-215">output di Hello data factory viene archiviato **afgetstarted** come configurato nel modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="8f35b-216">Fare clic su **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="8f35b-217">Fare doppio clic su **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="8f35b-218">Viene visualizzato un **anno = 2014** cartella perché tutti i log web hello data nell'anno 2014.</span><span class="sxs-lookup"><span data-stu-id="8f35b-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="8f35b-220">Se il drill-down elenco hello, verrà visualizzato tre cartelle relativi a gennaio, febbraio e marzo.</span><span class="sxs-lookup"><span data-stu-id="8f35b-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="8f35b-221">È presente un log per ogni mese.</span><span class="sxs-lookup"><span data-stu-id="8f35b-221">And there is a log for each month.</span></span>

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="8f35b-223">Entità di modello hello Factory di dati</span><span class="sxs-lookup"><span data-stu-id="8f35b-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="8f35b-224">Ecco come modello di gestione risorse per una data factory di primo livello hello simile:</span><span class="sxs-lookup"><span data-stu-id="8f35b-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="8f35b-225">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="8f35b-225">Define data factory</span></span>
<span data-ttu-id="8f35b-226">È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="8f35b-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="8f35b-227">dataFactoryName Hello è il nome di hello di hello data factory che è specificare quando si distribuisce il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="8f35b-228">Factory di dati è attualmente supportata solo in aree geografiche di Stati Uniti orientali, Stati Uniti occidentali e Nord Europa hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="8f35b-229">Definizione di entità all'interno di data factory di hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="8f35b-230">Hello entità Data Factory seguenti vengono definite nel modello JSON hello:</span><span class="sxs-lookup"><span data-stu-id="8f35b-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="8f35b-231">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="8f35b-232">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f35b-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="8f35b-233">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="8f35b-234">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="8f35b-235">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="8f35b-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="8f35b-236">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-236">Azure Storage linked service</span></span>
<span data-ttu-id="8f35b-237">Archiviazione di Azure Hello collegato collegamenti al servizio la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="8f35b-238">In questa esercitazione, hello stesso account di archiviazione viene utilizzato come account di archiviazione di hello predefinito HDInsight, archiviazione di dati di input e archiviazione dei dati di output.</span><span class="sxs-lookup"><span data-stu-id="8f35b-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="8f35b-239">Di conseguenza, si definisce un solo servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="8f35b-240">Nella definizione di servizio collegato hello, specificare il nome di hello e chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="8f35b-241">Vedere [servizio collegato di archiviazione di Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

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
<span data-ttu-id="8f35b-242">Hello **connectionString** utilizza hello parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="8f35b-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="8f35b-243">Si specificano valori per questi parametri durante la distribuzione del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="8f35b-244">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f35b-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="8f35b-245">In hello HDInsight su richiesta collegato definizione del servizio, si specificano valori per parametri di configurazione che vengono utilizzati da toocreate servizio Data Factory di hello un HDInsight Hadoop cluster in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="8f35b-246">Vedere [servizi collegati di calcolo](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) articolo per informazioni dettagliate su JSON proprietà utilizzate toodefine un servizio collegato di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="8f35b-247">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="8f35b-247">Note hello following points:</span></span>

* <span data-ttu-id="8f35b-248">Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente.</span><span class="sxs-lookup"><span data-stu-id="8f35b-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="8f35b-249">Hello cluster HDInsight Hadoop viene creato in hello stessa regione dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="8f35b-250">Hello preavviso *timeToLive* impostazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="8f35b-251">data factory di Hello Elimina automaticamente i cluster hello dopo cluster hello è un periodo di inattività per 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="8f35b-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="8f35b-252">Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="8f35b-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="8f35b-253">HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="8f35b-254">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-254">This behavior is by design.</span></span> <span data-ttu-id="8f35b-255">Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="8f35b-256">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="8f35b-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f35b-257">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="8f35b-258">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="8f35b-259">i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="8f35b-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="8f35b-260">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="8f35b-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="8f35b-261">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-261">Azure blob input dataset</span></span>
<span data-ttu-id="8f35b-262">Nella definizione di set di dati input hello, specificare nomi di hello del contenitore blob, cartelle e file che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="8f35b-263">Vedere [proprietà set di dati Blob di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

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

<span data-ttu-id="8f35b-264">Si noti hello impostazioni specifiche nella definizione JSON hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f35b-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="8f35b-265">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-265">Azure Blob output dataset</span></span>
<span data-ttu-id="8f35b-266">Nella definizione di set di dati di output hello, specificare nomi hello del contenitore blob e di cartella che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="8f35b-267">Vedere [proprietà set di dati Blob di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="8f35b-268">folderPath Hello specifica hello toohello cartella che contiene i dati di output di hello:</span><span class="sxs-lookup"><span data-stu-id="8f35b-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="8f35b-269">Hello [disponibilità dataset](../data-factory/data-factory-create-datasets.md#dataset-availability) impostazione è come segue:</span><span class="sxs-lookup"><span data-stu-id="8f35b-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="8f35b-270">In Data Factory di Azure, l'output della pipeline di set di dati disponibilità unità hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="8f35b-271">In questo esempio hello sezione viene prodotta mensile hello ultimo giorno del mese (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="8f35b-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="8f35b-272">Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="8f35b-273">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="8f35b-273">Data pipeline</span></span>
<span data-ttu-id="8f35b-274">Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta.</span><span class="sxs-lookup"><span data-stu-id="8f35b-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="8f35b-275">Vedere [JSON di Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="8f35b-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

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

<span data-ttu-id="8f35b-276">pipeline di Hello contiene un'attività, attività HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="8f35b-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="8f35b-277">Poiché sia la data di inizio che la data di fine sono nel mese di gennaio 2016, vengono elaboratori i dati per un solo mese (una sezione).</span><span class="sxs-lookup"><span data-stu-id="8f35b-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="8f35b-278">Entrambi *avviare* e *fine* dell'attività hello presentano una data già trascorsa, pertanto hello Data Factory elabora i dati per mese hello immediatamente.</span><span class="sxs-lookup"><span data-stu-id="8f35b-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="8f35b-279">Se una data futura fine hello è data factory di hello crea un'altra sezione al momento di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="8f35b-280">Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="8f35b-281">Pulire esercitazione hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="8f35b-282">Eliminare i contenitori di blob hello creati dal cluster HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="8f35b-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="8f35b-283">Con il servizio collegato di HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster in tempo reale esistente (timeToLive); e hello cluster viene eliminato quando viene eseguita l'elaborazione di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="8f35b-284">Per ogni cluster, Azure Data Factory crea un contenitore blob nell'archiviazione blob di Azure utilizzato come account di archiviazione predefinito hello per cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="8f35b-285">Anche se il cluster HDInsight è stato eliminato, contenitore di archiviazione blob di hello predefinito e account di archiviazione hello associato non vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="8f35b-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="8f35b-286">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-286">This behavior is by design.</span></span> <span data-ttu-id="8f35b-287">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f35b-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="8f35b-288">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f35b-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="8f35b-289">i nomi di Hello di questi contenitori seguono un modello: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="8f35b-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="8f35b-290">Eliminare hello **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp** cartelle.</span><span class="sxs-lookup"><span data-stu-id="8f35b-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="8f35b-291">contenitore adfjobs Hello contiene i registri dei processi da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8f35b-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="8f35b-292">Eliminare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-292">Delete hello resource group</span></span>
<span data-ttu-id="8f35b-293">[Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) è usato toodeploy, gestire e monitorare la soluzione come gruppo.</span><span class="sxs-lookup"><span data-stu-id="8f35b-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="8f35b-294">Se si elimina un gruppo di risorse, tutti i componenti di hello all'interno di hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="8f35b-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="8f35b-295">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f35b-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f35b-296">Fare clic su **gruppi di risorse** hello riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8f35b-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="8f35b-297">Fare clic su nome gruppo di risorse hello che è stato creato nello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f35b-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="8f35b-298">Se si dispone di un numero eccessivo di gruppi di risorse elencati, utilizzare il filtro di hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="8f35b-299">Gruppo di risorse hello viene aperto in un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="8f35b-300">In hello **risorse** riquadro, si hanno account di archiviazione predefinito hello e hello data factory elencati, a meno che il gruppo di risorse hello è condividere con altri progetti.</span><span class="sxs-lookup"><span data-stu-id="8f35b-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="8f35b-301">Fare clic su **eliminare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="8f35b-302">In questo modo Elimina l'account di archiviazione hello e dati hello archiviati nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="8f35b-303">Immettere l'eliminazione del tooconfirm nome gruppo di risorse hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="8f35b-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="8f35b-304">Nel caso in cui non si desidera account di archiviazione hello toodelete quando si elimina il gruppo di risorse hello, prendere in considerazione hello seguente architettura separando i dati di business hello dall'account di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="8f35b-305">In questo caso, si dispone di un gruppo di risorse per account di archiviazione hello con i dati aziendali hello e hello altro gruppo di risorse per account di archiviazione predefinito hello HDInsight collegato hello e servizio data factory.</span><span class="sxs-lookup"><span data-stu-id="8f35b-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="8f35b-306">Quando si elimina il gruppo di risorse secondo hello, non influisce sulla account di archiviazione di dati business hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="8f35b-307">toodo in modo:</span><span class="sxs-lookup"><span data-stu-id="8f35b-307">toodo so:</span></span>

* <span data-ttu-id="8f35b-308">Aggiungere hello seguente gruppo di risorse di primo livello toohello insieme hello Microsoft.DataFactory/datafactories risorse nel modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="8f35b-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="8f35b-309">Viene creato un account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="8f35b-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="8f35b-310">Aggiungere un nuovo servizio collegato punto toohello nuovo account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="8f35b-310">Add a new linked service point toohello new storage account:</span></span>

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
* <span data-ttu-id="8f35b-311">Configurare il servizio ondemand collegato di HDInsight hello con un dependsOn aggiuntive e un additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="8f35b-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="8f35b-312">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f35b-312">Next steps</span></span>
<span data-ttu-id="8f35b-313">In questo articolo, si è appreso come toouse su richiesta toocreate Data Factory di Azure HDInsight cluster tooprocess processi Hive.</span><span class="sxs-lookup"><span data-stu-id="8f35b-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="8f35b-314">tooread più:</span><span class="sxs-lookup"><span data-stu-id="8f35b-314">tooread more:</span></span>

* [<span data-ttu-id="8f35b-315">Esercitazione di Hadoop: Introduzione all'uso di Hadoop basato su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f35b-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="8f35b-316">Creare cluster Hadoop basati su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f35b-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="8f35b-317">Documentazione relativa a HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f35b-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="8f35b-318">Documentazione di Data Factory</span><span class="sxs-lookup"><span data-stu-id="8f35b-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="8f35b-319">Appendice</span><span class="sxs-lookup"><span data-stu-id="8f35b-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="8f35b-320">Script dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8f35b-320">Azure CLI script</span></span>
<span data-ttu-id="8f35b-321">È possibile utilizzare l'interfaccia CLI di Azure anziché utilizzare l'esercitazione di Azure PowerShell toodo hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="8f35b-322">toouse CLI di Azure, installare innanzitutto CLI di Azure in base alle hello attenendosi alle istruzioni:</span><span class="sxs-lookup"><span data-stu-id="8f35b-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="8f35b-323">Utilizzare l'archiviazione di Azure CLI tooprepare hello e copiare i file hello</span><span class="sxs-lookup"><span data-stu-id="8f35b-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

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

<span data-ttu-id="8f35b-324">nome di contenitore Hello *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="8f35b-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="8f35b-325">Mantenerlo invariato,</span><span class="sxs-lookup"><span data-stu-id="8f35b-325">Keep it as it is.</span></span> <span data-ttu-id="8f35b-326">In caso contrario è necessario un modello di gestione risorse di tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="8f35b-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="8f35b-327">Per assistenza con questo script CLI, vedere [Using hello CLI di Azure con l'archiviazione di Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8f35b-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
