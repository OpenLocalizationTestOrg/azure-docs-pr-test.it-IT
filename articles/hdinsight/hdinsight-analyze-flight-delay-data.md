---
title: dati del ritardo di volo aaaAnalyze con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse uno Windows PowerShell script toocreate un cluster HDInsight, eseguire un processo Hive, eseguire un processo Sqoop ed eliminare cluster hello.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="4d259-103">Analizzare i dati sui ritardi dei voli con Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d259-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="4d259-104">Hive fornisce un metodo per l'esecuzione di processi MapReduce mediante un linguaggio di scripting simile a SQL, denominato *[HiveQL][hadoop-hiveql]*, che può essere applicato per attività di riepilogo, query e analisi di volumi di dati molto elevati.</span><span class="sxs-lookup"><span data-stu-id="4d259-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d259-105">Hello passaggi in questo documento richiedono un cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="4d259-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="4d259-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4d259-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4d259-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4d259-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="4d259-108">Per i passaggi relativi a un cluster basato su Linux, vedere [Analizzare i dati sui ritardi dei voli con Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4d259-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="4d259-109">Uno dei vantaggi principali di hello di Azure HDInsight è la separazione di hello del calcolo e archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4d259-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="4d259-110">HDInsight usa l'archiviazione BLOB di Azure per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4d259-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="4d259-111">Un tipico processo è costituito da tre parti:</span><span class="sxs-lookup"><span data-stu-id="4d259-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="4d259-112">**Archiviare dati nell'archivio BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4d259-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="4d259-113">Ad esempio, i dati meteo, i dati dei sensori, i blog e, in questo caso, i dati sui ritardi dei voli vengono salvati nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="4d259-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="4d259-114">**Eseguire i processi.**</span><span class="sxs-lookup"><span data-stu-id="4d259-114">**Run jobs.**</span></span> <span data-ttu-id="4d259-115">Quando si tratta di dati di ora tooprocess hello, si esegue uno script di Windows PowerShell (o un'applicazione client) toocreate un cluster HDInsight, eseguire i processi ed eliminare il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="4d259-116">processi di Hello Salva dati di output tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="4d259-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="4d259-117">dati di output di Hello viene mantenuti anche dopo l'eliminazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="4d259-118">In questo modo, l'utente paga solo in base al consumo effettivo.</span><span class="sxs-lookup"><span data-stu-id="4d259-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="4d259-119">**Recuperare l'output di hello dall'archiviazione Blob di Azure**, o l'esportazione di database SQL di Azure di hello dati tooan in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="4d259-120">Hello seguente diagramma illustra uno scenario di hello e la struttura di hello di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="4d259-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="4d259-122">Si noti che hello numeri nel diagramma hello corrispondono toohello i titoli di sezione.</span><span class="sxs-lookup"><span data-stu-id="4d259-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="4d259-123">**M** è l'acronimo di processo principale hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-123">**M** stands for hello main process.</span></span> <span data-ttu-id="4d259-124">**Oggetto** è l'acronimo di contenuto hello nell'appendice hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="4d259-125">parte principale di Hello dell'esercitazione hello viene illustrato come toouse uno Windows PowerShell script tooperform hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="4d259-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="4d259-126">Creare un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d259-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="4d259-127">Eseguire un processo Hive in Media ritardi di hello cluster toocalculate aeroporti.</span><span class="sxs-lookup"><span data-stu-id="4d259-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="4d259-128">Hello flight delay vengono memorizzati in un account di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="4d259-129">Eseguire un Sqoop processo tooexport hello Hive processo output tooan database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="4d259-130">Eliminare il cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="4d259-131">Nelle appendici hello, è possibile trovare istruzioni hello per il caricamento di dati di ritardo di volo, la creazione o il caricamento di una stringa di query Hive e preparazione dei database SQL di Azure hello per processo Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="4d259-132">passaggi di Hello in questo documento sono cluster HDInsight basati su tooWindows specifici.</span><span class="sxs-lookup"><span data-stu-id="4d259-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="4d259-133">Per i passaggi relativi a un cluster basato su Linux, vedere [Analizzare i dati sui ritardi dei voli con Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4d259-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4d259-134">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4d259-134">Prerequisites</span></span>
<span data-ttu-id="4d259-135">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4d259-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="4d259-136">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d259-136">**An Azure subscription**.</span></span> <span data-ttu-id="4d259-137">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4d259-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4d259-138">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4d259-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4d259-139">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="4d259-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="4d259-140">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="4d259-141">Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d259-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="4d259-142">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="4d259-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="4d259-143">**File usati in questa esercitazione**</span><span class="sxs-lookup"><span data-stu-id="4d259-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="4d259-144">Questa esercitazione viene utilizzato hello in prestazioni dei dati di volo airline da [Research e amministrazione tecnologia innovativa, Bureau delle statistiche di trasporto o RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="4d259-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="4d259-145">Una copia di hello dati sono stati caricati tooan contenitore di archiviazione Blob di Azure con l'autorizzazione di accesso hello Blob pubblici.</span><span class="sxs-lookup"><span data-stu-id="4d259-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="4d259-146">Una parte dello script PowerShell copia i dati di hello dal contenitore di blob predefinito per la toohello contenitore hello blob pubblico del cluster.</span><span class="sxs-lookup"><span data-stu-id="4d259-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="4d259-147">Hello HiveQL lo script è inoltre copiati toohello nello stesso contenitore di Blob.</span><span class="sxs-lookup"><span data-stu-id="4d259-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="4d259-148">Se si desidera toolearn come tooget/carica hello dati tooyour proprietari di account di archiviazione e come toocreate/carica hello HiveQL lo script di file, vedere [appendice](#appendix-a) e [appendice B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="4d259-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="4d259-149">Hello nella tabella seguente sono elencati i file hello utilizzati in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="4d259-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="4d259-150">File</span><span class="sxs-lookup"><span data-stu-id="4d259-150">Files</span></span></th><th><span data-ttu-id="4d259-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4d259-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="4d259-152">file di script HiveQL Hello utilizzato hello processo Hive.</span><span class="sxs-lookup"><span data-stu-id="4d259-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="4d259-153">Questo script è stato caricato tooan account di archiviazione Blob di Azure con accesso pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="4d259-154"><a href="#appendix-b">Appendice B</a> include istruzioni sulla preparazione e sul caricamento di questo file tooyour un Blob di Azure account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="4d259-155">Dati di input per il processo Hive hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-155">Input data for hello Hive job.</span></span> <span data-ttu-id="4d259-156">dati Hello sono stato caricato tooan account di archiviazione Blob di Azure con accesso pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="4d259-157"><a href="#appendix-a">Appendice A</a> contiene istruzioni recupero di dati hello e il caricamento di hello dati tooyour un Blob di Azure account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="4d259-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="4d259-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="4d259-159">percorso di output di Hello per processo Hive hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="4d259-160">contenitore predefinito Hello viene utilizzato per archiviare i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="4d259-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="4d259-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="4d259-162">Hello Hive processo stato cartella contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="4d259-163">Creare cluster ed eseguire processi Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="4d259-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="4d259-164">Per Hadoop MapReduce è prevista l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="4d259-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="4d259-165">Hello toorun modo economico per la maggior parte un processo Hive è toocreate un cluster per il processo di hello ed eliminare il processo di hello dopo aver completato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="4d259-166">Hello script riportato di seguito vengono illustrate intero processo hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="4d259-167">Per altre informazioni sulla creazione di un cluster HDInsight e sull'esecuzione di processi Hive, vedere [Creare cluster Hadoop in HDInsight][hdinsight-provision] e [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="4d259-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="4d259-168">**query Hive di hello toorun da Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4d259-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="4d259-169">Creare una tabella di database e hello SQL di Azure per l'output del processo Sqoop hello usando istruzioni hello in [appendice C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="4d259-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="4d259-170">Aprire Windows PowerShell ISE ed eseguire lo script seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="4d259-171">La connessione a database SQL tooyour e vedere i ritardi dei voli Media in base alla città nella tabella AvgDelays hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="4d259-173"><a id="appendix-a"></a>Appendice A - caricamento volo ritardo dati tooAzure nell'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="4d259-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="4d259-174">Caricamento dei file di dati hello e i file di script HiveQL hello (vedere [appendice B](#appendix-b)) richiede una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="4d259-175">idea Hello è il file di dati di toostore hello e file HiveQL hello prima di creare un cluster HDInsight e in esecuzione il processo di Hive hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="4d259-176">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="4d259-176">You have two options:</span></span>

* <span data-ttu-id="4d259-177">**Utilizzare hello stesso account di archiviazione di Azure che verrà utilizzato dal cluster HDInsight hello come file system predefinito hello.**</span><span class="sxs-lookup"><span data-stu-id="4d259-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="4d259-178">Poiché il cluster HDInsight hello avrà una chiave di accesso di account di archiviazione hello, non è necessario toomake modifiche aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="4d259-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="4d259-179">**Utilizzare un account di archiviazione di Azure diverso dal file system predefinito del cluster di HDInsight hello.**</span><span class="sxs-lookup"><span data-stu-id="4d259-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="4d259-180">In caso di hello, è necessario modificare parte creazione hello di Windows PowerShell script trovato in hello [cluster HDInsight creare e esecuzione i processi Hive/Sqoop](#runjob) toolink hello account di archiviazione come un account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="4d259-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="4d259-181">Per istruzioni, vedere [Creare cluster Hadoop in HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="4d259-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="4d259-182">cluster HDInsight Hello in grado di conoscere la chiave di accesso hello per hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="4d259-183">percorso di archiviazione Blob Hello per file di dati è hard-coded in file di script HiveQL hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="4d259-184">È necessario aggiornarlo di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="4d259-184">You must update it accordingly.</span></span>

<span data-ttu-id="4d259-185">**dati di volo hello toodownload**</span><span class="sxs-lookup"><span data-stu-id="4d259-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="4d259-186">Sfoglia troppo[Research e innovativa tecnologia amministrazione Bureau di statistiche trasporto][rita-website].</span><span class="sxs-lookup"><span data-stu-id="4d259-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="4d259-187">Nella pagina hello selezionare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="4d259-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="4d259-188">Nome</span><span class="sxs-lookup"><span data-stu-id="4d259-188">Name</span></span></th><th><span data-ttu-id="4d259-189">Valore</span><span class="sxs-lookup"><span data-stu-id="4d259-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="4d259-190">Filter Year</span><span class="sxs-lookup"><span data-stu-id="4d259-190">Filter Year</span></span></td><td><span data-ttu-id="4d259-191">2013</span><span class="sxs-lookup"><span data-stu-id="4d259-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="4d259-192">Filter Period</span><span class="sxs-lookup"><span data-stu-id="4d259-192">Filter Period</span></span></td><td><span data-ttu-id="4d259-193">January</span><span class="sxs-lookup"><span data-stu-id="4d259-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-194">Fields</span><span class="sxs-lookup"><span data-stu-id="4d259-194">Fields</span></span></td><td><span data-ttu-id="4d259-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (deselezionare tutti gli altri campi)</span><span class="sxs-lookup"><span data-stu-id="4d259-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="4d259-196">
3. Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="4d259-196">
3. Click **Download**.</span></span>
<span data-ttu-id="4d259-197">4.</span><span class="sxs-lookup"><span data-stu-id="4d259-197">4.</span></span> <span data-ttu-id="4d259-198">Decomprimere hello file toohello **C:\Tutorials\FlightDelay\2013Data** cartella.</span><span class="sxs-lookup"><span data-stu-id="4d259-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="4d259-199">Ogni file è in formato CSV e ha dimensioni pari a circa 60 GB.</span><span class="sxs-lookup"><span data-stu-id="4d259-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="4d259-200">5.</span><span class="sxs-lookup"><span data-stu-id="4d259-200">5.</span></span> <span data-ttu-id="4d259-201">Rinominare hello file toohello del mese hello che contiene dati per.</span><span class="sxs-lookup"><span data-stu-id="4d259-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="4d259-202">Ad esempio, verrebbe denominato file hello contenente i dati di gennaio hello *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="4d259-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="4d259-203">6.</span><span class="sxs-lookup"><span data-stu-id="4d259-203">6.</span></span> <span data-ttu-id="4d259-204">Ripetere toodownload i passaggi 2 e 5 un file per ognuna delle hello in 2013 12 mesi.</span><span class="sxs-lookup"><span data-stu-id="4d259-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="4d259-205">È necessario un minimo di un'esercitazione di hello toorun file.</span><span class="sxs-lookup"><span data-stu-id="4d259-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="4d259-206">**tooupload hello volo ritardo dati tooAzure nell'archiviazione Blob**</span><span class="sxs-lookup"><span data-stu-id="4d259-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="4d259-207">Preparare i parametri di hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="4d259-208">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="4d259-208">Variable Name</span></span></th><th><span data-ttu-id="4d259-209">Note</span><span class="sxs-lookup"><span data-stu-id="4d259-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="4d259-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="4d259-210">$storageAccountName</span></span></td><td><span data-ttu-id="4d259-211">account di archiviazione di Azure in cui si desidera tooupload hello dati Hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="4d259-212">$blobContainerName</span></span></td><td><span data-ttu-id="4d259-213">contenitore Blob Hello in cui si desidera tooupload hello dati.</span><span class="sxs-lookup"><span data-stu-id="4d259-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="4d259-214">Aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="4d259-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="4d259-215">3.</span><span class="sxs-lookup"><span data-stu-id="4d259-215">3.</span></span> <span data-ttu-id="4d259-216">Incollare lo script seguente nel riquadro di script hello hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="4d259-217">Premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="4d259-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="4d259-218">Se si sceglie toouse un metodo diverso per il caricamento di file hello, verificare che il percorso di file hello è esercitazioni/flightdelay/data.</span><span class="sxs-lookup"><span data-stu-id="4d259-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="4d259-219">sintassi di Hello per accedere ai file hello è:</span><span class="sxs-lookup"><span data-stu-id="4d259-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="4d259-220">percorso esercitazioni/flightdelay/dati Hello è hello virtuale creata durante il caricamento di file hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="4d259-221">Verificare che siano disponibili 12 file, uno per ogni mese.</span><span class="sxs-lookup"><span data-stu-id="4d259-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="4d259-222">È necessario aggiornare hello Hive query tooread dalla nuova posizione hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="4d259-223">È necessario configurare hello contenitore accesso autorizzazione toobe pubblico o associare toohello account di archiviazione hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4d259-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="4d259-224">Stringa di query Hive hello in caso contrario, non sarà in grado di tooaccess i file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="4d259-225"><a id="appendix-b"></a>Appendice B: creare e caricare uno script HiveQL</span><span class="sxs-lookup"><span data-stu-id="4d259-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="4d259-226">Con Azure PowerShell, è possibile eseguire più istruzioni HiveQL uno alla volta oppure hello pacchetto HiveQL istruzione in un file di script.</span><span class="sxs-lookup"><span data-stu-id="4d259-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="4d259-227">In questa sezione viene illustrato come uno script HiveQL toocreate hello caricamento script e tooAzure nell'archiviazione Blob tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d259-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="4d259-228">Hive richiede hello HiveQL script toobe archiviati nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="4d259-229">Hello script HiveQL eseguirà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="4d259-230">**Elimina tabella delays_raw hello**, nel caso in cui hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="4d259-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="4d259-231">**Creare una tabella hello delays_raw esterna Hive** che punta il percorso di archiviazione Blob toohello con i file di ritardo di hello volo.</span><span class="sxs-lookup"><span data-stu-id="4d259-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="4d259-232">La query consente di specificare che i campi sono delimitati da "," e che le righe vengono interrotte da "\n".</span><span class="sxs-lookup"><span data-stu-id="4d259-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="4d259-233">Poiché questo comportamento pone un problema quando i valori di campo contengono virgole perché Hive non è possibile distinguere tra una virgola, che è un delimitatore di campo e uno che fa parte di un valore del campo (caso hello nei valori dei campi per l'origine\_Città\_nome e destinazione\_ Città\_nome).</span><span class="sxs-lookup"><span data-stu-id="4d259-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="4d259-234">tooaddress, hello query crea colonne TEMP toohold dati in modo non corretto sono suddiviso in colonne.</span><span class="sxs-lookup"><span data-stu-id="4d259-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="4d259-235">**Elimina tabella ritardi hello**, nel caso in cui hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="4d259-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="4d259-236">**Creare una tabella di ritardi hello**.</span><span class="sxs-lookup"><span data-stu-id="4d259-236">**Create hello delays table**.</span></span> <span data-ttu-id="4d259-237">È utile tooclean dei dati hello prima un'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="4d259-238">Questa query crea una nuova tabella, *ritardi*, dalla tabella delays_raw hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="4d259-239">Si noti che le colonne TEMP hello (come indicato in precedenza) non vengono copiate e che hello **sottostringa** funzione è virgolette tooremove utilizzato dai dati hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="4d259-240">**Calcolare hello weather medio ritardo e i gruppi hello risultati in base al nome di città.**</span><span class="sxs-lookup"><span data-stu-id="4d259-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="4d259-241">Verranno inoltre visualizzate le archiviazione tooBlob di hello risultati.</span><span class="sxs-lookup"><span data-stu-id="4d259-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="4d259-242">Si noti che eseguono query hello rimuoverà apostrofi dai dati hello ed escluderà le righe in cui il valore per hello **weather_delay** è null.</span><span class="sxs-lookup"><span data-stu-id="4d259-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="4d259-243">Ciò è necessario perché Sqoop, usato più avanti nell'esercitazione, non è in grado di gestire correttamente tali valori per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4d259-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="4d259-244">Per un elenco completo di comandi HiveQL hello, vedere [Hive Data Definition Language][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="4d259-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="4d259-245">Ogni comando HiveQL deve terminare con un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="4d259-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="4d259-246">**un file di script HiveQL toocreate**</span><span class="sxs-lookup"><span data-stu-id="4d259-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="4d259-247">Preparare i parametri di hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="4d259-248">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="4d259-248">Variable Name</span></span></th><th><span data-ttu-id="4d259-249">Note</span><span class="sxs-lookup"><span data-stu-id="4d259-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="4d259-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="4d259-250">$storageAccountName</span></span></td><td><span data-ttu-id="4d259-251">account di archiviazione di Azure in cui si desidera tooupload hello HiveQL script Hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="4d259-252">$blobContainerName</span></span></td><td><span data-ttu-id="4d259-253">contenitore Blob Hello in cui si desidera tooupload hello HiveQL script.</span><span class="sxs-lookup"><span data-stu-id="4d259-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="4d259-254">Aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="4d259-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="4d259-255">3.</span><span class="sxs-lookup"><span data-stu-id="4d259-255">3.</span></span> <span data-ttu-id="4d259-256">Copiare e incollare lo script seguente nel riquadro di script hello hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="4d259-257">Di seguito sono variabili hello utilizzate nello script hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="4d259-258">**$hqlLocalFileName** -hello script Salva file di script HiveQL hello localmente prima di caricarlo tooBlob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="4d259-259">Questo è il nome di file hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-259">This is hello file name.</span></span> <span data-ttu-id="4d259-260">valore predefinito di Hello è <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="4d259-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="4d259-261">**$hqlBlobName** -si tratta di hello HiveQL blob nome del file script utilizzato nell'archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="4d259-262">valore predefinito di Hello è tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="4d259-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="4d259-263">Poiché verrà scritto il file hello direttamente tooAzure nell'archiviazione Blob, non c'è un "/" all'inizio di hello del nome blob hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="4d259-264">Se si desidera tooaccess hello file dall'archiviazione Blob, è necessario tooadd un "/" all'inizio di hello del nome file hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="4d259-265">**$srcDataFolder** e **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="4d259-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="4d259-266"><a id="appendix-c"></a>Appendice C - preparare un database SQL di Azure per l'output del processo Sqoop hello</span><span class="sxs-lookup"><span data-stu-id="4d259-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="4d259-267">**database SQL di hello tooprepare (di tipo merge questo con hello Sqoop script)**</span><span class="sxs-lookup"><span data-stu-id="4d259-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="4d259-268">Preparare i parametri di hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="4d259-269">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="4d259-269">Variable Name</span></span></th><th><span data-ttu-id="4d259-270">Note</span><span class="sxs-lookup"><span data-stu-id="4d259-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="4d259-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="4d259-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="4d259-272">nome di Hello del server di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="4d259-273">Immettere nulla toocreate un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="4d259-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="4d259-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="4d259-275">nome dell'account Hello per server di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="4d259-276">Se $sqlDatabaseServerName è un server esistente, hello account e la password di account di accesso sono utilizzati tooauthenticate con server hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="4d259-277">In caso contrario sono toocreate utilizzato un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="4d259-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="4d259-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="4d259-279">password di accesso Hello per server di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="4d259-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="4d259-281">Questo valore viene usato solo durante la creazione di un nuovo server di database di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="4d259-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="4d259-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="4d259-283">database SQL Hello utilizzato nella tabella AvgDelays hello toocreate per processo Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="4d259-284">Lasciando il valore vuoto, verrà creato un database denominato "HDISqoop".</span><span class="sxs-lookup"><span data-stu-id="4d259-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="4d259-285">nome della tabella per l'output del processo Sqoop hello Hello è AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="4d259-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="4d259-286">Aprire Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="4d259-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="4d259-287">3.</span><span class="sxs-lookup"><span data-stu-id="4d259-287">3.</span></span> <span data-ttu-id="4d259-288">Copiare e incollare lo script seguente nel riquadro di script hello hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="4d259-289">Hello script Usa un servizio di stato representational transfer (REST), http://bot.whatismyipaddress.com, tooretrieve l'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="4d259-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="4d259-290">indirizzo IP di Hello viene utilizzato per la creazione di una regola del firewall per il server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="4d259-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="4d259-291">Ecco alcune variabili utilizzate nello script hello:</span><span class="sxs-lookup"><span data-stu-id="4d259-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="4d259-292">**$ipAddressRestService** -hello predefinita è http://bot.whatismyipaddress.com. È un servizio REST per l'indirizzo IP pubblico che consente di ottenere l'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="4d259-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="4d259-293">È anche possibile usare altri servizi.</span><span class="sxs-lookup"><span data-stu-id="4d259-293">You can use other services if you want.</span></span> <span data-ttu-id="4d259-294">indirizzo IP esterno Hello recuperato tramite il servizio hello sarà toocreate utilizzata una regola del firewall per il server di database SQL di Azure, in modo che è possibile accedere ai database hello dalla propria workstation (usando uno script di Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4d259-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="4d259-295">**$fireWallRuleName** -nome hello hello regola del firewall per server di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="4d259-296">nome predefinito Hello è <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="4d259-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="4d259-297">È anche possibile rinominarla.</span><span class="sxs-lookup"><span data-stu-id="4d259-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="4d259-298">**$sqlDatabaseMaxSizeGB** : questo valore viene usato solo durante la creazione di un nuovo server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="4d259-299">valore predefinito di Hello è 10GB.</span><span class="sxs-lookup"><span data-stu-id="4d259-299">hello default value is 10GB.</span></span> <span data-ttu-id="4d259-300">sufficiente per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4d259-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="4d259-301">**$sqlDatabaseName** : questo valore viene usato solo durante la creazione di un nuovo database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d259-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="4d259-302">valore predefinito di Hello è HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="4d259-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="4d259-303">Se si rinomina il, è necessario aggiornare di conseguenza script di Windows PowerShell di Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="4d259-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="4d259-304">Premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="4d259-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="4d259-305">Convalidare l'output di hello dello script.</span><span class="sxs-lookup"><span data-stu-id="4d259-305">Validate hello script output.</span></span> <span data-ttu-id="4d259-306">Verificare che lo script hello è stato eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="4d259-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="4d259-307"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d259-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="4d259-308">Dopo aver compreso come tooupload tooAzure un file nell'archiviazione Blob, come un Hive toopopulate tabella utilizzando i dati di hello dall'archiviazione Blob di Azure, come toorun Hive query e come toouse Sqoop tooexport dati dal database di SQL Azure tooan HDFS.</span><span class="sxs-lookup"><span data-stu-id="4d259-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="4d259-309">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="4d259-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="4d259-310">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4d259-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="4d259-311">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4d259-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4d259-312">[Usare Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="4d259-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="4d259-313">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="4d259-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="4d259-314">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4d259-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4d259-315">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4d259-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
