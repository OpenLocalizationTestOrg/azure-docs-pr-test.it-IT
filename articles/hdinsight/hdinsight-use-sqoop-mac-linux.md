---
title: aaaApache Sqoop con Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse tooimport Sqoop Apache e l'esportazione tra Hadoop in HDInsight e un Database di SQL Azure.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Utilizzare Apache Sqoop tooimport ed esportare dati tra Hadoop in HDInsight e il Database SQL

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Informazioni su come toouse Sqoop Apache tooimport ed esportazione tra un Hadoop cluster HDInsight di Azure e Database di SQL Azure o Microsoft SQL Server. passaggi di Hello hello di utilizzare questo documento `sqoop` direttamente dal nodo head hello del cluster Hadoop hello. Nodo head di SSH tooconnect toohello e di eseguire comandi hello in questo documento.

> [!IMPORTANT]
> Hello passaggi descritti in questo documento funzionano solo con i cluster HDInsight che utilizzano Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Installare FreeTDS

1. Utilizzare cluster di HDInsight toohello tooconnect SSH. Ad esempio, hello comando seguente si connette toohello nodo head primario di un cluster denominato `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilizzare hello tooinstall comando disporre di FreeTDS seguenti:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    Disporre di FreeTDS viene usato in vari passaggi tooconnect tooSQL Database.

## <a name="create-hello-table-in-sql-database"></a>Creare la tabella hello nel Database SQL

> [!IMPORTANT]
> Se si utilizza il cluster di HDInsight hello e Database SQL creato nel [creare cluster e il database SQL](hdinsight-use-sqoop.md), ignorare i passaggi di hello in questa sezione. Hello database e tabella sono stati creati i passaggi da parte di hello in hello [creare cluster e il database SQL](hdinsight-use-sqoop.md) documento.

1. Dalla sessione SSH hello, utilizzare hello seguente server di Database SQL toohello tooconnect comando.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Viene visualizzato toohello simili di output il testo seguente:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. In hello `1>` richiesto, immettere hello seguente query:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate. In primo luogo, hello **mobiledata** viene creata una tabella, quindi un indice cluster viene aggiunto tooit (obbligatorio dal Database SQL).

    Hello utilizzare query tooverify che hello nella tabella seguente è stata creata:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Vedrai toohello simili di output il testo seguente:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.

## <a name="sqoop-export"></a>Esportazione con Sqoop

1. Da cluster toohello connessione SSH hello utilizzare hello successivo comando tooverify che Sqoop possa vedere il Database SQL:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Quando richiesto, immettere la password di hello per l'accesso al Database SQL hello.

    Questo comando restituisce un elenco di database, tra cui hello **sqooptest** database creato in precedenza.

2. dati tooexport **hivesampletable** toohello **mobiledata** tabella, utilizzare hello comando seguente:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Questo comando indica Sqoop tooconnect toohello **sqooptest** database. Sqoop quindi Esporta dati da **wasb: / / / hive/warehouse/hivesampletable** toohello **mobiledata** tabella.

    > [!IMPORTANT]
    > Utilizzare `wasb:///` se hello predefinito per il cluster è un account di archiviazione di Azure. Usare `adl:///` se è un Azure Data Lake Store.

3. Al termine del comando hello, usare hello database toohello tooconnect di comando tramite TSQL seguente:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Una volta connessi, utilizzare hello seguente tooverify istruzioni che hello dati è stato esportato toohello **mobiledata** tabella:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Verrà visualizzato un elenco di dati nella tabella hello. Tipo `exit` utilità di tooexit hello tsql.

## <a name="sqoop-import"></a>Importazione con Sqoop

1. Comando che segue hello di utilizzare dati tooimport hello **mobiledata** tabella nel Database SQL, toohello **wasb: / / / esercitazioni/usesqoop/importeddata** directory HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    i campi di Hello nei dati hello sono separati da un carattere di tabulazione e righe hello vengono terminate da un carattere di nuova riga.

2. Una volta completata l'importazione di hello, utilizzare hello toolist comando dati hello nella nuova directory hello seguenti:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Uso di SQL Server

È inoltre possibile utilizzare Sqoop tooimport ed esportare dati da SQL Server, nel data center o in una macchina virtuale ospitata in Azure. Hello differenze tra l'utilizzo di Database SQL e SQL Server sono:

* HDInsight sia SQL Server deve essere in hello stessa rete virtuale di Azure.

    Per un esempio, vedere hello [rete locale di connettersi a HDInsight tooyour](./connect-on-premises-network.md) documento.

    Per ulteriori informazioni sull'uso di HDInsight con una rete virtuale di Azure, vedere hello [estendere HDInsight con la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento. Per ulteriori informazioni sulla rete virtuale di Azure, vedere hello [Panoramica di rete virtuale](../virtual-network/virtual-networks-overview.md) documento.

* SQL Server deve essere tooallow configurata l'autenticazione di SQL. Per ulteriori informazioni, vedere hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) documento.

* È possibile connessioni remote tooaccept di tooconfigure SQL Server. Per ulteriori informazioni, vedere hello [come motore di database tootroubleshoot toohello di connessione SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.

* Creare hello **sqooptest** database in SQL Server utilizzando un'utilità, ad esempio **SQL Server Management Studio** o **tsql**. procedura di Hello per l'utilizzo di hello CLI di Azure funziona solo per Database SQL di Azure.

    Hello utilizzare hello toocreate di istruzioni Transact-SQL seguente **mobiledata** tabella:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* Durante la connessione SQL Server toohello da HDInsight, è possibile indirizzo IP di hello toouse di hello SQL Server. ad esempio:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Limitazioni

* Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.

* Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop rende più inserimenti anziché l'invio in batch le operazioni di inserimento hello.

## <a name="next-steps"></a>Passaggi successivi

Ora si è appreso come toouse Sqoop. toolearn informazioni, vedere:

* [Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.
* [Analizzare i dati di ritardo volo tramite HDInsight][hdinsight-analyze-flight-data]: utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.
* [Caricare dati tooHDInsight][hdinsight-upload-data]: trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
