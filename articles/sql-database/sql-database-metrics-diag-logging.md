---
title: Metriche del database SQL di Azure e registrazione diagnostica | Microsoft Docs
description: "Informazioni sulla configurazione del database SQL di Azure per archiviare le statistiche sull'utilizzo delle risorse, la connettività e l'esecuzione delle query."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="409c5-103">Metriche del database SQL di Azure e registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="409c5-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="409c5-104">Il database SQL di Azure può generare metriche e log di diagnostica per facilitare il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="409c5-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="409c5-105">È possibile configurare il database SQL di Azure per archiviare l'utilizzo delle risorse, i ruoli di lavoro e sessioni e la connettività in una delle risorse di Azure seguenti:</span><span class="sxs-lookup"><span data-stu-id="409c5-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="409c5-106">**Archiviazione di Azure**: per l'archiviazione di enormi quantità di dati di telemetria a un costo conveniente</span><span class="sxs-lookup"><span data-stu-id="409c5-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="409c5-107">**Hub eventi di Azure**: per l'integrazione dei dati di telemetria del database SQL di Azure con soluzioni di monitoraggio personalizzate o pipeline attive</span><span class="sxs-lookup"><span data-stu-id="409c5-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="409c5-108">**Log Analytics di Azure**: per usare una soluzione di monitoraggio già pronta con funzionalità di reporting, avviso e mitigazione</span><span class="sxs-lookup"><span data-stu-id="409c5-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architettura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="409c5-110">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="409c5-110">Enable logging</span></span>

<span data-ttu-id="409c5-111">Le metriche e la registrazione diagnostica non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="409c5-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="409c5-112">È possibile abilitare e gestire le metriche e la gestione diagnostica usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="409c5-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="409c5-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-113">Azure portal</span></span>
- <span data-ttu-id="409c5-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="409c5-114">PowerShell</span></span>
- <span data-ttu-id="409c5-115">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-115">Azure CLI</span></span>
- <span data-ttu-id="409c5-116">API REST</span><span class="sxs-lookup"><span data-stu-id="409c5-116">REST API</span></span> 
- <span data-ttu-id="409c5-117">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="409c5-117">Resource Manager template</span></span>

<span data-ttu-id="409c5-118">Quando si abilitano le metriche e la registrazione diagnostica, è necessario specificare la risorsa di Azure in cui vengono raccolti i dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="409c5-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="409c5-119">Opzioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="409c5-119">Options available:</span></span>
- <span data-ttu-id="409c5-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="409c5-120">Log analytics</span></span>
- <span data-ttu-id="409c5-121">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="409c5-121">Event Hub</span></span>
- <span data-ttu-id="409c5-122">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-122">Azure Storage</span></span> 

<span data-ttu-id="409c5-123">È possibile eseguire il provisioning di una nuova risorsa di Azure o selezionare una risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="409c5-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="409c5-124">Dopo aver selezionato la risorsa di archiviazione, è necessario specificare quali dati raccogliere.</span><span class="sxs-lookup"><span data-stu-id="409c5-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="409c5-125">Le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="409c5-125">Options available include:</span></span>

- <span data-ttu-id="409c5-126">**[Metriche 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**: contiene percentuale DTU, limite DTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP</span><span class="sxs-lookup"><span data-stu-id="409c5-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="409c5-127">Se si specifica l'hub eventi o un account di archiviazione di Azure, è possibile indicare un criterio di conservazione per specificare che vengano eliminati i dati che superano un periodo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="409c5-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="409c5-128">Se si specifica Log Analytics, i criteri di conservazione dipendono dal piano tariffario selezionato.</span><span class="sxs-lookup"><span data-stu-id="409c5-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="409c5-129">Per altre informazioni, vedere [Prezzi di Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="409c5-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="409c5-130">È consigliabile leggere fino in fondo gli articoli [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) per comprendere non solo come abilitare la registrazione, ma anche le metriche e le categorie di log supportate dai vari servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="409c5-131">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-131">Azure portal</span></span>

<span data-ttu-id="409c5-132">Per abilitare le metriche e la raccolta di log di diagnostica nel portale di Azure, passare alla pagina del pool elastico o del database SQL di Azure e fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="409c5-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Abilitazione nel portale di Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="409c5-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="409c5-134">PowerShell</span></span>

<span data-ttu-id="409c5-135">Per abilitare le metriche e la registrazione diagnostica tramite PowerShell, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="409c5-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="409c5-136">Per abilitare la memorizzazione dei log di diagnostica in un account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="409c5-137">L'ID account di archiviazione è l'ID risorsa per l'account di archiviazione a cui devono essere inviati i log.</span><span class="sxs-lookup"><span data-stu-id="409c5-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="409c5-138">Per abilitare la trasmissione dei log di diagnostica a un hub eventi, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="409c5-139">L'ID regola del bus di servizio è una stringa nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="409c5-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="409c5-140">Per consentire l'invio dei log di diagnostica all'area di lavoro di Log Analytics , usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="409c5-141">È possibile ottenere l'ID risorsa dell'area di lavoro di Log Analytics usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="409c5-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="409c5-142">È possibile combinare questi parametri per abilitare più opzioni di output.</span><span class="sxs-lookup"><span data-stu-id="409c5-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="409c5-143">CLI</span><span class="sxs-lookup"><span data-stu-id="409c5-143">CLI</span></span>

<span data-ttu-id="409c5-144">Per abilitare le metriche e la registrazione diagnostica tramite l'interfaccia della riga di comando di Azure, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="409c5-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="409c5-145">Per abilitare la memorizzazione dei log di diagnostica in un account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="409c5-146">L'ID account di archiviazione è l'ID risorsa per l'account di archiviazione a cui devono essere inviati i log.</span><span class="sxs-lookup"><span data-stu-id="409c5-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="409c5-147">Per abilitare la trasmissione dei log di diagnostica a un hub eventi, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="409c5-148">L'ID regola del bus di servizio è una stringa nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="409c5-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="409c5-149">Per consentire l'invio dei log di diagnostica all'area di lavoro di Log Analytics , usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="409c5-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="409c5-150">È possibile combinare questi parametri per abilitare più opzioni di output.</span><span class="sxs-lookup"><span data-stu-id="409c5-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="409c5-151">API REST</span><span class="sxs-lookup"><span data-stu-id="409c5-151">REST API</span></span>

<span data-ttu-id="409c5-152">Informazioni su come [modificare le impostazioni di diagnostica usando l'API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="409c5-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="409c5-153">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="409c5-153">Resource Manager template</span></span>

<span data-ttu-id="409c5-154">Informazioni su come [abilitare automaticamente le impostazioni di diagnostica durante la creazione di risorse con un modello di Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="409c5-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="409c5-155">Eseguire lo streaming in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="409c5-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="409c5-156">Le metriche del database SQL Azure e i log di diagnostica possono essere trasmessi in Log Analytics usando l'opzione "Invia a Log Analytics" presente nel portale oppure abilitando Log Analytics in un'impostazione di diagnostica tramite cmdlet di PowerShell di Azure, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="409c5-157">Panoramica dell'installazione</span><span class="sxs-lookup"><span data-stu-id="409c5-157">Installation overview</span></span>

<span data-ttu-id="409c5-158">Monitorare la flotta del database SQL di Azure è semplice con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="409c5-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="409c5-159">Sono necessari tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="409c5-159">Three steps are required:</span></span>

1.  <span data-ttu-id="409c5-160">Creare la risorsa Log Analytics</span><span class="sxs-lookup"><span data-stu-id="409c5-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="409c5-161">Configurare i database per registrare le metriche e i log di diagnostica nella risorsa Log Analytics creata</span><span class="sxs-lookup"><span data-stu-id="409c5-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="409c5-162">Installare la soluzione **Analisi SQL di Azure** dalla raccolta in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="409c5-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="409c5-163">Creare la risorsa Log Analytics</span><span class="sxs-lookup"><span data-stu-id="409c5-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="409c5-164">Fare clic su **Nuovo** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="409c5-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="409c5-165">Fare clic su **Monitoraggio e gestione**</span><span class="sxs-lookup"><span data-stu-id="409c5-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="409c5-166">Fare clic su **Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="409c5-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="409c5-167">Compilare il modulo Log Analytics con le informazioni aggiuntive necessarie: nome dell'area di lavoro, sottoscrizione, gruppo di risorse, posizione e livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="409c5-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![log analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="409c5-169">Configurare i database per registrare le metriche e i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="409c5-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="409c5-170">Il modo più semplice per configurare la posizione in cui i database registrano le metriche è tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="409c5-171">Nel portale di Azure passare alla risorsa database SQL di Azure e fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="409c5-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="409c5-172">Installare la soluzione Analisi SQL di Azure dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="409c5-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="409c5-173">Quando la risorsa Log Analytics è stata creata e i dati vengono trasmessi a essa, installare una soluzione Analisi SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="409c5-174">Questa operazione può essere eseguita tramite la **raccolta soluzioni** disponibile nella home page di OMS e nel menu laterale.</span><span class="sxs-lookup"><span data-stu-id="409c5-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="409c5-175">Nella raccolta, trovare e fare clic sulla soluzione **Analisi SQL di Azure** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="409c5-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![soluzione di monitoraggio](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="409c5-177">Nella home page di OMS viene visualizzato un nuovo riquadro chiamato **Analisi SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="409c5-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="409c5-178">Se si seleziona questo riquadro viene aperto il dashboard di Analisi SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="409c5-179">Uso della soluzione Analisi SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="409c5-180">Analisi SQL di Azure è un dashboard gerarchico che consente di spostarsi nella gerarchia di risorse del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="409c5-181">Questa funzionalità consente di eseguire un monitoraggio di alto livello ma consente anche di definire l'ambito del monitoraggio esattamente per il set di risorse corretto.</span><span class="sxs-lookup"><span data-stu-id="409c5-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="409c5-182">Il dashboard contiene gli elenchi delle diverse risorse sotto la risorsa selezionata.</span><span class="sxs-lookup"><span data-stu-id="409c5-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="409c5-183">Ad esempio, per una sottoscrizione selezionata è possibile vedere tutti i server, i pool elastici e i database che appartengono alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="409c5-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="409c5-184">Inoltre, per i pool elastici e i database, è possibile vedere metriche di utilizzo delle risorse per quella risorsa.</span><span class="sxs-lookup"><span data-stu-id="409c5-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="409c5-185">Sono inclusi grafici per DTU, CPU, IO, LOG, sessioni, processi di lavoro, connessioni e archiviazione in GB.</span><span class="sxs-lookup"><span data-stu-id="409c5-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="409c5-186">Eseguire lo streaming nell'hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="409c5-187">Le metriche del database SQL Azure e i log di diagnostica possono essere trasmessi nell'hub eventi usando l'opzione "Stream to an event hub" (Esegui streaming in un Hub eventi) presente nel portale oppure abilitando l'ID regola del bus di servizio in un'impostazione di diagnostica tramite cmdlet di PowerShell di Azure, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="409c5-188">Cosa fare con le metriche e i log di diagnostica nell'hub eventi?</span><span class="sxs-lookup"><span data-stu-id="409c5-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="409c5-189">Una volta eseguito lo streaming dei dati selezionati nell'hub eventi, si è un passo più vicini all'abilitazione di scenari di monitoraggio avanzati.</span><span class="sxs-lookup"><span data-stu-id="409c5-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="409c5-190">Hub eventi funge da "porta principale" per una pipeline di eventi. Dopo aver raccolto i dati in un hub eventi, è possibile trasformarli e archiviarli tramite qualsiasi provider di analisi in tempo reale o adattatore di invio in batch/archiviazione.</span><span class="sxs-lookup"><span data-stu-id="409c5-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="409c5-191">Gli hub di eventi separano la produzione di un flusso di eventi dal consumo di questi eventi, in modo che i consumer di eventi può accedere agli eventi in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="409c5-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="409c5-192">Per altre informazioni sull'hub eventi, vedere:</span><span class="sxs-lookup"><span data-stu-id="409c5-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="409c5-193">[Cosa sono gli hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="409c5-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="409c5-194">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="409c5-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="409c5-195">Ecco alcuni esempi di come è possibile usare la funzionalità di trasmissione:</span><span class="sxs-lookup"><span data-stu-id="409c5-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="409c5-196">Visualizzare lo stato di integrità del servizio mediante la trasmissione di dati sul "percorso critico" a Power BI: hub eventi, analisi di flusso e Power BI permettono di trasformare facilmente i dati di metriche e diagnostica in informazioni quasi in tempo reale sui servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="409c5-197">Per una panoramica della configurazione dell'hub eventi, dell'elaborazione dei dati con analisi di flusso e dell'uso di Power BI come output, vedere [Analisi di flusso e Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="409c5-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="409c5-198">Eseguire lo streaming dei log in stream di registrazione e telemetria di terze parti: usando lo streaming degli hub eventi è possibile trasmettere le metriche e i log di diagnostica a diverse soluzioni di monitoraggio e analisi di log di terze parti.</span><span class="sxs-lookup"><span data-stu-id="409c5-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="409c5-199">Compilare una piattaforma di registrazione e telemetria personalizzata: se è disponibile una piattaforma di telemetria personalizzata o si intende crearne una, le caratteristiche di pubblicazione-sottoscrizione altamente scalabili dell'hub eventi offrono grande flessibilità per l'inserimento dei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="409c5-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="409c5-200">[Vedere la guida all'uso dell'hub eventi in una piattaforma di telemetria su scala globale di Dan Rosanova](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="409c5-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="409c5-201">Eseguire lo streaming in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-201">Stream into Azure Storage</span></span>

<span data-ttu-id="409c5-202">Le metriche del database SQL Azure e i log di diagnostica possono essere archiviati in Archiviazione di Azure usando l'opzione "Archive to a storage account" (Archivia in un account di archiviazione) presente nel portale di Azure oppure abilitando Archiviazione di Azure in un'impostazione di diagnostica tramite cmdlet di PowerShell di Azure, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="409c5-203">Schema delle metriche e dei log di diagnostica nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="409c5-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="409c5-204">Dopo aver configurato la raccolta delle metriche e dei log di diagnostica, viene creato un contenitore di archiviazione nell'account di archiviazione selezionato quando sono disponibili le prime righe di dati.</span><span class="sxs-lookup"><span data-stu-id="409c5-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="409c5-205">La struttura di questi BLOB è:</span><span class="sxs-lookup"><span data-stu-id="409c5-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="409c5-206">O, più semplicemente:</span><span class="sxs-lookup"><span data-stu-id="409c5-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="409c5-207">Ad esempio, un nome del BLOB per la metrica 1 minuto potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="409c5-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="409c5-208">Se si vuole registrare i dati dal pool elastico, il nome del BLOB è leggermente diverso:</span><span class="sxs-lookup"><span data-stu-id="409c5-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="409c5-209">Scaricare le metriche e i log da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="409c5-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="409c5-210">Vedere [Scaricare le metriche e i log di diagnostica da Archiviazione di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="409c5-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="409c5-211">metriche 1 minuto</span><span class="sxs-lookup"><span data-stu-id="409c5-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="409c5-212">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="409c5-212">**Resource**</span></span>|<span data-ttu-id="409c5-213">**Metriche**</span><span class="sxs-lookup"><span data-stu-id="409c5-213">**Metrics**</span></span>|
|<span data-ttu-id="409c5-214">Database</span><span class="sxs-lookup"><span data-stu-id="409c5-214">Database</span></span>|<span data-ttu-id="409c5-215">Percentuale DTU, DTU utilizzata, limite DTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP, deadlock</span><span class="sxs-lookup"><span data-stu-id="409c5-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="409c5-216">Pool elastico</span><span class="sxs-lookup"><span data-stu-id="409c5-216">Elastic pool</span></span>|<span data-ttu-id="409c5-217">Percentuale eDTU, eDTU utilizzata, limite eDTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, limite di archiviazione, percentuale di archiviazione XTP</span><span class="sxs-lookup"><span data-stu-id="409c5-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="409c5-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="409c5-218">Next steps</span></span>

- <span data-ttu-id="409c5-219">Leggere fino in fondo gli articoli [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) per comprendere non solo come abilitare la registrazione, ma anche le metriche e le categorie di log supportate dai vari servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="409c5-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="409c5-220">Per informazioni sugli hub eventi, leggere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="409c5-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="409c5-221">[Cosa sono gli hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="409c5-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="409c5-222">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="409c5-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="409c5-223">Vedere [Scaricare le metriche e i log di diagnostica da Archiviazione di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="409c5-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
