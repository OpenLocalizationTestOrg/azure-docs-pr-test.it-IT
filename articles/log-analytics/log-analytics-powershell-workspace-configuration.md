---
title: Usare PowerShell per creare e configurare un'area di lavoro di Log Analytics | Documentazione Microsoft
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="d34ea-104">Gestire Log Analytics con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34ea-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="d34ea-105">È possibile usare i [cmdlet di PowerShell per Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) per eseguire varie funzioni in Log Analytics dalla riga di comando o nell'ambito di uno script.</span><span class="sxs-lookup"><span data-stu-id="d34ea-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="d34ea-106">Esempi di attività che è possibile eseguire con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d34ea-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="d34ea-107">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d34ea-107">Create a workspace</span></span>
* <span data-ttu-id="d34ea-108">Aggiungere o rimuovere una soluzione</span><span class="sxs-lookup"><span data-stu-id="d34ea-108">Add or remove a solution</span></span>
* <span data-ttu-id="d34ea-109">Importare ed esportare ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d34ea-109">Import and export saved searches</span></span>
* <span data-ttu-id="d34ea-110">Creare un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="d34ea-110">Create a computer group</span></span>
* <span data-ttu-id="d34ea-111">Abilitare la raccolta dei log IIS dai computer su cui è stato installato l'agente di Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="d34ea-112">Raccogliere i contatori delle prestazioni dai computer Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="d34ea-113">Raccogliere gli eventi dal syslog sui computer Linux</span><span class="sxs-lookup"><span data-stu-id="d34ea-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="d34ea-114">Raccogliere gli eventi dai log eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="d34ea-115">Raccogliere i log eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="d34ea-115">Collect custom event logs</span></span>
* <span data-ttu-id="d34ea-116">Aggiungere l'agente Log Analytics a una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d34ea-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="d34ea-117">Configurare Log Analytics per indicizzare i dati raccolti tramite Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="d34ea-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="d34ea-118">Questo articolo presenta due codici di esempio con cui vengono illustrate alcune delle funzioni che è possibile eseguire da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d34ea-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="d34ea-119">Per altre funzioni, è possibile fare riferimento all'articolo sui [cmdlet di PowerShell per Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) .</span><span class="sxs-lookup"><span data-stu-id="d34ea-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="d34ea-120">In precedenza Log Analytics veniva chiamato Operational Insight, motivo per cui nei cmdlet viene usato questo nome.</span><span class="sxs-lookup"><span data-stu-id="d34ea-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d34ea-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d34ea-121">Prerequisites</span></span>
<span data-ttu-id="d34ea-122">Questi esempi funzionano con la versione 2.3.0 o successive del modulo AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="d34ea-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="d34ea-123">Creare e configurare un'area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d34ea-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="d34ea-124">Lo script di esempio seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="d34ea-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="d34ea-125">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d34ea-125">Create a workspace</span></span>
2. <span data-ttu-id="d34ea-126">Elencare le soluzioni disponibili</span><span class="sxs-lookup"><span data-stu-id="d34ea-126">List the available solutions</span></span>
3. <span data-ttu-id="d34ea-127">Aggiungere soluzioni all'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d34ea-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="d34ea-128">Importare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d34ea-128">Import saved searches</span></span>
5. <span data-ttu-id="d34ea-129">Esportare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="d34ea-129">Export saved searches</span></span>
6. <span data-ttu-id="d34ea-130">Creare un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="d34ea-130">Create a computer group</span></span>
7. <span data-ttu-id="d34ea-131">Abilitare la raccolta dei log IIS dai computer su cui è stato installato l'agente di Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="d34ea-132">Raccogliere i dati dei contatori delle prestazioni del disco logico dai computer Linux (% inodi usati; megabyte liberi; % di spazio usato; trasferimenti/sec del disco; letture/sec del disco; scritture/sec del disco)</span><span class="sxs-lookup"><span data-stu-id="d34ea-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="d34ea-133">Raccogliere gli eventi syslog dai computer Linux</span><span class="sxs-lookup"><span data-stu-id="d34ea-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="d34ea-134">Raccogliere gli eventi di errore e di avviso dal log eventi dell'applicazione dai computer Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="d34ea-135">Raccogliere i dati del contatore delle prestazioni dei Mbyte di memoria disponibili dai computer Windows</span><span class="sxs-lookup"><span data-stu-id="d34ea-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="d34ea-136">Raccogliere i dati di un log personalizzato</span><span class="sxs-lookup"><span data-stu-id="d34ea-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="d34ea-137">Configurazione di Log Analytics per indicizzare Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="d34ea-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="d34ea-138">Per il monitoraggio senza agenti delle risorse di Azure, in queste ultime la diagnostica di Azure deve essere abilitata e configurata per la scrittura in un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d34ea-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="d34ea-139">Questo approccio permette di inviare i dati direttamente a Log Analytics e non ne richiede la scrittura in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d34ea-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="d34ea-140">Le risorse supportate includono:</span><span class="sxs-lookup"><span data-stu-id="d34ea-140">Supported resources include:</span></span>

| <span data-ttu-id="d34ea-141">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="d34ea-141">Resource Type</span></span> | <span data-ttu-id="d34ea-142">Log</span><span class="sxs-lookup"><span data-stu-id="d34ea-142">Logs</span></span> | <span data-ttu-id="d34ea-143">Metrica</span><span class="sxs-lookup"><span data-stu-id="d34ea-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d34ea-144">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="d34ea-144">Application Gateways</span></span>    | <span data-ttu-id="d34ea-145">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-145">Yes</span></span> | <span data-ttu-id="d34ea-146">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-146">Yes</span></span> |
| <span data-ttu-id="d34ea-147">Account di Automazione</span><span class="sxs-lookup"><span data-stu-id="d34ea-147">Automation accounts</span></span>     | <span data-ttu-id="d34ea-148">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-148">Yes</span></span> | |
| <span data-ttu-id="d34ea-149">Account Batch</span><span class="sxs-lookup"><span data-stu-id="d34ea-149">Batch accounts</span></span>          | <span data-ttu-id="d34ea-150">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-150">Yes</span></span> | <span data-ttu-id="d34ea-151">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-151">Yes</span></span> |
| <span data-ttu-id="d34ea-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d34ea-152">Data Lake analytics</span></span>     | <span data-ttu-id="d34ea-153">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-153">Yes</span></span> | | 
| <span data-ttu-id="d34ea-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d34ea-154">Data Lake store</span></span>         | <span data-ttu-id="d34ea-155">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-155">Yes</span></span> | |
| <span data-ttu-id="d34ea-156">Pool SQL elastico</span><span class="sxs-lookup"><span data-stu-id="d34ea-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="d34ea-157">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-157">Yes</span></span> |
| <span data-ttu-id="d34ea-158">Spazio dei nomi dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="d34ea-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="d34ea-159">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-159">Yes</span></span> |
| <span data-ttu-id="d34ea-160">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="d34ea-160">IoT Hubs</span></span>                |     | <span data-ttu-id="d34ea-161">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-161">Yes</span></span> |
| <span data-ttu-id="d34ea-162">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="d34ea-162">Key Vault</span></span>               | <span data-ttu-id="d34ea-163">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-163">Yes</span></span> | |
| <span data-ttu-id="d34ea-164">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d34ea-164">Load Balancers</span></span>          | <span data-ttu-id="d34ea-165">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-165">Yes</span></span> | |
| <span data-ttu-id="d34ea-166">App per la logica</span><span class="sxs-lookup"><span data-stu-id="d34ea-166">Logic Apps</span></span>              | <span data-ttu-id="d34ea-167">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-167">Yes</span></span> | <span data-ttu-id="d34ea-168">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-168">Yes</span></span> |
| <span data-ttu-id="d34ea-169">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="d34ea-169">Network Security Groups</span></span> | <span data-ttu-id="d34ea-170">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-170">Yes</span></span> | |
| <span data-ttu-id="d34ea-171">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d34ea-171">Redis Cache</span></span>             |     | <span data-ttu-id="d34ea-172">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-172">Yes</span></span> |
| <span data-ttu-id="d34ea-173">Servizi di ricerca</span><span class="sxs-lookup"><span data-stu-id="d34ea-173">Search services</span></span>         | <span data-ttu-id="d34ea-174">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-174">Yes</span></span> | <span data-ttu-id="d34ea-175">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-175">Yes</span></span> |
| <span data-ttu-id="d34ea-176">Spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d34ea-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="d34ea-177">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-177">Yes</span></span> |
| <span data-ttu-id="d34ea-178">SQL (versione 12)</span><span class="sxs-lookup"><span data-stu-id="d34ea-178">SQL (v12)</span></span>               |     | <span data-ttu-id="d34ea-179">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-179">Yes</span></span> |
| <span data-ttu-id="d34ea-180">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d34ea-180">Web Sites</span></span>               |     | <span data-ttu-id="d34ea-181">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-181">Yes</span></span> |
| <span data-ttu-id="d34ea-182">Server farm Web</span><span class="sxs-lookup"><span data-stu-id="d34ea-182">Web Server farms</span></span>        |     | <span data-ttu-id="d34ea-183">Sì</span><span class="sxs-lookup"><span data-stu-id="d34ea-183">Yes</span></span> |

<span data-ttu-id="d34ea-184">Per informazioni dettagliate sulle metriche disponibili, vedere [Metriche supportate con il monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d34ea-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="d34ea-185">Per informazioni dettagliate sui registri disponibili, vedere [Servizi supportati e schema per i log di diagnostica](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d34ea-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="d34ea-186">Il cmdlet precedente può essere usato anche per la raccolta di log da risorse presenti in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="d34ea-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="d34ea-187">Il funzionamento del cmdlet in sottoscrizioni diverse è possibile perché vengono specificati sia l'ID della risorsa che crea i log sia l'area di lavoro a cui questi vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="d34ea-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="d34ea-188">Configurazione di Log Analytics per indicizzare la diagnostica di Azure dall'Archiviazione</span><span class="sxs-lookup"><span data-stu-id="d34ea-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="d34ea-189">Per raccogliere dati di log dall'interno di un'istanza in esecuzione di un servizio cloud classico o di un cluster di Service Fabric, è necessario prima scrivere i dati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d34ea-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="d34ea-190">Log Analytics viene quindi configurato per la raccolta dei log dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d34ea-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="d34ea-191">Le risorse supportate includono:</span><span class="sxs-lookup"><span data-stu-id="d34ea-191">Supported resources include:</span></span>

* <span data-ttu-id="d34ea-192">Servizi cloud classici (ruoli di lavoro e Web)</span><span class="sxs-lookup"><span data-stu-id="d34ea-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="d34ea-193">Cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d34ea-193">Service fabric clusters</span></span>

<span data-ttu-id="d34ea-194">L'esempio seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="d34ea-194">The following example shows how to:</span></span>

1. <span data-ttu-id="d34ea-195">Elencare gli account di archiviazione esistenti e i percorsi da cui Log Analytics eseguirà l'indicizzazione dei dati</span><span class="sxs-lookup"><span data-stu-id="d34ea-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="d34ea-196">Creare una configurazione che possa essere letta da un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d34ea-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="d34ea-197">Aggiornare la configurazione appena creata in modo da poter indicizzare i dati anche da altri percorsi</span><span class="sxs-lookup"><span data-stu-id="d34ea-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="d34ea-198">Eliminare la configurazione appena creata</span><span class="sxs-lookup"><span data-stu-id="d34ea-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="d34ea-199">Lo script precedente può essere usato anche per la raccolta di log da account di archiviazione presenti in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="d34ea-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="d34ea-200">Il funzionamento dello script in sottoscrizioni diverse è possibile perché vengono specificati sia l'ID risorsa dell'account di archiviazione che la chiave di accesso corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d34ea-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="d34ea-201">Quando si modifica la chiave di accesso, è necessario aggiornare le informazioni di archiviazione con la nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="d34ea-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d34ea-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d34ea-202">Next steps</span></span>
* <span data-ttu-id="d34ea-203">[cmdlet di PowerShell per Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) .</span><span class="sxs-lookup"><span data-stu-id="d34ea-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

