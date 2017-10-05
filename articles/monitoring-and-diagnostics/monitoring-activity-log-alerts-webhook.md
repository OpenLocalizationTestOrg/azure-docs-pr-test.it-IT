---
title: "Informazioni sullo schema webhook degli avvisi del log attività | Microsoft Docs"
description: "Informazioni sullo schema del formato JSON che viene pubblicato in un URL del webhook all'attivazione di un avviso del log attività."
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="5a75c-103">Webhook per gli avvisi del log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="5a75c-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="5a75c-104">Nella definizione di un gruppo di azione è possibile configurare gli endpoint webhook in modo da ricevere le notifiche per gli avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="5a75c-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="5a75c-105">Con i webhook è possibile instradare queste notifiche ad altri sistemi per la post-elaborazione o azioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="5a75c-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="5a75c-106">L'articolo illustra anche il modo in cui il payload per il protocollo HTTP POST viene percepito da un webhook.</span><span class="sxs-lookup"><span data-stu-id="5a75c-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="5a75c-107">Per altre informazioni sugli avvisi del log di attività, vedere come [creare gli avvisi del log attività di Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5a75c-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="5a75c-108">Per informazioni su gruppi di azioni, vedere come [creare gruppi di azioni](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5a75c-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="5a75c-109">Autenticazione del webhook</span><span class="sxs-lookup"><span data-stu-id="5a75c-109">Authenticate the webhook</span></span>
<span data-ttu-id="5a75c-110">Facoltativamente il webhook può usare l'autorizzazione basata su token per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5a75c-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="5a75c-111">L'URI del webhook viene salvato con un ID token, ad esempio `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="5a75c-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="5a75c-112">Schema del payload</span><span class="sxs-lookup"><span data-stu-id="5a75c-112">Payload schema</span></span>
<span data-ttu-id="5a75c-113">Il payload JSON contenuto nell'operazione POST varia a seconda del campo data.context.activityLog.eventSource del payload.</span><span class="sxs-lookup"><span data-stu-id="5a75c-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="5a75c-114">Comune</span><span class="sxs-lookup"><span data-stu-id="5a75c-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="5a75c-115">Amministrativo</span><span class="sxs-lookup"><span data-stu-id="5a75c-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="5a75c-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="5a75c-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="5a75c-117">Per i dettagli su schemi specifici relativi agli avvisi del log attività per le notifiche sull'integrità del servizio, vedere [Notifiche sull'integrità del servizio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="5a75c-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="5a75c-118">Per i dettagli su schemi specifici relativi a tutti gli altri avvisi del log attività, vedere [Panoramica del log attività di Azure](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5a75c-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="5a75c-119">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="5a75c-119">Element name</span></span> | <span data-ttu-id="5a75c-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5a75c-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a75c-121">status</span><span class="sxs-lookup"><span data-stu-id="5a75c-121">status</span></span> |<span data-ttu-id="5a75c-122">Usato per avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="5a75c-122">Used for metric alerts.</span></span> <span data-ttu-id="5a75c-123">Sempre impostato su "Activated" per gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="5a75c-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="5a75c-124">context</span><span class="sxs-lookup"><span data-stu-id="5a75c-124">context</span></span> |<span data-ttu-id="5a75c-125">Contesto dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-125">Context of the event.</span></span> |
| <span data-ttu-id="5a75c-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="5a75c-126">resourceProviderName</span></span> |<span data-ttu-id="5a75c-127">Provider della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="5a75c-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="5a75c-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="5a75c-128">conditionType</span></span> |<span data-ttu-id="5a75c-129">Sempre "Event".</span><span class="sxs-lookup"><span data-stu-id="5a75c-129">Always "Event."</span></span> |
| <span data-ttu-id="5a75c-130">name</span><span class="sxs-lookup"><span data-stu-id="5a75c-130">name</span></span> |<span data-ttu-id="5a75c-131">Nome della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="5a75c-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="5a75c-132">id</span><span class="sxs-lookup"><span data-stu-id="5a75c-132">id</span></span> |<span data-ttu-id="5a75c-133">ID risorsa dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="5a75c-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="5a75c-134">description</span><span class="sxs-lookup"><span data-stu-id="5a75c-134">description</span></span> |<span data-ttu-id="5a75c-135">Descrizione dell'avviso impostata al momento della creazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="5a75c-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="5a75c-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5a75c-136">subscriptionId</span></span> |<span data-ttu-id="5a75c-137">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a75c-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="5a75c-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="5a75c-138">timestamp</span></span> |<span data-ttu-id="5a75c-139">Data e ora in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta.</span><span class="sxs-lookup"><span data-stu-id="5a75c-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="5a75c-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="5a75c-140">resourceId</span></span> |<span data-ttu-id="5a75c-141">ID risorsa della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="5a75c-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="5a75c-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5a75c-142">resourceGroupName</span></span> |<span data-ttu-id="5a75c-143">Nome del gruppo di risorse della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="5a75c-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="5a75c-144">properties</span><span class="sxs-lookup"><span data-stu-id="5a75c-144">properties</span></span> |<span data-ttu-id="5a75c-145">Set di coppie `<Key, Value>` (cioè `Dictionary<String, String>`), inclusi dettagli relativi all'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="5a75c-146">event</span><span class="sxs-lookup"><span data-stu-id="5a75c-146">event</span></span> |<span data-ttu-id="5a75c-147">Elemento contenente i metadati relativi all'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="5a75c-148">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="5a75c-148">authorization</span></span> |<span data-ttu-id="5a75c-149">Proprietà di controllo degli accessi in base al ruolo per l'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="5a75c-150">Queste proprietà includono in genere action, role e scope.</span><span class="sxs-lookup"><span data-stu-id="5a75c-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="5a75c-151">category</span><span class="sxs-lookup"><span data-stu-id="5a75c-151">category</span></span> |<span data-ttu-id="5a75c-152">Categoria dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-152">Category of the event.</span></span> <span data-ttu-id="5a75c-153">I valori supportati includono Administrative, Alert, Security, ServiceHealth e Recommendation.</span><span class="sxs-lookup"><span data-stu-id="5a75c-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="5a75c-154">caller</span><span class="sxs-lookup"><span data-stu-id="5a75c-154">caller</span></span> |<span data-ttu-id="5a75c-155">Indirizzo di posta elettronica dell'utente che ha eseguito l'operazione, attestazione UPN o attestazione SPN, a seconda della disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5a75c-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="5a75c-156">Può essere null per alcune chiamate di sistema.</span><span class="sxs-lookup"><span data-stu-id="5a75c-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="5a75c-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="5a75c-157">correlationId</span></span> |<span data-ttu-id="5a75c-158">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="5a75c-158">Usually a GUID in string format.</span></span> <span data-ttu-id="5a75c-159">Gli eventi con correlationId appartengono alla stessa azione di livello superiore e in genere condividono un elemento correlationId.</span><span class="sxs-lookup"><span data-stu-id="5a75c-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="5a75c-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="5a75c-160">eventDescription</span></span> |<span data-ttu-id="5a75c-161">Testo statico che descrive l'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-161">Static text description of the event.</span></span> |
| <span data-ttu-id="5a75c-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="5a75c-162">eventDataId</span></span> |<span data-ttu-id="5a75c-163">Identificatore univoco dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="5a75c-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="5a75c-164">eventSource</span></span> |<span data-ttu-id="5a75c-165">Nome del servizio o dell'infrastruttura di Azure che ha generato l'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="5a75c-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="5a75c-166">httpRequest</span></span> |<span data-ttu-id="5a75c-167">La richiesta in genere include clientRequestId, clientIpAddress e method HTTP, ad esempio PUT.</span><span class="sxs-lookup"><span data-stu-id="5a75c-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="5a75c-168">level</span><span class="sxs-lookup"><span data-stu-id="5a75c-168">level</span></span> |<span data-ttu-id="5a75c-169">Uno dei valori seguenti: Critical, Error, Warning, Informational e Verbose.</span><span class="sxs-lookup"><span data-stu-id="5a75c-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="5a75c-170">operationId</span><span class="sxs-lookup"><span data-stu-id="5a75c-170">operationId</span></span> |<span data-ttu-id="5a75c-171">In genere un GUID condiviso tra gli eventi corrispondenti a una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="5a75c-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="5a75c-172">operationName</span><span class="sxs-lookup"><span data-stu-id="5a75c-172">operationName</span></span> |<span data-ttu-id="5a75c-173">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="5a75c-173">Name of the operation.</span></span> |
| <span data-ttu-id="5a75c-174">properties</span><span class="sxs-lookup"><span data-stu-id="5a75c-174">properties</span></span> |<span data-ttu-id="5a75c-175">Proprietà dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5a75c-175">Properties of the event.</span></span> |
| <span data-ttu-id="5a75c-176">status</span><span class="sxs-lookup"><span data-stu-id="5a75c-176">status</span></span> |<span data-ttu-id="5a75c-177">Stringa.</span><span class="sxs-lookup"><span data-stu-id="5a75c-177">String.</span></span> <span data-ttu-id="5a75c-178">Stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="5a75c-178">Status of the operation.</span></span> <span data-ttu-id="5a75c-179">I valori comuni includono: Started, In Progress, Succeeded, Failed, Active e Resolved.</span><span class="sxs-lookup"><span data-stu-id="5a75c-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="5a75c-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="5a75c-180">subStatus</span></span> |<span data-ttu-id="5a75c-181">In genere include il codice di stato HTTP della chiamata REST corrispondente.</span><span class="sxs-lookup"><span data-stu-id="5a75c-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="5a75c-182">Può includere anche altre stringhe che descrivono uno stato secondario.</span><span class="sxs-lookup"><span data-stu-id="5a75c-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="5a75c-183">I valori di stato secondario comuni includono OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="5a75c-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a75c-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a75c-184">Next steps</span></span>
* <span data-ttu-id="5a75c-185">[Altre informazioni sul log attività](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5a75c-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="5a75c-186">[Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="5a75c-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="5a75c-187">[Usare un'app per la logica per inviare SMS tramite Twilio da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5a75c-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="5a75c-188">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="5a75c-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="5a75c-189">[Usare un'app per la logica per inviare un messaggio Slack da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5a75c-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="5a75c-190">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="5a75c-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="5a75c-191">[Usare un'app per la logica per inviare un messaggio a una coda di Azure da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5a75c-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="5a75c-192">Questo esempio si riferisce agli avvisi relativi alle metriche, ma può essere modificato per funzionare con un avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="5a75c-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
