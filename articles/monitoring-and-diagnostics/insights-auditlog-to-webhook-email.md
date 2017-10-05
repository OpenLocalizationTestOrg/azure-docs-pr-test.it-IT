---
title: "Chiamare un webhook negli avvisi dei log attività di Azure | Documentazione Microsoft"
description: "Instradare gli eventi del log attività ad altri servizi per azioni personalizzate. Inviare ad esempio SMS, registrare i bug o inviare notifiche al team tramite servizio di chat o messaggistica."
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
ms.openlocfilehash: 341ab32ad0ec691285fbf1537ee298ab30156a5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="1ea80-104">Chiamare un webhook negli avvisi dei log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="1ea80-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="1ea80-105">I webhook consentono di instradare le notifiche di avviso di Azure ad altri sistemi per la post-elaborazione o le azioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="1ea80-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="1ea80-106">È possibile usare un webhook in un avviso per instradarlo a servizi che inviano SMS, registrano bug, inviano notifiche a un team tramite servizi di messaggistica/chat o eseguono un numero qualsiasi di altre azioni.</span><span class="sxs-lookup"><span data-stu-id="1ea80-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="1ea80-107">Questo articolo descrive come impostare un webhook da chiamare quando viene generato un avviso dei log attività di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea80-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="1ea80-108">L'articolo illustra anche il modo in cui il payload per il protocollo HTTP POST viene percepito da un webhook.</span><span class="sxs-lookup"><span data-stu-id="1ea80-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="1ea80-109">Per informazioni sulla configurazione e lo schema di un avviso relativo alle metriche di Azure, [vedere invece questa pagina](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1ea80-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="1ea80-110">È anche possibile impostare un avviso del registro attività per l'invio di un messaggio di posta all'attivazione.</span><span class="sxs-lookup"><span data-stu-id="1ea80-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="1ea80-111">Questa funzionalità è attualmente disponibile in anteprima e verrà rimossa in futuro.</span><span class="sxs-lookup"><span data-stu-id="1ea80-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="1ea80-112">È possibile configurare un avviso del log attività usando i [cmdlet di Azure PowerShell](insights-powershell-samples.md#create-metric-alerts), l'[interfaccia della riga di comando multipiattaforma](insights-cli-samples.md#work-with-alerts) o l'[API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ea80-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="1ea80-113">Attualmente, non è possibile usare il portale di Azure per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ea80-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="1ea80-114">Autenticazione del webhook</span><span class="sxs-lookup"><span data-stu-id="1ea80-114">Authenticating the webhook</span></span>
<span data-ttu-id="1ea80-115">L'autenticazione del webhook può essere eseguita con uno di questi metodi:</span><span class="sxs-lookup"><span data-stu-id="1ea80-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="1ea80-116">**Autorizzazione basata su token**: l'URI del webhook viene salvato con un ID token, ad esempio `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="1ea80-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="1ea80-117">**Autorizzazione di base**: l'URI del webhook viene salvato con nome utente e password, ad esempio `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="1ea80-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="1ea80-118">Schema del payload</span><span class="sxs-lookup"><span data-stu-id="1ea80-118">Payload schema</span></span>
<span data-ttu-id="1ea80-119">L'operazione POST contiene il seguente payload e schema JSON per tutti gli avvisi basati sul registro attività.</span><span class="sxs-lookup"><span data-stu-id="1ea80-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="1ea80-120">Questo schema è simile a quello usato per gli avvisi basati su metriche.</span><span class="sxs-lookup"><span data-stu-id="1ea80-120">This schema is similar to the one used by metric-based alerts.</span></span>

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

| <span data-ttu-id="1ea80-121">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1ea80-121">Element Name</span></span> | <span data-ttu-id="1ea80-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ea80-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ea80-123">status</span><span class="sxs-lookup"><span data-stu-id="1ea80-123">status</span></span> |<span data-ttu-id="1ea80-124">Usato per avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="1ea80-124">Used for metric alerts.</span></span> <span data-ttu-id="1ea80-125">Sempre impostato su "Activated" per gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="1ea80-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="1ea80-126">context</span><span class="sxs-lookup"><span data-stu-id="1ea80-126">context</span></span> |<span data-ttu-id="1ea80-127">Contesto dell'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-127">Context of the event.</span></span> |
| <span data-ttu-id="1ea80-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="1ea80-128">resourceProviderName</span></span> |<span data-ttu-id="1ea80-129">Provider della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="1ea80-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="1ea80-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="1ea80-130">conditionType</span></span> |<span data-ttu-id="1ea80-131">Sempre "Event".</span><span class="sxs-lookup"><span data-stu-id="1ea80-131">Always "Event."</span></span> |
| <span data-ttu-id="1ea80-132">name</span><span class="sxs-lookup"><span data-stu-id="1ea80-132">name</span></span> |<span data-ttu-id="1ea80-133">Nome della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="1ea80-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="1ea80-134">id</span><span class="sxs-lookup"><span data-stu-id="1ea80-134">id</span></span> |<span data-ttu-id="1ea80-135">ID risorsa dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="1ea80-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="1ea80-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ea80-136">description</span></span> |<span data-ttu-id="1ea80-137">Descrizione dell'avviso definita durante la creazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="1ea80-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="1ea80-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1ea80-138">subscriptionId</span></span> |<span data-ttu-id="1ea80-139">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea80-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="1ea80-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="1ea80-140">timestamp</span></span> |<span data-ttu-id="1ea80-141">Data e ora in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta.</span><span class="sxs-lookup"><span data-stu-id="1ea80-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="1ea80-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="1ea80-142">resourceId</span></span> |<span data-ttu-id="1ea80-143">ID risorsa della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="1ea80-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="1ea80-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1ea80-144">resourceGroupName</span></span> |<span data-ttu-id="1ea80-145">Nome del gruppo di risorse della risorsa interessata</span><span class="sxs-lookup"><span data-stu-id="1ea80-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="1ea80-146">properties</span><span class="sxs-lookup"><span data-stu-id="1ea80-146">properties</span></span> |<span data-ttu-id="1ea80-147">Set di coppie `<Key, Value>`, ad esempio `Dictionary<String, String>`, contenente i dettagli relativi all'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="1ea80-148">event</span><span class="sxs-lookup"><span data-stu-id="1ea80-148">event</span></span> |<span data-ttu-id="1ea80-149">Elemento contenente i metadati relativi all'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="1ea80-150">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="1ea80-150">authorization</span></span> |<span data-ttu-id="1ea80-151">Proprietà di Controllo degli accessi in base al ruolo dell'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-151">The RBAC properties of the event.</span></span> <span data-ttu-id="1ea80-152">Includono in genere "action", "role" e "scope".</span><span class="sxs-lookup"><span data-stu-id="1ea80-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="1ea80-153">category</span><span class="sxs-lookup"><span data-stu-id="1ea80-153">category</span></span> |<span data-ttu-id="1ea80-154">Categoria dell'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-154">Category of the event.</span></span> <span data-ttu-id="1ea80-155">I valori supportati includono Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="1ea80-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="1ea80-156">caller</span><span class="sxs-lookup"><span data-stu-id="1ea80-156">caller</span></span> |<span data-ttu-id="1ea80-157">Indirizzo di posta elettronica dell'utente che ha eseguito l'operazione, attestazione UPN o attestazione SPN, a seconda della disponibilità.</span><span class="sxs-lookup"><span data-stu-id="1ea80-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="1ea80-158">Può essere null per alcune chiamate di sistema.</span><span class="sxs-lookup"><span data-stu-id="1ea80-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="1ea80-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="1ea80-159">correlationId</span></span> |<span data-ttu-id="1ea80-160">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="1ea80-160">Usually a GUID in string format.</span></span> <span data-ttu-id="1ea80-161">Gli eventi con correlationId appartengono alla stessa azione di livello superiore e in genere condividono un elemento correlationId.</span><span class="sxs-lookup"><span data-stu-id="1ea80-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="1ea80-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="1ea80-162">eventDescription</span></span> |<span data-ttu-id="1ea80-163">Testo statico che descrive l'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-163">Static text description of the event.</span></span> |
| <span data-ttu-id="1ea80-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="1ea80-164">eventDataId</span></span> |<span data-ttu-id="1ea80-165">Identificatore univoco dell'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="1ea80-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="1ea80-166">eventSource</span></span> |<span data-ttu-id="1ea80-167">Nome del servizio o dell'infrastruttura di Azure che ha generato l'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="1ea80-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="1ea80-168">httpRequest</span></span> |<span data-ttu-id="1ea80-169">In genere include "clientRequestId", "clientIpAddress" e "method" (metodo HTTP, ad esempio PUT).</span><span class="sxs-lookup"><span data-stu-id="1ea80-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="1ea80-170">level</span><span class="sxs-lookup"><span data-stu-id="1ea80-170">level</span></span> |<span data-ttu-id="1ea80-171">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose".</span><span class="sxs-lookup"><span data-stu-id="1ea80-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="1ea80-172">operationId</span><span class="sxs-lookup"><span data-stu-id="1ea80-172">operationId</span></span> |<span data-ttu-id="1ea80-173">In genere un GUID condiviso tra gli eventi corrispondenti a una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="1ea80-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="1ea80-174">operationName</span><span class="sxs-lookup"><span data-stu-id="1ea80-174">operationName</span></span> |<span data-ttu-id="1ea80-175">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="1ea80-175">Name of the operation.</span></span> |
| <span data-ttu-id="1ea80-176">properties</span><span class="sxs-lookup"><span data-stu-id="1ea80-176">properties</span></span> |<span data-ttu-id="1ea80-177">Proprietà dell'evento.</span><span class="sxs-lookup"><span data-stu-id="1ea80-177">Properties of the event.</span></span> |
| <span data-ttu-id="1ea80-178">status</span><span class="sxs-lookup"><span data-stu-id="1ea80-178">status</span></span> |<span data-ttu-id="1ea80-179">Stringa.</span><span class="sxs-lookup"><span data-stu-id="1ea80-179">String.</span></span> <span data-ttu-id="1ea80-180">Stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="1ea80-180">Status of the operation.</span></span> <span data-ttu-id="1ea80-181">I valori comuni includono: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="1ea80-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="1ea80-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="1ea80-182">subStatus</span></span> |<span data-ttu-id="1ea80-183">In genere include il codice di stato HTTP della chiamata REST corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1ea80-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="1ea80-184">Può includere anche altre stringhe che descrivono uno stato secondario.</span><span class="sxs-lookup"><span data-stu-id="1ea80-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="1ea80-185">I valori di stato secondario comuni includono: OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="1ea80-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1ea80-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ea80-186">Next steps</span></span>
* [<span data-ttu-id="1ea80-187">Altre informazioni sul log attività</span><span class="sxs-lookup"><span data-stu-id="1ea80-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="1ea80-188">Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure</span><span class="sxs-lookup"><span data-stu-id="1ea80-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="1ea80-189">[Usare l'app per la logica per inviare SMS tramite Twilio da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="1ea80-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="1ea80-190">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del registro attività.</span><span class="sxs-lookup"><span data-stu-id="1ea80-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="1ea80-191">[Usare l'app per la logica per inviare un messaggio Slack da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="1ea80-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="1ea80-192">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del registro attività.</span><span class="sxs-lookup"><span data-stu-id="1ea80-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="1ea80-193">[Usare l'app per la logica per inviare un messaggio a una coda di Azure da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="1ea80-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="1ea80-194">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del registro attività.</span><span class="sxs-lookup"><span data-stu-id="1ea80-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
