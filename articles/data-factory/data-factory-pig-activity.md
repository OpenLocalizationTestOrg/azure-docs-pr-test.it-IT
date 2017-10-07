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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Trasformare dati usando l'attività Pig in Azure Data Factory
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md) 
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

attività Pig di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue query Pig nel [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux. In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.

> [!NOTE] 
> Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo. 

## <a name="syntax"></a>Sintassi

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
## <a name="syntax-details"></a>Dettagli sintassi
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome dell'attività hello |Sì |
| description |Testo che descrive le attività di hello viene utilizzato per |No |
| type |HDInsightPig |Sì |
| inputs |Uno o più input utilizzata da hello attività Pig |No |
| outputs |Uno o più output prodotti da hello attività Pig |Sì |
| linkedServiceName |Cluster di HDInsight toohello riferimento registrato come un servizio collegato in Data Factory |Sì |
| script |Specificare hello Pig script inline |No |
| script path |Archiviare lo script Pig hello in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file. Usare la proprietà "script" o "scriptPath". Non è possibile usare entrambe le proprietà. nome del file Hello è tra maiuscole e minuscole. |No |
| defines |Specificare i parametri come coppie chiave/valore per il riferimento all'interno di uno script Pig hello |No |

## <a name="example"></a>Esempio
Si consideri un esempio di gioco registra analitica in cui si desidera ora hello tooidentify impiegata dai lettori giochi avviata dall'azienda.

Hello log gioco di esempio seguente è un file separato da virgole (,). Contiene i seguenti campi: ProfileID, SessionStart, durata, SrcIPAddress e GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **script Pig** tooprocess dati:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

hello tooexecute questo Pig script in una pipeline di Data Factory, alla procedura seguente:

1. Creare un servizio collegato di tooregister [HDInsight un cluster di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurare [cluster di calcolo di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). In questo esempio il servizio collegato è denominato **HDInsightLinkedService**.
2. Creare un [servizio collegato](data-factory-azure-blob-connector.md) tooconfigure hello connessione tooAzure nell'archiviazione Blob hello dati di hosting. In questo esempio il servizio collegato è denominato **StorageLinkedService**.
3. Creare [set di dati](data-factory-create-datasets.md) rivolte verso l'input toohello e hello i dati di output. Si parlerà di set di dati input hello **PigSampleIn** e set di dati di output di hello **PigSampleOut**.
4. Copia query Pig hello in hello un file di archiviazione Blob Azure configurato nel passaggio &#2;. Se l'archiviazione di Azure che ospita i dati di hello hello è diverso da hello uno che ospita il file di query hello, creare un servizio collegato di archiviazione di Azure separato. Fare riferimento a servizio toohello collegato nella configurazione di attività hello. Utilizzare * * scriptPath * * file di script toospecify hello percorso toopig e **scriptLinkedService**. 
   
   > [!NOTE]
   > È inoltre possibile fornire hello Pig script inline nella definizione di attività hello hello **script** proprietà. Tuttavia, non è consigliabile questo approccio come tutti i caratteri speciali in script hello deve toobe caratteri di escape e può causare problemi di debug. procedura consigliata Hello è toofollow passaggio #4.
   > 
   > 
5. Creare pipeline hello con hello HDInsightPig attività. Questa attività consente di elaborare i dati di input hello eseguendo lo script Pig in cluster HDInsight.

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
6. Distribuire la pipeline hello. Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) . 
7. Monitorare le pipeline hello tramite il monitoraggio di hello data factory e le viste a gestione. Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) .

## <a name="specifying-parameters-for-a-pig-script"></a>Specifica dei parametri per uno script Pig
Prendere in considerazione hello di esempio seguente: registri giochi sono caricamento ogni giorno nell'archiviazione Blob di Azure e archiviati in una cartella partizionata in base alla data e ora. Si desidera che lo script Pig tooparameterize hello e passare il percorso di cartella di input di hello in modo dinamico in fase di esecuzione e anche produrre output di hello partizionato con data e ora.

toouse script Pig con parametri, eseguire hello seguenti:

* Definire i parametri di hello in **definisce**.

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
* In hello Script Pig, fanno riferimento i parametri toohello utilizzando '**$parameterName**' come illustrato nell'esempio seguente hello:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Vedere anche
* [Attività Hive](data-factory-hive-activity.md)
* [Attività MapReduce](data-factory-map-reduce.md)
* [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
* [Chiamare i programmi Spark](data-factory-spark.md)
* [Chiamare gli script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

