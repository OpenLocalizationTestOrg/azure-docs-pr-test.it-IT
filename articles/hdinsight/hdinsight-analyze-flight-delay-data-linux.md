---
title: 'Analizzare i dati sui ritardi dei voli con Hive in HDInsight: Azure | Microsoft Docs'
description: Informazioni su come utilizzare Hive per analizzare i dati sui voli in HDInsight basato su Linux, e su come esportare i dati al database SQL mediante Sqoop.
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="052a1-103">Analizzare i dati sui ritardi dei voli con Hive in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="052a1-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="052a1-104">Informazioni su come analizzare i dati sui ritardi dei voli usando Hive in HDInsight basato su Linux, quindi su come esportare i dati nel database SQL di Azure mediante Sqoop.</span><span class="sxs-lookup"><span data-stu-id="052a1-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="052a1-105">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="052a1-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="052a1-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="052a1-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="052a1-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="052a1-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="052a1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="052a1-108">Prerequisites</span></span>

* <span data-ttu-id="052a1-109">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="052a1-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="052a1-110">Per la procedura sulla creazione di un nuovo cluster HDInsight basato su Linux, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="052a1-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="052a1-111">Un **database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="052a1-111">**Azure SQL Database**.</span></span> <span data-ttu-id="052a1-112">Come archivio dati di destinazione usare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="052a1-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="052a1-113">Se non si ha già un database SQL, vedere l' [esercitazione sul database SQL per creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="052a1-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="052a1-114">L'**interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="052a1-114">**Azure CLI**.</span></span> <span data-ttu-id="052a1-115">Se l'interfaccia della riga di comando di Azure non è installata, vedere l'articolo relativo all' [installazione e configurazione dell'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) per altri passaggi.</span><span class="sxs-lookup"><span data-stu-id="052a1-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="052a1-116">Scaricare i dati relativi ai voli</span><span class="sxs-lookup"><span data-stu-id="052a1-116">Download the flight data</span></span>

1. <span data-ttu-id="052a1-117">Passare alla pagina [Research and Innovative Technology Administration, Bureau of Transportation Statistics (RITA)][rita-website].</span><span class="sxs-lookup"><span data-stu-id="052a1-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="052a1-118">Selezionare i valori seguenti nella pagina:</span><span class="sxs-lookup"><span data-stu-id="052a1-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="052a1-119">Nome</span><span class="sxs-lookup"><span data-stu-id="052a1-119">Name</span></span> | <span data-ttu-id="052a1-120">Valore</span><span class="sxs-lookup"><span data-stu-id="052a1-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="052a1-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="052a1-121">Filter Year</span></span> |<span data-ttu-id="052a1-122">2013</span><span class="sxs-lookup"><span data-stu-id="052a1-122">2013</span></span> |
   | <span data-ttu-id="052a1-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="052a1-123">Filter Period</span></span> |<span data-ttu-id="052a1-124">January</span><span class="sxs-lookup"><span data-stu-id="052a1-124">January</span></span> |
   | <span data-ttu-id="052a1-125">Fields</span><span class="sxs-lookup"><span data-stu-id="052a1-125">Fields</span></span> |<span data-ttu-id="052a1-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="052a1-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="052a1-127">Deselezionare tutti gli altri campi</span><span class="sxs-lookup"><span data-stu-id="052a1-127">Clear all other fields</span></span> |

3. <span data-ttu-id="052a1-128">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="052a1-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="052a1-129">Caricare i dati</span><span class="sxs-lookup"><span data-stu-id="052a1-129">Upload the data</span></span>

1. <span data-ttu-id="052a1-130">Usare il comando seguente per caricare il file con estensione zip nel nodo head del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="052a1-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="052a1-131">Sostituire **FILENAME** con il nome del file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="052a1-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="052a1-132">Sostituire **USERNAME** con l'account di accesso SSH per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="052a1-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="052a1-133">Sostituire CLUSTERNAME con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="052a1-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="052a1-134">Se è stata usata una password per l'autenticazione a SSH, viene richiesto di specificarla.</span><span class="sxs-lookup"><span data-stu-id="052a1-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="052a1-135">Se è stata usata una chiave pubblica, può essere necessario usare il parametro `-i` e specificare il percorso alla chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="052a1-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="052a1-136">Ad esempio: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="052a1-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="052a1-137">Una volta completato il caricamento, connettersi al cluster tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="052a1-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="052a1-138">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="052a1-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="052a1-139">Dopo la connessione, usare il comando seguente per decomprimere il file con estensione zip:</span><span class="sxs-lookup"><span data-stu-id="052a1-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="052a1-140">Questo comando estrae un file con estensione CSV di circa 60 MB.</span><span class="sxs-lookup"><span data-stu-id="052a1-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="052a1-141">Usare il comando seguente per creare una directory nell'archivio di HDInsight e quindi copiare il file nella directory:</span><span class="sxs-lookup"><span data-stu-id="052a1-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="052a1-142">Creare ed eseguire HiveQL</span><span class="sxs-lookup"><span data-stu-id="052a1-142">Create and run the HiveQL</span></span>

<span data-ttu-id="052a1-143">Usare la procedura seguente per importare dati dal file con estensione csv in una tabella Hive denominata **Delays**.</span><span class="sxs-lookup"><span data-stu-id="052a1-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="052a1-144">Usare il comando seguente per creare e modificare un nuovo file denominato **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="052a1-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="052a1-145">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="052a1-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="052a1-146">Per salvare il file, usare **Ctrl + X** e quindi premere **Y**.</span><span class="sxs-lookup"><span data-stu-id="052a1-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="052a1-147">Per avviare Hive ed eseguire il file **flightdelays.hql**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="052a1-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="052a1-148">In questo esempio viene usato `localhost` dal momento che si è connessi al nodo head del cluster HDInsight, in cui HiveServer2 è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="052a1-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="052a1-149">Al termine dell'esecuzione dello script __flightdelays__, usare il comando seguente per aprire una sessione Beeline interattiva:</span><span class="sxs-lookup"><span data-stu-id="052a1-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="052a1-150">Quando si riceve il prompt di `jdbc:hive2://localhost:10001/>`, usare la query seguente per recuperare i dati dai dati sui ritardi dei voli importati.</span><span class="sxs-lookup"><span data-stu-id="052a1-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="052a1-151">Grazie a questa query viene recuperato un elenco di città in cui si sono verificati ritardi meteo e il tempo di ritardo medio che può essere salvato in `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="052a1-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="052a1-152">Sqoop legge in seguito i dati da questo percorso e li esporta nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="052a1-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="052a1-153">Per uscire da Beeline, immettere `!quit` al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="052a1-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="052a1-154">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="052a1-154">Create a SQL Database</span></span>

<span data-ttu-id="052a1-155">Se si dispone già di un database SQL, è necessario ottenere il nome del server.</span><span class="sxs-lookup"><span data-stu-id="052a1-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="052a1-156">È possibile trovare il nome del server nel [Portale di Azure](https://portal.azure.com) selezionando **Database SQL**e quindi filtrando il nome del database che si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="052a1-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="052a1-157">Il nome del server è elencato nella colonna **SERVER** .</span><span class="sxs-lookup"><span data-stu-id="052a1-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="052a1-158">Se non si dispone già di un database SQL, vedere le informazioni in [Esercitazione sul database SQL: Creare un database SQL in pochi minuti usando il portale di Azure](../sql-database/sql-database-get-started.md) per crearne uno.</span><span class="sxs-lookup"><span data-stu-id="052a1-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="052a1-159">Salvare il nome del server usato per il database.</span><span class="sxs-lookup"><span data-stu-id="052a1-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="052a1-160">Creare una tabella del database SQL</span><span class="sxs-lookup"><span data-stu-id="052a1-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="052a1-161">Sono disponibili diversi modi per connettersi al database SQL per creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="052a1-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="052a1-162">Nei seguenti passaggi viene usato [FreeTDS](http://www.freetds.org/) dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="052a1-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="052a1-163">Per connettersi al cluster HDInsight basato su Linux, usare SSH ed eseguire la procedura seguente dalla sessione di SSH.</span><span class="sxs-lookup"><span data-stu-id="052a1-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="052a1-164">Immettere il comando seguente per installare FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="052a1-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="052a1-165">Al termine dell'installazione, usare il comando seguente per connettersi al server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="052a1-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="052a1-166">Sostituire **serverName** con il nome server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="052a1-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="052a1-167">Sostituire **adminLogin** e **adminPassword** con le credenziali di accesso per il database SQL.</span><span class="sxs-lookup"><span data-stu-id="052a1-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="052a1-168">Sostituire **databaseName** con il nome del database.</span><span class="sxs-lookup"><span data-stu-id="052a1-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="052a1-169">L'output che si riceve è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="052a1-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="052a1-170">Al prompt di `1>` , immettere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="052a1-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="052a1-171">Dopo aver immesso l'istruzione `GO`, vengono valutate le istruzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="052a1-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="052a1-172">Questa query crea una tabella denominata **delays**, con un indice cluster.</span><span class="sxs-lookup"><span data-stu-id="052a1-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="052a1-173">Per verificare la corretta creazione della tabella, usare la query seguente:</span><span class="sxs-lookup"><span data-stu-id="052a1-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="052a1-174">L'output è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="052a1-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="052a1-175">Per uscire dall'utilità tsql, immettere `exit` al prompt di `1>`.</span><span class="sxs-lookup"><span data-stu-id="052a1-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="052a1-176">Esportare i dati con Sqoop</span><span class="sxs-lookup"><span data-stu-id="052a1-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="052a1-177">Usare il comando seguente per verificare che Sqoop possa visualizzare il database SQL:</span><span class="sxs-lookup"><span data-stu-id="052a1-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="052a1-178">Questo comando restituisce un elenco di database, compreso il database in cui è stata creata in precedenza la tabella Ritardi.</span><span class="sxs-lookup"><span data-stu-id="052a1-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="052a1-179">Usare il comando seguente per esportare dati dalla tabella hivesampletable alla tabella mobiledata:</span><span class="sxs-lookup"><span data-stu-id="052a1-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="052a1-180">Sqoop si connette al database contenente la tabella Ritardi ed esporta i dati dalla directory `/tutorials/flightdelays/output` alla tabella dei ritardi.</span><span class="sxs-lookup"><span data-stu-id="052a1-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="052a1-181">Al termine dell'esecuzione del comando, usare le informazioni seguenti per connettersi al database tramite TSQL:</span><span class="sxs-lookup"><span data-stu-id="052a1-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="052a1-182">Sopo la connessione, usare le istruzioni seguenti per verificare che i dati siano stati esportati nella tabella mobiledata:</span><span class="sxs-lookup"><span data-stu-id="052a1-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="052a1-183">Dovrebbe essere visualizzato un elenco di dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="052a1-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="052a1-184">Digitare `exit` per uscire dall'utilità tsql.</span><span class="sxs-lookup"><span data-stu-id="052a1-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="052a1-185"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="052a1-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="052a1-186">Per altre informazioni su come usare i dati in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="052a1-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="052a1-187">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="052a1-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="052a1-188">[Usare Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="052a1-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="052a1-189">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="052a1-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="052a1-190">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="052a1-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="052a1-191">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="052a1-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="052a1-192">[Sviluppare programmi di streaming Hadoop in Python per HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="052a1-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
