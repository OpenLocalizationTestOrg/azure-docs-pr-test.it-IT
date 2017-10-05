---
title: "Caricare grandi quantità in Data Lake Store usando i metodi offline | Documentazione Microsoft"
description: Usare lo strumento AdlCopy per copiare i dati da BLOB di Archiviazione di Azure a Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="0c8a4-103">Usare il servizio Importazione/Esportazione di Microsoft Azure per la copia offline dei dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="0c8a4-104">Questo articolo contiene informazioni su come copiare set di dati di grandi dimensioni (> 200 GB) in Azure Data Lake Store usando metodi di copia offline, ad esempio il [servizio Importazione/Esportazione di Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="0c8a4-105">In particolare, il file usato come esempio in questo articolo ha una dimensione di 339.420.860.416 byte, vale a dire circa 319 GB sul disco.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="0c8a4-106">Chiameremo questo file 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="0c8a4-107">Il servizio Importazione/Esportazione di Azure consente di trasferire in modo sicuro grandi quantità di dati nell'archiviazione BLOB di Azure attraverso la spedizione delle unità disco rigido a un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c8a4-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c8a4-108">Prerequisites</span></span>
<span data-ttu-id="0c8a4-109">Per eseguire le procedure descritte è necessario:</span><span class="sxs-lookup"><span data-stu-id="0c8a4-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="0c8a4-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-110">**An Azure subscription**.</span></span> <span data-ttu-id="0c8a4-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0c8a4-112">**Un account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="0c8a4-113">**Un account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="0c8a4-114">Per istruzioni su come crearne uno, vedere [Introduzione ad Archivio Data Lake di Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0c8a4-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="0c8a4-115">Preparazione dei dati</span><span class="sxs-lookup"><span data-stu-id="0c8a4-115">Preparing the data</span></span>
<span data-ttu-id="0c8a4-116">Prima di usare il servizio di importazione/esportazione, è necessario suddividere il file di dati da trasferire **in copie di dimensioni inferiori a 200 GB**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="0c8a4-117">Lo strumento di importazione non funziona con file di dimensioni superiori a 200 GB.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="0c8a4-118">In questa esercitazione il file viene suddiviso in blocchi di 100 GB.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="0c8a4-119">A tale scopo è possibile usare [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="0c8a4-120">Cygwin supporta i comandi di Linux.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="0c8a4-121">In questo caso usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0c8a4-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="0c8a4-122">L'operazione di suddivisione crea file con i nomi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="0c8a4-123">Preparare i dischi con i dati</span><span class="sxs-lookup"><span data-stu-id="0c8a4-123">Get disks ready with data</span></span>
<span data-ttu-id="0c8a4-124">Per preparare le unità disco rigido, seguire le istruzioni in [Usare il servizio Importazione/Esportazione di Azure](../storage/common/storage-import-export-service.md), sezione **Preparare le unità**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="0c8a4-125">Di seguito è riportata la sequenza generale:</span><span class="sxs-lookup"><span data-stu-id="0c8a4-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="0c8a4-126">Procurarsi un disco rigido che soddisfi i requisiti per l'uso con il servizio di Importazione/Esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="0c8a4-127">Identificare un account di archiviazione di Azure in cui verranno copiati i dati dopo la spedizione al data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="0c8a4-128">Usare lo [strumento di importazione/esportazione di Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="0c8a4-129">Di seguito è riportato un frammento di codice di esempio che indica come usare lo strumento.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="0c8a4-130">Per altri frammenti di codice di esempio, vedere [Usare il servizio Importazione/Esportazione di Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="0c8a4-131">Il comando precedente crea un file journal nel percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="0c8a4-132">Usare questo file journal per creare un processo di importazione dal [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="0c8a4-133">Creare un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="0c8a4-133">Create an import job</span></span>
<span data-ttu-id="0c8a4-134">È ora possibile creare un processo di importazione usando le istruzioni in [Usare il servizio Importazione/Esportazione di Azure](../storage/common/storage-import-export-service.md), sezione **Creare il processo di importazione**.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="0c8a4-135">Per questo processo di importazione fornire, oltre ad altri dettagli, anche il file journal creato durante la preparazione delle unità disco.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="0c8a4-136">Spedire fisicamente i dischi</span><span class="sxs-lookup"><span data-stu-id="0c8a4-136">Physically ship the disks</span></span>
<span data-ttu-id="0c8a4-137">A questo punto è possibile spedire fisicamente i dischi a un data center di Azure,</span><span class="sxs-lookup"><span data-stu-id="0c8a4-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="0c8a4-138">dove i dati verranno copiati nei BLOB di Archiviazione di Azure specificato durante la creazione del processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="0c8a4-139">Inoltre, se durante la creazione del processo si è scelto di inserire le informazioni di rilevamento in un secondo momento, è possibile tornare al processo di importazione e aggiornare il numero di tracciabilità.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="0c8a4-140">Copiare i dati dai BLOB di Archiviazione di Azure in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="0c8a4-141">Completato il processo di importazione, è possibile verificare se i dati sono disponibili nei BLOB di Archiviazione di Azure specificati.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="0c8a4-142">È quindi possibile usare diversi metodi per trasferire i dati dai BLOB ad Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="0c8a4-143">Per tutte le opzioni disponibili per il caricamento di dati, vedere [Inserire i dati in Archivio Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="0c8a4-144">In questa sezione sono riportate le definizioni JSON che è possibile usare per creare una pipeline di Azure Data Factory per la copia dei dati.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="0c8a4-145">È possibile usare queste definizioni JSON dal [portale di Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="0c8a4-146">Servizio collegato all'origine (BLOB di Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0c8a4-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="0c8a4-147">Servizio collegato alla destinazione (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="0c8a4-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="0c8a4-148">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="0c8a4-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="0c8a4-149">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="0c8a4-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="0c8a4-150">Pipeline (attività di copia)</span><span class="sxs-lookup"><span data-stu-id="0c8a4-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="0c8a4-151">Per altre informazioni, vedere l'articolo sullo [spostamento dei dati dal BLOB di Archiviazione di Azure ad Azure Data Lake Store con Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="0c8a4-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="0c8a4-152">Ricostruire i file di dati in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="0c8a4-153">Il file originale da 319 GB è stato suddiviso in file di dimensioni minori, in modo che possano essere trasferiti usando il servizio di Importazione/Esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="0c8a4-154">Ora che i dati sono in Azure Data Lake Store, è possibile riportare il file alla dimensione originale.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="0c8a4-155">A tale scopo, è possibile usare i cmdlet di Azure PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="0c8a4-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="0c8a4-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c8a4-156">Next steps</span></span>
* [<span data-ttu-id="0c8a4-157">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0c8a4-158">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0c8a4-159">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0c8a4-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
