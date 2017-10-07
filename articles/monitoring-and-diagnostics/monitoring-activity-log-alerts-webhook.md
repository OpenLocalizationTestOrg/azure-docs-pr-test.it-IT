---
title: "schema di webhook hello aaaUnderstand utilizzato negli avvisi del registro attività | Documenti Microsoft"
description: "Informazioni sullo schema hello di hello JSON che viene registrato l'URL del webhook tooa quando viene attivato un avviso di log di attività."
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
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="a2ace-103">Webhook per gli avvisi del log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="a2ace-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="a2ace-104">Come parte della definizione di hello di un gruppo di azioni, è possibile configurare webhook endpoint tooreceive attività Registro notifiche di avviso.</span><span class="sxs-lookup"><span data-stu-id="a2ace-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="a2ace-105">Con webhook, è possibile distribuire questi sistemi tooother notifiche per le azioni di post-elaborazione o personalizzate.</span><span class="sxs-lookup"><span data-stu-id="a2ace-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="a2ace-106">Questo articolo illustra i payload hello per hello HTTP POST tooa webhook è simile.</span><span class="sxs-lookup"><span data-stu-id="a2ace-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="a2ace-107">Per ulteriori informazioni sugli avvisi di log di attività, vedere come troppo[creare attività di Azure gli avvisi del registro](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a2ace-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="a2ace-108">Per informazioni su gruppi di azioni, vedere come troppo[creare gruppi di azioni](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="a2ace-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="a2ace-109">L'autenticazione hello webhook</span><span class="sxs-lookup"><span data-stu-id="a2ace-109">Authenticate hello webhook</span></span>
<span data-ttu-id="a2ace-110">Hello webhook possono utilizzare facoltativamente basata su token di autorizzazione per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a2ace-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="a2ace-111">Hello webhook URI viene salvato con un ID del token, ad esempio, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="a2ace-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="a2ace-112">Schema del payload</span><span class="sxs-lookup"><span data-stu-id="a2ace-112">Payload schema</span></span>
<span data-ttu-id="a2ace-113">payload JSON Hello contenuti in hello operazione POST varia in base a campo data.context.activityLog.eventSource del payload hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="a2ace-114">Comune</span><span class="sxs-lookup"><span data-stu-id="a2ace-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="a2ace-115">Amministrativo</span><span class="sxs-lookup"><span data-stu-id="a2ace-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="a2ace-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="a2ace-116">ServiceHealth</span></span>
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

<span data-ttu-id="a2ace-117">Per i dettagli su schemi specifici relativi agli avvisi del log attività per le notifiche sull'integrità del servizio, vedere [Notifiche sull'integrità del servizio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="a2ace-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="a2ace-118">Per informazioni dettagliate specifiche dello schema su tutti gli avvisi di log altre attività, vedere [Panoramica del log attività Azure hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a2ace-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="a2ace-119">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="a2ace-119">Element name</span></span> | <span data-ttu-id="a2ace-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a2ace-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2ace-121">status</span><span class="sxs-lookup"><span data-stu-id="a2ace-121">status</span></span> |<span data-ttu-id="a2ace-122">Usato per avvisi relativi alle metriche.</span><span class="sxs-lookup"><span data-stu-id="a2ace-122">Used for metric alerts.</span></span> <span data-ttu-id="a2ace-123">Impostare sempre troppo "attivato" per gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="a2ace-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="a2ace-124">context</span><span class="sxs-lookup"><span data-stu-id="a2ace-124">context</span></span> |<span data-ttu-id="a2ace-125">Contesto dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-125">Context of hello event.</span></span> |
| <span data-ttu-id="a2ace-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="a2ace-126">resourceProviderName</span></span> |<span data-ttu-id="a2ace-127">provider di risorse Hello di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="a2ace-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="a2ace-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="a2ace-128">conditionType</span></span> |<span data-ttu-id="a2ace-129">Sempre "Event".</span><span class="sxs-lookup"><span data-stu-id="a2ace-129">Always "Event."</span></span> |
| <span data-ttu-id="a2ace-130">name</span><span class="sxs-lookup"><span data-stu-id="a2ace-130">name</span></span> |<span data-ttu-id="a2ace-131">Nome della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="a2ace-132">id</span><span class="sxs-lookup"><span data-stu-id="a2ace-132">id</span></span> |<span data-ttu-id="a2ace-133">ID risorsa dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="a2ace-134">description</span><span class="sxs-lookup"><span data-stu-id="a2ace-134">description</span></span> |<span data-ttu-id="a2ace-135">Descrizione dell'avviso impostato quando viene creato l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="a2ace-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a2ace-136">subscriptionId</span></span> |<span data-ttu-id="a2ace-137">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ace-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="a2ace-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="a2ace-138">timestamp</span></span> |<span data-ttu-id="a2ace-139">Ora in cui hello è stato generato l'evento dal servizio di Azure che ha elaborato la richiesta hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="a2ace-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="a2ace-140">resourceId</span></span> |<span data-ttu-id="a2ace-141">ID di risorsa di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="a2ace-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="a2ace-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="a2ace-142">resourceGroupName</span></span> |<span data-ttu-id="a2ace-143">Nome del gruppo di risorse hello per hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="a2ace-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="a2ace-144">properties</span><span class="sxs-lookup"><span data-stu-id="a2ace-144">properties</span></span> |<span data-ttu-id="a2ace-145">Set di `<Key, Value>` coppie (vale a dire `Dictionary<String, String>`) che include i dettagli sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="a2ace-146">event</span><span class="sxs-lookup"><span data-stu-id="a2ace-146">event</span></span> |<span data-ttu-id="a2ace-147">Elemento che contiene i metadati relativi a eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="a2ace-148">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="a2ace-148">authorization</span></span> |<span data-ttu-id="a2ace-149">proprietà di controllo di accesso basato sui ruoli Hello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="a2ace-150">Queste proprietà includono in genere azione hello, hello ruolo e ambito hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="a2ace-151">category</span><span class="sxs-lookup"><span data-stu-id="a2ace-151">category</span></span> |<span data-ttu-id="a2ace-152">Categoria di eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-152">Category of hello event.</span></span> <span data-ttu-id="a2ace-153">I valori supportati includono Administrative, Alert, Security, ServiceHealth e Recommendation.</span><span class="sxs-lookup"><span data-stu-id="a2ace-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="a2ace-154">caller</span><span class="sxs-lookup"><span data-stu-id="a2ace-154">caller</span></span> |<span data-ttu-id="a2ace-155">Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a2ace-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="a2ace-156">Può essere null per alcune chiamate di sistema.</span><span class="sxs-lookup"><span data-stu-id="a2ace-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="a2ace-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="a2ace-157">correlationId</span></span> |<span data-ttu-id="a2ace-158">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="a2ace-158">Usually a GUID in string format.</span></span> <span data-ttu-id="a2ace-159">Gli eventi con ID correlazione appartengono toohello stessa azione di dimensioni maggiori e in genere condividono un ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="a2ace-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="a2ace-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="a2ace-160">eventDescription</span></span> |<span data-ttu-id="a2ace-161">Descrizione di testo statico dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="a2ace-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="a2ace-162">eventDataId</span></span> |<span data-ttu-id="a2ace-163">Identificatore univoco per l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="a2ace-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="a2ace-164">eventSource</span></span> |<span data-ttu-id="a2ace-165">Nome di hello Azure servizio o dell'infrastruttura che l'evento generato hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="a2ace-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="a2ace-166">httpRequest</span></span> |<span data-ttu-id="a2ace-167">Hello richiesta include in genere hello clientRequestId, clientIpAddress e il metodo HTTP (ad esempio PUT).</span><span class="sxs-lookup"><span data-stu-id="a2ace-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="a2ace-168">level</span><span class="sxs-lookup"><span data-stu-id="a2ace-168">level</span></span> |<span data-ttu-id="a2ace-169">Uno dei seguenti valori hello: critico, errore, avviso, informativo e dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a2ace-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="a2ace-170">operationId</span><span class="sxs-lookup"><span data-stu-id="a2ace-170">operationId</span></span> |<span data-ttu-id="a2ace-171">In genere un GUID condiviso tra gli eventi di hello toosingle operazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a2ace-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="a2ace-172">operationName</span><span class="sxs-lookup"><span data-stu-id="a2ace-172">operationName</span></span> |<span data-ttu-id="a2ace-173">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-173">Name of hello operation.</span></span> |
| <span data-ttu-id="a2ace-174">properties</span><span class="sxs-lookup"><span data-stu-id="a2ace-174">properties</span></span> |<span data-ttu-id="a2ace-175">Proprietà di evento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-175">Properties of hello event.</span></span> |
| <span data-ttu-id="a2ace-176">status</span><span class="sxs-lookup"><span data-stu-id="a2ace-176">status</span></span> |<span data-ttu-id="a2ace-177">Stringa.</span><span class="sxs-lookup"><span data-stu-id="a2ace-177">String.</span></span> <span data-ttu-id="a2ace-178">Stato dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-178">Status of hello operation.</span></span> <span data-ttu-id="a2ace-179">I valori comuni includono: Started, In Progress, Succeeded, Failed, Active e Resolved.</span><span class="sxs-lookup"><span data-stu-id="a2ace-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="a2ace-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="a2ace-180">subStatus</span></span> |<span data-ttu-id="a2ace-181">In genere include codice di stato HTTP hello della chiamata REST corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="a2ace-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="a2ace-182">Può includere anche altre stringhe che descrivono uno stato secondario.</span><span class="sxs-lookup"><span data-stu-id="a2ace-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="a2ace-183">I valori di stato secondario comuni includono OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="a2ace-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2ace-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2ace-184">Next steps</span></span>
* <span data-ttu-id="a2ace-185">[Altre informazioni sui log attività hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a2ace-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="a2ace-186">[Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="a2ace-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="a2ace-187">[Utilizzare un toosend di logica app un SMS tramite Twilio da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a2ace-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="a2ace-188">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.</span><span class="sxs-lookup"><span data-stu-id="a2ace-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="a2ace-189">[Utilizzare un toosend app logica un messaggio da un avviso Azure Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a2ace-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="a2ace-190">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.</span><span class="sxs-lookup"><span data-stu-id="a2ace-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="a2ace-191">[Utilizzare un toosend app logica tooan un messaggio Azure coda da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a2ace-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="a2ace-192">In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.</span><span class="sxs-lookup"><span data-stu-id="a2ace-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
