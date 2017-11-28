---
title: "dati aaaTransform utilizzando Hadoop Streaming attività - Azure | Documenti Microsoft"
description: "Informazioni su come utilizzare possibile hello attività di Streaming di Hadoop in un Azure factory tootransform dati tramite l'esecuzione di programmi Hadoop Streaming in un cluster di HDInsight su richiesta o il personalizzati."
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
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="dd8ce-103">Trasformare dati usando l'attività di streaming di Hadoop in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="dd8ce-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="dd8ce-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="dd8ce-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="dd8ce-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="dd8ce-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="dd8ce-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="dd8ce-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="dd8ce-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="dd8ce-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="dd8ce-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="dd8ce-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="dd8ce-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="dd8ce-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="dd8ce-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="dd8ce-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="dd8ce-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="dd8ce-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="dd8ce-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="dd8ce-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="dd8ce-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="dd8ce-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="dd8ce-114">È possibile utilizzare attività HDInsightStreamingActivity hello richiamare un processo Hadoop Streaming da una pipeline di Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="dd8ce-115">Hello frammento di codice JSON seguente mostra la sintassi hello per l'utilizzo di hello HDInsightStreamingActivity in un file JSON di pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="dd8ce-116">Attività Streaming di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue i programmi di Streaming di Hadoop nel [la propria](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight basati su Windows/Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dd8ce-117">In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="dd8ce-118">Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="dd8ce-119">Esempio JSON</span><span class="sxs-lookup"><span data-stu-id="dd8ce-119">JSON sample</span></span>
<span data-ttu-id="dd8ce-120">cluster HDInsight Hello viene popolato automaticamente con i programmi di esempio (wc.exe e cat.exe) e i dati (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="dd8ce-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="dd8ce-121">Per impostazione predefinita, nome del contenitore di hello utilizzato dal cluster HDInsight hello è il nome di hello del cluster di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="dd8ce-122">Ad esempio, se il nome del cluster è myhdicluster, nome del contenitore blob hello associata sarebbe myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="dd8ce-123">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="dd8ce-123">Note hello following points:</span></span>

1. <span data-ttu-id="dd8ce-124">Set hello **linkedServiceName** toohello nome hello collegato del servizio che fa riferimento il cluster di HDInsight tooyour su quali hello streaming mapreduce processo viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="dd8ce-125">Impostare il tipo di hello dell'attività hello troppo**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="dd8ce-126">Per hello **mapper** proprietà, specificare il nome di hello del mapper eseguibile.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="dd8ce-127">Nell'esempio hello cat.exe è mapper hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="dd8ce-128">Per hello **riduttore** proprietà, specificare il nome di hello del file eseguibile del reducer.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="dd8ce-129">Nell'esempio hello wc.exe è file eseguibile del reducer hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="dd8ce-130">Per hello **input** digitare proprietà, specificare i file di input hello (incluso il percorso di hello) per il mapper hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="dd8ce-131">Nell'esempio hello: "//adfsample @<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample è il contenitore di blob hello, esempio/data/Gutenberg è la cartella hello e davinci.txt è blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="dd8ce-132">Per hello **output** digitare proprietà, specificare i file di output di hello (incluso il percorso di hello) per riduttore hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="dd8ce-133">output di Hello del processo Hadoop Streaming hello viene scritto toohello percorso specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="dd8ce-134">In hello **filePaths** sezione, specificare i percorsi per gli eseguibili del mapper e del reducer hello hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="dd8ce-135">Nell'esempio hello: "adfsample/example/apps/wc.exe", adfsample è il contenitore di blob hello, example/apps è la cartella hello e wc.exe è hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="dd8ce-136">Per hello **fileLinkedService** proprietà, specificare l'archiviazione di Azure che rappresenta il servizio collegato archiviazione di Azure che contiene file hello specificati nella sezione filePaths hello di hello hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="dd8ce-137">Per hello **argomenti** proprietà, specificare gli argomenti di hello per hello processo di streaming.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="dd8ce-138">Hello **getDebugInfo** proprietà è un elemento facoltativo.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="dd8ce-139">Quando si imposta tooFailure, hello registri vengono scaricati solo in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="dd8ce-140">Quando si imposta tooAlways, i log vengono sempre scaricati indipendentemente lo stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="dd8ce-141">Come illustrato nell'esempio hello, specificare un set di dati di output di hello attività di Streaming di Hadoop per hello **restituisce** proprietà.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="dd8ce-142">Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="dd8ce-143">Non è necessario toospecify qualsiasi set di dati di input per l'attività hello per hello **input** proprietà.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="dd8ce-144">Esempio</span><span class="sxs-lookup"><span data-stu-id="dd8ce-144">Example</span></span>
<span data-ttu-id="dd8ce-145">pipeline Hello in questa procedura dettagliata viene eseguito il programma MapReduce streaming di hello Conteggio parole il cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="dd8ce-146">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="dd8ce-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="dd8ce-147">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dd8ce-147">Azure Storage linked service</span></span>
<span data-ttu-id="dd8ce-148">Creare innanzitutto un hello toolink servizio collegato di archiviazione Azure utilizzato da hello Azure HDInsight cluster toohello data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="dd8ce-149">Se si copia e Incolla hello seguente di codice, non dimenticare tooreplace account nome account e la chiave con nome hello e dello spazio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="dd8ce-150">Servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd8ce-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="dd8ce-151">Successivamente, si crea un servizio collegato di toolink Azure HDInsight cluster toohello data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="dd8ce-152">Se si copia e Incolla hello seguente di codice, sostituire il nome del cluster HDInsight con nome hello del cluster HDInsight e modificare i valori di nome e una password utente.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="dd8ce-153">DATASETS</span><span class="sxs-lookup"><span data-stu-id="dd8ce-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="dd8ce-154">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="dd8ce-154">Output dataset</span></span>
<span data-ttu-id="dd8ce-155">pipeline Hello in questo esempio non accetta alcun input.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="dd8ce-156">Specificare un set di dati di output di hello attività Streaming di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="dd8ce-157">Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="dd8ce-158">Pipeline</span><span class="sxs-lookup"><span data-stu-id="dd8ce-158">Pipeline</span></span>
<span data-ttu-id="dd8ce-159">pipeline di Hello in questo esempio include una sola attività che è di tipo: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="dd8ce-160">cluster HDInsight Hello viene popolato automaticamente con i programmi di esempio (wc.exe e cat.exe) e i dati (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="dd8ce-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="dd8ce-161">Per impostazione predefinita, nome del contenitore di hello utilizzato dal cluster HDInsight hello è il nome di hello del cluster di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="dd8ce-162">Ad esempio, se il nome del cluster è myhdicluster, nome del contenitore blob hello associata sarebbe myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="dd8ce-163">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dd8ce-163">See Also</span></span>
* [<span data-ttu-id="dd8ce-164">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="dd8ce-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="dd8ce-165">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="dd8ce-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="dd8ce-166">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="dd8ce-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="dd8ce-167">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="dd8ce-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="dd8ce-168">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="dd8ce-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

