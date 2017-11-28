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
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="60fb4-105">Utilizzare il client di Beeline hello con Apache Hive</span><span class="sxs-lookup"><span data-stu-id="60fb4-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="60fb4-106">Informazioni su come toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) query toorun Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="60fb4-107">Beeline è un client di Hive che è incluso nei nodi head di hello del cluster di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="60fb4-108">Beeline utilizza JDBC tooconnect tooHiveServer2, un servizio ospitato nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="60fb4-109">È inoltre possibile utilizzare in modalità remota in Beeline tooaccess Hive in HDInsight hello internet.</span><span class="sxs-lookup"><span data-stu-id="60fb4-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="60fb4-110">Hello nella tabella seguente fornisce le stringhe di connessione per l'utilizzo con Beeline:</span><span class="sxs-lookup"><span data-stu-id="60fb4-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="60fb4-111">Esecuzione di Beeline da</span><span class="sxs-lookup"><span data-stu-id="60fb4-111">Where you run Beeline from</span></span> | <span data-ttu-id="60fb4-112">parameters</span><span class="sxs-lookup"><span data-stu-id="60fb4-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60fb4-113">Un SSH tooa nodo head o edge nodo connessione</span><span class="sxs-lookup"><span data-stu-id="60fb4-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="60fb4-114">Cluster hello esterno</span><span class="sxs-lookup"><span data-stu-id="60fb4-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="60fb4-115">Sostituire `admin` con account di accesso hello cluster per il cluster.</span><span class="sxs-lookup"><span data-stu-id="60fb4-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="60fb4-116">Sostituire `password` con password hello per account di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="60fb4-117">Sostituire `clustername` con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="60fb4-118"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60fb4-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="60fb4-119">Un cluster Hadoop basato su Linux in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="60fb4-120">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="60fb4-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="60fb4-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="60fb4-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="60fb4-122">Un client SSH o un client Beeline locale.</span><span class="sxs-lookup"><span data-stu-id="60fb4-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="60fb4-123">La maggior parte dei passaggi di hello in questo documento si presuppone che si utilizza Beeline da un cluster di toohello sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="60fb4-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="60fb4-124">Per informazioni sull'esecuzione Beeline dal cluster hello esterno, vedere hello [utilizzati in remoto Beeline](#remote) sezione.</span><span class="sxs-lookup"><span data-stu-id="60fb4-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="60fb4-125">Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="60fb4-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="60fb4-126"><a id="beeline"></a>Usare Beeline</span><span class="sxs-lookup"><span data-stu-id="60fb4-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="60fb4-127">Quando si avvia Beeline, è necessario fornire una stringa di connessione per HiveServer2 nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="60fb4-128">comando di hello toorun dal cluster hello esterno, è necessario fornire anche nome account di accesso cluster hello (impostazione predefinita `admin`) e la password.</span><span class="sxs-lookup"><span data-stu-id="60fb4-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="60fb4-129">Utilizzare hello tabella toofind hello connessione stringa formato e i parametri toouse seguenti:</span><span class="sxs-lookup"><span data-stu-id="60fb4-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="60fb4-130">Esecuzione di Beeline da</span><span class="sxs-lookup"><span data-stu-id="60fb4-130">Where you run Beeline from</span></span> | <span data-ttu-id="60fb4-131">parameters</span><span class="sxs-lookup"><span data-stu-id="60fb4-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="60fb4-132">Un SSH tooa nodo head o edge nodo connessione</span><span class="sxs-lookup"><span data-stu-id="60fb4-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="60fb4-133">Cluster hello esterno</span><span class="sxs-lookup"><span data-stu-id="60fb4-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="60fb4-134">Ad esempio, hello comando seguente può essere utilizzato toostart Beeline da un cluster di toohello sessione SSH:</span><span class="sxs-lookup"><span data-stu-id="60fb4-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="60fb4-135">Questo comando Avvia hello Beeline client e si connette tooHiveServer2 nel nodo head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="60fb4-136">Al termine del comando hello, verrà visualizzato un `jdbc:hive2://headnodehost:10001/>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="60fb4-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="60fb4-137">I comandi di Beeline iniziano di solito con un carattere `!`, ad esempio `!help` visualizza la Guida.</span><span class="sxs-lookup"><span data-stu-id="60fb4-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="60fb4-138">Tuttavia hello `!` può essere omesso per alcuni comandi.</span><span class="sxs-lookup"><span data-stu-id="60fb4-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="60fb4-139">Ad esempio, anche `help` funziona.</span><span class="sxs-lookup"><span data-stu-id="60fb4-139">For example, `help` also works.</span></span>

    <span data-ttu-id="60fb4-140">È presente un `!sql`, che viene utilizzato tooexecute istruzioni HiveQL.</span><span class="sxs-lookup"><span data-stu-id="60fb4-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="60fb4-141">Tuttavia, HiveQL viene comunemente usata che è possibile omettere hello precedente `!sql`.</span><span class="sxs-lookup"><span data-stu-id="60fb4-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="60fb4-142">Hello due istruzioni seguenti sono equivalente:</span><span class="sxs-lookup"><span data-stu-id="60fb4-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="60fb4-143">In un nuovo cluster viene elencata solo una tabella: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="60fb4-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="60fb4-144">Comando che segue di hello utilizzare schema hello toodisplay per hivesampletable hello:</span><span class="sxs-lookup"><span data-stu-id="60fb4-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="60fb4-145">Questo comando restituisce hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="60fb4-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="60fb4-146">Vengono descritte le colonne di hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="60fb4-147">Mentre è stato possibile eseguire alcune query sui dati, ma creare un nuovo toodemonstrate tabella come dati tooload in Hive e applicare uno schema.</span><span class="sxs-lookup"><span data-stu-id="60fb4-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="60fb4-148">Immettere hello seguendo le istruzioni toocreate una tabella denominata **log4jLogs** utilizzando dati di esempio forniti con i cluster di HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="60fb4-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="60fb4-149">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="60fb4-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="60fb4-150">`DROP TABLE`-Se hello tabella esiste, viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="60fb4-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="60fb4-151">`CREATE EXTERNAL TABLE`: crea una tabella **esterna** in Hive.</span><span class="sxs-lookup"><span data-stu-id="60fb4-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="60fb4-152">Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive.</span><span class="sxs-lookup"><span data-stu-id="60fb4-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="60fb4-153">dati Hello viene lasciati nella posizione originale hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="60fb4-154">`ROW FORMAT`-Modalità hello di formattazione.</span><span class="sxs-lookup"><span data-stu-id="60fb4-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="60fb4-155">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="60fb4-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="60fb4-156">`STORED AS TEXTFILE LOCATION`-In cui vengono archiviati hello e nel quale formato di file.</span><span class="sxs-lookup"><span data-stu-id="60fb4-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="60fb4-157">`SELECT`-Consente di selezionare un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="60fb4-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="60fb4-158">Questa query restituisce **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="60fb4-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="60fb4-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply hello tooall nei file di schema directory hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="60fb4-160">In questo caso, la directory hello contiene file che non corrispondono allo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="60fb4-161">tooprevent i dati errati nei risultati di hello, questa istruzione indica di Hive che si dovrebbe restituire solo dati da file che terminano con. log.</span><span class="sxs-lookup"><span data-stu-id="60fb4-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="60fb4-162">Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="60fb4-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="60fb4-163">Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="60fb4-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="60fb4-164">Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="60fb4-165">Hello l'output di questo comando è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="60fb4-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="60fb4-166">Utilizzare tooexit Beeline, `!exit`.</span><span class="sxs-lookup"><span data-stu-id="60fb4-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="60fb4-167"><a id="file"></a>Utilizzare Beeline toorun un file HiveQL</span><span class="sxs-lookup"><span data-stu-id="60fb4-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="60fb4-168">Utilizzare hello seguendo i passaggi toocreate un file, quindi eseguirlo tramite Beeline.</span><span class="sxs-lookup"><span data-stu-id="60fb4-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="60fb4-169">Comando che segue hello utilizzare toocreate un file denominato **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="60fb4-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="60fb4-170">Utilizzare hello segue testo come contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="60fb4-171">Questa query crea una nuova tabella "interna" denominata **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="60fb4-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="60fb4-172">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="60fb4-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="60fb4-173">**Crea tabella IF NOT EXISTS** -se la tabella hello non esiste già, viene creato.</span><span class="sxs-lookup"><span data-stu-id="60fb4-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="60fb4-174">Poiché hello **esterno** parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="60fb4-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="60fb4-175">Le tabelle interne vengono archiviate nel data warehouse di hello Hive e vengono gestite completamente dall'Hive.</span><span class="sxs-lookup"><span data-stu-id="60fb4-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="60fb4-176">**ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC).</span><span class="sxs-lookup"><span data-stu-id="60fb4-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="60fb4-177">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="60fb4-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="60fb4-178">**INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="60fb4-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="60fb4-179">A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="60fb4-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="60fb4-180">file hello toosave, usare **Ctrl**+**x**, quindi immettere **Y**e infine **invio**.</span><span class="sxs-lookup"><span data-stu-id="60fb4-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="60fb4-181">Utilizzare i seguenti file hello toorun utilizzando Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="60fb4-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="60fb4-182">Hello `-i` parametro Avvia Beeline, viene eseguito hello istruzioni nel file query.hql hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="60fb4-183">Al termine della query hello, verrà visualizzato hello `jdbc:hive2://headnodehost:10001/>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="60fb4-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="60fb4-184">È anche possibile eseguire un file utilizzando hello `-f` parametro, che viene chiuso Beeline dopo completamento della query hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="60fb4-185">tooverify che hello **degli errori** tabella è stata creata, utilizzare hello seguente istruzione tooreturn tutte le righe di hello **degli errori**:</span><span class="sxs-lookup"><span data-stu-id="60fb4-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="60fb4-186">Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.</span><span class="sxs-lookup"><span data-stu-id="60fb4-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="60fb4-187"><a id="remote"></a>Usare Beeline da remoto</span><span class="sxs-lookup"><span data-stu-id="60fb4-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="60fb4-188">Se si hanno Beeline installato localmente o si utilizza, ad esempio tramite un'immagine Docker [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), è necessario utilizzare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="60fb4-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="60fb4-189">__Stringa di connessione__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="60fb4-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="60fb4-190">__Nome account di accesso del cluster__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="60fb4-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="60fb4-191">__Password di accesso al cluster__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="60fb4-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="60fb4-192">Sostituire hello `clustername` nella stringa di connessione hello con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="60fb4-193">Sostituire `admin` con nome hello di account di accesso del cluster e sostituire `password` con password hello per l'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="60fb4-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="60fb4-194"><a id="sparksql"></a>Usare Beeline con Spark</span><span class="sxs-lookup"><span data-stu-id="60fb4-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="60fb4-195">Spark fornisce la propria implementazione di HiveServer2, che è spesso server Spark Thrift di cui tooas hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="60fb4-196">Questo servizio utilizza le query tooresolve Spark SQL anziché Hive e può fornire prestazioni migliori a seconda della query.</span><span class="sxs-lookup"><span data-stu-id="60fb4-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="60fb4-197">server Spark Thrift toohello di tooconnect di un Spark in cluster HDInsight, utilizzare porta `10002` anziché `10001`.</span><span class="sxs-lookup"><span data-stu-id="60fb4-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="60fb4-198">ad esempio `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="60fb4-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60fb4-199">server Spark Thrift Hello è non direttamente accessibile su internet di hello.</span><span class="sxs-lookup"><span data-stu-id="60fb4-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="60fb4-200">È possibile connettersi tooit da una sessione SSH o all'interno di hello stessa rete virtuale di Azure come hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60fb4-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="60fb4-201"><a id="summary"></a><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60fb4-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="60fb4-202">Per ulteriori informazioni generali su Hive in HDInsight, vedere hello seguente documento:</span><span class="sxs-lookup"><span data-stu-id="60fb4-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="60fb4-203">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60fb4-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="60fb4-204">Per ulteriori informazioni su altre modalità è possibile lavorare con Hadoop in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="60fb4-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="60fb4-205">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60fb4-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="60fb4-206">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60fb4-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="60fb4-207">Se si utilizza Tez con Hive, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="60fb4-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="60fb4-208">Utilizzare hello Tez UI in HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="60fb4-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="60fb4-209">Utilizzare hello vista Ambari Tez in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="60fb4-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
