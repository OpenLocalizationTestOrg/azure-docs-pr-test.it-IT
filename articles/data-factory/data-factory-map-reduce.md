---
title: aaaInvoke programma MapReduce da Data Factory di Azure
description: Informazioni su come dati tooprocess eseguendo i programmi MapReduce in un Azure HDInsight cluster da una data factory di Azure.
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
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="1319b-103">Richiamare i programmi MapReduce da Data factory</span><span class="sxs-lookup"><span data-stu-id="1319b-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1319b-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="1319b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1319b-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="1319b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1319b-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="1319b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1319b-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="1319b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1319b-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="1319b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1319b-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1319b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1319b-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1319b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1319b-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="1319b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1319b-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1319b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1319b-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="1319b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1319b-114">attività MapReduce di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue i programmi MapReduce in [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="1319b-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1319b-115">In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="1319b-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="1319b-116">Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1319b-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="1319b-117">Introduzione</span><span class="sxs-lookup"><span data-stu-id="1319b-117">Introduction</span></span>
<span data-ttu-id="1319b-118">Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati.</span><span class="sxs-lookup"><span data-stu-id="1319b-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="1319b-119">Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="1319b-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="1319b-120">In questo articolo viene descritto l'utilizzo di hello attività MapReduce di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1319b-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="1319b-121">Vedere [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) per informazioni dettagliate sull'esecuzione di script Pig/Hive in un cluster HDInsight basato su Windows/Linux da una pipeline usando le attività Pig e Hive di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1319b-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="1319b-122">JSON per attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="1319b-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="1319b-123">Nella definizione JSON per hello attività HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="1319b-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="1319b-124">Set hello **tipo** di hello **attività** troppo**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1319b-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="1319b-125">Specificare il nome di hello classe hello per **className** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1319b-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="1319b-126">Specificare i file JAR di hello percorso toohello tra nome file hello **jarFilePath** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1319b-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="1319b-127">Specificare il servizio di hello collegato che fa riferimento toohello archiviazione Blob di Azure che contiene i file JAR hello per **jarLinkedService** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1319b-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="1319b-128">Specificare gli argomenti per il programma MapReduce hello in hello **argomenti** sezione.</span><span class="sxs-lookup"><span data-stu-id="1319b-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="1319b-129">In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="1319b-130">toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni).</span><span class="sxs-lookup"><span data-stu-id="1319b-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
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
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="1319b-131">È possibile utilizzare hello attività MapReduce di HDInsight toorun qualsiasi file jar MapReduce in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1319b-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="1319b-132">In hello definizione JSON di esempio seguente di una pipeline, hello attività HDInsight è configurata in un file JAR Mahout toorun.</span><span class="sxs-lookup"><span data-stu-id="1319b-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="1319b-133">Esempio in GitHub</span><span class="sxs-lookup"><span data-stu-id="1319b-133">Sample on GitHub</span></span>
<span data-ttu-id="1319b-134">È possibile scaricare un esempio per l'utilizzo di hello attività MapReduce di HDInsight da: [Data Factory esempi su GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="1319b-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="1319b-135">Eseguire il programma di conteggio parole hello</span><span class="sxs-lookup"><span data-stu-id="1319b-135">Running hello Word Count program</span></span>
<span data-ttu-id="1319b-136">pipeline Hello in questo esempio viene eseguito il programma MapReduce Conteggio parole hello il cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="1319b-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="1319b-137">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="1319b-137">Linked Services</span></span>
<span data-ttu-id="1319b-138">Creare innanzitutto un hello toolink servizio collegato di archiviazione Azure utilizzato da hello Azure HDInsight cluster toohello data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="1319b-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="1319b-139">Se si copia e Incolla hello seguente di codice, non dimenticare tooreplace **nome account** e **chiave dell'account** con nome hello e la chiave di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="1319b-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="1319b-140">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1319b-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="1319b-141">Servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1319b-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="1319b-142">Successivamente, si crea un servizio collegato di toolink Azure HDInsight cluster toohello data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="1319b-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="1319b-143">Se si copia e Incolla hello di codice seguente, sostituire **nome del cluster HDInsight** con nome hello del cluster HDInsight e modifica nome utente e password specificati.</span><span class="sxs-lookup"><span data-stu-id="1319b-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="1319b-144">DATASETS</span><span class="sxs-lookup"><span data-stu-id="1319b-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="1319b-145">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="1319b-145">Output dataset</span></span>
<span data-ttu-id="1319b-146">pipeline Hello in questo esempio non accetta alcun input.</span><span class="sxs-lookup"><span data-stu-id="1319b-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="1319b-147">Specificare un set di dati di output di hello attività MapReduce di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1319b-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="1319b-148">Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1319b-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="1319b-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="1319b-149">Pipeline</span></span>
<span data-ttu-id="1319b-150">pipeline di Hello in questo esempio include una sola attività che è di tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="1319b-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="1319b-151">Alcune delle proprietà importanti di hello in hello JSON sono:</span><span class="sxs-lookup"><span data-stu-id="1319b-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="1319b-152">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1319b-152">Property</span></span> | <span data-ttu-id="1319b-153">Note</span><span class="sxs-lookup"><span data-stu-id="1319b-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="1319b-154">type</span><span class="sxs-lookup"><span data-stu-id="1319b-154">type</span></span> |<span data-ttu-id="1319b-155">è necessario impostare il tipo di Hello troppo**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="1319b-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="1319b-156">className</span><span class="sxs-lookup"><span data-stu-id="1319b-156">className</span></span> |<span data-ttu-id="1319b-157">Nome della classe hello è: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="1319b-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="1319b-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="1319b-158">jarFilePath</span></span> |<span data-ttu-id="1319b-159">Percorso file jar toohello contenente la classe hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="1319b-160">Se si copia e Incolla hello seguente di codice, non dimenticare nome hello toochange del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="1319b-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="1319b-161">jarLinkedService</span></span> |<span data-ttu-id="1319b-162">Servizio collegato di archiviazione Azure che contiene i file jar hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="1319b-163">Il servizio collegato fa riferimento toohello spazio di archiviazione associato al cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="1319b-164">arguments</span><span class="sxs-lookup"><span data-stu-id="1319b-164">arguments</span></span> |<span data-ttu-id="1319b-165">programma wordcount Hello accetta due argomenti, un input e output.</span><span class="sxs-lookup"><span data-stu-id="1319b-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="1319b-166">file di input Hello è davinci.txt hello.</span><span class="sxs-lookup"><span data-stu-id="1319b-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="1319b-167">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="1319b-167">frequency/interval</span></span> |<span data-ttu-id="1319b-168">Hello per queste proprietà corrispondono hello output set di dati.</span><span class="sxs-lookup"><span data-stu-id="1319b-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="1319b-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1319b-169">linkedServiceName</span></span> |<span data-ttu-id="1319b-170">fa riferimento a servizio collegato di HDInsight toohello è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1319b-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="1319b-171">Esecuzione dei programmi Spark</span><span class="sxs-lookup"><span data-stu-id="1319b-171">Run Spark programs</span></span>
<span data-ttu-id="1319b-172">È possibile utilizzare i programmi MapReduce attività toorun Spark il cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1319b-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="1319b-173">Per i dettagli, vedere [Chiamare i programmi Spark da Azure Data Factory](data-factory-spark.md) .</span><span class="sxs-lookup"><span data-stu-id="1319b-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="1319b-174">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1319b-174">See Also</span></span>
* [<span data-ttu-id="1319b-175">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="1319b-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="1319b-176">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="1319b-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="1319b-177">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="1319b-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="1319b-178">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="1319b-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="1319b-179">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="1319b-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

