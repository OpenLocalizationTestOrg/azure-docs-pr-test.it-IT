---
title: 'Controllare lo stato, configurare la registrazione e ottenere avvisi: App per la logica di Azure | Microsoft Docs'
description: Monitorare lo stato e le prestazioni per le app per la logica, registrare i dati di diagnostica e configurare gli avvisi
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="c0994-103">Monitorare lo stato, configurare la registrazione diagnostica e attivare gli avvisi per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="c0994-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="c0994-104">Dopo avere [creato ed eseguito un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md), è possibile controllarne la cronologia delle esecuzioni, la cronologia dei trigger, lo stato e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c0994-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="c0994-105">Per il monitoraggio degli eventi in tempo reale e il debug avanzato, configurare la [registrazione diagnostica](#azure-diagnostics) per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="c0994-106">In questo modo è possibile [trovare e visualizzare gli eventi](#find-events), ad esempio eventi di attivazione, eventi di esecuzione ed eventi di azione.</span><span class="sxs-lookup"><span data-stu-id="c0994-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="c0994-107">È anche possibile usare questi [dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0994-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="c0994-108">Per ottenere notifiche sugli errori o su altri possibili problemi, configurare gli [avvisi](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="c0994-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="c0994-109">È ad esempio possibile creare un avviso che rileva "quando più di cinque esecuzioni in un'ora hanno esito negativo".</span><span class="sxs-lookup"><span data-stu-id="c0994-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="c0994-110">È anche possibile configurare il monitoraggio, la verifica e la registrazione a livello di codice usando [impostazioni e proprietà degli eventi di Diagnostica di Azure](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="c0994-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="c0994-111">Visualizzare la cronologia di esecuzioni e trigger per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c0994-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="c0994-112">Per trovare l'app per la logica nel [portale di Azure](https://portal.azure.com) scegliere **Altri servizi** dal menu principale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0994-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="c0994-113">Nella casella di ricerca cercare "app per la logica" e scegliere **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="c0994-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Trovare l'app per la logica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="c0994-115">Il portale di Azure visualizza tutte le app per la logica associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0994-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="c0994-116">Selezionare l'app per la logica, quindi scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="c0994-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="c0994-117">Il portale di Azure visualizza la cronologia delle esecuzioni e la cronologia dei trigger per l'app per la logica,</span><span class="sxs-lookup"><span data-stu-id="c0994-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="c0994-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-118">For example:</span></span>

   ![Cronologia delle esecuzioni e cronologia dei trigger delle app per la logica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="c0994-120">**Cronologia esecuzioni** visualizza tutte le esecuzioni per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="c0994-121">**Cronologia trigger** visualizza tutte le attività dei trigger per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="c0994-122">Per le descrizioni degli stati, vedere [Risolvere i problemi relativi all'app per la logica](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="c0994-123">Se non si trovano i dati previsti, scegliere **Aggiorna** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="c0994-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="c0994-124">Per visualizzare i passaggi da una specifica esecuzione, selezionarla in **Cronologia esecuzioni**.</span><span class="sxs-lookup"><span data-stu-id="c0994-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="c0994-125">La vista di monitoraggio mostra ogni passaggio di tale esecuzione,</span><span class="sxs-lookup"><span data-stu-id="c0994-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="c0994-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-126">For example:</span></span>

   ![Azioni per una specifica esecuzione](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="c0994-128">Per ottenere altri dettagli sull'esecuzione, scegliere **Dettagli esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="c0994-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="c0994-129">Queste informazioni riepilogano i passaggi, lo stato, gli input e gli output per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c0994-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Scegliere "Dettagli esecuzione"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="c0994-131">È ad esempio possibile ottenere l'**ID di correlazione** dell'esecuzione, che potrebbe essere necessario quando si usa l'[API REST per App per la logica](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="c0994-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="c0994-132">Per ottenere informazioni dettagliate su un passaggio specifico, scegliere il passaggio.</span><span class="sxs-lookup"><span data-stu-id="c0994-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="c0994-133">È ora possibile esaminare dettagli come input, output ed eventuali errori verificatisi per tale passaggio,</span><span class="sxs-lookup"><span data-stu-id="c0994-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="c0994-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-134">For example:</span></span>

   ![Dettagli del passaggio](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="c0994-136">Tutti i dettagli ed eventi di runtime vengono crittografati nel servizio App per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="c0994-137">Vengono decrittografati solo quando un utente richiede di visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="c0994-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="c0994-138">È anche possibile controllare l'accesso a questi eventi con il [controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="c0994-139">Per ottenere informazioni dettagliate su un evento di attivazione specifico, tornare al riquadro **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="c0994-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="c0994-140">In **Cronologia trigger** selezionare l'evento di attivazione.</span><span class="sxs-lookup"><span data-stu-id="c0994-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="c0994-141">È ora possibile esaminare dettagli come input e output, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Dettagli dell'output dell'evento di attivazione](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="c0994-143">Attivare la registrazione diagnostica per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c0994-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="c0994-144">Per il debug avanzato con dettagli ed eventi di runtime, è possibile configurare la registrazione diagnostica con [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="c0994-145">Log Analytics è un servizio di [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) che consente di monitorare gli ambienti cloud e locali per garantirne la disponibilità e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c0994-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="c0994-146">Prima di iniziare, è necessario avere un'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="c0994-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="c0994-147">Informazioni su [come creare un'area di lavoro di OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="c0994-148">Nel [portale di Azure](https://portal.azure.com) trovare e selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="c0994-149">Nel menu del pannello dell'app per la logica, in **Monitoraggio** scegliere **Diagnostica** > **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="c0994-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Andare a Monitoraggio, Diagnostica, Impostazioni di diagnostica](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="c0994-151">In **Impostazioni di diagnostica** scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c0994-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Attivare i log di diagnostica](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="c0994-153">Selezionare ora l'area di lavoro di OMS e la categoria di eventi per la registrazione, come indicato:</span><span class="sxs-lookup"><span data-stu-id="c0994-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="c0994-154">Selezionare **Invia a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c0994-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="c0994-155">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="c0994-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="c0994-156">In **Aree di lavoro OMS** selezionare l'area di lavoro di OMS da usare per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c0994-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="c0994-157">In **Log** selezionare la categoria **WorkflowRuntime**.</span><span class="sxs-lookup"><span data-stu-id="c0994-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="c0994-158">Scegliere l'intervallo di metrica.</span><span class="sxs-lookup"><span data-stu-id="c0994-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="c0994-159">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c0994-159">When you're done, choose **Save**.</span></span>

   ![Selezionare l'area di lavoro di OMS e i dati per la registrazione](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="c0994-161">È ora possibile trovare eventi e altri dati per eventi di attivazione, eventi di esecuzione ed eventi di azione.</span><span class="sxs-lookup"><span data-stu-id="c0994-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="c0994-162">Trovare eventi e dati per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c0994-162">Find events and data for your logic app</span></span>

<span data-ttu-id="c0994-163">Per trovare e visualizzare gli eventi nell'app per la logica, ad esempio eventi di attivazione, eventi di esecuzione ed eventi di azione, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="c0994-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="c0994-164">Nel [portale di Azure](https://portal.azure.com) scegliere **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="c0994-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c0994-165">Cercare "Log Analytics", quindi scegliere **Log Analytics**, come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="c0994-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Scegliere "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="c0994-167">In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="c0994-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="c0994-169">In **Gestione** scegliere **Portale di OMS**.</span><span class="sxs-lookup"><span data-stu-id="c0994-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Scegliere "Portale di OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="c0994-171">Nella home page di OMS scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="c0994-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="c0994-173">-oppure-</span><span class="sxs-lookup"><span data-stu-id="c0994-173">-or-</span></span>

   ![Dal menu di OMS scegliere "Ricerca log"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="c0994-175">Nella casella di ricerca specificare un campo che si vuole trovare e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="c0994-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="c0994-176">Quando si inizia a digitare, OMS visualizza le possibili corrispondenze e operazioni che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="c0994-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="c0994-177">Per trovare, ad esempio, i primi 10 eventi che si sono verificati, immettere e selezionare questa query di ricerca: **Category=WorkflowRuntime |top 10**</span><span class="sxs-lookup"><span data-stu-id="c0994-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Immettere la stringa di ricerca](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="c0994-179">Altre informazioni su [come trovare i dati in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="c0994-180">Nella barra a sinistra della pagina dei risultati scegliere l'intervallo di tempo che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="c0994-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="c0994-181">Per affinare la query aggiungendo un filtro, scegliere **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0994-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Scegliere l'intervallo di tempo per i risultati della query](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="c0994-183">In **Aggiungi filtri** immettere il nome del filtro per trovare quello desiderato.</span><span class="sxs-lookup"><span data-stu-id="c0994-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="c0994-184">Selezionare il filtro e scegliere **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0994-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="c0994-185">L'esempio usa la parola "status" per trovare gli eventi non riusciti in **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c0994-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="c0994-186">Qui il filtro per **status_s** è già selezionato.</span><span class="sxs-lookup"><span data-stu-id="c0994-186">Here the filter for **status_s** is already selected.</span></span>

   ![Selezionare il filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="c0994-188">Nella barra a sinistra selezionare il valore del filtro che si vuole usare e scegliere **Applica**.</span><span class="sxs-lookup"><span data-stu-id="c0994-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Selezionare il valore del filtro, scegliere "Applica"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="c0994-190">Tornare ora alla query che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="c0994-190">Now return to the query that you're building.</span></span> <span data-ttu-id="c0994-191">La query viene aggiornata con il filtro e il valore selezionati.</span><span class="sxs-lookup"><span data-stu-id="c0994-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="c0994-192">Vengono ora filtrati anche i risultati precedenti.</span><span class="sxs-lookup"><span data-stu-id="c0994-192">Your previous results are now filtered too.</span></span>

   ![Tornare alla query con i risultati filtrati](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="c0994-194">Per salvare la query per un uso futuro, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c0994-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="c0994-195">Informazioni su [come salvare la query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="c0994-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="c0994-196">Estendere l'uso dei dati di diagnostica con altri servizi</span><span class="sxs-lookup"><span data-stu-id="c0994-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="c0994-197">Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="c0994-198">Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c0994-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="c0994-199">Trasmettere i log di diagnostica di Azure a Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="c0994-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="c0994-200">È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md),</span><span class="sxs-lookup"><span data-stu-id="c0994-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="c0994-201">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0994-201">For example:</span></span>

* [<span data-ttu-id="c0994-202">Trasmettere i dati da Hub eventi ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="c0994-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="c0994-203">Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI</span><span class="sxs-lookup"><span data-stu-id="c0994-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="c0994-204">In base alle opzioni che si vuole configurare, assicurarsi prima di tutto di [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o di [creare un hub eventi di Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="c0994-205">Selezionare quindi le opzioni per la posizione a cui si vogliono inviare i dati di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="c0994-205">Then select the options for where you want to send diagnostic data:</span></span>

![Inviare i dati all'hub di eventi o all'account di archiviazione di Azure](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="c0994-207">I periodi di conservazione si applicano solo quando si sceglie di usare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c0994-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="c0994-208">Configurare gli avvisi per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c0994-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="c0994-209">Per monitorare metriche specifiche o le soglie superate per l'app per la logica, configurare gli [avvisi in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="c0994-210">Informazioni sulle [metriche in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c0994-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="c0994-211">Per configurare gli avvisi senza [Azure Log Analytics](../log-analytics/log-analytics-overview.md), seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="c0994-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="c0994-212">Per azioni e criteri di avviso più avanzati, [configurare anche Log Analytics](#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="c0994-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="c0994-213">Nel menu del pannello dell'app per la logica, in **Monitoraggio** scegliere **Diagnostica** > **Regole di avviso** > **Aggiungi avviso**, come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="c0994-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Aggiungere un avviso per l'app per la logica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="c0994-215">Nel pannello **Aggiungi una regola di avviso** creare l'avviso come indicato:</span><span class="sxs-lookup"><span data-stu-id="c0994-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="c0994-216">In **Risorsa** selezionare l'app per la logica, se non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="c0994-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="c0994-217">Specificare un nome e una descrizione per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c0994-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="c0994-218">Selezionare una **metrica** o un evento di cui si vuole tenere traccia.</span><span class="sxs-lookup"><span data-stu-id="c0994-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="c0994-219">Selezionare una **condizione**, specificare una **soglia** per la metrica e selezionare il **periodo** per il monitoraggio di questa metrica.</span><span class="sxs-lookup"><span data-stu-id="c0994-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="c0994-220">Scegliere se inviare posta per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c0994-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="c0994-221">Specificare eventuali altri indirizzi di posta elettronica a cui inviare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c0994-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="c0994-222">È anche possibile specificare l'URL di un webhook a cui si vuole inviare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c0994-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="c0994-223">Questa regola, ad esempio, invia un avviso quando cinque o più esecuzioni in un'ora hanno esito negativo:</span><span class="sxs-lookup"><span data-stu-id="c0994-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Creare una regola di avviso per la metrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="c0994-225">Per eseguire un'app per la logica da un avviso, è possibile includere il [trigger della richiesta](../connectors/connectors-native-reqres.md) nel flusso di lavoro, che consente di eseguire attività come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0994-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="c0994-226">Pubblicare su Slack</span><span class="sxs-lookup"><span data-stu-id="c0994-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="c0994-227">Inviare un testo</span><span class="sxs-lookup"><span data-stu-id="c0994-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="c0994-228">Aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="c0994-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="c0994-229">Impostazioni e dettagli degli eventi di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="c0994-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="c0994-230">Ogni evento di diagnostica ha dettagli sull'app per la logica e sull'evento stesso, ad esempio lo stato, l'ora di inizio, l'ora di fine e così via.</span><span class="sxs-lookup"><span data-stu-id="c0994-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="c0994-231">Per configurare a livello di codice il monitoraggio, la verifica e la registrazione, è possibile usare questi dettagli con l'[API REST per App per la logica di Azure](https://docs.microsoft.com/rest/api/logic) e l'[API REST per Diagnostica di Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="c0994-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="c0994-232">L'evento `ActionCompleted`, ad esempio, ha le proprietà `clientTrackingId` e `trackedProperties` che è possibile usare per la verifica e il monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="c0994-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="c0994-233">`clientTrackingId`: se non specificata, Azure genera automaticamente questo ID e correla gli eventi in un'esecuzione dell'app per la logica, inclusi eventuali flussi di lavoro annidati chiamati dall'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="c0994-234">È possibile specificare manualmente questo ID da un trigger passando un'intestazione `x-ms-client-tracking-id` con il valore dell'ID personalizzato nella richiesta del trigger.</span><span class="sxs-lookup"><span data-stu-id="c0994-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="c0994-235">È possibile usare un trigger di richiesta, un trigger HTTP o un trigger webhook.</span><span class="sxs-lookup"><span data-stu-id="c0994-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="c0994-236">`trackedProperties`: per tenere traccia degli input o degli output nei dati di diagnostica, è possibile aggiungere le proprietà rilevate alle azioni nella definizione JSON dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c0994-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="c0994-237">Le proprietà rilevate possono tenere traccia solo di singoli input e output di azioni, ma è possibile usare le proprietà `correlation` degli eventi per correlare più azioni in un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c0994-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="c0994-238">Per tenere traccia di una o più proprietà, aggiungere la sezione `trackedProperties` e le proprietà desiderate alla definizione dell'azione.</span><span class="sxs-lookup"><span data-stu-id="c0994-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="c0994-239">Si supponga, ad esempio, di voler tenere traccia di dati come un "ID ordine" nella telemetria:</span><span class="sxs-lookup"><span data-stu-id="c0994-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="c0994-240">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0994-240">Next steps</span></span>

* [<span data-ttu-id="c0994-241">Creare modelli per la distribuzione delle app per la logica e la gestione dei rilasci</span><span class="sxs-lookup"><span data-stu-id="c0994-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="c0994-242">Scenari B2B con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c0994-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="c0994-243">Monitorare i messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="c0994-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)