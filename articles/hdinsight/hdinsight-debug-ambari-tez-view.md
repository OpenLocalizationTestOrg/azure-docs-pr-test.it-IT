---
title: aaaUse Ambari Tez visualizzazione con HDInsight - Azure | Documenti Microsoft
description: Informazioni su come hello toouse Ambari Tez visualizzare processi Tez toodebug in HDInsight.
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="e8449-103">Utilizzare viste Ambari toodebug Tez processi in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8449-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="e8449-104">interfaccia utente Web Ambari per HDInsight Hello contiene una visualizzazione di Tez che può essere utilizzati i processi toounderstand e debug che utilizzano Tez.</span><span class="sxs-lookup"><span data-stu-id="e8449-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="e8449-105">visualizzazione di Tez Hello consente processo hello toovisualize come un grafico degli elementi connessi, analizza ogni elemento e recuperare le statistiche e informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="e8449-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8449-106">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="e8449-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e8449-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e8449-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e8449-108">Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e8449-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8449-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8449-109">Prerequisites</span></span>

* <span data-ttu-id="e8449-110">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="e8449-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e8449-111">Per la procedura di creazione di un cluster, vedere [Esercitazione di Hadoop: Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8449-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="e8449-112">Un moderno Web browser che supporta HTML5.</span><span class="sxs-lookup"><span data-stu-id="e8449-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="e8449-113">Informazioni su Tez</span><span class="sxs-lookup"><span data-stu-id="e8449-113">Understanding Tez</span></span>

<span data-ttu-id="e8449-114">Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e8449-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="e8449-115">Per i cluster HDInsight basati su Linux, è il motore predefinito hello per l'Hive.</span><span class="sxs-lookup"><span data-stu-id="e8449-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="e8449-116">Tez crea indirizzate aciclico Graph (DAG) che descrive l'ordine di hello delle azioni necessarie per processi.</span><span class="sxs-lookup"><span data-stu-id="e8449-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="e8449-117">Singole azioni vengono chiamate i vertici ed eseguire una parte di hello processo globale.</span><span class="sxs-lookup"><span data-stu-id="e8449-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="e8449-118">l'esecuzione effettiva Hello del lavoro hello descritto da un vertice viene chiamata un'attività e può essere distribuita in più nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="e8449-119">Hello informazioni sulla visualizzazione Tez</span><span class="sxs-lookup"><span data-stu-id="e8449-119">Understanding hello Tez view</span></span>

<span data-ttu-id="e8449-120">Hello Tez visualizzazione fornisce informazioni cronologiche e informazioni sui processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e8449-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="e8449-121">Queste informazioni mostrano in che modo un processo viene distribuito tra i cluster.</span><span class="sxs-lookup"><span data-stu-id="e8449-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="e8449-122">Vengono inoltre visualizzati i contatori utilizzati da attività e i vertici e informazioni sull'errore correlate toohello processo.</span><span class="sxs-lookup"><span data-stu-id="e8449-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="e8449-123">Può offrire informazioni utili in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="e8449-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="e8449-124">Monitoraggio dei processi con esecuzione prolungata, visualizzazione hello lo stato di avanzamento della mappa e ridurre le attività.</span><span class="sxs-lookup"><span data-stu-id="e8449-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="e8449-125">Analisi dei dati cronologici per i processi di esito positivo o negativo toolearn come l'elaborazione potrebbe essere migliorata o perché non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="e8449-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="e8449-126">Generare un DAG</span><span class="sxs-lookup"><span data-stu-id="e8449-126">Generate a DAG</span></span>

<span data-ttu-id="e8449-127">Hello Tez vista contiene dati solo se un processo che utilizza hello Tez motore è attualmente in esecuzione o è stato eseguito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e8449-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="e8449-128">Le query Hive semplici possono essere risolte senza usare Tez.</span><span class="sxs-lookup"><span data-stu-id="e8449-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="e8449-129">Query più complesse che eseguono filtraggio, raggruppamento, ordinamento, unione e così via.</span><span class="sxs-lookup"><span data-stu-id="e8449-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="e8449-130">Utilizzare il motore di Tez hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-130">use hello Tez engine.</span></span>

<span data-ttu-id="e8449-131">Utilizzare i seguenti passaggi toorun una query Hive che utilizza Tez hello:</span><span class="sxs-lookup"><span data-stu-id="e8449-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="e8449-132">In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8449-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="e8449-133">Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **viste** icona.</span><span class="sxs-lookup"><span data-stu-id="e8449-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="e8449-134">La presente icona ha l'aspetto di una serie di quadrati.</span><span class="sxs-lookup"><span data-stu-id="e8449-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="e8449-135">Nell'elenco a discesa hello che viene visualizzato, selezionare **Hive vista**.</span><span class="sxs-lookup"><span data-stu-id="e8449-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Selezione della visualizzazione Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="e8449-137">Quando viene caricato hello vista Hive, seguente hello Incolla query hello Editor di Query e quindi fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="e8449-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="e8449-138">Una volta completato il processo di hello, verrà visualizzato l'output di hello visualizzati in hello **risultati della Query processo** sezione.</span><span class="sxs-lookup"><span data-stu-id="e8449-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="e8449-139">i risultati di Hello saranno simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e8449-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="e8449-140">Seleziona hello **Log** scheda. Viene visualizzato toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e8449-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="e8449-141">Salvare hello **id App** valore, questo valore viene utilizzato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="e8449-142">Utilizzare hello Tez visualizzazione</span><span class="sxs-lookup"><span data-stu-id="e8449-142">Use hello Tez View</span></span>

1. <span data-ttu-id="e8449-143">Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **viste** icona.</span><span class="sxs-lookup"><span data-stu-id="e8449-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="e8449-144">Nell'elenco a discesa hello che viene visualizzato, selezionare **Tez vista**.</span><span class="sxs-lookup"><span data-stu-id="e8449-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Selezione della visualizzazione Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="e8449-146">Quando viene caricato hello Tez visualizzazione, viene visualizzato un elenco di query hive che sono attualmente in esecuzione o sono stati eseguiti nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Tutti i DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="e8449-148">Se si dispone di una sola voce, è per query hello che è stato eseguito nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="e8449-149">Se si dispone di più voci, è possibile cercare utilizzando i campi di hello nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="e8449-150">Seleziona hello **ID Query** per una query Hive.</span><span class="sxs-lookup"><span data-stu-id="e8449-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="e8449-151">Informazioni sulle query hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-151">Information about hello query is displayed.</span></span>

    ![DAG Details](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="e8449-153">le schede di Hello in questa pagina consentono di hello tooview le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="e8449-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="e8449-154">**Eseguire una query Dettagli**: informazioni dettagliate su query Hive hello.</span><span class="sxs-lookup"><span data-stu-id="e8449-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="e8449-155">**Tempistiche**: informazioni sulla durata di ogni fase dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e8449-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="e8449-156">**Configurazioni**: configurazione di hello utilizzata per la query.</span><span class="sxs-lookup"><span data-stu-id="e8449-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="e8449-157">Da __Dettagli Query__ è possibile utilizzare hello collegamenti toofind informazioni hello __applicazione__ o hello __DAG__ per questa query.</span><span class="sxs-lookup"><span data-stu-id="e8449-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="e8449-158">Hello __applicazione__ collegamento Visualizza le informazioni su hello applicazione YARN per questa query.</span><span class="sxs-lookup"><span data-stu-id="e8449-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="e8449-159">Da qui è possibile accedere hello YARN registri delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e8449-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="e8449-160">Hello __DAG__ collegamento Visualizza le informazioni su un grafo aciclico diretto hello per questa query.</span><span class="sxs-lookup"><span data-stu-id="e8449-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="e8449-161">Da qui è possibile visualizzare una rappresentazione grafica di hello DAG.</span><span class="sxs-lookup"><span data-stu-id="e8449-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="e8449-162">È inoltre possibile trovare informazioni sui vertici hello all'interno di hello DAG.</span><span class="sxs-lookup"><span data-stu-id="e8449-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8449-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8449-163">Next Steps</span></span>

<span data-ttu-id="e8449-164">Ora che si è appreso come hello toouse Tez Visualizza, altre informazioni, vedere [utilizzando Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e8449-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="e8449-165">Per informazioni tecniche relative a Tez dettagliate, vedere hello [pagina Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="e8449-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="e8449-166">Per ulteriori informazioni sull'uso di Ambari con HDInsight, vedere [gestione dei cluster HDInsight tramite interfaccia utente Web Ambari hello](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="e8449-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
