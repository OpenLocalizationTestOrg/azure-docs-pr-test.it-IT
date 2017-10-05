---
title: Schema di eventi di Griglia di eventi di Azure
description: "Vengono descritte le proprietà disponibili per gli eventi con Griglia di eventi di Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="f5d60-103">Schema di eventi di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="f5d60-103">Event Grid event schema</span></span>

<span data-ttu-id="f5d60-104">Questo articolo illustra le proprietà e lo schema per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="f5d60-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="f5d60-105">Gli eventi sono costituiti da un set di cinque proprietà di tipo stringa obbligatorie e un oggetto **data** obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f5d60-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="f5d60-106">Le proprietà sono comuni a tutti gli eventi di tutti gli autori.</span><span class="sxs-lookup"><span data-stu-id="f5d60-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="f5d60-107">L'oggetto **data** contiene le proprietà specifiche per ogni autore.</span><span class="sxs-lookup"><span data-stu-id="f5d60-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="f5d60-108">Per gli argomenti di sistema, le proprietà sono specifiche del provider di risorse, ad esempio Archiviazione o Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f5d60-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="f5d60-109">Gli eventi vengono inviati a Griglia di eventi di Azure in una matrice, che può contenere più oggetti evento.</span><span class="sxs-lookup"><span data-stu-id="f5d60-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="f5d60-110">Se c'è un unico evento, la matrice ha una lunghezza pari a 1.</span><span class="sxs-lookup"><span data-stu-id="f5d60-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="f5d60-111">Proprietà degli eventi</span><span class="sxs-lookup"><span data-stu-id="f5d60-111">Event properties</span></span>

<span data-ttu-id="f5d60-112">Tutti gli eventi contengono gli stessi dati di livello principale indicati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f5d60-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="f5d60-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f5d60-113">Property</span></span> | <span data-ttu-id="f5d60-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5d60-114">Type</span></span> | <span data-ttu-id="f5d60-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5d60-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="f5d60-116">argomento</span><span class="sxs-lookup"><span data-stu-id="f5d60-116">topic</span></span> | <span data-ttu-id="f5d60-117">string</span><span class="sxs-lookup"><span data-stu-id="f5d60-117">string</span></span> | <span data-ttu-id="f5d60-118">Percorso risorsa completo dell'origine evento.</span><span class="sxs-lookup"><span data-stu-id="f5d60-118">Full resource path to the event source.</span></span> <span data-ttu-id="f5d60-119">Questo campo non è scrivibile.</span><span class="sxs-lookup"><span data-stu-id="f5d60-119">This field is not writeable.</span></span> |
| <span data-ttu-id="f5d60-120">subject</span><span class="sxs-lookup"><span data-stu-id="f5d60-120">subject</span></span> | <span data-ttu-id="f5d60-121">string</span><span class="sxs-lookup"><span data-stu-id="f5d60-121">string</span></span> | <span data-ttu-id="f5d60-122">Percorso dell'oggetto dell'evento definito dall'autore.</span><span class="sxs-lookup"><span data-stu-id="f5d60-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="f5d60-123">eventType</span><span class="sxs-lookup"><span data-stu-id="f5d60-123">eventType</span></span> | <span data-ttu-id="f5d60-124">string</span><span class="sxs-lookup"><span data-stu-id="f5d60-124">string</span></span> | <span data-ttu-id="f5d60-125">Uno dei tipi di evento registrati per l'origine evento.</span><span class="sxs-lookup"><span data-stu-id="f5d60-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="f5d60-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="f5d60-126">eventTime</span></span> | <span data-ttu-id="f5d60-127">string</span><span class="sxs-lookup"><span data-stu-id="f5d60-127">string</span></span> | <span data-ttu-id="f5d60-128">Ora di generazione dell'evento in base all'ora UTC del provider.</span><span class="sxs-lookup"><span data-stu-id="f5d60-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="f5d60-129">id</span><span class="sxs-lookup"><span data-stu-id="f5d60-129">id</span></span> | <span data-ttu-id="f5d60-130">string</span><span class="sxs-lookup"><span data-stu-id="f5d60-130">string</span></span> | <span data-ttu-id="f5d60-131">Identificatore univoco dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f5d60-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="f5d60-132">data</span><span class="sxs-lookup"><span data-stu-id="f5d60-132">data</span></span> | <span data-ttu-id="f5d60-133">object</span><span class="sxs-lookup"><span data-stu-id="f5d60-133">object</span></span> | <span data-ttu-id="f5d60-134">Dati dell'evento specifici del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="f5d60-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="f5d60-135">Origini evento disponibili</span><span class="sxs-lookup"><span data-stu-id="f5d60-135">Available event sources</span></span>

<span data-ttu-id="f5d60-136">Le origini evento seguenti pubblicano gli eventi per l'utilizzo tramite Griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="f5d60-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="f5d60-137">Gruppi di risorse (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="f5d60-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="f5d60-138">Sottoscrizioni di Azure (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="f5d60-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="f5d60-139">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f5d60-139">Event Hubs</span></span>
* <span data-ttu-id="f5d60-140">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="f5d60-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="f5d60-141">Sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f5d60-141">Azure Subscriptions</span></span>

<span data-ttu-id="f5d60-142">Le sottoscrizioni di Azure possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f5d60-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f5d60-143">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="f5d60-143">Available event types</span></span>

- <span data-ttu-id="f5d60-144">**Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="f5d60-145">**Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="f5d60-146">**Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="f5d60-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="f5d60-147">**Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="f5d60-148">**Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="f5d60-149">**Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="f5d60-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="f5d60-150">Ciò si verifica quando viene annullata la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="f5d60-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="f5d60-151">Schema di eventi di esempio</span><span class="sxs-lookup"><span data-stu-id="f5d60-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="f5d60-152">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="f5d60-152">Resource Groups</span></span>

<span data-ttu-id="f5d60-153">I gruppi di risorse possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f5d60-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f5d60-154">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="f5d60-154">Available event types</span></span>

- <span data-ttu-id="f5d60-155">**Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="f5d60-156">**Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="f5d60-157">**Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="f5d60-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="f5d60-158">**Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="f5d60-159">**Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f5d60-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="f5d60-160">**Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="f5d60-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="f5d60-161">Ciò si verifica quando viene annullata la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="f5d60-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="f5d60-162">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="f5d60-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="f5d60-163">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f5d60-163">Event Hubs</span></span>

<span data-ttu-id="f5d60-164">Gli eventi di Hub eventi vengono attualmente generati solo quando un file viene automaticamente inviato al servizio di archiviazione usando la funzionalità di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="f5d60-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f5d60-165">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="f5d60-165">Available event types</span></span>

- <span data-ttu-id="f5d60-166">**Microsoft.EventHub.CaptureFileCreated**: generato quando viene creato un file di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="f5d60-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="f5d60-167">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="f5d60-167">Example event</span></span>

<span data-ttu-id="f5d60-168">Questo evento di esempio mostra lo schema di un evento di Hub eventi generato quando la funzionalità di acquisizione archivia un file.</span><span class="sxs-lookup"><span data-stu-id="f5d60-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="f5d60-169">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="f5d60-169">Azure Blob Storage</span></span>

<span data-ttu-id="f5d60-170">Archiviazione BLOB di Azure in anteprima privata con registrazione per l'integrazione con Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="f5d60-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f5d60-171">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="f5d60-171">Available event types</span></span>

- <span data-ttu-id="f5d60-172">**Microsoft.Storage.BlobCreated**: generato quando viene creato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="f5d60-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="f5d60-173">**Microsoft.Storage.BlobDeleted**: generato quando viene eliminato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="f5d60-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="f5d60-174">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="f5d60-174">Example event</span></span>

<span data-ttu-id="f5d60-175">Questo evento di esempio mostra lo schema di un evento di archiviazione generato quando viene creato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="f5d60-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="f5d60-176">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="f5d60-176">Custom Topics</span></span>

<span data-ttu-id="f5d60-177">Il payload di dati degli eventi personalizzati è definito dall'utente e può essere qualsiasi elemento JSON ben formattato.</span><span class="sxs-lookup"><span data-stu-id="f5d60-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="f5d60-178">I dati di livello principale devono contenere gli stessi campi degli eventi standard definiti dalle risorse.</span><span class="sxs-lookup"><span data-stu-id="f5d60-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="f5d60-179">Quando si pubblicano eventi in argomenti personalizzati, prendere in considerazione la modellazione dell'oggetto degli eventi in modo da supportare le operazioni di instradamento e filtro.</span><span class="sxs-lookup"><span data-stu-id="f5d60-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="f5d60-180">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="f5d60-180">Example event</span></span>

<span data-ttu-id="f5d60-181">L'esempio seguente mostra un evento per un argomento personalizzato:</span><span class="sxs-lookup"><span data-stu-id="f5d60-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="f5d60-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5d60-182">Next steps</span></span>

* <span data-ttu-id="f5d60-183">Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md)</span><span class="sxs-lookup"><span data-stu-id="f5d60-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="f5d60-184">Per informazioni sulla creazione di una sottoscrizione di Griglia di eventi, vedere [Schema di sottoscrizione per Griglia di eventi](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5d60-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
