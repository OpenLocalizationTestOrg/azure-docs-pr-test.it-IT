---
title: aaaUse PowerShell tooCreate e configurare un'area di lavoro di Log Analitica | Documenti Microsoft
description: "Log Analytics usa i dati provenienti dai server nell'infrastruttura locale o cloud. È possibile raccogliere i dati del computer dall'archiviazione di Azure quando vengono generati dalla diagnostica di Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="d2e21-104">Gestire Log Analytics con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2e21-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="d2e21-105">È possibile utilizzare hello [i cmdlet di PowerShell Analitica Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform le diverse funzioni Log Analitica dalla riga di comando o come parte di uno script.</span><span class="sxs-lookup"><span data-stu-id="d2e21-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="d2e21-106">Esempi di attività hello che è possibile eseguire con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2e21-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="d2e21-107">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d2e21-107">Create a workspace</span></span>
* <span data-ttu-id="d2e21-108">Aggiungere o rimuovere una soluzione</span><span class="sxs-lookup"><span data-stu-id="d2e21-108">Add or remove a solution</span></span>
* <span data-ttu-id="d2e21-109">Importare ed esportare ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d2e21-109">Import and export saved searches</span></span>
* <span data-ttu-id="d2e21-110">Creare un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="d2e21-110">Create a computer group</span></span>
* <span data-ttu-id="d2e21-111">Abilitare la raccolta di log di IIS dal computer con installato l'agente di Windows hello</span><span class="sxs-lookup"><span data-stu-id="d2e21-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="d2e21-112">Raccogliere i contatori delle prestazioni dai computer Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="d2e21-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="d2e21-113">Raccogliere gli eventi dal syslog sui computer Linux</span><span class="sxs-lookup"><span data-stu-id="d2e21-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="d2e21-114">Raccogliere gli eventi dai log eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="d2e21-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="d2e21-115">Raccogliere i log eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="d2e21-115">Collect custom event logs</span></span>
* <span data-ttu-id="d2e21-116">Aggiungere hello log analitica agente tooan macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d2e21-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="d2e21-117">Configurare log analitica tooindex dati raccolti tramite diagnostica Azure</span><span class="sxs-lookup"><span data-stu-id="d2e21-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="d2e21-118">Questo articolo fornisce due esempi di codice che illustrano alcune delle funzioni hello che è possibile eseguire da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2e21-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="d2e21-119">È possibile fare riferimento toohello [riferimento ai cmdlet di PowerShell Analitica Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) per altre funzioni.</span><span class="sxs-lookup"><span data-stu-id="d2e21-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="d2e21-120">Log Analitica era precedentemente denominato Operational Insights, perché è il nome di hello utilizzato nei cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="d2e21-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d2e21-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d2e21-121">Prerequisites</span></span>
<span data-ttu-id="d2e21-122">Questi esempi funzionano con la versione 2.3.0 o successiva del modulo AzureRm.OperationalInsights hello.</span><span class="sxs-lookup"><span data-stu-id="d2e21-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="d2e21-123">Creare e configurare un'area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d2e21-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="d2e21-124">Hello seguente script di esempio viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="d2e21-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="d2e21-125">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d2e21-125">Create a workspace</span></span>
2. <span data-ttu-id="d2e21-126">Elenco hello disponibili soluzioni</span><span class="sxs-lookup"><span data-stu-id="d2e21-126">List hello available solutions</span></span>
3. <span data-ttu-id="d2e21-127">Aggiungere soluzioni toohello area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d2e21-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="d2e21-128">Importare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d2e21-128">Import saved searches</span></span>
5. <span data-ttu-id="d2e21-129">Esportare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d2e21-129">Export saved searches</span></span>
6. <span data-ttu-id="d2e21-130">Creare un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="d2e21-130">Create a computer group</span></span>
7. <span data-ttu-id="d2e21-131">Abilitare la raccolta di log di IIS dal computer con installato l'agente di Windows hello</span><span class="sxs-lookup"><span data-stu-id="d2e21-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="d2e21-132">Raccogliere i dati dei contatori delle prestazioni del disco logico dai computer Linux (% inodi usati; megabyte liberi; % di spazio usato; trasferimenti/sec del disco; letture/sec del disco; scritture/sec del disco)</span><span class="sxs-lookup"><span data-stu-id="d2e21-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="d2e21-133">Raccogliere gli eventi syslog dai computer Linux</span><span class="sxs-lookup"><span data-stu-id="d2e21-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="d2e21-134">Raccogliere gli eventi di errore e avviso da hello registro eventi dell'applicazione dai computer Windows</span><span class="sxs-lookup"><span data-stu-id="d2e21-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="d2e21-135">Raccogliere i dati del contatore delle prestazioni dei Mbyte di memoria disponibili dai computer Windows</span><span class="sxs-lookup"><span data-stu-id="d2e21-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="d2e21-136">Raccogliere i dati di un log personalizzato</span><span class="sxs-lookup"><span data-stu-id="d2e21-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="d2e21-137">Configurazione di Log Analitica tooindex diagnostica Windows Azure</span><span class="sxs-lookup"><span data-stu-id="d2e21-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="d2e21-138">Per il monitoraggio senza agenti di risorse di Azure, le risorse di hello devono toohave diagnostica Windows Azure toowrite abilitato e configurato tooa Log Analitica area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d2e21-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="d2e21-139">Questo approccio invia i dati direttamente tooLog Analitica e non richiede dati toobe scritto tooa account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2e21-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="d2e21-140">Le risorse supportate includono:</span><span class="sxs-lookup"><span data-stu-id="d2e21-140">Supported resources include:</span></span>

| <span data-ttu-id="d2e21-141">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="d2e21-141">Resource Type</span></span> | <span data-ttu-id="d2e21-142">Log</span><span class="sxs-lookup"><span data-stu-id="d2e21-142">Logs</span></span> | <span data-ttu-id="d2e21-143">Metrica</span><span class="sxs-lookup"><span data-stu-id="d2e21-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d2e21-144">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="d2e21-144">Application Gateways</span></span>    | <span data-ttu-id="d2e21-145">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-145">Yes</span></span> | <span data-ttu-id="d2e21-146">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-146">Yes</span></span> |
| <span data-ttu-id="d2e21-147">Account di Automazione</span><span class="sxs-lookup"><span data-stu-id="d2e21-147">Automation accounts</span></span>     | <span data-ttu-id="d2e21-148">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-148">Yes</span></span> | |
| <span data-ttu-id="d2e21-149">Account Batch</span><span class="sxs-lookup"><span data-stu-id="d2e21-149">Batch accounts</span></span>          | <span data-ttu-id="d2e21-150">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-150">Yes</span></span> | <span data-ttu-id="d2e21-151">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-151">Yes</span></span> |
| <span data-ttu-id="d2e21-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d2e21-152">Data Lake analytics</span></span>     | <span data-ttu-id="d2e21-153">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-153">Yes</span></span> | | 
| <span data-ttu-id="d2e21-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2e21-154">Data Lake store</span></span>         | <span data-ttu-id="d2e21-155">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-155">Yes</span></span> | |
| <span data-ttu-id="d2e21-156">Pool SQL elastico</span><span class="sxs-lookup"><span data-stu-id="d2e21-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="d2e21-157">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-157">Yes</span></span> |
| <span data-ttu-id="d2e21-158">Spazio dei nomi dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="d2e21-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="d2e21-159">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-159">Yes</span></span> |
| <span data-ttu-id="d2e21-160">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="d2e21-160">IoT Hubs</span></span>                |     | <span data-ttu-id="d2e21-161">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-161">Yes</span></span> |
| <span data-ttu-id="d2e21-162">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="d2e21-162">Key Vault</span></span>               | <span data-ttu-id="d2e21-163">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-163">Yes</span></span> | |
| <span data-ttu-id="d2e21-164">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d2e21-164">Load Balancers</span></span>          | <span data-ttu-id="d2e21-165">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-165">Yes</span></span> | |
| <span data-ttu-id="d2e21-166">App per la logica</span><span class="sxs-lookup"><span data-stu-id="d2e21-166">Logic Apps</span></span>              | <span data-ttu-id="d2e21-167">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-167">Yes</span></span> | <span data-ttu-id="d2e21-168">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-168">Yes</span></span> |
| <span data-ttu-id="d2e21-169">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="d2e21-169">Network Security Groups</span></span> | <span data-ttu-id="d2e21-170">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-170">Yes</span></span> | |
| <span data-ttu-id="d2e21-171">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d2e21-171">Redis Cache</span></span>             |     | <span data-ttu-id="d2e21-172">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-172">Yes</span></span> |
| <span data-ttu-id="d2e21-173">Servizi di ricerca</span><span class="sxs-lookup"><span data-stu-id="d2e21-173">Search services</span></span>         | <span data-ttu-id="d2e21-174">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-174">Yes</span></span> | <span data-ttu-id="d2e21-175">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-175">Yes</span></span> |
| <span data-ttu-id="d2e21-176">Spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d2e21-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="d2e21-177">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-177">Yes</span></span> |
| <span data-ttu-id="d2e21-178">SQL (versione 12)</span><span class="sxs-lookup"><span data-stu-id="d2e21-178">SQL (v12)</span></span>               |     | <span data-ttu-id="d2e21-179">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-179">Yes</span></span> |
| <span data-ttu-id="d2e21-180">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d2e21-180">Web Sites</span></span>               |     | <span data-ttu-id="d2e21-181">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-181">Yes</span></span> |
| <span data-ttu-id="d2e21-182">Server farm Web</span><span class="sxs-lookup"><span data-stu-id="d2e21-182">Web Server farms</span></span>        |     | <span data-ttu-id="d2e21-183">Sì</span><span class="sxs-lookup"><span data-stu-id="d2e21-183">Yes</span></span> |

<span data-ttu-id="d2e21-184">Per informazioni dettagliate hello delle metriche disponibili hello, fare riferimento troppo[metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d2e21-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="d2e21-185">Per informazioni dettagliate sulle hello registri disponibili hello, fare riferimento troppo[supportata servizi e lo schema per i log di diagnostica](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d2e21-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="d2e21-186">È possibile utilizzare anche hello precedente cmdlet toocollect log dalle risorse di cui si trovano in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="d2e21-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="d2e21-187">cmdlet di Hello è toowork in grado di nelle sottoscrizioni poiché hello dell'area di lavoro hello log vengono inviati e si desidera fornire id hello della risorsa sia hello creazione di log.</span><span class="sxs-lookup"><span data-stu-id="d2e21-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="d2e21-188">Configurazione di Log Analitica tooindex diagnostica da archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d2e21-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="d2e21-189">dati log toocollect dall'interno di un'istanza di un servizio cloud classico o un cluster di service fabric in esecuzione, è necessario un toofirst scrittura hello dati tooAzure archivio.</span><span class="sxs-lookup"><span data-stu-id="d2e21-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="d2e21-190">Log Analitica viene quindi configurato registri hello toocollect dall'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="d2e21-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="d2e21-191">Le risorse supportate includono:</span><span class="sxs-lookup"><span data-stu-id="d2e21-191">Supported resources include:</span></span>

* <span data-ttu-id="d2e21-192">Servizi cloud classici (ruoli di lavoro e Web)</span><span class="sxs-lookup"><span data-stu-id="d2e21-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="d2e21-193">Cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2e21-193">Service fabric clusters</span></span>

<span data-ttu-id="d2e21-194">Hello seguente come esempio per:</span><span class="sxs-lookup"><span data-stu-id="d2e21-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="d2e21-195">Elenco di account di archiviazione esistente hello e le posizioni Log Analitica indicizza i dati da</span><span class="sxs-lookup"><span data-stu-id="d2e21-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="d2e21-196">Creare un tooread di configurazione da un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d2e21-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="d2e21-197">Hello creati dati di configurazione tooindex da altri percorsi di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="d2e21-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="d2e21-198">Eliminare la configurazione di hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="d2e21-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="d2e21-199">È anche possibile utilizzare hello precedenti registri toocollect script dagli account di archiviazione in diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="d2e21-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="d2e21-200">script Hello è in grado di toowork tra sottoscrizioni poiché si desidera fornire l'id di risorsa account di archiviazione hello e una chiave di accesso corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d2e21-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="d2e21-201">Quando si modifica la chiave di accesso hello, è necessario tooupdate hello archiviazione insight toohave hello nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="d2e21-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d2e21-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2e21-202">Next steps</span></span>
* <span data-ttu-id="d2e21-203">[cmdlet di PowerShell per Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) .</span><span class="sxs-lookup"><span data-stu-id="d2e21-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

