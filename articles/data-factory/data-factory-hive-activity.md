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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Trasformare dati usando l'attività Hive in Azure Data Factory 
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

attività Hive di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue query Hive nel [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux. In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.

> [!NOTE] 
> Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo. 

## <a name="syntax"></a>Sintassi

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
## <a name="syntax-details"></a>Dettagli sintassi
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome dell'attività hello |Sì |
| description |Testo che descrive le attività di hello viene utilizzato per |No |
| type |HDinsightHive |Sì |
| inputs |Input utilizzato dall'attività Hive hello |No |
| outputs |Output generato dall'attività Hive hello |Sì |
| linkedServiceName |Cluster di HDInsight toohello riferimento registrato come un servizio collegato in Data Factory |Sì |
| script |Specificare hello Hive script inline |No |
| script path |Hello archivio Hive script in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file. Usare la proprietà "script" o "scriptPath". Non è possibile usare entrambe le proprietà. nome del file Hello è tra maiuscole e minuscole. |No |
| defines |Specificare i parametri come coppie chiave/valore per il riferimento all'interno dello script Hive hello utilizzando 'hiveconf' |No |

## <a name="example"></a>Esempio
Si consideri un esempio di gioco registra analitica in cui si desidera ora hello tooidentify impiegato dagli utenti giochi avviata dall'azienda. 

Hello log seguente è riportato un esempio gioco log, che è la virgola (`,`) separati e contiene i seguenti campi: ProfileID, SessionStart, durata, SrcIPAddress e GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **lo script Hive** tooprocess dati:

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

tooexecute script Hive in una pipeline di Data Factory, è necessario seguente hello toodo

1. Creare un servizio collegato di tooregister [HDInsight un cluster di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurare [cluster di calcolo di HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). In questo esempio il servizio collegato è denominato "HDInsightLinkedService".
2. Creare un [servizio collegato](data-factory-azure-blob-connector.md) tooconfigure hello connessione tooAzure nell'archiviazione Blob hello dati di hosting. In questo esempio il servizio collegato è denominato "StorageLinkedService".
3. Creare [set di dati](data-factory-create-datasets.md) rivolte verso l'input toohello e hello i dati di output. È ora possibile chiamare set di dati input hello "HiveSampleIn" e set di dati di output "HiveSampleOut" hello
4. Copia query Hive hello come tooAzure un file di archiviazione Blob configurato nel passaggio &#2;. Se l'archiviazione hello per ospitare i dati hello è diverso da hello uno che ospita il file di query, creare un servizio collegato di archiviazione di Azure separato e fa riferimento tooit nell'attività hello. Utilizzare * * scriptPath * * file di query toohive percorso toospecify hello e **scriptLinkedService** toospecify hello archiviazione di Azure che contiene i file di script hello. 
   
   > [!NOTE]
   > È inoltre possibile fornire hello Hive script inline nella definizione di attività hello hello **script** proprietà. Questo approccio non è consigliato come tutti i caratteri speciali in script hello all'interno di documenti JSON hello deve toobe caratteri di escape e può causa problemi di debug. procedura consigliata Hello è toofollow passaggio #4.
   > 
   > 
5. Creare una pipeline con attività HDInsightHive hello. attività Hello processi/trasformazioni dati hello.

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
6. Distribuire la pipeline hello. Per informazioni dettagliate, vedere l'argomento relativo alla [creazione di pipeline](data-factory-create-pipelines.md) . 
7. Monitorare le pipeline hello tramite il monitoraggio di hello data factory e le viste a gestione. Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Data factory di Azure](data-factory-monitor-manage-pipelines.md) . 

## <a name="specifying-parameters-for-a-hive-script"></a>Specifica dei parametri per uno script Hive
In questo esempio i log di giochi vengono inseriti giornalmente nel sistema di archiviazione BLOB di Azure e memorizzati in una cartella partizionata con data e ora. Si desidera tooparameterize hello Hive script e passare il percorso di cartella di input di hello in modo dinamico in fase di esecuzione e anche produrre output di hello partizionato con data e ora.

toouse script Hive con parametri, procedere come segue hello

* Definire i parametri di hello in **definisce**.

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
* Fare riferimento in hello Script Hive, toohello parametro utilizzando **${hiveconf: ParameterName}**. 
  
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
## <a name="see-also"></a>Vedere anche
* [Attività di Pig](data-factory-pig-activity.md)
* [Attività MapReduce](data-factory-map-reduce.md)
* [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
* [Chiamare i programmi Spark](data-factory-spark.md)
* [Chiamare gli script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

