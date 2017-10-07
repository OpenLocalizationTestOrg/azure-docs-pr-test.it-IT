---
title: Data Lake archivio Hive ottimizzazione linee guida sulle prestazioni aaaAzure | Documenti Microsoft
description: Linee guida per l'ottimizzazione delle prestazioni di Hive in Azure Data Lake Store
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Linee guida per l'ottimizzazione delle prestazioni di Hive in HDInsight e di Azure Data Lake Store

le impostazioni predefinite di Hello sono state impostate tooprovide buone prestazioni in molti casi di utilizzo diversi.  Per le query con utilizzo intensivo dei / o, Hive può essere ottimizzato tooget migliori prestazioni con ADLS.  

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Assicurarsi di abilitare Desktop remoto per il cluster hello.
* **Esecuzione di Hive in HDInsight**.  toolearn sull'esecuzione di processi Hive in HDInsight, vedere [utilizzare Hive in HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Linee guida per l'ottimizzazione delle prestazioni in ADLS**.  Per i concetti generali relativi alle prestazioni, vedere [Linee guida per l'ottimizzazione delle prestazioni in Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>parameters

Di seguito sono hello più importanti impostazioni tootune per migliorare le prestazioni di ADLS:

* **hive.tez.Container.Size** : quantità di hello di memoria utilizzata da ogni attività.

* **tez.grouping.min-size**: la dimensione minima di ciascun mapper

* **tez.grouping.max-size**: la dimensione massima di ciascun mapper

* **hive.exec.reducer.bytes.per.reducer**: la dimensione di ciascun riduttore

**hive.tez.Container.Size** -dimensione del contenitore hello determina la quantità di memoria disponibile per ogni attività.  Si tratta di input principale di hello per il controllo della concorrenza hello nell'Hive.  

**dimensioni tez.Grouping.min** : questo parametro consente di dimensioni minime di hello tooset di ogni mapper.  Se il numero di hello di BizTalk Mapper che sceglie Tez è minore del valore di questo parametro hello, Tez utilizzerà il valore di hello impostato.  

**dimensioni tez.Grouping.max** – parametro hello consente dimensioni massime di hello tooset di ogni mapper.  Se il numero di hello di BizTalk Mapper che sceglie Tez è superiore rispetto al valore di questo parametro hello, Tez utilizzerà il valore di hello impostato.  

**hive.Exec.REDUCER.bytes.per.REDUCER** : questo parametro imposta dimensioni hello di ogni reducer.  Per impostazione predefinita, ogni riduttore ha una dimensione di 256 MB.  

## <a name="guidance"></a>Indicazioni

**Impostare hive.exec.reducer.bytes.per.reducer** : valore predefinito di hello funziona bene quando i dati di hello non compressi.  Per i dati compressi, si dovrebbero ridurre dimensioni hello del reducer hello.  

**Set hive.tez.container.size**: in ciascun nodo, la memoria viene specificata da yarn.nodemanager.resource.memory-mb e dovrebbe essere impostata correttamente nel cluster HDI per impostazione predefinita.  Per ulteriori informazioni sull'impostazione hello appropriata per la memoria in YARN, vedere questo [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

I carichi di lavoro con utilizzo intensivo dei / o possono trarre vantaggio dal parallelismo riducendo la dimensione del contenitore Tez hello. In questo modo utente hello più contenitori di cui aumenta la concorrenza.  Tuttavia, alcune query di Hive richiedono una notevole quantità di memoria (ad esempio MapJoin).  Se l'attività hello non dispone di sufficiente memoria, si otterrà un'eccezione di memoria insufficiente durante il runtime.  Se si ricevono eccezioni di memoria insufficiente, è necessario aumentare la memoria hello.   

numero di simultanee Hello parallelismo delle attività in esecuzione verrà associato per la memoria YARN totale hello.  numero di Hello di contenitori YARN indicherà il numero di attività simultanee è possibile eseguire.  memoria YARN toofind hello per ogni nodo, è possibile passare tooAmbari.  Passare tooYARN e visualizzare scheda configurazioni hello.  memoria YARN Hello viene visualizzato in questa finestra.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
le prestazioni di chiave tooimproving Hello usando ADLS sono concorrenza hello tooincrease quanto possibile.  Tez calcola automaticamente il numero di hello di attività che devono essere creati in modo non è necessario tooset è.   

## <a name="example-calculation"></a>Calcolo di esempio

Si supponga di disporre di un cluster D14 a 8 nodi.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Limitazioni
**Limitazione di Azure Data Lake Store** 

UIf si riscontra hello Limita larghezza di banda fornita da ADLS, iniziare toosee errori di attività. Ciò può essere constatato verificando la presenza di errori di limitazione nei log delle attività.  È possibile ridurre il parallelismo hello mediante l'aumento delle dimensioni del contenitore Tez.  Se occorre maggiore concorrenza per il processo, contattare Microsoft.   

toocheck se sono recupero limitate, è necessario il debug di hello tooenable registrazione sul lato client hello. Di seguito viene indicato come procedere:

1. Inserire hello seguente proprietà nelle proprietà log4j hello nella configurazione di Hive. Questa operazione può essere eseguita dalla vista Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG riavviare tutti i nodi di hello/servizio per effetto di tootake configurazione hello.

2. Se sono recupero limitate, codice di errore HTTP 429 hello nel file di log hive hello verrà visualizzato. file di log hive Hello è /tmp/&lt;utente&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Ulteriori informazioni sull'ottimizzazione di Hive

Ecco alcuni articoli di blog che consentiranno di ottimizzare le query di Hive:
* [Ottimizzare le query Hive per Hadoop in HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Risoluzione dei problemi di prestazioni delle query Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Discussione Ignite sull'ottimizzazione di Hive in HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
