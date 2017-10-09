---
title: schema di sottoscrizione evento griglia aaaAzure
description: "Descrive le proprietà di hello per la sottoscrizione dell'evento tooan con griglia di eventi di Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Schema di sottoscrizione per Griglia di eventi

una sottoscrizione di evento griglia toocreate, si invia un toohello richiesta operazione sottoscrizione Create Event. Utilizzare hello seguente formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Ad esempio, toocreate una sottoscrizione di eventi per un account di archiviazione denominato `examplestorage` in un gruppo di risorse denominato `examplegroup`, utilizzare hello seguente formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hello descritti proprietà hello e sullo schema per il corpo della richiesta di hello hello.
 
## <a name="event-subscription-properties"></a>Proprietà delle sottoscrizioni eventi

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| destination | object | oggetto Hello che definisce l'endpoint di hello. |
| filter | object | Un campo facoltativo per filtrare hello tipi di eventi. |

### <a name="destination-object"></a>oggetto destination

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| endpointType | string | tipo di Hello di endpoint per la sottoscrizione di hello (webhook/HTTP, Hub eventi o coda). | 
| endpointUrl | string |  | 

### <a name="filter-object"></a>oggetto filter

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| includedEventTypes | array | Corrispondenza quando il tipo di evento hello nel messaggio di evento hello tooone una corrispondenza esatta dei seguenti nomi di tipo di evento. Genera un errore quando il nome di evento non corrisponde a nomi di tipi di evento hello registrato per l'origine evento hello. Il valore predefinito corrisponde a tutti i tipi di evento. |
| subjectBeginsWith | string | Corrispondenza di prefisso filtro toohello soggetto campo nel messaggio di evento hello. valore predefinito di Hello o stringa vuota corrisponde a tutti. | 
| subjectEndsWith | string | Suffisso corrispondenza filtro toohello soggetto campo nel messaggio di evento hello. valore predefinito di Hello o stringa vuota corrisponde a tutti. |
| subjectIsCaseSensitive | string | Controlla la corrispondenza tra maiuscole e minuscole per i filtri. |


## <a name="example-subscription-schema"></a>Schema di sottoscrizione di esempio

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione tooEvent griglia, vedere [che cos'è una griglia di eventi?](overview.md)
