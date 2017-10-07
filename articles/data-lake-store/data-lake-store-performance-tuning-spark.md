---
title: aaaAzure Data Lake archivio Spark ottimizzazione linee guida | Documenti Microsoft
description: Linee guida per l'ottimizzazione delle prestazioni di Spark in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Linee guida per l'ottimizzazione delle prestazioni di Spark in HDInsight e di Azure Data Lake Store

Quando l'ottimizzazione delle prestazioni in Spark, è necessario numero hello tooconsider di App che verranno eseguiti nel cluster.  Per impostazione predefinita, è possibile eseguire 4 App contemporaneamente nel cluster HDI (Nota: hello impostazione predefinita è soggetto toochange).  È possibile decidere toouse meno App in modo è possibile eseguire l'override delle impostazioni predefinite di hello e utilizzare altri cluster hello per le app.  

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Assicurarsi di abilitare Desktop remoto per il cluster hello.
* **Esecuzione di cluster Spark in Azure Data Lake Store**.  Per ulteriori informazioni, vedere [usare HDInsight Spark cluster tooanalyze dati archivio Data Lake](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Linee guida per l'ottimizzazione delle prestazioni in ADLS**.  Per i concetti generali relativi alle prestazioni, vedere [Linee guida per l'ottimizzazione delle prestazioni in Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>parameters

Quando si eseguono Spark processi, ecco le impostazioni più importanti hello che possono essere le prestazioni ottimizzate tooincrease ADLS:

* **Num executor** -hello numero di attività simultanee che possono essere eseguite.

* **Memoria esecutore** -quantità hello di memoria allocata dell'executor tooeach.

* **Executor core** -numero hello di core allocati tooeach executor.                     

**Num executor** Num executor imposta il numero massimo di hello delle attività eseguibili in parallelo.  numero effettivo di Hello di attività che possono eseguire in parallelo è vincolata dalla memoria hello e le risorse di CPU disponibili nel cluster.

**Memoria esecutore** è hello quantità di memoria allocata dell'executor tooeach.  memoria Hello necessaria per ogni esecutore dipende dal processo hello.  Per operazioni complesse, della memoria hello deve toobe superiore.  Per operazioni semplici come la lettura e la scrittura, la quantità di memoria richiesta è inferiore.  Hello quantità di memoria per ogni esecutore possono essere visualizzati in Ambari.  In Ambari, passare tooSpark e visualizzarle scheda configurazioni hello.  

**Executor core** Imposta quantità hello di core utilizzati per l'esecutore, che determina il numero di hello di thread paralleli che può essere eseguita ogni executor.  Ad esempio, se executor Core = 2, quindi ogni esecutore è possibile eseguire attività in parallelo 2 in executor hello.  executor Hello-core necessarie saranno dipende dal processo hello.  I processi I/O intensivi non richiedono una grande quantità di memoria per ogni attività. In questo modo, ogni executor può gestire più attività in parallelo.

Per impostazione predefinita, durante l'esecuzione di Spark in HDInsight, vengono definiti due core YARN virtuali per ogni core fisico.  Questo numero fornisce un buon bilanciamento tra concorrenza e quantità di contesto nel passaggio tra più thread.  

## <a name="guidance"></a>Indicazioni

Durante l'esecuzione di carichi di lavoro analitici toowork Spark con i dati in archivio Data Lake, è consigliabile utilizzare hello più recente HDInsight versione tooget hello migliori prestazioni con archivio Data Lake. Quando il processo è più elevato utilizzo dei / o, determinati parametri possono essere configurato tooimprove prestazioni.  Azure Data Lake Store è una piattaforma di archiviazione altamente scalabile in grado di gestire un'elevata velocità effettiva.  Se il processo di hello è principalmente costituito da lettura o scrittura, quindi aumentare la concorrenza per tooand dei / o dall'archivio Azure Data Lake di migliorare le prestazioni.

Esistono alcuni concorrenza di tooincrease metodi generali per i processi con utilizzo intensivo dei / o.

**Passaggio 1: Determinare quante applicazioni sono in esecuzione nel cluster** : È necessario conoscere il numero di applicazioni sono in esecuzione nel cluster di hello inclusi hello corrente.  valori predefiniti Hello per ogni Spark impostazione dà per scontato che sono presenti 4 App in esecuzione contemporaneamente.  Pertanto, sarà necessario solo il 25% del cluster di hello disponibili per ogni app.  tooget ottenere prestazioni migliori, è possibile sostituire i valori predefiniti di hello modificando il numero di hello di executor.  

**Passaggio 2: Impostare l'executor memoria** : hello in primo luogo tooset è hello executor di memoria.  memoria Hello sarà dipende dal processo hello siano toorun continua.  È possibile aumentare la concorrenza allocando una quantità inferiore di memoria per ogni executor.  Se viene visualizzato eccezioni di memoria insufficiente quando si esegue il processo, è necessario aumentare il valore di hello per questo parametro.  Uno alternativo è tooget maggiore quantità di memoria utilizzando un cluster con una maggiore quantità di memoria o aumento delle dimensioni di hello del cluster.  Quantità di memoria consentirà toobe executor più utilizzato, il che significa maggiore concorrenza.

**Passaggio 3: Impostare l'executor core** : i/o intensivo carichi di lavoro che non dispongono di operazioni complesse, è buona toostart con un numero elevato di core di executor tooincrease hello svariate attività in parallelo per ogni executor.  L'impostazione too4 esecutore core è un buon inizio.   

    executor-cores = 4
Aumentare il numero di hello executor core offrirà parallelismo in modo è possibile sperimentare diversi executor-Core.  Per i processi che includono operazioni più complesse, è necessario ridurre il numero di hello di core per l'esecutore.  Se executor-cores viene impostato su un valore superiore a 4, la Garbage Collection può diventare inefficiente e incidere negativamente sulle prestazioni.

**Passaggio 4: Determinare la quantità di memoria YARN nel cluster**. Queste informazioni sono disponibili in Ambari.  Passare tooYARN e visualizzare scheda configurazioni hello.  memoria YARN Hello viene visualizzato in questa finestra.  
Nota: quando si è nella finestra di hello, è possibile visualizzare anche dimensioni predefinite del contenitore YARN hello.  dimensione del contenitore YARN Hello è hello stesso come memoria per ogni parametro dell'executor.

    Total YARN memory = nodes * YARN memory per node
**Passaggio 5: Calcolare num-executors**

**Calcolare il vincolo di memoria** -parametro num executor hello è vincolato dalla memoria o CPU.  limitazione della memoria Hello è determinato dalla quantità di hello di memoria YARN disponibile per l'applicazione.  Prendere il valore della memoria totale di YARN e dividerlo per il valore executor-memory.  vincolo Hello deve toobe deallocare dimensionate per numero hello di App in modo che verrà diviso per il numero di hello di App.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calcolare il vincolo di CPU** -hello vincolo relativo alla CPU viene calcolato come totale core virtuali divisi hello numero di core per l'esecutore di hello.  Per ogni core fisico sono presenti 2 core virtuali.  Limitazione della memoria toohello simile, abbiamo divisione dal numero di hello di App.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Impostare l'executor di num** – parametro num executor hello è determinato tenendo hello minimo hello vincoli di memoria e CPU hello. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Impostare un numero maggiore di num-executors non si traduce necessariamente in un miglioramento delle prestazioni.  Si noti che l'aggiunta di esecutori può comportare un carico extra per ciascuno di questi ultimi, con una potenziale diminuzione delle prestazioni.  Num executor è limitato da risorse cluster hello.    

## <a name="example-calculation"></a>Calcolo di esempio

Si supponga che si dispone di un cluster costituito da 8 nodi D4v2 2 in esecuzione le applicazioni inclusi hello quello che si sta toorun.  

**Passaggio 1: Determinare quante applicazioni sono in esecuzione nel cluster** : è possibile sapere che si dispone di 2 app nel cluster, inclusi hello uno sarà toorun.  

**Passaggio 2: Impostare executor-memory**. Per questo esempio, si stabilisce che 6 GB di memoria per executor saranno sufficienti per il processo I/O intensivo.  

    executor-memory = 6GB
**Passaggio 3: Impostare l'executor core** : poiché si tratta di un processo con utilizzo intensivo dei / o, è possibile impostare il numero di hello di core per ogni too4 executor.  L'impostazione di core per toolarger executor di 4 può causare problemi di garbage collection.  

    executor-cores = 4
**Passaggio 4: Determinare le quantità di memoria YARN cluster** : esplorazione toofind tooAmbari out che ogni D4v2 è 25 GB di memoria YARN.  Poiché sono presenti 8 nodi, memoria YARN hello viene moltiplicata per 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Passaggio 5: Calcolare num executor** – parametro num executor hello è determinato tenendo hello minima di memoria hello e il vincolo di CPU hello diviso hello n. di App in esecuzione su Spark.    

**Calcolare il vincolo di memoria** : vincolo memoria hello viene calcolato come memoria YARN totale hello divisa per la memoria hello per executor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calcolare il vincolo di CPU** -hello vincolo relativo alla CPU viene calcolato come hello core yarn totale divisi hello numero di core per l'esecutore.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Impostare num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

