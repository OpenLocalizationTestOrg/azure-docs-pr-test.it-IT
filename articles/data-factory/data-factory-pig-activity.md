---
title: "i dati di aaaTransform utilizzando attività Pig di Azure Data Factory | Documenti Microsoft"
description: "Informazioni su come è possibile utilizzare un script Pig di Azure data factory toorun Ciao attività Pig in un cluster di HDInsight su richiesta o il personalizzati."
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
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="f10f6-103">Trasformare dati usando l'attività Pig in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f10f6-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="f10f6-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="f10f6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="f10f6-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="f10f6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="f10f6-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="f10f6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="f10f6-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="f10f6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="f10f6-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="f10f6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="f10f6-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f10f6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="f10f6-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f10f6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="f10f6-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="f10f6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="f10f6-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f10f6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="f10f6-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="f10f6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="f10f6-114">attività Pig di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue query Pig nel [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="f10f6-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f10f6-115">In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="f10f6-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="f10f6-116">Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f10f6-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="f10f6-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f10f6-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="f10f6-118">Dettagli sintassi</span><span class="sxs-lookup"><span data-stu-id="f10f6-118">Syntax details</span></span>
| <span data-ttu-id="f10f6-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f10f6-119">Property</span></span> | <span data-ttu-id="f10f6-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f10f6-120">Description</span></span> | <span data-ttu-id="f10f6-121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f10f6-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f10f6-122">name</span><span class="sxs-lookup"><span data-stu-id="f10f6-122">name</span></span> |<span data-ttu-id="f10f6-123">Nome dell'attività hello</span><span class="sxs-lookup"><span data-stu-id="f10f6-123">Name of hello activity</span></span> |<span data-ttu-id="f10f6-124">Sì</span><span class="sxs-lookup"><span data-stu-id="f10f6-124">Yes</span></span> |
| <span data-ttu-id="f10f6-125">description</span><span class="sxs-lookup"><span data-stu-id="f10f6-125">description</span></span> |<span data-ttu-id="f10f6-126">Testo che descrive le attività di hello viene utilizzato per</span><span class="sxs-lookup"><span data-stu-id="f10f6-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="f10f6-127">No</span><span class="sxs-lookup"><span data-stu-id="f10f6-127">No</span></span> |
| <span data-ttu-id="f10f6-128">type</span><span class="sxs-lookup"><span data-stu-id="f10f6-128">type</span></span> |<span data-ttu-id="f10f6-129">HDInsightPig</span><span class="sxs-lookup"><span data-stu-id="f10f6-129">HDinsightPig</span></span> |<span data-ttu-id="f10f6-130">Sì</span><span class="sxs-lookup"><span data-stu-id="f10f6-130">Yes</span></span> |
| <span data-ttu-id="f10f6-131">inputs</span><span class="sxs-lookup"><span data-stu-id="f10f6-131">inputs</span></span> |<span data-ttu-id="f10f6-132">Uno o più input utilizzata da hello attività Pig</span><span class="sxs-lookup"><span data-stu-id="f10f6-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="f10f6-133">No</span><span class="sxs-lookup"><span data-stu-id="f10f6-133">No</span></span> |
| <span data-ttu-id="f10f6-134">outputs</span><span class="sxs-lookup"><span data-stu-id="f10f6-134">outputs</span></span> |<span data-ttu-id="f10f6-135">Uno o più output prodotti da hello attività Pig</span><span class="sxs-lookup"><span data-stu-id="f10f6-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="f10f6-136">Sì</span><span class="sxs-lookup"><span data-stu-id="f10f6-136">Yes</span></span> |
| <span data-ttu-id="f10f6-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f10f6-137">linkedServiceName</span></span> |<span data-ttu-id="f10f6-138">Cluster di HDInsight toohello riferimento registrato come un servizio collegato in Data Factory</span><span class="sxs-lookup"><span data-stu-id="f10f6-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="f10f6-139">Sì</span><span class="sxs-lookup"><span data-stu-id="f10f6-139">Yes</span></span> |
| <span data-ttu-id="f10f6-140">script</span><span class="sxs-lookup"><span data-stu-id="f10f6-140">script</span></span> |<span data-ttu-id="f10f6-141">Specificare hello Pig script inline</span><span class="sxs-lookup"><span data-stu-id="f10f6-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="f10f6-142">No</span><span class="sxs-lookup"><span data-stu-id="f10f6-142">No</span></span> |
| <span data-ttu-id="f10f6-143">script path</span><span class="sxs-lookup"><span data-stu-id="f10f6-143">script path</span></span> |<span data-ttu-id="f10f6-144">Archiviare lo script Pig hello in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file.</span><span class="sxs-lookup"><span data-stu-id="f10f6-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="f10f6-145">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="f10f6-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="f10f6-146">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="f10f6-146">Both cannot be used together.</span></span> <span data-ttu-id="f10f6-147">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="f10f6-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="f10f6-148">No</span><span class="sxs-lookup"><span data-stu-id="f10f6-148">No</span></span> |
| <span data-ttu-id="f10f6-149">defines</span><span class="sxs-lookup"><span data-stu-id="f10f6-149">defines</span></span> |<span data-ttu-id="f10f6-150">Specificare i parametri come coppie chiave/valore per il riferimento all'interno di uno script Pig hello</span><span class="sxs-lookup"><span data-stu-id="f10f6-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="f10f6-151">No</span><span class="sxs-lookup"><span data-stu-id="f10f6-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="f10f6-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="f10f6-152">Example</span></span>
<span data-ttu-id="f10f6-153">Si consideri un esempio di gioco registra analitica in cui si desidera ora hello tooidentify impiegata dai lettori giochi avviata dall'azienda.</span><span class="sxs-lookup"><span data-stu-id="f10f6-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="f10f6-154">Hello log gioco di esempio seguente è un file separato da virgole (,).</span><span class="sxs-lookup"><span data-stu-id="f10f6-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="f10f6-155">Contiene i seguenti campi: ProfileID, SessionStart, durata, SrcIPAddress e GameType hello.</span><span class="sxs-lookup"><span data-stu-id="f10f6-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="f10f6-156">Hello **script Pig** tooprocess dati:</span><span class="sxs-lookup"><span data-stu-id="f10f6-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="f10f6-157">hello tooexecute questo Pig script in una pipeline di Data Factory, alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f10f6-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="f10f6-158">Creare un servizio collegato di tooregister [HDInsight un cluster di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurare [cluster di calcolo di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="f10f6-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="f10f6-159">In questo esempio il servizio collegato è denominato **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f10f6-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="f10f6-160">Creare un [servizio collegato](data-factory-azure-blob-connector.md) tooconfigure hello connessione tooAzure nell'archiviazione Blob hello dati di hosting.</span><span class="sxs-lookup"><span data-stu-id="f10f6-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="f10f6-161">In questo esempio il servizio collegato è denominato **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f10f6-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="f10f6-162">Creare [set di dati](data-factory-create-datasets.md) rivolte verso l'input toohello e hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="f10f6-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="f10f6-163">Si parlerà di set di dati input hello **PigSampleIn** e set di dati di output di hello **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="f10f6-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="f10f6-164">Copia query Pig hello in hello un file di archiviazione Blob Azure configurato nel passaggio &#2;.</span><span class="sxs-lookup"><span data-stu-id="f10f6-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="f10f6-165">Se l'archiviazione di Azure che ospita i dati di hello hello è diverso da hello uno che ospita il file di query hello, creare un servizio collegato di archiviazione di Azure separato.</span><span class="sxs-lookup"><span data-stu-id="f10f6-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="f10f6-166">Fare riferimento a servizio toohello collegato nella configurazione di attività hello.</span><span class="sxs-lookup"><span data-stu-id="f10f6-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="f10f6-167">Utilizzare * * scriptPath * * file di script toospecify hello percorso toopig e **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f10f6-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f10f6-168">È inoltre possibile fornire hello Pig script inline nella definizione di attività hello hello **script** proprietà.</span><span class="sxs-lookup"><span data-stu-id="f10f6-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="f10f6-169">Tuttavia, non è consigliabile questo approccio come tutti i caratteri speciali in script hello deve toobe caratteri di escape e può causare problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="f10f6-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="f10f6-170">procedura consigliata Hello è toofollow passaggio #4.</span><span class="sxs-lookup"><span data-stu-id="f10f6-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="f10f6-171">Creare pipeline hello con hello HDInsightPig attività.</span><span class="sxs-lookup"><span data-stu-id="f10f6-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="f10f6-172">Questa attività consente di elaborare i dati di input hello eseguendo lo script Pig in cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f10f6-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="f10f6-173">Distribuire la pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="f10f6-173">Deploy hello pipeline.</span></span> <span data-ttu-id="f10f6-174">Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="f10f6-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="f10f6-175">Monitorare le pipeline hello tramite il monitoraggio di hello data factory e le viste a gestione.</span><span class="sxs-lookup"><span data-stu-id="f10f6-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="f10f6-176">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="f10f6-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="f10f6-177">Specifica dei parametri per uno script Pig</span><span class="sxs-lookup"><span data-stu-id="f10f6-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="f10f6-178">Prendere in considerazione hello di esempio seguente: registri giochi sono caricamento ogni giorno nell'archiviazione Blob di Azure e archiviati in una cartella partizionata in base alla data e ora.</span><span class="sxs-lookup"><span data-stu-id="f10f6-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="f10f6-179">Si desidera che lo script Pig tooparameterize hello e passare il percorso di cartella di input di hello in modo dinamico in fase di esecuzione e anche produrre output di hello partizionato con data e ora.</span><span class="sxs-lookup"><span data-stu-id="f10f6-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="f10f6-180">toouse script Pig con parametri, eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f10f6-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="f10f6-181">Definire i parametri di hello in **definisce**.</span><span class="sxs-lookup"><span data-stu-id="f10f6-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="f10f6-182">In hello Script Pig, fanno riferimento i parametri toohello utilizzando '**$parameterName**' come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f10f6-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="f10f6-183">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f10f6-183">See Also</span></span>
* [<span data-ttu-id="f10f6-184">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="f10f6-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="f10f6-185">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="f10f6-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="f10f6-186">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="f10f6-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="f10f6-187">Chiamare i programmi Spark</span><span class="sxs-lookup"><span data-stu-id="f10f6-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="f10f6-188">Chiamare gli script R</span><span class="sxs-lookup"><span data-stu-id="f10f6-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

