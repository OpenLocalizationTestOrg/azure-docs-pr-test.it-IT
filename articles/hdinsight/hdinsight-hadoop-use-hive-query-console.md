---
title: Usare Hive di Hadoop in Query Console in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare Query Console basata sul Web per eseguire query Hive in un cluster Hadoop di HDInsight dal browser.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="74425-103">Eseguire query Hive usando Query Console</span><span class="sxs-lookup"><span data-stu-id="74425-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="74425-104">In questo articolo si apprenderà come usare Query Console per eseguire query Hive in un cluster HDInsight Hadoop dal browser.</span><span class="sxs-lookup"><span data-stu-id="74425-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74425-105">Query Console di HDInsight è disponibile solo nei cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="74425-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="74425-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="74425-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="74425-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="74425-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="74425-108">Per HDInsight 3.4 o versione successiva, vedere [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) (Eseguire query Hive nella vista Ambari Hive) per informazioni sull'esecuzione di query Hive da un Web browser.</span><span class="sxs-lookup"><span data-stu-id="74425-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="74425-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="74425-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="74425-110">Per seguire la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="74425-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="74425-111">Un cluster HDInsight Hadoop basato su Windows</span><span class="sxs-lookup"><span data-stu-id="74425-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="74425-112">Un Web browser moderno</span><span class="sxs-lookup"><span data-stu-id="74425-112">A modern web browser</span></span>

## <span data-ttu-id="74425-113"><a id="run"></a> Eseguire query Hive usando Query Console</span><span class="sxs-lookup"><span data-stu-id="74425-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="74425-114">Aprire un Web browser e passare a **https://CLUSTERNAME.azurehdinsight.net**, dove **CLUSTERNAME** è il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74425-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="74425-115">Quando richiesto, immettere il nome utente e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="74425-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="74425-116">Nei collegamenti nella parte superiore della pagina fare clic su **Hive Editor**.</span><span class="sxs-lookup"><span data-stu-id="74425-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="74425-117">Verrà visualizzato un modulo che può essere usato per immettere le istruzioni HiveQL che si desidera eseguire nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74425-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![L'editor Hive](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="74425-119">Sostituire il testo `Select * from hivesampletable` con le seguenti istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="74425-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="74425-120">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="74425-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="74425-121">**DROP TABLE**: elimina la tabella e il file di dati, se la tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="74425-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="74425-122">**CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="74425-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="74425-123">Le tabelle esterne archiviano solo la definizione della tabella in Hive. I dati vengono lasciati nella posizione originale.</span><span class="sxs-lookup"><span data-stu-id="74425-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="74425-124">È consigliabile usare le tabelle esterne quando si prevede che i dati sottostanti vengano aggiornati da un'origine esterna, ad esempio un processo automatico di caricamento dei dati, oppure da un'altra operazione MapReduce, ma si vuole che le query Hive usino sempre i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="74425-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="74425-125">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="74425-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="74425-126">**ROW FORMAT**: indica a Hive il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="74425-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="74425-127">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="74425-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="74425-128">**STORED AS TEXTFILE LOCATION**: indica a Hive dove sono archiviati i dati (la directory example/data) e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="74425-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="74425-129">**SELECT**: seleziona il numero di tutte le righe in cui la colonna **t4** include il valore **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="74425-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="74425-130">Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="74425-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="74425-131">**INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="74425-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="74425-132">Questo limita la ricerca al file sample. log che contiene i dati, ed evita la restituzione di dati da altri file di dati di esempio che non corrispondono allo schema che è stato definito.</span><span class="sxs-lookup"><span data-stu-id="74425-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="74425-133">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="74425-133">Click **Submit**.</span></span> <span data-ttu-id="74425-134">L'opzione **Job Session** nella parte inferiore della pagina dovrebbe visualizzare i dettagli del processo.</span><span class="sxs-lookup"><span data-stu-id="74425-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="74425-135">Quando il campo **Status** (Stato) viene impostato su **Completed** (Operazione completata), fare clic su **View Details** (Visualizza dettagli) per il processo.</span><span class="sxs-lookup"><span data-stu-id="74425-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="74425-136">Nella pagina dei dettagli il campo **Job Output** (Output processo) contiene `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="74425-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="74425-137">È possibile usare il pulsante **Download** al di sotto di questo campo per scaricare un file contenente l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="74425-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="74425-138"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="74425-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="74425-139">Come è possibile notare, Query Console fornisce un modo semplice per eseguire query Hive in un cluster HDInsight, monitorare lo stato del processo e recuperare l'output.</span><span class="sxs-lookup"><span data-stu-id="74425-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="74425-140">Per altre informazioni sull'uso Query Console di Hive per eseguire processi Hive, fare clic su **Getting Started** nella parte superiore di Query Console, quindi usare gli esempi.</span><span class="sxs-lookup"><span data-stu-id="74425-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="74425-141">Ogni esempio illustra il processo di utilizzo di Hive per l'analisi dei dati, fornendo anche spiegazioni sulle istruzioni HiveQL usate nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="74425-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="74425-142"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74425-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="74425-143">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="74425-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="74425-144">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="74425-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="74425-145">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="74425-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="74425-146">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="74425-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="74425-147">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="74425-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="74425-148">Se si usa Tez con Hive, vedere i documenti seguenti per le informazioni di debug:</span><span class="sxs-lookup"><span data-stu-id="74425-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="74425-149">Usare l'interfaccia utente di Tez in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="74425-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="74425-150">Usare la vista Ambari Tez in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="74425-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
