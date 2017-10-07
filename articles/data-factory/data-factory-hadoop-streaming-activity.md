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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Trasformare dati usando l'attività di streaming di Hadoop in Azure Data Factory
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

È possibile utilizzare attività HDInsightStreamingActivity hello richiamare un processo Hadoop Streaming da una pipeline di Data Factory di Azure. Hello frammento di codice JSON seguente mostra la sintassi hello per l'utilizzo di hello HDInsightStreamingActivity in un file JSON di pipeline. 

Attività Streaming di HDInsight in una Data Factory Hello [pipeline](data-factory-create-pipelines.md) esegue i programmi di Streaming di Hadoop nel [la propria](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight basati su Windows/Linux cluster. In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato.

> [!NOTE] 
> Se si tooAzure nuova Data Factory, leggere [tooAzure introduzione Data Factory](data-factory-introduction.md) e hello esercitazione: [la pipeline di dati prima di compilare](data-factory-build-your-first-pipeline.md) prima di leggere questo articolo. 

## <a name="json-sample"></a>Esempio JSON
cluster HDInsight Hello viene popolato automaticamente con i programmi di esempio (wc.exe e cat.exe) e i dati (davinci.txt). Per impostazione predefinita, nome del contenitore di hello utilizzato dal cluster HDInsight hello è il nome di hello del cluster di hello stesso. Ad esempio, se il nome del cluster è myhdicluster, nome del contenitore blob hello associata sarebbe myhdicluster. 

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

Si noti hello seguenti punti:

1. Set hello **linkedServiceName** toohello nome hello collegato del servizio che fa riferimento il cluster di HDInsight tooyour su quali hello streaming mapreduce processo viene eseguito.
2. Impostare il tipo di hello dell'attività hello troppo**HDInsightStreaming**.
3. Per hello **mapper** proprietà, specificare il nome di hello del mapper eseguibile. Nell'esempio hello cat.exe è mapper hello eseguibile.
4. Per hello **riduttore** proprietà, specificare il nome di hello del file eseguibile del reducer. Nell'esempio hello wc.exe è file eseguibile del reducer hello.
5. Per hello **input** digitare proprietà, specificare i file di input hello (incluso il percorso di hello) per il mapper hello. Nell'esempio hello: "//adfsample @<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample è il contenitore di blob hello, esempio/data/Gutenberg è la cartella hello e davinci.txt è blob hello.
6. Per hello **output** digitare proprietà, specificare i file di output di hello (incluso il percorso di hello) per riduttore hello. output di Hello del processo Hadoop Streaming hello viene scritto toohello percorso specificato per questa proprietà.
7. In hello **filePaths** sezione, specificare i percorsi per gli eseguibili del mapper e del reducer hello hello. Nell'esempio hello: "adfsample/example/apps/wc.exe", adfsample è il contenitore di blob hello, example/apps è la cartella hello e wc.exe è hello eseguibile.
8. Per hello **fileLinkedService** proprietà, specificare l'archiviazione di Azure che rappresenta il servizio collegato archiviazione di Azure che contiene file hello specificati nella sezione filePaths hello di hello hello.
9. Per hello **argomenti** proprietà, specificare gli argomenti di hello per hello processo di streaming.
10. Hello **getDebugInfo** proprietà è un elemento facoltativo. Quando si imposta tooFailure, hello registri vengono scaricati solo in caso di errore. Quando si imposta tooAlways, i log vengono sempre scaricati indipendentemente lo stato di esecuzione hello.

> [!NOTE]
> Come illustrato nell'esempio hello, specificare un set di dati di output di hello attività di Streaming di Hadoop per hello **restituisce** proprietà. Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione. Non è necessario toospecify qualsiasi set di dati di input per l'attività hello per hello **input** proprietà.  
> 
> 

## <a name="example"></a>Esempio
pipeline Hello in questa procedura dettagliata viene eseguito il programma MapReduce streaming di hello Conteggio parole il cluster HDInsight di Azure. 

### <a name="linked-services"></a>Servizi collegati
#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Creare innanzitutto un hello toolink servizio collegato di archiviazione Azure utilizzato da hello Azure HDInsight cluster toohello data factory di Azure. Se si copia e Incolla hello seguente di codice, non dimenticare tooreplace account nome account e la chiave con nome hello e dello spazio di archiviazione di Azure. 

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
Successivamente, si crea un servizio collegato di toolink Azure HDInsight cluster toohello data factory di Azure. Se si copia e Incolla hello seguente di codice, sostituire il nome del cluster HDInsight con nome hello del cluster HDInsight e modificare i valori di nome e una password utente. 

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
pipeline Hello in questo esempio non accetta alcun input. Specificare un set di dati di output di hello attività Streaming di HDInsight. Questo set di dati è semplicemente un dummy set di dati è necessario toodrive hello pipeline pianificazione. 

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

### <a name="pipeline"></a>Pipeline
pipeline di Hello in questo esempio include una sola attività che è di tipo: **HDInsightStreaming**. 

cluster HDInsight Hello viene popolato automaticamente con i programmi di esempio (wc.exe e cat.exe) e i dati (davinci.txt). Per impostazione predefinita, nome del contenitore di hello utilizzato dal cluster HDInsight hello è il nome di hello del cluster di hello stesso. Ad esempio, se il nome del cluster è myhdicluster, nome del contenitore blob hello associata sarebbe myhdicluster.  

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
## <a name="see-also"></a>Vedere anche
* [Attività Hive](data-factory-hive-activity.md)
* [Attività di Pig](data-factory-pig-activity.md)
* [Attività MapReduce](data-factory-map-reduce.md)
* [Chiamare i programmi Spark](data-factory-spark.md)
* [Chiamare gli script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

