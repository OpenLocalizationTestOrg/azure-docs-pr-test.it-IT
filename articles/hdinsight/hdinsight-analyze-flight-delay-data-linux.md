---
title: dati del ritardo di volo aaaAnalyze con Hive in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse Hive dati volo tooanalyze in HDInsight basati su Linux, quindi esportare hello dati tooSQL utilizzando Sqoop del Database.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Analizzare i dati sui ritardi dei voli con Hive in HDInsight basato su Linux

Informazioni su come dati del ritardo di volo tooanalyze usando Hive in HDInsight basati su Linux, quindi esportano hello dati tooAzure Database SQL utilizzando Sqoop.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Prerequisiti

* **Un cluster HDInsight**. Per la procedura sulla creazione di un nuovo cluster HDInsight basato su Linux, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

* Un **database SQL di Azure**. Come archivio dati di destinazione usare un database SQL di Azure. Se non si ha già un database SQL, vedere l' [esercitazione sul database SQL per creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md).

* **Interfaccia della riga di comando di Azure**. Se non è stato installato hello CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) per più passaggi.

## <a name="download-hello-flight-data"></a>Il download dei dati di volo hello

1. Sfoglia troppo[Research e innovativa tecnologia amministrazione Bureau di statistiche trasporto][rita-website].

2. Nella pagina hello selezionare hello seguenti valori:

   | Nome | Valore |
   | --- | --- |
   | Filter Year |2013 |
   | Filter Period |January |
   | Fields |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Deselezionare tutti gli altri campi |

3. Fare clic su **Download**.

## <a name="upload-hello-data"></a>Caricare i dati di hello

1. Utilizzare hello comando tooupload hello zip file toohello HDInsight nodo head del cluster seguenti:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Sostituire **FILENAME** con nome hello del file zip hello. Sostituire **USERNAME** con account di accesso di hello SSH per il cluster HDInsight hello. Sostituire CLUSTERNAME con nome hello del cluster HDInsight hello.

   > [!NOTE]
   > Se si utilizza un tooauthenticate password l'account di accesso SSH, richiesto per la password di hello. Se si utilizza una chiave pubblica, potrebbe essere necessario hello toouse `-i` parametro e specificare toohello percorso hello corrispondente chiave privata. ad esempio `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Una volta completato il caricamento di hello, connettere il cluster di toohello tramite SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una volta connessi, utilizzare hello seguenti il file con estensione zip toounzip hello:

    ```
    unzip FILENAME.zip
    ```

    Questo comando estrae un file con estensione CSV di circa 60 MB.

4. Utilizzare hello seguire comando toocreate una directory di archiviazione di HDInsight e quindi copiare directory toohello del file hello:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Creare ed eseguire hello HiveQL

Utilizzare hello passaggi seguenti tooimport dati da file CSV hello in una tabella Hive denominata **ritardi**.

1. Seguente hello utilizzare comandi toocreate e modifica di un nuovo file denominato **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Utilizzare hello segue testo come contenuto di hello di questo file:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. file hello toosave, usare **Ctrl + X**, quindi **Y** .

3. toostart Hive e hello esecuzione **flightdelays.hql** , utilizzare hello comando seguente:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > In questo esempio, `localhost` viene utilizzato poiché si è connessi toohello nodo head del cluster HDInsight hello, ovvero in cui è in esecuzione HiveServer2.

4. Una volta hello __flightdelays.hql__ tooopen una sessione interattiva di Beeline mediante utilizzare hello seguente comando al termine dell'esecuzione di script:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Quando si riceve hello `jdbc:hive2://localhost:10001/>` prompt, usare hello seguente tooretrieve eseguire query sui dati dai dati di ritardo volo hello importato.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Questa query recupera un elenco di città che ritardo ritardi weather esperti, insieme a Media hello e salvarlo troppo`/tutorials/flightdelays/output`. In un secondo momento, Sqoop legge i dati di hello da questa posizione ed esportarlo tooAzure Database SQL.

6. Immettere tooexit Beeline, `!quit` al prompt dei comandi hello.

## <a name="create-a-sql-database"></a>Creare un database SQL

Se si dispone già di un Database SQL, è necessario ottenere il nome di server hello. È possibile trovare il nome di server hello in hello [portale di Azure](https://portal.azure.com) selezionando **database SQL**, e quindi il filtro sul nome hello di hello database che si desidera toouse. nome del server Hello è elencato nella hello **SERVER** colonna.

Se si dispone già di un Database SQL, utilizzare le informazioni di hello in [esercitazione Database SQL: creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md) toocreate uno. Salvare il nome di server hello utilizzato per il database hello.

## <a name="create-a-sql-database-table"></a>Creare una tabella del database SQL

> [!NOTE]
> Esistono molti modi tooconnect tooSQL Database e creare una tabella. Hello seguenti utilizzano [disporre di FreeTDS](http://www.freetds.org/) dal cluster HDInsight hello.


1. Utilizzare cluster HDInsight basati su Linux SSH tooconnect toohello e hello esecuzione seguendo i passaggi di una sessione SSH hello.

2. Utilizzare hello tooinstall comando disporre di FreeTDS seguenti:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Al termine dell'installazione di hello, utilizzare hello seguente server di Database SQL toohello tooconnect comando. Sostituire **serverName** con nome del server di Database SQL di hello. Sostituire **adminLogin** e **adminPassword** con account di accesso di hello per il Database SQL. Sostituire **databaseName** con il nome di database hello.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Viene visualizzato toohello simili di output il testo seguente:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. In hello `1>` richiesto, immettere hello seguenti righe:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate. Questa query crea una tabella denominata **delays**, con un indice cluster.

    Hello utilizzare query tooverify che hello nella tabella seguente è stata creata:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Hello l'output è simile toohello seguente testo:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.

## <a name="export-data-with-sqoop"></a>Esportare i dati con Sqoop

1. Comando che segue di hello utilizzare tooverify che Sqoop possa vedere il Database SQL:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Questo comando restituisce un elenco di database, incluso database hello tabella ritardi hello creato in precedenza.

2. Comando che segue di hello utilizzare dati tooexport hivesampletable toohello mobiledata tabella:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop Collega database toohello contenente hello ritardi tabella e l'esportazione di dati da hello `/tutorials/flightdelays/output` tabella ritardi toohello di directory.

3. Al termine del comando hello, usare hello tooconnect toohello database tramite TSQL seguente:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Una volta connessi, utilizzare hello tooverify istruzioni che dati hello è stato esportato toohello mobiledata nella tabella seguente:

    ```
    SELECT * FROM delays
    GO
    ```

    Verrà visualizzato un elenco di dati nella tabella hello. Tipo `exit` utilità di tooexit hello tsql.

## <a id="nextsteps"></a> Passaggi successivi

toolearn più toowork modi con i dati in HDInsight, vedere hello seguenti documenti:

* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Oozie con HDInsight][hdinsight-use-oozie]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]
* [Sviluppare programmi di streaming Hadoop in Python per HDInsight][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
