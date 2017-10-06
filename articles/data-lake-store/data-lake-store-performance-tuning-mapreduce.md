---
title: aaaAzure Data Lake archivio MapReduce ottimizzazione linee guida | Documenti Microsoft
description: Linee guida per l'ottimizzazione delle prestazioni di MapReduce in Azure Data Lake Store
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Linee guida per l'ottimizzazione delle prestazioni di MapReduce in HDInsight e in Azure Data Lake Store


## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Assicurarsi di abilitare Desktop remoto per il cluster hello.
* **Uso di MapReduce in HDInsight**.  Per ulteriori informazioni, vedere [Usare MapReduce in Hadoop su HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Linee guida per l'ottimizzazione delle prestazioni in ADLS**.  Per i concetti generali relativi alle prestazioni, vedere [Linee guida per l'ottimizzazione delle prestazioni in Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>parameters

Quando si eseguono i processi di MapReduce, ecco i parametri di hello più importanti che è possibile configurare performance tooincrease su ADLS:

* **MapReduce.Map.Memory.MB** : quantità di hello di BizTalk mapper tooeach tooallocate di memoria
* **MapReduce.job.Maps** : hello numero di attività di mappa per processo
* **MapReduce** : quantità di hello di riduttore tooeach tooallocate di memoria
* **MapReduce.job.reduces** : hello numero di attività di riduzione per processo

**MapReduce.Map.Memory / Mapreduce.reduce.memory** questo numero deve essere regolato in base alle quantità di memoria è necessaria per la mappa hello e/o ridurre l'attività.  i valori predefiniti di Hello di mapreduce.map.memory e mapreduce.reduce.memory possono essere visualizzati in Ambari mediante la configurazione di Yarn hello.  In Ambari, passare tooYARN e visualizzarle scheda configurazioni hello.  verrà visualizzato Hello memoria YARN.  

**MapReduce.job.Maps / Mapreduce.job.reduces** per stabilire numero massimo di hello di BizTalk Mapper o riduttori toobe creato.  numero di Hello di divisioni determinerà il numero di BizTalk Mapper verrà creato per il processo MapReduce hello.  Pertanto, potrebbero essere meno BizTalk Mapper richiesto se sono presenti meno divisioni numero hello di BizTalk Mapper richiesto.       

## <a name="guidance"></a>Indicazioni

**Passaggio 1: Determinare il numero di processi in esecuzione** -per impostazione predefinita, MapReduce verrà utilizzato l'intero cluster hello per il processo.  È possibile utilizzare meno del cluster hello utilizzando meno BizTalk Mapper di quanti sono i contenitori disponibili.  materiale sussidiario Hello in questo documento si presuppone che l'applicazione hello unica applicazione in esecuzione nel cluster.      

**Passaggio 2: Impostare mapreduce.map.memory/mapreduce.reduce.memory** : dimensioni della memoria hello per mappa di hello e ridurre le attività saranno dipende il processo specifico.  Se si desidera tooincrease concorrenza, è possibile ridurre la dimensione della memoria hello.  numero di Hello delle attività in esecuzione contemporaneamente dipende dal numero di hello di contenitori.  Riducendo la quantità hello di memoria per ogni mapping o riduttore, possono creare più contenitori, che consentono più toorun di BizTalk Mapper o riduttori contemporaneamente.  Decrescente hello memoria troppo elevato può comportare alcuni toorun processi memoria insufficiente.  Se si verifica un errore di heap durante l'esecuzione del processo, è necessario aumentare la memoria hello al mapper o riduttore.  Si noti che l'aggiunta di contenitori può comportare un carico extra per ciascuno di questi ultimi, con una potenziale diminuzione delle prestazioni.  Un'altra alternativa è tooget maggiore quantità di memoria utilizzando un cluster con una maggiore quantità di memoria o aumentare il numero di hello nodi del cluster.  Quantità di memoria consentirà toobe contenitori più utilizzato, il che significa maggiore concorrenza.  

**Passaggio 3: Determinare la memoria totale YARN** -mapreduce.job.maps/mapreduce.job.reduces tootune, è necessario considerare hello quantità totale di YARN memoria disponibile per l'utilizzo.  Le informazioni sono disponibili in Ambari.  Passare tooYARN e visualizzare scheda configurazioni hello.  memoria YARN Hello viene visualizzato in questa finestra.  Si deve moltiplicare hello YARN di memoria con il numero di hello di nodi nel cluster tooget hello totale YARN memoria.

    Total YARN memory = nodes * YARN memory per node
Se si utilizza un cluster vuoto, della memoria può essere hello YARN memoria per il cluster.  Se altre applicazioni utilizzano memoria, è possibile scegliere una parte della memoria del cluster utilizzare tooonly riducendo il numero di hello di BizTalk Mapper o riduttori numero toohello di contenitori desideri toouse.  

**Passaggio 4: Calcolare il numero di contenitori YARN** : contenitori YARN prevedono quantità hello di concorrenza per il processo di hello.  Prendere il valore della memoria totale di YARN e dividerlo per mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Passaggio 5: Impostare mapreduce.job.maps/mapreduce.job.reduces** impostare mapreduce.job.maps/mapreduce.job.reduces tooat numero minimo di hello di contenitori disponibili.  È possibile provare a utilizzare ulteriore aumentando il numero di hello di BizTalk Mapper e riduttori toosee se ottenere prestazioni migliori.  Tenere presente comunque che l'aggiunta di mapper comporterà un carico extra. Un numero eccessivo di mapper potrà causare una diminuzione nelle prestazioni.  

Pianificazione della CPU e l'isolamento di CPU sono disattivate per impostazione predefinita, in modo hello numero di contenitori YARN è vincolato dalla memoria.

## <a name="example-calculation"></a>Calcolo di esempio

Si supponga che si dispone di un cluster costituito da 8 nodi D14 e si desidera toorun un processo con utilizzo intensivo dei / o.  Di seguito sono calcoli hello che è necessario eseguire:

**Passaggio 1: Determinare il numero di processi in esecuzione** -per questo esempio, si presuppone che il processo è hello unico in esecuzione.  

**Passaggio 2: configurare mapreduce.map.memory/mapreduce.reduce.memory**. Nell'esempio riportato si esegue un processo con attività di I/O intensive e si decide che sono sufficienti 3 GB di memoria per le attività di mapping.

    mapreduce.map.memory = 3GB
**Passaggio 3: determinare la memoria totale di YARN**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Passaggio 4: calcolare il numero dei contenitori YARN**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Passaggio 5: configurare mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Limitazioni

**Limitazione di Azure Data Lake Store**

In quanto servizio multi-tenant, ADLS imposta dei limiti di larghezza di banda a livello di account.  Se si riscontra questi limiti, si inizierà toosee errori di attività. Ciò può essere constatato verificando la presenza di errori di limitazione nei log delle attività.  Se occorre ulteriore larghezza di banda per il processo, contattare Microsoft.   

toocheck se sono recupero limitate, è necessario il debug di hello tooenable registrazione sul lato client hello. Di seguito viene indicato come procedere:

1. PUT hello seguenti proprietà nelle proprietà log4j hello Ambari > YARN > Configurazione > avanzate yarn log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Riavviare tutti i nodi di hello/servizio per effetto di tootake configurazione hello.

3. Se sono recupero limitate, codice di errore HTTP 429 hello nel file di log YARN hello verrà visualizzato. file di log YARN Hello è /tmp/&lt;utente&gt;/yarn.log

## <a name="examples-toorun"></a>Esempi tooRun

toodemonstrate come MapReduce viene eseguita in un archivio Azure Data Lake, di seguito è un codice di esempio che è stato eseguito in un cluster con hello seguenti impostazioni:

* D14v2 a 16 nodi
* Cluster Hadoop con HDI 3.6 in esecuzione

Per un punto di partenza, ecco alcuni toorun i comandi di esempio MapReduce Teragen Terasort e Teravalidate.  È possibile modificare questi comandi in base alle risorse.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
