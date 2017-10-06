---
title: aaaMigrate Azure avvisi su eventi di gestione tooActivity gli avvisi del Registro | Documenti Microsoft
description: "A partire dal 1° ottobre verranno rimossi gli avvisi relativi agli eventi di gestione. È necessario quindi prepararsi e migrare gli avvisi esistenti."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Eseguire la migrazione di Azure avvisi per gli avvisi del registro tooActivity gestione eventi


> [!WARNING]
> A partire dal 1° ottobre verranno disattivati gli avvisi relativi agli eventi di gestione. Se si dispone di questi avvisi e ne esegue la migrazione in tal caso, utilizzare le direzioni di hello sotto toounderstand.
>
> 

## <a name="what-is-changing"></a>Cosa cambierà

Monitoraggio di Azure (precedentemente Azure Insights) offerto un toocreate funzionalità un avviso generato da eventi di gestione e che ha generato le notifiche tooa webhook URL o gli indirizzi email. È possibile aver creato uno di questi avvisi in uno dei modi seguenti:
* Nel portale di Azure per determinati tipi di risorsa hello, monitoraggio -> avvisi -> Aggiungi avviso, in cui "Avviso" è troppo "Eventi"
* Il cmdlet PowerShell Add-AzureRmLogAlertRule hello in esecuzione
* Utilizzando direttamente [hello avviso API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) con OData. Type = "ManagementEventRuleCondition" e dataSource.odata.type = "RuleManagementEventDataSource"
 
Hello script PowerShell seguente restituisce un elenco di tutti gli avvisi sugli eventi di gestione presenti nella sottoscrizione, nonché le condizioni di hello impostato su ogni avviso.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

Se non sono presenti avvisi sugli eventi di gestione, cmdlet PowerShell hello precedente verrà restituito come una serie di messaggi di avviso simile alla seguente:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Questi messaggi di avviso possono essere ignorati. Se si dispone di avvisi sugli eventi di gestione, l'output di hello di questo cmdlet PowerShell sarà simile al seguente:

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Ogni avviso è separato da una linea tratteggiata e dettagli includono l'ID di risorsa hello di avviso di hello e regole di hello specifici da monitorare.

Questa funzionalità è stata eseguita la transizione troppo[gli avvisi del registro attività Monitoraggio Azure](monitoring-activity-log-alerts.md). Questi nuovi avvisi consentono tooset una condizione per eventi del registro attività e ricevano una notifica quando un nuovo evento soddisfa la condizione di hello. Gli avvisi sugli eventi di gestione presentano anche una serie di miglioramenti:
* È possibile riutilizzare il gruppo di destinatari di notifica ("azioni") in numero di avvisi tramite [gruppi di azioni](monitoring-action-groups.md), ridurre la complessità di hello di modifica che deve ricevere un avviso.
* È possibile ricevere una notifica direttamente sul telefono tramite SMS con la funzionalità Gruppi di azioni.
* È possibile [creare avvisi del log attività con i modelli di Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* È possibile creare le condizioni con maggiore flessibilità e la complessità di toomeet alle specifiche esigenze.
* Le notifiche vengono recapitate più rapidamente.
 
## <a name="how-toomigrate"></a>Come toomigrate
 
toocreate una nuova attività del Log degli avvisi, è possibile:
* Seguire [la Guida su come toocreate un avviso in hello portale di Azure](monitoring-activity-log-alerts.md)
* Informazioni su come troppo[creare un avviso utilizzando un modello di gestione risorse](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Avvisi su eventi di gestione creato in precedenza non sarà automaticamente migrati tooActivity gli avvisi del registro. È necessario hello toouse precedente avvisi hello toolist uno script di PowerShell sugli eventi di gestione che attualmente configurata e ricreare manualmente come gli avvisi del registro attività. Questa operazione deve essere eseguita entro il 1° ottobre. A partire da quella data, infatti, gli avvisi di eventi di gestione non saranno più visibili nella sottoscrizione di Azure. Altri tipi di avvisi di Azure, tra cui gli avvisi metrica di Monitoraggio di Azure, gli avvisi di Application Insights e gli avvisi di Log Analytics, non sono interessati da questa modifica. Se per eventuali domande, pubblicare un post nei commenti hello riportato di seguito.


## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sul [log attività](monitoring-overview-activity-logs.md)
* Configurare [gli avvisi del log attività tramite il portale di Azure](monitoring-activity-log-alerts.md)
* Configurare [gli avvisi del log attività tramite Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md)
* Altre informazioni sulle [notifiche del servizio](monitoring-service-notifications.md)
* Altre informazioni sui [gruppi di azione](monitoring-action-groups.md)
