---
title: schema di eventi eventi griglia aaaAzure
description: "Vengono descritte le proprietà di hello forniti per gli eventi con griglia di eventi di Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="45c7d-103">Schema di eventi di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="45c7d-103">Event Grid event schema</span></span>

<span data-ttu-id="45c7d-104">Questo articolo fornisce le proprietà di hello e lo schema per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="45c7d-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="45c7d-105">Gli eventi sono costituiti da un set di cinque proprietà di tipo stringa obbligatorie e un oggetto **data** obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="45c7d-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="45c7d-106">proprietà Hello sono comuni tooall eventi da qualsiasi server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="45c7d-107">Hello **dati** oggetto contiene proprietà che sono server di pubblicazione tooeach specifico.</span><span class="sxs-lookup"><span data-stu-id="45c7d-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="45c7d-108">Gli argomenti di sistema, queste proprietà sono i provider di risorse toohello specifico, ad esempio archiviazione o hub eventi.</span><span class="sxs-lookup"><span data-stu-id="45c7d-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="45c7d-109">Gli eventi vengono inviati tooAzure griglia eventi in una matrice, che può contenere più oggetti evento.</span><span class="sxs-lookup"><span data-stu-id="45c7d-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="45c7d-110">Se è presente solo un singolo evento, la matrice hello ha una lunghezza pari a 1.</span><span class="sxs-lookup"><span data-stu-id="45c7d-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="45c7d-111">Proprietà degli eventi</span><span class="sxs-lookup"><span data-stu-id="45c7d-111">Event properties</span></span>

<span data-ttu-id="45c7d-112">Tutti gli eventi conterranno hello stesso seguenti dati di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="45c7d-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="45c7d-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="45c7d-113">Property</span></span> | <span data-ttu-id="45c7d-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="45c7d-114">Type</span></span> | <span data-ttu-id="45c7d-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45c7d-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="45c7d-116">argomento</span><span class="sxs-lookup"><span data-stu-id="45c7d-116">topic</span></span> | <span data-ttu-id="45c7d-117">string</span><span class="sxs-lookup"><span data-stu-id="45c7d-117">string</span></span> | <span data-ttu-id="45c7d-118">Origine di eventi toohello percorso completo della risorsa.</span><span class="sxs-lookup"><span data-stu-id="45c7d-118">Full resource path toohello event source.</span></span> <span data-ttu-id="45c7d-119">Questo campo non è scrivibile.</span><span class="sxs-lookup"><span data-stu-id="45c7d-119">This field is not writeable.</span></span> |
| <span data-ttu-id="45c7d-120">subject</span><span class="sxs-lookup"><span data-stu-id="45c7d-120">subject</span></span> | <span data-ttu-id="45c7d-121">string</span><span class="sxs-lookup"><span data-stu-id="45c7d-121">string</span></span> | <span data-ttu-id="45c7d-122">Oggetto evento toohello del percorso definito server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="45c7d-123">eventType</span><span class="sxs-lookup"><span data-stu-id="45c7d-123">eventType</span></span> | <span data-ttu-id="45c7d-124">string</span><span class="sxs-lookup"><span data-stu-id="45c7d-124">string</span></span> | <span data-ttu-id="45c7d-125">Uno dei hello registrato i tipi di evento per l'origine evento.</span><span class="sxs-lookup"><span data-stu-id="45c7d-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="45c7d-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="45c7d-126">eventTime</span></span> | <span data-ttu-id="45c7d-127">string</span><span class="sxs-lookup"><span data-stu-id="45c7d-127">string</span></span> | <span data-ttu-id="45c7d-128">eventi di hello Hello viene generato in base all'ora UTC del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="45c7d-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="45c7d-129">id</span><span class="sxs-lookup"><span data-stu-id="45c7d-129">id</span></span> | <span data-ttu-id="45c7d-130">string</span><span class="sxs-lookup"><span data-stu-id="45c7d-130">string</span></span> | <span data-ttu-id="45c7d-131">Identificatore univoco per l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="45c7d-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="45c7d-132">data</span><span class="sxs-lookup"><span data-stu-id="45c7d-132">data</span></span> | <span data-ttu-id="45c7d-133">object</span><span class="sxs-lookup"><span data-stu-id="45c7d-133">object</span></span> | <span data-ttu-id="45c7d-134">Provider di risorse toohello specifico di dati di evento.</span><span class="sxs-lookup"><span data-stu-id="45c7d-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="45c7d-135">Origini evento disponibili</span><span class="sxs-lookup"><span data-stu-id="45c7d-135">Available event sources</span></span>

<span data-ttu-id="45c7d-136">le seguenti origini evento Hello pubblica eventi per l'utilizzo tramite la griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="45c7d-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="45c7d-137">Gruppi di risorse (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="45c7d-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="45c7d-138">Sottoscrizioni di Azure (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="45c7d-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="45c7d-139">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="45c7d-139">Event Hubs</span></span>
* <span data-ttu-id="45c7d-140">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="45c7d-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="45c7d-141">Sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="45c7d-141">Azure Subscriptions</span></span>

<span data-ttu-id="45c7d-142">Le sottoscrizioni di Azure possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="45c7d-143">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="45c7d-143">Available event types</span></span>

- <span data-ttu-id="45c7d-144">**Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="45c7d-145">**Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="45c7d-146">**Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="45c7d-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="45c7d-147">**Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="45c7d-148">**Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="45c7d-149">**Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="45c7d-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="45c7d-150">Ciò si verifica quando viene annullata la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="45c7d-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="45c7d-151">Schema di eventi di esempio</span><span class="sxs-lookup"><span data-stu-id="45c7d-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="45c7d-152">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="45c7d-152">Resource Groups</span></span>

<span data-ttu-id="45c7d-153">I gruppi di risorse possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="45c7d-154">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="45c7d-154">Available event types</span></span>

- <span data-ttu-id="45c7d-155">**Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="45c7d-156">**Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="45c7d-157">**Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="45c7d-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="45c7d-158">**Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="45c7d-159">**Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="45c7d-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="45c7d-160">**Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata.</span><span class="sxs-lookup"><span data-stu-id="45c7d-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="45c7d-161">Ciò si verifica quando viene annullata la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="45c7d-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="45c7d-162">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="45c7d-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="45c7d-163">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="45c7d-163">Event Hubs</span></span>

<span data-ttu-id="45c7d-164">Eventi di hub di eventi appartengono generato solo quando un file viene inviato automaticamente toostorage utilizzando la funzionalità di acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="45c7d-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="45c7d-165">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="45c7d-165">Available event types</span></span>

- <span data-ttu-id="45c7d-166">**Microsoft.EventHub.CaptureFileCreated**: generato quando viene creato un file di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="45c7d-167">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="45c7d-167">Example event</span></span>

<span data-ttu-id="45c7d-168">Questo evento di esempio mostra schema hello di un evento di hub di eventi generato quando viene archiviato un file di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="45c7d-169">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="45c7d-169">Azure Blob Storage</span></span>

<span data-ttu-id="45c7d-170">Archiviazione BLOB di Azure in anteprima privata con registrazione per l'integrazione con Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="45c7d-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="45c7d-171">Tipi di evento disponibili</span><span class="sxs-lookup"><span data-stu-id="45c7d-171">Available event types</span></span>

- <span data-ttu-id="45c7d-172">**Microsoft.Storage.BlobCreated**: generato quando viene creato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="45c7d-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="45c7d-173">**Microsoft.Storage.BlobDeleted**: generato quando viene eliminato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="45c7d-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="45c7d-174">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="45c7d-174">Example event</span></span>

<span data-ttu-id="45c7d-175">Questo evento di esempio mostra schema hello di un evento di archiviazione generato quando viene creato un blob.</span><span class="sxs-lookup"><span data-stu-id="45c7d-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="45c7d-176">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="45c7d-176">Custom Topics</span></span>

<span data-ttu-id="45c7d-177">payload dei dati degli eventi personalizzati Hello è definito dall'utente e può essere qualsiasi JSON corretto.</span><span class="sxs-lookup"><span data-stu-id="45c7d-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="45c7d-178">dati di livello principale Hello devono contenere hello stessi campi come eventi standard risorsa definita.</span><span class="sxs-lookup"><span data-stu-id="45c7d-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="45c7d-179">Quando si pubblicano gli argomenti di eventi toocustom è necessario considerare il soggetto hello del tooaid eventi routing e il filtro di modellazione.</span><span class="sxs-lookup"><span data-stu-id="45c7d-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="45c7d-180">Evento di esempio</span><span class="sxs-lookup"><span data-stu-id="45c7d-180">Example event</span></span>

<span data-ttu-id="45c7d-181">Hello di esempio seguente viene illustrato un evento per un argomento personalizzato:</span><span class="sxs-lookup"><span data-stu-id="45c7d-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="45c7d-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45c7d-182">Next steps</span></span>

* <span data-ttu-id="45c7d-183">Per un'introduzione tooEvent griglia, vedere [che cos'è una griglia di eventi?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="45c7d-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="45c7d-184">toolearn sulla creazione di una sottoscrizione di griglia di eventi, vedere [schema sottoscrizione evento griglia](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="45c7d-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
