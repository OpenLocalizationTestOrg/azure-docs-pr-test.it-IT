---
title: aaaUse Hadoop Hive nella Console di Query in HDInsight - Azure hello | Documenti Microsoft
description: Informazioni su come toouse hello basata sul web Console Query toorun query Hive in un HDInsight Hadoop cluster dal browser.
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
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="1d415-103">Esecuzione di query Hive utilizzando hello Console di Query</span><span class="sxs-lookup"><span data-stu-id="1d415-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="1d415-104">In questo articolo si apprenderà come query Hive in un HDInsight Hadoop toouse hello HDInsight Query Console toorun cluster dal browser.</span><span class="sxs-lookup"><span data-stu-id="1d415-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d415-105">Hello Console Query HDInsight è disponibile solo in cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1d415-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1d415-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1d415-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1d415-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1d415-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="1d415-108">Per HDInsight 3.4 o versione successiva, vedere [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) (Eseguire query Hive nella vista Ambari Hive) per informazioni sull'esecuzione di query Hive da un Web browser.</span><span class="sxs-lookup"><span data-stu-id="1d415-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="1d415-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d415-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="1d415-110">passaggi di hello toocomplete in questo articolo, sarà necessario seguente hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="1d415-111">Un cluster HDInsight Hadoop basato su Windows</span><span class="sxs-lookup"><span data-stu-id="1d415-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="1d415-112">Un Web browser moderno</span><span class="sxs-lookup"><span data-stu-id="1d415-112">A modern web browser</span></span>

## <span data-ttu-id="1d415-113"><a id="run"></a>Esecuzione di query Hive utilizzando hello Console di Query</span><span class="sxs-lookup"><span data-stu-id="1d415-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="1d415-114">Aprire un web browser e passare troppo**https://CLUSTERNAME.azurehdinsight.net**, dove **CLUSTERNAME** hello nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d415-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="1d415-115">Se richiesto, immettere nome utente hello e la password usata al momento della creazione del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="1d415-116">Selezionare i collegamenti hello nella parte superiore di hello della pagina hello, **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="1d415-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="1d415-117">Consente di visualizzare un form che può essere utilizzati tooenter hello HiveQL istruzioni che si desidera toorun nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![editor dell'hive Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="1d415-119">Sostituire il testo hello `Select * from hivesampletable` con hello seguendo le istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="1d415-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="1d415-120">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="1d415-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="1d415-121">**DROP TABLE**: Elimina tabella hello e file di dati hello hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="1d415-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="1d415-122">**CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="1d415-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="1d415-123">Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive; dati Hello viene lasciati nella posizione originale hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="1d415-124">Tabelle esterne devono essere utilizzate quando si prevede di hello toobe dati aggiornati da un'origine esterna (ad esempio, un processo di caricamento automatico dei dati) o da un'altra operazione MapReduce sottostante, ma è sempre che dati più recenti di hello toouse una query Hive.</span><span class="sxs-lookup"><span data-stu-id="1d415-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="1d415-125">Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="1d415-126">**FORMATO di riga**: indica Hive formattazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="1d415-127">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="1d415-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="1d415-128">**ARCHIVIATO come file di testo percorso**: indica Hive in cui si hello dati archiviati (directory dati di esempio/hello) e a cui è archiviato come testo</span><span class="sxs-lookup"><span data-stu-id="1d415-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="1d415-129">**Selezionare**: selezionare un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="1d415-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="1d415-130">Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="1d415-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="1d415-131">**INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="1d415-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="1d415-132">Questo limita hello ricerca toohello sample.log file contenente dati hello e si impedisce la restituzione di dati da altri esempio i file di dati che non corrispondono allo schema di hello che è definiti.</span><span class="sxs-lookup"><span data-stu-id="1d415-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="1d415-133">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1d415-133">Click **Submit**.</span></span> <span data-ttu-id="1d415-134">Hello **sessione del processo** in hello nella parte inferiore della pagina hello deve visualizzare i dettagli per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="1d415-135">Quando hello **stato** campo modifiche troppo**completato**selezionare **Visualizza dettagli** per processo hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="1d415-136">Nella pagina dettagli hello hello **Output processo** contiene `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="1d415-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="1d415-137">È possibile utilizzare hello **scaricare** pulsante sotto toodownload questo campo, un file che contiene l'output di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="1d415-138"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="1d415-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="1d415-139">Come si può notare, hello Console di Query fornisce un modo semplice di toorun esegue una query Hive in un cluster HDInsight, monitorare lo stato del processo hello e recuperare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="1d415-140">Selezionare toolearn ulteriori informazioni sull'utilizzo dei processi di Console di Query Hive toorun Hive, **Introduzione** nella parte superiore di hello di hello Console di Query, quindi utilizzare gli esempi di hello forniti.</span><span class="sxs-lookup"><span data-stu-id="1d415-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="1d415-141">Ogni esempio vengono illustrati il processo di hello dell'utilizzo di dati tooanalyze Hive, tra cui una spiegazione sulle istruzioni HiveQL hello utilizzate nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1d415-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="1d415-142"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d415-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="1d415-143">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1d415-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="1d415-144">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d415-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="1d415-145">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1d415-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1d415-146">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d415-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1d415-147">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d415-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1d415-148">Se si utilizza Tez con Hive, vedere hello documenti per le informazioni di debug seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d415-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="1d415-149">Utilizzare hello Tez UI in HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="1d415-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="1d415-150">Utilizzare hello vista Ambari Tez in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="1d415-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
