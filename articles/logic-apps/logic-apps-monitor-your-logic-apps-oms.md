---
title: aaaMonitor e ottenere informazioni dettagliate sull'app logica viene eseguita mediante OMS - App Azure per la logica | Documenti Microsoft
description: "Monitorare l'esecuzione dell'applicazione logica con informazioni dettagliate tooget Log Analitica e Operations Management Suite (OMS) e le informazioni di debug più dettagliate per la risoluzione dei problemi e diagnostica"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="ecb74-103">Monitorare e ottenere informazioni dettagliate sulle esecuzioni dell'app per la logica con Operations Management Suite (OMS) e Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ecb74-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="ecb74-104">Per informazioni di debug più dettagliate e monitoraggio, è possibile attivare Analitica di Log in hello contemporaneamente quando si crea un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="ecb74-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="ecb74-105">Log Analitica fornisce Diagnostica registrazione e monitoraggio per l'app logica viene eseguita tramite il portale di Operations Management Suite (OMS) hello.</span><span class="sxs-lookup"><span data-stu-id="ecb74-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="ecb74-106">Quando si aggiunge hello logica di gestione delle App soluzione tooOMS, si ottiene lo stato aggregato per la logica app viene eseguita e dettagli specifici, ad esempio lo stato, il tempo di esecuzione, lo stato di un nuovo invio e ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="ecb74-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="ecb74-107">Questo argomento viene illustrato come tooturn nel Log Analitica o installare hello soluzione logica di gestione delle App in OMS, in modo che è possibile visualizzare gli eventi di runtime e i dati per l'applicazione della logica di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ecb74-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="ecb74-108">toomonitor logica App, seguire questi passaggi troppo [attivare la registrazione diagnostica e inviare la logica app runtime dati tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="ecb74-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="ecb74-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ecb74-109">Requirements</span></span>

<span data-ttu-id="ecb74-110">Prima di iniziare, è necessario toohave un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="ecb74-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="ecb74-111">Informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ecb74-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="ecb74-112">Attivare la registrazione della diagnostica durante la creazione di app per la logica</span><span class="sxs-lookup"><span data-stu-id="ecb74-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="ecb74-113">Nel [portale di Azure](https://portal.azure.com) creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ecb74-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="ecb74-114">Scegliere **Nuovo** > **Enterprise Integration** > **App per la logica** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Creare un'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="ecb74-116">In hello **crea la logica app** eseguire queste attività, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="ecb74-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="ecb74-117">Assegnare un nome all'app per la logica e selezionare la sottoscrizione di Azure personale.</span><span class="sxs-lookup"><span data-stu-id="ecb74-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="ecb74-118">Creare o selezionare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecb74-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="ecb74-119">Impostare **Log Analitica** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="ecb74-120">Area di lavoro OMS selezionare hello in cui si desidera troppo invia dati per l'applicazione della logica di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ecb74-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="ecb74-121">Quando si è pronti, scegliere **Pin toodashboard** > **crea**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Creare l'app per la logica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="ecb74-123">Al termine di questo passaggio, Azure crea l'app per la logica, che ora è associata all'area di lavoro OMS personale.</span><span class="sxs-lookup"><span data-stu-id="ecb74-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="ecb74-124">Inoltre, questo passaggio installa automaticamente anche soluzioni di gestione delle App logica hello nell'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="ecb74-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="ecb74-125">in OMS, l'esecuzione dell'app logica tooview [continuare con la procedura](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="ecb74-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="ecb74-126">Installare una soluzione di gestione delle App logica hello in OMS</span><span class="sxs-lookup"><span data-stu-id="ecb74-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="ecb74-127">Se Log Analytics è già stato attivato al momento della creazione dell'app per la logica, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="ecb74-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="ecb74-128">Si dispone già di soluzione di gestione delle app di logica di hello installato in OMS.</span><span class="sxs-lookup"><span data-stu-id="ecb74-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="ecb74-129">In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="ecb74-130">Digitare "Log Analytics" come filtro e scegliere **Log Analytics**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ecb74-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Scegliere "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="ecb74-132">In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="ecb74-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="ecb74-134">In **Gestione** scegliere **Portale di OMS**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Scegliere "Portale di OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="ecb74-136">Nella home page OMS, se viene visualizzata l'intestazione aggiornamento hello, scegliere il banner hello in modo che si aggiorna l'area di lavoro OMS prima.</span><span class="sxs-lookup"><span data-stu-id="ecb74-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="ecb74-137">Scegliere quindi **Raccolta soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-137">Then choose **Solutions Gallery**.</span></span>

   ![Scegliere "Raccolta soluzioni"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="ecb74-139">In **tutte le soluzioni**, trovare e scegliere il riquadro di hello per hello **logica di gestione delle app** soluzione.</span><span class="sxs-lookup"><span data-stu-id="ecb74-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Scegliere "Logic Apps Management" ("Gestione delle app per la logica")](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="ecb74-141">soluzione hello tooinstall nell'area di lavoro OMS, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Scegliere "Aggiungi" per "Logic Apps Management" ("Gestione delle app per la logica")](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="ecb74-143">Visualizzare le esecuzioni dell'app per la logica nell'area di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="ecb74-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="ecb74-144">conteggio hello tooview e lo stato per l'app logica viene eseguito, pagina di panoramica passare toohello dell'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="ecb74-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="ecb74-145">Esaminare i dettagli di hello in hello **logica di gestione delle app** riquadro.</span><span class="sxs-lookup"><span data-stu-id="ecb74-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Riquadro di panoramica con il numero e lo stato delle esecuzioni dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="ecb74-147">Se questo aggiornamento viene invece riquadro logica di gestione delle App hello, scegliere il banner hello in modo che si aggiorna l'area di lavoro OMS prima.</span><span class="sxs-lookup"><span data-stu-id="ecb74-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Aggiornare "l'area di lavoro di OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="ecb74-149">tooview un riepilogo con ulteriori dettagli sull'esecuzione dell'applicazione logica, scegliere hello **logica di gestione delle app** riquadro.</span><span class="sxs-lookup"><span data-stu-id="ecb74-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="ecb74-150">In questo riquadro le esecuzioni dell'app per la logica vengono raggruppate in base al nome o allo stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ecb74-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Riepilogo dello stato per le esecuzioni dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="ecb74-152">tooview che tutti hello viene eseguita per una logica specifica app o stato, riga hello selezionare per un'app di logica o lo stato.</span><span class="sxs-lookup"><span data-stu-id="ecb74-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="ecb74-153">Di seguito è riportato un esempio che illustra tutte le esecuzioni di hello per un'applicazione una logica specifica:</span><span class="sxs-lookup"><span data-stu-id="ecb74-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Visualizzare le esecuzioni per un'app per la logica o uno stato](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="ecb74-155">Hello **nuovo invio** colonna viene visualizzato "Sì" per le operazioni risultanti da un'esecuzione inviata di nuovo.</span><span class="sxs-lookup"><span data-stu-id="ecb74-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="ecb74-156">toofilter questi risultati, è possibile eseguire il filtro sia sul lato client e lato server.</span><span class="sxs-lookup"><span data-stu-id="ecb74-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="ecb74-157">Filtro lato client: per ogni colonna, scegliere i filtri di hello desiderati.</span><span class="sxs-lookup"><span data-stu-id="ecb74-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="ecb74-158">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="ecb74-158">Here are some examples:</span></span>

     ![Esempi di filtri di colonna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="ecb74-160">Filtro lato server: toochoose un numero di hello finestra o toolimit ora specifica di esecuzione che vengono visualizzati, usare il controllo ambito hello nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="ecb74-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="ecb74-161">Per impostazione predefinita, vengono visualizzati contemporaneamente solo 1.000 record.</span><span class="sxs-lookup"><span data-stu-id="ecb74-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Intervallo di tempo hello modifica](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="ecb74-163">tooview tutti hello azioni e i relativi dettagli per un specifico, selezionare una riga, che verrà visualizzata la pagina di ricerca nei Log hello.</span><span class="sxs-lookup"><span data-stu-id="ecb74-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="ecb74-164">tooview queste informazioni in una tabella, scegliere **tabella**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="ecb74-165">query di hello toochange, è possibile modificare la stringa di query hello nella barra di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="ecb74-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="ecb74-166">Per un'esperienza migliore, scegliere **Analisi avanzata**.</span><span class="sxs-lookup"><span data-stu-id="ecb74-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Visualizzare azioni e i dettagli per un'esecuzione dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="ecb74-168">Nella pagina hello Azure Log Analitica qui è possibile aggiornare le query e visualizzare hello risultante dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ecb74-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="ecb74-169">Questa query utilizza [il linguaggio di query Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), che può essere modificato se si desidera tooview diversi risultati.</span><span class="sxs-lookup"><span data-stu-id="ecb74-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics - Visualizzazione Query](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="ecb74-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ecb74-171">Next steps</span></span>

* [<span data-ttu-id="ecb74-172">Monitorare i messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="ecb74-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
