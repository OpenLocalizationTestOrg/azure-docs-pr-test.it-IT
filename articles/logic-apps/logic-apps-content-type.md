---
title: Gestire tipi di contenuto - App per la logica di Azure | Documentazione Microsoft
description: 'Procedura: come App per la logica di Azure gestisce i tipi di contenuto in fase di progettazione e di runtime'
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="a6fad-103">Gestire i tipi di contenuto di app per la logica</span><span class="sxs-lookup"><span data-stu-id="a6fad-103">Handle content types in logic apps</span></span>

<span data-ttu-id="a6fad-104">Molti tipi diversi di contenuto possono attraversare un'app per la logica, tra cui JSON, XML, file flat e dati binari.</span><span class="sxs-lookup"><span data-stu-id="a6fad-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="a6fad-105">Sebbene il motore di App per la logica supporti tutti i tipi di contenuto, alcuni vengono riconosciuti in modo nativo dal motore.</span><span class="sxs-lookup"><span data-stu-id="a6fad-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="a6fad-106">Altri potrebbero richiedere cast o conversioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="a6fad-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="a6fad-107">Questo articolo descrive come il motore gestisce i differenti tipi di contenuto e come gestire correttamente questi tipi quando è necessario.</span><span class="sxs-lookup"><span data-stu-id="a6fad-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="a6fad-108">Intestazione Content-Type</span><span class="sxs-lookup"><span data-stu-id="a6fad-108">Content-Type Header</span></span>

<span data-ttu-id="a6fad-109">Per semplicità, esaminiamo due valori `Content-Types` che non richiedono alcuna conversione o cast da usare nei tipi di contenuto `application/json` e `text/plain` di un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a6fad-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="a6fad-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="a6fad-110">Application/JSON</span></span>

<span data-ttu-id="a6fad-111">Il motore del flusso di lavoro si basa sull'intestazione `Content-Type` delle chiamate HTTP per determinare la gestione appropriata.</span><span class="sxs-lookup"><span data-stu-id="a6fad-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="a6fad-112">Qualsiasi richiesta con tipo di contenuto `application/json` viene archiviata e gestita come un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="a6fad-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="a6fad-113">Per impostazione predefinita, il contenuto JSON può anche essere analizzato senza che sia necessario alcun cast.</span><span class="sxs-lookup"><span data-stu-id="a6fad-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="a6fad-114">Ad esempio, è possibile analizzare una richiesta con l'intestazione content-type `application/json ` in un flusso di lavoro usando un'espressione come `@body('myAction')['foo'][0]` per ottenere il valore `bar` in questo caso:</span><span class="sxs-lookup"><span data-stu-id="a6fad-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="a6fad-115">Non è necessario alcun cast aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="a6fad-115">No additional casting is needed.</span></span> <span data-ttu-id="a6fad-116">Se si lavora con dati JSON ma non è stata specificata un'intestazione, è possibile impostare manualmente i dati su JSON usando la funzione `@json()`, ad esempio `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="a6fad-117">Schema e generatore di schemi</span><span class="sxs-lookup"><span data-stu-id="a6fad-117">Schema and schema generator</span></span>

<span data-ttu-id="a6fad-118">Il trigger della richiesta consente di immettere uno schema JSON per il payload che si prevede di ricevere.</span><span class="sxs-lookup"><span data-stu-id="a6fad-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="a6fad-119">Questo schema consente alla finestra di progettazione di generare token per consentire di usare il contenuto della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a6fad-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="a6fad-120">Se non si dispone di uno schema pronto, selezionare **Usare il payload di esempio per generare lo schema** per generare uno schema JSON da un payload di esempio.</span><span class="sxs-lookup"><span data-stu-id="a6fad-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="a6fad-122">Azione di "analisi JSON"</span><span class="sxs-lookup"><span data-stu-id="a6fad-122">'Parse JSON' action</span></span>

<span data-ttu-id="a6fad-123">L'azione `Parse JSON` consente di analizzare il contenuto JSON in token descrittivi per l'uso di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a6fad-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="a6fad-124">Analogamente al trigger di richiesta, questa azione consente di immettere o generare uno schema JSON per il contenuto da analizzare.</span><span class="sxs-lookup"><span data-stu-id="a6fad-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="a6fad-125">Questo strumento rende molto più semplice l'uso di dati da Bus di servizio, Cosmos DB e così via.</span><span class="sxs-lookup"><span data-stu-id="a6fad-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Analizzare JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="a6fad-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="a6fad-127">Text/plain</span></span>

<span data-ttu-id="a6fad-128">Come per `application/json`, i messaggi HTTP ricevuti con l'intestazione `Content-Type` di `text/plain` vengono archiviati nel formato non elaborato.</span><span class="sxs-lookup"><span data-stu-id="a6fad-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="a6fad-129">Inoltre, se questi messaggi sono inclusi in azioni successive senza eseguire il cast, queste richieste passano con l'intestazione `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="a6fad-130">Ad esempio, quando si usa un file flat, è possibile che venga visualizzato questo contenuto HTTP come `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="a6fad-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="a6fad-131">Se nell'azione successiva si invia la richiesta come corpo di un'altra richiesta (`@body('flatfile')`), la richiesta avrà un'intestazione Content-Type `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="a6fad-132">Se si lavora con dati che sono testo normale ma non è stata specificata un'intestazione, è possibile impostare manualmente i dati come testo usando la funzione `@string()`, ad esempio `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="a6fad-133">Application/xml, Application/octet-stream e funzioni del convertitore</span><span class="sxs-lookup"><span data-stu-id="a6fad-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="a6fad-134">Il motore dell'app per la logica mantiene sempre il valore `Content-Type` che è stato ricevuto per la richiesta o risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6fad-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="a6fad-135">Se quindi il motore riceve contenuto con il `Content-Type` di `application/octet-stream` e si include questo contenuto in un'azione successiva senza eseguire il cast, la richiesta in uscita ha `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="a6fad-136">In questo modo, il motore può garantire che non vengano persi dati durante lo spostamento nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a6fad-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="a6fad-137">Tuttavia, lo stato dell'azione, ovvero gli input e gli output, viene archiviato in un oggetto JSON mentre attraversa il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a6fad-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="a6fad-138">Per mantenere alcuni tipi di dati, il motore converte il contenuto in una stringa binaria con codifica Base64, con i metadati appropriati per conservare sia `$content` che `$content-type`, che viene automaticamente convertita.</span><span class="sxs-lookup"><span data-stu-id="a6fad-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="a6fad-139">`@json()`: esegue il cast dei dati in `application/json`</span><span class="sxs-lookup"><span data-stu-id="a6fad-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="a6fad-140">`@xml()`: esegue il cast dei dati in `application/xml`</span><span class="sxs-lookup"><span data-stu-id="a6fad-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="a6fad-141">`@binary()`: esegue il cast dei dati in `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="a6fad-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="a6fad-142">`@string()`: esegue il cast dei dati in `text/plain`</span><span class="sxs-lookup"><span data-stu-id="a6fad-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="a6fad-143">`@base64()` : converte il contenuto in una stringa Base64</span><span class="sxs-lookup"><span data-stu-id="a6fad-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="a6fad-144">`@base64toString()`: converte una stringa Base64 codificata in `text/plain`</span><span class="sxs-lookup"><span data-stu-id="a6fad-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="a6fad-145">`@base64toBinary()`: converte una stringa Base64 codificata in `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="a6fad-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="a6fad-146">`@encodeDataUri()` : codifica una stringa come matrice di byte dataUri</span><span class="sxs-lookup"><span data-stu-id="a6fad-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="a6fad-147">`@decodeDataUri()` : decodifica un dataUri in una matrice di byte</span><span class="sxs-lookup"><span data-stu-id="a6fad-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="a6fad-148">Ad esempio, se si riceve una richiesta HTTP con `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="a6fad-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="a6fad-149">Si potrebbe eseguire il cast e usarlo in un secondo tempo con un elemento simile a `@xml(triggerBody())` o all'interno di una funzione come `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="a6fad-150">Altri tipi di contenuto</span><span class="sxs-lookup"><span data-stu-id="a6fad-150">Other content types</span></span>

<span data-ttu-id="a6fad-151">Esistono altri tipi di contenuto che sono supportati e funzionano con le app per la logica, ma potrebbero richiedere il recupero manuale del corpo del messaggio con la decodifica di `$content`.</span><span class="sxs-lookup"><span data-stu-id="a6fad-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="a6fad-152">Ad esempio si supponga di attivare una richiesta `application/x-www-url-formencoded` dove `$content` rappresenta il payload codificato come stringa Base64 per mantenere tutti i dati:</span><span class="sxs-lookup"><span data-stu-id="a6fad-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="a6fad-153">Poiché la richiesta non è in testo normale o JSON, la richiesta viene archiviata nell'azione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a6fad-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Poiché al momento non esiste una funzione nativa per dati del modulo, questi dati possono essere usati all'interno di un flusso di lavoro eseguendo manualmente l'accesso ai dati con una funzione come `@string(body('formdataAction'))`. Se la richiesta in uscita deve avere anche l'intestazione content-type `application/x-www-url-formencoded`, è sufficiente aggiungere la richiesta al corpo dell'azione senza cast come `@body('formdataAction')`. Questo metodo tuttavia funziona solo se il corpo è l'unico parametro nell'input `body`. <span data-ttu-id="a6fad-157">Se si tenta di usare `@body('formdataAction')` in una richiesta `application/json`, verrà visualizzato un errore di runtime perché viene inviato il corpo codificato.</span><span class="sxs-lookup"><span data-stu-id="a6fad-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

