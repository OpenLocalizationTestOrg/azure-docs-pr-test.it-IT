---
title: aaaUse Tez UI con HDInsight - basati su Windows Azure | Documenti Microsoft
description: Informazioni su come i processi di hello toouse UI Tez toodebug Tez in HDInsight di HDInsight basati su Windows.
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="c2987-103">Utilizzare i processi di UI Tez toodebug Tez hello in HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="c2987-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="c2987-104">Hello UI Tez è una pagina web che possono essere utilizzati i processi toounderstand e debug che utilizzano Tez come motore di esecuzione hello nei cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="c2987-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c2987-105">Hello Tez UI consente processo hello toovisualize come un grafico degli elementi connessi, analizza ogni elemento e recuperare le statistiche e informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="c2987-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2987-106">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Windows.</span><span class="sxs-lookup"><span data-stu-id="c2987-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="c2987-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c2987-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c2987-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c2987-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2987-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c2987-109">Prerequisites</span></span>
* <span data-ttu-id="c2987-110">Un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="c2987-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c2987-111">Per la procedura di creazione di un nuovo cluster, vedere [Introduzione all'uso di HDInsight basato su Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c2987-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c2987-112">Hello UI Tez è disponibile solo in cluster HDInsight basati su Windows creati dopo l'8 febbraio 2016.</span><span class="sxs-lookup"><span data-stu-id="c2987-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="c2987-113">Un client Desktop remoto basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="c2987-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="c2987-114">Informazioni su Tez</span><span class="sxs-lookup"><span data-stu-id="c2987-114">Understanding Tez</span></span>
<span data-ttu-id="c2987-115">Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c2987-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="c2987-116">Per i cluster HDInsight basati su Windows, è un motore facoltativo che è possibile abilitare per l'Hive usando hello comando seguente come parte della query Hive:</span><span class="sxs-lookup"><span data-stu-id="c2987-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="c2987-117">Quando il lavoro viene inviato tooTez, viene creato un indirizzate aciclico Graph (DAG) che descrive l'ordine di hello di esecuzione delle azioni hello richiesto dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="c2987-118">Singole azioni vengono chiamate i vertici ed eseguire una parte di hello processo globale.</span><span class="sxs-lookup"><span data-stu-id="c2987-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="c2987-119">l'esecuzione effettiva Hello del lavoro hello descritto da un vertice viene chiamata un'attività e può essere distribuita in più nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="c2987-120">Hello comprensione Tez UI</span><span class="sxs-lookup"><span data-stu-id="c2987-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="c2987-121">Hello UI Tez è una pagina web che fornisce informazioni sui processi in esecuzione o che hanno in precedenza è stata eseguita con Tez.</span><span class="sxs-lookup"><span data-stu-id="c2987-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="c2987-122">Consente di hello tooview DAG generati da Tez, come viene distribuito tra i cluster, i contatori, ad esempio la memoria utilizzata da attività e i vertici e informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="c2987-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="c2987-123">Può offrire informazioni utili in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="c2987-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="c2987-124">Monitoraggio dei processi con esecuzione prolungata, visualizzazione hello lo stato di avanzamento della mappa e ridurre le attività.</span><span class="sxs-lookup"><span data-stu-id="c2987-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="c2987-125">Analisi dei dati cronologici per i processi di esito positivo o negativo toolearn come l'elaborazione potrebbe essere migliorata o perché non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="c2987-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="c2987-126">Generare un DAG</span><span class="sxs-lookup"><span data-stu-id="c2987-126">Generate a DAG</span></span>
<span data-ttu-id="c2987-127">Hello Tez UI conterrà dati solo se un processo che utilizza hello Tez motore è attualmente in esecuzione o è stato eseguito in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="c2987-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="c2987-128">Le query Hive semplici in genere possono essere risolte senza usare Tez, ma quelle più complesse che eseguono operazioni di filtro, raggruppamento, ordinamento, join e così via di solito richiedono Tez.</span><span class="sxs-lookup"><span data-stu-id="c2987-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="c2987-129">Utilizzare hello seguendo i passaggi toorun una query Hive che verrà eseguito utilizzando Tez.</span><span class="sxs-lookup"><span data-stu-id="c2987-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="c2987-130">In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2987-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="c2987-131">Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="c2987-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="c2987-132">Verrà visualizzata una pagina con hello seguenti query di esempio.</span><span class="sxs-lookup"><span data-stu-id="c2987-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="c2987-133">Cancellare la query di esempio hello e sostituirlo con il seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="c2987-134">Seleziona hello **Invia** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c2987-134">Select hello **Submit** button.</span></span> <span data-ttu-id="c2987-135">Hello **sessione del processo** sezione hello parte inferiore della pagina hello verrà visualizzato lo stato di hello di query hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="c2987-136">Una volta hello troppo modifiche allo stato**completato**selezionare hello **Visualizza dettagli** collegare tooview hello risultati.</span><span class="sxs-lookup"><span data-stu-id="c2987-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="c2987-137">Hello **Output processo** dovrebbe essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2987-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="c2987-138">Utilizzare hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="c2987-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="c2987-139">Hello UI Tez è disponibile solo da desktop hello hello head dei nodi del cluster, è necessario utilizzare i nodi head toohello tooconnect del Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c2987-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="c2987-140">Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2987-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="c2987-141">Selezionare hello hello superiore del Pannello di HDInsight hello **Desktop remoto** icona.</span><span class="sxs-lookup"><span data-stu-id="c2987-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="c2987-142">Verrà visualizzata blade desktop remoto hello</span><span class="sxs-lookup"><span data-stu-id="c2987-142">This will display hello remote desktop blade</span></span>

    ![Icona Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="c2987-144">Dal Pannello di hello Desktop remoto, selezionare **Connetti** nodo head del cluster toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c2987-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="c2987-145">Quando richiesto, utilizzare hello cluster utente nome e la password tooauthenticate hello connessione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c2987-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Icona Connetti di Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="c2987-147">Se non è stato abilitato connessione Desktop remoto, fornire un nome utente, password e la data di scadenza, quindi selezionare **abilitare** tooenable Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c2987-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="c2987-148">Una volta è stata abilitata, è possibile utilizzare hello precedenti passaggi tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c2987-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="c2987-149">Una volta connessi, aprire Internet Explorer sul desktop remoto di hello, icona dell'ingranaggio hello selezionare nella parte superiore di hello destra del browser hello e quindi selezionare **impostazioni visualizzazione compatibilità**.</span><span class="sxs-lookup"><span data-stu-id="c2987-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="c2987-150">Dalla parte inferiore di hello del **impostazioni visualizzazione compatibilità**, deselezionare la casella di controllo hello per **visualizzare i siti intranet in vista di compatibilità** e **gli elenchi di compatibilità di utilizzare Microsoft**, e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="c2987-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="c2987-151">In Internet Explorer passare toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="c2987-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="c2987-152">Verrà visualizzata hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="c2987-152">This will display hello Tez UI</span></span>

    ![Interfaccia utente di Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="c2987-154">Quando viene caricato hello Tez UI, verrà visualizzato un elenco di DAG attualmente in esecuzione o sono stati eseguiti nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="c2987-155">visualizzazione predefinita Hello include hello Dag Name, Id, autore, stato, ora di inizio, ora di fine, durata, ID dell'applicazione e coda.</span><span class="sxs-lookup"><span data-stu-id="c2987-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="c2987-156">È possibile aggiungere più colonne utilizzando l'icona dell'ingranaggio hello in hello destra della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="c2987-157">Se si dispone di una sola voce, sia per le query hello che è stato eseguito nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="c2987-158">Se si dispone di più voci, è possibile eseguire la ricerca specificando i criteri di ricerca nei campi hello sopra hello DAG, quindi premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="c2987-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="c2987-159">Seleziona hello **Dag Name** per hello la voce più recente DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="c2987-160">Verrà visualizzato informazioni hello DAG, nonché toodownload opzione hello un file zip dei file JSON che contengono informazioni hello DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![DAG Details](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="c2987-162">Sopra hello **dettagli DAG** sono numerosi collegamenti che possono essere utilizzati toodisplay informazioni hello DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="c2987-163">**DAG Counters** (Contatori DAG) visualizza informazioni sui contatori per il DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="c2987-164">**Graphical View** (Visualizzazione grafica) visualizza una rappresentazione grafica del DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="c2987-165">**Tutti i vertici** Visualizza un elenco di vertici hello in questo DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="c2987-166">**Tutte le attività** Visualizza un elenco di attività hello per tutti i vertici in questo DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="c2987-167">**Tutti TaskAttempts** Visualizza informazioni su hello tenta toorun attività per questa DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c2987-168">Se si scorre una visualizzazione della colonna hello per vertici, attività e TaskAttempts, si noti che sono presenti collegamenti tooview **contatori** e **consente di visualizzare o scaricare i log** per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="c2987-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="c2987-169">Se si è verificato un errore con il processo di hello, hello DAG dettagli verrà visualizzato lo stato non riuscito, insieme ai collegamenti tooinformation sull'operazione non riuscita di hello.</span><span class="sxs-lookup"><span data-stu-id="c2987-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="c2987-170">Informazioni di diagnostica verranno visualizzate sotto i dettagli di hello DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="c2987-171">Selezionare **Graphical View** (Visualizzazione grafica).</span><span class="sxs-lookup"><span data-stu-id="c2987-171">Select **Graphical View**.</span></span> <span data-ttu-id="c2987-172">Verrà visualizzata una rappresentazione grafica di hello DAG.</span><span class="sxs-lookup"><span data-stu-id="c2987-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="c2987-173">È possibile posizionare il mouse hello sopra ogni vertice in hello vista toodisplay le informazioni.</span><span class="sxs-lookup"><span data-stu-id="c2987-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Graphical View](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="c2987-175">Facendo clic su un vertice caricherà hello **dettagli del Vertex** per quell'elemento.</span><span class="sxs-lookup"><span data-stu-id="c2987-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="c2987-176">Fare clic su hello **1 mappa** dettagli del vertex toodisplay per questo elemento.</span><span class="sxs-lookup"><span data-stu-id="c2987-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="c2987-177">Selezionare **conferma** navigazione hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c2987-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Vertex Details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="c2987-179">Si noti che è ora possibile i collegamenti nella parte superiore di hello della pagina hello toovertices correlate e attività.</span><span class="sxs-lookup"><span data-stu-id="c2987-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c2987-180">Può arrivare in questa pagina inoltre tornando troppo**DAG dettagli**, se si seleziona **dettagli del Vertex**e quindi selezionando hello **1 mappa** vertice.</span><span class="sxs-lookup"><span data-stu-id="c2987-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="c2987-181">**Vertex Counters** (Contatori vertice) visualizza informazioni sui contatori per il vertice.</span><span class="sxs-lookup"><span data-stu-id="c2987-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="c2987-182">**Tasks** (Attività) visualizza le attività per il vertice.</span><span class="sxs-lookup"><span data-stu-id="c2987-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="c2987-183">**Attività tentativi** consente di visualizzare informazioni sulle attività di toorun tentativi per questo vertice.</span><span class="sxs-lookup"><span data-stu-id="c2987-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="c2987-184">**Sources &amp; Sinks** (Origini e sink) visualizza le origini dati e i sink per il vertice.</span><span class="sxs-lookup"><span data-stu-id="c2987-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c2987-185">Come con menu precedente hello, è possibile scorrere visualizzazione della colonna hello per le attività, i tentativi di attività e origini & Sinks__ toodisplay collega toomore informazioni per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="c2987-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="c2987-186">Selezionare **attività**, e quindi selezionare hello elemento **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="c2987-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="c2987-187">Verranno visualizzati i dati di **Task Details** (Dettagli attività) per questa attività.</span><span class="sxs-lookup"><span data-stu-id="c2987-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="c2987-188">Da questa schermata è possibile visualizzare **Task Counters** (Contatori attività) e **Task Attempts** (Tentativi attività).</span><span class="sxs-lookup"><span data-stu-id="c2987-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Dettagli dell'attività](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="c2987-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2987-190">Next Steps</span></span>
<span data-ttu-id="c2987-191">Ora che si è appreso come hello toouse Tez Visualizza, altre informazioni, vedere [utilizzando Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c2987-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="c2987-192">Per informazioni tecniche relative a Tez dettagliate, vedere hello [pagina Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="c2987-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
