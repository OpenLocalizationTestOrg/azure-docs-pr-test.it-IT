---
title: Richiamare il programma MapReduce da Data factory di Azure
description: Informazioni su come elaborare i dati eseguendo programmi MapReduce in un cluster Azure HDInsight da un'istanza di Data factory di Azure.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="328f4-103">Richiamare i programmi MapReduce da Data factory</span><span class="sxs-lookup"><span data-stu-id="328f4-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="328f4-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="328f4-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="328f4-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="328f4-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="328f4-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="328f4-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="328f4-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="328f4-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="328f4-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="328f4-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="328f4-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="328f4-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="328f4-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="328f4-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="328f4-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="328f4-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="328f4-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="328f4-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="328f4-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="328f4-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="328f4-114">L'attività HDInsight MapReduce in una [pipeline](data-factory-create-pipelines.md) di Data Factory esegue i programmi di MapReduce nei cluster HDInsight [personalizzati](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) basati su Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="328f4-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="328f4-115">Questo articolo si basa sull'articolo relativo alle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) che presenta una panoramica generale della trasformazione dei dati e le attività di trasformazione supportate.</span><span class="sxs-lookup"><span data-stu-id="328f4-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="328f4-116">Se non si ha familiarità con Azure Data Factory, prima di leggere questo articolo leggere [Introduzione ad Azure Data Factory](data-factory-introduction.md) ed eseguire l'esercitazione [Creare la prima pipeline di dati](data-factory-build-your-first-pipeline.md) .</span><span class="sxs-lookup"><span data-stu-id="328f4-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="328f4-117">Introduzione</span><span class="sxs-lookup"><span data-stu-id="328f4-117">Introduction</span></span>
<span data-ttu-id="328f4-118">Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati.</span><span class="sxs-lookup"><span data-stu-id="328f4-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="328f4-119">Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="328f4-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="328f4-120">In questo articolo viene descritto l'utilizzo dell'attività MapReduce di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="328f4-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="328f4-121">Vedere [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) per informazioni dettagliate sull'esecuzione di script Pig/Hive in un cluster HDInsight basato su Windows/Linux da una pipeline usando le attività Pig e Hive di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="328f4-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="328f4-122">JSON per attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="328f4-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="328f4-123">Nella definizione JSON per l'attività HDInsight:</span><span class="sxs-lookup"><span data-stu-id="328f4-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="328f4-124">Impostare l'oggetto **type** di **activity** su **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="328f4-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="328f4-125">Specificare il nome della classe per la proprietà **className** .</span><span class="sxs-lookup"><span data-stu-id="328f4-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="328f4-126">Specificare il percorso del file JAR, incluso il nome di file per la proprietà **jarFilePath** .</span><span class="sxs-lookup"><span data-stu-id="328f4-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="328f4-127">Specificare il servizio collegato che fa riferimento all'archivio BLOB di Azure contenente il file JAR per la proprietà **jarLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="328f4-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="328f4-128">Specificare gli eventuali argomenti per il programma MapReduce nella sezione **arguments** .</span><span class="sxs-lookup"><span data-stu-id="328f4-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="328f4-129">In fase di esecuzione, vengono visualizzati alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="328f4-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="328f4-130">Per differenziare gli argomenti con gli argomenti di MapReduce, è consigliabile usare sia l'opzione che il valore come argomenti, come illustrato nell'esempio seguente (- s, --input - output e così via sono opzioni immediatamente seguite dai valori).</span><span class="sxs-lookup"><span data-stu-id="328f4-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="328f4-131">È possibile usare l’attività MapReduce di HDInsight per l'esecuzione di file JAR di MapReduce in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="328f4-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="328f4-132">Nella definizione JSON seguente di una pipeline di esempio l'attività HDInsight è configurata per eseguire un file JAR di Mahout.</span><span class="sxs-lookup"><span data-stu-id="328f4-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="328f4-133">Esempio in GitHub</span><span class="sxs-lookup"><span data-stu-id="328f4-133">Sample on GitHub</span></span>
<span data-ttu-id="328f4-134">È possibile scaricare un esempio relativo all'uso dell'attività MapReduce di HDInsight da: [esempi di Data factory in GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="328f4-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="328f4-135">Esecuzione del programma di conteggio delle parole</span><span class="sxs-lookup"><span data-stu-id="328f4-135">Running the Word Count program</span></span>
<span data-ttu-id="328f4-136">La pipeline in questo esempio esegue il programma di mapping e riduzione del conteggio delle parole sul cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="328f4-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="328f4-137">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="328f4-137">Linked Services</span></span>
<span data-ttu-id="328f4-138">In primo luogo, si crea un servizio collegato per collegare l'archiviazione di Azure utilizzata dal cluster HDInsight di Azure per la factory di dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="328f4-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="328f4-139">Se si copia e incolla il codice seguente, non dimenticare di sostituire il **nome account** e la **chiave account** con il nome e la chiave di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="328f4-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="328f4-140">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="328f4-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="328f4-141">Servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="328f4-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="328f4-142">Successivamente, si crea un servizio collegato per collegare il cluster HDInsight di Azure alla factory di dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="328f4-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="328f4-143">Se si copia e incolla il codice seguente, sostituire **nome del cluster HDInsight** con il nome del cluster HDInsight e modificare i valori nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="328f4-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="328f4-144">Set di dati</span><span class="sxs-lookup"><span data-stu-id="328f4-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="328f4-145">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="328f4-145">Output dataset</span></span>
<span data-ttu-id="328f4-146">La pipeline in questo esempio non accetta alcun input.</span><span class="sxs-lookup"><span data-stu-id="328f4-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="328f4-147">Specificare un set di dati di output per l'attività MapReduce di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="328f4-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="328f4-148">Questo è solo un set di dati fittizio necessario per la pianificazione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="328f4-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="328f4-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="328f4-149">Pipeline</span></span>
<span data-ttu-id="328f4-150">La pipeline in questo esempio contiene una sola attività che è di tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="328f4-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="328f4-151">Alcune delle proprietà importanti in JSON sono:</span><span class="sxs-lookup"><span data-stu-id="328f4-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="328f4-152">Proprietà</span><span class="sxs-lookup"><span data-stu-id="328f4-152">Property</span></span> | <span data-ttu-id="328f4-153">Note</span><span class="sxs-lookup"><span data-stu-id="328f4-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="328f4-154">type</span><span class="sxs-lookup"><span data-stu-id="328f4-154">type</span></span> |<span data-ttu-id="328f4-155">Il tipo deve essere impostato su **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="328f4-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="328f4-156">className</span><span class="sxs-lookup"><span data-stu-id="328f4-156">className</span></span> |<span data-ttu-id="328f4-157">Il nome della classe è: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="328f4-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="328f4-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="328f4-158">jarFilePath</span></span> |<span data-ttu-id="328f4-159">Percorso del file jar contenente la classe.</span><span class="sxs-lookup"><span data-stu-id="328f4-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="328f4-160">Se si copia e incolla il codice seguente, non dimenticare di modificare il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="328f4-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="328f4-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="328f4-161">jarLinkedService</span></span> |<span data-ttu-id="328f4-162">Servizio collegato di Archiviazione di Azure che contiene il file jar.</span><span class="sxs-lookup"><span data-stu-id="328f4-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="328f4-163">Questo servizio collegato fa riferimento allo spazio di archiviazione associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="328f4-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="328f4-164">arguments</span><span class="sxs-lookup"><span data-stu-id="328f4-164">arguments</span></span> |<span data-ttu-id="328f4-165">Il programma wordcount accetta due argomenti, un input e un output.</span><span class="sxs-lookup"><span data-stu-id="328f4-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="328f4-166">Il file di input è il file davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="328f4-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="328f4-167">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="328f4-167">frequency/interval</span></span> |<span data-ttu-id="328f4-168">I valori per queste proprietà corrispondono al set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="328f4-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="328f4-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="328f4-169">linkedServiceName</span></span> |<span data-ttu-id="328f4-170">fa riferimento al servizio collegato di HDInsight creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="328f4-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="328f4-171">Esecuzione dei programmi Spark</span><span class="sxs-lookup"><span data-stu-id="328f4-171">Run Spark programs</span></span>
<span data-ttu-id="328f4-172">È possibile usare l'attività MapReduce per eseguire i programmi Spark nel cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="328f4-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="328f4-173">Per i dettagli, vedere [Chiamare i programmi Spark da Azure Data Factory](data-factory-spark.md) .</span><span class="sxs-lookup"><span data-stu-id="328f4-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="328f4-174">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="328f4-174">See Also</span></span>
* [<span data-ttu-id="328f4-175">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="328f4-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="328f4-176">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="328f4-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="328f4-177">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="328f4-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="328f4-178">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="328f4-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="328f4-179">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="328f4-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

