---
title: soluzione di rete Analitica in Log Analitica aaaAzure | Documenti Microsoft
description: "È possibile utilizzare hello soluzione Analitica di rete di Azure nei registri del gruppo protezione rete di Azure tooreview Analitica di Log e nei registri di Gateway applicazione Azure."
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
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="0c0f1-103">Soluzioni di monitoraggio di rete di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0c0f1-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="0c0f1-104">Log Analitica offre hello seguenti soluzioni per il monitoraggio delle reti:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="0c0f1-105">Monitoraggio delle prestazioni di rete per</span><span class="sxs-lookup"><span data-stu-id="0c0f1-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="0c0f1-106">Monitoraggio integrità hello della rete</span><span class="sxs-lookup"><span data-stu-id="0c0f1-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="0c0f1-107">Azure tooreview analitica di Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="0c0f1-108">Log di gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="0c0f1-109">Metriche di gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="0c0f1-110">Gruppo di sicurezza di rete di Azure analitica tooreview</span><span class="sxs-lookup"><span data-stu-id="0c0f1-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="0c0f1-111">Log dei gruppi di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="0c0f1-112">Monitoraggio delle prestazioni di rete</span><span class="sxs-lookup"><span data-stu-id="0c0f1-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="0c0f1-113">Hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) soluzione di gestione è una soluzione, che controlla integrità hello, disponibilità e raggiungibilità di reti di monitoraggio di rete.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="0c0f1-114">È utilizzato toomonitor connettività tra:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="0c0f1-115">Cloud pubblico e risorse locali</span><span class="sxs-lookup"><span data-stu-id="0c0f1-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="0c0f1-116">Data center e percorsi utente (succursali)</span><span class="sxs-lookup"><span data-stu-id="0c0f1-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="0c0f1-117">Subnet che ospitano vari livelli di un'applicazione multilivello.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="0c0f1-118">Per altre informazioni, vedere [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="0c0f1-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="0c0f1-119">Azure Application Gateway Analytics e Azure Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="0c0f1-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="0c0f1-120">soluzioni di hello toouse:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="0c0f1-121">Aggiungere tooLog soluzione di gestione hello Analitica, e</span><span class="sxs-lookup"><span data-stu-id="0c0f1-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="0c0f1-122">Abilitare la diagnostica toodirect hello diagnostica tooa Log Analitica dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="0c0f1-123">Non è necessario toowrite nell'archiviazione Blob tooAzure hello registri.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="0c0f1-124">È possibile abilitare la diagnostica e la soluzione corrispondente hello per uno o entrambi i gruppi di sicurezza di rete e di Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="0c0f1-125">Se non si abilita la registrazione diagnostica per un determinato tipo di risorsa, ma installare la soluzione hello, pannelli di dashboard hello per tale risorsa sono vuoti e visualizzare un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="0c0f1-126">Nel gennaio January 2017, hello supportate consentono di inviare i log da gruppi di sicurezza di rete e di gateway applicazione tooLog che Analitica modificato.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="0c0f1-127">Se viene visualizzato hello **Analitica di rete di Azure (deprecato)** soluzioni, fare riferimento troppo[la migrazione da una soluzione Analitica rete precedente hello](#migrating-from-the-old-networking-analytics-solution) per la procedura è necessario toofollow.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="0c0f1-128">Esaminare i dettagli della raccolta di dati di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="0c0f1-129">analitica di Gateway applicazione Azure Hello hello Network Security Group analitica soluzioni di gestione e raccolta i registri di diagnostica direttamente dal gateway applicazione Azure e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="0c0f1-130">Non è necessario toowrite hello registri tooAzure nell'archiviazione Blob e non è richiesto per la raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="0c0f1-131">Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per analitica di Gateway applicazione Azure e analitica Network Security Group hello.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="0c0f1-132">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="0c0f1-132">Platform</span></span> | <span data-ttu-id="0c0f1-133">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="0c0f1-133">Direct agent</span></span> | <span data-ttu-id="0c0f1-134">Agente di Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="0c0f1-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="0c0f1-135">Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-135">Azure</span></span> | <span data-ttu-id="0c0f1-136">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="0c0f1-136">Operations Manager required?</span></span> | <span data-ttu-id="0c0f1-137">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="0c0f1-138">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="0c0f1-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0c0f1-139">Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-139">Azure</span></span> |  |  |<span data-ttu-id="0c0f1-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="0c0f1-140">&#8226;</span></span> |  |  |<span data-ttu-id="0c0f1-141">Quando connesso</span><span class="sxs-lookup"><span data-stu-id="0c0f1-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="0c0f1-142">Soluzione di analisi del gateway applicazione di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0c0f1-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Simbolo di Analisi gateway applicazione di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="0c0f1-144">Hello seguendo i registri è supportato per i gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="0c0f1-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="0c0f1-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="0c0f1-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="0c0f1-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="0c0f1-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="0c0f1-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="0c0f1-148">Hello seguenti metriche è supportato per i gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="0c0f1-149">Velocità effettiva di 5 minuti</span><span class="sxs-lookup"><span data-stu-id="0c0f1-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="0c0f1-150">Installare e configurare la soluzione hello</span><span class="sxs-lookup"><span data-stu-id="0c0f1-150">Install and configure hello solution</span></span>
<span data-ttu-id="0c0f1-151">Utilizzare hello seguendo le istruzioni tooinstall e configurare la soluzione analitica di Gateway applicazione Azure hello:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="0c0f1-152">Abilitare una soluzione analitica di Gateway applicazione Azure hello da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0c0f1-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="0c0f1-153">Abilitare la registrazione diagnostica per hello [gateway applicazione](../application-gateway/application-gateway-diagnostics.md) desiderato toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="0c0f1-154">Abilitare la diagnostica di Gateway applicazione Azure nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="0c0f1-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="0c0f1-155">Nel portale di Azure hello, passare toohello Gateway applicazione risorse toomonitor</span><span class="sxs-lookup"><span data-stu-id="0c0f1-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="0c0f1-156">Selezionare *log di diagnostica* hello tooopen dopo</span><span class="sxs-lookup"><span data-stu-id="0c0f1-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="0c0f1-158">Fare clic su *attivare la diagnostica* hello tooopen dopo</span><span class="sxs-lookup"><span data-stu-id="0c0f1-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="0c0f1-160">tooturn sulla diagnostica, fare clic su *su* in *stato*</span><span class="sxs-lookup"><span data-stu-id="0c0f1-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="0c0f1-161">Fare clic sulla casella di controllo hello *inviare tooLog Analitica*</span><span class="sxs-lookup"><span data-stu-id="0c0f1-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="0c0f1-162">Selezionare un'area di lavoro Log Analytics esistente o creare una</span><span class="sxs-lookup"><span data-stu-id="0c0f1-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="0c0f1-163">Fare clic sulla casella di controllo di hello in **Log** per ognuna delle hello log tipi toocollect</span><span class="sxs-lookup"><span data-stu-id="0c0f1-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="0c0f1-164">Fare clic su *salvare* registrazione hello tooenable di diagnostica tooLog Analitica</span><span class="sxs-lookup"><span data-stu-id="0c0f1-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="0c0f1-165">Abilitare la diagnostica di rete di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c0f1-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="0c0f1-166">Hello lo script di PowerShell seguente viene fornito un esempio di come tooenable registrazione diagnostica per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="0c0f1-167">Usare l'analisi dei gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-167">Use Azure Application Gateway analytics</span></span>
![Immagine del riquadro di analisi dei gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="0c0f1-169">Dopo aver fatto clic hello **analitica di Gateway applicazione Azure** riquadro su hello panoramica, è possibile visualizzare i riepiloghi dei registri e quindi eseguire il drill-toodetails per hello seguenti categorie:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="0c0f1-170">Log di accesso del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="0c0f1-171">Errori di client e server per i log di accesso del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="0c0f1-172">Richieste all'ora per ogni gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="0c0f1-173">Richieste non riuscite all'ora per ogni gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="0c0f1-174">Errori per agente utente per gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="0c0f1-175">Prestazioni del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-175">Application Gateway performance</span></span>
  * <span data-ttu-id="0c0f1-176">Integrità dell'host per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="0c0f1-177">Valore massimo e 95° percentile per le richieste non riuscite del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="0c0f1-180">In hello **analitica di Gateway applicazione Azure** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli hello e quindi fare clic su uno tooview informazioni dettagliate sulla pagina ricerca nei log hello.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="0c0f1-181">In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="0c0f1-182">È inoltre possibile filtrare dai risultati di hello toonarrow facet.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="0c0f1-183">Soluzione di analisi del gruppo di sicurezza di rete di Azure in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0c0f1-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Simbolo di Analisi gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="0c0f1-185">Hello seguendo i registri è supportato per i gruppi di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="0c0f1-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="0c0f1-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="0c0f1-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="0c0f1-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="0c0f1-188">Installare e configurare la soluzione hello</span><span class="sxs-lookup"><span data-stu-id="0c0f1-188">Install and configure hello solution</span></span>
<span data-ttu-id="0c0f1-189">Utilizzare hello seguendo le istruzioni tooinstall e configurare la soluzione di hello Analitica di rete di Azure:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="0c0f1-190">Abilitare la soluzione analitica di gruppo di sicurezza di rete di Azure hello da [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0c0f1-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="0c0f1-191">Abilitare la registrazione diagnostica per hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) risorse desiderate toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="0c0f1-192">Abilitare la diagnostica di gruppo di sicurezza di rete di Azure nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="0c0f1-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="0c0f1-193">Nel portale di Azure hello, passare toohello Network Security Group risorse toomonitor</span><span class="sxs-lookup"><span data-stu-id="0c0f1-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="0c0f1-194">Selezionare *log di diagnostica* hello tooopen dopo</span><span class="sxs-lookup"><span data-stu-id="0c0f1-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="0c0f1-196">Fare clic su *attivare la diagnostica* hello tooopen dopo</span><span class="sxs-lookup"><span data-stu-id="0c0f1-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="0c0f1-198">tooturn sulla diagnostica, fare clic su *su* in *stato*</span><span class="sxs-lookup"><span data-stu-id="0c0f1-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="0c0f1-199">Fare clic sulla casella di controllo hello *inviare tooLog Analitica*</span><span class="sxs-lookup"><span data-stu-id="0c0f1-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="0c0f1-200">Selezionare un'area di lavoro Log Analytics esistente o creare una</span><span class="sxs-lookup"><span data-stu-id="0c0f1-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="0c0f1-201">Fare clic sulla casella di controllo di hello in **Log** per ognuna delle hello log tipi toocollect</span><span class="sxs-lookup"><span data-stu-id="0c0f1-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="0c0f1-202">Fare clic su *salvare* registrazione hello tooenable di diagnostica tooLog Analitica</span><span class="sxs-lookup"><span data-stu-id="0c0f1-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="0c0f1-203">Abilitare la diagnostica di rete di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c0f1-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="0c0f1-204">Hello lo script di PowerShell seguente viene fornito un esempio di come tooenable registrazione diagnostica per i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0c0f1-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="0c0f1-205">Usare l'analisi del gruppo di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="0c0f1-206">Dopo aver fatto clic hello **analitica gruppo di sicurezza di rete di Azure** riquadro su hello panoramica, è possibile visualizzare i riepiloghi dei registri e quindi eseguire il drill-toodetails per hello seguenti categorie:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="0c0f1-207">Flussi bloccati dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0c0f1-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="0c0f1-208">Regole dei gruppi di sicurezza di rete con flussi bloccati</span><span class="sxs-lookup"><span data-stu-id="0c0f1-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="0c0f1-209">Indirizzi MAC con flussi bloccati</span><span class="sxs-lookup"><span data-stu-id="0c0f1-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="0c0f1-210">Flussi consentiti dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0c0f1-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="0c0f1-211">Regole dei gruppi di sicurezza di rete con flussi consentiti</span><span class="sxs-lookup"><span data-stu-id="0c0f1-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="0c0f1-212">Indirizzi MAC con flussi consentiti</span><span class="sxs-lookup"><span data-stu-id="0c0f1-212">MAC addresses with allowed flows</span></span>

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="0c0f1-215">In hello **analitica gruppo di sicurezza di rete di Azure** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli hello e quindi fare clic su uno tooview informazioni dettagliate sulla pagina ricerca nei log hello.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="0c0f1-216">In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="0c0f1-217">È inoltre possibile filtrare dai risultati di hello toonarrow facet.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="0c0f1-218">La migrazione da una soluzione Analitica rete precedente hello</span><span class="sxs-lookup"><span data-stu-id="0c0f1-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="0c0f1-219">Nel gennaio January 2017, hello supportate consentono di inviare i log dal gateway applicazione Azure e i gruppi di sicurezza di rete di Azure tooLog che Analitica modificato.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="0c0f1-220">Queste modifiche consentono hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="0c0f1-221">I log vengono scritti direttamente tooLog Analitica senza hello necessario toouse un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="0c0f1-222">Minore latenza dall'ora di hello quando i registri sono generati toothem disponibile nel Log Analitica</span><span class="sxs-lookup"><span data-stu-id="0c0f1-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="0c0f1-223">Meno passaggi di configurazione</span><span class="sxs-lookup"><span data-stu-id="0c0f1-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="0c0f1-224">Un formato comune per tutti i tipi di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="0c0f1-225">hello toouse aggiornata soluzioni:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="0c0f1-226">Configurare diagnostica toobe inviato direttamente tooLog Analitica da gateway per applicazioni Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="0c0f1-227">Configurare diagnostica toobe inviato tooLog Analitica direttamente dai gruppi di sicurezza di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f1-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="0c0f1-228">Abilitare hello *Analitica di Gateway applicazione Azure* hello e *Analitica di gruppo di sicurezza di Azure rete* soluzione tramite hello processo descritto in [soluzioni aggiungere Log Analitica da Hello Solutions Gallery](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="0c0f1-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="0c0f1-229">Aggiornare le query salvate, dashboard o avvisi toouse hello nuovo tipo di dati</span><span class="sxs-lookup"><span data-stu-id="0c0f1-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="0c0f1-230">Il tipo è tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="0c0f1-231">È possibile utilizzare i log di rete hello ResourceType toofilter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="0c0f1-232">Invece di:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-232">Instead of:</span></span> | <span data-ttu-id="0c0f1-233">Usare:</span><span class="sxs-lookup"><span data-stu-id="0c0f1-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="0c0f1-234">Per qualsiasi campo che contiene un suffisso di \_s, \_d, o \_g in nome hello cambia hello primo carattere toolower maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="0c0f1-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="0c0f1-235">Per qualsiasi campo che contiene un suffisso di \_o nel nome, i dati di hello è suddiviso in singoli campi in base ai nomi di campo hello annidato.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="0c0f1-236">Rimuovere hello *Analitica di rete di Azure (obsoleto)* soluzione.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="0c0f1-237">Se si utilizza PowerShell, usare `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="0c0f1-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="0c0f1-238">I dati raccolti prima modifica hello non è visibile nella nuova soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="0c0f1-239">È possibile continuare tooquery per questa operazione utilizzando dati hello vecchio tipo e i nomi dei campi.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0c0f1-240">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="0c0f1-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="0c0f1-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c0f1-241">Next steps</span></span>
* <span data-ttu-id="0c0f1-242">Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0f1-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
