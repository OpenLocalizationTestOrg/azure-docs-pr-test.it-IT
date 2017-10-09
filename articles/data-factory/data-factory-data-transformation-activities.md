---
title: 'Trasformazione dei dati: elaborare e trasformare i dati | Microsoft Docs'
description: Informazioni su come tootransform dati o elaborare i dati in Data Factory di Azure usando Azure Data Lake Analitica, Hadoop e Machine Learning.
keywords: "trasformazione di dati, elaborare dati, trasformare dati, attività di trasformazione"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Trasformare i dati in Azure Data Factory
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Panoramica
In questo articolo vengono illustrate le attività di trasformazione di dati in Data Factory di Azure è possibile utilizzare tootransform ed elabora i dati non elaborati in stime e approfondimenti. L'attività di trasformazione viene eseguita in un ambiente di elaborazione, ad esempio cluster HDInsight di Azure o un Batch di Azure. Fornisce collegamenti tooarticles con informazioni dettagliate su ogni attività di trasformazione.

Data Factory supporta hello seguente attività di trasformazione di dati che possono essere aggiunti troppo[pipeline](data-factory-create-pipelines.md) sia singolarmente o concatenati con un'altra attività.

> [!NOTE]
> Per la procedura dettagliata, vedere l'articolo [Creare una pipeline con la trasformazione Hive](data-factory-build-your-first-pipeline.md) .  
> 
> 

## <a name="hdinsight-hive-activity"></a>Attività Hive di HDInsight
attività Hive di HDInsight in una pipeline di Data Factory Hello esegue query Hive per proprio conto o il cluster HDInsight basati su Windows o Linux su richiesta. Vedere l'articolo [Attività Hive](data-factory-hive-activity.md) per i dettagli. 

## <a name="hdinsight-pig-activity"></a>Attività Pig di HDInsight
attività Pig di HDInsight in una pipeline di Data Factory Hello esegue query Pig autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta. Vedere l'articolo [Attività Pig](data-factory-pig-activity.md) per i dettagli. 

## <a name="hdinsight-mapreduce-activity"></a>Attività MapReduce di HDInsight
attività MapReduce di HDInsight in una pipeline di Data Factory Hello esegue i programmi MapReduce autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta. Vedere l'articolo [Attività MapReduce](data-factory-map-reduce.md) per i dettagli.

## <a name="hdinsight-streaming-activity"></a>Attività di streaming di HDInsight
Hello attività Streaming di HDInsight in una pipeline di Data Factory esegue i programmi di Hadoop Streaming autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta. Vedere l' [attività di streaming di HDInsight](data-factory-hadoop-streaming-activity.md) per i dettagli.

## <a name="hdinsight-spark-activity"></a>Attività Spark di HDInsight
attività HDInsight Spark in una pipeline di Data Factory Hello esegue programmi Spark nel cluster HDInsight. Per conoscere i dettagli, vedere [Richiamare i programmi Spark da Azure Data Factory](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Attività di Machine Learning
Servizio per analitica predittiva web di Azure consente di Data Factory è tooeasily creare pipeline che utilizzano una versione pubblicata di Azure Machine Learning. Utilizzando hello [attività di esecuzione Batch](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) in una pipeline di Data Factory di Azure, è possibile richiamare un stime di toomake servizio web Machine Learning sui dati hello in batch.

Nel corso del tempo, modelli predittivi di hello in hello Machine Learning esperimenti punteggio necessario toobe ripetere il training utilizzando il nuovo set di dati di input. Dopo avere completato con ripetizione di training, si desidera hello tooupdate punteggio servizio web con hello Training modello di Machine Learning. È possibile utilizzare hello [attività della risorsa di aggiornamento](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) servizio web di hello tooupdate con modello sottoposto a training appena hello.  

Vedere [Usare le attività Machine Learning](data-factory-azure-ml-batch-execution-activity.md) per i relativi dettagli. 

## <a name="stored-procedure-activity"></a>Attività stored procedure
È possibile utilizzare l'attività di hello Stored Procedure di SQL Server in un tooinvoke pipeline Data Factory una stored procedure in uno dei seguenti archivi dati hello: Database SQL di Azure, Azure SQL Data Warehouse, il Database di SQL Server nell'organizzazione o una macchina virtuale di Azure. Vedere l'articolo [Attività stored procedure](data-factory-stored-proc-activity.md) per i dettagli.  

## <a name="data-lake-analytics-u-sql-activity"></a>Attività U-SQL di Data Lake Analytics
L'attività U-SQL di Data Lake Analytics esegue uno script U-SQL in un cluster di Azure Data Lake Analytics. Vedere l'articolo [Attività di U-SQL di Data Analytics](data-factory-usql-activity.md) per i dettagli. 

## <a name="net-custom-activity"></a>Attività personalizzata .NET
Se è necessario tootransform dati in modo che non è supportato da Data Factory, è possibile creare un'attività personalizzata con la logica di elaborazione dei dati e utilizzare attività hello nella pipeline hello. È possibile configurare hello personalizzato .NET attività toorun utilizzando un servizio Azure Batch o un cluster Azure HDInsight. Vedere l'articolo [Usare le attività personalizzate](data-factory-use-custom-activities.md) per i dettagli. 

È possibile creare gli script R toorun un'attività personalizzata nel cluster di HDInsight con R installato. Vedere [RunRScriptUsingADFSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Esempio relativo all'esecuzione di script R con Azure Data Factory). 

## <a name="compute-environments"></a>Ambienti di calcolo
Creare un servizio collegato per l'ambiente di calcolo hello e quindi utilizzare il servizio collegato hello quando si definisce un'attività di trasformazione. Esistono due tipi di ambienti di calcolo supportati da Data factory. 

1. **Su richiesta**: In questo caso, ambiente di elaborazione hello è completamente gestiti da Data Factory. Viene automaticamente creata dal servizio Data Factory hello prima tooprocess inviato dati è un processo e rimosse quando viene completato il processo di hello. È possibile configurare e controllare le impostazioni del livello di granularità dell'ambiente di calcolo su richiesta hello per l'esecuzione del processo, la gestione di cluster e l'avvio di azioni. 
2. **Bring Your Own**: In questo caso, è possibile registrare il proprio ambiente di elaborazione (ad esempio cluster HDInsight) come servizio collegato in Data factory. ambiente di elaborazione Hello è gestita dall'utente e hello servizio Data Factory utilizza le attività di hello tooexecute. 

Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md) toolearn articolo sui servizi supportati da Data Factory di calcolo. 

## <a name="summary"></a>Riepilogo
Azure Data Factory supporta hello seguente attività di trasformazione dei dati e gli ambienti di calcolo per le attività di hello hello. le attività di trasformazione Hello possono essere aggiunto toopipelines singolarmente o concatenati con un'altra attività.

| Attività di trasformazione dei dati | Ambiente di calcolo |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Attività di Machine Learning: esecuzione batch e aggiornamento risorse](data-factory-azure-ml-batch-execution-activity.md) |Macchina virtuale di Azure |
| [Stored procedure](data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse o SQL Server |
| [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md) |Azure Data Lake Analytics. |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] o Batch di Azure |

