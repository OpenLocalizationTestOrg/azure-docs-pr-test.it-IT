---
title: aaaMonitor e gestire dati pipeline - Azure | Documenti Microsoft
description: Informazioni su come toouse hello monitoraggio e gestione toomonitor app e gestire le pipeline e data factory di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="b2764-103">Monitorare e gestire le pipeline di Data Factory di Azure utilizzando app hello di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="b2764-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2764-104">Con il portale di Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2764-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="b2764-105">Con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="b2764-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="b2764-106">In questo articolo viene descritto come toouse hello toomonitor app di gestione e monitoraggio, gestire ed eseguire il debug le pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b2764-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="b2764-107">Fornisce inoltre informazioni su come toocreate avvisi tooget notificata in caso di errori.</span><span class="sxs-lookup"><span data-stu-id="b2764-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="b2764-108">È possibile iniziare con un'applicazione hello da hello guardando seguente video:</span><span class="sxs-lookup"><span data-stu-id="b2764-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="b2764-109">interfaccia utente di Hello illustrato hello video potrebbe non corrispondere esattamente ciò che viene visualizzato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="b2764-110">È leggermente meno recente, ma i concetti rimangono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="b2764-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="b2764-111">Avviare l'applicazione di monitoraggio e gestione hello</span><span class="sxs-lookup"><span data-stu-id="b2764-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="b2764-112">hello toolaunch monitoraggio e gestione app, fare clic su hello **monitoraggio e gestione** riquadro hello **Data Factory** pannello per il data factory.</span><span class="sxs-lookup"><span data-stu-id="b2764-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Monitoraggio delle sezione nella home page di hello Data Factory](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="b2764-114">Dovrebbe essere hello monitoraggio e gestione delle app aperte in una finestra separata.</span><span class="sxs-lookup"><span data-stu-id="b2764-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![App di monitoraggio e gestione](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="b2764-116">Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", deselezionare hello **bloccare i cookie di terze parti e i dati del sito** - casella di controllo o mantenere è selezionata, creare un'eccezione per **login.microsoftonline.com** , quindi riprovare a eseguire tooopen hello app.</span><span class="sxs-lookup"><span data-stu-id="b2764-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="b2764-117">Nell'elenco di attività Windows hello nel riquadro centrale di hello, verrà visualizzata una finestra di attività per ogni esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="b2764-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="b2764-118">Ad esempio, se hai hello attività pianificata toorun ogni ora per cinque ore, vedrai cinque windows attività associata a sezioni di dati di cinque.</span><span class="sxs-lookup"><span data-stu-id="b2764-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="b2764-119">Se non viene visualizzato windows attività nell'elenco di hello nella parte inferiore di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2764-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="b2764-120">Hello aggiornamento **ora di inizio** e **ora di fine** filtri hello toomatch superiore hello avviare e fine della pipeline e quindi fare clic su hello **applica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b2764-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="b2764-121">elenco di attività Windows Hello non viene aggiornato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b2764-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="b2764-122">Fare clic su hello **aggiornamento** pulsante sulla barra degli strumenti hello hello **attività Windows** elenco.</span><span class="sxs-lookup"><span data-stu-id="b2764-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="b2764-123">Se non è un tootest applicazione Data Factory questi passaggi con, hello esercitazione: [copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b2764-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="b2764-124">Comprendere hello monitoraggio e Gestione applicazione</span><span class="sxs-lookup"><span data-stu-id="b2764-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="b2764-125">Sono disponibili tre schede a sinistra di hello: **Esplora inventario risorse**, **visualizzazioni di monitoraggio**, e **avvisi**.</span><span class="sxs-lookup"><span data-stu-id="b2764-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="b2764-126">prima scheda Hello (**Esplora inventario risorse**) è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b2764-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="b2764-127">Scheda Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="b2764-127">Resource Explorer</span></span>
<span data-ttu-id="b2764-128">Verrà visualizzata hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b2764-128">You see hello following:</span></span>

* <span data-ttu-id="b2764-129">Esplora inventario risorse Hello **visualizzazione ad albero** nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="b2764-130">Hello **vista diagramma** nella parte superiore di hello nel riquadro centrale hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="b2764-131">Hello **attività Windows** elenco nella parte inferiore di hello nel riquadro centrale hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="b2764-132">Hello **proprietà**, **attività finestra Esplora**, e **Script** schede nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="b2764-133">In Esplora inventario risorse, visualizzare tutte le risorse (pipeline, i set di dati, servizi collegati) nella data factory di hello in una visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="b2764-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="b2764-134">Quando si seleziona un oggetto in Esplora risorse:</span><span class="sxs-lookup"><span data-stu-id="b2764-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="b2764-135">Hello associati Data Factory di entità viene evidenziata in vista diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="b2764-136">[Associata windows attività](data-factory-scheduling-and-execution.md) sono evidenziate nell'elenco di attività Windows hello nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="b2764-137">proprietà Hello dell'oggetto selezionato hello vengono visualizzate nella finestra Proprietà hello nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="b2764-138">Hello definizione JSON dell'oggetto selezionato hello è visibile, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="b2764-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="b2764-139">Ad esempio: un servizio collegato, un set di dati o una pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2764-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Scheda Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="b2764-141">Vedere hello [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo per informazioni dettagliate sulle finestre di attività.</span><span class="sxs-lookup"><span data-stu-id="b2764-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="b2764-142">Vista Diagramma</span><span class="sxs-lookup"><span data-stu-id="b2764-142">Diagram View</span></span>
<span data-ttu-id="b2764-143">Vista diagramma di una data factory Hello offre un unico riquadro della finestra effetto cristallo toomonitor e gestire una data factory e delle relative risorse.</span><span class="sxs-lookup"><span data-stu-id="b2764-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="b2764-144">Quando si seleziona un'entità di Data Factory (set di dati/pipeline) in vista diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="b2764-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="b2764-145">Hello data factory entità selezionata nella visualizzazione ad albero di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="b2764-146">Hello associata l'attività di windows sono evidenziate nell'elenco di attività Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="b2764-147">proprietà Hello dell'oggetto selezionato hello vengono visualizzate nella finestra Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="b2764-148">Quando la pipeline hello è attivata (non in pausa), questo viene visualizzato con una linea verde:</span><span class="sxs-lookup"><span data-stu-id="b2764-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline in esecuzione](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="b2764-150">È possibile sospendere, riprendere o terminare una pipeline selezionandolo nella vista diagramma hello e utilizzando i pulsanti di hello hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b2764-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Sospendere o riprendere hello barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="b2764-152">Esistono tre pulsanti della barra di comando per la pipeline di hello in vista diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="b2764-153">È possibile utilizzare pipeline hello toopause hello secondo pulsante.</span><span class="sxs-lookup"><span data-stu-id="b2764-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="b2764-154">La sospensione non termina l'attività attualmente in esecuzione hello e consente loro di procedere toocompletion.</span><span class="sxs-lookup"><span data-stu-id="b2764-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="b2764-155">il terzo pulsante Hello sospende pipeline hello e termina l'esecuzione di attività esistenti.</span><span class="sxs-lookup"><span data-stu-id="b2764-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="b2764-156">primo pulsante Hello riprende pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="b2764-157">Quando la pipeline viene sospesa, il colore di hello della pipeline hello cambia.</span><span class="sxs-lookup"><span data-stu-id="b2764-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="b2764-158">Ad esempio, una pipeline sospesa l'aspetto in hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="b2764-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Pipeline in pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="b2764-160">È possibile selezionare più due o più pipeline tasto Ctrl hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="b2764-161">È possibile utilizzare toopause o ripresa di hello comando barra dei pulsanti più pipeline contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b2764-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="b2764-162">È anche possibile fare doppio clic su una pipeline e selezionare le opzioni toosuspend, riprendere o terminare una pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2764-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Menu di scelta rapida per le pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="b2764-164">Fare clic su hello **pipeline aprire** opzione toosee tutte le attività di hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menu Apri pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="b2764-166">Nella visualizzazione pipeline hello aperto, vedrai tutte le attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="b2764-167">In questo esempio è presente soltanto l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="b2764-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Pipeline aperta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="b2764-169">toogo nuovamente toohello visualizzazione precedente, fare clic sul nome di factory hello dati in menu di navigazione hello nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="b2764-170">Nella visualizzazione pipeline hello, quando si seleziona un set di dati di output o quando si sposta il puntatore del mouse su set di dati con output di hello vedrai finestra popup di attività Windows hello per tale set di dati.</span><span class="sxs-lookup"><span data-stu-id="b2764-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Finestra popup di Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="b2764-172">È possibile fare clic una finestra toosee di attività per tale hello **proprietà** finestra nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Proprietà della finestra attività](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="b2764-174">Nel riquadro destro hello passare toohello **attività finestra Esplora** scheda toosee ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="b2764-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="b2764-176">Anche possibile vedere **risolto variabili** a ogni tentativo di esecuzione per un'attività in hello **tentativi** sezione.</span><span class="sxs-lookup"><span data-stu-id="b2764-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Variabili risolte](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="b2764-178">Passare toohello **Script** scheda toosee hello JSON Crea script per definizione per l'oggetto selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="b2764-180">Le finestre attività vengono visualizzate in tre posizioni:</span><span class="sxs-lookup"><span data-stu-id="b2764-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="b2764-181">Hello Windows attività popup hello vista diagramma (riquadro centrale).</span><span class="sxs-lookup"><span data-stu-id="b2764-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="b2764-182">nel riquadro di destra hello, Hello attività Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="b2764-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="b2764-183">elenco di attività Windows Hello nel riquadro inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="b2764-184">Nel messaggio popup di attività Windows hello e attività Esplora risorse, è possibile scorrere toohello settimana precedente e hello settimana successiva tramite hello frecce destra e sinistra.</span><span class="sxs-lookup"><span data-stu-id="b2764-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Freccia sinistra/destra in Activity Window Explorer (Esplora finestra attività)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="b2764-186">Nella parte inferiore di hello di hello vista diagramma, vedrai questi pulsanti: Zoom avanti, Zoom indietro, tooFit Zoom, eseguire lo Zoom 100%, il layout di blocco.</span><span class="sxs-lookup"><span data-stu-id="b2764-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="b2764-187">Hello **layout blocco** pulsante consente di spostare accidentalmente tabelle e pipeline in vista diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="b2764-188">È attivo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b2764-188">It's on by default.</span></span> <span data-ttu-id="b2764-189">È possibile disattivarla e spostare le entità nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="b2764-190">Quando si disattiva, è possibile utilizzare le pipeline e tabelle di hello ultimo pulsante tooautomatically posizione.</span><span class="sxs-lookup"><span data-stu-id="b2764-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="b2764-191">È inoltre possibile ingrandire o ridurre utilizzando rotellina del mouse hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Comandi di zoom nella visualizzazione diagramma](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="b2764-193">Elenco Activity Windows (Finestre attività)</span><span class="sxs-lookup"><span data-stu-id="b2764-193">Activity Windows list</span></span>
<span data-ttu-id="b2764-194">elenco di attività Windows Hello nella parte inferiore di hello del riquadro centrale hello Visualizza tutte le finestre attività per i set di dati di hello selezionato in Esplora inventario risorse hello o hello vista diagramma.</span><span class="sxs-lookup"><span data-stu-id="b2764-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="b2764-195">Per impostazione predefinita, l'elenco di hello è in ordine decrescente, il che significa che vedere finestra attività hello più recente nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="b2764-197">Questo elenco non vengono aggiornati automaticamente, quindi utilizzare hello aggiornamento pulsante hello barra degli strumenti toomanually aggiornarlo.</span><span class="sxs-lookup"><span data-stu-id="b2764-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="b2764-198">Le finestre attività possono essere in uno dei seguenti stati hello:</span><span class="sxs-lookup"><span data-stu-id="b2764-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="b2764-199">Stato</span><span class="sxs-lookup"><span data-stu-id="b2764-199">Status</span></span></th><th align="left"><span data-ttu-id="b2764-200">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="b2764-200">Substatus</span></span></th><th align="left"><span data-ttu-id="b2764-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b2764-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="b2764-202">Waiting</span><span class="sxs-lookup"><span data-stu-id="b2764-202">Waiting</span></span></td><td><span data-ttu-id="b2764-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="b2764-203">ScheduleTime</span></span></td><td><span data-ttu-id="b2764-204">tempo di Hello non venga per toorun finestra attività di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="b2764-205">DatasetDependencies</span></span></td><td><span data-ttu-id="b2764-206">le dipendenze upstream Hello non sono pronte.</span><span class="sxs-lookup"><span data-stu-id="b2764-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="b2764-207">ComputeResources</span></span></td><td><span data-ttu-id="b2764-208">risorse di calcolo Hello non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="b2764-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="b2764-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="b2764-210">Tutte le istanze di attività hello sono occupate in esecuzione altre attività di windows.</span><span class="sxs-lookup"><span data-stu-id="b2764-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="b2764-211">ActivityResume</span></span></td><td><span data-ttu-id="b2764-212">attività di Hello è sospesa e non può eseguire windows attività hello fino a quando non viene ripreso.</span><span class="sxs-lookup"><span data-stu-id="b2764-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-213">Retry</span><span class="sxs-lookup"><span data-stu-id="b2764-213">Retry</span></span></td><td><span data-ttu-id="b2764-214">l'esecuzione dell'attività Hello verrà riprovata.</span><span class="sxs-lookup"><span data-stu-id="b2764-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-215">Convalida</span><span class="sxs-lookup"><span data-stu-id="b2764-215">Validation</span></span></td><td><span data-ttu-id="b2764-216">La convalida non è ancora stata avviata.</span><span class="sxs-lookup"><span data-stu-id="b2764-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="b2764-217">ValidationRetry</span></span></td><td><span data-ttu-id="b2764-218">La convalida è in attesa toobe ripetuta.</span><span class="sxs-lookup"><span data-stu-id="b2764-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="b2764-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="b2764-219">InProgress</span></span></td><td><span data-ttu-id="b2764-220">Convalida in corso.</span><span class="sxs-lookup"><span data-stu-id="b2764-220">Validating</span></span></td><td><span data-ttu-id="b2764-221">La convalida è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2764-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="b2764-222">finestra attività Hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="b2764-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="b2764-223">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="b2764-223">Failed</span></span></td><td><span data-ttu-id="b2764-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b2764-224">TimedOut</span></span></td><td><span data-ttu-id="b2764-225">l'esecuzione dell'attività Hello ha richiesto più tempo rispetto a quelle consentite dall'attività hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="b2764-226">Canceled</span></span></td><td><span data-ttu-id="b2764-227">finestra attività Hello è stata annullata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b2764-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-228">Convalida</span><span class="sxs-lookup"><span data-stu-id="b2764-228">Validation</span></span></td><td><span data-ttu-id="b2764-229">Convalida non riuscita.</span><span class="sxs-lookup"><span data-stu-id="b2764-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="b2764-230">finestra attività Hello Impossibile toobe generato o convalidato.</span><span class="sxs-lookup"><span data-stu-id="b2764-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="b2764-231">Ready</span><span class="sxs-lookup"><span data-stu-id="b2764-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="b2764-232">finestra attività Hello è pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b2764-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="b2764-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="b2764-234">finestra attività Hello non è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="b2764-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2764-235">Nessuno</span><span class="sxs-lookup"><span data-stu-id="b2764-235">None</span></span></td><td>-</td><td><span data-ttu-id="b2764-236">Una finestra attività utilizzato tooexist con un altro stato, ma è stata reimpostata.</span><span class="sxs-lookup"><span data-stu-id="b2764-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="b2764-237">Quando si fa clic su una finestra delle attività nell'elenco di hello, vedrai dettagli in hello **attività Esplora** o hello **proprietà** finestra hello destra.</span><span class="sxs-lookup"><span data-stu-id="b2764-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="b2764-239">Aggiornare le finestre attività</span><span class="sxs-lookup"><span data-stu-id="b2764-239">Refresh activity windows</span></span>
<span data-ttu-id="b2764-240">Dettagli Hello non vengono aggiornati automaticamente, pertanto utilizzare il pulsante di aggiornamento hello (secondo pulsante hello) sulla barra toomanually Aggiorna hello attività windows elenco dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="b2764-241">Finestra Properties</span><span class="sxs-lookup"><span data-stu-id="b2764-241">Properties window</span></span>
<span data-ttu-id="b2764-242">finestra Proprietà Hello è nel riquadro di destra hello di hello monitoraggio e gestione delle app.</span><span class="sxs-lookup"><span data-stu-id="b2764-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Finestra Properties](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="b2764-244">Vengono visualizzate le proprietà per l'elemento hello selezionato in Esplora risorse (visualizzazione struttura ad albero), hello vista diagramma o elenco di attività Windows.</span><span class="sxs-lookup"><span data-stu-id="b2764-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="b2764-245">Esplora finestre attività</span><span class="sxs-lookup"><span data-stu-id="b2764-245">Activity Window Explorer</span></span>
<span data-ttu-id="b2764-246">Hello **attività finestra Esplora** finestra Trova nel riquadro di destra hello di hello monitoraggio e gestione delle app.</span><span class="sxs-lookup"><span data-stu-id="b2764-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="b2764-247">Visualizza informazioni dettagliate su finestra hello attività selezionate nella finestra popup di attività Windows hello o un elenco di attività Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="b2764-249">È possibile passare la finestra di attività tooanother facendo clic su di essa nella visualizzazione di calendario hello nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="b2764-250">È inoltre possibile utilizzare i tasti freccia sinistra/destra di hello Windows di attività superiore toosee hello da hello settimana precedente o hello settimana successiva.</span><span class="sxs-lookup"><span data-stu-id="b2764-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="b2764-251">È possibile utilizzare i pulsanti della barra degli strumenti hello nella finestra attività di hello inferiore riquadro toorerun hello o aggiornare i dettagli di hello nel riquadro di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="b2764-252">Script</span><span class="sxs-lookup"><span data-stu-id="b2764-252">Script</span></span>
<span data-ttu-id="b2764-253">È possibile utilizzare hello **Script** hello tooview scheda Definizione JSON di hello selezionato entità Data Factory (servizio collegato, set di dati o pipeline).</span><span class="sxs-lookup"><span data-stu-id="b2764-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="b2764-255">Uso delle viste di sistema</span><span class="sxs-lookup"><span data-stu-id="b2764-255">Use system views</span></span>
<span data-ttu-id="b2764-256">Monitoraggio e gestione di app Hello include viste di sistema predefinito (**windows attività recente**, **attività windows non**, **finestre attività In corso**) che consentono di windows di recente o non è riuscita o in corso attività tooview per la data factory.</span><span class="sxs-lookup"><span data-stu-id="b2764-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="b2764-257">Passare toohello **visualizzazioni di monitoraggio** scheda sinistra hello facendovi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="b2764-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Scheda Monitoring Views](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="b2764-259">Al momento sono disponibili tre viste di sistema supportate.</span><span class="sxs-lookup"><span data-stu-id="b2764-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="b2764-260">Selezionare un'opzione toosee recenti attività windows, windows di attività non riuscita o in corso attività di windows nell'elenco di attività Windows hello (nella parte inferiore di hello del riquadro centrale hello).</span><span class="sxs-lookup"><span data-stu-id="b2764-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="b2764-261">Quando si seleziona hello **windows attività recente** opzione, viene visualizzato recente tutte le finestre attività in ordine decrescente di hello **ora dell'ultimo tentativo**.</span><span class="sxs-lookup"><span data-stu-id="b2764-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="b2764-262">È possibile utilizzare hello **attività windows non** visualizzare le finestre attività toosee tutti non riuscita nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="b2764-263">Selezionare una finestra di attività non riuscita in hello elenco toosee dettagli in hello **proprietà** finestra o hello **attività finestra Esplora**.</span><span class="sxs-lookup"><span data-stu-id="b2764-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="b2764-264">È anche possibile scaricare i log relativi a una finestra attività non riuscita.</span><span class="sxs-lookup"><span data-stu-id="b2764-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="b2764-265">Ordinamento e filtro delle finestre attività</span><span class="sxs-lookup"><span data-stu-id="b2764-265">Sort and filter activity windows</span></span>
<span data-ttu-id="b2764-266">Hello modifica **ora di inizio** e **ora di fine** impostazioni nel comando hello barra toofilter windows di attività.</span><span class="sxs-lookup"><span data-stu-id="b2764-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="b2764-267">Dopo aver modificato hello ora di inizio e fine, fare clic su hello pulsante Avanti toohello fine ora toorefresh hello attività elenco di Windows.</span><span class="sxs-lookup"><span data-stu-id="b2764-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Ora di inizio e ora di fine](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="b2764-269">Tutte le volte in cui sono attualmente in formato UTC in app di gestione e monitoraggio hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="b2764-270">In hello **elenco attività Windows**, fare clic sul nome di una colonna hello (ad esempio: stato).</span><span class="sxs-lookup"><span data-stu-id="b2764-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Menu della colonna nell'elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="b2764-272">È possibile eseguire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b2764-272">You can do hello following:</span></span>

* <span data-ttu-id="b2764-273">Applicare l'ordinamento crescente.</span><span class="sxs-lookup"><span data-stu-id="b2764-273">Sort in ascending order.</span></span>
* <span data-ttu-id="b2764-274">Applicare l'ordinamento decrescente.</span><span class="sxs-lookup"><span data-stu-id="b2764-274">Sort in descending order.</span></span>
* <span data-ttu-id="b2764-275">Filtrare in base a uno o più valori, ad esempio Pronto, In attesa e così via.</span><span class="sxs-lookup"><span data-stu-id="b2764-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="b2764-276">Quando si specifica un filtro su una colonna, verrà visualizzato il pulsante di filtro hello abilitato per la colonna, che indica che i valori nella colonna hello hello sono valori filtrati.</span><span class="sxs-lookup"><span data-stu-id="b2764-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filtrare una colonna dell'elenco di attività Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="b2764-278">È possibile utilizzare hello stessi filtri di tooclear finestra popup.</span><span class="sxs-lookup"><span data-stu-id="b2764-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="b2764-279">tooclear tutti i filtri per l'elenco di attività Windows hello, fare clic su pulsante Cancella filtro hello hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b2764-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Cancella tutti i filtri per l'elenco di attività Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="b2764-281">Esecuzione di azioni batch</span><span class="sxs-lookup"><span data-stu-id="b2764-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="b2764-282">Rieseguire finestre attività selezionate</span><span class="sxs-lookup"><span data-stu-id="b2764-282">Rerun selected activity windows</span></span>
<span data-ttu-id="b2764-283">Selezionare una finestra attività, fare clic su hello freccia giù per hello primo pulsante e selezionare **Riesegui** / **eseguire di nuovo con monte nella pipeline**.</span><span class="sxs-lookup"><span data-stu-id="b2764-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="b2764-284">Quando si seleziona hello **eseguire di nuovo con monte nella pipeline** , opzione consente di rieseguire anche tutte le finestre attività upstream.</span><span class="sxs-lookup"><span data-stu-id="b2764-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="b2764-285">![Rieseguire una finestra attività](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="b2764-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="b2764-286">È anche possibile selezionare più finestre di attività nell'elenco di hello ed eseguirli di nuovo in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b2764-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="b2764-287">È possibile impostare toofilter attività in base allo stato hello (ad esempio: **non riuscito**) e quindi eseguire nuovamente windows attività hello non è riuscita dopo aver risolto il problema hello che causa toofail di windows hello attività.</span><span class="sxs-lookup"><span data-stu-id="b2764-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="b2764-288">Vedere la seguente sezione per informazioni dettagliate sui filtri delle finestre di attività nell'elenco di hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="b2764-289">Sospendere o riprendere l'esecuzione di più pipeline</span><span class="sxs-lookup"><span data-stu-id="b2764-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="b2764-290">È possibile multiselect due o più pipeline tasto Ctrl hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="b2764-291">È possibile utilizzare i pulsanti della barra di comando hello (che vengono evidenziati nel rettangolo rosso hello hello seguente immagine) o ripresa di toopause li.</span><span class="sxs-lookup"><span data-stu-id="b2764-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Sospendere o riprendere hello barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="b2764-293">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="b2764-293">Create alerts</span></span>
<span data-ttu-id="b2764-294">Hello **avvisi** pagina consente di creare un avviso e gli avvisi esistenti Visualizza/Modifica/eliminazione.</span><span class="sxs-lookup"><span data-stu-id="b2764-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="b2764-295">Permette anche di abilitare o disabilitare un avviso.</span><span class="sxs-lookup"><span data-stu-id="b2764-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="b2764-296">toosee hello pagina avvisi, fare clic su hello **avvisi** scheda.</span><span class="sxs-lookup"><span data-stu-id="b2764-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Scheda Alerts](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="b2764-298">toocreate un avviso</span><span class="sxs-lookup"><span data-stu-id="b2764-298">toocreate an alert</span></span>
1. <span data-ttu-id="b2764-299">Fare clic su **Aggiungi avviso** tooadd un avviso.</span><span class="sxs-lookup"><span data-stu-id="b2764-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="b2764-300">Vedrai hello **dettagli** pagina.</span><span class="sxs-lookup"><span data-stu-id="b2764-300">You see hello **Details** page.</span></span>

    ![Creazione di avvisi: pagina Details](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="b2764-302">Specificare hello **nome** e **descrizione** avviso hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b2764-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="b2764-303">Dovrebbe essere hello **filtri** pagina.</span><span class="sxs-lookup"><span data-stu-id="b2764-303">You should see hello **Filters** page.</span></span>

    ![Creazione di avvisi: pagina Filters](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="b2764-305">Seleziona hello **evento**, **stato**, e **substatus** che si desidera toocreate (facoltativo) un servizio Data Factory di avviso per e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b2764-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="b2764-306">Dovrebbe essere hello **destinatari** pagina.</span><span class="sxs-lookup"><span data-stu-id="b2764-306">You should see hello **Recipients** page.</span></span>

    ![Creazione di avvisi: pagina Recipients](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="b2764-308">Seleziona hello **gli amministratori delle sottoscrizioni di posta elettronica** opzione e/o immettere un **e-mail amministratore aggiuntiva**, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b2764-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="b2764-309">Verrà visualizzato l'avviso hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="b2764-309">You should see hello alert in hello list.</span></span>

    ![Elenco degli avvisi](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="b2764-311">Nell'elenco di avvisi hello, utilizzare i pulsanti di hello associati hello avviso tooedit/delete/Abilita/disabilita un avviso.</span><span class="sxs-lookup"><span data-stu-id="b2764-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="b2764-312">Evento, stato e stato secondario</span><span class="sxs-lookup"><span data-stu-id="b2764-312">Event/status/substatus</span></span>
<span data-ttu-id="b2764-313">Hello nella tabella seguente sono elencate per hello eventi disponibili e gli stati (e stati secondari).</span><span class="sxs-lookup"><span data-stu-id="b2764-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="b2764-314">Nome evento</span><span class="sxs-lookup"><span data-stu-id="b2764-314">Event name</span></span> | <span data-ttu-id="b2764-315">Stato</span><span class="sxs-lookup"><span data-stu-id="b2764-315">Status</span></span> | <span data-ttu-id="b2764-316">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="b2764-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2764-317">Esecuzione attività avviata</span><span class="sxs-lookup"><span data-stu-id="b2764-317">Activity Run Started</span></span> |<span data-ttu-id="b2764-318">Started</span><span class="sxs-lookup"><span data-stu-id="b2764-318">Started</span></span> |<span data-ttu-id="b2764-319">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="b2764-319">Starting</span></span> |
| <span data-ttu-id="b2764-320">Esecuzione attività terminata</span><span class="sxs-lookup"><span data-stu-id="b2764-320">Activity Run Finished</span></span> |<span data-ttu-id="b2764-321">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b2764-321">Succeeded</span></span> |<span data-ttu-id="b2764-322">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b2764-322">Succeeded</span></span> |
| <span data-ttu-id="b2764-323">Esecuzione attività terminata</span><span class="sxs-lookup"><span data-stu-id="b2764-323">Activity Run Finished</span></span> |<span data-ttu-id="b2764-324">Non riuscito</span><span class="sxs-lookup"><span data-stu-id="b2764-324">Failed</span></span> |<span data-ttu-id="b2764-325">Allocazione risorse non riuscita</span><span class="sxs-lookup"><span data-stu-id="b2764-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="b2764-326">Esecuzione non riuscita</span><span class="sxs-lookup"><span data-stu-id="b2764-326">Failed Execution</span></span><br/><br/><span data-ttu-id="b2764-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="b2764-327">Timed Out</span></span><br/><br/><span data-ttu-id="b2764-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="b2764-328">Failed Validation</span></span><br/><br/><span data-ttu-id="b2764-329">Abbandonato</span><span class="sxs-lookup"><span data-stu-id="b2764-329">Abandoned</span></span> |
| <span data-ttu-id="b2764-330">Creazione cluster HDI su richiesta avviata</span><span class="sxs-lookup"><span data-stu-id="b2764-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="b2764-331">Started</span><span class="sxs-lookup"><span data-stu-id="b2764-331">Started</span></span> |-|
| <span data-ttu-id="b2764-332">Creazione cluster HDI su richiesta completata</span><span class="sxs-lookup"><span data-stu-id="b2764-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="b2764-333">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b2764-333">Succeeded</span></span> |-|
| <span data-ttu-id="b2764-334">Cluster HDI su richiesta eliminato</span><span class="sxs-lookup"><span data-stu-id="b2764-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="b2764-335">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b2764-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="b2764-336">tooedit, eliminare o disabilitare un avviso</span><span class="sxs-lookup"><span data-stu-id="b2764-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="b2764-337">Utilizzare hello seguente tooedit pulsanti (evidenziati in rosso), eliminare o disabilitare un avviso.</span><span class="sxs-lookup"><span data-stu-id="b2764-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Pulsanti degli avvisi](./media/data-factory-monitor-manage-app/AlertButtons.png)
