---
title: soluzione Analitica SQL in Log Analitica aaaAzure | Documenti Microsoft
description: Hello soluzione Analitica SQL Azure consente di gestire i database SQL di Azure.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="e2aee-103">Monitorare un database SQL di Azure usando Azure SQL Analytics (anteprima) in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e2aee-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Simbolo di Analisi SQL di Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="e2aee-105">Hello soluzione Analitica SQL Azure in Azure Log Analitica raccoglie e visualizza le metriche delle prestazioni di SQL Azure importanti.</span><span class="sxs-lookup"><span data-stu-id="e2aee-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="e2aee-106">Utilizzando le metriche di hello raccolti con soluzione hello, è possibile creare avvisi e le regole di monitoraggio personalizzate.</span><span class="sxs-lookup"><span data-stu-id="e2aee-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="e2aee-107">È anche possibile monitorare il database SQL di Azure e le metriche dei pool elastici in più sottoscrizioni e pool elastici di Azure e visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="e2aee-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="e2aee-108">soluzione Hello consente inoltre di problemi di tooidentify a ogni livello dello stack applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2aee-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="e2aee-109">Usa [metriche di diagnostica Azure](log-analytics-azure-storage.md) insieme Log Analitica Visualizza i dati di toopresent su tutti i database SQL di Azure e i pool elastici in un'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="e2aee-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="e2aee-110">Attualmente, questa soluzione di anteprima supporta backup too150, 000 i database di SQL Azure e 5.000 pool elastico SQL per ogni area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e2aee-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="e2aee-111">Hello soluzione Analitica SQL Azure, come altri disponibili per i Log Analitica, consente di monitorare e ricevere notifiche sull'integrità hello di risorse di Azure, in questo caso, il Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="e2aee-112">Database SQL di Microsoft Azure è un servizio di database relazionale scalabile che offre familiarità tooapplications di funzionalità simile a SQL Server in esecuzione in hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="e2aee-113">Log Analitica consente toocollect, correlare e visualizzare i dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="e2aee-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="e2aee-114">Origini connesse</span><span class="sxs-lookup"><span data-stu-id="e2aee-114">Connected sources</span></span>

<span data-ttu-id="e2aee-115">Hello soluzione Analitica SQL Azure non usa gli agenti tooconnect toohello servizio Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="e2aee-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="e2aee-116">Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="e2aee-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="e2aee-117">Origine connessa</span><span class="sxs-lookup"><span data-stu-id="e2aee-117">Connected Source</span></span> | <span data-ttu-id="e2aee-118">Supporto</span><span class="sxs-lookup"><span data-stu-id="e2aee-118">Support</span></span> | <span data-ttu-id="e2aee-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e2aee-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e2aee-120">Agenti di Windows</span><span class="sxs-lookup"><span data-stu-id="e2aee-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="e2aee-121">No</span><span class="sxs-lookup"><span data-stu-id="e2aee-121">No</span></span> | <span data-ttu-id="e2aee-122">Diretta degli agenti di Windows non vengono utilizzati dalla soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="e2aee-123">Agenti Linux</span><span class="sxs-lookup"><span data-stu-id="e2aee-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="e2aee-124">No</span><span class="sxs-lookup"><span data-stu-id="e2aee-124">No</span></span> | <span data-ttu-id="e2aee-125">Gli agenti Linux diretti non vengono utilizzati dalla soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="e2aee-126">Gruppo di gestione SCOM</span><span class="sxs-lookup"><span data-stu-id="e2aee-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="e2aee-127">No</span><span class="sxs-lookup"><span data-stu-id="e2aee-127">No</span></span> | <span data-ttu-id="e2aee-128">Una connessione diretta da hello SCOM agente tooLog Analitica non è utilizzata dalla soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="e2aee-129">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e2aee-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="e2aee-130">No</span><span class="sxs-lookup"><span data-stu-id="e2aee-130">No</span></span> | <span data-ttu-id="e2aee-131">Log Analitica leggere hello dati da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2aee-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="e2aee-132">Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="e2aee-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="e2aee-133">Sì</span><span class="sxs-lookup"><span data-stu-id="e2aee-133">Yes</span></span> | <span data-ttu-id="e2aee-134">Dati di metrica Azure vengono inviati tooLog Analitica direttamente da Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="e2aee-135">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e2aee-135">Prerequisites</span></span>

- <span data-ttu-id="e2aee-136">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-136">An Azure Subscription.</span></span> <span data-ttu-id="e2aee-137">Se non si ha una sottoscrizione, è possibile crearne una [gratuitamente](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e2aee-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="e2aee-138">Un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2aee-138">A Log Analytics workspace.</span></span> <span data-ttu-id="e2aee-139">È possibile usarne una esistente o [crearne una nuova](log-analytics-get-started.md) prima di iniziare a usare questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="e2aee-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="e2aee-140">Abilitare la diagnostica di Azure per i database di SQL Azure e i pool elastici e [configurarli toosend loro tooLog dati Analitica](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="e2aee-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="e2aee-141">Configurazione</span><span class="sxs-lookup"><span data-stu-id="e2aee-141">Configuration</span></span>

<span data-ttu-id="e2aee-142">Eseguire hello seguendo i passaggi tooadd hello Azure SQL Analitica soluzione tooyour dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e2aee-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="e2aee-143">Aggiungere hello Azure SQL Analitica soluzione tooyour area di lavoro da [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="e2aee-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="e2aee-144">Nel portale di Azure hello, fare clic su **New** (hello simbolo +), quindi hello seleziona nell'elenco di risorse, **monitoraggio + gestione**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="e2aee-145">![Monitoraggio e gestione](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="e2aee-146">In hello **monitoraggio + gestione** fare clic su elenco **tutti**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="e2aee-147">In hello **consigliato** elenco, fare clic su **più** e quindi nell'elenco nuovo hello individuare **Analitica di SQL Azure (anteprima)** e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="e2aee-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="e2aee-148">![Soluzione Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="e2aee-149">In hello **Analitica di SQL Azure (anteprima)** pannello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="e2aee-150">![Creare](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="e2aee-151">In hello **Crea nuova soluzione** blade, dell'area di lavoro selezionare hello che desidera tooadd hello soluzione tooand, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="e2aee-152">![aggiungere tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="e2aee-153">tooconfigure più sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e2aee-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="e2aee-154">toosupport più sottoscrizioni, usare uno script di PowerShell hello da [registrazione metriche di risorsa abilitare Azure tramite PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="e2aee-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="e2aee-155">Fornire l'ID risorsa dell'area di lavoro di hello come parametro durante l'esecuzione di dati di diagnostica di hello script toosend dalle risorse nell'area di lavoro tooa una sottoscrizione di Azure in un'altra sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="e2aee-156">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="e2aee-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="e2aee-157">Utilizzo di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="e2aee-157">Using hello solution</span></span>

<span data-ttu-id="e2aee-158">Quando si aggiunge l'area di lavoro tooyour soluzione hello, hello riquadro Analitica SQL Azure viene aggiunto tooyour dell'area di lavoro e viene visualizzato nella panoramica.</span><span class="sxs-lookup"><span data-stu-id="e2aee-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="e2aee-159">riquadro Hello Mostra il numero di hello di database SQL di Azure e i pool elastici SQL di Azure connessa a soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Riquadro Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="e2aee-161">Visualizzazione dei dati di Analisi SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2aee-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="e2aee-162">Fare clic su hello **Analitica SQL Azure** riquadro tooopen hello Azure SQL Analitica dashboard.</span><span class="sxs-lookup"><span data-stu-id="e2aee-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="e2aee-163">dashboard Hello include pannelli hello definiti di seguito.</span><span class="sxs-lookup"><span data-stu-id="e2aee-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="e2aee-164">Ogni pannello elenca le risorse too15 (sottoscrizione server, il pool elastico e database).</span><span class="sxs-lookup"><span data-stu-id="e2aee-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="e2aee-165">Fare clic su uno qualsiasi dei dashboard di hello risorse tooopen hello per tale risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="e2aee-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="e2aee-166">Elastico Pool o il Database contiene grafici hello con le metriche per una risorsa selezionata.</span><span class="sxs-lookup"><span data-stu-id="e2aee-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="e2aee-167">Fare clic su una finestra di dialogo ricerca nei Log di hello tooopen di grafico.</span><span class="sxs-lookup"><span data-stu-id="e2aee-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="e2aee-168">Pannello</span><span class="sxs-lookup"><span data-stu-id="e2aee-168">Blade</span></span> | <span data-ttu-id="e2aee-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e2aee-169">Description</span></span> |
|---|---|
| <span data-ttu-id="e2aee-170">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="e2aee-170">Subscriptions</span></span> | <span data-ttu-id="e2aee-171">Elenco delle sottoscrizioni con numero di server, pool e database connessi.</span><span class="sxs-lookup"><span data-stu-id="e2aee-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="e2aee-172">Server</span><span class="sxs-lookup"><span data-stu-id="e2aee-172">Servers</span></span> | <span data-ttu-id="e2aee-173">Elenco dei server con numero di pool e database connessi.</span><span class="sxs-lookup"><span data-stu-id="e2aee-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="e2aee-174">Pool elastici</span><span class="sxs-lookup"><span data-stu-id="e2aee-174">Elastic Pools</span></span> | <span data-ttu-id="e2aee-175">Elenco di pool elastico connesso con hello osservato di eDTU e GB massimo di periodo.</span><span class="sxs-lookup"><span data-stu-id="e2aee-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="e2aee-176">Database</span><span class="sxs-lookup"><span data-stu-id="e2aee-176">Databases</span></span> | <span data-ttu-id="e2aee-177">Elenco di database connessi con DTU e GB massimo osservati hello periodo.</span><span class="sxs-lookup"><span data-stu-id="e2aee-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="e2aee-178">Analizzare i dati e creare avvisi</span><span class="sxs-lookup"><span data-stu-id="e2aee-178">Analyze data and create alerts</span></span>

<span data-ttu-id="e2aee-179">È possibile creare facilmente avvisi con dati hello provenienti dalle risorse di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="e2aee-180">Di seguito sono riportati due query utili di [ricerca nei log](log-analytics-log-searches.md) che è possibile usare per gli avvisi:</span><span class="sxs-lookup"><span data-stu-id="e2aee-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="e2aee-181">*Elevato utilizzo di DTU nel database SQL di Azure*</span><span class="sxs-lookup"><span data-stu-id="e2aee-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="e2aee-182">*Elevato utilizzo di DTU nel pool elastico del database SQL di Azure*</span><span class="sxs-lookup"><span data-stu-id="e2aee-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="e2aee-183">È possibile utilizzare questi tooalert le query basate su avviso sulle soglie specifiche per i Database di SQL Azure e il pool elastico.</span><span class="sxs-lookup"><span data-stu-id="e2aee-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="e2aee-184">un avviso per l'area di lavoro OMS tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="e2aee-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="e2aee-185">tooconfigure un avviso per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="e2aee-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="e2aee-186">Passare toohello [portale OMS](http://mms.microsoft.com/) ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e2aee-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="e2aee-187">Aprire l'area di lavoro di hello che è stato configurato per la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="e2aee-188">Nella pagina di panoramica hello, fare clic su hello **Analitica di SQL Azure (anteprima)** riquadro.</span><span class="sxs-lookup"><span data-stu-id="e2aee-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="e2aee-189">Eseguire una delle query di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="e2aee-190">In Ricerca log fare clic su **Avviso**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="e2aee-191">![Creare un avviso nella ricerca](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="e2aee-192">In hello **Aggiungi regola di avviso** pagina, configurare le proprietà appropriate hello e hello soglie specifiche che si desidera e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e2aee-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="e2aee-193">![Aggiungere una regola di avviso](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="e2aee-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="e2aee-194">Agire sui dati di Analisi SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2aee-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="e2aee-195">Ad esempio, una delle query più utili di hello che è possibile eseguire è l'utilizzo di DTU toocompare hello per tutti i pool elastico di SQL Azure per tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="e2aee-196">Unità di velocità effettiva database (DTU) fornisce un modo toodescribe hello capacità relativa di un livello di prestazioni di database Basic, Standard e Premium e pool.</span><span class="sxs-lookup"><span data-stu-id="e2aee-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="e2aee-197">Le unità DTU sono basate su una misura combinata di CPU, memoria, operazioni di lettura e di scrittura.</span><span class="sxs-lookup"><span data-stu-id="e2aee-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="e2aee-198">Aumentare delle Dtu hello potenza offerto da Aumenta livello di prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="e2aee-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="e2aee-199">Un livello delle prestazioni con 5 DTU, ad esempio, ha cinque volte la potenza di un livello delle prestazioni con 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="e2aee-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="e2aee-200">Quota massima di DTU si applica il pool di server ed elastica tooeach.</span><span class="sxs-lookup"><span data-stu-id="e2aee-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="e2aee-201">Eseguendo hello seguenti query di ricerca di Log, è possibile stabilire facilmente se si sottoutilizzano o oltre che utilizzano il pool elastico SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="e2aee-202">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="e2aee-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="e2aee-203">Nell'esempio seguente di hello, si noterà che un pool elastico ha un utilizzo elevato prossimo al 100% DTU mentre altri hanno un utilizzo minimo.</span><span class="sxs-lookup"><span data-stu-id="e2aee-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="e2aee-204">È possibile esaminare ulteriori modifiche recenti potenziali tootroubleshoot nel proprio ambiente usando i log attività di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Risultati della ricerca log: utilizzo elevato](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="e2aee-206">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e2aee-206">See also</span></span>

- <span data-ttu-id="e2aee-207">Utilizzare [ricerche nei Log](log-analytics-log-searches.md) nel Log Analitica tooview in dettaglio i dati di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e2aee-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="e2aee-208">[Creare dashboard personalizzati](log-analytics-dashboards.md) che mostrino i dati per Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="e2aee-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="e2aee-209">[Creare avvisi](log-analytics-alerts.md) quando si verificano eventi specifici relativi ad Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="e2aee-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
