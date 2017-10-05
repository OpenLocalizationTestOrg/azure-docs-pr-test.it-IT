---
title: "Schema degli eventi del log attività Azure | Microsoft Docs"
description: "Informazioni sullo schema degli eventi per i dati emessi nel log attività"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="52415-103">Schema degli eventi del log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="52415-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="52415-104">Il **log attività di Azure** fornisce informazioni approfondite sugli eventi a livello di sottoscrizione che si sono verificati in Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="52415-105">Questo articolo descrive lo schema degli eventi per ogni categoria di dati.</span><span class="sxs-lookup"><span data-stu-id="52415-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="52415-106">Amministrativo</span><span class="sxs-lookup"><span data-stu-id="52415-106">Administrative</span></span>
<span data-ttu-id="52415-107">Questa categoria contiene il record di tutte le operazioni di creazione, aggiornamento, eliminazione e azione eseguite tramite Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52415-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="52415-108">Tra gli esempi dei tipi di eventi visualizzati in questa categoria sono inclusi "create virtual machine" e "delete network security group". Ogni azione eseguita da un utente o da un'applicazione usando Resource Manager viene modellata come operazione in un determinato tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="52415-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="52415-109">Se l'operazione è di tipo scrittura, eliminazione o azione, i record di avvio e riuscita o di non riuscita di tale operazione vengono registrati nella categoria amministrativa.</span><span class="sxs-lookup"><span data-stu-id="52415-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="52415-110">La categoria amministrativa include anche eventuali modifiche al controllo degli accessi in base al ruolo in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52415-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="52415-111">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="52415-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="52415-112">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="52415-112">Property descriptions</span></span>
| <span data-ttu-id="52415-113">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-113">Element Name</span></span> | <span data-ttu-id="52415-114">Description</span><span class="sxs-lookup"><span data-stu-id="52415-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52415-115">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="52415-115">authorization</span></span> |<span data-ttu-id="52415-116">BLOB delle proprietà RBAC dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="52415-117">In genere include le proprietà "action", "role" e "scope".</span><span class="sxs-lookup"><span data-stu-id="52415-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="52415-118">caller</span><span class="sxs-lookup"><span data-stu-id="52415-118">caller</span></span> |<span data-ttu-id="52415-119">Indirizzo di posta elettronica dell'utente che ha eseguito l'operazione, attestazione UPN o attestazione SPN, a seconda della disponibilità.</span><span class="sxs-lookup"><span data-stu-id="52415-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="52415-120">channels</span><span class="sxs-lookup"><span data-stu-id="52415-120">channels</span></span> |<span data-ttu-id="52415-121">Uno dei valori seguenti: "Admin" o "Operation".</span><span class="sxs-lookup"><span data-stu-id="52415-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="52415-122">claims</span><span class="sxs-lookup"><span data-stu-id="52415-122">claims</span></span> |<span data-ttu-id="52415-123">Token JWT usato da Active Directory per autenticare l'utente o l'applicazione per eseguire questa operazione in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52415-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="52415-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="52415-124">correlationId</span></span> |<span data-ttu-id="52415-125">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="52415-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="52415-126">Gli eventi che condividono un elemento correlationId appartengono alla stessa azione.</span><span class="sxs-lookup"><span data-stu-id="52415-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="52415-127">Description</span><span class="sxs-lookup"><span data-stu-id="52415-127">description</span></span> |<span data-ttu-id="52415-128">Testo statico che descrive un evento.</span><span class="sxs-lookup"><span data-stu-id="52415-128">Static text description of an event.</span></span> |
| <span data-ttu-id="52415-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="52415-129">eventDataId</span></span> |<span data-ttu-id="52415-130">Identificatore univoco di un evento.</span><span class="sxs-lookup"><span data-stu-id="52415-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="52415-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="52415-131">httpRequest</span></span> |<span data-ttu-id="52415-132">BLOB che descrive la richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="52415-132">Blob describing the Http Request.</span></span> <span data-ttu-id="52415-133">In genere include "clientRequestId", "clientIpAddress" e "method" (metodo HTTP,</span><span class="sxs-lookup"><span data-stu-id="52415-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="52415-134">ad esempio PUT).</span><span class="sxs-lookup"><span data-stu-id="52415-134">For example, PUT).</span></span> |
| <span data-ttu-id="52415-135">necessario</span><span class="sxs-lookup"><span data-stu-id="52415-135">level</span></span> |<span data-ttu-id="52415-136">Livello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-136">Level of the event.</span></span> <span data-ttu-id="52415-137">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="52415-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="52415-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="52415-138">resourceGroupName</span></span> |<span data-ttu-id="52415-139">Nome del gruppo di risorse della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="52415-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="52415-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="52415-140">resourceProviderName</span></span> |<span data-ttu-id="52415-141">Nome del provider di risorse della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="52415-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="52415-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="52415-142">resourceId</span></span> |<span data-ttu-id="52415-143">ID risorsa della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="52415-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="52415-144">operationId</span><span class="sxs-lookup"><span data-stu-id="52415-144">operationId</span></span> |<span data-ttu-id="52415-145">GUID condiviso tra gli eventi che corrispondono a una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="52415-146">operationName</span><span class="sxs-lookup"><span data-stu-id="52415-146">operationName</span></span> |<span data-ttu-id="52415-147">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-147">Name of the operation.</span></span> |
| <span data-ttu-id="52415-148">properties</span><span class="sxs-lookup"><span data-stu-id="52415-148">properties</span></span> |<span data-ttu-id="52415-149">Set di coppie `<Key, Value>`, ovvero un dizionario, che descrive i dettagli dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="52415-150">status</span><span class="sxs-lookup"><span data-stu-id="52415-150">status</span></span> |<span data-ttu-id="52415-151">Stringa che descrive lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-151">String describing the status of the operation.</span></span> <span data-ttu-id="52415-152">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="52415-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="52415-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="52415-153">subStatus</span></span> |<span data-ttu-id="52415-154">In genere si tratta del codice di stato HTTP della chiamata REST corrispondente, ma può includere altre stringhe che descrivono uno stato secondario, come i valori comuni seguenti: OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="52415-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="52415-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-155">eventTimestamp</span></span> |<span data-ttu-id="52415-156">Timestamp del momento in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta corrispondente all'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="52415-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-157">submissionTimestamp</span></span> |<span data-ttu-id="52415-158">Timestamp del momento in cui l'evento è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="52415-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="52415-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52415-159">subscriptionId</span></span> |<span data-ttu-id="52415-160">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="52415-161">Integrità del servizio</span><span class="sxs-lookup"><span data-stu-id="52415-161">Service health</span></span>
<span data-ttu-id="52415-162">Questa categoria contiene il record degli eventi imprevisti di integrità del servizio che si sono verificati in Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="52415-163">Un esempio del tipo di evento visualizzato in questa categoria è "SQL Azure in East US is experiencing downtime".</span><span class="sxs-lookup"><span data-stu-id="52415-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="52415-164">Gli eventi di integrità del servizio sono di sei tipi: Action Required, Assisted Recovery, Incident, Maintenance, Information o Security, che vengono visualizzati solo se una risorsa della sottoscrizione è interessata dall'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="52415-165">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="52415-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="52415-166">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="52415-166">Property descriptions</span></span>
<span data-ttu-id="52415-167">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-167">Element Name</span></span> | <span data-ttu-id="52415-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-168">Description</span></span>
-------- | -----------
<span data-ttu-id="52415-169">channels</span><span class="sxs-lookup"><span data-stu-id="52415-169">channels</span></span> | <span data-ttu-id="52415-170">Uno dei valori seguenti: "Admin" o "Operation"</span><span class="sxs-lookup"><span data-stu-id="52415-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="52415-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="52415-171">correlationId</span></span> | <span data-ttu-id="52415-172">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="52415-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="52415-173">Gli eventi che appartengono alla stessa azione in genere condividono lo stesso correlationId.</span><span class="sxs-lookup"><span data-stu-id="52415-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="52415-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-174">description</span></span> | <span data-ttu-id="52415-175">Descrizione dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-175">Description of the event.</span></span>
<span data-ttu-id="52415-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="52415-176">eventDataId</span></span> | <span data-ttu-id="52415-177">Identificatore univoco di un evento.</span><span class="sxs-lookup"><span data-stu-id="52415-177">The unique identifier of an event.</span></span>
<span data-ttu-id="52415-178">eventName</span><span class="sxs-lookup"><span data-stu-id="52415-178">eventName</span></span> | <span data-ttu-id="52415-179">Titolo dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-179">The title of the event.</span></span>
<span data-ttu-id="52415-180">necessario</span><span class="sxs-lookup"><span data-stu-id="52415-180">level</span></span> | <span data-ttu-id="52415-181">Livello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-181">Level of the event.</span></span> <span data-ttu-id="52415-182">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="52415-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="52415-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="52415-183">resourceProviderName</span></span> | <span data-ttu-id="52415-184">Nome del provider di risorse della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="52415-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="52415-185">Se non è noto, sarà null.</span><span class="sxs-lookup"><span data-stu-id="52415-185">If not known, this will be null.</span></span>
<span data-ttu-id="52415-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="52415-186">resourceType</span></span>| <span data-ttu-id="52415-187">Tipo della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="52415-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="52415-188">Se non è noto, sarà null.</span><span class="sxs-lookup"><span data-stu-id="52415-188">If not known, this will be null.</span></span>
<span data-ttu-id="52415-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="52415-189">subStatus</span></span> | <span data-ttu-id="52415-190">In genere, null per gli eventi di integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="52415-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="52415-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-191">eventTimestamp</span></span> | <span data-ttu-id="52415-192">Timestamp indicante quando l'evento del log è stato generato e inviato al log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="52415-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-193">submissionTimestamp</span></span> |   <span data-ttu-id="52415-194">Timestamp indicante quando l'evento è diventato disponibile nel log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="52415-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52415-195">subscriptionId</span></span> | <span data-ttu-id="52415-196">Sottoscrizione di Azure in cui è stato registrato l'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="52415-197">status</span><span class="sxs-lookup"><span data-stu-id="52415-197">status</span></span> | <span data-ttu-id="52415-198">Stringa che descrive lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-198">String describing the status of the operation.</span></span> <span data-ttu-id="52415-199">Alcuni valori comuni sono: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="52415-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="52415-200">operationName</span><span class="sxs-lookup"><span data-stu-id="52415-200">operationName</span></span> | <span data-ttu-id="52415-201">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-201">Name of the operation.</span></span> <span data-ttu-id="52415-202">In genere, Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="52415-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="52415-203">category</span><span class="sxs-lookup"><span data-stu-id="52415-203">category</span></span> | <span data-ttu-id="52415-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="52415-204">"ServiceHealth"</span></span>
<span data-ttu-id="52415-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="52415-205">resourceId</span></span> | <span data-ttu-id="52415-206">ID risorsa della risorsa interessata, se noto.</span><span class="sxs-lookup"><span data-stu-id="52415-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="52415-207">L'ID sottoscrizione viene fornito diversamente.</span><span class="sxs-lookup"><span data-stu-id="52415-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="52415-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="52415-208">Properties.title</span></span> | <span data-ttu-id="52415-209">Titolo della comunicazione localizzato.</span><span class="sxs-lookup"><span data-stu-id="52415-209">The localized title for this communication.</span></span> <span data-ttu-id="52415-210">L'inglese è la lingua predefinita.</span><span class="sxs-lookup"><span data-stu-id="52415-210">English is the default language.</span></span>
<span data-ttu-id="52415-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="52415-211">Properties.communication</span></span> | <span data-ttu-id="52415-212">Dettagli localizzati della comunicazione con markup HTML.</span><span class="sxs-lookup"><span data-stu-id="52415-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="52415-213">L'inglese è la lingua predefinita.</span><span class="sxs-lookup"><span data-stu-id="52415-213">English is the default.</span></span>
<span data-ttu-id="52415-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="52415-214">Properties.incidentType</span></span> | <span data-ttu-id="52415-215">Valori possibili: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="52415-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="52415-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="52415-216">Properties.trackingId</span></span> | <span data-ttu-id="52415-217">Identifica l'evento imprevisto a cui è associato l'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="52415-218">Usare questa proprietà per correlare gli eventi relativi a un evento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="52415-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="52415-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="52415-219">Properties.impactedServices</span></span> | <span data-ttu-id="52415-220">BLOB JSON preceduto da un carattere di escape che descrive i servizi e le aree su cui ha effetto l'evento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="52415-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="52415-221">Un elenco di servizi, ognuno dei quali ha un nome di servizio e un elenco delle aree interessate, ognuna con un nome di area.</span><span class="sxs-lookup"><span data-stu-id="52415-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="52415-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="52415-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="52415-223">La comunicazione in inglese</span><span class="sxs-lookup"><span data-stu-id="52415-223">The communication in English</span></span>
<span data-ttu-id="52415-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="52415-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="52415-225">La comunicazione in inglese con markup HTML o come testo normale</span><span class="sxs-lookup"><span data-stu-id="52415-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="52415-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="52415-226">Properties.stage</span></span> | <span data-ttu-id="52415-227">I valori possibili di AssistedRecovery, ActionRequired, Information, Incident, Security sono Active e Resolved.</span><span class="sxs-lookup"><span data-stu-id="52415-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="52415-228">Per la manutenzione i valori possibili sono: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span><span class="sxs-lookup"><span data-stu-id="52415-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="52415-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="52415-229">Properties.communicationId</span></span> | <span data-ttu-id="52415-230">La comunicazione a cui è associato l'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="52415-231">Avviso</span><span class="sxs-lookup"><span data-stu-id="52415-231">Alert</span></span>
<span data-ttu-id="52415-232">Questa categoria contiene il record di tutte le attivazioni degli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="52415-233">Un esempio del tipo di evento visualizzato in questa categoria è "CPU % on myVM has been over 80 for the past 5 minutes".</span><span class="sxs-lookup"><span data-stu-id="52415-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="52415-234">In diversi sistemi Azure il concetto di avviso prevede la possibilità di definire una regola di qualche tipo e di ricevere una notifica quando le condizioni corrispondono a tale regola.</span><span class="sxs-lookup"><span data-stu-id="52415-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="52415-235">Ogni volta che un tipo di avviso di Azure supportato viene "attivato" o vengono soddisfatte le condizioni per generare una notifica, viene anche eseguito il push di un record dell'attivazione in questa categoria del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="52415-236">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="52415-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="52415-237">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="52415-237">Property descriptions</span></span>
| <span data-ttu-id="52415-238">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-238">Element Name</span></span> | <span data-ttu-id="52415-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52415-240">caller</span><span class="sxs-lookup"><span data-stu-id="52415-240">caller</span></span> | <span data-ttu-id="52415-241">Sempre Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="52415-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="52415-242">channels</span><span class="sxs-lookup"><span data-stu-id="52415-242">channels</span></span> | <span data-ttu-id="52415-243">Sempre "Admin, Operation"</span><span class="sxs-lookup"><span data-stu-id="52415-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="52415-244">claims</span><span class="sxs-lookup"><span data-stu-id="52415-244">claims</span></span> | <span data-ttu-id="52415-245">BLOB JSON con il nome dell'entità servizio (SPN) o il tipo di risorsa del motore degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="52415-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="52415-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="52415-246">correlationId</span></span> | <span data-ttu-id="52415-247">GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="52415-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="52415-248">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-248">description</span></span> |<span data-ttu-id="52415-249">Testo statico che descrive l'evento dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="52415-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="52415-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="52415-250">eventDataId</span></span> |<span data-ttu-id="52415-251">Identificatore univoco dell'evento dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="52415-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="52415-252">necessario</span><span class="sxs-lookup"><span data-stu-id="52415-252">level</span></span> |<span data-ttu-id="52415-253">Livello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-253">Level of the event.</span></span> <span data-ttu-id="52415-254">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="52415-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="52415-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="52415-255">resourceGroupName</span></span> |<span data-ttu-id="52415-256">Nome del gruppo di risorse della risorsa interessata, se si tratta di un avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="52415-257">Per gli altri tipi di avvisi, è il nome del gruppo di risorse contenente l'avviso stesso.</span><span class="sxs-lookup"><span data-stu-id="52415-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="52415-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="52415-258">resourceProviderName</span></span> |<span data-ttu-id="52415-259">Nome del provider di risorse della risorsa interessata, se si tratta di un avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="52415-260">Per gli altri tipi di avvisi, è il nome del provider di risorse per l'avviso stesso.</span><span class="sxs-lookup"><span data-stu-id="52415-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="52415-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="52415-261">resourceId</span></span> | <span data-ttu-id="52415-262">ID della risorsa interessata, se si tratta di un avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="52415-263">Per gli altri tipi di avvisi, è l'ID della risorsa dell'avviso stessa.</span><span class="sxs-lookup"><span data-stu-id="52415-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="52415-264">operationId</span><span class="sxs-lookup"><span data-stu-id="52415-264">operationId</span></span> |<span data-ttu-id="52415-265">GUID condiviso tra gli eventi che corrispondono a una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="52415-266">operationName</span><span class="sxs-lookup"><span data-stu-id="52415-266">operationName</span></span> |<span data-ttu-id="52415-267">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-267">Name of the operation.</span></span> |
| <span data-ttu-id="52415-268">properties</span><span class="sxs-lookup"><span data-stu-id="52415-268">properties</span></span> |<span data-ttu-id="52415-269">Set di coppie `<Key, Value>`, ovvero un dizionario, che descrive i dettagli dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="52415-270">status</span><span class="sxs-lookup"><span data-stu-id="52415-270">status</span></span> |<span data-ttu-id="52415-271">Stringa che descrive lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-271">String describing the status of the operation.</span></span> <span data-ttu-id="52415-272">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="52415-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="52415-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="52415-273">subStatus</span></span> | <span data-ttu-id="52415-274">In genere null per gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="52415-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="52415-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-275">eventTimestamp</span></span> |<span data-ttu-id="52415-276">Timestamp del momento in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta corrispondente all'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="52415-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-277">submissionTimestamp</span></span> |<span data-ttu-id="52415-278">Timestamp del momento in cui l'evento è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="52415-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="52415-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52415-279">subscriptionId</span></span> |<span data-ttu-id="52415-280">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="52415-281">Campo delle proprietà per ogni tipo di avviso</span><span class="sxs-lookup"><span data-stu-id="52415-281">Properties field per alert type</span></span>
<span data-ttu-id="52415-282">Il campo delle proprietà conterrà valori diversi a seconda dell'origine dell'evento dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="52415-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="52415-283">Due comuni provider di eventi di avviso sono gli avvisi e gli avvisi delle metriche del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="52415-284">Proprietà degli avvisi del log attività</span><span class="sxs-lookup"><span data-stu-id="52415-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="52415-285">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-285">Element Name</span></span> | <span data-ttu-id="52415-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52415-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52415-287">properties.subscriptionId</span></span> | <span data-ttu-id="52415-288">ID della sottoscrizione dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="52415-289">properties.eventDataId</span></span> | <span data-ttu-id="52415-290">ID dei dati dell'evento dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="52415-291">properties.resourceGroup</span></span> | <span data-ttu-id="52415-292">Gruppo di risorse dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="52415-293">properties.resourceId</span></span> | <span data-ttu-id="52415-294">ID della risorsa dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-295">properties.eventTimestamp</span></span> | <span data-ttu-id="52415-296">Timestamp dell'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="52415-297">properties.operationName</span></span> | <span data-ttu-id="52415-298">Nome dell'operazione dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="52415-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="52415-299">properties.status</span></span> | <span data-ttu-id="52415-300">Stato dall'evento del log attività che ha causato l'attivazione di questa regola di avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="52415-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="52415-301">Proprietà degli avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="52415-301">Properties for metric alerts</span></span>
| <span data-ttu-id="52415-302">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-302">Element Name</span></span> | <span data-ttu-id="52415-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52415-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="52415-304">properties.RuleUri</span></span> | <span data-ttu-id="52415-305">ID risorsa della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="52415-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="52415-306">properties.RuleName</span></span> | <span data-ttu-id="52415-307">Nome della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="52415-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="52415-308">properties.RuleDescription</span></span> | <span data-ttu-id="52415-309">Descrizione della regola di avviso per la metrica (definita nella regola di avviso).</span><span class="sxs-lookup"><span data-stu-id="52415-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="52415-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="52415-310">properties.Threshold</span></span> | <span data-ttu-id="52415-311">Valore della soglia usato nella valutazione della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="52415-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="52415-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="52415-313">Dimensioni della finestra usate nella valutazione della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="52415-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="52415-314">properties.Aggregation</span></span> | <span data-ttu-id="52415-315">Tipo di aggregazione definito nella regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="52415-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="52415-316">properties.Operator</span></span> | <span data-ttu-id="52415-317">Operatore condizionale usato nella valutazione della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="52415-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="52415-318">properties.MetricName</span></span> | <span data-ttu-id="52415-319">Nome della metrica usato nella valutazione della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="52415-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="52415-320">properties.MetricUnit</span></span> | <span data-ttu-id="52415-321">Unità della metrica usata nella valutazione della regola di avviso per la metrica.</span><span class="sxs-lookup"><span data-stu-id="52415-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="52415-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="52415-322">Autoscale</span></span>
<span data-ttu-id="52415-323">Questa categoria contiene il record degli eventi correlati all'operazione del motore di ridimensionamento automatico in base alle impostazioni di scalabilità automatica definite nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52415-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="52415-324">Un esempio del tipo di evento visualizzato in questa categoria è "Autoscale scale up action failed".</span><span class="sxs-lookup"><span data-stu-id="52415-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="52415-325">Con il ridimensionamento automatico è possibile aumentare o ridurre automaticamente il numero di istanze in un tipo di risorsa supportato in base all'ora del giorno e/o ai dati di caricamento (metrica) usando un'impostazione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="52415-326">Quando vengono soddisfatte le condizioni per aumentare o ridurre le prestazioni, gli eventi di avvio riusciti o quelli non riusciti verranno registrati in questa categoria.</span><span class="sxs-lookup"><span data-stu-id="52415-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="52415-327">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="52415-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="52415-328">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="52415-328">Property descriptions</span></span>
| <span data-ttu-id="52415-329">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="52415-329">Element Name</span></span> | <span data-ttu-id="52415-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52415-331">caller</span><span class="sxs-lookup"><span data-stu-id="52415-331">caller</span></span> | <span data-ttu-id="52415-332">Sempre Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="52415-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="52415-333">channels</span><span class="sxs-lookup"><span data-stu-id="52415-333">channels</span></span> | <span data-ttu-id="52415-334">Sempre "Admin, Operation"</span><span class="sxs-lookup"><span data-stu-id="52415-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="52415-335">claims</span><span class="sxs-lookup"><span data-stu-id="52415-335">claims</span></span> | <span data-ttu-id="52415-336">BLOB JSON con il nome dell'entità servizio (SPN) o il tipo di risorsa del motore di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="52415-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="52415-337">correlationId</span></span> | <span data-ttu-id="52415-338">GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="52415-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="52415-339">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52415-339">description</span></span> |<span data-ttu-id="52415-340">Testo statico che descrive l'evento di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="52415-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="52415-341">eventDataId</span></span> |<span data-ttu-id="52415-342">Identificatore univoco dell'evento di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="52415-343">necessario</span><span class="sxs-lookup"><span data-stu-id="52415-343">level</span></span> |<span data-ttu-id="52415-344">Livello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-344">Level of the event.</span></span> <span data-ttu-id="52415-345">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="52415-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="52415-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="52415-346">resourceGroupName</span></span> |<span data-ttu-id="52415-347">Nome del gruppo di risorse dell'impostazione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="52415-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="52415-348">resourceProviderName</span></span> |<span data-ttu-id="52415-349">Nome del provider di risorse dell'impostazione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="52415-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="52415-350">resourceId</span></span> |<span data-ttu-id="52415-351">ID risorsa dell'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="52415-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="52415-352">operationId</span><span class="sxs-lookup"><span data-stu-id="52415-352">operationId</span></span> |<span data-ttu-id="52415-353">GUID condiviso tra gli eventi che corrispondono a una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="52415-354">operationName</span><span class="sxs-lookup"><span data-stu-id="52415-354">operationName</span></span> |<span data-ttu-id="52415-355">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-355">Name of the operation.</span></span> |
| <span data-ttu-id="52415-356">properties</span><span class="sxs-lookup"><span data-stu-id="52415-356">properties</span></span> |<span data-ttu-id="52415-357">Set di coppie `<Key, Value>`, ovvero un dizionario, che descrive i dettagli dell'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="52415-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="52415-358">properties.Description</span></span> | <span data-ttu-id="52415-359">Descrizione dettagliata delle operazioni eseguite dal motore di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="52415-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="52415-360">properties.ResourceName</span></span> | <span data-ttu-id="52415-361">ID della risorsa interessata (risorsa in cui è in corso l'azione di ridimensionamento)</span><span class="sxs-lookup"><span data-stu-id="52415-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="52415-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="52415-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="52415-363">Numero di istanze prima che venisse eseguita l'azione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="52415-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="52415-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="52415-365">Numero di istanze dopo che è stata eseguita l'azione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="52415-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="52415-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="52415-367">Timestamp indicante quando si è verificata l'azione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="52415-368">status</span><span class="sxs-lookup"><span data-stu-id="52415-368">status</span></span> |<span data-ttu-id="52415-369">Stringa che descrive lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="52415-369">String describing the status of the operation.</span></span> <span data-ttu-id="52415-370">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="52415-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="52415-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="52415-371">subStatus</span></span> | <span data-ttu-id="52415-372">In genere null per il ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="52415-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="52415-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-373">eventTimestamp</span></span> |<span data-ttu-id="52415-374">Timestamp del momento in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta corrispondente all'evento.</span><span class="sxs-lookup"><span data-stu-id="52415-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="52415-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="52415-375">submissionTimestamp</span></span> |<span data-ttu-id="52415-376">Timestamp del momento in cui l'evento è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="52415-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="52415-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52415-377">subscriptionId</span></span> |<span data-ttu-id="52415-378">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52415-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52415-379">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52415-379">Next steps</span></span>
* [<span data-ttu-id="52415-380">Altre informazioni sul log attività (in precedenza, log di controllo)</span><span class="sxs-lookup"><span data-stu-id="52415-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="52415-381">Trasmettere il log attività di Azure a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="52415-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
