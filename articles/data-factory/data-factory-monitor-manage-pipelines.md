---
title: aaaMonitor e gestire le pipeline utilizzando hello portale di Azure e PowerShell | Documenti Microsoft
description: "Informazioni su come toouse hello portale di Azure e Azure PowerShell toomonitor e gestire hello Azure data factory e le pipeline che è stato creato."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="b820e-103">Monitorare e gestire le pipeline di Data Factory di Azure tramite il portale di Azure hello e PowerShell</span><span class="sxs-lookup"><span data-stu-id="b820e-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b820e-104">Con il portale di Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b820e-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="b820e-105">Con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="b820e-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="b820e-106">applicazione di monitoraggio e gestione Hello fornisce un supporto migliore per il monitoraggio e le pipeline di dati di gestione e risoluzione dei problemi relativi a eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="b820e-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="b820e-107">Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="b820e-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="b820e-108">In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug le pipeline tramite il portale di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b820e-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="b820e-109">Hello inoltre fornite informazioni su come toocreate gli avvisi e ottenere una notifica sugli errori.</span><span class="sxs-lookup"><span data-stu-id="b820e-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="b820e-110">Informazioni sulle pipeline e sugli stati delle attività</span><span class="sxs-lookup"><span data-stu-id="b820e-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="b820e-111">Utilizzando hello portale di Azure, è possibile:</span><span class="sxs-lookup"><span data-stu-id="b820e-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="b820e-112">Visualizzare la data factory come diagramma.</span><span class="sxs-lookup"><span data-stu-id="b820e-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="b820e-113">Visualizzare le attività all'interno di una pipeline.</span><span class="sxs-lookup"><span data-stu-id="b820e-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="b820e-114">Visualizzare set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="b820e-114">View input and output datasets.</span></span>

<span data-ttu-id="b820e-115">Questa sezione descrive anche la modalità di transizione dallo stato tooanother uno stato di una sezione di set di dati.</span><span class="sxs-lookup"><span data-stu-id="b820e-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="b820e-116">Passare a data factory di tooyour</span><span class="sxs-lookup"><span data-stu-id="b820e-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="b820e-117">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b820e-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b820e-118">Fare clic su **Data factory** menu hello sulla sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="b820e-119">Se non è visualizzata, fare clic su **più servizi >**, quindi fare clic su **Data factory** in hello **INTELLIGENCE + analisi** categoria.</span><span class="sxs-lookup"><span data-stu-id="b820e-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Esplora tutto > Data factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="b820e-121">In hello **Data factory** blade, factory di hello selezionare dati che si è interessati.</span><span class="sxs-lookup"><span data-stu-id="b820e-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Selezionare la data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="b820e-123">Si dovrebbe essere hello home page per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-123">You should see hello home page for hello data factory.</span></span>

   ![Pannello Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="b820e-125">Vista diagramma della data factory</span><span class="sxs-lookup"><span data-stu-id="b820e-125">Diagram view of your data factory</span></span>
<span data-ttu-id="b820e-126">Hello **diagramma** visualizzazione di una data factory offre un unico riquadro della finestra effetto cristallo toomonitor e gestire data factory di hello e delle relative risorse.</span><span class="sxs-lookup"><span data-stu-id="b820e-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="b820e-127">hello toosee **diagramma** visualizzare la data factory, fare clic su **diagramma** hello home page per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Vista diagramma](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="b820e-129">È possibile eseguire lo zoom avanti, eseguire lo zoom indietro, toofit zoom, zoom too100%, blocco hello del layout hello diagramma e posiziona automaticamente le pipeline e set di dati.</span><span class="sxs-lookup"><span data-stu-id="b820e-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="b820e-130">È inoltre possibile visualizzare informazioni sulla derivazione dei dati hello (vale a dire Mostra gli elementi a monte e a valle degli elementi selezionati).</span><span class="sxs-lookup"><span data-stu-id="b820e-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="b820e-131">Attività all'interno di una pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="b820e-132">Fare clic sulla pipeline hello e quindi fare clic su **pipeline aprire** toosee tutte le attività in hello pipeline, insieme ai set di dati di input e output per le attività di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="b820e-133">Questa funzionalità è utile quando la pipeline include più di un'attività e si desidera derivazione operative di hello toounderstand di una singola pipeline.</span><span class="sxs-lookup"><span data-stu-id="b820e-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menu Apri pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="b820e-135">In hello l'esempio seguente, viene visualizzato nella pipeline hello con un input e un output di un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="b820e-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Attività all'interno di una pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="b820e-137">È possibile spostarsi indietro toohello home page della data factory di hello facendo hello **Data factory** collegamento di navigazione hello nell'angolo superiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Spostarsi indietro toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="b820e-139">Stato di visualizzazione hello di ogni attività all'interno di una pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="b820e-140">È possibile visualizzare lo stato corrente di hello di un'attività visualizzando lo stato di hello di uno dei set di dati hello generati dalle attività hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="b820e-141">Facendo doppio clic su hello **OutputBlobTable** in hello **diagramma**, è possibile visualizzare tutte le sezioni di hello generate dall'esecuzione di attività diverse all'interno di una pipeline.</span><span class="sxs-lookup"><span data-stu-id="b820e-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="b820e-142">È possibile vedere che attività di copia hello è stato eseguito correttamente per hello ultime otto ore e prodotti sezioni hello hello **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="b820e-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Stato della pipeline hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="b820e-144">sezioni di set di dati Hello nella data factory di hello possono avere uno dei seguenti stati hello:</span><span class="sxs-lookup"><span data-stu-id="b820e-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="b820e-145">Stato</span><span class="sxs-lookup"><span data-stu-id="b820e-145">State</span></span></th><th align="left"><span data-ttu-id="b820e-146">Sottostato</span><span class="sxs-lookup"><span data-stu-id="b820e-146">Substate</span></span></th><th align="left"><span data-ttu-id="b820e-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b820e-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="b820e-148">Waiting</span><span class="sxs-lookup"><span data-stu-id="b820e-148">Waiting</span></span></td><td><span data-ttu-id="b820e-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="b820e-149">ScheduleTime</span></span></td><td><span data-ttu-id="b820e-150">tempo di Hello non venga per toorun sezione hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="b820e-151">DatasetDependencies</span></span></td><td><span data-ttu-id="b820e-152">le dipendenze upstream Hello non sono pronte.</span><span class="sxs-lookup"><span data-stu-id="b820e-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="b820e-153">ComputeResources</span></span></td><td><span data-ttu-id="b820e-154">risorse di calcolo Hello non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="b820e-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="b820e-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="b820e-156">Tutte le istanze di attività hello sono occupate con l'esecuzione di altre sezioni.</span><span class="sxs-lookup"><span data-stu-id="b820e-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="b820e-157">ActivityResume</span></span></td><td><span data-ttu-id="b820e-158">attività di Hello è sospesa e non possono essere eseguiti a intervalli hello finché non viene ripreso attività hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-159">Retry</span><span class="sxs-lookup"><span data-stu-id="b820e-159">Retry</span></span></td><td><span data-ttu-id="b820e-160">L'esecuzione dell'attività viene ritentata.</span><span class="sxs-lookup"><span data-stu-id="b820e-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-161">Convalida</span><span class="sxs-lookup"><span data-stu-id="b820e-161">Validation</span></span></td><td><span data-ttu-id="b820e-162">La convalida non è ancora stata avviata.</span><span class="sxs-lookup"><span data-stu-id="b820e-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="b820e-163">ValidationRetry</span></span></td><td><span data-ttu-id="b820e-164">La convalida è in attesa toobe ripetuta.</span><span class="sxs-lookup"><span data-stu-id="b820e-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="b820e-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="b820e-165">InProgress</span></span></td><td><span data-ttu-id="b820e-166">Convalida in corso.</span><span class="sxs-lookup"><span data-stu-id="b820e-166">Validating</span></span></td><td><span data-ttu-id="b820e-167">La convalida è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b820e-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="b820e-168">sezione Hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="b820e-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="b820e-169">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="b820e-169">Failed</span></span></td><td><span data-ttu-id="b820e-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b820e-170">TimedOut</span></span></td><td><span data-ttu-id="b820e-171">l'esecuzione dell'attività Hello ha richiesto più tempo rispetto a quelle consentite dall'attività hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="b820e-172">Canceled</span></span></td><td><span data-ttu-id="b820e-173">sezione Hello è stata annullata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b820e-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-174">Convalida</span><span class="sxs-lookup"><span data-stu-id="b820e-174">Validation</span></span></td><td><span data-ttu-id="b820e-175">Convalida non riuscita.</span><span class="sxs-lookup"><span data-stu-id="b820e-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="b820e-176">sezione Hello Impossibile toobe generato e/o convalidare.</span><span class="sxs-lookup"><span data-stu-id="b820e-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="b820e-177">Ready</span><span class="sxs-lookup"><span data-stu-id="b820e-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="b820e-178">sezione di Hello è pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b820e-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="b820e-179">Skipped</span></span></td><td><span data-ttu-id="b820e-180">Nessuno</span><span class="sxs-lookup"><span data-stu-id="b820e-180">None</span></span></td><td><span data-ttu-id="b820e-181">sezione Hello non elaborate.</span><span class="sxs-lookup"><span data-stu-id="b820e-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b820e-182">Nessuno</span><span class="sxs-lookup"><span data-stu-id="b820e-182">None</span></span></td><td>-</td><td><span data-ttu-id="b820e-183">Una sezione utilizza tooexist con un altro stato, ma è stato reimpostato.</span><span class="sxs-lookup"><span data-stu-id="b820e-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="b820e-184">È possibile visualizzare i dettagli di hello su una sezione facendo clic su una voce della sezione in hello **sezioni aggiornato di recente** blade.</span><span class="sxs-lookup"><span data-stu-id="b820e-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Dettagli della sezione](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="b820e-186">Se la sezione hello è stata eseguita più volte, vedrai più righe in hello **viene eseguita l'attività** elenco.</span><span class="sxs-lookup"><span data-stu-id="b820e-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="b820e-187">È possibile visualizzare informazioni dettagliate su un'attività eseguire facendo voce hello eseguire hello **viene eseguita l'attività** elenco.</span><span class="sxs-lookup"><span data-stu-id="b820e-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="b820e-188">Hello sono elencati tutti i file di log di hello, insieme a un messaggio di errore, se presente.</span><span class="sxs-lookup"><span data-stu-id="b820e-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="b820e-189">Questa funzionalità è utili registri di debug e di tooview senza tooleave la data factory.</span><span class="sxs-lookup"><span data-stu-id="b820e-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Dettagli esecuzione attività](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="b820e-191">Se non è la sezione hello in hello **pronto** stato, è possibile vedere le sezioni upstream hello che non sono pronto e bloccano l'intervallo corrente di hello l'esecuzione in hello **sezioni Upstream non pronte** elenco.</span><span class="sxs-lookup"><span data-stu-id="b820e-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="b820e-192">Questa funzionalità è utile quando è la sezione **in attesa** stato e si desidera che le dipendenze upstream toounderstand hello che hello sezione è in attesa.</span><span class="sxs-lookup"><span data-stu-id="b820e-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Sezioni upstream non pronte](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="b820e-194">Diagramma di stato del set di dati</span><span class="sxs-lookup"><span data-stu-id="b820e-194">Dataset state diagram</span></span>
<span data-ttu-id="b820e-195">Dopo la distribuzione di una data factory e hello pipeline dispongono di un periodo attivo valido, set di dati hello seziona transizione da uno stato tooanother.</span><span class="sxs-lookup"><span data-stu-id="b820e-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="b820e-196">Attualmente, lo stato della sezione hello segue hello seguente diagramma di stato:</span><span class="sxs-lookup"><span data-stu-id="b820e-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Diagramma di stato](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="b820e-198">il flusso di transizione dello stato di set di dati in data factory di Hello è hello seguente: in attesa -> In corso/In esecuzione (Validating) -> pronto/non riuscito.</span><span class="sxs-lookup"><span data-stu-id="b820e-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="b820e-199">sezione Hello viene avviato in un **in attesa** stato, in attesa di toobe precondizioni soddisfatti prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b820e-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="b820e-200">Quindi avvia l'esecuzione di attività hello e sezione hello diventa un **In corso** stato.</span><span class="sxs-lookup"><span data-stu-id="b820e-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="b820e-201">l'esecuzione dell'attività Hello potrebbe riuscire o meno.</span><span class="sxs-lookup"><span data-stu-id="b820e-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="b820e-202">sezione Hello è contrassegnato come **pronto** o **Failed**, in base ai risultati di hello dell'esecuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="b820e-203">È possibile reimpostare hello sezione toogo da hello **pronto** o **Failed** stato toohello **in attesa** stato.</span><span class="sxs-lookup"><span data-stu-id="b820e-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="b820e-204">È inoltre possibile contrassegnare lo stato di sezione hello troppo**Skip**, impedendo così l'attività hello eseguire e di non elaborazione hello sezione.</span><span class="sxs-lookup"><span data-stu-id="b820e-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="b820e-205">Sospendere e riprendere le pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-205">Pause and resume pipelines</span></span>
<span data-ttu-id="b820e-206">È possibile gestire le pipeline usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b820e-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="b820e-207">Ad esempio, è possibile sospendere e riprendere le pipeline eseguendo i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b820e-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b820e-208">vista diagramma Hello non supporta la sospensione e ripresa di pipeline.</span><span class="sxs-lookup"><span data-stu-id="b820e-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="b820e-209">Se si desidera toouse un'interfaccia utente, è possibile utilizzare Monitoraggio hello e la gestione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b820e-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="b820e-210">Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b820e-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="b820e-211">È possibile sospendere o sospendere le pipeline utilizzando hello **Suspend AzureRmDataFactoryPipeline** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b820e-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="b820e-212">Questo cmdlet è utile quando non si desidera toorun le pipeline finché non viene risolto un problema.</span><span class="sxs-lookup"><span data-stu-id="b820e-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="b820e-213">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b820e-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="b820e-214">Dopo hello problema è stato risolto con pipeline hello, è possibile riprendere pipeline hello sospeso eseguendo hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="b820e-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="b820e-215">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b820e-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="b820e-216">Eseguire il debug delle pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-216">Debug pipelines</span></span>
<span data-ttu-id="b820e-217">Data Factory di Azure offre funzionalità avanzate di toodebug e risolvere i problemi di pipeline utilizzando hello portale di Azure e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b820e-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="b820e-218">[! Si noti} è molto più semplice tootroubleshot hello di errori tramite Monitoraggio e gestione App.</span><span class="sxs-lookup"><span data-stu-id="b820e-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="b820e-219">Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b820e-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="b820e-220">Trovare gli errori in una pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-220">Find errors in a pipeline</span></span>
<span data-ttu-id="b820e-221">Se l'esecuzione dell'attività hello ha esito negativo in una pipeline, i set di dati di hello viene generato dalla pipeline hello è in stato di errore a causa di errore hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="b820e-222">È possibile eseguire il debug e risolvere gli errori nella Data Factory di Azure tramite hello dei seguenti metodi.</span><span class="sxs-lookup"><span data-stu-id="b820e-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="b820e-223">Utilizzare hello toodebug portale Azure un errore</span><span class="sxs-lookup"><span data-stu-id="b820e-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="b820e-224">In hello **tabella** pannello, fare clic sulla sezione problema hello con hello **stato** impostare troppo**non riuscito**.</span><span class="sxs-lookup"><span data-stu-id="b820e-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Pannello Tabella con sezione con errori](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="b820e-226">In hello **sezione dati** pannello, fare clic sull'attività hello eseguire che non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="b820e-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Sezione dati con un errore](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="b820e-228">In hello **Dettagli esecuzione attività** pannello, è possibile scaricare i file di hello associati con l'elaborazione di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="b820e-229">Fare clic su **scaricare** per stato/stderr toodownload hello file di log che contiene dettagli sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Pannello Dettagli esecuzione attività con errore](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="b820e-231">Utilizzare PowerShell toodebug un errore</span><span class="sxs-lookup"><span data-stu-id="b820e-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="b820e-232">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b820e-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="b820e-233">Eseguire hello **Get AzureRmDataFactorySlice** comando sezioni hello toosee e i relativi stati.</span><span class="sxs-lookup"><span data-stu-id="b820e-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="b820e-234">Si noterà una sezione con stato hello **Failed**.</span><span class="sxs-lookup"><span data-stu-id="b820e-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="b820e-235">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b820e-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="b820e-236">Sostituire **StartDateTime** con l'ora di inizio della pipeline.</span><span class="sxs-lookup"><span data-stu-id="b820e-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="b820e-237">A questo punto, eseguire hello **Get AzureRmDataFactoryRun** tooget cmdlet dettagli attività hello eseguire per sezione hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="b820e-238">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b820e-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="b820e-239">il valore di Hello di StartDateTime è ora di inizio hello sezione errore/problema hello annotato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="b820e-240">Data e ora Hello deve essere racchiuse tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="b820e-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="b820e-241">Verrà visualizzato l'output con i dettagli sull'errore hello che è simile toohello seguente:</span><span class="sxs-lookup"><span data-stu-id="b820e-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="b820e-242">È possibile eseguire hello **Salva AzureRmDataFactoryLog** cmdlet con il valore Id vedere dall'output di hello e scaricare i file di log di hello utilizzando hello hello **- DownloadLogsoption** per hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b820e-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="b820e-243">Eseguire nuovamente le operazioni non riuscite in una pipeline</span><span class="sxs-lookup"><span data-stu-id="b820e-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b820e-244">È più facile tootroubleshoot errori ed eseguire di nuovo le sezioni non riuscite utilizzando hello monitoraggio e gestione delle App.</span><span class="sxs-lookup"><span data-stu-id="b820e-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="b820e-245">Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="b820e-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="b820e-246">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b820e-246">Use hello Azure portal</span></span>
<span data-ttu-id="b820e-247">Dopo aver il debug degli errori in una pipeline di risoluzione dei problemi, è possibile rieseguire errori passando sezione errore toohello e facendo clic su hello **eseguire** pulsante sulla barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="b820e-249">Nel caso sezione hello convalida non è riuscita a causa di un errore dei criteri (ad esempio, se dati non sono disponibili), è possibile correggere l'errore hello e convalidare di nuovo facendo hello **convalida** pulsante sulla barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Correggere gli errori e convalidare](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="b820e-251">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b820e-251">Use Azure PowerShell</span></span>
<span data-ttu-id="b820e-252">È possibile eseguire nuovamente gli errori utilizzando hello **Set AzureRmDataFactorySliceStatus** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b820e-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="b820e-253">Vedere hello [Set AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) argomento per la sintassi e altri dettagli sul cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="b820e-254">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="b820e-254">**Example:**</span></span>

<span data-ttu-id="b820e-255">esempio Hello Imposta stato hello di tutte le sezioni per hello nella tabella 'DAWikiAggregatedData' too'Waiting' in hello data factory di Azure 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="b820e-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="b820e-256">Hello 'Tipo di aggiornamento' è impostato too'UpstreamInPipeline ', il che significa che gli stati di ogni sezione per la tabella hello e tutte le tabelle (upstream) dipendenti hello siano impostati too'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="b820e-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="b820e-257">Hello altri valori possibili per questo parametro sono 'Individuale'.</span><span class="sxs-lookup"><span data-stu-id="b820e-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="b820e-258">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="b820e-258">Create alerts</span></span>
<span data-ttu-id="b820e-259">Azure registra eventi utente quando una risorsa di Azure (ad esempio, una data factory) viene creata, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="b820e-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="b820e-260">È possibile creare avvisi per questi eventi.</span><span class="sxs-lookup"><span data-stu-id="b820e-260">You can create alerts on these events.</span></span> <span data-ttu-id="b820e-261">È possibile utilizzare Data Factory toocapture diverse metriche e creare avvisi per le metriche.</span><span class="sxs-lookup"><span data-stu-id="b820e-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="b820e-262">È consigliabile usare gli eventi per il monitoraggio in tempo reale e le metriche per motivi cronologici.</span><span class="sxs-lookup"><span data-stu-id="b820e-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="b820e-263">Avvisi relativi agli eventi</span><span class="sxs-lookup"><span data-stu-id="b820e-263">Alerts on events</span></span>
<span data-ttu-id="b820e-264">Gli eventi di Azure forniscono utili informazioni su quanto accade alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b820e-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="b820e-265">Quando si usa Azure Data Factory, vengono generati eventi quando:</span><span class="sxs-lookup"><span data-stu-id="b820e-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="b820e-266">Una data factory viene creata, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="b820e-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="b820e-267">L'elaborazione dati (esecuzione) viene avviata o completata.</span><span class="sxs-lookup"><span data-stu-id="b820e-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="b820e-268">Un cluster HDInsight su richiesta viene creato o rimosso.</span><span class="sxs-lookup"><span data-stu-id="b820e-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="b820e-269">È possibile creare avvisi per questi eventi utente e configurarli amministratore toohello le notifiche di posta elettronica toosend e coadministrators della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="b820e-270">Inoltre, è possibile specificare gli indirizzi di posta elettronica aggiuntivi di utenti che necessitano di tooreceive notifiche di posta elettronica quando vengono soddisfatte le condizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="b820e-271">Questa funzionalità è utile quando si desidera tooget notifiche in caso di errori e non toocontinuously monitoraggio la data factory.</span><span class="sxs-lookup"><span data-stu-id="b820e-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="b820e-272">Attualmente, portale hello non vengono visualizzati avvisi sugli eventi.</span><span class="sxs-lookup"><span data-stu-id="b820e-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="b820e-273">Hello utilizzare [monitoraggio e gestione di app](data-factory-monitor-manage-app.md) toosee tutti gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b820e-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="b820e-274">Specificare una definizione di avviso</span><span class="sxs-lookup"><span data-stu-id="b820e-274">Specify an alert definition</span></span>
<span data-ttu-id="b820e-275">toospecify una definizione di avviso, si crea un file JSON che descrive le operazioni che si desidera toobe avvisati sul hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="b820e-276">Nell'esempio seguente di hello, avviso hello invia una notifica di posta elettronica per hello RunFinished operazione.</span><span class="sxs-lookup"><span data-stu-id="b820e-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="b820e-277">toobe specifico, viene inviata una notifica di posta elettronica quando è stata completata un'esecuzione in data factory di hello e hello eseguire non è riuscita (stato = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="b820e-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="b820e-278">È possibile rimuovere **subStatus** dalla definizione JSON se non si desidera ricevere un avviso in caso di errore specifico toobe hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="b820e-279">In questo esempio imposta avviso hello per tutte le data factory nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b820e-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="b820e-280">Se si desidera toobe di avviso hello impostato per una particolare data factory, è possibile specificare data factory di **resourceUri** in hello **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="b820e-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="b820e-281">Hello nella tabella seguente sono elencate per hello operazioni disponibili e gli stati (e stati secondari).</span><span class="sxs-lookup"><span data-stu-id="b820e-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="b820e-282">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="b820e-282">Operation name</span></span> | <span data-ttu-id="b820e-283">Stato</span><span class="sxs-lookup"><span data-stu-id="b820e-283">Status</span></span> | <span data-ttu-id="b820e-284">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="b820e-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b820e-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="b820e-285">RunStarted</span></span> |<span data-ttu-id="b820e-286">Started</span><span class="sxs-lookup"><span data-stu-id="b820e-286">Started</span></span> |<span data-ttu-id="b820e-287">Starting</span><span class="sxs-lookup"><span data-stu-id="b820e-287">Starting</span></span> |
| <span data-ttu-id="b820e-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="b820e-288">RunFinished</span></span> |<span data-ttu-id="b820e-289">Failed/Succeeded</span><span class="sxs-lookup"><span data-stu-id="b820e-289">Failed / Succeeded</span></span> |<span data-ttu-id="b820e-290">Allocazione risorse non riuscita</span><span class="sxs-lookup"><span data-stu-id="b820e-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="b820e-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="b820e-291">Succeeded</span></span><br/><br/><span data-ttu-id="b820e-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="b820e-292">FailedExecution</span></span><br/><br/><span data-ttu-id="b820e-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b820e-293">TimedOut</span></span><br/><br/><span data-ttu-id="b820e-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="b820e-294"><Canceled</span></span><br/><br/><span data-ttu-id="b820e-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="b820e-295">FailedValidation</span></span><br/><br/><span data-ttu-id="b820e-296">Abbandonato</span><span class="sxs-lookup"><span data-stu-id="b820e-296">Abandoned</span></span> |
| <span data-ttu-id="b820e-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="b820e-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="b820e-298">Started</span><span class="sxs-lookup"><span data-stu-id="b820e-298">Started</span></span> | |
| <span data-ttu-id="b820e-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="b820e-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="b820e-300">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b820e-300">Succeeded</span></span> | |
| <span data-ttu-id="b820e-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="b820e-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="b820e-302">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="b820e-302">Succeeded</span></span> | |

<span data-ttu-id="b820e-303">Vedere [Crea regola di avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx) per informazioni dettagliate sugli elementi JSON hello utilizzati nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="b820e-304">Distribuire avviso hello</span><span class="sxs-lookup"><span data-stu-id="b820e-304">Deploy hello alert</span></span>
<span data-ttu-id="b820e-305">avviso di hello toodeploy, utilizzare cmdlet di Azure PowerShell hello **New AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b820e-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="b820e-306">Dopo la distribuzione del gruppo di risorse hello è stato completato, vedrai hello seguenti messaggi:</span><span class="sxs-lookup"><span data-stu-id="b820e-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="b820e-307">È possibile utilizzare hello [Crea regola di avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="b820e-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="b820e-308">payload JSON Hello è esempio JSON di toohello simile.</span><span class="sxs-lookup"><span data-stu-id="b820e-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="b820e-309">Recuperare l'elenco di hello di distribuzioni del gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="b820e-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="b820e-310">elenco di hello tooretrieve di distribuito distribuzioni del gruppo di risorse di Azure, utilizzare i cmdlet di hello **Get AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b820e-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="b820e-311">Risolvere i problemi relativi a eventi utente</span><span class="sxs-lookup"><span data-stu-id="b820e-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="b820e-312">È possibile visualizzare tutti gli eventi di hello che vengono generati dopo aver fatto clic hello **operazioni e le metriche** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b820e-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Riquadro Metriche e operazioni](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="b820e-314">Fare clic su hello **eventi** riquadro eventi hello toosee.</span><span class="sxs-lookup"><span data-stu-id="b820e-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Riquadro Eventi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="b820e-316">In hello **eventi** pannello, è possibile visualizzare i dettagli sugli eventi, eventi filtrati e così via.</span><span class="sxs-lookup"><span data-stu-id="b820e-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Pannello Eventi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="b820e-318">Fare clic su un **operazione** nell'elenco di operazioni hello che provoca un errore.</span><span class="sxs-lookup"><span data-stu-id="b820e-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Selezionare un'operazione](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="b820e-320">Fare clic su un **errore** dettagli sull'errore hello toosee dell'evento.</span><span class="sxs-lookup"><span data-stu-id="b820e-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Evento di errore](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="b820e-322">Vedere [informazioni dettagliate di Azure cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) per i cmdlet di PowerShell che è possibile utilizzare tooadd, ottenere o rimuovere gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b820e-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="b820e-323">Ecco alcuni esempi di utilizzo hello **Get AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b820e-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="b820e-324">Eseguire hello seguente get-help comandi toosee dettagli ed esempi per cmdlet Get-AlertRule hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="b820e-325">Se viene visualizzato gli eventi di generazione dell'avviso hello in hello portale pannello ma non ricevere notifiche tramite posta elettronica, controllare se l'indirizzo di posta elettronica hello specificato è impostato tooreceive messaggi di posta elettronica da mittenti esterni.</span><span class="sxs-lookup"><span data-stu-id="b820e-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="b820e-326">messaggi di avviso Hello potrebbero sono state bloccate dalle impostazioni di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b820e-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="b820e-327">Avvisi relativi alle metriche</span><span class="sxs-lookup"><span data-stu-id="b820e-327">Alerts on metrics</span></span>
<span data-ttu-id="b820e-328">Azure Data Factory consente di acquisire diverse metriche e di creare avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="b820e-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="b820e-329">È possibile monitorare e creare avvisi per hello seguenti metriche per le sezioni hello la data factory:</span><span class="sxs-lookup"><span data-stu-id="b820e-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="b820e-330">**Esecuzioni non riuscite**</span><span class="sxs-lookup"><span data-stu-id="b820e-330">**Failed Runs**</span></span>
* <span data-ttu-id="b820e-331">**Esecuzioni riuscite**</span><span class="sxs-lookup"><span data-stu-id="b820e-331">**Successful Runs**</span></span>

<span data-ttu-id="b820e-332">Queste metriche sono utili e consentono una panoramica generale e non viene eseguito in data factory di hello tooget.</span><span class="sxs-lookup"><span data-stu-id="b820e-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="b820e-333">Le metriche vengono emesse ogni volta che viene eseguita una sezione.</span><span class="sxs-lookup"><span data-stu-id="b820e-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="b820e-334">Inizio hello ora hello, queste metriche vengono aggregate e inserito tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b820e-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="b820e-335">metriche tooenable, impostare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b820e-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="b820e-336">Abilitazione di metriche</span><span class="sxs-lookup"><span data-stu-id="b820e-336">Enable metrics</span></span>
<span data-ttu-id="b820e-337">tooenable metriche, fare clic su informazioni seguenti hello hello **Data Factory** pannello:</span><span class="sxs-lookup"><span data-stu-id="b820e-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="b820e-338">**Monitoraggio** > **Metrica** > **Impostazioni di diagnostica** > **Diagnostica**</span><span class="sxs-lookup"><span data-stu-id="b820e-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Collegamento per la diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="b820e-340">In hello **diagnostica** pannello, fare clic su **su**, selezionare l'account di archiviazione hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="b820e-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Pannello Diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="b820e-342">Operazione può richiedere ora tooone per hello metriche toobe visibile in hello **monitoraggio** pannello poiché l'aggregazione di metriche si verifica ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b820e-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="b820e-343">Configurare un avviso relativo alle metriche</span><span class="sxs-lookup"><span data-stu-id="b820e-343">Set up an alert on metrics</span></span>
<span data-ttu-id="b820e-344">Fare clic su hello **metriche Data Factory** riquadro:</span><span class="sxs-lookup"><span data-stu-id="b820e-344">Click hello **Data Factory metrics** tile:</span></span>

![Riquadro Metriche data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="b820e-346">In hello **metrica** pannello, fare clic su **+ Aggiungi avviso** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="b820e-347">![Pannello Metriche data factory > Aggiungi avviso](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="b820e-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="b820e-348">In hello **aggiungere una regola di avviso** pagina hello alla procedura seguente e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b820e-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="b820e-349">Immettere un nome per l'avviso hello (esempio: "non riuscito-avviso").</span><span class="sxs-lookup"><span data-stu-id="b820e-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="b820e-350">Immettere una descrizione dell'avviso hello (esempio: "Invia un messaggio di posta elettronica quando si verifica un errore").</span><span class="sxs-lookup"><span data-stu-id="b820e-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="b820e-351">Selezionare una metrica tra "Esecuzioni non riuscite" ed "Esecuzioni riuscite".</span><span class="sxs-lookup"><span data-stu-id="b820e-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="b820e-352">Specificare una condizione e un valore di soglia.</span><span class="sxs-lookup"><span data-stu-id="b820e-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="b820e-353">Specificare hello periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b820e-353">Specify hello period of time.</span></span>
* <span data-ttu-id="b820e-354">Specificare se è necessario inviare un messaggio di posta elettronica tooowners, contributors e readers.</span><span class="sxs-lookup"><span data-stu-id="b820e-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Pannello Metriche data factory > Aggiungi regola di avviso](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="b820e-356">Dopo che la regola di avviso hello viene aggiunto correttamente, pannello hello chiude e viene visualizzato di nuovo avviso hello in hello **metrica** blade.</span><span class="sxs-lookup"><span data-stu-id="b820e-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Pannello Metriche data factory > Nuovo avviso aggiunto](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="b820e-358">Verrà inoltre visualizzato il numero di hello di avvisi in hello **regole di avviso** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b820e-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="b820e-359">Fare clic su hello **regole di avviso** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b820e-359">Click hello **Alert rules** tile.</span></span>

![Pannello Metriche data factory - Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="b820e-361">In hello **avvisi regole** pannello viene visualizzato di tutti gli avvisi esistenti.</span><span class="sxs-lookup"><span data-stu-id="b820e-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="b820e-362">tooadd un avviso, fare clic su **Aggiungi avviso** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Pannello Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="b820e-364">Notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="b820e-364">Alert notifications</span></span>
<span data-ttu-id="b820e-365">Dopo che la regola di avviso hello corrisponde a hello condizione, viene visualizzato un messaggio di posta elettronica che segnala hello avviso viene attivato.</span><span class="sxs-lookup"><span data-stu-id="b820e-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="b820e-366">Dopo che viene risolto hello e condizione di avviso hello non corrisponde più, viene visualizzato un messaggio di posta elettronica che segnala hello avviso verrà risolto.</span><span class="sxs-lookup"><span data-stu-id="b820e-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="b820e-367">Questo comportamento è diverso da quello degli eventi in cui viene inviata una notifica per ogni errore qualificato da una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="b820e-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="b820e-368">Distribuire avvisi tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="b820e-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="b820e-369">È possibile distribuire gli avvisi per le metriche hello stessa modalità utilizzata per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="b820e-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="b820e-370">**Definizione di avviso**</span><span class="sxs-lookup"><span data-stu-id="b820e-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="b820e-371">Sostituire *subscriptionId*, *resourceGroupName*, e *dataFactoryName* nell'esempio hello con valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="b820e-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="b820e-372">*metricName* supporta attualmente due valori:</span><span class="sxs-lookup"><span data-stu-id="b820e-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="b820e-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="b820e-373">FailedRuns</span></span>
* <span data-ttu-id="b820e-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="b820e-374">SuccessfulRuns</span></span>

<span data-ttu-id="b820e-375">**Distribuire avviso hello**</span><span class="sxs-lookup"><span data-stu-id="b820e-375">**Deploy hello alert**</span></span>

<span data-ttu-id="b820e-376">avviso di hello toodeploy, utilizzare cmdlet di Azure PowerShell hello **New AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b820e-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="b820e-377">Al termine della distribuzione, verrà visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="b820e-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="b820e-378">È inoltre possibile utilizzare hello **Aggiungi AlertRule** toodeploy cmdlet una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="b820e-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="b820e-379">Vedere hello [Aggiungi AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) argomento per informazioni dettagliate ed esempi.</span><span class="sxs-lookup"><span data-stu-id="b820e-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="b820e-380">Spostare un gruppo di risorse diverso tooa data factory o una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="b820e-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="b820e-381">È possibile spostare un gruppo di risorse diverso dati tooa factory o una sottoscrizione diversa utilizzando hello **spostare** barra pulsante hello home page della data factory dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b820e-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Spostare una data factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="b820e-383">È inoltre possibile spostare le risorse correlate (ad esempio gli avvisi che sono associati a data factory di hello), insieme a data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b820e-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Finestra di dialogo Sposta risorse](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
