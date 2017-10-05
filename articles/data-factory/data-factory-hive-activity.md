---
title: "Trasformare dati usando l'attività Hive - Azure | Documentazione Microsoft"
description: "Informazioni su come usare l'attività Hive in una data factory di Azure per eseguire query Hive in un cluster HDInsight su richiesta o nel proprio cluster HDInsight."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="5ec36-103">Trasformare dati usando l'attività Hive in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5ec36-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5ec36-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="5ec36-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5ec36-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="5ec36-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5ec36-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="5ec36-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5ec36-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="5ec36-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5ec36-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="5ec36-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5ec36-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5ec36-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5ec36-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5ec36-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5ec36-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="5ec36-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5ec36-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5ec36-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5ec36-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="5ec36-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5ec36-114">L'attività Hive di HDInsight in una [pipeline](data-factory-create-pipelines.md) di Data Factory esegue query Hive sul [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) cluster HDInsight o sul cluster HDInsight [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) basato su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="5ec36-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5ec36-115">Questo articolo si basa sull'articolo relativo alle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) che presenta una panoramica generale della trasformazione dei dati e le attività di trasformazione supportate.</span><span class="sxs-lookup"><span data-stu-id="5ec36-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ec36-116">Se non si ha familiarità con Azure Data Factory, prima di leggere questo articolo leggere [Introduzione ad Azure Data Factory](data-factory-introduction.md) ed eseguire l'esercitazione [Creare la prima pipeline di dati](data-factory-build-your-first-pipeline.md) .</span><span class="sxs-lookup"><span data-stu-id="5ec36-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="5ec36-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="5ec36-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="5ec36-118">Dettagli sintassi</span><span class="sxs-lookup"><span data-stu-id="5ec36-118">Syntax details</span></span>
| <span data-ttu-id="5ec36-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5ec36-119">Property</span></span> | <span data-ttu-id="5ec36-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ec36-120">Description</span></span> | <span data-ttu-id="5ec36-121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5ec36-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ec36-122">name</span><span class="sxs-lookup"><span data-stu-id="5ec36-122">name</span></span> |<span data-ttu-id="5ec36-123">Nome dell'attività</span><span class="sxs-lookup"><span data-stu-id="5ec36-123">Name of the activity</span></span> |<span data-ttu-id="5ec36-124">Sì</span><span class="sxs-lookup"><span data-stu-id="5ec36-124">Yes</span></span> |
| <span data-ttu-id="5ec36-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ec36-125">description</span></span> |<span data-ttu-id="5ec36-126">Testo descrittivo per lo scopo dell'attività</span><span class="sxs-lookup"><span data-stu-id="5ec36-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="5ec36-127">No</span><span class="sxs-lookup"><span data-stu-id="5ec36-127">No</span></span> |
| <span data-ttu-id="5ec36-128">type</span><span class="sxs-lookup"><span data-stu-id="5ec36-128">type</span></span> |<span data-ttu-id="5ec36-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="5ec36-129">HDinsightHive</span></span> |<span data-ttu-id="5ec36-130">Sì</span><span class="sxs-lookup"><span data-stu-id="5ec36-130">Yes</span></span> |
| <span data-ttu-id="5ec36-131">inputs</span><span class="sxs-lookup"><span data-stu-id="5ec36-131">inputs</span></span> |<span data-ttu-id="5ec36-132">Input utilizzati dall'attività Hive</span><span class="sxs-lookup"><span data-stu-id="5ec36-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="5ec36-133">No</span><span class="sxs-lookup"><span data-stu-id="5ec36-133">No</span></span> |
| <span data-ttu-id="5ec36-134">outputs</span><span class="sxs-lookup"><span data-stu-id="5ec36-134">outputs</span></span> |<span data-ttu-id="5ec36-135">Output generati dall'attività Hive</span><span class="sxs-lookup"><span data-stu-id="5ec36-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="5ec36-136">Sì</span><span class="sxs-lookup"><span data-stu-id="5ec36-136">Yes</span></span> |
| <span data-ttu-id="5ec36-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5ec36-137">linkedServiceName</span></span> |<span data-ttu-id="5ec36-138">Riferimento al cluster HDInsight registrato come servizio collegato in Data factory</span><span class="sxs-lookup"><span data-stu-id="5ec36-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="5ec36-139">Sì</span><span class="sxs-lookup"><span data-stu-id="5ec36-139">Yes</span></span> |
| <span data-ttu-id="5ec36-140">script</span><span class="sxs-lookup"><span data-stu-id="5ec36-140">script</span></span> |<span data-ttu-id="5ec36-141">Specificare lo script Hive inline</span><span class="sxs-lookup"><span data-stu-id="5ec36-141">Specify the Hive script inline</span></span> |<span data-ttu-id="5ec36-142">No</span><span class="sxs-lookup"><span data-stu-id="5ec36-142">No</span></span> |
| <span data-ttu-id="5ec36-143">script path</span><span class="sxs-lookup"><span data-stu-id="5ec36-143">script path</span></span> |<span data-ttu-id="5ec36-144">Archiviare lo script Hive in un archivio BLOB di Azure e immettere il percorso del file.</span><span class="sxs-lookup"><span data-stu-id="5ec36-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="5ec36-145">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="5ec36-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="5ec36-146">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="5ec36-146">Both cannot be used together.</span></span> <span data-ttu-id="5ec36-147">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="5ec36-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="5ec36-148">No</span><span class="sxs-lookup"><span data-stu-id="5ec36-148">No</span></span> |
| <span data-ttu-id="5ec36-149">defines</span><span class="sxs-lookup"><span data-stu-id="5ec36-149">defines</span></span> |<span data-ttu-id="5ec36-150">Specificare i parametri come coppie chiave/valore per fare riferimento ad essi nello script Hive usando "hiveconf"</span><span class="sxs-lookup"><span data-stu-id="5ec36-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="5ec36-151">No</span><span class="sxs-lookup"><span data-stu-id="5ec36-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="5ec36-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ec36-152">Example</span></span>
<span data-ttu-id="5ec36-153">Si prenda ad esempio l'analisi di log di giochi, in cui si desidera verificare il tempo che gli utenti hanno dedicato a giocare alle partite avviate dalla società.</span><span class="sxs-lookup"><span data-stu-id="5ec36-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="5ec36-154">Il log seguente è un log di esempio di un gioco in cui i valori sono separati da virgola (`,`) e che contiene i campi ProfileID, SessionStart, Duration, SrcIPAddress e GameType.</span><span class="sxs-lookup"><span data-stu-id="5ec36-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="5ec36-155">Lo **script Hive** per elaborare tali dati sarà:</span><span class="sxs-lookup"><span data-stu-id="5ec36-155">The **Hive script** to process this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="5ec36-156">Per eseguire lo script Hive in una pipeline di Data factory, è necessario seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5ec36-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="5ec36-157">Creare un servizio collegato per registrare [il proprio cluster di elaborazione di HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) oppure configurare [un cluster di elaborazione di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="5ec36-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="5ec36-158">In questo esempio il servizio collegato è denominato "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="5ec36-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="5ec36-159">Creare un [servizio collegato](data-factory-azure-blob-connector.md) per configurare la connessione all'archivio BLOB di Azure che ospita i dati.</span><span class="sxs-lookup"><span data-stu-id="5ec36-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="5ec36-160">In questo esempio il servizio collegato è denominato "StorageLinkedService".</span><span class="sxs-lookup"><span data-stu-id="5ec36-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="5ec36-161">Creare [set di dati](data-factory-create-datasets.md) che puntano ai dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="5ec36-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="5ec36-162">In questo esempio il set di dati di input è denominato "HiveSampleIn", mentre il set di dati di output è denominato "HiveSampleOut".</span><span class="sxs-lookup"><span data-stu-id="5ec36-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="5ec36-163">Copiare la query Hive come file nell'archivio BLOB di Azure configurato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="5ec36-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="5ec36-164">Se la risorsa di archiviazione che deve ospitare i dati è diverso da quello che ospita il file di query, creare un altro servizio collegato di Archiviazione di Azure e fare riferimento a quest'ultimo nell'attività.</span><span class="sxs-lookup"><span data-stu-id="5ec36-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="5ec36-165">Usare **scriptPath ** per specificare il percorso del file di query Hive e **scriptLinkedService** per specificare la risorsa di archiviazione di Azure contenente il file di script.</span><span class="sxs-lookup"><span data-stu-id="5ec36-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5ec36-166">È anche possibile fornire lo script Hive inline nella definizione dell'attività tramite la proprietà **script** .</span><span class="sxs-lookup"><span data-stu-id="5ec36-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="5ec36-167">Si sconsiglia tuttavia questo approccio perché è necessario eseguire l'escape di tutti i caratteri speciali dello script nel documento JSON, con possibili problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="5ec36-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="5ec36-168">Si consiglia di seguire il passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="5ec36-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="5ec36-169">Creare la pipeline riportata con l'attività HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="5ec36-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="5ec36-170">L'attività elabora/trasforma i dati.</span><span class="sxs-lookup"><span data-stu-id="5ec36-170">The activity processes/transforms the data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="5ec36-171">Distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="5ec36-171">Deploy the pipeline.</span></span> <span data-ttu-id="5ec36-172">Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="5ec36-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="5ec36-173">Monitorare la pipeline mediante le viste di monitoraggio e gestione delle pipeline di Data factory.</span><span class="sxs-lookup"><span data-stu-id="5ec36-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="5ec36-174">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="5ec36-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="5ec36-175">Specifica dei parametri per uno script Hive</span><span class="sxs-lookup"><span data-stu-id="5ec36-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="5ec36-176">In questo esempio i log di giochi vengono inseriti giornalmente nel sistema di archiviazione BLOB di Azure e memorizzati in una cartella partizionata con data e ora.</span><span class="sxs-lookup"><span data-stu-id="5ec36-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="5ec36-177">Si desidera impostare i parametri per lo script Hive e passare il percorso della cartella di input in modo dinamico durante il runtime, generando l'output partizionato con data e ora.</span><span class="sxs-lookup"><span data-stu-id="5ec36-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="5ec36-178">Per usare lo script con parametri Hive, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5ec36-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="5ec36-179">Definire i parametri in **defines**.</span><span class="sxs-lookup"><span data-stu-id="5ec36-179">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="5ec36-180">Nello script Hive fare riferimento al parametro tramite **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="5ec36-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="5ec36-181">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ec36-181">See Also</span></span>
* [<span data-ttu-id="5ec36-182">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="5ec36-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="5ec36-183">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="5ec36-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="5ec36-184">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="5ec36-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="5ec36-185">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="5ec36-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="5ec36-186">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="5ec36-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

