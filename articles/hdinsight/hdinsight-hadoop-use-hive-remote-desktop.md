---
title: aaaUse Hadoop Hive e Desktop remoto in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come cluster di tooconnect tooHadoop in HDInsight mediante Desktop remoto e quindi eseguire le query Hive usando hello Hive interfaccia della riga di comando.
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
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="b9ac3-103">Uso di Hive con Hadoop in HDInsight con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b9ac3-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="b9ac3-104">In questo articolo si apprenderà come tooconnect tooan HDInsight cluster tramite Desktop remoto e quindi eseguire Hive esegue una query utilizzando hello Hive interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="b9ac3-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9ac3-105">Desktop remoto è disponibile solo nei cluster HDInsight che usa Windows come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="b9ac3-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b9ac3-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b9ac3-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="b9ac3-108">Per HDInsight 3.4 o successiva, vedere [utilizzare Hive con HDInsight e Beeline](hdinsight-hadoop-use-hive-beeline.md) per informazioni sull'esecuzione di query Hive direttamente nel cluster hello dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="b9ac3-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9ac3-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="b9ac3-110">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="b9ac3-111">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="b9ac3-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="b9ac3-112">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="b9ac3-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="b9ac3-113"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b9ac3-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="b9ac3-114">Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="b9ac3-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="b9ac3-115"><a id="hive"></a>Utilizzare il comando di Hive hello</span><span class="sxs-lookup"><span data-stu-id="b9ac3-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="b9ac3-116">Quando si è connessi toohello desktop per il cluster HDInsight hello, usare hello seguendo i passaggi toowork con Hive:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="b9ac3-117">Dal desktop di HDInsight hello, avviare hello **della riga di comando Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="b9ac3-118">Immettere hello hello toostart comando CLI Hive seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="b9ac3-119">Quando è stata avviata hello CLI, verrà visualizzato il prompt di Hive CLI hello: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="b9ac3-120">Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **log4jLogs** utilizzando dati di esempio:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="b9ac3-121">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="b9ac3-122">**DROP TABLE**: Elimina tabella hello e file di dati hello hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="b9ac3-123">**CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="b9ac3-124">Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive (Buongiorno dati viene lasciati nella posizione originale hello).</span><span class="sxs-lookup"><span data-stu-id="b9ac3-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="b9ac3-125">Tabelle esterne devono essere utilizzate quando si prevede di hello toobe dati aggiornati da un'origine esterna (ad esempio, un processo di caricamento automatico dei dati) o da un'altra operazione MapReduce sottostante, ma è sempre che dati più recenti di hello toouse una query Hive.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="b9ac3-126">Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="b9ac3-127">**FORMATO di riga**: indica Hive formattazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="b9ac3-128">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="b9ac3-129">**ARCHIVIATO come file di testo percorso**: indica Hive in cui si hello dati archiviati (directory dati di esempio/hello) e a cui è archiviato come testo.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="b9ac3-130">**Selezionare**: seleziona un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="b9ac3-131">Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="b9ac3-132">**INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="b9ac3-133">Questo limita hello ricerca toohello sample.log file contenente dati hello e si impedisce la restituzione di dati da altri esempio i file di dati che non corrispondono allo schema di hello che è definiti.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="b9ac3-134">Hello utilizzare seguendo le istruzioni toocreate 'internal' nuova tabella denominata **degli errori**:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="b9ac3-135">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="b9ac3-136">**CREATE TABLE IF NOT EXISTS**: crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="b9ac3-137">Poiché hello **esterno** parola chiave non viene usato, si tratta di una tabella interna, che viene archiviata nel data warehouse di hello Hive e completamente gestita da Hive.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b9ac3-138">A differenza di **esterno** tabelle, anche l'eliminazione di una tabella interna Elimina hello dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="b9ac3-139">**ARCHIVIATI AS ORC**: archivia i dati di hello in formato a colonne (ORC) con ottimizzazione per la riga.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="b9ac3-140">Questo è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="b9ac3-141">**INSERT OVERWRITE ... Selezionare**: Seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="b9ac3-142">tooverify che solo le righe che contengono **[errore]** nella colonna t4 sono stata archiviata toohello **degli errori** tabella, utilizzare hello seguente istruzione tooreturn tutte le righe di hello **degli errori**:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="b9ac3-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="b9ac3-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="b9ac3-144">Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="b9ac3-145"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b9ac3-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="b9ac3-146">Come si può notare, hello hello comando Hive fornisce toointeractively un modo più semplice eseguire query Hive in un cluster HDInsight, hello di monitoraggio dello stato del processo e recuperare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="b9ac3-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="b9ac3-147"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9ac3-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b9ac3-148">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="b9ac3-149">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9ac3-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="b9ac3-150">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b9ac3-151">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9ac3-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b9ac3-152">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9ac3-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="b9ac3-153">Se si utilizza Tez con Hive, vedere hello documenti per le informazioni di debug seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9ac3-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="b9ac3-154">Utilizzare hello Tez UI in HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="b9ac3-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="b9ac3-155">Utilizzare hello vista Ambari Tez in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="b9ac3-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
