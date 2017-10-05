---
title: "Trasformare dati usando l'attività Pig in Azure Data Factory | Documentazione Microsoft"
description: "Informazioni su come usare l'attività Pig in una data factory di Azure per eseguire query Pig in un cluster HDInsight su richiesta o nel proprio cluster HDInsight."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="16726-103">Trasformare dati usando l'attività Pig in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="16726-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="16726-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="16726-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="16726-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="16726-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="16726-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="16726-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="16726-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="16726-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="16726-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="16726-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="16726-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="16726-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="16726-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="16726-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="16726-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="16726-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="16726-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="16726-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="16726-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="16726-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="16726-114">L'attività Pig di HDInsight in una [pipeline](data-factory-create-pipelines.md) di Data factory esegue query Pig sul cluster HDInsight [dell'utente](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o sul cluster HDInsight [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) basato su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="16726-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="16726-115">Questo articolo si basa sull'articolo relativo alle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) che presenta una panoramica generale della trasformazione dei dati e le attività di trasformazione supportate.</span><span class="sxs-lookup"><span data-stu-id="16726-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="16726-116">Se non si ha familiarità con Azure Data Factory, prima di leggere questo articolo leggere [Introduzione ad Azure Data Factory](data-factory-introduction.md) ed eseguire l'esercitazione [Creare la prima pipeline di dati](data-factory-build-your-first-pipeline.md) .</span><span class="sxs-lookup"><span data-stu-id="16726-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="16726-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="16726-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="16726-118">Dettagli sintassi</span><span class="sxs-lookup"><span data-stu-id="16726-118">Syntax details</span></span>
| <span data-ttu-id="16726-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="16726-119">Property</span></span> | <span data-ttu-id="16726-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16726-120">Description</span></span> | <span data-ttu-id="16726-121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16726-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16726-122">name</span><span class="sxs-lookup"><span data-stu-id="16726-122">name</span></span> |<span data-ttu-id="16726-123">Nome dell'attività</span><span class="sxs-lookup"><span data-stu-id="16726-123">Name of the activity</span></span> |<span data-ttu-id="16726-124">Sì</span><span class="sxs-lookup"><span data-stu-id="16726-124">Yes</span></span> |
| <span data-ttu-id="16726-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16726-125">description</span></span> |<span data-ttu-id="16726-126">Testo descrittivo per lo scopo dell'attività</span><span class="sxs-lookup"><span data-stu-id="16726-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="16726-127">No</span><span class="sxs-lookup"><span data-stu-id="16726-127">No</span></span> |
| <span data-ttu-id="16726-128">type</span><span class="sxs-lookup"><span data-stu-id="16726-128">type</span></span> |<span data-ttu-id="16726-129">HDInsightPig</span><span class="sxs-lookup"><span data-stu-id="16726-129">HDinsightPig</span></span> |<span data-ttu-id="16726-130">Sì</span><span class="sxs-lookup"><span data-stu-id="16726-130">Yes</span></span> |
| <span data-ttu-id="16726-131">inputs</span><span class="sxs-lookup"><span data-stu-id="16726-131">inputs</span></span> |<span data-ttu-id="16726-132">Uno o più input usati dall'attività Pig</span><span class="sxs-lookup"><span data-stu-id="16726-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="16726-133">No</span><span class="sxs-lookup"><span data-stu-id="16726-133">No</span></span> |
| <span data-ttu-id="16726-134">outputs</span><span class="sxs-lookup"><span data-stu-id="16726-134">outputs</span></span> |<span data-ttu-id="16726-135">Uno o più input prodotti dall'attività Pig</span><span class="sxs-lookup"><span data-stu-id="16726-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="16726-136">Sì</span><span class="sxs-lookup"><span data-stu-id="16726-136">Yes</span></span> |
| <span data-ttu-id="16726-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="16726-137">linkedServiceName</span></span> |<span data-ttu-id="16726-138">Riferimento al cluster HDInsight registrato come servizio collegato in Data factory</span><span class="sxs-lookup"><span data-stu-id="16726-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="16726-139">Sì</span><span class="sxs-lookup"><span data-stu-id="16726-139">Yes</span></span> |
| <span data-ttu-id="16726-140">script</span><span class="sxs-lookup"><span data-stu-id="16726-140">script</span></span> |<span data-ttu-id="16726-141">Specificare lo script Pig inline</span><span class="sxs-lookup"><span data-stu-id="16726-141">Specify the Pig script inline</span></span> |<span data-ttu-id="16726-142">No</span><span class="sxs-lookup"><span data-stu-id="16726-142">No</span></span> |
| <span data-ttu-id="16726-143">script path</span><span class="sxs-lookup"><span data-stu-id="16726-143">script path</span></span> |<span data-ttu-id="16726-144">Archiviare lo script Pig in un archivio BLOB di Azure e immettere il percorso del file.</span><span class="sxs-lookup"><span data-stu-id="16726-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="16726-145">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="16726-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="16726-146">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="16726-146">Both cannot be used together.</span></span> <span data-ttu-id="16726-147">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="16726-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="16726-148">No</span><span class="sxs-lookup"><span data-stu-id="16726-148">No</span></span> |
| <span data-ttu-id="16726-149">defines</span><span class="sxs-lookup"><span data-stu-id="16726-149">defines</span></span> |<span data-ttu-id="16726-150">Specificare i parametri come coppie chiave/valore per fare riferimento ad essi nello script Pig</span><span class="sxs-lookup"><span data-stu-id="16726-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="16726-151">No</span><span class="sxs-lookup"><span data-stu-id="16726-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="16726-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="16726-152">Example</span></span>
<span data-ttu-id="16726-153">Si prenda ad esempio l'analisi di log di giochi, in cui si desidera verificare il tempo che i giocatori hanno dedicato a giocare alle partite avviate dalla società.</span><span class="sxs-lookup"><span data-stu-id="16726-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="16726-154">Il log del gioco di esempio seguente è un file separato da virgole (,).</span><span class="sxs-lookup"><span data-stu-id="16726-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="16726-155">Il file contiene i campi ProfileID, SessionStart, Duration, SrcIPAddress e GameType.</span><span class="sxs-lookup"><span data-stu-id="16726-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="16726-156">Lo **script Pig** per elaborare tali dati sarà:</span><span class="sxs-lookup"><span data-stu-id="16726-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="16726-157">Per eseguire lo script Pig in una pipeline di Data Factory, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="16726-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="16726-158">Creare un servizio collegato per registrare [il proprio cluster di elaborazione di HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) oppure configurare [un cluster di elaborazione di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="16726-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="16726-159">In questo esempio il servizio collegato è denominato **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16726-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="16726-160">Creare un [servizio collegato](data-factory-azure-blob-connector.md) per configurare la connessione all'archivio BLOB di Azure che ospita i dati.</span><span class="sxs-lookup"><span data-stu-id="16726-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="16726-161">In questo esempio il servizio collegato è denominato **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16726-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="16726-162">Creare [set di dati](data-factory-create-datasets.md) che puntano ai dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="16726-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="16726-163">In questo esempio il set di dati di input è denominato **PigSampleIn**, mentre il set di dati di output è denominato **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="16726-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="16726-164">Copiare la query Pig in un file di archiviazione BLOB di Azure configurato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="16726-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="16726-165">Se l'archiviazione di Azure che ospita i dati è diversa da quella che ospita il file di query, creare un servizio collegato ad archiviazione di Azure separato.</span><span class="sxs-lookup"><span data-stu-id="16726-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="16726-166">Fare riferimento al servizio collegato nella configurazione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="16726-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="16726-167">Usare **scriptPath ** per specificare il percorso del file di script Pig e **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16726-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="16726-168">È anche possibile fornire lo script Pig inline nella definizione dell'attività tramite la proprietà **script** .</span><span class="sxs-lookup"><span data-stu-id="16726-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="16726-169">Tuttavia, si sconsiglia questo approccio poiché è necessario eseguire l'escape di tutti i caratteri speciali dello script, con possibili problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="16726-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="16726-170">Si consiglia di seguire il passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="16726-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="16726-171">Creare la pipeline riportata con l'attività HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="16726-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="16726-172">L'attività elabora i dati di input eseguendo script Pig nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16726-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="16726-173">Distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="16726-173">Deploy the pipeline.</span></span> <span data-ttu-id="16726-174">Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="16726-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="16726-175">Monitorare la pipeline mediante le viste di monitoraggio e gestione delle pipeline di Data factory.</span><span class="sxs-lookup"><span data-stu-id="16726-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="16726-176">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="16726-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="16726-177">Specifica dei parametri per uno script Pig</span><span class="sxs-lookup"><span data-stu-id="16726-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="16726-178">Si consideri l'esempio seguente: i log di giochi vengono inseriti giornalmente nel sistema di archiviazione BLOB di Azure e memorizzati in una cartella partizionata secondo data e ora.</span><span class="sxs-lookup"><span data-stu-id="16726-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="16726-179">Si desidera impostare i parametri per lo script Pig e passare il percorso della cartella di input in modo dinamico durante il runtime, generando l'output partizionato con data e ora.</span><span class="sxs-lookup"><span data-stu-id="16726-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="16726-180">Per impostare i parametri per lo script Pig, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16726-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="16726-181">Definire i parametri in **defines**.</span><span class="sxs-lookup"><span data-stu-id="16726-181">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="16726-182">Nello Script Pig, fare riferimento ai parametri mediante '**$parameterName**' come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="16726-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="16726-183">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="16726-183">See Also</span></span>
* [<span data-ttu-id="16726-184">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="16726-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="16726-185">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="16726-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="16726-186">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="16726-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="16726-187">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="16726-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="16726-188">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="16726-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

