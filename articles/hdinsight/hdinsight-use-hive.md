---
title: "aaaWhat è Apache Hive e HiveQL - HDInsight di Azure | Documenti Microsoft"
description: "Apache Hive è un sistema di data warehouse per Hadoop. È possibile eseguire query di dati archiviati nell'Hive tramite HiveQL, quali simile tooTransact-SQL. In questo documento, informazioni su come toouse Hive e HiveQL con Azure HDInsight."
keywords: "hiveql, novità hive, hiveql hadoop, hive, qual è l'hive di informazioni su come toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Cosa sono Apache Hive e HiveQL in Azure HDInsight

[Apache Hive](http://hive.apache.org/) è un sistema di data warehouse per Hadoop. Hive consente di eseguire attività di riepilogo, query e analisi dei dati. HiveQL, ovvero un linguaggio di query simili tooSQL sono scritte le query hive.

Hive consente tooproject struttura sui dati in larga misura non strutturati. Dopo aver definito una struttura di hello, è possibile utilizzare dati di hello tooquery HiveQL senza una conoscenza del linguaggio o MapReduce.

HDInsight offre diversi tipi di cluster ottimizzati per carichi di lavoro specifici. Hello seguenti tipi di cluster viene spesso usata per le query Hive:

* __Hive interattivo__: Hadoop A cluster che fornisce [bassa latenza Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) funzionalità tooimprove tempi di risposta query interattive. Per ulteriori informazioni, vedere hello [iniziano con interattivo Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.

* __Hadoop__: un cluster Hadoop che è ottimizzato per carichi di lavoro di elaborazione batch. Per ulteriori informazioni, vedere hello [avviare con Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.

* __Spark__: Apache Spark ha una funzionalità integrata per l'utilizzo di Hive. Per ulteriori informazioni, vedere hello [iniziano con Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.

* __HBase__: HiveQL può essere utilizzato tooquery dati archiviati in HBase. Per ulteriori informazioni, vedere hello [iniziano con HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.

## <a name="how-toouse-hive"></a>Come toouse Hive

Utilizzare hello toodiscover tabella come toouse Hive con HDInsight seguenti:

| **Usare questo metodo** se si vuole... | ...una shell **interattiva** | ...elaborazione**batch** | ...con questo **sistema operativo cluster** | ...da questo **sistema operativo client** |
|:--- |:---:|:---:|:--- |:--- |
| [Vista di Hive](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |Qualsiasi versione (basata su browser) |
| [Client Beeline](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [API REST](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux o Windows* |Linux, Unix, Mac OS X o Windows |
| [HDInsight Tools per Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux o Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux o Windows* |Windows |

> [!IMPORTANT]
> \*Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Se si utilizza un cluster HDInsight basati su Windows, è possibile utilizzare hello [console Query](hdinsight-hadoop-use-hive-query-console.md) dal browser o [Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md) query Hive toorun.

## <a name="hiveql-language-reference"></a>Informazioni di riferimento sul linguaggio HiveQL

Riferimenti al linguaggio HiveQL è disponibile in hello [manuale di linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive e la struttura dei dati

Hive interpreta come toowork con strutturato e dati semistrutturati. Ad esempio, file di testo in cui i campi di hello sono delimitati da caratteri specifici. Hello HiveQL istruzione crea una tabella dati delimitati da spazi:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive supporta inoltre **serializzatori/deserializzatori** personalizzati per dati complessi o strutturati in modo irregolare. Per ulteriori informazioni, vedere hello [come toouse un SerDe JSON personalizzato con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.

Per ulteriori informazioni sui formati di file supportati da Hive, vedere hello [manuale di linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Confronto tra le tabelle interne ed esterne di Hive

Con Hive è possibile creare due tipi di tabelle:

* __Interno__: dati vengono archiviati nel data warehouse di hello Hive. Hello del data warehouse si trova in `/hive/warehouse/` in spazio di archiviazione predefinito hello per cluster hello.

    Usare tabelle interne quando:

    * I dati sono temporanei.
    * Si desidera ciclo di vita di Hive toomanage hello della tabella di hello e dati.

* __Esterno__: dati vengono archiviati all'esterno di data warehouse di hello. dati Hello possono essere archiviati in tutte le archiviazioni accessibili dal cluster hello.

    Usare tabelle esterne quando:

    * dati Hello viene inoltre utilizzati all'esterno di Hive. Ad esempio, i file di dati hello vengono aggiornati da un altro processo (che non consente di bloccare file hello.)
    * I dati devono tooremain in hello sottostante posizione, anche dopo l'eliminazione di tabella hello.
    * È necessario un percorso personalizzato, ad esempio un account di archiviazione non predefinito.
    * Un programma diverso da hive gestisce il formato di dati di hello, posizione, e così via.

Per ulteriori informazioni, vedere hello [Hive interno e introduzione di tabelle esterno] [ cindygross-hive-tables] post di blog.

## <a name="user-defined-functions-udf"></a>Funzioni definite dall'utente (UDF)

Hive può anche essere esteso tramite **funzioni definite dall'utente (UDF)**, Una funzione definita dall'utente consente a funzionalità tooimplement o logica che non è facilmente modellata in HiveQL. Per un esempio di utilizzo di funzioni definite dall'utente con Hive, vedere hello seguenti documenti:

* [Usare una funzione Java definita dall'utente con Hive](hdinsight-hadoop-hive-java-udf.md)

* [Usare una funzione Python definita dall'utente con Hive e Pig](hdinsight-python.md)

* [Usare una funzione C# definita dall'utente con Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Funzionamento di tooHDInsight tooadd un Hive personalizzato definite dall'utente](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Un'esempio Hive funzione definita dall'utente tooconvert formati data/ora tooHive timestamp](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Dati di esempio

Hive in HDInsight include una tabella interna denominata `hivesampletable`. HDInsight offre inoltre set di dati di esempio che possono essere usati con Hive. Questi set di dati vengono archiviati in hello `/example/data` e `/HdiSamples` directory. Queste directory esistano nel servizio di archiviazione hello predefinito per il cluster.

## <a id="job"></a>Query Hive di esempio

Hello seguente HiveQL istruzioni progetto colonne hello `/example/data/sample.log` file:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

Nell'esempio precedente hello, le istruzioni HiveQL hello eseguono hello seguenti azioni:

* `set hive.execution.engine=tez;`: Set hello esecuzione motore toouse Tez. L'uso di Tez invece di MapReduce offre un aumento delle prestazioni delle query. Per ulteriori informazioni su Tez, vedere hello [Tez Apache utilizzo per migliorare le prestazioni](#usetez) sezione.

    > [!NOTE]
    > Questa istruzione è obbligatoria solo quando si usa un cluster HDInsight basato su Windows. Tez è di tipo motore di esecuzione predefinito hello per HDInsight basati su Linux.

* `DROP TABLE`: Se hello tabella esiste già, eliminarla.

* `CREATE EXTERNAL TABLE`: crea una nuova tabella **esterna** in Hive. Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive. dati Hello viene lasciati nella posizione originale hello e nel formato originale hello.

* `ROW FORMAT`: Indica la formattazione di dati hello Hive. In questo caso, i campi di hello in ogni log sono separati da uno spazio.

* `STORED AS TEXTFILE LOCATION`: Indica Hive dove hello memorizzati (hello `example/data` directory) e a cui è archiviato come testo. è possibile in un file o distribuiti tra più file all'interno di directory hello dati Hello.

* `SELECT`: Consente di selezionare un conteggio di tutte le righe in cui hello colonna **t4** contiene il valore di hello **[errore]**. L'istruzione restituisce un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply hello tooall nei file di schema directory hello. In questo caso, la directory hello contiene file che non corrispondono allo schema di hello. tooprevent i dati errati nei risultati di hello, questa istruzione indica di Hive che si dovrebbe restituire solo dati da file che terminano con. log.

> [!NOTE]
> Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna. Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.
>
> Eliminazione di una tabella esterna **non** eliminare i dati di hello, Elimina solo la definizione di tabella hello.

toocreate un **interno** tabella anziché esterno, usare hello HiveQL seguente:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Queste istruzioni consentono di eseguire hello seguenti azioni:

* `CREATE TABLE IF NOT EXISTS`: Se la tabella hello non esiste, crearla. Poiché hello **esterno** parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna. tabella Hello verrà archiviata nel data warehouse di hello Hive e completamente gestita da Hive.

* `STORED AS ORC`: Archivia dati hello in formato con ottimizzazione per la riga a colonne (ORC). ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.

* `INSERT OVERWRITE ... SELECT`: Consente di selezionare le righe da hello **log4jLogs** tabella che contiene **[errore]**, e quindi inserisce hello dati in hello **degli errori** tabella.

> [!NOTE]
> A differenza delle tabelle esterne, eliminazione di una tabella interna elimina anche i dati sottostanti hello.

## <a name="improve-hive-query-performance"></a>Ottimizzare le prestazioni delle query di Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) è un framework che consente alle applicazioni con utilizzo intensivo di dati, ad esempio Hive, toorun in modo più efficiente su larga scala. Tez è abilitata come impostazione predefinita per i cluster HDInsight basati su Linux.

> [!NOTE]
> Tez è attualmente disattivata per impostazione predefinita per i cluster HDInsight basati su Windows e deve essere abilitata. per una query Hive, è necessario impostare tootake sfruttare Tez, hello il valore seguente:
>
> `set hive.execution.engine=tez;`
>
> Tez è il motore predefinito hello per i cluster HDInsight basati su Linux.

Hello [Hive nei documenti di progettazione Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiene i dettagli sulle scelte di implementazione hello e le configurazioni di ottimizzazione.

tooaid eseguire il debug di processi viene eseguito utilizzando Tez, HDInsight fornisce hello segue le interfacce utente web che consentono di tooview dettagli dei processi Tez:

* [Utilizzare hello vista Ambari Tez in HDInsight basati su Linux](hdinsight-debug-ambari-tez-view.md)

* [Utilizzare hello Tez UI in HDInsight basati su Windows](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Low Latency Analytical Processing (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (o Live Long and Process) è una nuova funzionalità di Hive 2.0 che consente di mettere in cache le query in memoria. LLAP rende molto più veloce, le query di Hive troppo[x 26 più velocemente di quanto Hive 1. x in alcuni casi](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight fornisce LLAP hello Hive interattiva di tipo cluster. Per ulteriori informazioni, vedere hello [iniziano con Hive interattivo](hdinsight-hadoop-use-interactive-hive.md) documento.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Processi di Hive e SQL Server Integration Services

È possibile utilizzare SQL Server Integration Services (SSIS) toorun un processo Hive. Hello Azure Feature Pack per SSIS fornisce hello seguenti dei componenti che funzionano con i processi Hive in HDInsight.

* [Attività di Hive di Azure HDInsight][hivetask]

* [Gestione connessione della sottoscrizione di Azure][connectionmanager]

Altre informazioni su hello Azure Feature Pack per SSIS [qui][ssispack].

## <a id="nextsteps"></a>Passaggi successivi

Ora che si è appreso che cos'è Hive e come toouse con Hadoop in HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.

* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
