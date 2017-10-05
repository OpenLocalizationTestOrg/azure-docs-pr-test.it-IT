---
title: "Trasformare dati usando l'attività di streaming di Hadoop - Azure | Documentazione Microsoft"
description: "Informazioni su come usare l'attività di Hadoop Streaming in una Data factory di Azure per trasformare i dati eseguendo i programmi di Hadoop Streaming in un cluster HDInsight personalizzato o su richiesta."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="66f62-103">Trasformare dati usando l'attività di streaming di Hadoop in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="66f62-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="66f62-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="66f62-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="66f62-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="66f62-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="66f62-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="66f62-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="66f62-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="66f62-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="66f62-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="66f62-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="66f62-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="66f62-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="66f62-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="66f62-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="66f62-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="66f62-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="66f62-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="66f62-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="66f62-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="66f62-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="66f62-114">È possibile usare l'attività HDInsightStreamingActivity per richiamare un processo di Hadoop Streaming da una pipeline di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f62-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="66f62-115">Il frammento JSON seguente illustra la sintassi per l'uso di HDInsightStreamingActivity in un file JSON della pipeline.</span><span class="sxs-lookup"><span data-stu-id="66f62-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="66f62-116">L'attività HDInsight Streaming Activity in una [pipeline](data-factory-create-pipelines.md) di Data Factory esegue i programmi di Hadoop Streaming nei cluster HDInsight [personalizzati](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) basati su Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="66f62-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="66f62-117">Questo articolo si basa sull'articolo relativo alle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) che presenta una panoramica generale della trasformazione dei dati e le attività di trasformazione supportate.</span><span class="sxs-lookup"><span data-stu-id="66f62-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="66f62-118">Se non si ha familiarità con Azure Data Factory, leggere l'[Introduzione ad Azure Data Factory](data-factory-introduction.md) ed eseguire l'esercitazione: [Creare la prima pipeline di dati](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="66f62-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="66f62-119">Esempio JSON</span><span class="sxs-lookup"><span data-stu-id="66f62-119">JSON sample</span></span>
<span data-ttu-id="66f62-120">Il cluster HDInsight viene popolato automaticamente con programmi di esempio (wc.exe e cat.exe) e con i dati (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="66f62-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="66f62-121">Per impostazione predefinita, il nome del contenitore che viene utilizzato dal cluster HDInsight è il nome del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="66f62-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="66f62-122">Ad esempio, se il nome del cluster è myhdicluster, il nome del contenitore BLOB associato sarebbe myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="66f62-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="66f62-123">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="66f62-123">Note the following points:</span></span>

1. <span data-ttu-id="66f62-124">Impostare **linkedServiceName** sul nome del servizio collegato che punta al cluster HDInsight in cui viene eseguito il processo di streaming mapreduce.</span><span class="sxs-lookup"><span data-stu-id="66f62-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="66f62-125">Impostare il tipo di attività su **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="66f62-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="66f62-126">Per la proprietà **mapper** specificare il nome dell'eseguibile del mapper.</span><span class="sxs-lookup"><span data-stu-id="66f62-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="66f62-127">Nell'esempio cat.exe è l'eseguibile del mapper.</span><span class="sxs-lookup"><span data-stu-id="66f62-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="66f62-128">Per la proprietà **reducer** specificare il nome dell'eseguibile del reducer.</span><span class="sxs-lookup"><span data-stu-id="66f62-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="66f62-129">Nell'esempio wc.exe è l'eseguibile del mapper.</span><span class="sxs-lookup"><span data-stu-id="66f62-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="66f62-130">Per la proprietà di tipo **input** specificare il file di input (incluso il percorso) per il mapper.</span><span class="sxs-lookup"><span data-stu-id="66f62-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="66f62-131">Nell'esempio "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt" adfsample è il contenitore BLOB, example/data/Gutenberg è la cartella e davinci.txt è il BLOB.</span><span class="sxs-lookup"><span data-stu-id="66f62-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="66f62-132">Per la proprietà di tipo **output** specificare il file di output (incluso il percorso) per il reducer.</span><span class="sxs-lookup"><span data-stu-id="66f62-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="66f62-133">L'output del processo di Hadoop Streaming viene scritto nel percorso specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="66f62-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="66f62-134">Nella sezione **filePaths** specificare i percorsi dei file eseguibili del mapper e del reducer.</span><span class="sxs-lookup"><span data-stu-id="66f62-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="66f62-135">Nell'esempio: "adfsample/example/apps/wc.exe", adfsample è il contenitore BLOB, example/apps è la cartella e wc.exe è l'eseguibile.</span><span class="sxs-lookup"><span data-stu-id="66f62-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="66f62-136">Per la proprietà **fileLinkedService** specificare il servizio collegato Archiviazione di Azure che rappresenta l'archivio di Azure contenente i file specificati nella sezione filePaths.</span><span class="sxs-lookup"><span data-stu-id="66f62-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="66f62-137">Per la proprietà **arguments** specificare gli argomenti per il processo di streaming.</span><span class="sxs-lookup"><span data-stu-id="66f62-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="66f62-138">La proprietà **getDebugInfo** è un elemento facoltativo.</span><span class="sxs-lookup"><span data-stu-id="66f62-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="66f62-139">Quando viene impostata su Failure, i log vengono scaricati solo in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="66f62-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="66f62-140">Quando viene impostata su Always, i log vengono sempre scaricati indipendentemente dallo stato dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="66f62-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="66f62-141">Come illustrato nell'esempio, è necessario specificare un set di dati di output per l'attività di Hadoop Streaming per la proprietà **output** .</span><span class="sxs-lookup"><span data-stu-id="66f62-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="66f62-142">Questo è solo un set di dati fittizio necessario per la pianificazione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="66f62-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="66f62-143">Non è necessario specificare alcun set di dati di input per l'attività per la proprietà **input** .</span><span class="sxs-lookup"><span data-stu-id="66f62-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="66f62-144">Esempio</span><span class="sxs-lookup"><span data-stu-id="66f62-144">Example</span></span>
<span data-ttu-id="66f62-145">La pipeline in questa procedura dettagliata esegue il programma di mapping e riduzione dello streaming del conteggio delle parole sul cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f62-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="66f62-146">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="66f62-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="66f62-147">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="66f62-147">Azure Storage linked service</span></span>
<span data-ttu-id="66f62-148">In primo luogo, si crea un servizio collegato per collegare l'archiviazione di Azure utilizzata dal cluster HDInsight di Azure per la factory di dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f62-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="66f62-149">Se si copia e incolla il codice seguente, non dimenticare di sostituire il nome account e la chiave account con il nome e la chiave di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f62-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="66f62-150">Servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="66f62-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="66f62-151">Successivamente, si crea un servizio collegato per collegare il cluster HDInsight di Azure alla factory di dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f62-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="66f62-152">Se si copia e incolla il codice seguente, sostituire il nome del cluster HDInsight con il nome del cluster HDInsight e modificare i valori nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="66f62-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="66f62-153">Set di dati</span><span class="sxs-lookup"><span data-stu-id="66f62-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="66f62-154">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="66f62-154">Output dataset</span></span>
<span data-ttu-id="66f62-155">La pipeline in questo esempio non accetta alcun input.</span><span class="sxs-lookup"><span data-stu-id="66f62-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="66f62-156">È necessario specificare un set di dati di output per l'attività Streaming di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66f62-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="66f62-157">Questo è solo un set di dati fittizio necessario per la pianificazione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="66f62-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="66f62-158">Pipeline</span><span class="sxs-lookup"><span data-stu-id="66f62-158">Pipeline</span></span>
<span data-ttu-id="66f62-159">La pipeline in questo esempio contiene una sola attività che è di tipo: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="66f62-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="66f62-160">Il cluster HDInsight viene popolato automaticamente con programmi di esempio (wc.exe e cat.exe) e con i dati (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="66f62-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="66f62-161">Per impostazione predefinita, il nome del contenitore che viene utilizzato dal cluster HDInsight è il nome del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="66f62-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="66f62-162">Ad esempio, se il nome del cluster è myhdicluster, il nome del contenitore BLOB associato sarebbe myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="66f62-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="66f62-163">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="66f62-163">See Also</span></span>
* [<span data-ttu-id="66f62-164">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="66f62-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="66f62-165">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="66f62-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="66f62-166">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="66f62-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="66f62-167">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="66f62-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="66f62-168">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="66f62-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

