---
title: Usare l'interfaccia utente di Tez con HDInsight basato su Windows - Azure | Microsoft Docs
description: Informazioni su come usare l'interfaccia utente di Tez per il debug di processi Tez in HDInsight basato su Windows.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="486a2-103">Usare l'interfaccia utente di Tez per il debug di processi Tez in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="486a2-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="486a2-104">L'interfaccia utente di Tez è una pagina Web che può essere usata per la comprensione e il debug di processi che usano Tez come motore di esecuzione nei cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="486a2-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="486a2-105">L'interfaccia utente di Tez consente di visualizzare il processo come grafico di elementi connessi, esaminare ogni elemento e recuperare statistiche e informazioni sulla registrazione.</span><span class="sxs-lookup"><span data-stu-id="486a2-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="486a2-106">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Windows.</span><span class="sxs-lookup"><span data-stu-id="486a2-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="486a2-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="486a2-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="486a2-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="486a2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="486a2-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="486a2-109">Prerequisites</span></span>
* <span data-ttu-id="486a2-110">Un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="486a2-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="486a2-111">Per la procedura di creazione di un nuovo cluster, vedere [Introduzione all'uso di HDInsight basato su Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="486a2-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="486a2-112">L'interfaccia utente di Tez è disponibile solo nei cluster HDInsight basati su Windows creati dopo l'8 febbraio 2016.</span><span class="sxs-lookup"><span data-stu-id="486a2-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="486a2-113">Un client Desktop remoto basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="486a2-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="486a2-114">Informazioni su Tez</span><span class="sxs-lookup"><span data-stu-id="486a2-114">Understanding Tez</span></span>
<span data-ttu-id="486a2-115">Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="486a2-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="486a2-116">Per i cluster HDInsight basati su Windows, è un motore facoltativo che è possibile abilitare per Hive usando il comando seguente come parte della query Hive:</span><span class="sxs-lookup"><span data-stu-id="486a2-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="486a2-117">Quando riceve il lavoro, Tez crea un grafo aciclico diretto (DAG) che descrive l'ordine di esecuzione delle azioni necessarie per il processo.</span><span class="sxs-lookup"><span data-stu-id="486a2-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="486a2-118">Le singole azioni sono chiamate vertici ed eseguono una parte dell'intero processo.</span><span class="sxs-lookup"><span data-stu-id="486a2-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="486a2-119">L'esecuzione vera e propria del lavoro descritta da un vertice è chiamata attività e può essere distribuita in più nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="486a2-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="486a2-120">Informazioni sull'interfaccia utente di Tez</span><span class="sxs-lookup"><span data-stu-id="486a2-120">Understanding the Tez UI</span></span>
<span data-ttu-id="486a2-121">L'interfaccia utente di Tez è una pagina Web che fornisce informazioni sui processi in esecuzione o eseguiti in precedenza usando Tez.</span><span class="sxs-lookup"><span data-stu-id="486a2-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="486a2-122">Consente di visualizzare il DAG generato da Tez, come è distribuito nei cluster, i contatori, ad esempio la memoria usata dalle attività e dai vertici, e le informazioni sugli errori.</span><span class="sxs-lookup"><span data-stu-id="486a2-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="486a2-123">Può offrire informazioni utili negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="486a2-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="486a2-124">Monitoraggio di processi con esecuzione prolungata, visualizzazione dello stato delle attività di mapping e riduzione.</span><span class="sxs-lookup"><span data-stu-id="486a2-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="486a2-125">Analisi dei dati cronologici per i processi riusciti o non riusciti per capire come migliorare l'elaborazione o perché non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="486a2-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="486a2-126">Generare un DAG</span><span class="sxs-lookup"><span data-stu-id="486a2-126">Generate a DAG</span></span>
<span data-ttu-id="486a2-127">L'interfaccia utente di Tez conterrà dati solo se un processo che usa il motore Tez è attualmente in esecuzione è o stato eseguito in passato.</span><span class="sxs-lookup"><span data-stu-id="486a2-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="486a2-128">Le query Hive semplici in genere possono essere risolte senza usare Tez, ma quelle più complesse che eseguono operazioni di filtro, raggruppamento, ordinamento, join e così via di solito richiedono Tez.</span><span class="sxs-lookup"><span data-stu-id="486a2-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="486a2-129">Usare la procedura seguente per eseguire una query Hive che verrà eseguita con Tez.</span><span class="sxs-lookup"><span data-stu-id="486a2-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="486a2-130">In un Web browser passare a https://NOMECLUSTER.azurehdinsight.net, dove **NOMECLUSTER** è il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="486a2-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="486a2-131">Nel menu nella parte superiore della pagina selezionare **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="486a2-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="486a2-132">Verrà visualizzata una pagina con la query di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="486a2-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="486a2-133">Cancellare la query di esempio e sostituirla con la seguente.</span><span class="sxs-lookup"><span data-stu-id="486a2-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="486a2-134">Selezionare il pulsante **Invia**.</span><span class="sxs-lookup"><span data-stu-id="486a2-134">Select the **Submit** button.</span></span> <span data-ttu-id="486a2-135">La sezione **Sessione processo** nella parte inferiore della pagina visualizzerà lo stato della query.</span><span class="sxs-lookup"><span data-stu-id="486a2-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="486a2-136">Quando lo stato diventa **Operazione completata**, selezionare il collegamento **Visualizza dettagli** per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="486a2-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="486a2-137">L'**output del processo** dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="486a2-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="486a2-138">Usare l'interfaccia utente di Tez</span><span class="sxs-lookup"><span data-stu-id="486a2-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="486a2-139">Poiché l'interfaccia utente di Tez è disponibile solo nel desktop dei nodi head del cluster, è necessario usare Desktop remoto per connettersi ai nodi head.</span><span class="sxs-lookup"><span data-stu-id="486a2-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="486a2-140">Nel [portale di Azure](https://portal.azure.com)selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="486a2-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="486a2-141">Nella parte superiore del pannello HDInsight selezionare l'icona **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="486a2-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="486a2-142">Verrà visualizzato il pannello Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="486a2-142">This will display the remote desktop blade</span></span>

    ![Icona Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="486a2-144">Nel pannello Desktop remoto selezionare **Connetti** per connettersi al nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="486a2-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="486a2-145">Quando richiesto, usare il nome utente e la password di Desktop remoto per autenticare la connessione.</span><span class="sxs-lookup"><span data-stu-id="486a2-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Icona Connetti di Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="486a2-147">Se la connettività Desktop remoto non è stata abilitata, specificare nome utente, password e data di scadenza e quindi selezionare **Abilita** per abilitare Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="486a2-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="486a2-148">Una volta abilitata, seguire i passaggi precedenti per connettersi.</span><span class="sxs-lookup"><span data-stu-id="486a2-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="486a2-149">Dopo aver stabilito la connessione, aprire Internet Explorer sul desktop remoto, selezionare l'icona a forma di ingranaggio in alto a destra nel browser e quindi selezionare **Impostazioni Visualizzazione Compatibilità**.</span><span class="sxs-lookup"><span data-stu-id="486a2-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="486a2-150">Nella parte inferiore di **Impostazioni Visualizzazione Compatibilità** deselezionare le caselle di controllo **Visualizza siti Intranet in Visualizzazione Compatibilità** e **Usa elenchi di compatibilità Microsoft** e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="486a2-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="486a2-151">In Internet Explorer passare a http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="486a2-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="486a2-152">Verrà visualizzata l'interfaccia utente di Tez.</span><span class="sxs-lookup"><span data-stu-id="486a2-152">This will display the Tez UI</span></span>

    ![Interfaccia utente di Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="486a2-154">Quando l'interfaccia utente di Tez viene caricata, verrà visualizzato un elenco di DAG che sono attualmente in esecuzione o che sono stati eseguiti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="486a2-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="486a2-155">La visualizzazione predefinita include il nome DAG, l'ID, la persona che invia la richiesta, lo stato, l'ora di inizio, l'ora di fine, la durata, l'ID applicazione e la coda.</span><span class="sxs-lookup"><span data-stu-id="486a2-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="486a2-156">È possibile aggiungere altre colonne usando l'icona a forma di ingranaggio a destra nella pagina.</span><span class="sxs-lookup"><span data-stu-id="486a2-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="486a2-157">Se è presente una sola voce, sarà quella relativa alla query eseguita nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="486a2-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="486a2-158">Se sono presenti più voci, è possibile eseguire una ricerca immettendo i criteri di ricerca nei campi sopra i DAG e quindi premendo **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="486a2-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="486a2-159">In **Dag Name** (Nome DAG) selezionare la voce DAG più recente.</span><span class="sxs-lookup"><span data-stu-id="486a2-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="486a2-160">Verranno visualizzate le informazioni sul DAG, oltre all'opzione per scaricare uno zip di file JSON contenenti informazioni sul DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG Details](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="486a2-162">Sopra **DAG Details** (Dettagli DAG) sono presenti diversi collegamenti che possono essere usati per visualizzare informazioni sul DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="486a2-163">**DAG Counters** (Contatori DAG) visualizza informazioni sui contatori per il DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="486a2-164">**Graphical View** (Visualizzazione grafica) visualizza una rappresentazione grafica del DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="486a2-165">**All Vertices** (Tutti i vertici) visualizza un elenco dei vertici nel DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="486a2-166">**All Tasks** (Tutte le attività) visualizza un elenco delle attività per tutti i vertici nel DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="486a2-167">**All TaskAttempts** (Tutti i tentativi di attività) visualizza informazioni sui tentativi di eseguire attività per il DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="486a2-168">Scorrendo la visualizzazione colonne per vertici, attività e tentativi di attività, si noti che sono presenti collegamenti per visualizzare i **contatori** e per **visualizzare o scaricare i log** per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="486a2-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="486a2-169">Se si è verificato un errore nel processo, in DAG Details sarà visualizzato lo stato FAILED, con i collegamenti alle informazioni sull'attività non riuscita.</span><span class="sxs-lookup"><span data-stu-id="486a2-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="486a2-170">Le informazioni di diagnostica verranno visualizzate sotto i dettagli DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="486a2-171">Selezionare **Graphical View** (Visualizzazione grafica).</span><span class="sxs-lookup"><span data-stu-id="486a2-171">Select **Graphical View**.</span></span> <span data-ttu-id="486a2-172">Viene visualizzata una rappresentazione grafica del DAG.</span><span class="sxs-lookup"><span data-stu-id="486a2-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="486a2-173">È possibile posizionare il mouse su ogni vertice nella visualizzazione per accedere alle relative informazioni.</span><span class="sxs-lookup"><span data-stu-id="486a2-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Graphical View](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="486a2-175">Facendo clic su un vertice, verranno caricati i dati di **Vertex Details** (Dettagli vertice) per tale elemento.</span><span class="sxs-lookup"><span data-stu-id="486a2-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="486a2-176">Fare clic sul vertice **Map 1** (Mappa 1) per visualizzare i dettagli per questo elemento.</span><span class="sxs-lookup"><span data-stu-id="486a2-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="486a2-177">Selezionare **Confirm** (Conferma) per confermare lo spostamento.</span><span class="sxs-lookup"><span data-stu-id="486a2-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Vertex Details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="486a2-179">Si noti che ora nella parte superiore della pagina sono presenti i collegamenti relativi ai vertici e alle attività.</span><span class="sxs-lookup"><span data-stu-id="486a2-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="486a2-180">È possibile accedere a questa pagina anche tornando a **DAG Details** (Dettagli DAG) e selezionando **Vertex Details** (Dettagli vertice) e quindi il vertice **Map 1** (Mappa 1).</span><span class="sxs-lookup"><span data-stu-id="486a2-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="486a2-181">**Vertex Counters** (Contatori vertice) visualizza informazioni sui contatori per il vertice.</span><span class="sxs-lookup"><span data-stu-id="486a2-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="486a2-182">**Tasks** (Attività) visualizza le attività per il vertice.</span><span class="sxs-lookup"><span data-stu-id="486a2-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="486a2-183">**Task Attempts** (Tentativi attività) visualizza informazioni sui tentativi di eseguire attività per il vertice.</span><span class="sxs-lookup"><span data-stu-id="486a2-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="486a2-184">**Sources & Sinks** (Origini e sink) visualizza le origini dati e i sink per il vertice.</span><span class="sxs-lookup"><span data-stu-id="486a2-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="486a2-185">Come per il menu precedente, è possibile scorrere la visualizzazione colonne per Tasks, Task Attempts e Sources & Sinks per visualizzare i collegamenti ad altre informazioni per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="486a2-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="486a2-186">Selezionare **Tasks** (Attività) e quindi l'elemento denominato **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="486a2-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="486a2-187">Verranno visualizzati i dati di **Task Details** (Dettagli attività) per questa attività.</span><span class="sxs-lookup"><span data-stu-id="486a2-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="486a2-188">Da questa schermata è possibile visualizzare **Task Counters** (Contatori attività) e **Task Attempts** (Tentativi attività).</span><span class="sxs-lookup"><span data-stu-id="486a2-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Dettagli dell'attività](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="486a2-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="486a2-190">Next Steps</span></span>
<span data-ttu-id="486a2-191">A questo punto, dopo avere appreso come usare la visualizzazione Tez, è possibile trovare altre informazioni in [Uso di Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="486a2-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="486a2-192">Per informazioni tecniche più dettagliate su Tez, vedere la [pagina di Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="486a2-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
