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
# <a name="manage-log-analytics-using-powershell"></a>Gestire Log Analytics con PowerShell
È possibile utilizzare hello [i cmdlet di PowerShell Analitica Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform le diverse funzioni Log Analitica dalla riga di comando o come parte di uno script.  Esempi di attività hello che è possibile eseguire con PowerShell:

* Creare un'area di lavoro
* Aggiungere o rimuovere una soluzione
* Importare ed esportare ricerche salvate
* Creare un gruppo di computer
* Abilitare la raccolta di log di IIS dal computer con installato l'agente di Windows hello
* Raccogliere i contatori delle prestazioni dai computer Linux e Windows
* Raccogliere gli eventi dal syslog sui computer Linux 
* Raccogliere gli eventi dai log eventi di Windows
* Raccogliere i log eventi personalizzati
* Aggiungere hello log analitica agente tooan macchina virtuale di Azure
* Configurare log analitica tooindex dati raccolti tramite diagnostica Azure

Questo articolo fornisce due esempi di codice che illustrano alcune delle funzioni hello che è possibile eseguire da PowerShell.  È possibile fare riferimento toohello [riferimento ai cmdlet di PowerShell Analitica Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) per altre funzioni.

> [!NOTE]
> Log Analitica era precedentemente denominato Operational Insights, perché è il nome di hello utilizzato nei cmdlet hello.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questi esempi funzionano con la versione 2.3.0 o successiva del modulo AzureRm.OperationalInsights hello.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Creare e configurare un'area di lavoro di Log Analytics
Hello seguente script di esempio viene illustrato come:

1. Creare un'area di lavoro
2. Elenco hello disponibili soluzioni
3. Aggiungere soluzioni toohello area di lavoro
4. Importare le ricerche salvate
5. Esportare le ricerche salvate
6. Creare un gruppo di computer
7. Abilitare la raccolta di log di IIS dal computer con installato l'agente di Windows hello
8. Raccogliere i dati dei contatori delle prestazioni del disco logico dai computer Linux (% inodi usati; megabyte liberi; % di spazio usato; trasferimenti/sec del disco; letture/sec del disco; scritture/sec del disco)
9. Raccogliere gli eventi syslog dai computer Linux
10. Raccogliere gli eventi di errore e avviso da hello registro eventi dell'applicazione dai computer Windows
11. Raccogliere i dati del contatore delle prestazioni dei Mbyte di memoria disponibili dai computer Windows
12. Raccogliere i dati di un log personalizzato 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Configurazione di Log Analitica tooindex diagnostica Windows Azure
Per il monitoraggio senza agenti di risorse di Azure, le risorse di hello devono toohave diagnostica Windows Azure toowrite abilitato e configurato tooa Log Analitica area di lavoro. Questo approccio invia i dati direttamente tooLog Analitica e non richiede dati toobe scritto tooa account di archiviazione. Le risorse supportate includono:

| Tipo di risorsa | Log | Metrica |
| --- | --- | --- |
| Gateway applicazione    | Sì | Sì |
| Account di Automazione     | Sì | |
| Account Batch          | Sì | Sì |
| Data Lake Analytics     | Sì | | 
| Data Lake Store         | Sì | |
| Pool SQL elastico        |     | Sì |
| Spazio dei nomi dell'hub eventi     |     | Sì |
| Hub IoT                |     | Sì |
| Insieme di credenziali di chiave               | Sì | |
| Servizi di bilanciamento del carico          | Sì | |
| App per la logica              | Sì | Sì |
| Gruppi di sicurezza di rete | Sì | |
| Cache Redis             |     | Sì |
| Servizi di ricerca         | Sì | Sì |
| Spazio dei nomi del bus di servizio   |     | Sì |
| SQL (versione 12)               |     | Sì |
| Microsoft Azure               |     | Sì |
| Server farm Web        |     | Sì |

Per informazioni dettagliate hello delle metriche disponibili hello, fare riferimento troppo[metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Per informazioni dettagliate sulle hello registri disponibili hello, fare riferimento troppo[supportata servizi e lo schema per i log di diagnostica](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

È possibile utilizzare anche hello precedente cmdlet toocollect log dalle risorse di cui si trovano in sottoscrizioni diverse. cmdlet di Hello è toowork in grado di nelle sottoscrizioni poiché hello dell'area di lavoro hello log vengono inviati e si desidera fornire id hello della risorsa sia hello creazione di log.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Configurazione di Log Analitica tooindex diagnostica da archiviazione di Azure
dati log toocollect dall'interno di un'istanza di un servizio cloud classico o un cluster di service fabric in esecuzione, è necessario un toofirst scrittura hello dati tooAzure archivio. Log Analitica viene quindi configurato registri hello toocollect dall'account di archiviazione hello. Le risorse supportate includono:

* Servizi cloud classici (ruoli di lavoro e Web)
* Cluster di Service Fabric

Hello seguente come esempio per:

1. Elenco di account di archiviazione esistente hello e le posizioni Log Analitica indicizza i dati da
2. Creare un tooread di configurazione da un account di archiviazione
3. Hello creati dati di configurazione tooindex da altri percorsi di aggiornamento
4. Eliminare la configurazione di hello appena creato.

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

È anche possibile utilizzare hello precedenti registri toocollect script dagli account di archiviazione in diverse sottoscrizioni. script Hello è in grado di toowork tra sottoscrizioni poiché si desidera fornire l'id di risorsa account di archiviazione hello e una chiave di accesso corrispondente. Quando si modifica la chiave di accesso hello, è necessario tooupdate hello archiviazione insight toohave hello nuova chiave.


## <a name="next-steps"></a>Passaggi successivi
* [cmdlet di PowerShell per Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) .

