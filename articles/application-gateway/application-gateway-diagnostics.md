---
title: "aaaMonitor accedere ai log, registri di prestazioni, integrità back-end e le metriche per il Gateway applicazione | Documenti Microsoft"
description: Informazioni su come tooenable e gestire i registri di accesso e registri di prestazioni per il Gateway applicazione
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="c5040-103">Integrità back-end, log di diagnostica e metriche per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c5040-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="c5040-104">Tramite il Gateway applicazione Azure, è possibile monitorare le risorse in hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="c5040-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="c5040-105">[Integrità di back-end](#back-end-health): Gateway applicazione fornisce l'integrità di hello funzionalità toomonitor hello del server hello hello pool back-end tramite hello portale di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5040-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="c5040-106">È inoltre possibile trovare integrità hello di pool back-end hello tramite i log di diagnostica delle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="c5040-107">[Registri](#diagnostic-logs): i registri consentono per le prestazioni, l'accesso, e altri toobe dati salvati o utilizzati da una risorsa a scopo di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="c5040-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="c5040-108">[Metriche](#metrics): il gateway applicazione include attualmente una sola metrica.</span><span class="sxs-lookup"><span data-stu-id="c5040-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="c5040-109">Questa metrica consente di misurare la velocità effettiva hello del gateway applicazione hello in byte al secondo.</span><span class="sxs-lookup"><span data-stu-id="c5040-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="c5040-110">Integrità back-end</span><span class="sxs-lookup"><span data-stu-id="c5040-110">Back-end health</span></span>

<span data-ttu-id="c5040-111">Gateway applicazione fornisce l'integrità di hello funzionalità toomonitor hello dei singoli membri di pool back-end hello tramite il portale di hello, PowerShell e interfaccia di hello della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="c5040-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="c5040-112">È anche possibile trovare uno stato di integrità aggregato riepilogo del pool back-end tramite i log di diagnostica delle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="c5040-113">rapporto di stato di back-end Hello riflette l'output di hello di istanze di hello Gateway applicazione integrità probe toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c5040-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="c5040-114">Quando l'individuazione tramite probe ha esito positivo e hello nuovamente end possono ricevere il traffico, è considerato integro.</span><span class="sxs-lookup"><span data-stu-id="c5040-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="c5040-115">In caso contrario, viene considerato non integro.</span><span class="sxs-lookup"><span data-stu-id="c5040-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5040-116">Se è presente un gruppo di sicurezza di rete (gruppo) in una subnet del Gateway applicazione, aprire gli intervalli di porte 65503 65534 subnet Gateway applicazione hello per il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c5040-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="c5040-117">Queste porte sono obbligatorie per toowork di API back-end integrità hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="c5040-118">Visualizzare lo stato di back-end tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="c5040-118">View back-end health through hello portal</span></span>

<span data-ttu-id="c5040-119">Nel portale di hello integrità back-end viene fornito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c5040-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="c5040-120">In un gateway applicazione esistente selezionare **Monitoraggio** > **Integrità back-end**.</span><span class="sxs-lookup"><span data-stu-id="c5040-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="c5040-121">Ogni membro nel pool back-end hello è elencato in questa pagina (se si tratta di una scheda di rete, l'IP o FQDN).</span><span class="sxs-lookup"><span data-stu-id="c5040-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="c5040-122">Vengono visualizzati il nome del pool back-end, la porta, il nome delle impostazioni HTTP back-end e lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="c5040-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="c5040-123">I valori validi per lo stato di integrità sono **Integro**, **Danneggiato** e **Sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="c5040-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="c5040-124">Se viene visualizzato lo stato di integrità di back-end di **sconosciuto**, assicurarsi che back-end toohello di accesso non sia bloccata da una regola di gruppo, una route definita dall'utente (UDR) o un DNS nella rete virtuale hello personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c5040-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Integrità back-end][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="c5040-126">Visualizzare l'integrità back-end tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5040-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="c5040-127">Hello codice di PowerShell seguente viene illustrato come tooview integrità di back-end tramite hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5040-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="c5040-128">Visualizzare l'integrità back-end tramite l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c5040-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="c5040-129">Risultati</span><span class="sxs-lookup"><span data-stu-id="c5040-129">Results</span></span>

<span data-ttu-id="c5040-130">Hello frammento di codice seguente viene illustrato un esempio di risposta hello:</span><span class="sxs-lookup"><span data-stu-id="c5040-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="c5040-131"><a name="diagnostic-logging"></a>Registri di diagnostica</span><span class="sxs-lookup"><span data-stu-id="c5040-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="c5040-132">È possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="c5040-133">È possibile accedere alcuni di questi log tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="c5040-134">Tutti i log possono essere estratti dall'archiviazione BLOB di Azure e visualizzati in strumenti differenti, ad esempio [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e Power BI.</span><span class="sxs-lookup"><span data-stu-id="c5040-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="c5040-135">È possibile ulteriori informazioni sui tipi diversi hello dei log da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="c5040-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="c5040-136">**Log attività**: È possibile utilizzare [log attività Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (precedentemente conosciuto come registri e i log di controllo) tooview tutte le operazioni che vengono inviate tooyour sottoscrizione di Azure e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="c5040-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="c5040-137">Le voci di log di attività vengono raccolti per impostazione predefinita, ed è possibile visualizzarli in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5040-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="c5040-138">**Log di accesso**: È possibile utilizzare modelli di accesso questo log tooview Gateway applicazione e analizzare informazioni importanti, inclusi chiamante hello IP, URL richiesto, latenza nella risposta, codice restituito e byte e la disconnessione. Il log di accesso viene raccolto ogni 300 secondi.</span><span class="sxs-lookup"><span data-stu-id="c5040-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="c5040-139">Il log contiene un record per ogni istanza del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="c5040-140">istanza di Gateway applicazione Hello può essere identificato dalla proprietà instanceId hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="c5040-141">**Log delle prestazioni**: È possibile utilizzare questo tooview log delle prestazioni di istanze del Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="c5040-142">Questo log acquisisce le informazioni sulle prestazioni di ogni istanza, inclusi il totale delle richieste servite, la velocità effettiva in byte, il totale delle richieste non riuscite e il numero delle istanze back-end integre e non integre.</span><span class="sxs-lookup"><span data-stu-id="c5040-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="c5040-143">Il log delle prestazioni viene raccolto ogni 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="c5040-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="c5040-144">**Registro firewall**: È possibile utilizzare questo richieste hello tooview di log che vengono registrati tramite la modalità di rilevamento o prevenzione di un gateway di applicazione che viene configurato con firewall applicazione web di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="c5040-145">Sono disponibili solo per le risorse distribuite nel modello di distribuzione Azure Resource Manager hello log.</span><span class="sxs-lookup"><span data-stu-id="c5040-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c5040-146">Non è possibile utilizzare i log per le risorse nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="c5040-147">Per una migliore comprensione dei modelli di hello due, vedere hello [distribuzione classica e gestione di informazioni sulle risorse](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c5040-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="c5040-148">Sono disponibili tre opzioni di archiviazione dei log:</span><span class="sxs-lookup"><span data-stu-id="c5040-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="c5040-149">**Account di archiviazione**: ideali quando i log vengono archiviati per un periodo più lungo ed esaminati quando necessario.</span><span class="sxs-lookup"><span data-stu-id="c5040-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="c5040-150">**Hub eventi**: gli hub eventi sono un'ottima opzione per l'integrazione con altre informazioni di sicurezza e avvisi tooget per le risorse di strumenti di gestione degli eventi (SEIM).</span><span class="sxs-lookup"><span data-stu-id="c5040-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="c5040-151">**Log Analytics**: soluzione adatta al monitoraggio generale in tempo reale dell'applicazione o all'analisi delle tendenze.</span><span class="sxs-lookup"><span data-stu-id="c5040-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="c5040-152">Abilitare la registrazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5040-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="c5040-153">Registrazione attività viene abilitata automaticamente per tutte le risorse di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c5040-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="c5040-154">È necessario abilitare l'accesso e la raccolta dei dati di hello disponibili tramite i registri di prestazioni registrazione toostart.</span><span class="sxs-lookup"><span data-stu-id="c5040-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="c5040-155">tooenable registrazione, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5040-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="c5040-156">Annotare l'ID di risorsa dell'account di archiviazione, dove vengono archiviati i dati di log hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="c5040-157">Questo valore è formato hello: /Subscriptions/<ID\<subscriptionId\>/ResourceGroups /\<nome gruppo di risorse\>/providers/Microsoft.Storage/storageAccounts/\<nomeaccountdiarchiviazione\>.</span><span class="sxs-lookup"><span data-stu-id="c5040-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="c5040-158">È possibile usare qualsiasi account di archiviazione della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c5040-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="c5040-159">Utilizzare queste informazioni hello toofind portale Azure.</span><span class="sxs-lookup"><span data-stu-id="c5040-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portale: ID risorsa dell'account di archiviazione](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="c5040-161">Prendere nota dell'ID risorsa del gateway applicazione per cui è abilitata la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="c5040-162">Questo valore è formato hello: /Subscriptions/<ID\<subscriptionId\>/ResourceGroups /\<nome gruppo di risorse\>/providers/Microsoft.Network/applicationGateways/\<gateway applicazione nome\>.</span><span class="sxs-lookup"><span data-stu-id="c5040-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="c5040-163">È possibile utilizzare toofind portale hello queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="c5040-163">You can use hello portal toofind this information.</span></span>

    ![Portale: ID risorsa del gateway applicazione](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="c5040-165">Abilitare la registrazione diagnostica tramite hello cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c5040-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="c5040-166">I log attività non richiedono un account di archiviazione separato.</span><span class="sxs-lookup"><span data-stu-id="c5040-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="c5040-167">utilizzo di Hello dell'archiviazione per l'accesso e la registrazione delle prestazioni comporta costi di servizio.</span><span class="sxs-lookup"><span data-stu-id="c5040-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="c5040-168">Abilitare la registrazione tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5040-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="c5040-169">Nel portale di Azure hello, trovare la risorsa e fare clic su **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="c5040-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="c5040-170">Per il gateway applicazione sono disponibili tre log:</span><span class="sxs-lookup"><span data-stu-id="c5040-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="c5040-171">Log di accesso</span><span class="sxs-lookup"><span data-stu-id="c5040-171">Access log</span></span>
   * <span data-ttu-id="c5040-172">Log delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c5040-172">Performance log</span></span>
   * <span data-ttu-id="c5040-173">Log del firewall</span><span class="sxs-lookup"><span data-stu-id="c5040-173">Firewall log</span></span>

2. <span data-ttu-id="c5040-174">toostart la raccolta dei dati, fare clic su **attivare la diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="c5040-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Attivare la diagnostica][1]

3. <span data-ttu-id="c5040-176">Hello **le impostazioni di diagnostica** pannello fornisce le impostazioni di hello per hello i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c5040-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="c5040-177">In questo esempio, Log Analitica archivia i registri di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="c5040-178">Fare clic su **configura** in **Log Analitica** tooconfigure l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c5040-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="c5040-179">È anche possibile utilizzare gli hub di eventi e un archivio account toosave hello i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c5040-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Avvio del processo di configurazione hello][2]

4. <span data-ttu-id="c5040-181">Scegliere un'area di lavoro di Operations Management Suite (OMS) oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="c5040-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="c5040-182">Questo esempio usa un'area di lavoro esistente.</span><span class="sxs-lookup"><span data-stu-id="c5040-182">This example uses an existing one.</span></span>

   ![Opzioni per le aree di lavoro OMS][3]

5. <span data-ttu-id="c5040-184">Confermare le impostazioni di hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="c5040-184">Confirm hello settings and click **Save**.</span></span>

   ![Pannello delle impostazioni di diagnostica con le selezioni][4]

### <a name="activity-log"></a><span data-ttu-id="c5040-186">Log attività</span><span class="sxs-lookup"><span data-stu-id="c5040-186">Activity log</span></span>

<span data-ttu-id="c5040-187">Per impostazione predefinita, Azure genera log attività hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="c5040-188">Hello registri vengono mantenuti per 90 giorni nell'archivio di registri eventi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="c5040-189">Altre informazioni su questi registri leggendo hello [visualizzare eventi e log attività](../monitoring-and-diagnostics/insights-debugging-with-events.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c5040-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="c5040-190">Log di accesso</span><span class="sxs-lookup"><span data-stu-id="c5040-190">Access log</span></span>

<span data-ttu-id="c5040-191">log di accesso Hello viene generato solo se è attivato in ogni istanza del Gateway applicazione, come descritto in dettaglio nella hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c5040-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="c5040-192">Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="c5040-193">Ogni accesso del Gateway applicazione viene registrato nel formato JSON, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c5040-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="c5040-194">Valore</span><span class="sxs-lookup"><span data-stu-id="c5040-194">Value</span></span>  |<span data-ttu-id="c5040-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c5040-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="c5040-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="c5040-196">instanceId</span></span>     | <span data-ttu-id="c5040-197">Gateway applicazione istanza richiesta hello servite.</span><span class="sxs-lookup"><span data-stu-id="c5040-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="c5040-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="c5040-198">clientIP</span></span>     | <span data-ttu-id="c5040-199">IP di origine per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="c5040-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="c5040-200">clientPort</span></span>     | <span data-ttu-id="c5040-201">Porta di origine per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="c5040-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="c5040-202">httpMethod</span></span>     | <span data-ttu-id="c5040-203">Metodo HTTP utilizzato dalla richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="c5040-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="c5040-204">requestUri</span></span>     | <span data-ttu-id="c5040-205">URI della richiesta ricevuta hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="c5040-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="c5040-206">RequestQuery</span></span>     | <span data-ttu-id="c5040-207">**Server di routing**: istanza del pool Back-end che è stato inviato una richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="c5040-208">**X-AzureApplicationGateway-LOG-ID**: ID di correlazione utilizzato per la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="c5040-209">Può essere utilizzato tootroubleshoot traffico problemi nei server back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="c5040-210">**STATO SERVER**: codice di risposta HTTP ricevuti dal back-end hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="c5040-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="c5040-211">UserAgent</span></span>     | <span data-ttu-id="c5040-212">Agente utente dall'intestazione della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="c5040-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="c5040-213">httpStatus</span></span>     | <span data-ttu-id="c5040-214">Codice di stato HTTP restituito toohello client di Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="c5040-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="c5040-215">httpVersion</span></span>     | <span data-ttu-id="c5040-216">Versione HTTP della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="c5040-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="c5040-217">receivedBytes</span></span>     | <span data-ttu-id="c5040-218">Dimensione del pacchetto ricevuto, espressa in byte.</span><span class="sxs-lookup"><span data-stu-id="c5040-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="c5040-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="c5040-219">sentBytes</span></span>| <span data-ttu-id="c5040-220">Dimensione del pacchetto inviato, espressa in byte.</span><span class="sxs-lookup"><span data-stu-id="c5040-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="c5040-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="c5040-221">timeTaken</span></span>| <span data-ttu-id="c5040-222">Periodo di tempo (in millisecondi) impiegato per una richiesta toobe elaborati e toobe la risposta inviata.</span><span class="sxs-lookup"><span data-stu-id="c5040-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="c5040-223">Viene calcolata come intervallo hello dall'ora di hello quando il Gateway applicazione riceve il primo byte hello di un'ora di toohello richiesta HTTP quando la risposta hello inviano al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="c5040-224">È importante toonote che hello campo Time-Taken in genere include ora hello che i pacchetti hello richiesta e risposta vengono trasmessi in rete hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="c5040-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="c5040-225">sslEnabled</span></span>| <span data-ttu-id="c5040-226">Indica se i pool back-end di comunicazione toohello utilizzato SSL.</span><span class="sxs-lookup"><span data-stu-id="c5040-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="c5040-227">I valori validi sono on e off.</span><span class="sxs-lookup"><span data-stu-id="c5040-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="c5040-228">Log delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c5040-228">Performance log</span></span>

<span data-ttu-id="c5040-229">log delle prestazioni Hello viene generato solo se è abilitata in ogni istanza del Gateway applicazione, come descritto in dettaglio nella hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c5040-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="c5040-230">Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="c5040-231">dati del registro prestazioni Hello viene generati in intervalli di 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="c5040-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="c5040-232">viene registrato Hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5040-232">hello following data is logged:</span></span>


|<span data-ttu-id="c5040-233">Valore</span><span class="sxs-lookup"><span data-stu-id="c5040-233">Value</span></span>  |<span data-ttu-id="c5040-234">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c5040-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="c5040-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="c5040-235">instanceId</span></span>     |  <span data-ttu-id="c5040-236">Istanza del gateway applicazione per cui vengono generati i dati delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c5040-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="c5040-237">Per un gateway applicazione a più istanze viene visualizzata una riga per ogni istanza.</span><span class="sxs-lookup"><span data-stu-id="c5040-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="c5040-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="c5040-238">healthyHostCount</span></span>     | <span data-ttu-id="c5040-239">Numero di host integro nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="c5040-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="c5040-240">unHealthyHostCount</span></span>     | <span data-ttu-id="c5040-241">Numero di host nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="c5040-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="c5040-242">requestCount</span></span>     | <span data-ttu-id="c5040-243">Numero di richieste gestite.</span><span class="sxs-lookup"><span data-stu-id="c5040-243">Number of requests served.</span></span>        |
|<span data-ttu-id="c5040-244">latency</span><span class="sxs-lookup"><span data-stu-id="c5040-244">latency</span></span> | <span data-ttu-id="c5040-245">Latenza (in millisecondi) delle richieste da hello istanza toohello di back-end che risponde alle richieste di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="c5040-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="c5040-246">failedRequestCount</span></span>| <span data-ttu-id="c5040-247">Numero di richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="c5040-247">Number of failed requests.</span></span>|
|<span data-ttu-id="c5040-248">throughput</span><span class="sxs-lookup"><span data-stu-id="c5040-248">throughput</span></span>| <span data-ttu-id="c5040-249">Velocità effettiva Media dall'ultimo log hello, espresso in byte al secondo.</span><span class="sxs-lookup"><span data-stu-id="c5040-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="c5040-250">Latenza viene calcolata dal momento hello primo byte di hello della richiesta HTTP hello è ora toohello ricevuto quando non viene inviato l'ultimo byte hello di hello risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c5040-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="c5040-251">Gateway applicazione tempo di elaborazione di hello di hello somma di più hello toohello costo di rete torna terminare, più tempo hello hello back-end accetta tooprocess hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="c5040-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="c5040-252">Log del firewall</span><span class="sxs-lookup"><span data-stu-id="c5040-252">Firewall log</span></span>

<span data-ttu-id="c5040-253">Registro firewall Hello viene generato solo se è abilitata per il gateway ogni applicazione, come descritto in dettaglio nella hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c5040-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="c5040-254">Questo log richiede inoltre che il firewall applicazione web hello è configurato su un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5040-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="c5040-255">Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="c5040-256">viene registrato Hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5040-256">hello following data is logged:</span></span>


|<span data-ttu-id="c5040-257">Valore</span><span class="sxs-lookup"><span data-stu-id="c5040-257">Value</span></span>  |<span data-ttu-id="c5040-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c5040-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="c5040-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="c5040-259">instanceId</span></span>     | <span data-ttu-id="c5040-260">Istanza del gateway applicazione per cui vengono generati i dati del firewall.</span><span class="sxs-lookup"><span data-stu-id="c5040-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="c5040-261">Per un gateway applicazione a più istanze viene visualizzata una riga per ogni istanza.</span><span class="sxs-lookup"><span data-stu-id="c5040-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="c5040-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="c5040-262">clientIp</span></span>     |   <span data-ttu-id="c5040-263">IP di origine per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="c5040-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="c5040-264">clientPort</span></span>     |  <span data-ttu-id="c5040-265">Porta di origine per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="c5040-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="c5040-266">requestUri</span></span>     | <span data-ttu-id="c5040-267">URL della richiesta ricevuta hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="c5040-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="c5040-268">ruleSetType</span></span>     | <span data-ttu-id="c5040-269">Tipo di set di regole.</span><span class="sxs-lookup"><span data-stu-id="c5040-269">Rule set type.</span></span> <span data-ttu-id="c5040-270">valore disponibile di Hello è OWASP.</span><span class="sxs-lookup"><span data-stu-id="c5040-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="c5040-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="c5040-271">ruleSetVersion</span></span>     | <span data-ttu-id="c5040-272">Versione del set di regole usata.</span><span class="sxs-lookup"><span data-stu-id="c5040-272">Rule set version used.</span></span> <span data-ttu-id="c5040-273">I valori disponibili sono 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="c5040-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="c5040-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="c5040-274">ruleId</span></span>     | <span data-ttu-id="c5040-275">ID regola di generazione evento hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="c5040-276">Message</span><span class="sxs-lookup"><span data-stu-id="c5040-276">message</span></span>     | <span data-ttu-id="c5040-277">Messaggio descrittivo per hello evento.</span><span class="sxs-lookup"><span data-stu-id="c5040-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="c5040-278">Ulteriori informazioni sono fornite nella sezione dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="c5040-279">action</span><span class="sxs-lookup"><span data-stu-id="c5040-279">action</span></span>     |  <span data-ttu-id="c5040-280">Azione eseguita su richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-280">Action taken on hello request.</span></span> <span data-ttu-id="c5040-281">I valori disponibili sono Blocked e Allowed.</span><span class="sxs-lookup"><span data-stu-id="c5040-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="c5040-282">site</span><span class="sxs-lookup"><span data-stu-id="c5040-282">site</span></span>     | <span data-ttu-id="c5040-283">Sito per cui hello log è stato generato.</span><span class="sxs-lookup"><span data-stu-id="c5040-283">Site for which hello log was generated.</span></span> <span data-ttu-id="c5040-284">Attualmente viene visualizzato solo Global poiché le regole sono globali.</span><span class="sxs-lookup"><span data-stu-id="c5040-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="c5040-285">informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="c5040-285">details</span></span>     | <span data-ttu-id="c5040-286">Dettagli dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="c5040-287">details.message</span><span class="sxs-lookup"><span data-stu-id="c5040-287">details.message</span></span>     | <span data-ttu-id="c5040-288">Descrizione della regola hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="c5040-289">details.data</span><span class="sxs-lookup"><span data-stu-id="c5040-289">details.data</span></span>     | <span data-ttu-id="c5040-290">Trovare i dati specifici nella richiesta di tale regola hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c5040-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="c5040-291">details.file</span><span class="sxs-lookup"><span data-stu-id="c5040-291">details.file</span></span>     | <span data-ttu-id="c5040-292">File di configurazione contenente una regola di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="c5040-293">details.line</span><span class="sxs-lookup"><span data-stu-id="c5040-293">details.line</span></span>     | <span data-ttu-id="c5040-294">Numero di riga nel file di configurazione hello che ha attivato hello evento.</span><span class="sxs-lookup"><span data-stu-id="c5040-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="c5040-295">Visualizzare e analizzare i log attività hello</span><span class="sxs-lookup"><span data-stu-id="c5040-295">View and analyze hello activity log</span></span>

<span data-ttu-id="c5040-296">È possibile visualizzare e analizzare i dati del log attività utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="c5040-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="c5040-297">**Gli strumenti di Azure**: recuperare informazioni dal registro attività hello tramite Azure PowerShell, hello CLI di Azure, hello l'API REST di Azure o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5040-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="c5040-298">Istruzioni dettagliate per ogni metodo sono descritti in dettaglio in hello [operazioni di attività con Gestione risorse](../azure-resource-manager/resource-group-audit.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c5040-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="c5040-299">**Power BI**: se non si ha ancora un account [Power BI](https://powerbi.microsoft.com/pricing) , è possibile crearne uno di prova gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="c5040-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="c5040-300">Utilizzando hello [log attività Azure pacchetto di contenuto per Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), è possibile analizzare i dati con i dashboard preconfigurati, che è possibile utilizzare così come sono oppure personalizzare.</span><span class="sxs-lookup"><span data-stu-id="c5040-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="c5040-301">Visualizzare e analizzare accesso hello, prestazioni e i log del firewall</span><span class="sxs-lookup"><span data-stu-id="c5040-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="c5040-302">Azure [Log Analitica](../log-analytics/log-analytics-azure-networking-analytics.md) può raccogliere i file di registro eventi e contatori di hello dall'account di archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="c5040-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="c5040-303">Sono inclusi i log di visualizzazioni e tooanalyze funzionalità di ricerca avanzate.</span><span class="sxs-lookup"><span data-stu-id="c5040-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="c5040-304">È possibile anche connettersi tooyour account di archiviazione e recupero delle voci di log hello JSON per i log di accesso e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c5040-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="c5040-305">Dopo aver scaricato i file JSON hello, è possibile convertirli tooCSV e visualizzarli in Excel, Power BI o qualsiasi altro strumento di visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c5040-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="c5040-306">Se si ha familiarità con Visual Studio e concetti di base di modificare i valori costanti e variabili in c#, è possibile utilizzare hello [log strumenti convertitore](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibili da GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5040-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="c5040-307">Metrica</span><span class="sxs-lookup"><span data-stu-id="c5040-307">Metrics</span></span>

<span data-ttu-id="c5040-308">Le metriche sono una funzionalità per alcune risorse di Azure in cui è possibile visualizzare i contatori delle prestazioni nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="c5040-309">Per il gateway applicazione è ora disponibile una sola metrica.</span><span class="sxs-lookup"><span data-stu-id="c5040-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="c5040-310">Questa metrica è la velocità effettiva ed è possibile visualizzarlo nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="c5040-311">Gateway applicazione tooan e fare clic su **metriche**.</span><span class="sxs-lookup"><span data-stu-id="c5040-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="c5040-312">i valori hello tooview, selezionare la velocità effettiva in hello **le metriche disponibili** sezione.</span><span class="sxs-lookup"><span data-stu-id="c5040-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="c5040-313">Nella seguente immagine di hello, è possibile visualizzare un esempio con filtri di hello che è possibile utilizzare dati hello toodisplay negli intervalli di tempo diverso.</span><span class="sxs-lookup"><span data-stu-id="c5040-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Visualizzazione della metrica con filtri][5]

<span data-ttu-id="c5040-315">vedere un elenco corrente di metriche, toosee [metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c5040-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="c5040-316">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="c5040-316">Alert rules</span></span>

<span data-ttu-id="c5040-317">È possibile avviare le regole di avviso in base alle metriche per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="c5040-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="c5040-318">Ad esempio, un avviso può chiamare un webhook o un amministratore di posta elettronica se la velocità effettiva hello del gateway applicazione hello è di sopra, sotto o con una soglia per un periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="c5040-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="c5040-319">Hello di esempio seguente viene illustrato come creare una regola di avviso che invia un amministratore di posta elettronica tooan dopo le violazioni della velocità effettiva una soglia:</span><span class="sxs-lookup"><span data-stu-id="c5040-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="c5040-320">Fare clic su **Aggiungi avviso metrica** tooopen hello **Aggiungi regola** blade.</span><span class="sxs-lookup"><span data-stu-id="c5040-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="c5040-321">È anche possibile contattare questo pannello pannello metriche hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Pulsante "Aggiungi avviso per la metrica"][6]

2. <span data-ttu-id="c5040-323">In hello **Aggiungi regola** pannello compilare nome hello, la condizione, inviare una notifica di sezioni e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5040-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="c5040-324">In hello **condizione** selettore, selezionare uno dei valori hello quattro: **maggiore**, **maggiore o uguale**, **minore**, o  **Minore o uguale a**.</span><span class="sxs-lookup"><span data-stu-id="c5040-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="c5040-325">In hello **periodo** selettore, selezionare un periodo compreso tra 5 minuti too6 ore.</span><span class="sxs-lookup"><span data-stu-id="c5040-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="c5040-326">Se si seleziona **i proprietari, collaboratori e lettori di posta elettronica**, posta elettronica hello può essere dinamica in base agli utenti di hello che dispongono di accesso toothat risorse.</span><span class="sxs-lookup"><span data-stu-id="c5040-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="c5040-327">In caso contrario, è possibile fornire un elenco delimitato da virgole di utenti in hello **email(s) amministratore aggiuntive** casella.</span><span class="sxs-lookup"><span data-stu-id="c5040-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Aggiungere il pannello delle regole][7]

<span data-ttu-id="c5040-329">Se viene superata la soglia hello, arriva un messaggio di posta elettronica è simile toohello uno in hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="c5040-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Messaggio di posta elettronica per il superamento della soglia][8]

<span data-ttu-id="c5040-331">Dopo aver creato un avviso per la metrica, viene visualizzato un elenco di avvisi.</span><span class="sxs-lookup"><span data-stu-id="c5040-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="c5040-332">Fornisce una panoramica di tutte le regole di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="c5040-332">It provides an overview of all hello alert rules.</span></span>

![Elenco di avvisi e regole][9]

<span data-ttu-id="c5040-334">toolearn più sulle notifiche di avviso, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c5040-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="c5040-335">toounderstand ulteriori informazioni su webhook e come è possibile utilizzare con gli avvisi, visitare [configurare un webhook su un avviso di metrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c5040-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5040-336">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5040-336">Next steps</span></span>

* <span data-ttu-id="c5040-337">Visualizzare i log contatori ed eventi usando [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c5040-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="c5040-338">Post di blog [Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizzare il log attività di Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="c5040-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="c5040-339">Post di blog [View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Visualizzare e analizzare i log attività di Azure in Power BI e altre opzioni).</span><span class="sxs-lookup"><span data-stu-id="c5040-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
