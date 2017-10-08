---
title: procedure dettagliate di Spark aaaHDInsight con PySpark e la Scala in Azure | Documenti Microsoft
description: "Esempi di hello processo di analisi scientifica dei dati di Team che analizzerà hello utilizzano PySpark e Scala su un analitica predittiva toodo di Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Procedure dettagliate di data science per HDInsight Spark con PySpark e Scala in Azure

Queste procedure dettagliate utilizzano PySpark e Scala su un analitica predittiva di cluster toodo Azure Spark. Le funzioni seguono hello procedure hello processo di analisi scientifica dei dati del Team. Per una panoramica del processo di analisi scientifica dei dati di Team hello, vedere [il processo di analisi scientifica dei dati](data-science-process-overview.md). Per una panoramica di Spark in HDInsight, vedere [tooSpark introduzione in HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Procedure dettagliate di analisi scientifica dei dati aggiuntivi che eseguono hello processo di analisi scientifica dei dati di Team vengono raggruppate in hello **piattaforma** che utilizzano: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Stimare le mance dei taxi con PySpark in Azure Spark

Hello [usare Spark in HDInsight](machine-learning-data-science-spark-overview.md) procedura dettagliata Usa i dati di New York taxi toopredict se viene applicato un suggerimento e intervallo hello degli importi previsto toobe a pagamento. Usa hello Team processo di analisi scientifica dei dati in un scenario di utilizzo di un [cluster Azure HDInsight Spark](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare e funzionalità engineer dati hello disponibile pubblicamente NYC taxi di andata e ritorno e presentare set di dati. Questo argomento introduttivo imposta è con un cluster HDInsight Spark e hello Jupyter PySpark notebook utilizzato nel resto di hello della procedura dettagliata hello. Questi notebook illustrano come tooexplore i dati e come quindi toocreate e utilizzare i modelli. Hello avanzate di esplorazione dei dati e modellazione notebook Mostra come tooinclude convalida incrociata, hyper-parameter sweep e valutazione del modello.

### <a name="data-exploration-and-modeling-with-spark"></a>Modellazione ed esplorazione dei dati con Spark 
Esplorare hello set di dati e creare, assegnare un punteggio e valutare i modelli di machine learning hello affrontando hello [creare modelli di classificazione e regressione binari per i dati con hello Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) argomento.

### <a name="model-consumption"></a>Modellare il consumo
toolearn come modelli di classificazione e regressione hello tooscore creato in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Convalida incrociata e sweep di iperparametri
Per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri, vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Stimare le mance dei taxi con Scala in Azure Spark

Hello [Scala utilizzare con Spark in Azure](machine-learning-data-science-process-scala-walkthrough.md) procedura dettagliata Usa i dati di New York taxi toopredict se viene applicato un suggerimento e intervallo hello degli importi previsto toobe a pagamento. Viene illustrato come toouse Scala per le attività di apprendimento supervisionato macchina con libreria di apprendimento hello Spark macchina (MLlib) e SparkML pacchetti in un cluster Azure HDInsight Spark. Illustra le attività che costituiscono hello hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess): inserimento di dati e l'esplorazione, visualizzazione, progettazione di funzionalità, modellazione e il consumo di modello. i modelli di Hello compilati includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting.


## <a name="next-steps"></a>Passaggi successivi

Per una descrizione dei componenti principali di hello che costituiscono hello processo di analisi scientifica dei dati di Team, vedere [Cenni preliminari sul processo di analisi scientifica dei dati di Team](data-science-process-overview.md).

Per una descrizione del ciclo di vita di processo di analisi scientifica dei dati di Team hello che è possibile utilizzare toostructure i progetti di analisi scientifica dei dati, vedere [ciclo di vita del processo di analisi scientifica dei dati di Team](data-science-process-lifecycle.md). ciclo di vita Hello descrive i passaggi di hello, dall'inizio toofinish, i progetti seguenti in genere quando vengono eseguiti. 

