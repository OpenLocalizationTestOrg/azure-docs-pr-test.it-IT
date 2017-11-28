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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="204e1-103">Analizzare i dati sui ritardi dei voli con Hive in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="204e1-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="204e1-104">Informazioni su come dati del ritardo di volo tooanalyze usando Hive in HDInsight basati su Linux, quindi esportano hello dati tooAzure Database SQL utilizzando Sqoop.</span><span class="sxs-lookup"><span data-stu-id="204e1-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="204e1-105">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="204e1-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="204e1-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="204e1-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="204e1-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="204e1-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="204e1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="204e1-108">Prerequisites</span></span>

* <span data-ttu-id="204e1-109">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="204e1-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="204e1-110">Per la procedura sulla creazione di un nuovo cluster HDInsight basato su Linux, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="204e1-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="204e1-111">Un **database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="204e1-111">**Azure SQL Database**.</span></span> <span data-ttu-id="204e1-112">Come archivio dati di destinazione usare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="204e1-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="204e1-113">Se non si ha già un database SQL, vedere l' [esercitazione sul database SQL per creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="204e1-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="204e1-114">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="204e1-114">**Azure CLI**.</span></span> <span data-ttu-id="204e1-115">Se non è stato installato hello CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) per più passaggi.</span><span class="sxs-lookup"><span data-stu-id="204e1-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="204e1-116">Il download dei dati di volo hello</span><span class="sxs-lookup"><span data-stu-id="204e1-116">Download hello flight data</span></span>

1. <span data-ttu-id="204e1-117">Sfoglia troppo[Research e innovativa tecnologia amministrazione Bureau di statistiche trasporto][rita-website].</span><span class="sxs-lookup"><span data-stu-id="204e1-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="204e1-118">Nella pagina hello selezionare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="204e1-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="204e1-119">Nome</span><span class="sxs-lookup"><span data-stu-id="204e1-119">Name</span></span> | <span data-ttu-id="204e1-120">Valore</span><span class="sxs-lookup"><span data-stu-id="204e1-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="204e1-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="204e1-121">Filter Year</span></span> |<span data-ttu-id="204e1-122">2013</span><span class="sxs-lookup"><span data-stu-id="204e1-122">2013</span></span> |
   | <span data-ttu-id="204e1-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="204e1-123">Filter Period</span></span> |<span data-ttu-id="204e1-124">January</span><span class="sxs-lookup"><span data-stu-id="204e1-124">January</span></span> |
   | <span data-ttu-id="204e1-125">Fields</span><span class="sxs-lookup"><span data-stu-id="204e1-125">Fields</span></span> |<span data-ttu-id="204e1-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="204e1-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="204e1-127">Deselezionare tutti gli altri campi</span><span class="sxs-lookup"><span data-stu-id="204e1-127">Clear all other fields</span></span> |

3. <span data-ttu-id="204e1-128">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="204e1-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="204e1-129">Caricare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="204e1-129">Upload hello data</span></span>

1. <span data-ttu-id="204e1-130">Utilizzare hello comando tooupload hello zip file toohello HDInsight nodo head del cluster seguenti:</span><span class="sxs-lookup"><span data-stu-id="204e1-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="204e1-131">Sostituire **FILENAME** con nome hello del file zip hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="204e1-132">Sostituire **USERNAME** con account di accesso di hello SSH per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="204e1-133">Sostituire CLUSTERNAME con nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="204e1-134">Se si utilizza un tooauthenticate password l'account di accesso SSH, richiesto per la password di hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="204e1-135">Se si utilizza una chiave pubblica, potrebbe essere necessario hello toouse `-i` parametro e specificare toohello percorso hello corrispondente chiave privata.</span><span class="sxs-lookup"><span data-stu-id="204e1-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="204e1-136">ad esempio `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="204e1-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="204e1-137">Una volta completato il caricamento di hello, connettere il cluster di toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="204e1-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="204e1-138">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="204e1-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="204e1-139">Una volta connessi, utilizzare hello seguenti il file con estensione zip toounzip hello:</span><span class="sxs-lookup"><span data-stu-id="204e1-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="204e1-140">Questo comando estrae un file con estensione CSV di circa 60 MB.</span><span class="sxs-lookup"><span data-stu-id="204e1-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="204e1-141">Utilizzare hello seguire comando toocreate una directory di archiviazione di HDInsight e quindi copiare directory toohello del file hello:</span><span class="sxs-lookup"><span data-stu-id="204e1-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="204e1-142">Creare ed eseguire hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="204e1-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="204e1-143">Utilizzare hello passaggi seguenti tooimport dati da file CSV hello in una tabella Hive denominata **ritardi**.</span><span class="sxs-lookup"><span data-stu-id="204e1-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="204e1-144">Seguente hello utilizzare comandi toocreate e modifica di un nuovo file denominato **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="204e1-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="204e1-145">Utilizzare hello segue testo come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="204e1-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="204e1-146">file hello toosave, usare **Ctrl + X**, quindi **Y** .</span><span class="sxs-lookup"><span data-stu-id="204e1-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="204e1-147">toostart Hive e hello esecuzione **flightdelays.hql** , utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="204e1-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="204e1-148">In questo esempio, `localhost` viene utilizzato poiché si è connessi toohello nodo head del cluster HDInsight hello, ovvero in cui è in esecuzione HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="204e1-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="204e1-149">Una volta hello __flightdelays.hql__ tooopen una sessione interattiva di Beeline mediante utilizzare hello seguente comando al termine dell'esecuzione di script:</span><span class="sxs-lookup"><span data-stu-id="204e1-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="204e1-150">Quando si riceve hello `jdbc:hive2://localhost:10001/>` prompt, usare hello seguente tooretrieve eseguire query sui dati dai dati di ritardo volo hello importato.</span><span class="sxs-lookup"><span data-stu-id="204e1-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="204e1-151">Questa query recupera un elenco di città che ritardo ritardi weather esperti, insieme a Media hello e salvarlo troppo`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="204e1-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="204e1-152">In un secondo momento, Sqoop legge i dati di hello da questa posizione ed esportarlo tooAzure Database SQL.</span><span class="sxs-lookup"><span data-stu-id="204e1-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="204e1-153">Immettere tooexit Beeline, `!quit` al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="204e1-154">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="204e1-154">Create a SQL Database</span></span>

<span data-ttu-id="204e1-155">Se si dispone già di un Database SQL, è necessario ottenere il nome di server hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="204e1-156">È possibile trovare il nome di server hello in hello [portale di Azure](https://portal.azure.com) selezionando **database SQL**, e quindi il filtro sul nome hello di hello database che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="204e1-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="204e1-157">nome del server Hello è elencato nella hello **SERVER** colonna.</span><span class="sxs-lookup"><span data-stu-id="204e1-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="204e1-158">Se si dispone già di un Database SQL, utilizzare le informazioni di hello in [esercitazione Database SQL: creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md) toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="204e1-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="204e1-159">Salvare il nome di server hello utilizzato per il database hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="204e1-160">Creare una tabella del database SQL</span><span class="sxs-lookup"><span data-stu-id="204e1-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="204e1-161">Esistono molti modi tooconnect tooSQL Database e creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="204e1-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="204e1-162">Hello seguenti utilizzano [disporre di FreeTDS](http://www.freetds.org/) dal cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="204e1-163">Utilizzare cluster HDInsight basati su Linux SSH tooconnect toohello e hello esecuzione seguendo i passaggi di una sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="204e1-164">Utilizzare hello tooinstall comando disporre di FreeTDS seguenti:</span><span class="sxs-lookup"><span data-stu-id="204e1-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="204e1-165">Al termine dell'installazione di hello, utilizzare hello seguente server di Database SQL toohello tooconnect comando.</span><span class="sxs-lookup"><span data-stu-id="204e1-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="204e1-166">Sostituire **serverName** con nome del server di Database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="204e1-167">Sostituire **adminLogin** e **adminPassword** con account di accesso di hello per il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="204e1-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="204e1-168">Sostituire **databaseName** con il nome di database hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="204e1-169">Viene visualizzato toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="204e1-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="204e1-170">In hello `1>` richiesto, immettere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="204e1-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="204e1-171">Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate.</span><span class="sxs-lookup"><span data-stu-id="204e1-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="204e1-172">Questa query crea una tabella denominata **delays**, con un indice cluster.</span><span class="sxs-lookup"><span data-stu-id="204e1-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="204e1-173">Hello utilizzare query tooverify che hello nella tabella seguente è stata creata:</span><span class="sxs-lookup"><span data-stu-id="204e1-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="204e1-174">Hello l'output è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="204e1-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="204e1-175">Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="204e1-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="204e1-176">Esportare i dati con Sqoop</span><span class="sxs-lookup"><span data-stu-id="204e1-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="204e1-177">Comando che segue di hello utilizzare tooverify che Sqoop possa vedere il Database SQL:</span><span class="sxs-lookup"><span data-stu-id="204e1-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="204e1-178">Questo comando restituisce un elenco di database, incluso database hello tabella ritardi hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="204e1-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="204e1-179">Comando che segue di hello utilizzare dati tooexport hivesampletable toohello mobiledata tabella:</span><span class="sxs-lookup"><span data-stu-id="204e1-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="204e1-180">Sqoop Collega database toohello contenente hello ritardi tabella e l'esportazione di dati da hello `/tutorials/flightdelays/output` tabella ritardi toohello di directory.</span><span class="sxs-lookup"><span data-stu-id="204e1-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="204e1-181">Al termine del comando hello, usare hello tooconnect toohello database tramite TSQL seguente:</span><span class="sxs-lookup"><span data-stu-id="204e1-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="204e1-182">Una volta connessi, utilizzare hello tooverify istruzioni che dati hello è stato esportato toohello mobiledata nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="204e1-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="204e1-183">Verrà visualizzato un elenco di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="204e1-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="204e1-184">Tipo `exit` utilità di tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="204e1-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="204e1-185"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="204e1-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="204e1-186">toolearn più toowork modi con i dati in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="204e1-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="204e1-187">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="204e1-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="204e1-188">[Usare Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="204e1-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="204e1-189">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="204e1-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="204e1-190">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="204e1-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="204e1-191">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="204e1-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="204e1-192">[Sviluppare programmi di streaming Hadoop in Python per HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="204e1-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
