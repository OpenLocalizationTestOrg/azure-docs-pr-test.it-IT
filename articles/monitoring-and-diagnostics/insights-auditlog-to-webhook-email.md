---
title: "aaaCall un webhook sugli avvisi di Log attività di Azure | Documenti Microsoft"
description: "Route servizi attività di log eventi tooother per le azioni personalizzate. Inviare ad esempio SMS, registrare i bug o inviare notifiche al team tramite servizio di chat o messaggistica."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="75c0c-104">Chiamare un webhook negli avvisi dei log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="75c0c-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="75c0c-105">Webhook consentono di Azure tooroute sistemi tooother di notifica per le azioni di post-elaborazione o personalizzati di avviso.</span><span class="sxs-lookup"><span data-stu-id="75c0c-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="75c0c-106">È possibile utilizzare un webhook su un avviso tooroute è tooservices che invia SMS, registrare i bug, inviare una notifica di un team tramite servizi di chat o messaggistica o eseguire un numero qualsiasi di altre azioni.</span><span class="sxs-lookup"><span data-stu-id="75c0c-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="75c0c-107">In questo articolo viene descritto come tooset toobe un webhook chiamato quando un generato avvisi di Log attività di Azure.</span><span class="sxs-lookup"><span data-stu-id="75c0c-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="75c0c-108">Viene inoltre illustrato il payload di hello per hello HTTP POST tooa webhook è simile.</span><span class="sxs-lookup"><span data-stu-id="75c0c-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="75c0c-109">Per informazioni sull'installazione di hello e lo schema per un avviso metrica Azure [questa pagina viene visualizzata invece](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="75c0c-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="75c0c-110">È inoltre possibile impostare un messaggio di avviso toosend Log attività quando attivato.</span><span class="sxs-lookup"><span data-stu-id="75c0c-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="75c0c-111">Questa funzionalità è attualmente in anteprima e verrà rimossa in un determinato hello future.</span><span class="sxs-lookup"><span data-stu-id="75c0c-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="75c0c-112">È possibile impostare un avviso di Log attività utilizzando hello [i cmdlet di PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI multipiattaforma](insights-cli-samples.md#work-with-alerts), o [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="75c0c-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="75c0c-113">Attualmente, non è possibile impostare uno utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="75c0c-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="75c0c-114">L'autenticazione hello webhook</span><span class="sxs-lookup"><span data-stu-id="75c0c-114">Authenticating hello webhook</span></span>
<span data-ttu-id="75c0c-115">Hello webhook autenticazione utilizzando uno dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="75c0c-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="75c0c-116">**Autorizzazione basata su token** -hello webhook URI viene salvato con un ID del token, ad esempio,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="75c0c-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="75c0c-117">**Autorizzazione di base** -hello webhook URI viene salvato con un nome utente e password, ad esempio,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="75c0c-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="75c0c-118">Schema del payload</span><span class="sxs-lookup"><span data-stu-id="75c0c-118">Payload schema</span></span>
<span data-ttu-id="75c0c-119">operazione POST Hello contiene hello seguito payload JSON e lo schema per gli avvisi basati su Log attività.</span><span class="sxs-lookup"><span data-stu-id="75c0c-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="75c0c-120">Questo schema è simile toohello utilizzato da avvisi basati sulla metrica.</span><span class="sxs-lookup"><span data-stu-id="75c0c-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="75c0c-121">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="75c0c-121">Element Name</span></span> | <span data-ttu-id="75c0c-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="75c0c-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75c0c-123">status</span><span class="sxs-lookup"><span data-stu-id="75c0c-123">status</span></span> |<span data-ttu-id="75c0c-124">Usato per avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="75c0c-124">Used for metric alerts.</span></span> <span data-ttu-id="75c0c-125">Impostare sempre troppo "attivato" per gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="75c0c-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="75c0c-126">context</span><span class="sxs-lookup"><span data-stu-id="75c0c-126">context</span></span> |<span data-ttu-id="75c0c-127">Contesto dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-127">Context of hello event.</span></span> |
| <span data-ttu-id="75c0c-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="75c0c-128">resourceProviderName</span></span> |<span data-ttu-id="75c0c-129">provider di risorse Hello di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="75c0c-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="75c0c-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="75c0c-130">conditionType</span></span> |<span data-ttu-id="75c0c-131">Sempre "Event".</span><span class="sxs-lookup"><span data-stu-id="75c0c-131">Always "Event."</span></span> |
| <span data-ttu-id="75c0c-132">name</span><span class="sxs-lookup"><span data-stu-id="75c0c-132">name</span></span> |<span data-ttu-id="75c0c-133">Nome della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="75c0c-134">id</span><span class="sxs-lookup"><span data-stu-id="75c0c-134">id</span></span> |<span data-ttu-id="75c0c-135">ID risorsa dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="75c0c-136">description</span><span class="sxs-lookup"><span data-stu-id="75c0c-136">description</span></span> |<span data-ttu-id="75c0c-137">Descrizione avviso durante la creazione dell'avviso hello come set.</span><span class="sxs-lookup"><span data-stu-id="75c0c-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="75c0c-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="75c0c-138">subscriptionId</span></span> |<span data-ttu-id="75c0c-139">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75c0c-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="75c0c-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="75c0c-140">timestamp</span></span> |<span data-ttu-id="75c0c-141">Ora in cui hello è stato generato l'evento dal servizio di Azure che ha elaborato la richiesta hello hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="75c0c-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="75c0c-142">resourceId</span></span> |<span data-ttu-id="75c0c-143">ID di risorsa di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="75c0c-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="75c0c-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="75c0c-144">resourceGroupName</span></span> |<span data-ttu-id="75c0c-145">Nome del gruppo di risorse hello per hello interessati risorsa</span><span class="sxs-lookup"><span data-stu-id="75c0c-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="75c0c-146">properties</span><span class="sxs-lookup"><span data-stu-id="75c0c-146">properties</span></span> |<span data-ttu-id="75c0c-147">Set di `<Key, Value>` coppie (ad esempio `Dictionary<String, String>`) che include i dettagli sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="75c0c-148">event</span><span class="sxs-lookup"><span data-stu-id="75c0c-148">event</span></span> |<span data-ttu-id="75c0c-149">Elemento che contiene i metadati sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="75c0c-150">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="75c0c-150">authorization</span></span> |<span data-ttu-id="75c0c-151">proprietà RBAC Hello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="75c0c-152">In genere includono hello "action" e "ruolo" hello "ambito".</span><span class="sxs-lookup"><span data-stu-id="75c0c-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="75c0c-153">category</span><span class="sxs-lookup"><span data-stu-id="75c0c-153">category</span></span> |<span data-ttu-id="75c0c-154">Categoria di eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-154">Category of hello event.</span></span> <span data-ttu-id="75c0c-155">I valori supportati includono Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="75c0c-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="75c0c-156">caller</span><span class="sxs-lookup"><span data-stu-id="75c0c-156">caller</span></span> |<span data-ttu-id="75c0c-157">Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="75c0c-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="75c0c-158">Può essere null per alcune chiamate di sistema.</span><span class="sxs-lookup"><span data-stu-id="75c0c-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="75c0c-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="75c0c-159">correlationId</span></span> |<span data-ttu-id="75c0c-160">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="75c0c-160">Usually a GUID in string format.</span></span> <span data-ttu-id="75c0c-161">Gli eventi con ID correlazione appartengono toohello stessa azione di dimensioni maggiori e in genere condividono un ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="75c0c-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="75c0c-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="75c0c-162">eventDescription</span></span> |<span data-ttu-id="75c0c-163">Descrizione di testo statico dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="75c0c-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="75c0c-164">eventDataId</span></span> |<span data-ttu-id="75c0c-165">Identificatore univoco per l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="75c0c-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="75c0c-166">eventSource</span></span> |<span data-ttu-id="75c0c-167">Nome di hello Azure servizio o dell'infrastruttura che l'evento generato hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="75c0c-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="75c0c-168">httpRequest</span></span> |<span data-ttu-id="75c0c-169">In genere include hello "clientRequestId", "clientIpAddress" e "method" (il metodo HTTP, ad esempio PUT).</span><span class="sxs-lookup"><span data-stu-id="75c0c-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="75c0c-170">level</span><span class="sxs-lookup"><span data-stu-id="75c0c-170">level</span></span> |<span data-ttu-id="75c0c-171">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose".</span><span class="sxs-lookup"><span data-stu-id="75c0c-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="75c0c-172">operationId</span><span class="sxs-lookup"><span data-stu-id="75c0c-172">operationId</span></span> |<span data-ttu-id="75c0c-173">In genere un GUID condiviso tra gli eventi di hello toosingle operazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="75c0c-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="75c0c-174">operationName</span><span class="sxs-lookup"><span data-stu-id="75c0c-174">operationName</span></span> |<span data-ttu-id="75c0c-175">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-175">Name of hello operation.</span></span> |
| <span data-ttu-id="75c0c-176">properties</span><span class="sxs-lookup"><span data-stu-id="75c0c-176">properties</span></span> |<span data-ttu-id="75c0c-177">Proprietà di evento hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-177">Properties of hello event.</span></span> |
| <span data-ttu-id="75c0c-178">status</span><span class="sxs-lookup"><span data-stu-id="75c0c-178">status</span></span> |<span data-ttu-id="75c0c-179">Stringa.</span><span class="sxs-lookup"><span data-stu-id="75c0c-179">String.</span></span> <span data-ttu-id="75c0c-180">Stato dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-180">Status of hello operation.</span></span> <span data-ttu-id="75c0c-181">I valori comuni includono: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="75c0c-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="75c0c-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="75c0c-182">subStatus</span></span> |<span data-ttu-id="75c0c-183">In genere include codice di stato HTTP hello della chiamata REST corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="75c0c-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="75c0c-184">Può includere anche altre stringhe che descrivono uno stato secondario.</span><span class="sxs-lookup"><span data-stu-id="75c0c-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="75c0c-185">I valori di stato secondario comuni includono: OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="75c0c-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="75c0c-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75c0c-186">Next steps</span></span>
* [<span data-ttu-id="75c0c-187">Altre informazioni su hello Log attività</span><span class="sxs-lookup"><span data-stu-id="75c0c-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="75c0c-188">Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure</span><span class="sxs-lookup"><span data-stu-id="75c0c-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="75c0c-189">[Utilizzare la logica App toosend un SMS tramite Twilio da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="75c0c-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="75c0c-190">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.</span><span class="sxs-lookup"><span data-stu-id="75c0c-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="75c0c-191">[Utilizzare la logica App toosend un messaggio da un avviso Azure Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="75c0c-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="75c0c-192">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.</span><span class="sxs-lookup"><span data-stu-id="75c0c-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="75c0c-193">[Utilizzare la logica App toosend tooan un messaggio della coda di Azure da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="75c0c-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="75c0c-194">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.</span><span class="sxs-lookup"><span data-stu-id="75c0c-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
