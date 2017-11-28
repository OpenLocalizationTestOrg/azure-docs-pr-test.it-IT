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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="442dd-104">Eseguire la migrazione di Azure avvisi per gli avvisi del registro tooActivity gestione eventi</span><span class="sxs-lookup"><span data-stu-id="442dd-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="442dd-105">A partire dal 1° ottobre verranno disattivati gli avvisi relativi agli eventi di gestione.</span><span class="sxs-lookup"><span data-stu-id="442dd-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="442dd-106">Se si dispone di questi avvisi e ne esegue la migrazione in tal caso, utilizzare le direzioni di hello sotto toounderstand.</span><span class="sxs-lookup"><span data-stu-id="442dd-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="442dd-107">Cosa cambierà</span><span class="sxs-lookup"><span data-stu-id="442dd-107">What is changing</span></span>

<span data-ttu-id="442dd-108">Monitoraggio di Azure (precedentemente Azure Insights) offerto un toocreate funzionalità un avviso generato da eventi di gestione e che ha generato le notifiche tooa webhook URL o gli indirizzi email.</span><span class="sxs-lookup"><span data-stu-id="442dd-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="442dd-109">È possibile aver creato uno di questi avvisi in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="442dd-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="442dd-110">Nel portale di Azure per determinati tipi di risorsa hello, monitoraggio -> avvisi -> Aggiungi avviso, in cui "Avviso" è troppo "Eventi"</span><span class="sxs-lookup"><span data-stu-id="442dd-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="442dd-111">Il cmdlet PowerShell Add-AzureRmLogAlertRule hello in esecuzione</span><span class="sxs-lookup"><span data-stu-id="442dd-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="442dd-112">Utilizzando direttamente [hello avviso API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) con OData. Type = "ManagementEventRuleCondition" e dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="442dd-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="442dd-113">Hello script PowerShell seguente restituisce un elenco di tutti gli avvisi sugli eventi di gestione presenti nella sottoscrizione, nonché le condizioni di hello impostato su ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="442dd-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="442dd-114">Se non sono presenti avvisi sugli eventi di gestione, cmdlet PowerShell hello precedente verrà restituito come una serie di messaggi di avviso simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="442dd-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="442dd-115">Questi messaggi di avviso possono essere ignorati.</span><span class="sxs-lookup"><span data-stu-id="442dd-115">These warning messages can be ignored.</span></span> <span data-ttu-id="442dd-116">Se si dispone di avvisi sugli eventi di gestione, l'output di hello di questo cmdlet PowerShell sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="442dd-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="442dd-117">Ogni avviso è separato da una linea tratteggiata e dettagli includono l'ID di risorsa hello di avviso di hello e regole di hello specifici da monitorare.</span><span class="sxs-lookup"><span data-stu-id="442dd-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="442dd-118">Questa funzionalità è stata eseguita la transizione troppo[gli avvisi del registro attività Monitoraggio Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="442dd-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="442dd-119">Questi nuovi avvisi consentono tooset una condizione per eventi del registro attività e ricevano una notifica quando un nuovo evento soddisfa la condizione di hello.</span><span class="sxs-lookup"><span data-stu-id="442dd-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="442dd-120">Gli avvisi sugli eventi di gestione presentano anche una serie di miglioramenti:</span><span class="sxs-lookup"><span data-stu-id="442dd-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="442dd-121">È possibile riutilizzare il gruppo di destinatari di notifica ("azioni") in numero di avvisi tramite [gruppi di azioni](monitoring-action-groups.md), ridurre la complessità di hello di modifica che deve ricevere un avviso.</span><span class="sxs-lookup"><span data-stu-id="442dd-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="442dd-122">È possibile ricevere una notifica direttamente sul telefono tramite SMS con la funzionalità Gruppi di azioni.</span><span class="sxs-lookup"><span data-stu-id="442dd-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="442dd-123">È possibile [creare avvisi del log attività con i modelli di Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="442dd-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="442dd-124">È possibile creare le condizioni con maggiore flessibilità e la complessità di toomeet alle specifiche esigenze.</span><span class="sxs-lookup"><span data-stu-id="442dd-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="442dd-125">Le notifiche vengono recapitate più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="442dd-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="442dd-126">Come toomigrate</span><span class="sxs-lookup"><span data-stu-id="442dd-126">How toomigrate</span></span>
 
<span data-ttu-id="442dd-127">toocreate una nuova attività del Log degli avvisi, è possibile:</span><span class="sxs-lookup"><span data-stu-id="442dd-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="442dd-128">Seguire [la Guida su come toocreate un avviso in hello portale di Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="442dd-129">Informazioni su come troppo[creare un avviso utilizzando un modello di gestione risorse](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="442dd-130">Avvisi su eventi di gestione creato in precedenza non sarà automaticamente migrati tooActivity gli avvisi del registro.</span><span class="sxs-lookup"><span data-stu-id="442dd-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="442dd-131">È necessario hello toouse precedente avvisi hello toolist uno script di PowerShell sugli eventi di gestione che attualmente configurata e ricreare manualmente come gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="442dd-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="442dd-132">Questa operazione deve essere eseguita entro il 1° ottobre. A partire da quella data, infatti, gli avvisi di eventi di gestione non saranno più visibili nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="442dd-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="442dd-133">Altri tipi di avvisi di Azure, tra cui gli avvisi metrica di Monitoraggio di Azure, gli avvisi di Application Insights e gli avvisi di Log Analytics, non sono interessati da questa modifica.</span><span class="sxs-lookup"><span data-stu-id="442dd-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="442dd-134">Se per eventuali domande, pubblicare un post nei commenti hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="442dd-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="442dd-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="442dd-135">Next steps</span></span>

* <span data-ttu-id="442dd-136">Altre informazioni sul [log attività](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="442dd-137">Configurare [gli avvisi del log attività tramite il portale di Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="442dd-138">Configurare [gli avvisi del log attività tramite Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="442dd-139">Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="442dd-140">Altre informazioni sulle [notifiche del servizio](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="442dd-141">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="442dd-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
