---
title: aaaUpload elevati di dati in archivio Data Lake tramite metodi offline | Documenti Microsoft
description: TooData Lake archivio BLOB di hello utilizzare dati di toocopy AdlCopy dello strumento da archiviazione di Azure
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
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="9bc2e-103">Utilizzare il servizio di importazione/esportazione di Azure hello per copia offline di archivio data Lake di tooData</span><span class="sxs-lookup"><span data-stu-id="9bc2e-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="9bc2e-104">In questo articolo si apprenderà come set di dati di grandi dimensioni toocopy (> 200 GB) in un archivio Azure Data Lake utilizzando metodi di copia non in linea, ad esempio hello [servizio di importazione/esportazione di Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="9bc2e-105">In particolare, file hello utilizzato come un esempio in questo articolo è 339,420,860,416 byte, ovvero circa 319 GB su disco.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="9bc2e-106">Chiameremo questo file 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="9bc2e-107">Hello servizio importazione/esportazione di Azure consente di tootransfer grandi quantità di dati in modo sicuro nell'archiviazione Blob da disco rigido shipping tooAzure unità tooan Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bc2e-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9bc2e-108">Prerequisites</span></span>
<span data-ttu-id="9bc2e-109">Prima di iniziare, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="9bc2e-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-110">**An Azure subscription**.</span></span> <span data-ttu-id="9bc2e-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9bc2e-112">**Un account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="9bc2e-113">**Un account Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="9bc2e-114">Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="9bc2e-115">Preparazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="9bc2e-115">Preparing hello data</span></span>
<span data-ttu-id="9bc2e-116">Prima di utilizzare il servizio di importazione/esportazione di hello, trasferiti interruzione hello dati file toobe **in copie di meno di 200 GB** dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="9bc2e-117">lo strumento di importazione Hello non funziona con i file di dimensioni superiori a 200 GB.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="9bc2e-118">In questa esercitazione verranno suddivise file hello in blocchi di 100 GB.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="9bc2e-119">A tale scopo è possibile usare [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="9bc2e-120">Cygwin supporta i comandi di Linux.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="9bc2e-121">In questo caso, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="9bc2e-122">operazione di divisione Hello crea file con i seguenti nomi hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="9bc2e-123">Preparare i dischi con i dati</span><span class="sxs-lookup"><span data-stu-id="9bc2e-123">Get disks ready with data</span></span>
<span data-ttu-id="9bc2e-124">Seguire le istruzioni hello [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) (in hello **preparare le unità** sezione) tooprepare le unità disco rigido.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="9bc2e-125">Ecco hello sequenza generale:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="9bc2e-126">Ottenere un disco rigido che soddisfa hello requisito toobe utilizzato per il servizio di importazione/esportazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="9bc2e-127">Identificare un account di archiviazione di Azure in cui verranno copiati i dati di hello dopo essere stato spedito toohello Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="9bc2e-128">Hello utilizzare [strumento di importazione/esportazione di Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="9bc2e-129">Di seguito è riportato un frammento di esempio che illustra come toouse hello dello strumento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="9bc2e-130">Vedere [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) per più frammenti di codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="9bc2e-131">Hello comando precedente crea una registrazione di file hello percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="9bc2e-132">Utilizzare questo toocreate file journal un processo di importazione da hello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="9bc2e-133">Creare un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="9bc2e-133">Create an import job</span></span>
<span data-ttu-id="9bc2e-134">È ora possibile creare un processo di importazione utilizzando le istruzioni hello [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) (in hello **Crea processo di importazione hello** sezione).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="9bc2e-135">Per questo processo di importazione, con altri dettagli, fornire anche file journal hello creato durante la preparazione delle unità disco hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="9bc2e-136">Fisicamente spedire i dischi di hello</span><span class="sxs-lookup"><span data-stu-id="9bc2e-136">Physically ship hello disks</span></span>
<span data-ttu-id="9bc2e-137">È ora possibile fornire fisicamente hello dischi tooan Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="9bc2e-138">Dati hello non esiste, viene copiati sui blob di archiviazione di Azure toohello che immessa durante la creazione del processo di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="9bc2e-139">Inoltre, durante la creazione del processo di hello, se si è scelto di hello tooprovide in un secondo momento, le informazioni di rilevamento è ora possibile passare nuovamente tooyour importazione processo e aggiornamento hello numero di tracciabilità.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="9bc2e-140">Copiare i dati dall'archivio Data Lake di archiviazione di Azure BLOB tooAzure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="9bc2e-141">Dopo lo stato di hello di hello processo di importazione mostra che viene completato il processo, è possibile verificare se i dati di hello sono disponibili nei blob di archiviazione di Azure hello che è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="9bc2e-142">È quindi possibile utilizzare un'ampia gamma di metodi toomove che i dati da hello BLOB archivio tooAzure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="9bc2e-143">Per tutti hello opzioni disponibili per il caricamento dei dati, vedere [l'inserimento di dati in archivio Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="9bc2e-144">In questa sezione si forniscono le definizioni di hello JSON che è possibile utilizzare toocreate una pipeline di Data Factory di Azure per la copia dei dati.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="9bc2e-145">È possibile utilizzare queste definizioni JSON da hello [portale di Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="9bc2e-146">Servizio collegato all'origine (BLOB di Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="9bc2e-147">Servizio collegato alla destinazione (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="9bc2e-148">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="9bc2e-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="9bc2e-149">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="9bc2e-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="9bc2e-150">Pipeline (attività di copia)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="9bc2e-151">Per ulteriori informazioni, vedere [spostare dati da archiviazione di Azure blob usando Azure Data Factory di archivio Data Lake tooAzure](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="9bc2e-152">Ricostruire il file di dati hello in archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9bc2e-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="9bc2e-153">Siamo partiti da un file che era 319 GB e si è interrotta, verso il basso nei file di dimensioni minori in modo che possono essere trasferito tramite il servizio di importazione/esportazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="9bc2e-154">Dopo avere dati hello archivio Azure Data Lake, è possibile ricostruire dimensioni originali tooits di file hello.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="9bc2e-155">È possibile utilizzare hello seguente così toodo cmldts Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="9bc2e-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bc2e-156">Next steps</span></span>
* [<span data-ttu-id="9bc2e-157">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9bc2e-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="9bc2e-158">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9bc2e-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="9bc2e-159">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9bc2e-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
