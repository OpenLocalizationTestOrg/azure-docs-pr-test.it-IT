---
title: Usare Hive di Hadoop e Desktop remoto in HDInsight - Azure | Microsoft Docs
description: Informazioni su come connettersi a un cluster Hadoop in HDInsight tramite Desktop remoto e quindi eseguire query Hive usando l'interfaccia della riga di comando di Hive.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="97e40-103">Uso di Hive con Hadoop in HDInsight con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="97e40-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="97e40-104">In questo articolo si apprenderà come connettersi a un cluster HDInsight tramite Desktop remoto e quindi eseguire query Hive usando l'interfaccia della riga di comando di Hive.</span><span class="sxs-lookup"><span data-stu-id="97e40-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97e40-105">Desktop remoto è disponibile solo nei cluster HDInsight che usano Windows come sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="97e40-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="97e40-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="97e40-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="97e40-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="97e40-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="97e40-108">Per HDInsight 3.4 o versione successiva, vedere [Usare Hive con HDInsight e Beeline](hdinsight-hadoop-use-hive-beeline.md) per informazioni sull'esecuzione di query Hive direttamente sul cluster dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="97e40-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="97e40-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="97e40-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="97e40-110">Per seguire la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="97e40-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="97e40-111">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="97e40-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="97e40-112">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="97e40-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="97e40-113"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="97e40-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="97e40-114">Abilitare Desktop remoto per il cluster HDInsight e quindi connettersi seguendo le istruzioni disponibili in [Connettersi a cluster HDInsight tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="97e40-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="97e40-115"><a id="hive"></a>Usare il comando Hive</span><span class="sxs-lookup"><span data-stu-id="97e40-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="97e40-116">Una volta connessi al desktop per il cluster HDInsight, seguire questa procedura per l'uso con Hive:</span><span class="sxs-lookup"><span data-stu-id="97e40-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="97e40-117">Dal desktop di HDInsight avviare la **riga di comando di Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="97e40-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="97e40-118">Immettere il seguente comando per avviare l'interfaccia della riga di comando di Hive:</span><span class="sxs-lookup"><span data-stu-id="97e40-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="97e40-119">Dopo l'avvio dell'interfaccia della riga di comando, verrà visualizzato il prompt dell'interfaccia della riga di comando di Hive: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="97e40-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="97e40-120">Usando l'interfaccia della riga di comando, immettere le seguenti istruzioni per creare una nuova tabella denominata **log4jLogs** con i dati di esempio:</span><span class="sxs-lookup"><span data-stu-id="97e40-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="97e40-121">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="97e40-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="97e40-122">**DROP TABLE**: elimina la tabella e il file di dati, se la tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="97e40-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="97e40-123">**CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="97e40-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="97e40-124">Le tabelle esterne archiviano solo la definizione della tabella in Hive. I dati vengono lasciati nella posizione originale.</span><span class="sxs-lookup"><span data-stu-id="97e40-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="97e40-125">È consigliabile usare le tabelle esterne quando si prevede che i dati sottostanti vengano aggiornati da un'origine esterna, ad esempio un processo automatico di caricamento dei dati, oppure da un'altra operazione MapReduce, ma si vuole che le query Hive usino sempre i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="97e40-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="97e40-126">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="97e40-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="97e40-127">**ROW FORMAT**: indica a Hive il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="97e40-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="97e40-128">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="97e40-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="97e40-129">**STORED AS TEXTFILE LOCATION**: indica a Hive dove sono archiviati i dati (la directory example/data) e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="97e40-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="97e40-130">**SELECT**: seleziona un numero di tutte le righe in cui la colonna **t4** include il valore **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="97e40-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="97e40-131">Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="97e40-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="97e40-132">**INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="97e40-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="97e40-133">Questo limita la ricerca al file sample. log che contiene i dati, ed evita la restituzione di dati da altri file di dati di esempio che non corrispondono allo schema che è stato definito.</span><span class="sxs-lookup"><span data-stu-id="97e40-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="97e40-134">Usare le seguenti istruzioni per creare una nuova tabella "internal" denominata **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="97e40-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="97e40-135">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="97e40-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="97e40-136">**CREATE TABLE IF NOT EXISTS**: crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="97e40-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="97e40-137">Poiché non viene usata la parola chiave **EXTERNAL** , questa è una tabella interna che viene archiviata nel data warehouse di Hive e gestita completamente da Hive.</span><span class="sxs-lookup"><span data-stu-id="97e40-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="97e40-138">A differenza delle tabelle **EXTERNAL** , se si elimina una tabella interna, vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="97e40-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="97e40-139">**STORED AS ORC**: archivia i dati nel formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="97e40-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="97e40-140">Questo è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="97e40-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="97e40-141">**INSERT OVERWRITE ... SELECT**: seleziona dalla tabella **log4jLogs** le righe contenenti **[ERROR]**, quindi inserisce i dati nella tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="97e40-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="97e40-142">Per verificare che solo le righe contenenti **[ERROR]** nella colonna t4 siano state archiviate nella tabella **errorLogs**, usare l'istruzione seguente per restituire tutte le righe da **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="97e40-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="97e40-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="97e40-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="97e40-144">Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.</span><span class="sxs-lookup"><span data-stu-id="97e40-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="97e40-145"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="97e40-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="97e40-146">Come è possibile osservare, il comando Hive fornisce un modo semplice per eseguire query Hive in un cluster HDInsight, monitorare lo stato del processo e recuperare l'output in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="97e40-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="97e40-147"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97e40-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="97e40-148">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97e40-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="97e40-149">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97e40-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="97e40-150">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97e40-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="97e40-151">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97e40-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="97e40-152">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97e40-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="97e40-153">Se si usa Tez con Hive, vedere i documenti seguenti per le informazioni di debug:</span><span class="sxs-lookup"><span data-stu-id="97e40-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="97e40-154">Usare l'interfaccia utente di Tez in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="97e40-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="97e40-155">Usare la vista Ambari Tez in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="97e40-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
