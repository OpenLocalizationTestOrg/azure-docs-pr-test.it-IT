---
title: stato aaaCheck, impostare la registrazione e ottenere avvisi - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="dd601-103">Monitorare lo stato, configurare la registrazione diagnostica e attivare gli avvisi per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="dd601-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="dd601-104">Dopo avere [creato ed eseguito un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md), è possibile controllarne la cronologia delle esecuzioni, la cronologia dei trigger, lo stato e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="dd601-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="dd601-105">Per il monitoraggio degli eventi in tempo reale e il debug avanzato, configurare la [registrazione diagnostica](#azure-diagnostics) per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="dd601-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="dd601-106">In questo modo è possibile [trovare e visualizzare gli eventi](#find-events), ad esempio eventi di attivazione, eventi di esecuzione ed eventi di azione.</span><span class="sxs-lookup"><span data-stu-id="dd601-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="dd601-107">È anche possibile usare questi [dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd601-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="dd601-108">Impostare notifiche tooget sugli errori o altri problemi possibili, [avvisi](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="dd601-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="dd601-109">È ad esempio possibile creare un avviso che rileva "quando più di cinque esecuzioni in un'ora hanno esito negativo".</span><span class="sxs-lookup"><span data-stu-id="dd601-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="dd601-110">È anche possibile configurare il monitoraggio, la verifica e la registrazione a livello di codice usando [impostazioni e proprietà degli eventi di Diagnostica di Azure](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="dd601-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="dd601-111">Visualizzare la cronologia di esecuzioni e trigger per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="dd601-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="dd601-112">toofind app logica in hello [portale di Azure](https://portal.azure.com), in hello menu principale di Azure, scegliere **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="dd601-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="dd601-113">Nella casella di ricerca hello, cercare "logica app" e scegliere **logica app**.</span><span class="sxs-lookup"><span data-stu-id="dd601-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Trovare l'app per la logica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="dd601-115">portale di Azure Hello Visualizza tutte le applicazioni di logica di hello associati alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd601-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="dd601-116">Selezionare l'app per la logica, quindi scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="dd601-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="dd601-117">cronologia di esecuzione hello e trigger per l'applicazione della logica di seguito viene Hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd601-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="dd601-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-118">For example:</span></span>

   ![Cronologia delle esecuzioni e cronologia dei trigger delle app per la logica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="dd601-120">**Cronologia di esecuzione** Mostra tutte le esecuzioni di hello per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="dd601-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="dd601-121">**Attivare cronologia** Mostra tutte le attività hello trigger per l'app logica.</span><span class="sxs-lookup"><span data-stu-id="dd601-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="dd601-122">Per le descrizioni degli stati, vedere [Risolvere i problemi relativi all'app per la logica](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="dd601-123">Se non si trova dati hello previsti, sulla barra degli strumenti hello, scegliere **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="dd601-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="dd601-124">hello tooview i passaggi da un'esecuzione specifica, in **esegue cronologia**, selezionare che eseguono.</span><span class="sxs-lookup"><span data-stu-id="dd601-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="dd601-125">visualizzazione di monitoraggio Hello Mostra ogni passaggio eseguito.</span><span class="sxs-lookup"><span data-stu-id="dd601-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="dd601-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-126">For example:</span></span>

   ![Azioni per una specifica esecuzione](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="dd601-128">Scegliere ulteriori dettagli sull'esecuzione, hello tooget **Dettagli esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="dd601-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="dd601-129">Queste informazioni vengono riepilogati i passaggi di hello, lo stato, gli input e output per hello eseguire.</span><span class="sxs-lookup"><span data-stu-id="dd601-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Scegliere "Dettagli esecuzione"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="dd601-131">Ad esempio, è possibile ottenere hello dell'esecuzione **ID di correlazione**, che potrebbe essere necessario quando si utilizza hello [API REST per la logica app](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="dd601-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="dd601-132">i dettagli di tooget su un passaggio specifico, scegliere il passaggio.</span><span class="sxs-lookup"><span data-stu-id="dd601-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="dd601-133">È ora possibile esaminare dettagli come input, output ed eventuali errori verificatisi per tale passaggio,</span><span class="sxs-lookup"><span data-stu-id="dd601-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="dd601-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-134">For example:</span></span>

   ![Dettagli del passaggio](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="dd601-136">Tutti i dettagli di runtime e gli eventi vengono crittografati nel servizio App per la logica di hello.</span><span class="sxs-lookup"><span data-stu-id="dd601-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="dd601-137">Vengono decrittografate solo quando un utente richiede tooview tali dati.</span><span class="sxs-lookup"><span data-stu-id="dd601-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="dd601-138">È inoltre possibile controllare gli eventi di accesso toothese con [gestire accesso controllo (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="dd601-139">dettagli di tooget su un evento trigger specifico, tornare indietro toohello **Panoramica** riquadro.</span><span class="sxs-lookup"><span data-stu-id="dd601-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="dd601-140">In **attivare cronologia**selezionare evento trigger hello.</span><span class="sxs-lookup"><span data-stu-id="dd601-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="dd601-141">È ora possibile esaminare dettagli come input e output, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Dettagli dell'output dell'evento di attivazione](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="dd601-143">Attivare la registrazione diagnostica per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="dd601-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="dd601-144">Per il debug avanzato con dettagli ed eventi di runtime, è possibile configurare la registrazione diagnostica con [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="dd601-145">Log Analitica è un servizio in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitoraggio del cloud e si mantengono la disponibilità e prestazioni toohelp di ambienti locali.</span><span class="sxs-lookup"><span data-stu-id="dd601-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="dd601-146">Prima di iniziare, è necessario toohave un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="dd601-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="dd601-147">Informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="dd601-148">In hello [portale di Azure](https://portal.azure.com), individuare e selezionare l'app logica.</span><span class="sxs-lookup"><span data-stu-id="dd601-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="dd601-149">Nel menu Pannello app logica hello in **monitoraggio**, scegliere **diagnostica** > **le impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="dd601-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Passare le impostazioni di diagnostica tooMonitoring, diagnostica,](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="dd601-151">In **Impostazioni di diagnostica** scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="dd601-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Attivare i log di diagnostica](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="dd601-153">A questo punto selezionare categoria hello OMS area di lavoro e l'evento per la registrazione come illustrato:</span><span class="sxs-lookup"><span data-stu-id="dd601-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="dd601-154">Selezionare **inviare tooLog Analitica**.</span><span class="sxs-lookup"><span data-stu-id="dd601-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="dd601-155">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="dd601-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="dd601-156">In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="dd601-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="dd601-157">In **Log**selezionare hello **WorkflowRuntime** categoria.</span><span class="sxs-lookup"><span data-stu-id="dd601-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="dd601-158">Scegliere l'intervallo metrica "hello".</span><span class="sxs-lookup"><span data-stu-id="dd601-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="dd601-159">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dd601-159">When you're done, choose **Save**.</span></span>

   ![Selezionare l'area di lavoro di OMS e i dati per la registrazione](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="dd601-161">È ora possibile trovare eventi e altri dati per eventi di attivazione, eventi di esecuzione ed eventi di azione.</span><span class="sxs-lookup"><span data-stu-id="dd601-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="dd601-162">Trovare eventi e dati per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="dd601-162">Find events and data for your logic app</span></span>

<span data-ttu-id="dd601-163">toofind e visualizzare gli eventi nell'app logica, ad esempio gli eventi trigger, Esegui gli eventi e azione, seguono questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="dd601-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="dd601-164">In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="dd601-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="dd601-165">Cercare "Log Analytics", quindi scegliere **Log Analytics**, come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="dd601-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Scegliere "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="dd601-167">In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="dd601-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="dd601-169">In **Gestione** scegliere **Portale di OMS**.</span><span class="sxs-lookup"><span data-stu-id="dd601-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Scegliere "Portale di OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="dd601-171">Nella home page di OMS scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="dd601-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="dd601-173">-oppure-</span><span class="sxs-lookup"><span data-stu-id="dd601-173">-or-</span></span>

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="dd601-175">Nella casella di ricerca hello, specificare un campo che si desidera toofind e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="dd601-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="dd601-176">Quando si inizia a digitare, OMS mostra le corrispondenze e operazioni che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="dd601-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="dd601-177">Ad esempio, toofind hello primi 10 eventi che si sono verificati, immettere e selezionare la query di ricerca: **categoria = WorkflowRuntime | top 10**</span><span class="sxs-lookup"><span data-stu-id="dd601-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Immettere la stringa di ricerca](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="dd601-179">Altre informazioni, vedere [come toofind dati nel Log Analitica](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="dd601-180">Nella pagina di risultati hello, nella barra sinistra hello scegliere hello intervallo di tempo che si desidera tooview.</span><span class="sxs-lookup"><span data-stu-id="dd601-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="dd601-181">Scegliere la query aggiungendo un filtro, toorefine **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd601-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Scegliere l'intervallo di tempo per i risultati della query](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="dd601-183">In **aggiungere filtri**, immettere il nome di filtro di hello, pertanto è possibile trovare il filtro di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="dd601-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="dd601-184">Selezionare il filtro hello e scegliere **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd601-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="dd601-185">In questo esempio utilizza hello toofind di word "status" non è stato possibile eventi sotto **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="dd601-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="dd601-186">Di seguito hello filtro per **status_s** è già selezionato.</span><span class="sxs-lookup"><span data-stu-id="dd601-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Selezionare il filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="dd601-188">Nella barra sinistra hello, selezionare il valore del filtro hello che desidera toouse e scegliere **applica**.</span><span class="sxs-lookup"><span data-stu-id="dd601-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Selezionare il valore del filtro, scegliere "Applica"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="dd601-190">Ora restituiscono toohello query che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="dd601-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="dd601-191">La query viene aggiornata con il filtro e il valore selezionati.</span><span class="sxs-lookup"><span data-stu-id="dd601-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="dd601-192">Vengono ora filtrati anche i risultati precedenti.</span><span class="sxs-lookup"><span data-stu-id="dd601-192">Your previous results are now filtered too.</span></span>

   ![Restituire tooyour query con risultati filtrati](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="dd601-194">Scegliere la query per un utilizzo futuro, toosave **salvare**.</span><span class="sxs-lookup"><span data-stu-id="dd601-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="dd601-195">Informazioni su [come toosave query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="dd601-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="dd601-196">Estendere l'uso dei dati di diagnostica con altri servizi</span><span class="sxs-lookup"><span data-stu-id="dd601-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="dd601-197">Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="dd601-198">Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dd601-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="dd601-199">I log di diagnostica Azure tooAzure hub eventi del flusso</span><span class="sxs-lookup"><span data-stu-id="dd601-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="dd601-200">È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md),</span><span class="sxs-lookup"><span data-stu-id="dd601-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="dd601-201">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dd601-201">For example:</span></span>

* [<span data-ttu-id="dd601-202">Dati di flusso da hub eventi tooStream Analitica</span><span class="sxs-lookup"><span data-stu-id="dd601-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="dd601-203">Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI</span><span class="sxs-lookup"><span data-stu-id="dd601-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="dd601-204">In base alle opzioni di hello che si desidera configurare, assicurarsi che è primo [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o [creare un hub eventi Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="dd601-205">Selezionare quindi le opzioni di hello per cui si desidera toosend dati di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="dd601-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Inviare dati tooAzure storage account o l'evento hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="dd601-207">Periodi di memorizzazione si applicano solo quando si sceglie toouse un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd601-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="dd601-208">Configurare gli avvisi per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="dd601-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="dd601-209">metriche specifiche toomonitor oppure ha superato le soglie per la logica app, configurare [gli avvisi in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="dd601-210">Informazioni sulle [metriche in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="dd601-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="dd601-211">tooset di avvisi senza [Azure Log Analitica](../log-analytics/log-analytics-overview.md), seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="dd601-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="dd601-212">Per azioni e criteri di avviso più avanzati, [configurare anche Log Analytics](#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="dd601-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="dd601-213">Nel menu Pannello app logica hello in **monitoraggio**, scegliere **diagnostica** > **regole di avviso** > **Aggiungi avviso**come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dd601-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Aggiungere un avviso per l'app per la logica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="dd601-215">In hello **aggiungere una regola di avviso** pannello, creare l'avviso, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="dd601-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="dd601-216">In **Risorsa** selezionare l'app per la logica, se non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="dd601-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="dd601-217">Specificare un nome e una descrizione per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="dd601-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="dd601-218">Selezionare un **metrica** o eventi che si desidera tootrack.</span><span class="sxs-lookup"><span data-stu-id="dd601-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="dd601-219">Selezionare un **condizione**, specificare un **soglia** per metrica hello e seleziona hello **periodo** per il monitoraggio di questa metrica.</span><span class="sxs-lookup"><span data-stu-id="dd601-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="dd601-220">Selezionare se toosend di posta elettronica per l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="dd601-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="dd601-221">Specificare altri indirizzi di posta elettronica per l'invio avviso hello.</span><span class="sxs-lookup"><span data-stu-id="dd601-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="dd601-222">È inoltre possibile specificare un URL del webhook in cui si desidera che toosend hello avviso.</span><span class="sxs-lookup"><span data-stu-id="dd601-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="dd601-223">Questa regola, ad esempio, invia un avviso quando cinque o più esecuzioni in un'ora hanno esito negativo:</span><span class="sxs-lookup"><span data-stu-id="dd601-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Creare una regola di avviso per la metrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="dd601-225">un'app di logica toorun da un avviso, è possibile includere hello [trigger richiesta](../connectors/connectors-native-reqres.md) nel flusso di lavoro, che consente di eseguire attività come questi esempi:</span><span class="sxs-lookup"><span data-stu-id="dd601-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="dd601-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="dd601-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="dd601-227">Inviare un testo</span><span class="sxs-lookup"><span data-stu-id="dd601-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="dd601-228">Aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="dd601-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="dd601-229">Impostazioni e dettagli degli eventi di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="dd601-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="dd601-230">Ogni evento di diagnostica con i dettagli sull'applicazione logica e che l'evento, ad esempio, lo stato di hello, ora di inizio, ora di fine e così via.</span><span class="sxs-lookup"><span data-stu-id="dd601-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="dd601-231">tooprogrammatically impostare il monitoraggio, il rilevamento e la registrazione, unità organizzativa può utilizzare questi dettagli con hello [API REST per le app di Azure logica](https://docs.microsoft.com/rest/api/logic) hello e [API REST per la diagnostica di Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="dd601-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="dd601-232">Ad esempio, hello `ActionCompleted` evento ha hello `clientTrackingId` e `trackedProperties` proprietà che è possibile utilizzare per il rilevamento e monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="dd601-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="dd601-233">`clientTrackingId`: Se non è fornito, Azure automaticamente questo ID viene generato e mette in correlazione gli eventi in un'app di logica di esecuzione, incluse eventuali flussi di lavoro annidati che vengono chiamati da hello logica app.</span><span class="sxs-lookup"><span data-stu-id="dd601-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="dd601-234">È possibile specificare manualmente l'ID di un trigger, passando un `x-ms-client-tracking-id` intestazione con il valore di ID personalizzato nella richiesta di attivazione hello.</span><span class="sxs-lookup"><span data-stu-id="dd601-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="dd601-235">È possibile usare un trigger di richiesta, un trigger HTTP o un trigger webhook.</span><span class="sxs-lookup"><span data-stu-id="dd601-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="dd601-236">`trackedProperties`: tootrack input o output nei dati di diagnostica, è possibile aggiungere le proprietà rilevate tooactions nella definizione JSON logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd601-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="dd601-237">Le proprietà rilevate possono rilevare solo una singola azione input e output, ma è possibile utilizzare hello `correlation` le proprietà di eventi toocorrelate tra azioni in un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dd601-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="dd601-238">tootrack una o più proprietà, aggiungere hello `trackedProperties` sezione e hello proprietà desiderate di definizione dell'azione toohello.</span><span class="sxs-lookup"><span data-stu-id="dd601-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="dd601-239">Ad esempio, si supponga di che voler tootrack dati come un ID"ordine" nei dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="dd601-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dd601-240">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd601-240">Next steps</span></span>

* [<span data-ttu-id="dd601-241">Creare modelli per la distribuzione delle app per la logica e la gestione dei rilasci</span><span class="sxs-lookup"><span data-stu-id="dd601-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="dd601-242">Scenari B2B con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="dd601-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="dd601-243">Monitorare i messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="dd601-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)