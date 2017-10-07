---
title: "aaaTransform dati utilizzando l'attività Hive - Azure | Documenti Microsoft"
description: "Informazioni su come è possibile utilizzare attività Hive di hello in una query Hive di Azure data factory toorun in un cluster di HDInsight su richiesta o il proprio."
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
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="7d46c-103">Trasformare dati usando l'attività Hive in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7d46c-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="7d46c-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="7d46c-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="7d46c-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="7d46c-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="7d46c-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="7d46c-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="7d46c-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="7d46c-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="7d46c-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="7d46c-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="7d46c-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7d46c-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="7d46c-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7d46c-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="7d46c-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="7d46c-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="7d46c-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7d46c-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="7d46c-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="7d46c-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="7d46c-114">attività Hive di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue query Hive nel [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="7d46c-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7d46c-115">In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="7d46c-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="7d46c-116">Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7d46c-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="7d46c-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7d46c-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="7d46c-118">Dettagli sintassi</span><span class="sxs-lookup"><span data-stu-id="7d46c-118">Syntax details</span></span>
| <span data-ttu-id="7d46c-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7d46c-119">Property</span></span> | <span data-ttu-id="7d46c-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7d46c-120">Description</span></span> | <span data-ttu-id="7d46c-121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7d46c-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d46c-122">name</span><span class="sxs-lookup"><span data-stu-id="7d46c-122">name</span></span> |<span data-ttu-id="7d46c-123">Nome dell'attività hello</span><span class="sxs-lookup"><span data-stu-id="7d46c-123">Name of hello activity</span></span> |<span data-ttu-id="7d46c-124">Sì</span><span class="sxs-lookup"><span data-stu-id="7d46c-124">Yes</span></span> |
| <span data-ttu-id="7d46c-125">description</span><span class="sxs-lookup"><span data-stu-id="7d46c-125">description</span></span> |<span data-ttu-id="7d46c-126">Testo che descrive le attività di hello viene utilizzato per</span><span class="sxs-lookup"><span data-stu-id="7d46c-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="7d46c-127">No</span><span class="sxs-lookup"><span data-stu-id="7d46c-127">No</span></span> |
| <span data-ttu-id="7d46c-128">type</span><span class="sxs-lookup"><span data-stu-id="7d46c-128">type</span></span> |<span data-ttu-id="7d46c-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="7d46c-129">HDinsightHive</span></span> |<span data-ttu-id="7d46c-130">Sì</span><span class="sxs-lookup"><span data-stu-id="7d46c-130">Yes</span></span> |
| <span data-ttu-id="7d46c-131">inputs</span><span class="sxs-lookup"><span data-stu-id="7d46c-131">inputs</span></span> |<span data-ttu-id="7d46c-132">Input utilizzato dall'attività Hive hello</span><span class="sxs-lookup"><span data-stu-id="7d46c-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="7d46c-133">No</span><span class="sxs-lookup"><span data-stu-id="7d46c-133">No</span></span> |
| <span data-ttu-id="7d46c-134">outputs</span><span class="sxs-lookup"><span data-stu-id="7d46c-134">outputs</span></span> |<span data-ttu-id="7d46c-135">Output generato dall'attività Hive hello</span><span class="sxs-lookup"><span data-stu-id="7d46c-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="7d46c-136">Sì</span><span class="sxs-lookup"><span data-stu-id="7d46c-136">Yes</span></span> |
| <span data-ttu-id="7d46c-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7d46c-137">linkedServiceName</span></span> |<span data-ttu-id="7d46c-138">Cluster di HDInsight toohello riferimento registrato come un servizio collegato in Data Factory</span><span class="sxs-lookup"><span data-stu-id="7d46c-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="7d46c-139">Sì</span><span class="sxs-lookup"><span data-stu-id="7d46c-139">Yes</span></span> |
| <span data-ttu-id="7d46c-140">script</span><span class="sxs-lookup"><span data-stu-id="7d46c-140">script</span></span> |<span data-ttu-id="7d46c-141">Specificare hello Hive script inline</span><span class="sxs-lookup"><span data-stu-id="7d46c-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="7d46c-142">No</span><span class="sxs-lookup"><span data-stu-id="7d46c-142">No</span></span> |
| <span data-ttu-id="7d46c-143">script path</span><span class="sxs-lookup"><span data-stu-id="7d46c-143">script path</span></span> |<span data-ttu-id="7d46c-144">Hello archivio Hive script in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file.</span><span class="sxs-lookup"><span data-stu-id="7d46c-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="7d46c-145">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="7d46c-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="7d46c-146">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="7d46c-146">Both cannot be used together.</span></span> <span data-ttu-id="7d46c-147">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="7d46c-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="7d46c-148">No</span><span class="sxs-lookup"><span data-stu-id="7d46c-148">No</span></span> |
| <span data-ttu-id="7d46c-149">defines</span><span class="sxs-lookup"><span data-stu-id="7d46c-149">defines</span></span> |<span data-ttu-id="7d46c-150">Specificare i parametri come coppie chiave/valore per il riferimento all'interno dello script Hive hello utilizzando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="7d46c-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="7d46c-151">No</span><span class="sxs-lookup"><span data-stu-id="7d46c-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="7d46c-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="7d46c-152">Example</span></span>
<span data-ttu-id="7d46c-153">Si consideri un esempio di gioco registra analitica in cui si desidera ora hello tooidentify impiegato dagli utenti giochi avviata dall'azienda.</span><span class="sxs-lookup"><span data-stu-id="7d46c-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="7d46c-154">Hello log seguente è riportato un esempio gioco log, che è la virgola (`,`) separati e contiene i seguenti campi: ProfileID, SessionStart, durata, SrcIPAddress e GameType hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="7d46c-155">Hello **lo script Hive** tooprocess dati:</span><span class="sxs-lookup"><span data-stu-id="7d46c-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="7d46c-156">tooexecute script Hive in una pipeline di Data Factory, è necessario seguente hello toodo</span><span class="sxs-lookup"><span data-stu-id="7d46c-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="7d46c-157">Creare un servizio collegato di tooregister [HDInsight un cluster di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurare [cluster di calcolo di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="7d46c-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="7d46c-158">In questo esempio il servizio collegato è denominato "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="7d46c-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="7d46c-159">Creare un [servizio collegato](data-factory-azure-blob-connector.md) tooconfigure hello connessione tooAzure nell'archiviazione Blob hello dati di hosting.</span><span class="sxs-lookup"><span data-stu-id="7d46c-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="7d46c-160">In questo esempio il servizio collegato è denominato "StorageLinkedService".</span><span class="sxs-lookup"><span data-stu-id="7d46c-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="7d46c-161">Creare [set di dati](data-factory-create-datasets.md) rivolte verso l'input toohello e hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="7d46c-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="7d46c-162">È ora possibile chiamare set di dati input hello "HiveSampleIn" e set di dati di output "HiveSampleOut" hello</span><span class="sxs-lookup"><span data-stu-id="7d46c-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="7d46c-163">Copia query Hive hello come tooAzure un file di archiviazione Blob configurato nel passaggio &#2;.</span><span class="sxs-lookup"><span data-stu-id="7d46c-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="7d46c-164">Se l'archiviazione hello per ospitare i dati hello è diverso da hello uno che ospita il file di query, creare un servizio collegato di archiviazione di Azure separato e fa riferimento tooit nell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="7d46c-165">Utilizzare * * scriptPath * * file di query toohive percorso toospecify hello e **scriptLinkedService** toospecify hello archiviazione di Azure che contiene i file di script hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7d46c-166">È inoltre possibile fornire hello Hive script inline nella definizione di attività hello hello **script** proprietà.</span><span class="sxs-lookup"><span data-stu-id="7d46c-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="7d46c-167">Questo approccio non è consigliato come tutti i caratteri speciali in script hello all'interno di documenti JSON hello deve toobe caratteri di escape e può causa problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="7d46c-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="7d46c-168">procedura consigliata Hello è toofollow passaggio #4.</span><span class="sxs-lookup"><span data-stu-id="7d46c-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="7d46c-169">Creare una pipeline con attività HDInsightHive hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="7d46c-170">attività Hello processi/trasformazioni dati hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="7d46c-171">Distribuire la pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7d46c-171">Deploy hello pipeline.</span></span> <span data-ttu-id="7d46c-172">Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="7d46c-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="7d46c-173">Monitorare le pipeline hello tramite il monitoraggio di hello data factory e le viste a gestione.</span><span class="sxs-lookup"><span data-stu-id="7d46c-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="7d46c-174">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="7d46c-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="7d46c-175">Specifica dei parametri per uno script Hive</span><span class="sxs-lookup"><span data-stu-id="7d46c-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="7d46c-176">In questo esempio i log di giochi vengono inseriti giornalmente nel sistema di archiviazione BLOB di Azure e memorizzati in una cartella partizionata con data e ora.</span><span class="sxs-lookup"><span data-stu-id="7d46c-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="7d46c-177">Si desidera tooparameterize hello Hive script e passare il percorso di cartella di input di hello in modo dinamico in fase di esecuzione e anche produrre output di hello partizionato con data e ora.</span><span class="sxs-lookup"><span data-stu-id="7d46c-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="7d46c-178">toouse script Hive con parametri, procedere come segue hello</span><span class="sxs-lookup"><span data-stu-id="7d46c-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="7d46c-179">Definire i parametri di hello in **definisce**.</span><span class="sxs-lookup"><span data-stu-id="7d46c-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="7d46c-180">Fare riferimento in hello Script Hive, toohello parametro utilizzando **${hiveconf: ParameterName}**.</span><span class="sxs-lookup"><span data-stu-id="7d46c-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="7d46c-181">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7d46c-181">See Also</span></span>
* [<span data-ttu-id="7d46c-182">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="7d46c-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="7d46c-183">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="7d46c-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="7d46c-184">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="7d46c-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="7d46c-185">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="7d46c-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="7d46c-186">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="7d46c-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

