---
title: Schema di sottoscrizione per Griglia di eventi di Azure
description: "Descrive le proprietà per la sottoscrizione a un evento con Griglia di eventi di Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="dec4c-103">Schema di sottoscrizione per Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="dec4c-103">Event Grid subscription schema</span></span>

<span data-ttu-id="dec4c-104">Per creare una sottoscrizione di Griglia di eventi, si invia una richiesta all'operazione di sottoscrizione Crea evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="dec4c-105">Utilizzare il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="dec4c-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="dec4c-106">Ad esempio, per creare una sottoscrizione eventi per un account di archiviazione denominato `examplestorage` in un gruppo di risorse denominato `examplegroup`, usare il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="dec4c-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="dec4c-107">L'articolo descrive le proprietà e lo schema per il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="dec4c-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="dec4c-108">Proprietà delle sottoscrizioni eventi</span><span class="sxs-lookup"><span data-stu-id="dec4c-108">Event subscription properties</span></span>

| <span data-ttu-id="dec4c-109">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dec4c-109">Property</span></span> | <span data-ttu-id="dec4c-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="dec4c-110">Type</span></span> | <span data-ttu-id="dec4c-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dec4c-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="dec4c-112">destination</span><span class="sxs-lookup"><span data-stu-id="dec4c-112">destination</span></span> | <span data-ttu-id="dec4c-113">object</span><span class="sxs-lookup"><span data-stu-id="dec4c-113">object</span></span> | <span data-ttu-id="dec4c-114">Oggetto che definisce l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="dec4c-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="dec4c-115">filter</span><span class="sxs-lookup"><span data-stu-id="dec4c-115">filter</span></span> | <span data-ttu-id="dec4c-116">object</span><span class="sxs-lookup"><span data-stu-id="dec4c-116">object</span></span> | <span data-ttu-id="dec4c-117">Campo facoltativo per il filtro dei tipi di eventi.</span><span class="sxs-lookup"><span data-stu-id="dec4c-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="dec4c-118">oggetto destination</span><span class="sxs-lookup"><span data-stu-id="dec4c-118">destination object</span></span>

| <span data-ttu-id="dec4c-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dec4c-119">Property</span></span> | <span data-ttu-id="dec4c-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="dec4c-120">Type</span></span> | <span data-ttu-id="dec4c-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dec4c-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="dec4c-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="dec4c-122">endpointType</span></span> | <span data-ttu-id="dec4c-123">string</span><span class="sxs-lookup"><span data-stu-id="dec4c-123">string</span></span> | <span data-ttu-id="dec4c-124">Tipo di endpoint per la sottoscrizione (webhook/HTTP, hub eventi o coda).</span><span class="sxs-lookup"><span data-stu-id="dec4c-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="dec4c-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="dec4c-125">endpointUrl</span></span> | <span data-ttu-id="dec4c-126">string</span><span class="sxs-lookup"><span data-stu-id="dec4c-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="dec4c-127">oggetto filter</span><span class="sxs-lookup"><span data-stu-id="dec4c-127">filter object</span></span>

| <span data-ttu-id="dec4c-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dec4c-128">Property</span></span> | <span data-ttu-id="dec4c-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="dec4c-129">Type</span></span> | <span data-ttu-id="dec4c-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dec4c-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="dec4c-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="dec4c-131">includedEventTypes</span></span> | <span data-ttu-id="dec4c-132">array</span><span class="sxs-lookup"><span data-stu-id="dec4c-132">array</span></span> | <span data-ttu-id="dec4c-133">Corrisponde se il tipo di evento nel messaggio di evento è una corrispondenza esatta a uno di questi nomi di tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="dec4c-134">Genera un errore se il nome dell'evento non corrisponde ad alcuno dei nomi di tipo di evento registrati per l'origine evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="dec4c-135">Il valore predefinito corrisponde a tutti i tipi di evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-135">Default matches all event types.</span></span> |
| <span data-ttu-id="dec4c-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="dec4c-136">subjectBeginsWith</span></span> | <span data-ttu-id="dec4c-137">string</span><span class="sxs-lookup"><span data-stu-id="dec4c-137">string</span></span> | <span data-ttu-id="dec4c-138">Filtro di corrispondenza del prefisso per il campo dell'oggetto nel messaggio dell'evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="dec4c-139">La stringa predefinita o una stringa vuota corrisponde sempre.</span><span class="sxs-lookup"><span data-stu-id="dec4c-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="dec4c-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="dec4c-140">subjectEndsWith</span></span> | <span data-ttu-id="dec4c-141">string</span><span class="sxs-lookup"><span data-stu-id="dec4c-141">string</span></span> | <span data-ttu-id="dec4c-142">Filtro di corrispondenza del suffisso per il campo dell'oggetto nel messaggio dell'evento.</span><span class="sxs-lookup"><span data-stu-id="dec4c-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="dec4c-143">La stringa predefinita o una stringa vuota corrisponde sempre.</span><span class="sxs-lookup"><span data-stu-id="dec4c-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="dec4c-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="dec4c-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="dec4c-145">string</span><span class="sxs-lookup"><span data-stu-id="dec4c-145">string</span></span> | <span data-ttu-id="dec4c-146">Controlla la corrispondenza tra maiuscole e minuscole per i filtri.</span><span class="sxs-lookup"><span data-stu-id="dec4c-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="dec4c-147">Schema di sottoscrizione di esempio</span><span class="sxs-lookup"><span data-stu-id="dec4c-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dec4c-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dec4c-148">Next steps</span></span>

* <span data-ttu-id="dec4c-149">Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md)</span><span class="sxs-lookup"><span data-stu-id="dec4c-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>