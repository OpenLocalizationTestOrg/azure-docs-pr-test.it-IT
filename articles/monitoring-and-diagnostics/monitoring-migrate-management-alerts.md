---
title: "Eseguire la migrazione di avvisi di Azure su eventi di gestione in avvisi del log attività | Microsoft Docs"
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
ms.openlocfilehash: 08a457029d3721f5c38dbcd2d2aab7d09a241d8f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="a407f-104">Eseguire la migrazione di avvisi di Azure su eventi di gestione in avvisi del log attività</span><span class="sxs-lookup"><span data-stu-id="a407f-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="a407f-105">A partire dal 1° ottobre verranno disattivati gli avvisi relativi agli eventi di gestione.</span><span class="sxs-lookup"><span data-stu-id="a407f-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="a407f-106">Usare le istruzioni seguenti per capire se si hanno questi avvisi ed eventualmente eseguirne la migrazione.</span><span class="sxs-lookup"><span data-stu-id="a407f-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="a407f-107">Cosa cambierà</span><span class="sxs-lookup"><span data-stu-id="a407f-107">What is changing</span></span>

<span data-ttu-id="a407f-108">Monitoraggio di Azure (in precedenza Azure Insights) offriva una funzionalità per la creazione di un avviso che attivasse eventi di gestione e generasse notifiche all'URL di un webhook o a un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a407f-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="a407f-109">È possibile aver creato uno di questi avvisi in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a407f-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="a407f-110">Nel portale di Azure per determinati tipi di risorsa, in Monitoraggio -> Avvisi -> Aggiungi avviso, impostando "Avviso per" su "Eventi"</span><span class="sxs-lookup"><span data-stu-id="a407f-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="a407f-111">Eseguendo il cmdlet di PowerShell Add-AzureRmLogAlertRule</span><span class="sxs-lookup"><span data-stu-id="a407f-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="a407f-112">Usando direttamente l'[API REST per gli avvisi](http://docs.microsoft.com/rest/api/monitor/alertrules) con odata.type = "ManagementEventRuleCondition" e dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="a407f-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="a407f-113">Lo script di PowerShell seguente restituisce un elenco di tutti gli avvisi relativi ad eventi di gestione presenti nella sottoscrizione personale, oltre alle condizioni impostate su ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="a407f-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

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

<span data-ttu-id="a407f-114">Se non sono presenti avvisi relativi ad eventi di gestione, il cmdlet di PowerShell restituirà una serie di messaggi di avviso simili al seguente:</span><span class="sxs-lookup"><span data-stu-id="a407f-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="a407f-115">Questi messaggi di avviso possono essere ignorati.</span><span class="sxs-lookup"><span data-stu-id="a407f-115">These warning messages can be ignored.</span></span> <span data-ttu-id="a407f-116">Se invece sono presenti avvisi relativi ad eventi di gestione, l'output del cmdlet di PowerShell sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a407f-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="a407f-117">Gli avvisi sono separati tra loro da una linea tratteggiata e includono una serie di dettagli, tra cui l'ID risorsa dell'avviso e la regola specifica da monitorare.</span><span class="sxs-lookup"><span data-stu-id="a407f-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="a407f-118">Questa funzionalità è stata integrata negli [avvisi del log attività di Monitoraggio di Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a407f-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="a407f-119">Questi nuovi avvisi consentono di impostare una condizione sugli eventi del log attività e di ricevere una notifica nel momento in cui un nuovo evento soddisfa la condizione definita.</span><span class="sxs-lookup"><span data-stu-id="a407f-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="a407f-120">Gli avvisi sugli eventi di gestione presentano anche una serie di miglioramenti:</span><span class="sxs-lookup"><span data-stu-id="a407f-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="a407f-121">È possibile riusare il gruppo di destinatari di una notifica ("azioni") anche in altri avvisi tramite [Gruppi di azioni](monitoring-action-groups.md), in modo da ridurre la necessità di definire ogni volta gli utenti che devono ricevere un avviso.</span><span class="sxs-lookup"><span data-stu-id="a407f-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="a407f-122">È possibile ricevere una notifica direttamente sul telefono tramite SMS con la funzionalità Gruppi di azioni.</span><span class="sxs-lookup"><span data-stu-id="a407f-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="a407f-123">È possibile [creare avvisi del log attività con i modelli di Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a407f-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="a407f-124">È possibile creare condizioni più flessibili e complesse per soddisfare esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="a407f-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="a407f-125">Le notifiche vengono recapitate più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a407f-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="a407f-126">Come eseguire la migrazione</span><span class="sxs-lookup"><span data-stu-id="a407f-126">How to migrate</span></span>
 
<span data-ttu-id="a407f-127">Per creare un nuovo avviso del log attività, è possibile:</span><span class="sxs-lookup"><span data-stu-id="a407f-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="a407f-128">Seguire le [istruzioni su come creare un avviso nel portale di Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="a407f-129">Imparare a [creare un avviso usando un modello di Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="a407f-130">Gli avvisi di eventi di gestione creati in precedenza non verranno automaticamente migrati in avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="a407f-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="a407f-131">Usando lo script di PowerShell precedente, è necessario invece elencare gli avvisi di eventi di gestione attualmente configurati e ricrearli manualmente come avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="a407f-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="a407f-132">Questa operazione deve essere eseguita entro il 1° ottobre. A partire da quella data, infatti, gli avvisi di eventi di gestione non saranno più visibili nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a407f-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="a407f-133">Altri tipi di avvisi di Azure, tra cui gli avvisi metrica di Monitoraggio di Azure, gli avvisi di Application Insights e gli avvisi di Log Analytics, non sono interessati da questa modifica.</span><span class="sxs-lookup"><span data-stu-id="a407f-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="a407f-134">Per eventuali domande, aggiungerle ai commenti al termine dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="a407f-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a407f-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a407f-135">Next steps</span></span>

* <span data-ttu-id="a407f-136">Altre informazioni sul [log attività](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="a407f-137">Configurare [gli avvisi del log attività tramite il portale di Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="a407f-138">Configurare [gli avvisi del log attività tramite Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="a407f-139">Esaminare lo [schema webhook degli avvisi del log attività](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="a407f-140">Altre informazioni sulle [notifiche del servizio](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="a407f-141">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
