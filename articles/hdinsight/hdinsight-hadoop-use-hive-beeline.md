---
title: aaaUse Beeline con Apache Hive - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come viene eseguita una query toouse hello Beeline client toorun Hive con Hadoop in HDInsight. Beeline è un'utilità per l'utilizzo di HiveServer2 rispetto a JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Utilizzare il client di Beeline hello con Apache Hive

Informazioni su come toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) query toorun Hive in HDInsight.

Beeline è un client di Hive che è incluso nei nodi head di hello del cluster di HDInsight. Beeline utilizza JDBC tooconnect tooHiveServer2, un servizio ospitato nel cluster HDInsight. È inoltre possibile utilizzare in modalità remota in Beeline tooaccess Hive in HDInsight hello internet. Hello nella tabella seguente fornisce le stringhe di connessione per l'utilizzo con Beeline:

| Esecuzione di Beeline da | parameters |
| --- | --- | --- |
| Un SSH tooa nodo head o edge nodo connessione | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Cluster hello esterno | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Sostituire `admin` con account di accesso hello cluster per il cluster.
>
> Sostituire `password` con password hello per account di accesso cluster hello.
>
> Sostituire `clustername` con nome hello del cluster HDInsight.

## <a id="prereq"></a>Prerequisiti

* Un cluster Hadoop basato su Linux in HDInsight.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH o un client Beeline locale. La maggior parte dei passaggi di hello in questo documento si presuppone che si utilizza Beeline da un cluster di toohello sessione SSH. Per informazioni sull'esecuzione Beeline dal cluster hello esterno, vedere hello [utilizzati in remoto Beeline](#remote) sezione.

    Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Usare Beeline

1. Quando si avvia Beeline, è necessario fornire una stringa di connessione per HiveServer2 nel cluster HDInsight. comando di hello toorun dal cluster hello esterno, è necessario fornire anche nome account di accesso cluster hello (impostazione predefinita `admin`) e la password. Utilizzare hello tabella toofind hello connessione stringa formato e i parametri toouse seguenti:

    | Esecuzione di Beeline da | parameters |
    | --- | --- | --- |
    | Un SSH tooa nodo head o edge nodo connessione | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Cluster hello esterno | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Ad esempio, hello comando seguente può essere utilizzato toostart Beeline da un cluster di toohello sessione SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Questo comando Avvia hello Beeline client e si connette tooHiveServer2 nel nodo head del cluster hello. Al termine del comando hello, verrà visualizzato un `jdbc:hive2://headnodehost:10001/>` prompt dei comandi.

2. I comandi di Beeline iniziano di solito con un carattere `!`, ad esempio `!help` visualizza la Guida. Tuttavia hello `!` può essere omesso per alcuni comandi. Ad esempio, anche `help` funziona.

    È presente un `!sql`, che viene utilizzato tooexecute istruzioni HiveQL. Tuttavia, HiveQL viene comunemente usata che è possibile omettere hello precedente `!sql`. Hello due istruzioni seguenti sono equivalente:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    In un nuovo cluster viene elencata solo una tabella: **hivesampletable**.

3. Comando che segue di hello utilizzare schema hello toodisplay per hivesampletable hello:

    ```hiveql
    describe hivesampletable;
    ```

    Questo comando restituisce hello le seguenti informazioni:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Vengono descritte le colonne di hello nella tabella hello. Mentre è stato possibile eseguire alcune query sui dati, ma creare un nuovo toodemonstrate tabella come dati tooload in Hive e applicare uno schema.

4. Immettere hello seguendo le istruzioni toocreate una tabella denominata **log4jLogs** utilizzando dati di esempio forniti con i cluster di HDInsight hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

    * `DROP TABLE`-Se hello tabella esiste, viene eliminato.

    * `CREATE EXTERNAL TABLE`: crea una tabella **esterna** in Hive. Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive. dati Hello viene lasciati nella posizione originale hello.

    * `ROW FORMAT`-Modalità hello di formattazione. In questo caso, i campi di hello in ogni log sono separati da uno spazio.

    * `STORED AS TEXTFILE LOCATION`-In cui vengono archiviati hello e nel quale formato di file.

    * `SELECT`-Consente di selezionare un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**. Questa query restituisce **3**, poiché sono presenti tre righe contenenti questo valore.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply hello tooall nei file di schema directory hello. In questo caso, la directory hello contiene file che non corrispondono allo schema di hello. tooprevent i dati errati nei risultati di hello, questa istruzione indica di Hive che si dovrebbe restituire solo dati da file che terminano con. log.

  > [!NOTE]
  > Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna. Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.
  >
  > Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.

    Hello l'output di questo comando è simile toohello seguente testo:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. Utilizzare tooexit Beeline, `!exit`.

## <a id="file"></a>Utilizzare Beeline toorun un file HiveQL

Utilizzare hello seguendo i passaggi toocreate un file, quindi eseguirlo tramite Beeline.

1. Comando che segue hello utilizzare toocreate un file denominato **query.hql**:

    ```bash
    nano query.hql
    ```

2. Utilizzare hello segue testo come contenuto di hello del file hello. Questa query crea una nuova tabella "interna" denominata **errorLogs**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

    * **Crea tabella IF NOT EXISTS** -se la tabella hello non esiste già, viene creato. Poiché hello **esterno** parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna. Le tabelle interne vengono archiviate nel data warehouse di hello Hive e vengono gestite completamente dall'Hive.
    * **ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC). ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.
    * **INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.

    > [!NOTE]
    > A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.

3. file hello toosave, usare **Ctrl**+**x**, quindi immettere **Y**e infine **invio**.

4. Utilizzare i seguenti file hello toorun utilizzando Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Hello `-i` parametro Avvia Beeline, viene eseguito hello istruzioni nel file query.hql hello. Al termine della query hello, verrà visualizzato hello `jdbc:hive2://headnodehost:10001/>` prompt dei comandi. È anche possibile eseguire un file utilizzando hello `-f` parametro, che viene chiuso Beeline dopo completamento della query hello.

5. tooverify che hello **degli errori** tabella è stata creata, utilizzare hello seguente istruzione tooreturn tutte le righe di hello **degli errori**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Usare Beeline da remoto

Se si hanno Beeline installato localmente o si utilizza, ad esempio tramite un'immagine Docker [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), è necessario utilizzare hello seguenti parametri:

* __Stringa di connessione__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nome account di accesso del cluster__:`-n admin`

* __Password di accesso al cluster__ `-p 'password'`

Sostituire hello `clustername` nella stringa di connessione hello con nome hello del cluster HDInsight.

Sostituire `admin` con nome hello di account di accesso del cluster e sostituire `password` con password hello per l'account di accesso del cluster.

## <a id="sparksql"></a>Usare Beeline con Spark

Spark fornisce la propria implementazione di HiveServer2, che è spesso server Spark Thrift di cui tooas hello. Questo servizio utilizza le query tooresolve Spark SQL anziché Hive e può fornire prestazioni migliori a seconda della query.

server Spark Thrift toohello di tooconnect di un Spark in cluster HDInsight, utilizzare porta `10002` anziché `10001`. ad esempio `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> server Spark Thrift Hello è non direttamente accessibile su internet di hello. È possibile connettersi tooit da una sessione SSH o all'interno di hello stessa rete virtuale di Azure come hello cluster HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Passaggi successivi

Per ulteriori informazioni generali su Hive in HDInsight, vedere hello seguente documento:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per ulteriori informazioni su altre modalità è possibile lavorare con Hadoop in HDInsight, vedere hello seguenti documenti:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Se si utilizza Tez con Hive, vedere hello seguenti documenti:

* [Utilizzare hello Tez UI in HDInsight basati su Windows](hdinsight-debug-tez-ui.md)
* [Utilizzare hello vista Ambari Tez in HDInsight basati su Linux](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
