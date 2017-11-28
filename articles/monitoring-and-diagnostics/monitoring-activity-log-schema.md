---
title: "Schema di eventi del registro attività aaaAzure | Documenti Microsoft"
description: "Comprensione hello schema di eventi per i dati emessi in hello Log attività"
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
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="c11e6-103">Schema degli eventi del log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="c11e6-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="c11e6-104">Hello **Log attività Azure** è un log che fornisce informazioni approfondite tutti gli eventi a livello di sottoscrizione che si sono verificati in Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="c11e6-105">Questo articolo descrive allo schema di eventi hello per ogni categoria di dati.</span><span class="sxs-lookup"><span data-stu-id="c11e6-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="c11e6-106">Amministrativo</span><span class="sxs-lookup"><span data-stu-id="c11e6-106">Administrative</span></span>
<span data-ttu-id="c11e6-107">Questa categoria include i record di hello di tutti create, update, delete e azione di operazioni eseguite tramite Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="c11e6-108">Esempi di tipi di eventi visualizzati in questa categoria includono hello "Crea macchina virtuale" e "gruppo di sicurezza di rete delete" ogni azione eseguita da un utente o applicazione usando Gestione risorse viene modellato come un'operazione su un determinato tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="c11e6-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="c11e6-109">Se il tipo di operazione hello è scrivere, Delete o azione, i record di hello inizio hello sia esito positivo o esito negativo dell'operazione vengono registrati nella categoria amministrativa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="c11e6-110">categoria amministrativa Hello include anche qualsiasi controllo di accesso basato su toorole modifiche in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="c11e6-111">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="c11e6-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="c11e6-112">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="c11e6-112">Property descriptions</span></span>
| <span data-ttu-id="c11e6-113">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-113">Element Name</span></span> | <span data-ttu-id="c11e6-114">Description</span><span class="sxs-lookup"><span data-stu-id="c11e6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c11e6-115">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c11e6-115">authorization</span></span> |<span data-ttu-id="c11e6-116">BLOB di proprietà RBAC dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="c11e6-117">In genere include le proprietà di "azione", "role" e "scope" hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="c11e6-118">caller</span><span class="sxs-lookup"><span data-stu-id="c11e6-118">caller</span></span> |<span data-ttu-id="c11e6-119">Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c11e6-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="c11e6-120">channels</span><span class="sxs-lookup"><span data-stu-id="c11e6-120">channels</span></span> |<span data-ttu-id="c11e6-121">Uno dei seguenti valori hello: "Admin", "Operation"</span><span class="sxs-lookup"><span data-stu-id="c11e6-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="c11e6-122">claims</span><span class="sxs-lookup"><span data-stu-id="c11e6-122">claims</span></span> |<span data-ttu-id="c11e6-123">token JWT Hello utilizzati da Active Directory tooauthenticate hello utente o applicazione tooperform questa operazione nella console di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="c11e6-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-124">correlationId</span></span> |<span data-ttu-id="c11e6-125">In genere un GUID in formato stringa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="c11e6-126">Gli eventi che condividono un valore correlationId appartengono toohello stessa azione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="c11e6-127">description</span><span class="sxs-lookup"><span data-stu-id="c11e6-127">description</span></span> |<span data-ttu-id="c11e6-128">Testo statico che descrive un evento.</span><span class="sxs-lookup"><span data-stu-id="c11e6-128">Static text description of an event.</span></span> |
| <span data-ttu-id="c11e6-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="c11e6-129">eventDataId</span></span> |<span data-ttu-id="c11e6-130">Identificatore univoco di un evento.</span><span class="sxs-lookup"><span data-stu-id="c11e6-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="c11e6-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="c11e6-131">httpRequest</span></span> |<span data-ttu-id="c11e6-132">BLOB hello che descrive la richiesta Http.</span><span class="sxs-lookup"><span data-stu-id="c11e6-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="c11e6-133">In genere include hello "clientRequestId", "clientIpAddress" e "method" (metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="c11e6-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="c11e6-134">ad esempio PUT).</span><span class="sxs-lookup"><span data-stu-id="c11e6-134">For example, PUT).</span></span> |
| <span data-ttu-id="c11e6-135">level</span><span class="sxs-lookup"><span data-stu-id="c11e6-135">level</span></span> |<span data-ttu-id="c11e6-136">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-136">Level of hello event.</span></span> <span data-ttu-id="c11e6-137">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="c11e6-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="c11e6-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c11e6-138">resourceGroupName</span></span> |<span data-ttu-id="c11e6-139">Nome del gruppo di risorse hello per hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="c11e6-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="c11e6-140">resourceProviderName</span></span> |<span data-ttu-id="c11e6-141">Nome del provider di risorse hello per hello interessati risorsa</span><span class="sxs-lookup"><span data-stu-id="c11e6-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="c11e6-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="c11e6-142">resourceId</span></span> |<span data-ttu-id="c11e6-143">Id di risorsa di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="c11e6-144">operationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-144">operationId</span></span> |<span data-ttu-id="c11e6-145">Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="c11e6-146">operationName</span><span class="sxs-lookup"><span data-stu-id="c11e6-146">operationName</span></span> |<span data-ttu-id="c11e6-147">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-147">Name of hello operation.</span></span> |
| <span data-ttu-id="c11e6-148">properties</span><span class="sxs-lookup"><span data-stu-id="c11e6-148">properties</span></span> |<span data-ttu-id="c11e6-149">Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="c11e6-150">status</span><span class="sxs-lookup"><span data-stu-id="c11e6-150">status</span></span> |<span data-ttu-id="c11e6-151">Stringa che descrive lo stato di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="c11e6-152">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="c11e6-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="c11e6-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="c11e6-153">subStatus</span></span> |<span data-ttu-id="c11e6-154">In genere il codice di stato HTTP della corrispondente chiamata REST hello hello, ma può includere anche altre stringhe che descrive uno stato secondario, ad esempio i valori comuni: OK (codice di stato HTTP: 200), creato (codice di stato HTTP: 201), accettato (codice di stato HTTP: 202), il contenuto No (HTTP Codice di stato: 204), richiesta non valida (codice di stato HTTP: 400), non è stata trovata (codice di stato HTTP: 404), dei conflitti (codice di stato HTTP: 409), errore interno del Server (codice di stato HTTP: 500), Service non disponibile (codice di stato HTTP: 503), Timeout del Gateway (codice di stato HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="c11e6-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="c11e6-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-155">eventTimestamp</span></span> |<span data-ttu-id="c11e6-156">Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c11e6-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="c11e6-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-157">submissionTimestamp</span></span> |<span data-ttu-id="c11e6-158">Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="c11e6-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="c11e6-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c11e6-159">subscriptionId</span></span> |<span data-ttu-id="c11e6-160">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="c11e6-161">Integrità del servizio</span><span class="sxs-lookup"><span data-stu-id="c11e6-161">Service health</span></span>
<span data-ttu-id="c11e6-162">Questa categoria include i record di hello di eventuali problemi di integrità servizio che si sono verificati in Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="c11e6-163">Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "SQL Azure negli Stati Uniti orientali si è verificati i tempi di inattività".</span><span class="sxs-lookup"><span data-stu-id="c11e6-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="c11e6-164">Eventi di integrità del servizio sono disponibili in cinque tipi: azione richiesta, del recupero assistito, evento imprevisto, manutenzione, informazioni o sicurezza e vengono visualizzate solo se si dispone di una risorsa nella sottoscrizione hello che potrebbe essere interessata dall'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="c11e6-165">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="c11e6-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="c11e6-166">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="c11e6-166">Property descriptions</span></span>
<span data-ttu-id="c11e6-167">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-167">Element Name</span></span> | <span data-ttu-id="c11e6-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c11e6-168">Description</span></span>
-------- | -----------
<span data-ttu-id="c11e6-169">channels</span><span class="sxs-lookup"><span data-stu-id="c11e6-169">channels</span></span> | <span data-ttu-id="c11e6-170">È uno dei seguenti valori hello: "Admin", "Operation"</span><span class="sxs-lookup"><span data-stu-id="c11e6-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="c11e6-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-171">correlationId</span></span> | <span data-ttu-id="c11e6-172">È in genere un GUID in formato stringa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="c11e6-173">Gli eventi che appartengono toohello stessa azione condividono di solito hello stesso correlationId.</span><span class="sxs-lookup"><span data-stu-id="c11e6-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="c11e6-174">description</span><span class="sxs-lookup"><span data-stu-id="c11e6-174">description</span></span> | <span data-ttu-id="c11e6-175">Descrizione dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-175">Description of hello event.</span></span>
<span data-ttu-id="c11e6-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="c11e6-176">eventDataId</span></span> | <span data-ttu-id="c11e6-177">Identificatore univoco di Hello di un evento.</span><span class="sxs-lookup"><span data-stu-id="c11e6-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="c11e6-178">eventName</span><span class="sxs-lookup"><span data-stu-id="c11e6-178">eventName</span></span> | <span data-ttu-id="c11e6-179">titolo Hello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-179">hello title of hello event.</span></span>
<span data-ttu-id="c11e6-180">level</span><span class="sxs-lookup"><span data-stu-id="c11e6-180">level</span></span> | <span data-ttu-id="c11e6-181">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-181">Level of hello event.</span></span> <span data-ttu-id="c11e6-182">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="c11e6-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="c11e6-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="c11e6-183">resourceProviderName</span></span> | <span data-ttu-id="c11e6-184">Nome del provider di risorse hello per hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="c11e6-185">Se non è noto, sarà null.</span><span class="sxs-lookup"><span data-stu-id="c11e6-185">If not known, this will be null.</span></span>
<span data-ttu-id="c11e6-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="c11e6-186">resourceType</span></span>| <span data-ttu-id="c11e6-187">tipo di Hello della risorsa di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="c11e6-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="c11e6-188">Se non è noto, sarà null.</span><span class="sxs-lookup"><span data-stu-id="c11e6-188">If not known, this will be null.</span></span>
<span data-ttu-id="c11e6-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="c11e6-189">subStatus</span></span> | <span data-ttu-id="c11e6-190">In genere, null per gli eventi di integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="c11e6-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="c11e6-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-191">eventTimestamp</span></span> | <span data-ttu-id="c11e6-192">Timestamp dell'evento hello è stato generato e inviato toohello Log attività.</span><span class="sxs-lookup"><span data-stu-id="c11e6-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="c11e6-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-193">submissionTimestamp</span></span> |   <span data-ttu-id="c11e6-194">Timestamp dell'evento hello è diventato disponibile nel Log attività hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="c11e6-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c11e6-195">subscriptionId</span></span> | <span data-ttu-id="c11e6-196">Hello sottoscrizione di Azure in cui è stato registrato questo evento.</span><span class="sxs-lookup"><span data-stu-id="c11e6-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="c11e6-197">status</span><span class="sxs-lookup"><span data-stu-id="c11e6-197">status</span></span> | <span data-ttu-id="c11e6-198">Stringa che descrive lo stato di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="c11e6-199">Alcuni valori comuni sono: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="c11e6-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="c11e6-200">operationName</span><span class="sxs-lookup"><span data-stu-id="c11e6-200">operationName</span></span> | <span data-ttu-id="c11e6-201">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-201">Name of hello operation.</span></span> <span data-ttu-id="c11e6-202">In genere, Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="c11e6-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="c11e6-203">category</span><span class="sxs-lookup"><span data-stu-id="c11e6-203">category</span></span> | <span data-ttu-id="c11e6-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="c11e6-204">"ServiceHealth"</span></span>
<span data-ttu-id="c11e6-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="c11e6-205">resourceId</span></span> | <span data-ttu-id="c11e6-206">Id di risorsa di hello interessati risorsa, se noto.</span><span class="sxs-lookup"><span data-stu-id="c11e6-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="c11e6-207">L'ID sottoscrizione viene fornito diversamente.</span><span class="sxs-lookup"><span data-stu-id="c11e6-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="c11e6-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="c11e6-208">Properties.title</span></span> | <span data-ttu-id="c11e6-209">Hello titolo localizzato per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-209">hello localized title for this communication.</span></span> <span data-ttu-id="c11e6-210">L'inglese è una lingua predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-210">English is hello default language.</span></span>
<span data-ttu-id="c11e6-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="c11e6-211">Properties.communication</span></span> | <span data-ttu-id="c11e6-212">Hello localizzata dettagli di comunicazione hello con il markup HTML.</span><span class="sxs-lookup"><span data-stu-id="c11e6-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="c11e6-213">Inglese è l'impostazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-213">English is hello default.</span></span>
<span data-ttu-id="c11e6-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="c11e6-214">Properties.incidentType</span></span> | <span data-ttu-id="c11e6-215">Valori possibili: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="c11e6-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="c11e6-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="c11e6-216">Properties.trackingId</span></span> | <span data-ttu-id="c11e6-217">Identifica l'evento imprevisto di hello che è associato questo evento.</span><span class="sxs-lookup"><span data-stu-id="c11e6-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="c11e6-218">Utilizzare questo evento imprevisto di toocorrelate hello eventi tooan correlati.</span><span class="sxs-lookup"><span data-stu-id="c11e6-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="c11e6-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="c11e6-219">Properties.impactedServices</span></span> | <span data-ttu-id="c11e6-220">Un escape blob JSON che descrive i servizi di hello e le aree che sono interessate da evento imprevisto di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="c11e6-221">Un elenco di servizi, ognuno dei quali ha un nome di servizio e un elenco delle aree interessate, ognuna con un nome di area.</span><span class="sxs-lookup"><span data-stu-id="c11e6-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="c11e6-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="c11e6-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="c11e6-223">comunicazione Hello in inglese</span><span class="sxs-lookup"><span data-stu-id="c11e6-223">hello communication in English</span></span>
<span data-ttu-id="c11e6-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="c11e6-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="c11e6-225">comunicazione Hello in inglese come markup html o testo normale</span><span class="sxs-lookup"><span data-stu-id="c11e6-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="c11e6-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="c11e6-226">Properties.stage</span></span> | <span data-ttu-id="c11e6-227">I valori possibili di AssistedRecovery, ActionRequired, Information, Incident, Security sono Active e Resolved.</span><span class="sxs-lookup"><span data-stu-id="c11e6-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="c11e6-228">Per la manutenzione i valori possibili sono: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span><span class="sxs-lookup"><span data-stu-id="c11e6-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="c11e6-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-229">Properties.communicationId</span></span> | <span data-ttu-id="c11e6-230">comunicazione Hello questo evento è associato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="c11e6-231">Avviso</span><span class="sxs-lookup"><span data-stu-id="c11e6-231">Alert</span></span>
<span data-ttu-id="c11e6-232">Questa categoria include i record di hello di tutte le attivazioni di avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="c11e6-233">Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "% della CPU nella macchina virtuale myVM è stato superato l'80 per hello negli ultimi 5 minuti."</span><span class="sxs-lookup"><span data-stu-id="c11e6-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="c11e6-234">In diversi sistemi Azure il concetto di avviso prevede la possibilità di definire una regola di qualche tipo e di ricevere una notifica quando le condizioni corrispondono a tale regola.</span><span class="sxs-lookup"><span data-stu-id="c11e6-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="c11e6-235">Ogni volta che un tipo di avviso Azure supportato 'attiva,' o condizioni hello sono soddisfatto toogenerate una notifica, un record di attivazione hello viene inoltre inserito toothis categoria di hello Log attività.</span><span class="sxs-lookup"><span data-stu-id="c11e6-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="c11e6-236">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="c11e6-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="c11e6-237">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="c11e6-237">Property descriptions</span></span>
| <span data-ttu-id="c11e6-238">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-238">Element Name</span></span> | <span data-ttu-id="c11e6-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c11e6-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c11e6-240">caller</span><span class="sxs-lookup"><span data-stu-id="c11e6-240">caller</span></span> | <span data-ttu-id="c11e6-241">Sempre Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="c11e6-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="c11e6-242">channels</span><span class="sxs-lookup"><span data-stu-id="c11e6-242">channels</span></span> | <span data-ttu-id="c11e6-243">Sempre "Admin, Operation"</span><span class="sxs-lookup"><span data-stu-id="c11e6-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="c11e6-244">claims</span><span class="sxs-lookup"><span data-stu-id="c11e6-244">claims</span></span> | <span data-ttu-id="c11e6-245">Blob JSON con hello nome SPN (service principal name) o risorsa di tipo, del motore degli avvisi hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="c11e6-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-246">correlationId</span></span> | <span data-ttu-id="c11e6-247">Un GUID in formato stringa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="c11e6-248">description</span><span class="sxs-lookup"><span data-stu-id="c11e6-248">description</span></span> |<span data-ttu-id="c11e6-249">Descrizione di testo statico dell'evento di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="c11e6-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="c11e6-250">eventDataId</span></span> |<span data-ttu-id="c11e6-251">Identificatore univoco dell'evento di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="c11e6-252">level</span><span class="sxs-lookup"><span data-stu-id="c11e6-252">level</span></span> |<span data-ttu-id="c11e6-253">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-253">Level of hello event.</span></span> <span data-ttu-id="c11e6-254">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="c11e6-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="c11e6-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c11e6-255">resourceGroupName</span></span> |<span data-ttu-id="c11e6-256">Nome del gruppo di risorse hello per hello in presenza di risorse è un avviso di metrica.</span><span class="sxs-lookup"><span data-stu-id="c11e6-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="c11e6-257">Per altri tipi di avviso, questo è il nome di hello hello del gruppo di risorse che contiene l'avviso hello stesso.</span><span class="sxs-lookup"><span data-stu-id="c11e6-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="c11e6-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="c11e6-258">resourceProviderName</span></span> |<span data-ttu-id="c11e6-259">Nome del provider di risorse hello per hello in presenza di risorse è un avviso di metrica.</span><span class="sxs-lookup"><span data-stu-id="c11e6-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="c11e6-260">Per altri tipi di avviso, si tratta di nome hello del provider di risorse hello per avviso hello stesso.</span><span class="sxs-lookup"><span data-stu-id="c11e6-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="c11e6-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="c11e6-261">resourceId</span></span> | <span data-ttu-id="c11e6-262">Nome dell'ID di risorsa hello per hello in presenza di risorse è un avviso di metrica.</span><span class="sxs-lookup"><span data-stu-id="c11e6-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="c11e6-263">Per altri tipi di avviso, questo è l'ID della risorsa di avviso hello stessa risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="c11e6-264">operationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-264">operationId</span></span> |<span data-ttu-id="c11e6-265">Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="c11e6-266">operationName</span><span class="sxs-lookup"><span data-stu-id="c11e6-266">operationName</span></span> |<span data-ttu-id="c11e6-267">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-267">Name of hello operation.</span></span> |
| <span data-ttu-id="c11e6-268">properties</span><span class="sxs-lookup"><span data-stu-id="c11e6-268">properties</span></span> |<span data-ttu-id="c11e6-269">Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="c11e6-270">status</span><span class="sxs-lookup"><span data-stu-id="c11e6-270">status</span></span> |<span data-ttu-id="c11e6-271">Stringa che descrive lo stato di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="c11e6-272">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="c11e6-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="c11e6-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="c11e6-273">subStatus</span></span> | <span data-ttu-id="c11e6-274">In genere null per gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="c11e6-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="c11e6-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-275">eventTimestamp</span></span> |<span data-ttu-id="c11e6-276">Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c11e6-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="c11e6-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-277">submissionTimestamp</span></span> |<span data-ttu-id="c11e6-278">Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="c11e6-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="c11e6-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c11e6-279">subscriptionId</span></span> |<span data-ttu-id="c11e6-280">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="c11e6-281">Campo delle proprietà per ogni tipo di avviso</span><span class="sxs-lookup"><span data-stu-id="c11e6-281">Properties field per alert type</span></span>
<span data-ttu-id="c11e6-282">campo di proprietà Hello conterrà valori diversi a seconda dell'origine dell'evento di avviso hello hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="c11e6-283">Due comuni provider di eventi di avviso sono gli avvisi e gli avvisi delle metriche del log attività.</span><span class="sxs-lookup"><span data-stu-id="c11e6-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="c11e6-284">Proprietà degli avvisi del log attività</span><span class="sxs-lookup"><span data-stu-id="c11e6-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="c11e6-285">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-285">Element Name</span></span> | <span data-ttu-id="c11e6-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c11e6-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c11e6-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c11e6-287">properties.subscriptionId</span></span> | <span data-ttu-id="c11e6-288">ID sottoscrizione Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="c11e6-289">properties.eventDataId</span></span> | <span data-ttu-id="c11e6-290">dati evento Hello con ID di evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="c11e6-291">properties.resourceGroup</span></span> | <span data-ttu-id="c11e6-292">gruppo di risorse Hello da hello attività Registra evento che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="c11e6-293">properties.resourceId</span></span> | <span data-ttu-id="c11e6-294">ID di risorsa Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-295">properties.eventTimestamp</span></span> | <span data-ttu-id="c11e6-296">timestamp dell'evento Hello dell'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="c11e6-297">properties.operationName</span></span> | <span data-ttu-id="c11e6-298">nome dell'operazione Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="c11e6-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="c11e6-299">properties.status</span></span> | <span data-ttu-id="c11e6-300">stato Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.</span><span class="sxs-lookup"><span data-stu-id="c11e6-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="c11e6-301">Proprietà degli avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="c11e6-301">Properties for metric alerts</span></span>
| <span data-ttu-id="c11e6-302">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-302">Element Name</span></span> | <span data-ttu-id="c11e6-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c11e6-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c11e6-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="c11e6-304">properties.RuleUri</span></span> | <span data-ttu-id="c11e6-305">ID di risorsa di hello metrica regola di avviso stesso.</span><span class="sxs-lookup"><span data-stu-id="c11e6-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="c11e6-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="c11e6-306">properties.RuleName</span></span> | <span data-ttu-id="c11e6-307">nome Hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="c11e6-308">properties.RuleDescription</span></span> | <span data-ttu-id="c11e6-309">descrizione di Hello della regola di avviso metrica hello (come definito nella regola di avviso hello).</span><span class="sxs-lookup"><span data-stu-id="c11e6-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="c11e6-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="c11e6-310">properties.Threshold</span></span> | <span data-ttu-id="c11e6-311">valore di soglia Hello utilizzato nella valutazione di hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="c11e6-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="c11e6-313">dimensione della finestra Hello utilizzato nella valutazione di hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="c11e6-314">properties.Aggregation</span></span> | <span data-ttu-id="c11e6-315">tipo di aggregazione Hello definito nella regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="c11e6-316">properties.Operator</span></span> | <span data-ttu-id="c11e6-317">operatore condizionale Hello utilizzato nella valutazione di hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="c11e6-318">properties.MetricName</span></span> | <span data-ttu-id="c11e6-319">nome della metrica Hello della metrica hello utilizzato nella valutazione di hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="c11e6-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="c11e6-320">properties.MetricUnit</span></span> | <span data-ttu-id="c11e6-321">unità di metrica Hello metrica hello utilizzato nella valutazione di hello della regola di avviso metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="c11e6-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="c11e6-322">Autoscale</span></span>
<span data-ttu-id="c11e6-323">Questa categoria include i record di hello di qualsiasi operazione toohello correlati gli eventi del motore di scalabilità automatica hello in base alle impostazioni di scalabilità automatica che è stato definito nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="c11e6-324">Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "Scalabilità automatica scalabilità verticale azione non riuscita".</span><span class="sxs-lookup"><span data-stu-id="c11e6-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="c11e6-325">Utilizza la scalabilità automatica, è possibile automaticamente scalare in orizzontale o ridimensionare in hello numero di istanze in un tipo di risorsa supportati è basato sull'ora del giorno e/o caricamento dati (metrici) utilizzando un'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c11e6-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="c11e6-326">Quando vengono soddisfatte le condizioni di hello tooscale verso l'alto o verso il basso, hello start e ha avuto esito positivo o gli eventi non riusciti verranno registrati in questa categoria.</span><span class="sxs-lookup"><span data-stu-id="c11e6-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="c11e6-327">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="c11e6-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="c11e6-328">Descrizioni delle proprietà</span><span class="sxs-lookup"><span data-stu-id="c11e6-328">Property descriptions</span></span>
| <span data-ttu-id="c11e6-329">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="c11e6-329">Element Name</span></span> | <span data-ttu-id="c11e6-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c11e6-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c11e6-331">caller</span><span class="sxs-lookup"><span data-stu-id="c11e6-331">caller</span></span> | <span data-ttu-id="c11e6-332">Sempre Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="c11e6-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="c11e6-333">channels</span><span class="sxs-lookup"><span data-stu-id="c11e6-333">channels</span></span> | <span data-ttu-id="c11e6-334">Sempre "Admin, Operation"</span><span class="sxs-lookup"><span data-stu-id="c11e6-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="c11e6-335">claims</span><span class="sxs-lookup"><span data-stu-id="c11e6-335">claims</span></span> | <span data-ttu-id="c11e6-336">Blob JSON con tipo di nome SPN (service principal name) o risorse del motore di scalabilità automatica hello hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="c11e6-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-337">correlationId</span></span> | <span data-ttu-id="c11e6-338">Un GUID in formato stringa hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="c11e6-339">description</span><span class="sxs-lookup"><span data-stu-id="c11e6-339">description</span></span> |<span data-ttu-id="c11e6-340">Descrizione di testo statico dell'evento di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="c11e6-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="c11e6-341">eventDataId</span></span> |<span data-ttu-id="c11e6-342">Identificatore univoco dell'evento di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="c11e6-343">level</span><span class="sxs-lookup"><span data-stu-id="c11e6-343">level</span></span> |<span data-ttu-id="c11e6-344">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-344">Level of hello event.</span></span> <span data-ttu-id="c11e6-345">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="c11e6-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="c11e6-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c11e6-346">resourceGroupName</span></span> |<span data-ttu-id="c11e6-347">Nome del gruppo di risorse hello per l'impostazione di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="c11e6-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="c11e6-348">resourceProviderName</span></span> |<span data-ttu-id="c11e6-349">Nome del provider di risorse hello per l'impostazione di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="c11e6-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="c11e6-350">resourceId</span></span> |<span data-ttu-id="c11e6-351">Id risorsa dell'impostazione di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="c11e6-352">operationId</span><span class="sxs-lookup"><span data-stu-id="c11e6-352">operationId</span></span> |<span data-ttu-id="c11e6-353">Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione.</span><span class="sxs-lookup"><span data-stu-id="c11e6-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="c11e6-354">operationName</span><span class="sxs-lookup"><span data-stu-id="c11e6-354">operationName</span></span> |<span data-ttu-id="c11e6-355">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-355">Name of hello operation.</span></span> |
| <span data-ttu-id="c11e6-356">properties</span><span class="sxs-lookup"><span data-stu-id="c11e6-356">properties</span></span> |<span data-ttu-id="c11e6-357">Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="c11e6-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="c11e6-358">properties.Description</span></span> | <span data-ttu-id="c11e6-359">Descrizione dettagliata di quali motore di scalabilità automatica hello stava eseguendo.</span><span class="sxs-lookup"><span data-stu-id="c11e6-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="c11e6-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="c11e6-360">properties.ResourceName</span></span> | <span data-ttu-id="c11e6-361">ID di risorsa di hello interessati risorse (hello risorsa su cui hello l'esecuzione dell'azione di ridimensionamento)</span><span class="sxs-lookup"><span data-stu-id="c11e6-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="c11e6-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="c11e6-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="c11e6-363">numero di Hello di istanze prima azione di scalabilità automatica hello ha effetto.</span><span class="sxs-lookup"><span data-stu-id="c11e6-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="c11e6-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="c11e6-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="c11e6-365">numero di Hello di istanze dopo l'azione di scalabilità automatica hello ha effetto.</span><span class="sxs-lookup"><span data-stu-id="c11e6-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="c11e6-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="c11e6-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="c11e6-367">Hello timestamp di quando è eseguita hello azione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c11e6-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="c11e6-368">status</span><span class="sxs-lookup"><span data-stu-id="c11e6-368">status</span></span> |<span data-ttu-id="c11e6-369">Stringa che descrive lo stato di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c11e6-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="c11e6-370">Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="c11e6-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="c11e6-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="c11e6-371">subStatus</span></span> | <span data-ttu-id="c11e6-372">In genere null per il ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="c11e6-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="c11e6-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-373">eventTimestamp</span></span> |<span data-ttu-id="c11e6-374">Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c11e6-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="c11e6-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="c11e6-375">submissionTimestamp</span></span> |<span data-ttu-id="c11e6-376">Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="c11e6-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="c11e6-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c11e6-377">subscriptionId</span></span> |<span data-ttu-id="c11e6-378">ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c11e6-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c11e6-379">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c11e6-379">Next steps</span></span>
* [<span data-ttu-id="c11e6-380">Altre informazioni su hello Log attività (in precedenza i log di controllo)</span><span class="sxs-lookup"><span data-stu-id="c11e6-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="c11e6-381">Flusso hello Log attività Azure tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="c11e6-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
