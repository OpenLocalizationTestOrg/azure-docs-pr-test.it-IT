---
title: Monitorare e gestire le pipeline con il portale di Azure e PowerShell | Microsoft Docs
description: Informazioni su come usare il portale di Azure e Azure PowerShell per monitorare e gestire le pipeline e le data factory di Azure create.
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
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="4ed9b-103">Monitorare e gestire le pipeline di Azure Data Factory con il portale di Azure e PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ed9b-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ed9b-104">Con il portale di Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ed9b-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="4ed9b-105">Con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="4ed9b-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="4ed9b-106">L'applicazione di monitoraggio e gestione offre un supporto migliore per il monitoraggio e la gestione delle pipeline di dati, nonché per la risoluzione di eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="4ed9b-107">Per dettagli sull'uso dell'applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="4ed9b-108">Questo articolo descrive come monitorare e gestire le pipeline ed eseguirne il debug tramite il Portale di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="4ed9b-109">L'articolo contiene anche informazioni su come creare avvisi e ricevere notifiche sugli errori.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="4ed9b-110">Informazioni sulle pipeline e sugli stati delle attività</span><span class="sxs-lookup"><span data-stu-id="4ed9b-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="4ed9b-111">L'uso del portale di Azure consente di:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="4ed9b-112">Visualizzare la data factory come diagramma.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="4ed9b-113">Visualizzare le attività all'interno di una pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="4ed9b-114">Visualizzare set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-114">View input and output datasets.</span></span>

<span data-ttu-id="4ed9b-115">Questa sezione illustra anche come avviene la transizione di una sezione di un set di dati da uno stato a un altro.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="4ed9b-116">Passare alla data factory</span><span class="sxs-lookup"><span data-stu-id="4ed9b-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="4ed9b-117">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4ed9b-118">Fare clic su **Data factory** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="4ed9b-119">Se non è visibile, fare clic su **Altri servizi >**, quindi selezionare **Data factory** nella categoria **Intelligence e analisi**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Esplora tutto > Data factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="4ed9b-121">Nel pannello **Data factory** selezionare la data factory a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Selezionare la data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="4ed9b-123">Verrà visualizzata la home page della data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-123">You should see the home page for the data factory.</span></span>

   ![Pannello Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="4ed9b-125">Vista diagramma della data factory</span><span class="sxs-lookup"><span data-stu-id="4ed9b-125">Diagram view of your data factory</span></span>
<span data-ttu-id="4ed9b-126">La vista **Diagramma** di una data factory offre un'unica console da cui monitorare e gestire la data factory e i relativi asset.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="4ed9b-127">Per visualizzare la vista **Diagramma** della data factory, fare clic su **Diagramma** nella home page della data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Vista diagramma](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="4ed9b-129">È possibile eseguire lo zoom avanti, lo zoom indietro, lo zoom 100%, adattare alla finestra, bloccare il layout del diagramma e posizionare automaticamente pipeline e set di dati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="4ed9b-130">È anche possibile visualizzare le informazioni sulla derivazione dei dati, vale a dire gli elementi upstream e downstream degli elementi selezionati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="4ed9b-131">Attività all'interno di una pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="4ed9b-132">Fare clic con il pulsante destro del mouse sulla pipeline e scegliere **Apri pipeline** per visualizzare tutte le attività della pipeline, oltre ai set di dati di input e output relativi a tali attività.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="4ed9b-133">Questa funzionalità è utile quando la pipeline include più di una attività e si vuole conoscere la derivazione operativa di una singola pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Menu Apri pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="4ed9b-135">L'esempio seguente mostra un'attività di copia nella pipeline con un input e un output.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Attività all'interno di una pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="4ed9b-137">Per tornare alla home page della data factory, fare clic sul collegamento **Data factory** nella barra di navigazione nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Ritorno a Data factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="4ed9b-139">Visualizzare lo stato di ogni attività all'interno di una pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="4ed9b-140">Per visualizzare lo stato corrente di un'attività, visualizzare lo stato di uno dei set di dati generati dall'attività.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="4ed9b-141">Facendo doppio clic su **OutputBlobTable** nella vista **Diagramma**, è possibile visualizzare tutte le sezioni generate da esecuzioni diverse dell'attività all'interno di una pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="4ed9b-142">Si noti che l'attività di copia è stata eseguita correttamente nelle ultime otto ore e ha generato sezioni con lo stato **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![Stato della pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="4ed9b-144">Le sezioni dei set di dati nella data factory possono avere uno degli stati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="4ed9b-145">Stato</span><span class="sxs-lookup"><span data-stu-id="4ed9b-145">State</span></span></th><th align="left"><span data-ttu-id="4ed9b-146">Sottostato</span><span class="sxs-lookup"><span data-stu-id="4ed9b-146">Substate</span></span></th><th align="left"><span data-ttu-id="4ed9b-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ed9b-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="4ed9b-148">Waiting</span><span class="sxs-lookup"><span data-stu-id="4ed9b-148">Waiting</span></span></td><td><span data-ttu-id="4ed9b-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="4ed9b-149">ScheduleTime</span></span></td><td><span data-ttu-id="4ed9b-150">Non è il momento di eseguire la sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="4ed9b-151">DatasetDependencies</span></span></td><td><span data-ttu-id="4ed9b-152">Le dipendenze upstream non sono pronte.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="4ed9b-153">ComputeResources</span></span></td><td><span data-ttu-id="4ed9b-154">Le risorse di calcolo non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="4ed9b-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="4ed9b-156">Tutte le istanze di attività sono occupate nell’esecuzione di altre sezioni.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="4ed9b-157">ActivityResume</span></span></td><td><span data-ttu-id="4ed9b-158">L'attività è sospesa e non può eseguire le sezioni fino a quando non viene ripresa.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-159">Retry</span><span class="sxs-lookup"><span data-stu-id="4ed9b-159">Retry</span></span></td><td><span data-ttu-id="4ed9b-160">L'esecuzione dell'attività viene ritentata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-161">Convalida</span><span class="sxs-lookup"><span data-stu-id="4ed9b-161">Validation</span></span></td><td><span data-ttu-id="4ed9b-162">La convalida non è ancora stata avviata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="4ed9b-163">ValidationRetry</span></span></td><td><span data-ttu-id="4ed9b-164">La convalida è in attesa di essere ripetuta.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="4ed9b-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="4ed9b-165">InProgress</span></span></td><td><span data-ttu-id="4ed9b-166">Convalida in corso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-166">Validating</span></span></td><td><span data-ttu-id="4ed9b-167">La convalida è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="4ed9b-168">La sezione è in corso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="4ed9b-169">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="4ed9b-169">Failed</span></span></td><td><span data-ttu-id="4ed9b-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="4ed9b-170">TimedOut</span></span></td><td><span data-ttu-id="4ed9b-171">L'esecuzione dell'attività ha richiesto più tempo di quello consentito dall'attività.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="4ed9b-172">Canceled</span></span></td><td><span data-ttu-id="4ed9b-173">La sezione è stata annullata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-174">Convalida</span><span class="sxs-lookup"><span data-stu-id="4ed9b-174">Validation</span></span></td><td><span data-ttu-id="4ed9b-175">Convalida non riuscita.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="4ed9b-176">Non è stato possibile generare e/o convalidare la sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="4ed9b-177">Ready</span><span class="sxs-lookup"><span data-stu-id="4ed9b-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="4ed9b-178">La sezione è pronta per essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="4ed9b-179">Skipped</span></span></td><td><span data-ttu-id="4ed9b-180">None</span><span class="sxs-lookup"><span data-stu-id="4ed9b-180">None</span></span></td><td><span data-ttu-id="4ed9b-181">La sezione non viene elaborata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4ed9b-182">None</span><span class="sxs-lookup"><span data-stu-id="4ed9b-182">None</span></span></td><td>-</td><td><span data-ttu-id="4ed9b-183">Esisteva una sezione con uno stato differente, ma è stata reimpostata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="4ed9b-184">Per visualizzare i dettagli di una sezione, fare clic sulla voce di una sezione nel pannello **Sezioni aggiornate di recente**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Dettagli della sezione](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="4ed9b-186">Se la sezione è stata eseguita più volte, vengono visualizzate più righe nell'elenco **Esecuzioni attività** .</span><span class="sxs-lookup"><span data-stu-id="4ed9b-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="4ed9b-187">Per visualizzare i dettagli di un'esecuzione attività, fare clic sulla voce di un'esecuzione nell'elenco **Esecuzioni attività** .</span><span class="sxs-lookup"><span data-stu-id="4ed9b-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="4ed9b-188">L'elenco presenta tutti i file di log insieme a eventuali messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="4ed9b-189">Questa funzionalità è utile per visualizzare i log ed eseguirne il debug senza dover uscire dalla data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Dettagli esecuzione attività](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="4ed9b-191">Se lo stato della sezione non è **Pronto**, sarà possibile visualizzare le sezioni upstream che non sono pronte e bloccano l'esecuzione della sezione corrente nell'elenco **Sezioni upstream non pronte**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="4ed9b-192">Questa funzionalità è utile quando lo stato della sezione è **In attesa** e si vogliono conoscere le dipendenze upstream di cui la sezione è in attesa.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Sezioni upstream non pronte](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="4ed9b-194">Diagramma di stato del set di dati</span><span class="sxs-lookup"><span data-stu-id="4ed9b-194">Dataset state diagram</span></span>
<span data-ttu-id="4ed9b-195">Quando la data factory è stata distribuita e le pipeline hanno un periodo attivo valido, le sezioni del set di dati passano da uno stato a un altro.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="4ed9b-196">Attualmente lo stato delle sezioni segue questo diagramma di stato:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-196">Currently, the slice status follows the following state diagram:</span></span>

![Diagramma di stato](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="4ed9b-198">Il flusso di transizione di stato del set dati nella data factory è il seguente: In attesa -> In corso/In corso (Convalida) -> Pronto/Non riuscito.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="4ed9b-199">La sezione viene avviata nello stato **In attesa** e prima dell'esecuzione è necessario che vengano soddisfatte le precondizioni.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="4ed9b-200">In seguito inizia l'esecuzione dell'attività e la sezione passa allo stato **In corso**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="4ed9b-201">L'esecuzione dell'attività può avere esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="4ed9b-202">Lo stato della sezione sarà **Pronto** o **Non riuscito** in base al risultato dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="4ed9b-203">È possibile reimpostare la sezione in modo che dallo stato **Pronto** o **Non riuscito** torni allo stato **In attesa**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="4ed9b-204">È anche possibile impostare lo stato della sezione su **Ignora**per impedire l'esecuzione dell'attività e l'elaborazione della sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="4ed9b-205">Sospendere e riprendere le pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-205">Pause and resume pipelines</span></span>
<span data-ttu-id="4ed9b-206">È possibile gestire le pipeline usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="4ed9b-207">Ad esempio, è possibile sospendere e riprendere le pipeline eseguendo i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4ed9b-208">La vista diagramma non supporta la sospensione e la ripresa di pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="4ed9b-209">Se si vuole usare un'interfaccia utente, usare l'applicazione di gestione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="4ed9b-210">Per dettagli sull'uso dell'applicazione, vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="4ed9b-211">È possibile sospendere le pipeline usando il cmdlet di PowerShell **Suspend-AzureRmDataFactoryPipeline**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="4ed9b-212">Questo cmdlet è utile quando non si desidera eseguire le pipeline finché non viene risolto un problema.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="4ed9b-213">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="4ed9b-214">Dopo aver risolto il problema della pipeline, è possibile riprendere l'esecuzione della pipeline sospesa tramite il comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="4ed9b-215">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="4ed9b-216">Eseguire il debug delle pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-216">Debug pipelines</span></span>
<span data-ttu-id="4ed9b-217">Azure Data Factory offre funzionalità avanzate per il debug e la risoluzione dei problemi relativi alle pipeline tramite il portale di Azure e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="4ed9b-218">[!NOTA} È molto più semplice risolvere gli errori tramite l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="4ed9b-219">Per dettagli sull'uso dell'applicazione, vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="4ed9b-220">Trovare gli errori in una pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-220">Find errors in a pipeline</span></span>
<span data-ttu-id="4ed9b-221">Se l'esecuzione di un'attività in una pipeline non riesce, il set di dati generato dalla pipeline è in uno stato di errore.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="4ed9b-222">È possibile eseguire il debug e risolvere i problemi relativi agli errori in Azure Data Factory usando i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="4ed9b-223">Usare il portale di Azure per eseguire il debug di un errore</span><span class="sxs-lookup"><span data-stu-id="4ed9b-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="4ed9b-224">Nel pannello **Tabella** fare clic sulla sezione con errori con **Stato** impostato su **Non riuscito**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Pannello Tabella con sezione con errori](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="4ed9b-226">Nel pannello **Sezione dati** fare clic sull'esecuzione dell'attività non riuscita.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Sezione dati con un errore](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="4ed9b-228">Nel pannello **Dettagli esecuzione attività** è possibile scaricare i file associati all'elaborazione di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="4ed9b-229">Fare clic su **Scarica** in corrispondenza di Stato/stderr per scaricare il file di log degli errori che contiene i dettagli dell'errore stesso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Pannello Dettagli esecuzione attività con errore](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="4ed9b-231">Usare PowerShell per eseguire il debug di un errore</span><span class="sxs-lookup"><span data-stu-id="4ed9b-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="4ed9b-232">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="4ed9b-233">Eseguire il comando **Get-AzureRmDataFactorySlice** per vedere le sezioni e i relativi stati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="4ed9b-234">Verrà visualizzata una sezione con lo stato **Non riuscito**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="4ed9b-235">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="4ed9b-236">Sostituire **StartDateTime** con l'ora di inizio della pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="4ed9b-237">Eseguire ora il cmdlet **Get-AzureRmDataFactoryRun** per ottenere i dettagli sull'esecuzione dell'attività per la sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="4ed9b-238">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="4ed9b-239">Il valore di StartDateTime è l'orario di inizio per la sezione con errori/problemi di cui si è preso nota nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="4ed9b-240">La data e ora dovrebbe essere racchiusa tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="4ed9b-241">Si otterrà l'output con informazioni dettagliate sull'errore e sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-241">You should see output with details about the error that is similar to the following:</span></span>

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
5. <span data-ttu-id="4ed9b-242">È possibile eseguire il cmdlet **Save-AzureRmDataFactoryLog** con il valore ID visualizzato nell'output e scaricare i file di log usando l'opzione **-DownloadLogsoption** del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="4ed9b-243">Eseguire nuovamente le operazioni non riuscite in una pipeline</span><span class="sxs-lookup"><span data-stu-id="4ed9b-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ed9b-244">È più semplice risolvere gli errori e ripetere l'esecuzione di sezioni non riuscite tramite l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="4ed9b-245">Per dettagli sull'uso dell'applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="4ed9b-246">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ed9b-246">Use the Azure portal</span></span>
<span data-ttu-id="4ed9b-247">Dopo aver risolto i problemi relativi agli errori in una pipeline e averne eseguito il debug, è possibile eseguire nuovamente le operazioni non riuscite passando alla sezione degli errori e facendo clic sul pulsante **Esegui** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="4ed9b-249">Se non è possibile eseguire la convalida della sezione a causa di un errore relativo ai criteri, ad esempio se i dati non sono disponibili, è possibile correggere l'errore ed eseguire nuovamente la convalida facendo clic sul pulsante **Convalida** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Correggere gli errori e convalidare](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="4ed9b-251">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ed9b-251">Use Azure PowerShell</span></span>
<span data-ttu-id="4ed9b-252">È possibile eseguire nuovamente le operazioni non riuscite usando il cmdlet **Set-AzureRmDataFactorySliceStatus**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="4ed9b-253">Per informazioni sulla sintassi e altri dettagli sul cmdlet, vedere l'argomento [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="4ed9b-254">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-254">**Example:**</span></span>

<span data-ttu-id="4ed9b-255">L'esempio seguente mostra come impostare lo stato di tutte le sezioni per la tabella "DAWikiAggregatedData" su "In attesa" nella data factory "WikiADF" di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="4ed9b-256">"UpdateType" è impostato su "UpstreamInPipeline". Ciò significa che lo stato di ogni sezione della tabella e di tutte le tabelle dipendenti, ovvero upstream, viene impostato su "In attesa".</span><span class="sxs-lookup"><span data-stu-id="4ed9b-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="4ed9b-257">Un altro possibile valore per questo parametro è "Individuale".</span><span class="sxs-lookup"><span data-stu-id="4ed9b-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="4ed9b-258">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="4ed9b-258">Create alerts</span></span>
<span data-ttu-id="4ed9b-259">Azure registra eventi utente quando una risorsa di Azure (ad esempio, una data factory) viene creata, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="4ed9b-260">È possibile creare avvisi per questi eventi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-260">You can create alerts on these events.</span></span> <span data-ttu-id="4ed9b-261">Azure Data Factory consente di acquisire diverse metriche e di creare avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="4ed9b-262">È consigliabile usare gli eventi per il monitoraggio in tempo reale e le metriche per motivi cronologici.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="4ed9b-263">Avvisi relativi agli eventi</span><span class="sxs-lookup"><span data-stu-id="4ed9b-263">Alerts on events</span></span>
<span data-ttu-id="4ed9b-264">Gli eventi di Azure forniscono utili informazioni su quanto accade alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="4ed9b-265">Quando si usa Azure Data Factory, vengono generati eventi quando:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="4ed9b-266">Una data factory viene creata, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="4ed9b-267">L'elaborazione dati (esecuzione) viene avviata o completata.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="4ed9b-268">Un cluster HDInsight su richiesta viene creato o rimosso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="4ed9b-269">È possibile creare avvisi per questi eventi utente e configurarli per l'invio di notifiche tramite posta elettronica all'amministratore e ai coamministratori della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="4ed9b-270">Inoltre, è possibile specificare altri indirizzi di posta elettronica di utenti che devono ricevere notifiche tramite posta elettronica quando vengono soddisfatte le condizioni.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="4ed9b-271">Questa funzionalità è molto utile quando si desidera ricevere notifiche sugli errori senza monitorare continuamente la data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="4ed9b-272">Attualmente il portale non visualizza gli avvisi relativi agli eventi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="4ed9b-273">Usare l'[app di monitoraggio e gestione](data-factory-monitor-manage-app.md) per visualizzare tutti gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="4ed9b-274">Specificare una definizione di avviso</span><span class="sxs-lookup"><span data-stu-id="4ed9b-274">Specify an alert definition</span></span>
<span data-ttu-id="4ed9b-275">Per specificare una definizione di avviso, creare un file JSON che descrive le operazioni per cui si vuole essere avvisati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="4ed9b-276">Nell'esempio seguente l'avviso invia una notifica tramite posta elettronica per l'operazione RunFinished.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="4ed9b-277">In particolare, viene inviata una notifica tramite posta elettronica quando un'esecuzione nella data factory viene completata, ma l'esito è negativo (stato = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
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

<span data-ttu-id="4ed9b-278">Se non si vuole ricevere un avviso in caso di errore specifico, è possibile rimuovere **subStatus** dalla definizione JSON.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="4ed9b-279">Questo esempio configura l'avviso per tutte le data factory nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="4ed9b-280">Se si desidera che venga impostato l'avviso per una data factory specifica, è possibile indicare la data factory **resourceUri** nel blocco **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="4ed9b-281">La tabella seguente contiene l'elenco delle operazioni e degli stati e stati secondari disponibili.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="4ed9b-282">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="4ed9b-282">Operation name</span></span> | <span data-ttu-id="4ed9b-283">Stato</span><span class="sxs-lookup"><span data-stu-id="4ed9b-283">Status</span></span> | <span data-ttu-id="4ed9b-284">Stato secondario</span><span class="sxs-lookup"><span data-stu-id="4ed9b-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ed9b-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="4ed9b-285">RunStarted</span></span> |<span data-ttu-id="4ed9b-286">Started</span><span class="sxs-lookup"><span data-stu-id="4ed9b-286">Started</span></span> |<span data-ttu-id="4ed9b-287">Starting</span><span class="sxs-lookup"><span data-stu-id="4ed9b-287">Starting</span></span> |
| <span data-ttu-id="4ed9b-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="4ed9b-288">RunFinished</span></span> |<span data-ttu-id="4ed9b-289">Failed/Succeeded</span><span class="sxs-lookup"><span data-stu-id="4ed9b-289">Failed / Succeeded</span></span> |<span data-ttu-id="4ed9b-290">Allocazione risorse non riuscita</span><span class="sxs-lookup"><span data-stu-id="4ed9b-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="4ed9b-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="4ed9b-291">Succeeded</span></span><br/><br/><span data-ttu-id="4ed9b-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="4ed9b-292">FailedExecution</span></span><br/><br/><span data-ttu-id="4ed9b-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="4ed9b-293">TimedOut</span></span><br/><br/><span data-ttu-id="4ed9b-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="4ed9b-294"><Canceled</span></span><br/><br/><span data-ttu-id="4ed9b-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="4ed9b-295">FailedValidation</span></span><br/><br/><span data-ttu-id="4ed9b-296">Abbandonato</span><span class="sxs-lookup"><span data-stu-id="4ed9b-296">Abandoned</span></span> |
| <span data-ttu-id="4ed9b-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="4ed9b-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="4ed9b-298">Started</span><span class="sxs-lookup"><span data-stu-id="4ed9b-298">Started</span></span> | |
| <span data-ttu-id="4ed9b-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="4ed9b-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="4ed9b-300">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="4ed9b-300">Succeeded</span></span> | |
| <span data-ttu-id="4ed9b-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="4ed9b-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="4ed9b-302">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="4ed9b-302">Succeeded</span></span> | |

<span data-ttu-id="4ed9b-303">Per informazioni dettagliate sugli elementi JSON usati nell'esempio, vedere [Crea regola avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="4ed9b-304">Distribuire l'avviso</span><span class="sxs-lookup"><span data-stu-id="4ed9b-304">Deploy the alert</span></span>
<span data-ttu-id="4ed9b-305">Per distribuire l'avviso, usare il cmdlet **New-AzureRmResourceGroupDeployment**di Azure PowerShell, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="4ed9b-306">Al termine della distribuzione del gruppo di risorse, verranno visualizzati i messaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
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
> <span data-ttu-id="4ed9b-307">È possibile usare l'API REST di [Crea regola avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx) per creare una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="4ed9b-308">Il payload JSON è simile all'esempio JSON riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="4ed9b-309">Recuperare l'elenco delle distribuzioni di gruppi di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4ed9b-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="4ed9b-310">Per recuperare l'elenco delle distribuzioni di gruppi di risorse di Azure distribuite, usare il cmdlet **Get-AzureRmResourceGroupDeployment**, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="4ed9b-311">Risolvere i problemi relativi a eventi utente</span><span class="sxs-lookup"><span data-stu-id="4ed9b-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="4ed9b-312">È possibile visualizzare tutti gli eventi generati dopo aver selezionato il riquadro **Metriche e operazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Riquadro Metriche e operazioni](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="4ed9b-314">Fare clic sul riquadro **Eventi** per visualizzare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-314">Click the **Events** tile to see the events.</span></span>

    ![Riquadro Eventi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="4ed9b-316">Nel pannello **Eventi** è possibile visualizzare i dettagli sugli eventi, filtrare gli eventi e così via.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Pannello Eventi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="4ed9b-318">Fare clic su un'**operazione** nell'elenco delle operazioni che genera un errore.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Selezionare un'operazione](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="4ed9b-320">Fare clic su un evento di **errore** per visualizzare i dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-320">Click an **Error** event to see details about the error.</span></span>

    ![Evento di errore](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="4ed9b-322">Per informazioni sui cmdlet di PowerShell che è possibile usare per aggiungere, ottenere o rimuovere avvisi, vedere l'articolo relativo ai [cmdlet di Azure Insights](https://msdn.microsoft.com/library/mt282452.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="4ed9b-323">Ecco alcuni esempi di uso del cmdlet **Get-AlertRule** :</span><span class="sxs-lookup"><span data-stu-id="4ed9b-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of the data slices for the Azure Data Factory has failed processing.
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

<span data-ttu-id="4ed9b-324">Eseguire i seguenti comandi get-help per visualizzare informazioni dettagliate ed esempi per il cmdlet Get-AlertRule.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="4ed9b-325">Se gli eventi di generazione avvisi vengono visualizzati nel pannello del portale, ma non si ricevono le notifiche di posta elettronica, controllare se l'indirizzo di posta elettronica specificato è impostato per la ricezione di messaggi da mittenti esterni.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="4ed9b-326">I messaggi di avviso potrebbero essere stati bloccati dalle impostazioni di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="4ed9b-327">Avvisi relativi alle metriche</span><span class="sxs-lookup"><span data-stu-id="4ed9b-327">Alerts on metrics</span></span>
<span data-ttu-id="4ed9b-328">Azure Data Factory consente di acquisire diverse metriche e di creare avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="4ed9b-329">È possibile monitorare e creare avvisi per le metriche seguenti relative alle sezioni della data factory:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="4ed9b-330">**Esecuzioni non riuscite**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-330">**Failed Runs**</span></span>
* <span data-ttu-id="4ed9b-331">**Esecuzioni riuscite**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-331">**Successful Runs**</span></span>

<span data-ttu-id="4ed9b-332">Queste metriche sono utili e consentono di ottenere una panoramica di tutte le esecuzioni riuscite e non riuscite nella data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="4ed9b-333">Le metriche vengono emesse ogni volta che viene eseguita una sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="4ed9b-334">All'inizio di ogni ora, queste metriche vengono aggregate e inserite nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="4ed9b-335">Per abilitare le metriche, configurare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="4ed9b-336">Abilitazione di metriche</span><span class="sxs-lookup"><span data-stu-id="4ed9b-336">Enable metrics</span></span>
<span data-ttu-id="4ed9b-337">Per abilitare le metriche, fare clic su quanto segue nel pannello **Data factory**:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="4ed9b-338">**Monitoraggio** > **Metrica** > **Impostazioni di diagnostica** > **Diagnostica**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Collegamento per la diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="4ed9b-340">Nel pannello **Diagnostica** fare clic su **Sì**, selezionare l'account di archiviazione e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Pannello Diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="4ed9b-342">Potrebbe trascorrere anche un'ora prima che le metriche siano visibili nel pannello **Monitoraggio**, perché l'aggregazione delle metriche viene eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="4ed9b-343">Configurare un avviso relativo alle metriche</span><span class="sxs-lookup"><span data-stu-id="4ed9b-343">Set up an alert on metrics</span></span>
<span data-ttu-id="4ed9b-344">Fare clic sul riquadro **Metriche data factory**:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-344">Click the **Data Factory metrics** tile:</span></span>

![Riquadro Metriche data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="4ed9b-346">Nel pannello **Metrica** fare clic su **+ Aggiungi avviso** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="4ed9b-347">![Pannello Metriche data factory > Aggiungi avviso](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="4ed9b-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="4ed9b-348">Nella pagina **Aggiungi una regola di avviso**, attenersi alla procedura seguente e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="4ed9b-349">Immettere un nome per l'avviso, ad esempio "Avviso non riuscito".</span><span class="sxs-lookup"><span data-stu-id="4ed9b-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="4ed9b-350">Immettere una descrizione dell'avviso, ad esempio "Invia un messaggio di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="4ed9b-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="4ed9b-351">Selezionare una metrica tra "Esecuzioni non riuscite" ed "Esecuzioni riuscite".</span><span class="sxs-lookup"><span data-stu-id="4ed9b-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="4ed9b-352">Specificare una condizione e un valore di soglia.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="4ed9b-353">Specificare il periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-353">Specify the period of time.</span></span>
* <span data-ttu-id="4ed9b-354">Specificare se inviare un'e-mail a proprietari, collaboratori e lettori.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Pannello Metriche data factory > Aggiungi regola di avviso](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="4ed9b-356">Dopo aver aggiunto la regola di avviso, il pannello si chiude e il nuovo avviso viene visualizzato nel pannello **Metrica**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Pannello Metriche data factory > Nuovo avviso aggiunto](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="4ed9b-358">Nel riquadro **Regole di avviso** si dovrebbe vedere anche il numero degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="4ed9b-359">Fare clic sul riquadro **Regole di avviso**.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-359">Click the **Alert rules** tile.</span></span>

![Pannello Metriche data factory - Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="4ed9b-361">Nel pannello **Regole di avviso** vengono visualizzati gli avvisi esistenti.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="4ed9b-362">Per aggiungere un avviso, fare clic su **Aggiungi avviso** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Pannello Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="4ed9b-364">Notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="4ed9b-364">Alert notifications</span></span>
<span data-ttu-id="4ed9b-365">Quando la regola di avviso corrisponde alla condizione, si riceve un messaggio di posta elettronica che conferma l'attivazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="4ed9b-366">Quando il problema viene risolto e la condizione di avviso non corrisponde più, si riceve un messaggio di posta elettronica che conferma la risoluzione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="4ed9b-367">Questo comportamento è diverso da quello degli eventi in cui viene inviata una notifica per ogni errore qualificato da una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="4ed9b-368">Distribuire avvisi tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ed9b-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="4ed9b-369">È possibile distribuire avvisi per le metriche esattamente come avviene per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="4ed9b-370">**Definizione di avviso**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-370">**Alert definition**</span></span>

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

<span data-ttu-id="4ed9b-371">Sostituire *subscriptionId*, *resourceGroupName* e *dataFactoryName* nell'esempio precedente con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="4ed9b-372">*metricName* supporta attualmente due valori:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="4ed9b-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="4ed9b-373">FailedRuns</span></span>
* <span data-ttu-id="4ed9b-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="4ed9b-374">SuccessfulRuns</span></span>

<span data-ttu-id="4ed9b-375">**Distribuire l'avviso**</span><span class="sxs-lookup"><span data-stu-id="4ed9b-375">**Deploy the alert**</span></span>

<span data-ttu-id="4ed9b-376">Per distribuire l'avviso, usare il cmdlet **New-AzureRmResourceGroupDeployment**di Azure PowerShell, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="4ed9b-377">Al termine della distribuzione, verrà visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed9b-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="4ed9b-378">È anche possibile usare il cmdlet **Add-AlertRule** per distribuire una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="4ed9b-379">Per informazioni dettagliate ed esempi, vedere l'argomento [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ed9b-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="4ed9b-380">Spostare una data factory in un gruppo di risorse diverso o una sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="4ed9b-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="4ed9b-381">È possibile spostare una data factory in un gruppo di risorse diverso o in una sottoscrizione diversa usando il pulsante **Sposta** della barra dei comandi nella home page della data factory.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Spostare una data factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="4ed9b-383">È anche possibile spostare le risorse correlate insieme alla data factory, ad esempio gli avvisi ad essa associati.</span><span class="sxs-lookup"><span data-stu-id="4ed9b-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Finestra di dialogo Sposta risorse](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
