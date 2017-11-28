---
title: Soluzione Azure SQL Analytics in Log Analytics | Microsoft Docs
description: La soluzione Azure SQL Analytics consente di gestire i database SQL di Azure.
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
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="713ca-103">Monitorare un database SQL di Azure usando Azure SQL Analytics (anteprima) in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="713ca-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Simbolo di Analisi SQL di Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="713ca-105">La soluzione Analisi SQL di Azure in Azure Log Analytics raccoglie e visualizza importanti metriche sulle prestazioni di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="713ca-106">Usando le metriche raccolte con la soluzione, è possibile creare regole e avvisi di monitoraggio personalizzati.</span><span class="sxs-lookup"><span data-stu-id="713ca-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="713ca-107">È anche possibile monitorare il database SQL di Azure e le metriche dei pool elastici in più sottoscrizioni e pool elastici di Azure e visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="713ca-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="713ca-108">La soluzione consente anche di identificare i problemi a ogni livello dello stack di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="713ca-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="713ca-109">Usa le [metriche di Diagnostica di Azure](log-analytics-azure-storage.md) con le viste di Log Analytics per presentare i dati su tutti i database SQL di Azure e i pool elastici in un'unica area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="713ca-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="713ca-110">Questa soluzione in anteprima supporta attualmente fino a 150.000 database SQL di Azure e 5.000 pool elastici SQL per area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="713ca-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="713ca-111">La soluzione Analisi SQL di Azure, come altre disponibili per Log Analytics, consente di monitorare e ricevere notifiche sull'integrità delle risorse di Azure, in questo caso il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="713ca-112">Il database SQL di Microsoft Azure è un servizio di database relazionale scalabile che fornisce le comuni funzionalità di tipo SQL Server alle applicazioni in esecuzione nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="713ca-113">Log Analytics consente di raccogliere, correlare e visualizzare dati strutturati e non strutturati.</span><span class="sxs-lookup"><span data-stu-id="713ca-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="713ca-114">Origini connesse</span><span class="sxs-lookup"><span data-stu-id="713ca-114">Connected sources</span></span>

<span data-ttu-id="713ca-115">La soluzione Analisi SQL di Azure non usa agenti per connettersi al servizio Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="713ca-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="713ca-116">La tabella seguente descrive le origini connesse che sono supportate da questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="713ca-117">Origine connessa</span><span class="sxs-lookup"><span data-stu-id="713ca-117">Connected Source</span></span> | <span data-ttu-id="713ca-118">Supporto</span><span class="sxs-lookup"><span data-stu-id="713ca-118">Support</span></span> | <span data-ttu-id="713ca-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="713ca-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="713ca-120">Agenti di Windows</span><span class="sxs-lookup"><span data-stu-id="713ca-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="713ca-121">No</span><span class="sxs-lookup"><span data-stu-id="713ca-121">No</span></span> | <span data-ttu-id="713ca-122">Gli agenti Windows diretti non vengono usati dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="713ca-123">Agenti Linux</span><span class="sxs-lookup"><span data-stu-id="713ca-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="713ca-124">No</span><span class="sxs-lookup"><span data-stu-id="713ca-124">No</span></span> | <span data-ttu-id="713ca-125">Gli agenti Linux diretti non vengono usati dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="713ca-126">Gruppo di gestione SCOM</span><span class="sxs-lookup"><span data-stu-id="713ca-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="713ca-127">No</span><span class="sxs-lookup"><span data-stu-id="713ca-127">No</span></span> | <span data-ttu-id="713ca-128">Una connessione diretta dall'agente SCOM a Log Analytics non viene usata dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="713ca-129">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="713ca-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="713ca-130">No</span><span class="sxs-lookup"><span data-stu-id="713ca-130">No</span></span> | <span data-ttu-id="713ca-131">Log Analytics non legge i dati da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="713ca-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="713ca-132">Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="713ca-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="713ca-133">Sì</span><span class="sxs-lookup"><span data-stu-id="713ca-133">Yes</span></span> | <span data-ttu-id="713ca-134">I dati relativi alle metriche di Azure vengono inviati a Log Analytics direttamente da Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="713ca-135">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="713ca-135">Prerequisites</span></span>

- <span data-ttu-id="713ca-136">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-136">An Azure Subscription.</span></span> <span data-ttu-id="713ca-137">Se non si ha una sottoscrizione, è possibile crearne una [gratuitamente](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="713ca-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="713ca-138">Un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="713ca-138">A Log Analytics workspace.</span></span> <span data-ttu-id="713ca-139">È possibile usarne una esistente o [crearne una nuova](log-analytics-get-started.md) prima di iniziare a usare questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="713ca-140">Abilitare Diagnostica di Azure per i database SQL di Azure SQL e i pool elastici e [configurarli per l'invio dei dati a Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="713ca-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="713ca-141">Configurazione</span><span class="sxs-lookup"><span data-stu-id="713ca-141">Configuration</span></span>

<span data-ttu-id="713ca-142">Eseguire questa procedura per aggiungere la soluzione Analisi SQL di Azure all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="713ca-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="713ca-143">Aggiungere la soluzione Azure SQL Analytics da [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="713ca-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="713ca-144">Nel portale di Azure fare clic su **Nuovo** (il simbolo +), quindi nell'elenco di risorse selezionare **Monitoraggio e gestione**.</span><span class="sxs-lookup"><span data-stu-id="713ca-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="713ca-145">![Monitoraggio e gestione](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="713ca-146">Nell'elenco **Monitoraggio e gestione** fare clic su **Visualizza tutto**.</span><span class="sxs-lookup"><span data-stu-id="713ca-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="713ca-147">Nell'elenco **Consigliati** fare clic su **Altro** e quindi nel nuovo elenco trovare **Azure SQL Analytics (anteprima)** e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="713ca-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="713ca-148">![Soluzione Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="713ca-149">Nel pannello **Azure SQL Analytics (anteprima)** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="713ca-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="713ca-150">![Creare](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="713ca-151">Nel pannello **Crea nuova soluzione** selezionare l'area di lavoro che si vuole aggiungere alla soluzione e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="713ca-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="713ca-152">![Aggiunta all'area di lavoro](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="713ca-153">Per configurare più sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="713ca-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="713ca-154">Per supportare più sottoscrizioni, usare lo script di PowerShell contenuto in [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/) (Abilitare la registrazione delle metriche sulle risorse di Azure usando PowerShell).</span><span class="sxs-lookup"><span data-stu-id="713ca-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="713ca-155">Specificare l'ID risorsa dell'area di lavoro come parametro quando si esegue lo script per inviare i dati di diagnostica dalle risorse in una sottoscrizione di Azure a un'area di lavoro in un'altra sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="713ca-156">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="713ca-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="713ca-157">Uso della soluzione</span><span class="sxs-lookup"><span data-stu-id="713ca-157">Using the solution</span></span>

<span data-ttu-id="713ca-158">Quando si aggiunge la soluzione all'area di lavoro, il riquadro Azure SQL Analytics viene aggiunto all'area di lavoro e visualizzato in Panoramica.</span><span class="sxs-lookup"><span data-stu-id="713ca-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="713ca-159">Il riquadro mostra il numero di database SQL di Azure e di pool elastici SQL a cui la soluzione è connessa.</span><span class="sxs-lookup"><span data-stu-id="713ca-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Riquadro Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="713ca-161">Visualizzazione dei dati di Analisi SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="713ca-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="713ca-162">Fare clic sul riquadro **Analisi SQL di Azure** per aprire il dashboard Analisi SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="713ca-163">Il dashboard include i pannelli definiti di seguito.</span><span class="sxs-lookup"><span data-stu-id="713ca-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="713ca-164">Ogni pannello elenca un massimo di 15 risorse (sottoscrizione, server, pool elastico e database).</span><span class="sxs-lookup"><span data-stu-id="713ca-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="713ca-165">Fare clic su una delle risorse per aprire il dashboard per una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="713ca-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="713ca-166">Pool elastico o Database contengono i grafici con le metriche per una risorsa selezionata.</span><span class="sxs-lookup"><span data-stu-id="713ca-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="713ca-167">Fare clic su un grafico per aprire la finestra di dialogo Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="713ca-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="713ca-168">Pannello</span><span class="sxs-lookup"><span data-stu-id="713ca-168">Blade</span></span> | <span data-ttu-id="713ca-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="713ca-169">Description</span></span> |
|---|---|
| <span data-ttu-id="713ca-170">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="713ca-170">Subscriptions</span></span> | <span data-ttu-id="713ca-171">Elenco delle sottoscrizioni con numero di server, pool e database connessi.</span><span class="sxs-lookup"><span data-stu-id="713ca-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="713ca-172">Server</span><span class="sxs-lookup"><span data-stu-id="713ca-172">Servers</span></span> | <span data-ttu-id="713ca-173">Elenco dei server con numero di pool e database connessi.</span><span class="sxs-lookup"><span data-stu-id="713ca-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="713ca-174">Pool elastici</span><span class="sxs-lookup"><span data-stu-id="713ca-174">Elastic Pools</span></span> | <span data-ttu-id="713ca-175">Elenco di pool elastici connessi con numero massimo di GB ed eDTU nel periodo osservato.</span><span class="sxs-lookup"><span data-stu-id="713ca-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="713ca-176">Database</span><span class="sxs-lookup"><span data-stu-id="713ca-176">Databases</span></span> | <span data-ttu-id="713ca-177">Elenco di database connessi con numero massimo di GB e DTU nel periodo osservato.</span><span class="sxs-lookup"><span data-stu-id="713ca-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="713ca-178">Analizzare i dati e creare avvisi</span><span class="sxs-lookup"><span data-stu-id="713ca-178">Analyze data and create alerts</span></span>

<span data-ttu-id="713ca-179">È possibile creare facilmente avvisi con i dati provenienti dalle risorse del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="713ca-180">Di seguito sono riportati due query utili di [ricerca nei log](log-analytics-log-searches.md) che è possibile usare per gli avvisi:</span><span class="sxs-lookup"><span data-stu-id="713ca-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="713ca-181">*Elevato utilizzo di DTU nel database SQL di Azure*</span><span class="sxs-lookup"><span data-stu-id="713ca-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="713ca-182">*Elevato utilizzo di DTU nel pool elastico del database SQL di Azure*</span><span class="sxs-lookup"><span data-stu-id="713ca-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="713ca-183">È possibile usare queste query basate su avvisi per creare avvisi per soglie specifiche sia per i database SQL di Azure che per i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="713ca-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="713ca-184">Per configurare un avviso per l'area di lavoro OMS:</span><span class="sxs-lookup"><span data-stu-id="713ca-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="713ca-185">Per configurare un avviso per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="713ca-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="713ca-186">Aprire il [portale di OMS](http://mms.microsoft.com/) e accedere.</span><span class="sxs-lookup"><span data-stu-id="713ca-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="713ca-187">Aprire l'area di lavoro configurata per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="713ca-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="713ca-188">Nella pagina Panoramica fare clic sul riquadro **Azure SQL Analytics (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="713ca-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="713ca-189">Eseguire una delle query di esempio.</span><span class="sxs-lookup"><span data-stu-id="713ca-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="713ca-190">In Ricerca log fare clic su **Avviso**.</span><span class="sxs-lookup"><span data-stu-id="713ca-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="713ca-191">![Creare un avviso nella ricerca](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="713ca-192">Nella pagina **Aggiungi regola di avviso** configurare le proprietà necessarie e le soglie specifiche desiderate e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="713ca-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="713ca-193">![Aggiungere una regola di avviso](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="713ca-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="713ca-194">Agire sui dati di Analisi SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="713ca-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="713ca-195">Ad esempio, una delle query più utili che è possibile eseguire è confrontare l'utilizzo DTU per tutti i pool elastici SQL di Azure in tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="713ca-196">L'unità elaborata di database (DTU, Database Throughput Unit) consente di descrivere la capacità relativa di un livello delle prestazioni dei database e dei pool Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="713ca-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="713ca-197">Le unità DTU sono basate su una misura combinata di CPU, memoria, operazioni di lettura e di scrittura.</span><span class="sxs-lookup"><span data-stu-id="713ca-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="713ca-198">Quando le unità DTU aumentano, aumenta anche la potenza offerta dal livello delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="713ca-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="713ca-199">Un livello delle prestazioni con 5 DTU, ad esempio, ha cinque volte la potenza di un livello delle prestazioni con 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="713ca-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="713ca-200">A ogni server e pool elastico viene applicata una quota massima di DTU.</span><span class="sxs-lookup"><span data-stu-id="713ca-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="713ca-201">Eseguendo la query di ricerca log seguente, è possibile capire facilmente se si sta sottoutilizzando o sovrautilizzando i pool elastici SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="713ca-202">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), la query precedente verrà sostituita dalla seguente.</span><span class="sxs-lookup"><span data-stu-id="713ca-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="713ca-203">Nell'esempio seguente è possibile osservare che un pool elastico ha un utilizzo elevato, prossimo al 100% dell'unità DTU, mentre gli altri hanno un utilizzo molto basso.</span><span class="sxs-lookup"><span data-stu-id="713ca-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="713ca-204">È possibile eseguire un'indagine più approfondita per risolvere i problemi delle potenziali modifiche recenti dell'ambiente usando i log attività di Azure.</span><span class="sxs-lookup"><span data-stu-id="713ca-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Risultati della ricerca log: utilizzo elevato](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="713ca-206">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="713ca-206">See also</span></span>

- <span data-ttu-id="713ca-207">Usare le [ricerche log](log-analytics-log-searches.md) in Log Analytics per visualizzare i dati dettagliati per Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="713ca-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="713ca-208">[Creare dashboard personalizzati](log-analytics-dashboards.md) che mostrino i dati per Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="713ca-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="713ca-209">[Creare avvisi](log-analytics-alerts.md) quando si verificano eventi specifici relativi ad Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="713ca-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
