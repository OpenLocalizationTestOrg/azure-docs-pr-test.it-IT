---
title: Soluzione Azure Networking Analytics in Log Analytics | Microsoft Docs
description: "È possibile usare la soluzione Azure Networking Analytics in Log Analytics per esaminare i log dei gruppi di sicurezza di rete di Azure e i log dei gateway applicazione di Azure Application Gateway."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="f5881-103">Soluzioni di monitoraggio di rete di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="f5881-104">Log Analytics offre le seguenti soluzioni per il monitoraggio delle reti:</span><span class="sxs-lookup"><span data-stu-id="f5881-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="f5881-105">Monitoraggio delle prestazioni di rete per</span><span class="sxs-lookup"><span data-stu-id="f5881-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="f5881-106">Verificare l'integrità della rete</span><span class="sxs-lookup"><span data-stu-id="f5881-106">Monitor the health of your network</span></span>
* <span data-ttu-id="f5881-107">Azure Application Gateway Analytics per analizzare</span><span class="sxs-lookup"><span data-stu-id="f5881-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="f5881-108">Log di gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="f5881-109">Metriche di gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="f5881-110">Azure Network Security Group Analytics per analizzare</span><span class="sxs-lookup"><span data-stu-id="f5881-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="f5881-111">Log dei gruppi di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="f5881-112">Monitoraggio delle prestazioni di rete</span><span class="sxs-lookup"><span data-stu-id="f5881-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="f5881-113">La soluzione di gestione [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md) consente di monitorare l'integrità, la disponibilità e la raggiungibilità delle reti.</span><span class="sxs-lookup"><span data-stu-id="f5881-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="f5881-114">Viene usata per monitorare la connettività tra:</span><span class="sxs-lookup"><span data-stu-id="f5881-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="f5881-115">Cloud pubblico e risorse locali</span><span class="sxs-lookup"><span data-stu-id="f5881-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="f5881-116">Data center e percorsi utente (succursali)</span><span class="sxs-lookup"><span data-stu-id="f5881-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="f5881-117">Subnet che ospitano vari livelli di un'applicazione multilivello.</span><span class="sxs-lookup"><span data-stu-id="f5881-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="f5881-118">Per altre informazioni, vedere [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="f5881-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="f5881-119">Azure Application Gateway Analytics e Azure Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="f5881-120">Per usare le soluzioni:</span><span class="sxs-lookup"><span data-stu-id="f5881-120">To use the solutions:</span></span>
1. <span data-ttu-id="f5881-121">Aggiungere la soluzione di gestione a Log Analytics e</span><span class="sxs-lookup"><span data-stu-id="f5881-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="f5881-122">Abilitare la funzionalità diagnostica per indirizzare la diagnostica a un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5881-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="f5881-123">Non è necessario inserire i log nell'Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5881-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="f5881-124">È possibile abilitare la diagnostica e la soluzione corrispondente per uno o per entrambe le soluzioni: gateway applicazione e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="f5881-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="f5881-125">Se non si abilita la registrazione diagnostica per un tipo specifico di risorsa ma si installa la soluzione, i pannelli del dashboard per quella risorsa sono vuoti e visualizzano un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="f5881-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="f5881-126">A gennaio 2017 è stato modificato il metodo supportato per inviare i log dai gateway applicazione e dai gruppi di sicurezza di rete a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5881-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="f5881-127">Se viene visualizzata la soluzione **Azure Networking Analytics (deprecata)**, fare riferimento ai passaggi di [migrazione dalla vecchia soluzione Networking Analytics](#migrating-from-the-old-networking-analytics-solution) per istruzioni su come procedere.</span><span class="sxs-lookup"><span data-stu-id="f5881-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="f5881-128">Esaminare i dettagli della raccolta di dati di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="f5881-129">Le soluzioni di gestione delle analisi del gateway applicazione e del gruppo di sicurezza di rete di Azure raccolgono i log di diagnostica direttamente dalle due risorse appena citate.</span><span class="sxs-lookup"><span data-stu-id="f5881-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="f5881-130">Non è necessario inserire i log in Archiviazione BLOB di Azure né è necessario alcun agente per la raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="f5881-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="f5881-131">La tabella seguente illustra i metodi di raccolta dei dati e altri dettagli sulla modalità di raccolta dei dati per l'analisi del gateway applicazione e il gruppo di sicurezza di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5881-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="f5881-132">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="f5881-132">Platform</span></span> | <span data-ttu-id="f5881-133">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="f5881-133">Direct agent</span></span> | <span data-ttu-id="f5881-134">Agente di Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f5881-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="f5881-135">Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-135">Azure</span></span> | <span data-ttu-id="f5881-136">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="f5881-136">Operations Manager required?</span></span> | <span data-ttu-id="f5881-137">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="f5881-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="f5881-138">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="f5881-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f5881-139">Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-139">Azure</span></span> |  |  |<span data-ttu-id="f5881-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="f5881-140">&#8226;</span></span> |  |  |<span data-ttu-id="f5881-141">Quando connesso</span><span class="sxs-lookup"><span data-stu-id="f5881-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="f5881-142">Soluzione di analisi del gateway applicazione di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Simbolo di Analisi gateway applicazione di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="f5881-144">I log seguenti sono supportati per i gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="f5881-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="f5881-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="f5881-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="f5881-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="f5881-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="f5881-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="f5881-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="f5881-148">Le metriche seguenti sono supportate per i gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="f5881-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="f5881-149">Velocità effettiva di 5 minuti</span><span class="sxs-lookup"><span data-stu-id="f5881-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="f5881-150">Installare e configurare la soluzione</span><span class="sxs-lookup"><span data-stu-id="f5881-150">Install and configure the solution</span></span>
<span data-ttu-id="f5881-151">Usare le istruzioni seguenti per installare e configurare la soluzione di analisi del gateway applicazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="f5881-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="f5881-152">Abilitare la soluzione Azure Application Gateway Analytics da [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="f5881-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="f5881-153">Abilitare la registrazione diagnostica per i [gateway applicazione](../application-gateway/application-gateway-diagnostics.md) da monitorare.</span><span class="sxs-lookup"><span data-stu-id="f5881-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="f5881-154">Abilitare la diagnostica del gateway applicazione di Azure nel portale</span><span class="sxs-lookup"><span data-stu-id="f5881-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="f5881-155">Nel portale di Azure passare alla risorsa gateway applicazione da monitorare</span><span class="sxs-lookup"><span data-stu-id="f5881-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="f5881-156">Selezionare *Log di diagnostica* per aprire la pagina seguente</span><span class="sxs-lookup"><span data-stu-id="f5881-156">Select *Diagnostics logs* to open the following page</span></span>

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="f5881-158">Fare clic su *Attiva diagnostica* per aprire la pagina seguente</span><span class="sxs-lookup"><span data-stu-id="f5881-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="f5881-160">Per attivare la diagnostica, fare clic su *Attivato* in *Stato*</span><span class="sxs-lookup"><span data-stu-id="f5881-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="f5881-161">Selezionare la casella di controllo *Send to Log Analytics* (Invia a Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="f5881-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="f5881-162">Selezionare un'area di lavoro Log Analytics esistente o crearne una</span><span class="sxs-lookup"><span data-stu-id="f5881-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="f5881-163">Selezionare la casella di controllo in **Log** per ciascuno dei tipi di log da raccogliere</span><span class="sxs-lookup"><span data-stu-id="f5881-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="f5881-164">Fare clic su *Salva* per abilitare la registrazione della diagnostica per Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="f5881-165">Abilitare la diagnostica di rete di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5881-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="f5881-166">Lo script PowerShell seguente contiene un esempio su come abilitare la registrazione diagnostica per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5881-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="f5881-167">Usare l'analisi dei gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-167">Use Azure Application Gateway analytics</span></span>
![Immagine del riquadro di analisi dei gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="f5881-169">Dopo aver selezionato il riquadro **di analisi del gateway applicazione di Azure** nella panoramica, è possibile visualizzare i riepiloghi dei log e quindi analizzare i dettagli per le categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5881-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="f5881-170">Log di accesso del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="f5881-171">Errori di client e server per i log di accesso del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="f5881-172">Richieste all'ora per ogni gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="f5881-173">Richieste non riuscite all'ora per ogni gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="f5881-174">Errori per agente utente per gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="f5881-175">Prestazioni del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-175">Application Gateway performance</span></span>
  * <span data-ttu-id="f5881-176">Integrità dell'host per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="f5881-177">Valore massimo e 95° percentile per le richieste non riuscite del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f5881-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="f5881-180">Nel dashboard **di analisi del gateway applicazione di Azure** esaminare le informazioni di riepilogo in uno dei pannelli, quindi fare clic su un pannello per visualizzare le informazioni dettagliate nella pagina di ricerca di log.</span><span class="sxs-lookup"><span data-stu-id="f5881-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="f5881-181">In una pagina di ricerca di log qualsiasi è possibile visualizzare i risultati in base all'ora, ai dettagli e alla cronologia di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f5881-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="f5881-182">È anche possibile filtrare per facet in modo da limitare i risultati.</span><span class="sxs-lookup"><span data-stu-id="f5881-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="f5881-183">Soluzione di analisi del gruppo di sicurezza di rete di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Simbolo di Analisi gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="f5881-185">I log seguenti sono supportati per i gruppi di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="f5881-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="f5881-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="f5881-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="f5881-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="f5881-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="f5881-188">Installare e configurare la soluzione</span><span class="sxs-lookup"><span data-stu-id="f5881-188">Install and configure the solution</span></span>
<span data-ttu-id="f5881-189">Usare le istruzioni seguenti per installare e configurare la soluzione Azure Networking Analytics di Azure:</span><span class="sxs-lookup"><span data-stu-id="f5881-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="f5881-190">Abilitare la soluzione Azure Network Security Group Analytics da [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="f5881-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="f5881-191">Abilitare la registrazione diagnostica per le risorse [gruppo di sicurezza di rete](../virtual-network/virtual-network-nsg-manage-log.md) da monitorare.</span><span class="sxs-lookup"><span data-stu-id="f5881-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="f5881-192">Abilitare la diagnostica del gruppo di sicurezza di rete di Azure nel portale</span><span class="sxs-lookup"><span data-stu-id="f5881-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="f5881-193">Nel portale di Azure passare alla risorsa gruppo di sicurezza di rete da monitorare</span><span class="sxs-lookup"><span data-stu-id="f5881-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="f5881-194">Selezionare *Log di diagnostica* per aprire la pagina seguente</span><span class="sxs-lookup"><span data-stu-id="f5881-194">Select *Diagnostics logs* to open the following page</span></span>

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="f5881-196">Fare clic su *Attiva diagnostica* per aprire la pagina seguente</span><span class="sxs-lookup"><span data-stu-id="f5881-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="f5881-198">Per attivare la diagnostica, fare clic su *Attivato* in *Stato*</span><span class="sxs-lookup"><span data-stu-id="f5881-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="f5881-199">Selezionare la casella di controllo *Send to Log Analytics* (Invia a Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="f5881-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="f5881-200">Selezionare un'area di lavoro Log Analytics esistente o crearne una</span><span class="sxs-lookup"><span data-stu-id="f5881-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="f5881-201">Selezionare la casella di controllo in **Log** per ciascuno dei tipi di log da raccogliere</span><span class="sxs-lookup"><span data-stu-id="f5881-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="f5881-202">Fare clic su *Salva* per abilitare la registrazione della diagnostica per Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="f5881-203">Abilitare la diagnostica di rete di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5881-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="f5881-204">Lo script PowerShell seguente contiene un esempio su come abilitare la registrazione diagnostica per i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="f5881-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="f5881-205">Usare l'analisi del gruppo di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="f5881-206">Dopo aver selezionato il riquadro **di analisi del gruppo di sicurezza di rete di Azure** nella panoramica, è possibile visualizzare i riepiloghi dei log e quindi analizzare i dettagli per le categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5881-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="f5881-207">Flussi bloccati dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="f5881-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="f5881-208">Regole dei gruppi di sicurezza di rete con flussi bloccati</span><span class="sxs-lookup"><span data-stu-id="f5881-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="f5881-209">Indirizzi MAC con flussi bloccati</span><span class="sxs-lookup"><span data-stu-id="f5881-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="f5881-210">Flussi consentiti dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="f5881-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="f5881-211">Regole dei gruppi di sicurezza di rete con flussi consentiti</span><span class="sxs-lookup"><span data-stu-id="f5881-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="f5881-212">Indirizzi MAC con flussi consentiti</span><span class="sxs-lookup"><span data-stu-id="f5881-212">MAC addresses with allowed flows</span></span>

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="f5881-215">Nel dashboard **di analisi del gruppo di sicurezza di rete di Azure** esaminare le informazioni di riepilogo in uno dei pannelli, quindi fare clic su un pannello per visualizzare le informazioni dettagliate nella pagina di ricerca di log.</span><span class="sxs-lookup"><span data-stu-id="f5881-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="f5881-216">In una pagina di ricerca di log qualsiasi è possibile visualizzare i risultati in base all'ora, ai dettagli e alla cronologia di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f5881-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="f5881-217">È anche possibile filtrare per facet in modo da limitare i risultati.</span><span class="sxs-lookup"><span data-stu-id="f5881-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="f5881-218">Migrazione dalla vecchia soluzione Networking Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="f5881-219">A gennaio 2017 è stato modificato il metodo supportato per inviare i log dai gateway applicazione e dai gruppi di sicurezza di rete di Azure a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5881-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="f5881-220">In questo modo si otterranno i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5881-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="f5881-221">I log vengono scritti direttamente in Log Analytics senza la necessità di utilizzare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f5881-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="f5881-222">Minore latenza dal momento in cui i log vengono generati essendo immediatamente disponibili in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f5881-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="f5881-223">Meno passaggi di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5881-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="f5881-224">Un formato comune per tutti i tipi di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="f5881-225">Per usare le soluzioni aggiornate:</span><span class="sxs-lookup"><span data-stu-id="f5881-225">To use the updated solutions:</span></span>

1. [<span data-ttu-id="f5881-226">Configurare la diagnostica in modo che venga inviata direttamente a Log Analytics dai gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-226">Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="f5881-227">Configurare la diagnostica in modo che venga inviata direttamente a Log Analytics dai gruppi di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="f5881-227">Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="f5881-228">Abilitare la *soluzione di analisi del gateway applicazione* e del *gruppo di sicurezza di rete di Azure* seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="f5881-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="f5881-229">Aggiornare tutte le query salvate, i dashboard o gli avvisi per utilizzare il nuovo tipo di dati</span><span class="sxs-lookup"><span data-stu-id="f5881-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="f5881-230">Il tipo è AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="f5881-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="f5881-231">È possibile usare ResourceType per filtrare i log di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5881-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="f5881-232">Invece di:</span><span class="sxs-lookup"><span data-stu-id="f5881-232">Instead of:</span></span> | <span data-ttu-id="f5881-233">Usare:</span><span class="sxs-lookup"><span data-stu-id="f5881-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="f5881-234">Per ogni campo con suffisso di \_s, \_d o \_g nel nome, modificare il primo carattere in lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="f5881-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="f5881-235">Per ogni campo con suffisso di \_o nel nome, i dati sono suddivisi in singoli campi in base ai nomi dei campi nidificati.</span><span class="sxs-lookup"><span data-stu-id="f5881-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="f5881-236">Rimuovere la soluzione *Azure Networking Analytics (deprecata)*.</span><span class="sxs-lookup"><span data-stu-id="f5881-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="f5881-237">Se si usa PowerShell, usare `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="f5881-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="f5881-238">I dati raccolti prima della modifica non sono visibili nella nuova soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5881-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="f5881-239">È possibile continuare a eseguire query per questi dati utilizzando i nomi di campo e il tipo vecchi.</span><span class="sxs-lookup"><span data-stu-id="f5881-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f5881-240">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f5881-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="f5881-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5881-241">Next steps</span></span>
* <span data-ttu-id="f5881-242">Usare le [Ricerche nei log in Log Analytics](log-analytics-log-searches.md) per visualizzare i dati dettagliati per la diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5881-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
