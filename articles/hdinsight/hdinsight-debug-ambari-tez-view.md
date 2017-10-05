---
title: Usare la visualizzazione Tez di Ambari con HDInsight - Azure | Microsoft Docs
description: Informazioni sull'uso della visualizzazione Tez di Ambari per il debug di processi Tez in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="cccb5-103">Usare le visualizzazioni di Ambari per il debug di processi Tez in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cccb5-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="cccb5-104">L'interfaccia utente Web di Ambari per HDInsight contiene una visualizzazione Tez che può essere usata per la comprensione e il debug di processi che usano Tez.</span><span class="sxs-lookup"><span data-stu-id="cccb5-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="cccb5-105">La visualizzazione Tez consente di visualizzare il processo come grafico di elementi connessi, esaminare ogni elemento e recuperare statistiche e informazioni sulla registrazione.</span><span class="sxs-lookup"><span data-stu-id="cccb5-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cccb5-106">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="cccb5-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cccb5-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="cccb5-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cccb5-108">Per altre informazioni, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cccb5-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cccb5-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cccb5-109">Prerequisites</span></span>

* <span data-ttu-id="cccb5-110">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="cccb5-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="cccb5-111">Per la procedura di creazione di un cluster, vedere [Esercitazione di Hadoop: Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cccb5-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="cccb5-112">Un moderno Web browser che supporta HTML5.</span><span class="sxs-lookup"><span data-stu-id="cccb5-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="cccb5-113">Informazioni su Tez</span><span class="sxs-lookup"><span data-stu-id="cccb5-113">Understanding Tez</span></span>

<span data-ttu-id="cccb5-114">Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cccb5-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="cccb5-115">Per i cluster HDInsight basati su Linux si tratta del motore predefinito per Hive.</span><span class="sxs-lookup"><span data-stu-id="cccb5-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="cccb5-116">Tez crea un grafo aciclico diretto (DAG) che descrive l'ordine delle azioni necessarie per i processi.</span><span class="sxs-lookup"><span data-stu-id="cccb5-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="cccb5-117">Le singole azioni sono chiamate vertici ed eseguono una parte dell'intero processo.</span><span class="sxs-lookup"><span data-stu-id="cccb5-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="cccb5-118">L'esecuzione vera e propria del lavoro descritta da un vertice è chiamata attività e può essere distribuita in più nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="cccb5-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="cccb5-119">Informazioni sulla visualizzazione Tez</span><span class="sxs-lookup"><span data-stu-id="cccb5-119">Understanding the Tez view</span></span>

<span data-ttu-id="cccb5-120">La visualizzazione Tez fornisce informazioni sulla cronologia e sui processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cccb5-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="cccb5-121">Queste informazioni mostrano in che modo un processo viene distribuito tra i cluster.</span><span class="sxs-lookup"><span data-stu-id="cccb5-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="cccb5-122">Visualizza anche i contatori usati da attività e vertici e le informazioni sull'errore relazionato al processo.</span><span class="sxs-lookup"><span data-stu-id="cccb5-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="cccb5-123">Può offrire informazioni utili negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="cccb5-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="cccb5-124">Monitoraggio di processi con esecuzione prolungata, visualizzazione dello stato delle attività di mapping e riduzione.</span><span class="sxs-lookup"><span data-stu-id="cccb5-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="cccb5-125">Analisi dei dati cronologici per i processi riusciti o non riusciti per capire come migliorare l'elaborazione o perché non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cccb5-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="cccb5-126">Generare un DAG</span><span class="sxs-lookup"><span data-stu-id="cccb5-126">Generate a DAG</span></span>

<span data-ttu-id="cccb5-127">La visualizzazione Tez contiene dati solo se un processo che usa il motore Tez è attualmente in esecuzione o è stato eseguito precedentemente.</span><span class="sxs-lookup"><span data-stu-id="cccb5-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="cccb5-128">Le query Hive semplici possono essere risolte senza usare Tez.</span><span class="sxs-lookup"><span data-stu-id="cccb5-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="cccb5-129">Query più complesse che eseguono filtraggio, raggruppamento, ordinamento, unione e così via.</span><span class="sxs-lookup"><span data-stu-id="cccb5-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="cccb5-130">Usare il motore Tez.</span><span class="sxs-lookup"><span data-stu-id="cccb5-130">use the Tez engine.</span></span>

<span data-ttu-id="cccb5-131">Usare la procedura seguente per eseguire una query Hive che usa Tez:</span><span class="sxs-lookup"><span data-stu-id="cccb5-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="cccb5-132">In un Web browser passare a https://NOMECLUSTER.azurehdinsight.net, dove **NOMECLUSTER** è il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cccb5-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="cccb5-133">Dal menu nella parte superiore della pagina selezionare l'icona delle **visualizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="cccb5-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="cccb5-134">La presente icona ha l'aspetto di una serie di quadrati.</span><span class="sxs-lookup"><span data-stu-id="cccb5-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="cccb5-135">Nell'elenco a discesa visualizzato, selezionare **Hive View** (Visualizzazione Hive).</span><span class="sxs-lookup"><span data-stu-id="cccb5-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Selezione della visualizzazione Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="cccb5-137">Quando viene caricata la visualizzazione Hive, incollare la query seguente nell'editor di query e quindi fare clic su **execute** (esegui).</span><span class="sxs-lookup"><span data-stu-id="cccb5-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="cccb5-138">Al termine del processo, l'output verrà visualizzato nella sezione **Query Process Results** (Risultati elaborazione query).</span><span class="sxs-lookup"><span data-stu-id="cccb5-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="cccb5-139">I risultati dovrebbero essere simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cccb5-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="cccb5-140">Selezionare la scheda **Log**.</span><span class="sxs-lookup"><span data-stu-id="cccb5-140">Select the **Log** tab.</span></span> <span data-ttu-id="cccb5-141">Vengono restituite informazioni simili al seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cccb5-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="cccb5-142">Salvare il valore **App id**, poiché tale valore viene usato nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="cccb5-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="cccb5-143">Usare la visualizzazione Tez</span><span class="sxs-lookup"><span data-stu-id="cccb5-143">Use the Tez View</span></span>

1. <span data-ttu-id="cccb5-144">Dal menu nella parte superiore della pagina selezionare l'icona delle **visualizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="cccb5-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="cccb5-145">Nell'elenco a discesa visualizzato selezionare **Tez View** (Visualizzazione Tez).</span><span class="sxs-lookup"><span data-stu-id="cccb5-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Selezione della visualizzazione Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="cccb5-147">Quando la visualizzazione Tez viene caricata, viene visualizzato un elenco di query Hive che sono attualmente in esecuzione o che sono stati eseguiti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="cccb5-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Tutti i DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="cccb5-149">Se è presente una sola voce, è quella relativa alla query eseguita nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="cccb5-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="cccb5-150">Se si dispone di più voci, è possibile eseguire una ricerca con i campi nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="cccb5-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="cccb5-151">Selezionare il **ID Query** per una query Hive.</span><span class="sxs-lookup"><span data-stu-id="cccb5-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="cccb5-152">Verranno visualizzate informazioni sulla query.</span><span class="sxs-lookup"><span data-stu-id="cccb5-152">Information about the query is displayed.</span></span>

    ![DAG Details](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="cccb5-154">Le schede in questa pagina consentono di visualizzare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cccb5-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="cccb5-155">**Informazioni sulla query**: informazioni dettagliate sulla query Hive.</span><span class="sxs-lookup"><span data-stu-id="cccb5-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="cccb5-156">**Tempistiche**: informazioni sulla durata di ogni fase dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cccb5-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="cccb5-157">**Configurazioni**: la configurazione usata per questa query.</span><span class="sxs-lookup"><span data-stu-id="cccb5-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="cccb5-158">Da __Dettagli query__ è possibile usare i collegamenti per trovare le informazioni sull'__applicazione__ o il __DAG__ per questa query.</span><span class="sxs-lookup"><span data-stu-id="cccb5-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="cccb5-159">Il collegamento __Applicazione__ consente di visualizzare informazioni sull'applicazione YARN per questa query.</span><span class="sxs-lookup"><span data-stu-id="cccb5-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="cccb5-160">Da qui è possibile accedere ai registri dell'applicazione YARN.</span><span class="sxs-lookup"><span data-stu-id="cccb5-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="cccb5-161">Il collegamento __DAG__ consente di visualizzare le informazioni su un grafo aciclico diretto per questa query.</span><span class="sxs-lookup"><span data-stu-id="cccb5-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="cccb5-162">Da qui è possibile visualizzare una rappresentazione grafica del DAG.</span><span class="sxs-lookup"><span data-stu-id="cccb5-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="cccb5-163">È anche possibile trovare informazioni sui vertici all'interno del DAG.</span><span class="sxs-lookup"><span data-stu-id="cccb5-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cccb5-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cccb5-164">Next Steps</span></span>

<span data-ttu-id="cccb5-165">A questo punto, dopo avere appreso come usare la visualizzazione Tez, è possibile trovare altre informazioni in [Uso di Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="cccb5-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="cccb5-166">Per informazioni tecniche più dettagliate su Tez, vedere la [pagina di Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="cccb5-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="cccb5-167">Per altre informazioni sull'uso di Ambari con HDInsight, vedere [Gestire i cluster HDInsight usando l'interfaccia utente Web di Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="cccb5-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
