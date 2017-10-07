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
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Richiamare i programmi MapReduce da Data factory
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

attività MapReduce di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue i programmi MapReduce in [proprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight basati su Windows o Linux. In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.

> [!NOTE] 
> Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo.  

## <a name="introduction"></a>Introduzione
Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati. Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione. In questo articolo viene descritto l'utilizzo di hello attività MapReduce di HDInsight.

Vedere [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) per informazioni dettagliate sull'esecuzione di script Pig/Hive in un cluster HDInsight basato su Windows/Linux da una pipeline usando le attività Pig e Hive di HDInsight. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON per attività MapReduce di HDInsight
Nella definizione JSON per hello attività HDInsight hello: 

1. Set hello **tipo** di hello **attività** troppo**HDInsight**.
2. Specificare il nome di hello classe hello per **className** proprietà.
3. Specificare i file JAR di hello percorso toohello tra nome file hello **jarFilePath** proprietà.
4. Specificare il servizio di hello collegato che fa riferimento toohello archiviazione Blob di Azure che contiene i file JAR hello per **jarLinkedService** proprietà.   
5. Specificare gli argomenti per il programma MapReduce hello in hello **argomenti** sezione. In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello. toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni).

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
È possibile utilizzare hello attività MapReduce di HDInsight toorun qualsiasi file jar MapReduce in un cluster HDInsight. In hello definizione JSON di esempio seguente di una pipeline, hello attività HDInsight è configurata in un file JAR Mahout toorun.

## <a name="sample-on-github"></a>Esempio in GitHub
È possibile scaricare un esempio per l'utilizzo di hello attività MapReduce di HDInsight da: [Data Factory esempi su GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Eseguire il programma di conteggio parole hello
pipeline Hello in questo esempio viene eseguito il programma MapReduce Conteggio parole hello il cluster HDInsight di Azure.   

### <a name="linked-services"></a>Servizi collegati
Creare innanzitutto un hello toolink servizio collegato di archiviazione Azure utilizzato da hello Azure HDInsight cluster toohello data factory di Azure. Se si copia e Incolla hello seguente di codice, non dimenticare tooreplace **nome account** e **chiave dell'account** con nome hello e la chiave di archiviazione Azure. 

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure

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

#### <a name="azure-hdinsight-linked-service"></a>Servizio collegato Azure HDInsight
Successivamente, si crea un servizio collegato di toolink Azure HDInsight cluster toohello data factory di Azure. Se si copia e Incolla hello di codice seguente, sostituire **nome del cluster HDInsight** con nome hello del cluster HDInsight e modifica nome utente e password specificati.   

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

### <a name="datasets"></a>DATASETS
#### <a name="output-dataset"></a>Set di dati di output
pipeline Hello in questo esempio non accetta alcun input. Specificare un set di dati di output di hello attività MapReduce di HDInsight. Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione.  

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

### <a name="pipeline"></a>Pipeline
pipeline di Hello in questo esempio include una sola attività che è di tipo: HDInsightMapReduce. Alcune delle proprietà importanti di hello in hello JSON sono: 

| Proprietà | Note |
|:--- |:--- |
| type |è necessario impostare il tipo di Hello troppo**HDInsightMapReduce**. |
| className |Nome della classe hello è: **wordcount** |
| jarFilePath |Percorso file jar toohello contenente la classe hello. Se si copia e Incolla hello seguente di codice, non dimenticare nome hello toochange del cluster di hello. |
| jarLinkedService |Servizio collegato di archiviazione Azure che contiene i file jar hello. Il servizio collegato fa riferimento toohello spazio di archiviazione associato al cluster HDInsight hello. |
| arguments |programma wordcount Hello accetta due argomenti, un input e output. file di input Hello è davinci.txt hello. |
| frequenza/intervallo |Hello per queste proprietà corrispondono hello output set di dati. |
| linkedServiceName |fa riferimento a servizio collegato di HDInsight toohello è stato creato in precedenza. |

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

## <a name="run-spark-programs"></a>Esecuzione dei programmi Spark
È possibile utilizzare i programmi MapReduce attività toorun Spark il cluster HDInsight Spark. Per i dettagli, vedere [Chiamare i programmi Spark da Azure Data Factory](data-factory-spark.md) .  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Vedere anche
* [Attività Hive](data-factory-hive-activity.md)
* [Attività di Pig](data-factory-pig-activity.md)
* [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
* [Chiamare i programmi Spark](data-factory-spark.md)
* [Chiamare gli script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

