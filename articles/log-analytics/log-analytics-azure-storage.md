---
title: aaaCollect Azure servizio metriche e log per il Log Analitica | Documenti Microsoft
description: Configurare la diagnostica in risorse di Azure toowrite metriche e log tooLog Analitica.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Raccolta di log e metriche per i servizi di Azure da usare in Log Analytics

Esistono quattro diversi modi per raccogliere log e metriche per i servizi di Azure:

1. Diagnostica di Azure diretta tooLog Analitica (*diagnostica* in hello nella tabella seguente)
2. Diagnostica di Azure tooAzure archiviazione tooLog Analitica (*archiviazione* in hello nella tabella seguente)
3. I connettori per servizi di Azure (*connettori* in hello nella tabella seguente)
4. Script di toocollect e, successivamente, i dati post in Log Analitica (vuote nella tabella seguente hello e per i servizi che non sono elencati)


| Service                 | Tipo di risorsa                           | Log        | Metrica     | Soluzione |
| --- | --- | --- | --- | --- |
| Gateway di applicazione    | Microsoft.Network/applicationGateways   | Diagnostica | Diagnostica | [Analisi dei gateway applicazione di Azure](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application Insights    |                                         | Connettore   | Connettore   | [Application Insights Connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (anteprima) |
| Account di Automazione     | Microsoft.Automation/AutomationAccounts | Diagnostica |             | [Altre informazioni](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Account Batch          | Microsoft.Batch/batchAccounts           | Diagnostica | Diagnostica | |
| Servizi cloud classici  |                                         | Archiviazione     |             | [Altre informazioni](log-analytics-azure-storage-iis-table.md) |
| Servizi cognitivi      | Microsoft.CognitiveServices/accounts    |             | Diagnostica | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnostica |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | Diagnostica |             | |
| Spazio dei nomi dell'hub eventi     | Microsoft.EventHub/namespaces           | Diagnostica | Diagnostica | |
| Hub IoT                | Microsoft.Devices/IotHubs               |             | Diagnostica | |
| Insieme di credenziali delle chiavi               | Microsoft.KeyVault/vaults               | Diagnostica |             | [KeyVault Analytics](log-analytics-azure-key-vault.md) |
| Servizi di bilanciamento del carico          | Microsoft.Network/loadBalancers         | Diagnostica |             |  |
| App per la logica              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnostica | Diagnostica | |
| Gruppi di sicurezza di rete | Microsoft.Network/networksecuritygroups | Diagnostica |             | [Analisi del gruppo di sicurezza di rete di Azure](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Insiemi di credenziali di ripristino         | Microsoft.RecoveryServices/vaults       |             |             | [Azure Recovery Services Analytics (Anteprima)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Servizi di ricerca         | Microsoft.Search/searchServices         | Diagnostica | Diagnostica | |
| Spazio dei nomi del bus di servizio   | Microsoft.ServiceBus/namespaces         | Diagnostica | Diagnostica | [Service Bus Analytics (Anteprima)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Archiviazione     |             | [Service Fabric Analytics (anteprima)](log-analytics-service-fabric.md) |
| SQL (versione 12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnostica | [Azure SQL Analytics (Anteprima)](log-analytics-azure-sql.md) |
| Archiviazione                 |                                         |             | Script      | [Azure Storage Analytics (Anteprima)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Macchine virtuali        | Microsoft.Compute/virtualMachines       | Estensione   | Estensione <br> Diagnostica  | |
| Set di scalabilità di macchine virtuali | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnostica | |
| Server farm Web        | Microsoft.Web/serverfarms               |             | Diagnostica | |
| Microsoft Azure               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnostica | [Azure Web Apps Analytics (Anteprima)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Per il monitoraggio delle macchine virtuali di Azure (Linux e Windows), si consiglia di installare hello [estensione della macchina virtuale Analitica Log](log-analytics-azure-vm-extension.md). agente Hello vengono fornite informazioni raccolte da all'interno delle macchine virtuali. È inoltre possibile utilizzare l'estensione di hello per set di scalabilità di macchine virtuali.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnostica di Azure diretto tooLog Analitica
Molte risorse di Azure sono metriche e i log di diagnostica in grado di toowrite direttamente tooLog Analitica e non è il modo preferito hello di raccolta dei dati di hello per l'analisi. Quando si utilizza diagnostica Windows Azure, dati vengono scritti immediatamente tooLog Analitica e non vi è alcun toostorage di dati necessario toofirst scrittura hello.

Risorse di Azure che supportano [monitoraggio Azure](../monitoring-and-diagnostics/monitoring-overview.md) può inviare le metriche e i log direttamente tooLog Analitica.

* Per informazioni dettagliate hello delle metriche disponibili hello, fare riferimento troppo[metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Per informazioni dettagliate sulle hello registri disponibili hello, fare riferimento troppo[supportata servizi e lo schema per i log di diagnostica](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Abilitare la diagnostica con PowerShell
È necessario hello novembre 2016 (v2.3.0) o versione successiva versione di [Azure PowerShell](/powershell/azure/overview).

Hello seguente come esempio PowerShell toouse [Set AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnostica in un gruppo di sicurezza di rete. Hello stesso approccio funziona per tutte le risorse supportate, impostato `$resourceId` id della risorsa hello da diagnostica tooenable per risorsa toohello.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Abilitare la diagnostica con modelli di Resource Manager

diagnostica tooenable su una risorsa quando viene creato e diagnostica hello inviato dell'area di lavoro di tooyour Analitica di Log che è possibile utilizzare un toohello simile modello uno di seguito. Questo esempio è riferito a un account di Automazione, ma funziona per tutti i tipi di risorse supportati.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Diagnostica di Azure toostorage quindi tooLog Analitica

Per raccogliere i log da all'interno di alcune risorse, è possibile toosend hello registri tooAzure archiviazione e quindi configurare i log di hello tooread Analitica Log dall'archiviazione.

Log Analitica può usare la diagnostica di toocollect questo approccio dall'archiviazione di Azure per hello seguenti registri e risorse:

| Risorsa | Log |
| --- | --- |
| Service Fabric |ETWEvent <br> Evento operativo <br> Evento Reliable Actor <br> Evento Reliable Service |
| Macchine virtuali |Syslog Linux <br> Evento Windows <br> Log IIS <br> ETWEvent Windows |
| Ruoli Web <br> Ruoli di lavoro |Syslog Linux <br> Evento Windows <br> Log IIS <br> ETWEvent Windows |

> [!NOTE]
> Si vengono addebitate le tariffe normali dati di Azure per l'archiviazione e le transazioni quando si invia la diagnostica tooa account di archiviazione e quando Analitica Log legge dati hello dall'account di archiviazione.
>
>

Vedere [usare l'archivio blob per l'archiviazione IIS e di tabella per gli eventi](log-analytics-azure-storage-iis-table.md) toolearn ulteriori informazioni sulla modalità Analitica Log possibile raccogliere i registri.

## <a name="connectors-for-azure-services"></a>Connettori per i servizi di Azure

È un connettore per Application Insights, che consente di dati raccolti da Application Insights toobe inviati tooLog Analitica.

Altre informazioni su hello [connettore Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Script toocollect e post dati tooLog Analitica

Per i servizi di Azure che non forniscono un tooLog metriche e i registri in modo diretto di toosend Analitica, è possibile utilizzare un toocollect di script di automazione di Azure hello log e le metriche. Hello script può quindi l'uso di trasmissione hello dati tooLog Analitica hello [API agente di raccolta dati](log-analytics-data-collector-api.md)

raccolta di modelli di Azure Hello è [esempi dell'utilizzo di automazione di Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect dati da servizi e inviarli tooLog Analitica.

## <a name="next-steps"></a>Passaggi successivi

* [Utilizzare l'archiviazione blob per l'archiviazione IIS e di tabella per gli eventi](log-analytics-azure-storage-iis-table.md) registri hello tooread per servizi di Azure che scrivono diagnostica tootable di archiviazione o IIS log scritto tooblob archiviazione.
* [Abilitare soluzioni](log-analytics-add-solutions.md) tooprovide comprendere dati hello.
* [Utilizzare le query di ricerca](log-analytics-log-searches.md) dati hello tooanalyze.
