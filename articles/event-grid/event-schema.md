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
# <a name="event-grid-event-schema"></a>Schema di eventi di Griglia di eventi

Questo articolo fornisce le proprietà di hello e lo schema per gli eventi. Gli eventi sono costituiti da un set di cinque proprietà di tipo stringa obbligatorie e un oggetto **data** obbligatorio. proprietà Hello sono comuni tooall eventi da qualsiasi server di pubblicazione. Hello **dati** oggetto contiene proprietà che sono server di pubblicazione tooeach specifico. Gli argomenti di sistema, queste proprietà sono i provider di risorse toohello specifico, ad esempio archiviazione o hub eventi.

Gli eventi vengono inviati tooAzure griglia eventi in una matrice, che può contenere più oggetti evento. Se è presente solo un singolo evento, la matrice hello ha una lunghezza pari a 1. 
 
## <a name="event-properties"></a>Proprietà degli eventi

Tutti gli eventi conterranno hello stesso seguenti dati di livello superiore.

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| argomento | string | Origine di eventi toohello percorso completo della risorsa. Questo campo non è scrivibile. |
| subject | string | Oggetto evento toohello del percorso definito server di pubblicazione. |
| eventType | string | Uno dei hello registrato i tipi di evento per l'origine evento. |
| eventTime | string | eventi di hello Hello viene generato in base all'ora UTC del provider di hello. |
| id | string | Identificatore univoco per l'evento hello. |
| data | object | Provider di risorse toohello specifico di dati di evento. |

## <a name="available-event-sources"></a>Origini evento disponibili

le seguenti origini evento Hello pubblica eventi per l'utilizzo tramite la griglia di eventi:

* Gruppi di risorse (operazioni di gestione)
* Sottoscrizioni di Azure (operazioni di gestione)
* Hub eventi
* Argomenti personalizzati

## <a name="azure-subscriptions"></a>Sottoscrizioni di Azure

Le sottoscrizioni di Azure possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.

### <a name="available-event-types"></a>Tipi di evento disponibili

- **Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.  
- **Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.  
- **Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.  
- **Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.  
- **Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.  
- **Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata. Ciò si verifica quando viene annullata la distribuzione dei modelli.

### <a name="example-event-schema"></a>Schema di eventi di esempio

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



## <a name="resource-groups"></a>Gruppi di risorse

I gruppi di risorse possono ora generare eventi di gestione da Azure Resource Manager, ad esempio quando viene creata una VM o viene eliminato un account di archiviazione.

### <a name="available-event-types"></a>Tipi di evento disponibili

- **Microsoft.Resources.ResourceWriteSuccess**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito positivo.  
- **Microsoft.Resources.ResourceWriteFailure**: generato quando un'operazione di creazione o aggiornamento di una risorsa ha esito negativo.  
- **Microsoft.Resources.ResourceWriteCancel**: generato quando un'operazione di creazione o aggiornamento di una risorsa viene annullata.  
- **Microsoft.Resources.ResourceDeleteSuccess**: generato quando un'operazione di eliminazione di una risorsa ha esito positivo.  
- **Microsoft.Resources.ResourceDeleteFailure**: generato quando un'operazione di eliminazione di una risorsa ha esito negativo.  
- **Microsoft.Resources.ResourceDeleteCancel**: generato quando un'operazione di eliminazione di una risorsa viene annullata. Ciò si verifica quando viene annullata la distribuzione dei modelli.

### <a name="example-event"></a>Evento di esempio

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



## <a name="event-hubs"></a>Hub eventi

Eventi di hub di eventi appartengono generato solo quando un file viene inviato automaticamente toostorage utilizzando la funzionalità di acquisizione hello.

### <a name="available-event-types"></a>Tipi di evento disponibili

- **Microsoft.EventHub.CaptureFileCreated**: generato quando viene creato un file di acquisizione.

### <a name="example-event"></a>Evento di esempio

Questo evento di esempio mostra schema hello di un evento di hub di eventi generato quando viene archiviato un file di acquisizione. 

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



## <a name="azure-blob-storage"></a>Archiviazione BLOB di Azure

Archiviazione BLOB di Azure in anteprima privata con registrazione per l'integrazione con Griglia di eventi.

### <a name="available-event-types"></a>Tipi di evento disponibili

- **Microsoft.Storage.BlobCreated**: generato quando viene creato un BLOB.
- **Microsoft.Storage.BlobDeleted**: generato quando viene eliminato un BLOB.

### <a name="example-event"></a>Evento di esempio

Questo evento di esempio mostra schema hello di un evento di archiviazione generato quando viene creato un blob. 

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




## <a name="custom-topics"></a>Argomenti personalizzati

payload dei dati degli eventi personalizzati Hello è definito dall'utente e può essere qualsiasi JSON corretto. dati di livello principale Hello devono contenere hello stessi campi come eventi standard risorsa definita. Quando si pubblicano gli argomenti di eventi toocustom è necessario considerare il soggetto hello del tooaid eventi routing e il filtro di modellazione.

### <a name="example-event"></a>Evento di esempio

Hello di esempio seguente viene illustrato un evento per un argomento personalizzato:
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

## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione tooEvent griglia, vedere [che cos'è una griglia di eventi?](overview.md)
* toolearn sulla creazione di una sottoscrizione di griglia di eventi, vedere [schema sottoscrizione evento griglia](subscription-creation-schema.md).
