---
title: Usare Beeline con Apache Hive - Azure HDInsight | Microsoft Docs
description: "Informazioni su come usare il client Beeline per eseguire query Hive con Hadoop in HDInsight. Beeline è un'utilità per l'utilizzo di HiveServer2 rispetto a JDBC."
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
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="fbade-105">Usare il client Beeline con Apache Hive</span><span class="sxs-lookup"><span data-stu-id="fbade-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="fbade-106">Informazioni su come usare [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) per eseguire query Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="fbade-107">Beeline è un client Hive incluso nei nodi head del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="fbade-108">Beeline usa JDBC per connettersi a HiveServer2, un servizio ospitato nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="fbade-109">È anche possibile usare Beeline per accedere in remoto a Hive in HDInsight tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="fbade-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="fbade-110">Nella tabella seguente vengono elencate le stringhe di connessione da usare con Beeline:</span><span class="sxs-lookup"><span data-stu-id="fbade-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="fbade-111">Esecuzione di Beeline da</span><span class="sxs-lookup"><span data-stu-id="fbade-111">Where you run Beeline from</span></span> | <span data-ttu-id="fbade-112">Parametri</span><span class="sxs-lookup"><span data-stu-id="fbade-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fbade-113">Una connessione SSH a un nodo head o a un nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="fbade-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="fbade-114">All'esterno del cluster</span><span class="sxs-lookup"><span data-stu-id="fbade-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="fbade-115">Sostituire `admin` con l'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="fbade-116">Sostituire `password` con la password dell'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="fbade-117">Sostituire `clustername` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="fbade-118"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fbade-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="fbade-119">Un cluster Hadoop basato su Linux in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="fbade-120">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="fbade-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fbade-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fbade-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="fbade-122">Un client SSH o un client Beeline locale.</span><span class="sxs-lookup"><span data-stu-id="fbade-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="fbade-123">La maggior parte dei passaggi di questo documento presuppongono che si usi Beeline da una sessione SSH al cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="fbade-124">Per informazioni sull'esecuzione di Beeline dall'esterno del cluster, vedere la sezione sull'[uso di Beeline in remoto](#remote).</span><span class="sxs-lookup"><span data-stu-id="fbade-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="fbade-125">Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fbade-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="fbade-126"><a id="beeline"></a>Usare Beeline</span><span class="sxs-lookup"><span data-stu-id="fbade-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="fbade-127">Quando si avvia Beeline, è necessario fornire una stringa di connessione per HiveServer2 nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="fbade-128">Per eseguire il comando dall'esterno del cluster, è necessario fornire anche il nome account (predefinito: `admin`) e la password dell'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="fbade-129">Usare la tabella seguente per trovare il formato della stringa di connessione e i parametri da usare:</span><span class="sxs-lookup"><span data-stu-id="fbade-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="fbade-130">Esecuzione di Beeline da</span><span class="sxs-lookup"><span data-stu-id="fbade-130">Where you run Beeline from</span></span> | <span data-ttu-id="fbade-131">Parametri</span><span class="sxs-lookup"><span data-stu-id="fbade-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="fbade-132">Una connessione SSH a un nodo head o a un nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="fbade-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="fbade-133">All'esterno del cluster</span><span class="sxs-lookup"><span data-stu-id="fbade-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="fbade-134">Il comando seguente, ad esempio, può essere usato per avviare Beeline da una sessione SSH al cluster:</span><span class="sxs-lookup"><span data-stu-id="fbade-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="fbade-135">Questo comando avvia il client Beeline ed esegue la connessione a HiveServer2 nel nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="fbade-136">Al termine dell'esecuzione del comando, si aprirà il prompt `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="fbade-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="fbade-137">I comandi di Beeline iniziano di solito con un carattere `!`, ad esempio `!help` visualizza la Guida.</span><span class="sxs-lookup"><span data-stu-id="fbade-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="fbade-138">Tuttavia il carattere `!` può essere omesso per alcuni comandi.</span><span class="sxs-lookup"><span data-stu-id="fbade-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="fbade-139">Ad esempio, anche `help` funziona.</span><span class="sxs-lookup"><span data-stu-id="fbade-139">For example, `help` also works.</span></span>

    <span data-ttu-id="fbade-140">Il comando `!sql` consente di eseguire istruzioni HiveQL.</span><span class="sxs-lookup"><span data-stu-id="fbade-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="fbade-141">HiveQL è comunque così diffuso da poter omettere il precedente `!sql`.</span><span class="sxs-lookup"><span data-stu-id="fbade-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="fbade-142">Le due istruzioni seguenti sono equivalenti:</span><span class="sxs-lookup"><span data-stu-id="fbade-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="fbade-143">In un nuovo cluster viene elencata solo una tabella: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="fbade-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="fbade-144">Usare il comando seguente per visualizzare lo schema di hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="fbade-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="fbade-145">Questo comando restituisce le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fbade-145">This command returns the following information:</span></span>

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

    <span data-ttu-id="fbade-146">Tali informazioni descrivono le colonne nella tabella.</span><span class="sxs-lookup"><span data-stu-id="fbade-146">This information describes the columns in the table.</span></span> <span data-ttu-id="fbade-147">Anche se è possibile eseguire alcune query su questi dati, verrà creata una nuova tabella per dimostrare come caricare i dati in Hive e applicare uno schema.</span><span class="sxs-lookup"><span data-stu-id="fbade-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="fbade-148">Immettere le istruzioni seguenti per creare una tabella denominata **log4jLogs** usando i dati di esempio specificati con il cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="fbade-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="fbade-149">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="fbade-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="fbade-150">`DROP TABLE`: se la tabella esiste, viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="fbade-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="fbade-151">`CREATE EXTERNAL TABLE`: crea una tabella **esterna** in Hive.</span><span class="sxs-lookup"><span data-stu-id="fbade-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="fbade-152">Le tabelle esterne archiviano solo la definizione della tabella in Hive.</span><span class="sxs-lookup"><span data-stu-id="fbade-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="fbade-153">I dati rimangono nel percorso originale.</span><span class="sxs-lookup"><span data-stu-id="fbade-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="fbade-154">`ROW FORMAT`: indica il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="fbade-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="fbade-155">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="fbade-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="fbade-156">`STORED AS TEXTFILE LOCATION`: indica dove sono archiviati i dati e in quale formato di file.</span><span class="sxs-lookup"><span data-stu-id="fbade-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="fbade-157">`SELECT`: seleziona un conteggio di tutte le righe in cui la colonna **t4** include il valore **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="fbade-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="fbade-158">Questa query restituisce **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="fbade-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="fbade-159">`INPUT__FILE__NAME LIKE '%.log'`: Hive tenta di applicare lo schema a tutti i file della directory.</span><span class="sxs-lookup"><span data-stu-id="fbade-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="fbade-160">In questo caso la directory contiene file che non corrispondono allo schema.</span><span class="sxs-lookup"><span data-stu-id="fbade-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="fbade-161">Per evitare dati errati nei risultati, questa istruzione indica a Hive che devono essere restituiti dati solo da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="fbade-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fbade-162">Usa le tabelle esterne se si prevede che i dati sottostanti verranno aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="fbade-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="fbade-163">Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="fbade-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="fbade-164">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="fbade-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="fbade-165">L'output di questo comando è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="fbade-165">The output of this command is similar to the following text:</span></span>

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

5. <span data-ttu-id="fbade-166">Per uscire da Beeline, usare `!exit`.</span><span class="sxs-lookup"><span data-stu-id="fbade-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="fbade-167"><a id="file"></a>Usare Beeline per eseguire un file HiveQL</span><span class="sxs-lookup"><span data-stu-id="fbade-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="fbade-168">Usare la procedura seguente per creare un file, quindi eseguirlo tramite Beeline.</span><span class="sxs-lookup"><span data-stu-id="fbade-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="fbade-169">Usare il comando seguente per creare un file denominato **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="fbade-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="fbade-170">Usare il testo seguente come contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="fbade-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="fbade-171">Questa query crea una nuova tabella "interna" denominata **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="fbade-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="fbade-172">Le istruzioni eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="fbade-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="fbade-173">**CREATE TABLE IF NOT EXISTS**: crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="fbade-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="fbade-174">Poiché la parola chiave **EXTERNAL** non viene usata, questa istruzione crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="fbade-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="fbade-175">Le tabelle interne vengono archiviate nel data warehouse di Hive e sono totalmente gestite da Hive.</span><span class="sxs-lookup"><span data-stu-id="fbade-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="fbade-176">**STORED AS ORC** : archivia i dati nel formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="fbade-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="fbade-177">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="fbade-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="fbade-178">**INSERT OVERWRITE ... SELECT**: seleziona dalla tabella **log4jLogs** le righe contenenti **[ERROR]**, poi inserisce i dati nella tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="fbade-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbade-179">A differenza delle tabelle esterne, se si elimina una tabella interna, vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="fbade-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="fbade-180">Per salvare il file usare **Ctrl**+**_X**, quindi immettere **Y** e infine premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="fbade-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="fbade-181">Usare il codice seguente per eseguire il file tramite Beeline:</span><span class="sxs-lookup"><span data-stu-id="fbade-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="fbade-182">Il parametro `-i` avvia Beeline ed esegue le istruzioni nel file query.hql.</span><span class="sxs-lookup"><span data-stu-id="fbade-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="fbade-183">Dopo il completamento della query, viene visualizzato il prompt `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="fbade-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="fbade-184">È anche possibile eseguire un file usando il parametro `-f`, che chiude Beeline dopo il completamento della query.</span><span class="sxs-lookup"><span data-stu-id="fbade-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="fbade-185">Per verificare che la tabella **errorLogs** sia stata creata, usare l'istruzione seguente per restituire tutte le righe da **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="fbade-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="fbade-186">Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.</span><span class="sxs-lookup"><span data-stu-id="fbade-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="fbade-187"><a id="remote"></a>Usare Beeline da remoto</span><span class="sxs-lookup"><span data-stu-id="fbade-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="fbade-188">Se Beeline è installato localmente o se viene usato tramite un'immagine Docker, ad esempio [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), è necessario usare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="fbade-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="fbade-189">__Stringa di connessione__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="fbade-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="fbade-190">__Nome account di accesso del cluster__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="fbade-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="fbade-191">__Password di accesso al cluster__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="fbade-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="fbade-192">Sostituire `clustername` nella stringa di connessione con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="fbade-193">Sostituire `admin` con il nome dell'account di accesso del cluster e `password` con la password per l'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="fbade-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="fbade-194"><a id="sparksql"></a>Usare Beeline con Spark</span><span class="sxs-lookup"><span data-stu-id="fbade-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="fbade-195">Spark fornisce la propria implementazione di HiveServer2, spesso definita come server Spark Thrift.</span><span class="sxs-lookup"><span data-stu-id="fbade-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="fbade-196">Questo servizio usa Spark SQL invece di Hive per risolvere le query e può offrire prestazioni migliori a seconda della query.</span><span class="sxs-lookup"><span data-stu-id="fbade-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="fbade-197">Per connettersi al server Spark Thrift di un cluster Spark in HDInsight, usare la porta `10002` invece della `10001`.</span><span class="sxs-lookup"><span data-stu-id="fbade-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="fbade-198">Ad esempio: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="fbade-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbade-199">Il server Spark Thrift non è direttamente accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="fbade-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="fbade-200">È possibile connettersi solo da una sessione SSH o nella stessa rete virtuale di Azure del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbade-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="fbade-201"><a id="summary"></a><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fbade-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="fbade-202">Per informazioni più generali sull'uso di Hive con HDInsight, vedere il documento seguente:</span><span class="sxs-lookup"><span data-stu-id="fbade-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="fbade-203">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fbade-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="fbade-204">Per altre informazioni su come usare Hadoop con HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fbade-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="fbade-205">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fbade-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fbade-206">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fbade-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="fbade-207">Se si usa Tez con Hive, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fbade-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="fbade-208">Usare l'interfaccia utente di Tez in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="fbade-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="fbade-209">Usare la vista Ambari Tez in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="fbade-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
