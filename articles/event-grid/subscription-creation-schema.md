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
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="b0f61-103">Schema di sottoscrizione per Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="b0f61-103">Event Grid subscription schema</span></span>

<span data-ttu-id="b0f61-104">una sottoscrizione di evento griglia toocreate, si invia un toohello richiesta operazione sottoscrizione Create Event.</span><span class="sxs-lookup"><span data-stu-id="b0f61-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="b0f61-105">Utilizzare hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="b0f61-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="b0f61-106">Ad esempio, toocreate una sottoscrizione di eventi per un account di archiviazione denominato `examplestorage` in un gruppo di risorse denominato `examplegroup`, utilizzare hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="b0f61-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="b0f61-107">Hello descritti proprietà hello e sullo schema per il corpo della richiesta di hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0f61-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="b0f61-108">Proprietà delle sottoscrizioni eventi</span><span class="sxs-lookup"><span data-stu-id="b0f61-108">Event subscription properties</span></span>

| <span data-ttu-id="b0f61-109">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b0f61-109">Property</span></span> | <span data-ttu-id="b0f61-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="b0f61-110">Type</span></span> | <span data-ttu-id="b0f61-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0f61-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b0f61-112">destination</span><span class="sxs-lookup"><span data-stu-id="b0f61-112">destination</span></span> | <span data-ttu-id="b0f61-113">object</span><span class="sxs-lookup"><span data-stu-id="b0f61-113">object</span></span> | <span data-ttu-id="b0f61-114">oggetto Hello che definisce l'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="b0f61-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="b0f61-115">filter</span><span class="sxs-lookup"><span data-stu-id="b0f61-115">filter</span></span> | <span data-ttu-id="b0f61-116">object</span><span class="sxs-lookup"><span data-stu-id="b0f61-116">object</span></span> | <span data-ttu-id="b0f61-117">Un campo facoltativo per filtrare hello tipi di eventi.</span><span class="sxs-lookup"><span data-stu-id="b0f61-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="b0f61-118">oggetto destination</span><span class="sxs-lookup"><span data-stu-id="b0f61-118">destination object</span></span>

| <span data-ttu-id="b0f61-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b0f61-119">Property</span></span> | <span data-ttu-id="b0f61-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="b0f61-120">Type</span></span> | <span data-ttu-id="b0f61-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0f61-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b0f61-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="b0f61-122">endpointType</span></span> | <span data-ttu-id="b0f61-123">string</span><span class="sxs-lookup"><span data-stu-id="b0f61-123">string</span></span> | <span data-ttu-id="b0f61-124">tipo di Hello di endpoint per la sottoscrizione di hello (webhook/HTTP, Hub eventi o coda).</span><span class="sxs-lookup"><span data-stu-id="b0f61-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="b0f61-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="b0f61-125">endpointUrl</span></span> | <span data-ttu-id="b0f61-126">string</span><span class="sxs-lookup"><span data-stu-id="b0f61-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="b0f61-127">oggetto filter</span><span class="sxs-lookup"><span data-stu-id="b0f61-127">filter object</span></span>

| <span data-ttu-id="b0f61-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b0f61-128">Property</span></span> | <span data-ttu-id="b0f61-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="b0f61-129">Type</span></span> | <span data-ttu-id="b0f61-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0f61-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b0f61-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="b0f61-131">includedEventTypes</span></span> | <span data-ttu-id="b0f61-132">array</span><span class="sxs-lookup"><span data-stu-id="b0f61-132">array</span></span> | <span data-ttu-id="b0f61-133">Corrispondenza quando il tipo di evento hello nel messaggio di evento hello tooone una corrispondenza esatta dei seguenti nomi di tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="b0f61-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="b0f61-134">Genera un errore quando il nome di evento non corrisponde a nomi di tipi di evento hello registrato per l'origine evento hello.</span><span class="sxs-lookup"><span data-stu-id="b0f61-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="b0f61-135">Il valore predefinito corrisponde a tutti i tipi di evento.</span><span class="sxs-lookup"><span data-stu-id="b0f61-135">Default matches all event types.</span></span> |
| <span data-ttu-id="b0f61-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="b0f61-136">subjectBeginsWith</span></span> | <span data-ttu-id="b0f61-137">string</span><span class="sxs-lookup"><span data-stu-id="b0f61-137">string</span></span> | <span data-ttu-id="b0f61-138">Corrispondenza di prefisso filtro toohello soggetto campo nel messaggio di evento hello.</span><span class="sxs-lookup"><span data-stu-id="b0f61-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="b0f61-139">valore predefinito di Hello o stringa vuota corrisponde a tutti.</span><span class="sxs-lookup"><span data-stu-id="b0f61-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="b0f61-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="b0f61-140">subjectEndsWith</span></span> | <span data-ttu-id="b0f61-141">string</span><span class="sxs-lookup"><span data-stu-id="b0f61-141">string</span></span> | <span data-ttu-id="b0f61-142">Suffisso corrispondenza filtro toohello soggetto campo nel messaggio di evento hello.</span><span class="sxs-lookup"><span data-stu-id="b0f61-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="b0f61-143">valore predefinito di Hello o stringa vuota corrisponde a tutti.</span><span class="sxs-lookup"><span data-stu-id="b0f61-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="b0f61-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="b0f61-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="b0f61-145">string</span><span class="sxs-lookup"><span data-stu-id="b0f61-145">string</span></span> | <span data-ttu-id="b0f61-146">Controlla la corrispondenza tra maiuscole e minuscole per i filtri.</span><span class="sxs-lookup"><span data-stu-id="b0f61-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="b0f61-147">Schema di sottoscrizione di esempio</span><span class="sxs-lookup"><span data-stu-id="b0f61-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b0f61-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0f61-148">Next steps</span></span>

* <span data-ttu-id="b0f61-149">Per un'introduzione tooEvent griglia, vedere [che cos'è una griglia di eventi?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="b0f61-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
