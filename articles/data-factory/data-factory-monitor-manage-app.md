---
title: Monitorare e gestire le pipeline di dati - Azure | Documentazione Microsoft
description: Informazioni sull'uso dell'app di monitoraggio e gestione per monitorare e gestire le data factory e le pipeline di Azure.
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
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="85426-103">Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="85426-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85426-104">Con il portale di Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="85426-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="85426-105">Con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="85426-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="85426-106">Questo articolo descrive come usare l'app di monitoraggio e gestione per monitorare, gestire ed eseguire il debug delle pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="85426-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="85426-107">L'articolo contiene anche informazioni su come creare avvisi per ricevere notifiche relative agli errori.</span><span class="sxs-lookup"><span data-stu-id="85426-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="85426-108">Per un'introduzione all'uso dell'applicazione, vedere il video seguente:</span><span class="sxs-lookup"><span data-stu-id="85426-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="85426-109">L'interfaccia utente visualizzata nel video potrebbe non corrispondere esattamente a ciò che viene visualizzato nel portale.</span><span class="sxs-lookup"><span data-stu-id="85426-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="85426-110">L'interfaccia visualizzata nel video è di poco precedente, ma i concetti rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="85426-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="85426-111">Avviare l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="85426-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="85426-112">Per avviare l'app di monitoraggio e gestione, fare clic sul riquadro **Monitoraggio e gestione** nel pannello **Data factory** della data factory.</span><span class="sxs-lookup"><span data-stu-id="85426-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Riquadro di monitoraggio nella home page di Data Factory](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="85426-114">L'app di monitoraggio e gestione si apre in una finestra separata.</span><span class="sxs-lookup"><span data-stu-id="85426-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![App di monitoraggio e gestione](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="85426-116">Se il Web browser è bloccato su "Concessione autorizzazioni in corso...", deselezionare la casella di controllo **Block third-party cookies and site data** (Blocco dei cookie di terze parti e dei dati dei siti) oppure lasciarla abilitata e creare un'eccezione per **login.microsoftonline.com** quindi provare di nuovo ad aprire l'app.</span><span class="sxs-lookup"><span data-stu-id="85426-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="85426-117">Nell'elenco di finestre attività nel riquadro centrale viene visualizzata una finestra attività per ogni esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="85426-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="85426-118">Se ad esempio un'attività è pianificata per essere eseguita ogni ora per cinque ore, sono visualizzate cinque finestre attività associate a cinque sezioni dati.</span><span class="sxs-lookup"><span data-stu-id="85426-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="85426-119">Se nell'elenco in basso non sono visualizzate finestre attività, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="85426-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="85426-120">Aggiornare i filtri relativi all'**ora di inizio** e all'**ora di fine** nella parte superiore in modo che corrispondano all'ora di inizio e all'ora di fine della pipeline e quindi fare clic sul pulsante **Applica**.</span><span class="sxs-lookup"><span data-stu-id="85426-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="85426-121">L'elenco delle finestre attività non viene aggiornato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="85426-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="85426-122">Fare clic sul pulsante **Aggiorna** sulla barra degli strumenti dell'elenco delle **finestre attività**.</span><span class="sxs-lookup"><span data-stu-id="85426-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="85426-123">Se non è disponibile un'applicazione Data Factory con cui testare questa procedura, eseguire l'esercitazione [Copiare dati da un archivio BLOB al database SQL usando Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="85426-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="85426-124">Informazioni sull'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="85426-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="85426-125">Sulla sinistra sono presenti tre schede: **Esplora risorse**, **Monitoring Views** (Visualizzazioni monitoraggio) e **Avvisi**.</span><span class="sxs-lookup"><span data-stu-id="85426-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="85426-126">La prima scheda (**Esplora risorse**) è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="85426-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="85426-127">Scheda Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="85426-127">Resource Explorer</span></span>
<span data-ttu-id="85426-128">Saranno visualizzate le informazioni illustrate nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="85426-128">You see the following:</span></span>

* <span data-ttu-id="85426-129">**Visualizzazione albero** di Esplora risorse nel pannello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="85426-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="85426-130">La **vista diagramma** nella parte superiore del riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="85426-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="85426-131">L'elenco **Activity Windows** (Finestre attività) in basso al riquadro nella parte centrale.</span><span class="sxs-lookup"><span data-stu-id="85426-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="85426-132">Le schede **Proprietà**, **Activity Window Explorer** (Esplora finestre attività) e **Script** nel riquadro destro.</span><span class="sxs-lookup"><span data-stu-id="85426-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="85426-133">In Esplora inventario risorse è possibile visualizzare tutte le risorse della data factory, ovvero le pipeline, i set di dati e i servizi collegati, in una visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="85426-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="85426-134">Quando si seleziona un oggetto in Esplora risorse:</span><span class="sxs-lookup"><span data-stu-id="85426-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="85426-135">L'entità di Data Factory associata viene evidenziata nella visualizzazione diagramma.</span><span class="sxs-lookup"><span data-stu-id="85426-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="85426-136">Le [finestre attività associate](data-factory-scheduling-and-execution.md) vengono evidenziate nell'elenco Activity Windows (Finestre attività).</span><span class="sxs-lookup"><span data-stu-id="85426-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="85426-137">Le proprietà dell'oggetto selezionato vengono visualizzate nella finestra Proprietà nel riquadro a destra.</span><span class="sxs-lookup"><span data-stu-id="85426-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="85426-138">Viene mostrata la definizione JSON dell’oggetto selezionato, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="85426-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="85426-139">Ad esempio: un servizio collegato, un set di dati o una pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Scheda Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="85426-141">Per informazioni dettagliate sulle finestre attività, vedere l'articolo [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="85426-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="85426-142">Visualizzazione diagramma</span><span class="sxs-lookup"><span data-stu-id="85426-142">Diagram View</span></span>
<span data-ttu-id="85426-143">La visualizzazione diagramma di una data factory offre un'unica console da cui monitorare e gestire la data factory e i relativi asset.</span><span class="sxs-lookup"><span data-stu-id="85426-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="85426-144">Quando si seleziona un'entità di Data Factory, (un set di dati o una pipeline) nella visualizzazione diagramma:</span><span class="sxs-lookup"><span data-stu-id="85426-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="85426-145">L'entità di Data Factory viene selezionata nella visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="85426-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="85426-146">Le finestre attività associate vengono evidenziate nell'elenco Activity Windows (Finestre attività).</span><span class="sxs-lookup"><span data-stu-id="85426-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="85426-147">Le proprietà dell'oggetto selezionato vengono visualizzate nella finestra Proprietà.</span><span class="sxs-lookup"><span data-stu-id="85426-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="85426-148">Quando la pipeline è abilitata (vale a dire non sospesa), viene visualizzata con una linea verde:</span><span class="sxs-lookup"><span data-stu-id="85426-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline in esecuzione](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="85426-150">È possibile mettere in pausa, riprendere o terminare una pipeline selezionandola nella vista diagramma e usando i pulsanti sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="85426-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Sospensione/ripresa nella barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="85426-152">Nella visualizzazione diagramma sono presenti tre pulsanti per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="85426-153">Il secondo pulsante può essere usato per sospendere l'esecuzione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="85426-154">La sospensione non termina le attività attualmente in esecuzione e le lascia continuare fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="85426-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="85426-155">Il terzo pulsante sospende l'esecuzione della pipeline e termina le attività esistenti in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="85426-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="85426-156">Il primo pulsante riprende l'esecuzione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="85426-157">Quando la pipeline è in pausa, il suo colore diventa giallo.</span><span class="sxs-lookup"><span data-stu-id="85426-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="85426-158">Ad esempio, una pipeline in pausa ha l'aspetto illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="85426-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Pipeline in pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="85426-160">È possibile selezionare contemporaneamente due o più pipeline tramite il tasto CTRL.</span><span class="sxs-lookup"><span data-stu-id="85426-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="85426-161">È possibile utilizzare i pulsanti della barra dei comandi per sospendere o riprendere più pipeline contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="85426-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="85426-162">È anche possibile fare clic con il pulsante destro del mouse su una pipeline e selezionare le opzioni corrispondenti alla sospensione, alla ripresa o all'interruzione.</span><span class="sxs-lookup"><span data-stu-id="85426-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Menu di scelta rapida per le pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="85426-164">Fare clic sull'opzione **Apri pipeline** per visualizzare tutte le attività all'interno della pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Menu Apri pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="85426-166">Nella visualizzazione pipeline aperta vengono visualizzate tutte le attività della pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="85426-167">In questo esempio è presente soltanto l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="85426-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Pipeline aperta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="85426-169">Per tornare alla visualizzazione precedente, fare clic sul nome della data factory nel menu di navigazione nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="85426-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="85426-170">Quando si seleziona un set di dati di output o si passa il mouse su un set di questo tipo, nella vista della pipeline viene visualizzata la finestra popup delle finestre attività relative al set di dati selezionato.</span><span class="sxs-lookup"><span data-stu-id="85426-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Finestra popup di Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="85426-172">È possibile fare clic su una finestra attività per visualizzarne i dettagli nella finestra **Proprietà** nel riquadro a destra.</span><span class="sxs-lookup"><span data-stu-id="85426-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Proprietà della finestra attività](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="85426-174">Nel riquadro destro passare alla scheda **Activity Windows** (Esplora finestra attività) per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="85426-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="85426-176">Vengono visualizzate anche le **variabili risolte** per ciascun tentativo di esecuzione di un'attività nella sezione **Tentativi**.</span><span class="sxs-lookup"><span data-stu-id="85426-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Variabili risolte](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="85426-178">Passare alla scheda **Script** per vedere la definizione dello script JSON per l'oggetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="85426-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="85426-180">Le finestre attività vengono visualizzate in tre posizioni:</span><span class="sxs-lookup"><span data-stu-id="85426-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="85426-181">Popup Activity Windows (Finestre attività) nella visualizzazione diagramma (nel riquadro centrale).</span><span class="sxs-lookup"><span data-stu-id="85426-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="85426-182">Activity Window Explorer (Esplora finestra attività) nel riquadro destro.</span><span class="sxs-lookup"><span data-stu-id="85426-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="85426-183">Elenco Activity Windows (Finestre attività) nel riquadro inferiore.</span><span class="sxs-lookup"><span data-stu-id="85426-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="85426-184">Nel popup Activity Windows (Finestre attività) e in Activity Window Explorer (Esplora finestra attività) è possibile scorrere fino alla settimana precedente e a quella successiva usando i pulsanti con la freccia sinistra e destra.</span><span class="sxs-lookup"><span data-stu-id="85426-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Freccia sinistra/destra in Activity Window Explorer (Esplora finestra attività)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="85426-186">Nella parte inferiore della visualizzazione diagramma, sono presenti i questi pulsanti: Fare zoom avanti, Fare zoom indietro, Adatta alla finestra, Zoom 100% e Lock layout (Blocca il layout).</span><span class="sxs-lookup"><span data-stu-id="85426-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="85426-187">Il pulsante **Lock layout** (Blocca il layout) impedisce di spostare accidentalmente tabelle e pipeline nella visualizzazione diagramma.</span><span class="sxs-lookup"><span data-stu-id="85426-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="85426-188">È attivo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="85426-188">It's on by default.</span></span> <span data-ttu-id="85426-189">È possibile disabilitarlo e spostare le entità nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="85426-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="85426-190">Quando il blocco viene disabilitato, è possibile usare l'ultimo pulsante per posizionare automaticamente pipeline e tabelle.</span><span class="sxs-lookup"><span data-stu-id="85426-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="85426-191">È inoltre possibile ingrandire o ridurre utilizzando la rotellina del mouse.</span><span class="sxs-lookup"><span data-stu-id="85426-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Comandi di zoom nella visualizzazione diagramma](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="85426-193">Elenco Activity Windows (Finestre attività)</span><span class="sxs-lookup"><span data-stu-id="85426-193">Activity Windows list</span></span>
<span data-ttu-id="85426-194">L'elenco Activity Windows (Finestre attività) nella parte inferiore del riquadro centrale riporta tutte le finestre attività per il set di dati selezionato in Esplora risorse o nella visualizzazione diagramma.</span><span class="sxs-lookup"><span data-stu-id="85426-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="85426-195">Per impostazione predefinita, l'elenco è in ordine decrescente. Ciò significa che la finestra attività più recente viene visualizzata in alto.</span><span class="sxs-lookup"><span data-stu-id="85426-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="85426-197">L'elenco non viene aggiornato automaticamente. Deve essere aggiornato manualmente usando il relativo pulsante nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="85426-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="85426-198">Di seguito sono riportati gli stati possibili per le finestre attività:</span><span class="sxs-lookup"><span data-stu-id="85426-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="85426-199">Stato</span><span class="sxs-lookup"><span data-stu-id="85426-199">Status</span></span></th><th align="left"><span data-ttu-id="85426-200">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="85426-200">Substatus</span></span></th><th align="left"><span data-ttu-id="85426-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="85426-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="85426-202">Waiting</span><span class="sxs-lookup"><span data-stu-id="85426-202">Waiting</span></span></td><td><span data-ttu-id="85426-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="85426-203">ScheduleTime</span></span></td><td><span data-ttu-id="85426-204">Non è ancora il momento di eseguire la finestra attività.</span><span class="sxs-lookup"><span data-stu-id="85426-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="85426-205">DatasetDependencies</span></span></td><td><span data-ttu-id="85426-206">Le dipendenze upstream non sono pronte.</span><span class="sxs-lookup"><span data-stu-id="85426-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="85426-207">ComputeResources</span></span></td><td><span data-ttu-id="85426-208">Le risorse di calcolo non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="85426-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="85426-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="85426-210">Tutte le istanze di attività sono occupate nell'esecuzione di altre finestre attività.</span><span class="sxs-lookup"><span data-stu-id="85426-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="85426-211">ActivityResume</span></span></td><td><span data-ttu-id="85426-212">L'attività è sospesa e non è possibile eseguire le finestre attività fino a quando non viene ripresa.</span><span class="sxs-lookup"><span data-stu-id="85426-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-213">Retry</span><span class="sxs-lookup"><span data-stu-id="85426-213">Retry</span></span></td><td><span data-ttu-id="85426-214">L'esecuzione dell'attività viene ritentata.</span><span class="sxs-lookup"><span data-stu-id="85426-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-215">Convalida</span><span class="sxs-lookup"><span data-stu-id="85426-215">Validation</span></span></td><td><span data-ttu-id="85426-216">La convalida non è ancora stata avviata.</span><span class="sxs-lookup"><span data-stu-id="85426-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="85426-217">ValidationRetry</span></span></td><td><span data-ttu-id="85426-218">La convalida è in attesa di essere ripetuta.</span><span class="sxs-lookup"><span data-stu-id="85426-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="85426-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="85426-219">InProgress</span></span></td><td><span data-ttu-id="85426-220">Convalida in corso.</span><span class="sxs-lookup"><span data-stu-id="85426-220">Validating</span></span></td><td><span data-ttu-id="85426-221">La convalida è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="85426-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="85426-222">È in corso l'elaborazione della finestra attività.</span><span class="sxs-lookup"><span data-stu-id="85426-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="85426-223">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="85426-223">Failed</span></span></td><td><span data-ttu-id="85426-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="85426-224">TimedOut</span></span></td><td><span data-ttu-id="85426-225">L'esecuzione dell'attività ha richiesto più tempo di quello consentito dall'attività.</span><span class="sxs-lookup"><span data-stu-id="85426-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="85426-226">Canceled</span></span></td><td><span data-ttu-id="85426-227">La finestra attività è stata annullata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="85426-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-228">Convalida</span><span class="sxs-lookup"><span data-stu-id="85426-228">Validation</span></span></td><td><span data-ttu-id="85426-229">Convalida non riuscita.</span><span class="sxs-lookup"><span data-stu-id="85426-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="85426-230">Non è stato possibile generare o convalidare la finestra attività.</span><span class="sxs-lookup"><span data-stu-id="85426-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="85426-231">Ready</span><span class="sxs-lookup"><span data-stu-id="85426-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="85426-232">La finestra attività è pronta per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="85426-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="85426-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="85426-234">La finestra attività non è stata elaborata.</span><span class="sxs-lookup"><span data-stu-id="85426-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="85426-235">None</span><span class="sxs-lookup"><span data-stu-id="85426-235">None</span></span></td><td>-</td><td><span data-ttu-id="85426-236">Una finestra attività esistente che in precedenza aveva un altro stato e che ora è stata reimpostata.</span><span class="sxs-lookup"><span data-stu-id="85426-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="85426-237">Quando si fa clic su una finestra attività nell'elenco, i relativi dettagli vengono visualizzati nella finestra **Activity Windows Explorer** (Esplora finestre attività) o **Proprietà** a destra.</span><span class="sxs-lookup"><span data-stu-id="85426-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="85426-239">Aggiornare le finestre attività</span><span class="sxs-lookup"><span data-stu-id="85426-239">Refresh activity windows</span></span>
<span data-ttu-id="85426-240">I dettagli non vengono aggiornati automaticamente. L'elenco delle finestre attività deve essere aggiornato manualmente usando il pulsante di aggiornamento, (il secondo pulsante) sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="85426-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="85426-241">Finestra Properties</span><span class="sxs-lookup"><span data-stu-id="85426-241">Properties window</span></span>
<span data-ttu-id="85426-242">La finestra Properties si trova nel riquadro destro dell'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="85426-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Finestra Properties](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="85426-244">Qui vengono visualizzate le proprietà dell'elemento selezionato nella visualizzazione albero di Resource Explorer, nella visualizzazione diagramma o nell'elenco delle Activity Windows (Finestre attività).</span><span class="sxs-lookup"><span data-stu-id="85426-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="85426-245">Esplora finestre attività</span><span class="sxs-lookup"><span data-stu-id="85426-245">Activity Window Explorer</span></span>
<span data-ttu-id="85426-246">La finestra **Activity Window Explorer** (Esplora finestre attività) si trova nel riquadro destro dell'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="85426-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="85426-247">Qui vengono visualizzati i dettagli relativi alla finestra attività selezionata nel popup o nell'elenco Activity Windows (Finestre attività).</span><span class="sxs-lookup"><span data-stu-id="85426-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="85426-249">Per passare a un'altra finestra attività, fare clic su di essa nella visualizzazione calendario in alto.</span><span class="sxs-lookup"><span data-stu-id="85426-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="85426-250">È anche possibile usare i pulsanti con la freccia sinistra o destra nella parte superiore per visualizzare le finestre attività della settimana precedente o successiva.</span><span class="sxs-lookup"><span data-stu-id="85426-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="85426-251">I pulsanti della barra degli strumenti nel riquadro inferiore consentono di rieseguire la finestra attività o di aggiornare i dettagli nel riquadro.</span><span class="sxs-lookup"><span data-stu-id="85426-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="85426-252">Script</span><span class="sxs-lookup"><span data-stu-id="85426-252">Script</span></span>
<span data-ttu-id="85426-253">È possibile usare la scheda **Script** per visualizzare la definizione JSON dell'entità Data Factory selezionata (servizio collegato, set di dati o pipeline).</span><span class="sxs-lookup"><span data-stu-id="85426-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="85426-255">Uso delle viste di sistema</span><span class="sxs-lookup"><span data-stu-id="85426-255">Use system views</span></span>
<span data-ttu-id="85426-256">L'app di monitoraggio e gestione include viste di sistema predefinite, (**Recent activity windows**, (Finestre attività recenti), **Failed activity windows** (Finestre attività non riuscite) e **In-Progress activity windows** (Finestre attività in corso)), che consentono di visualizzare le finestre attività recenti, non riuscite e in corso della data factory.</span><span class="sxs-lookup"><span data-stu-id="85426-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="85426-257">Fare clic per passare alla scheda **Visualizzazioni monitoraggio** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="85426-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Scheda Monitoring Views](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="85426-259">Al momento sono disponibili tre viste di sistema supportate.</span><span class="sxs-lookup"><span data-stu-id="85426-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="85426-260">Selezionare un'opzione per visualizzare le finestre attività recenti, non riuscite o in corso nell'elenco Activity Windows (Finestre attività), nella parte inferiore del riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="85426-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="85426-261">Quando si seleziona l'opzione **Recent activity windows** (Finestre attività recenti), le finestre attività recenti vengono visualizzate in ordine decrescente in base all'**ora dell'ultimo tentativo**.</span><span class="sxs-lookup"><span data-stu-id="85426-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="85426-262">L'opzione **Finestre attività non riuscite** consente di visualizzare tutte le finestre attività non riuscite nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="85426-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="85426-263">Selezionare una finestra attività non riuscita dall'elenco per visualizzarne i dettagli nella finestra **Proprietà** o in **Activity Window Explorer** (Esplora finestre attività).</span><span class="sxs-lookup"><span data-stu-id="85426-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="85426-264">È anche possibile scaricare i log relativi a una finestra attività non riuscita.</span><span class="sxs-lookup"><span data-stu-id="85426-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="85426-265">Ordinamento e filtro delle finestre attività</span><span class="sxs-lookup"><span data-stu-id="85426-265">Sort and filter activity windows</span></span>
<span data-ttu-id="85426-266">Modificare le impostazioni relative all'**ora di inizio** e all'**ora di fine** nella barra dei comandi per filtrare le finestre attività.</span><span class="sxs-lookup"><span data-stu-id="85426-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="85426-267">Dopo aver modificato queste impostazioni, fare clic sul pulsante accanto all'ora di fine per aggiornare l'elenco delle finestre attività.</span><span class="sxs-lookup"><span data-stu-id="85426-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Ora di inizio e ora di fine](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="85426-269">Al momento, nell'app di monitoraggio e gestione le ore sono in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="85426-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="85426-270">Nell' **elenco Finestre attività**fare clic sul nome di una colonna, ad esempio Stato.</span><span class="sxs-lookup"><span data-stu-id="85426-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Menu della colonna nell'elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="85426-272">A questo punto è possibile eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="85426-272">You can do the following:</span></span>

* <span data-ttu-id="85426-273">Applicare l'ordinamento crescente.</span><span class="sxs-lookup"><span data-stu-id="85426-273">Sort in ascending order.</span></span>
* <span data-ttu-id="85426-274">Applicare l'ordinamento decrescente.</span><span class="sxs-lookup"><span data-stu-id="85426-274">Sort in descending order.</span></span>
* <span data-ttu-id="85426-275">Filtrare in base a uno o più valori, ad esempio Pronto, In attesa e così via.</span><span class="sxs-lookup"><span data-stu-id="85426-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="85426-276">Quando si specifica un filtro in una colonna, il pulsante filtro è abilitato per la colonna a indicare che i valori nella colonna sono filtrati.</span><span class="sxs-lookup"><span data-stu-id="85426-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filtro della colonna dell'elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="85426-278">Per cancellare i filtri è possibile usare la stessa finestra popup.</span><span class="sxs-lookup"><span data-stu-id="85426-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="85426-279">Per cancellare tutti i filtri per l'elenco delle finestre attività, fare clic sul pulsante del filtro nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="85426-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Cancellare tutti i filtri nell'elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="85426-281">Esecuzione di azioni batch</span><span class="sxs-lookup"><span data-stu-id="85426-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="85426-282">Rieseguire finestre attività selezionate</span><span class="sxs-lookup"><span data-stu-id="85426-282">Rerun selected activity windows</span></span>
<span data-ttu-id="85426-283">Selezionare una finestra attività, fare clic sulla freccia giù del primo pulsante nella barra dei comandi e selezionare **Riesegui** / **Rerun with upstream in pipeline** (Riesegui con upstream nella pipeline).</span><span class="sxs-lookup"><span data-stu-id="85426-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="85426-284">L'opzione **Rerun with upstream in pipeline** (Riesegui con upstream nella pipeline) consente di rieseguire anche tutte le finestre attività upstream.</span><span class="sxs-lookup"><span data-stu-id="85426-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="85426-285">![Rieseguire una finestra attività](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="85426-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="85426-286">È anche possibile selezionare più finestre attività nell'elenco e rieseguirle contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="85426-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="85426-287">È possibile filtrare le finestre attività in base allo stato (ad esempio **Non riuscito**), quindi rieseguire le finestre attività non riuscite dopo aver corretto il problema che ne causa l'errore.</span><span class="sxs-lookup"><span data-stu-id="85426-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="85426-288">Vedere la sezione seguente per informazioni dettagliate sull'applicazione di filtri alle finestre attività nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="85426-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="85426-289">Sospendere o riprendere l'esecuzione di più pipeline</span><span class="sxs-lookup"><span data-stu-id="85426-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="85426-290">È possibile selezionare più due o più pipeline utilizzando il tasto CTRL.</span><span class="sxs-lookup"><span data-stu-id="85426-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="85426-291">È possibile utilizzare i pulsanti della barra dei comandi (che vengono evidenziati nel rettangolo rosso nella figura seguente) per sospendere o riprendere le pipeline.</span><span class="sxs-lookup"><span data-stu-id="85426-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Sospensione/ripresa nella barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="85426-293">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="85426-293">Create alerts</span></span>
<span data-ttu-id="85426-294">La pagina **Avvisi** consente di creare nuovi avvisi e di visualizzare, modificare o eliminare quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="85426-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="85426-295">Permette anche di abilitare o disabilitare un avviso.</span><span class="sxs-lookup"><span data-stu-id="85426-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="85426-296">Fare clic sulla scheda **Avvisi** per visualizzare la pagina.</span><span class="sxs-lookup"><span data-stu-id="85426-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Scheda Alerts](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="85426-298">Per creare un avviso</span><span class="sxs-lookup"><span data-stu-id="85426-298">To create an alert</span></span>
1. <span data-ttu-id="85426-299">Fare clic su **Aggiungi avviso** per aggiungere un avviso.</span><span class="sxs-lookup"><span data-stu-id="85426-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="85426-300">Verrà visualizzata la pagina **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="85426-300">You see the **Details** page.</span></span>

    ![Creazione di avvisi: pagina Details](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="85426-302">Specificare il **nome** e la **descrizione** dell'avviso e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="85426-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="85426-303">Viene visualizzata la pagina **Filtri** .</span><span class="sxs-lookup"><span data-stu-id="85426-303">You should see the **Filters** page.</span></span>

    ![Creazione di avvisi: pagina Filters](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="85426-305">Selezionare l'**evento**, lo **stato** e lo **stato secondario** (facoltativo) per cui si vuole creare un avviso dal servizio Data Factory e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="85426-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="85426-306">Dovrebbe essere visualizzata la pagina **Destinatari** .</span><span class="sxs-lookup"><span data-stu-id="85426-306">You should see the **Recipients** page.</span></span>

    ![Creazione di avvisi: pagina Recipients](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="85426-308">Selezionare l'opzione **Email subscription admins** (Invia email agli amministratori della sottoscrizione) e/o immettere un valore per l'**email degli amministratori aggiuntivi**, quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="85426-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="85426-309">L'avviso verrà visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="85426-309">You should see the alert in the list.</span></span>

    ![Elenco degli avvisi](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="85426-311">Nell'elenco degli avvisi, usare i pulsanti associati a un avviso per modificare, eliminare, disabilitare o abilitare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="85426-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="85426-312">Evento, stato e stato secondario</span><span class="sxs-lookup"><span data-stu-id="85426-312">Event/status/substatus</span></span>
<span data-ttu-id="85426-313">La tabella seguente fornisce l'elenco di eventi, stati e stati secondari disponibili.</span><span class="sxs-lookup"><span data-stu-id="85426-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="85426-314">Nome evento</span><span class="sxs-lookup"><span data-stu-id="85426-314">Event name</span></span> | <span data-ttu-id="85426-315">Stato</span><span class="sxs-lookup"><span data-stu-id="85426-315">Status</span></span> | <span data-ttu-id="85426-316">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="85426-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85426-317">Esecuzione attività avviata</span><span class="sxs-lookup"><span data-stu-id="85426-317">Activity Run Started</span></span> |<span data-ttu-id="85426-318">Started</span><span class="sxs-lookup"><span data-stu-id="85426-318">Started</span></span> |<span data-ttu-id="85426-319">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="85426-319">Starting</span></span> |
| <span data-ttu-id="85426-320">Esecuzione attività terminata</span><span class="sxs-lookup"><span data-stu-id="85426-320">Activity Run Finished</span></span> |<span data-ttu-id="85426-321">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="85426-321">Succeeded</span></span> |<span data-ttu-id="85426-322">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="85426-322">Succeeded</span></span> |
| <span data-ttu-id="85426-323">Esecuzione attività terminata</span><span class="sxs-lookup"><span data-stu-id="85426-323">Activity Run Finished</span></span> |<span data-ttu-id="85426-324">Non riuscito</span><span class="sxs-lookup"><span data-stu-id="85426-324">Failed</span></span> |<span data-ttu-id="85426-325">Allocazione risorse non riuscita</span><span class="sxs-lookup"><span data-stu-id="85426-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="85426-326">Esecuzione non riuscita</span><span class="sxs-lookup"><span data-stu-id="85426-326">Failed Execution</span></span><br/><br/><span data-ttu-id="85426-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="85426-327">Timed Out</span></span><br/><br/><span data-ttu-id="85426-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="85426-328">Failed Validation</span></span><br/><br/><span data-ttu-id="85426-329">Abbandonato</span><span class="sxs-lookup"><span data-stu-id="85426-329">Abandoned</span></span> |
| <span data-ttu-id="85426-330">Creazione cluster HDI su richiesta avviata</span><span class="sxs-lookup"><span data-stu-id="85426-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="85426-331">Started</span><span class="sxs-lookup"><span data-stu-id="85426-331">Started</span></span> |-|
| <span data-ttu-id="85426-332">Creazione cluster HDI su richiesta completata</span><span class="sxs-lookup"><span data-stu-id="85426-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="85426-333">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="85426-333">Succeeded</span></span> |-|
| <span data-ttu-id="85426-334">Cluster HDI su richiesta eliminato</span><span class="sxs-lookup"><span data-stu-id="85426-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="85426-335">Succeeded</span><span class="sxs-lookup"><span data-stu-id="85426-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="85426-336">Modificare, eliminare o disabilitare un avviso</span><span class="sxs-lookup"><span data-stu-id="85426-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="85426-337">Utilizzare i pulsanti seguenti (evidenziati in rosso) per modificare, eliminare o disabilitare un avviso.</span><span class="sxs-lookup"><span data-stu-id="85426-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Pulsanti degli avvisi](./media/data-factory-monitor-manage-app/AlertButtons.png)
