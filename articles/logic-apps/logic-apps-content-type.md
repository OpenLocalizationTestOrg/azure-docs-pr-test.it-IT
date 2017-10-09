---
title: tipi di contenuto aaaHandle - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="f7f4c-103">Gestire i tipi di contenuto di app per la logica</span><span class="sxs-lookup"><span data-stu-id="f7f4c-103">Handle content types in logic apps</span></span>

<span data-ttu-id="f7f4c-104">Molti tipi diversi di contenuto possono attraversare un'app per la logica, tra cui JSON, XML, file flat e dati binari.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="f7f4c-105">Mentre la logica App motore hello supporta tutti i tipi di contenuto, alcune in modo nativo vengono riconosciuti da hello logica App motore.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="f7f4c-106">Altri potrebbero richiedere cast o conversioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="f7f4c-107">In questo articolo viene descritto come motore hello gestisce diversi tipi di contenuto e come toocorrectly gestire questi tipi quando necessario.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="f7f4c-108">Intestazione Content-Type</span><span class="sxs-lookup"><span data-stu-id="f7f4c-108">Content-Type Header</span></span>

<span data-ttu-id="f7f4c-109">toostart in pratica, si esaminerà hello due `Content-Types` che non richiedono una conversione o cast che è possibile utilizzare in un'app di logica: `application/json` e `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="f7f4c-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="f7f4c-110">Application/JSON</span></span>

<span data-ttu-id="f7f4c-111">motore del flusso di lavoro di Hello si basa su hello `Content-Type` intestazione HTTP chiama la corretta gestione toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="f7f4c-112">Qualsiasi richiesta con tipo di contenuto hello `application/json` viene archiviato e gestito come un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="f7f4c-113">Per impostazione predefinita, il contenuto JSON può anche essere analizzato senza che sia necessario alcun cast.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="f7f4c-114">Ad esempio, è stato possibile analizzare una richiesta con l'intestazione del tipo di contenuto hello `application/json ` in un flusso di lavoro utilizzando un'espressione come `@body('myAction')['foo'][0]` valore hello tooget `bar` in questo caso:</span><span class="sxs-lookup"><span data-stu-id="f7f4c-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="f7f4c-115">Non è necessario alcun cast aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-115">No additional casting is needed.</span></span> <span data-ttu-id="f7f4c-116">Se si lavora con i dati JSON, ma non contiene un'intestazione specificata, è possibile manualmente eseguirne il cast tooJSON utilizzando hello `@json()` funzione, ad esempio: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="f7f4c-117">Schema e generatore di schemi</span><span class="sxs-lookup"><span data-stu-id="f7f4c-117">Schema and schema generator</span></span>

<span data-ttu-id="f7f4c-118">Hello trigger richiesta consente di tooenter uno schema JSON per il payload di hello tooreceive previsto.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="f7f4c-119">Questo schema consente di progettazione hello generare i token, pertanto è possibile utilizzare hello contenuto della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="f7f4c-120">Se non si dispone di uno schema pronto, selezionare **schema toogenerate payload di esempio utilizzare**, pertanto è possibile generare uno schema JSON da un payload di esempio.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="f7f4c-122">Azione di "analisi JSON"</span><span class="sxs-lookup"><span data-stu-id="f7f4c-122">'Parse JSON' action</span></span>

<span data-ttu-id="f7f4c-123">Hello `Parse JSON` azione consente di analizzare il contenuto JSON in token descrittivo per l'utilizzo di logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="f7f4c-124">Trigger di richiesta toohello simile, questa azione consente di immettere o generare uno schema JSON per contenuto desiderato tooparse hello.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="f7f4c-125">Questo strumento rende molto più semplice l'uso di dati da Bus di servizio, Cosmos DB e così via.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Analizzare JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="f7f4c-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="f7f4c-127">Text/plain</span></span>

<span data-ttu-id="f7f4c-128">Simile troppo`application/json`, i messaggi HTTP ricevuti con hello `Content-Type` intestazione `text/plain` vengono archiviati in formato non elaborato.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="f7f4c-129">Inoltre, se questi messaggi sono inclusi in azioni successive senza eseguire il cast, queste richieste passano con l'intestazione `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="f7f4c-130">Ad esempio, quando si usa un file flat, è possibile che venga visualizzato questo contenuto HTTP come `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="f7f4c-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="f7f4c-131">Se nell'azione successiva hello, si invia richiesta hello come corpo hello di un'altra richiesta (`@body('flatfile')`), richiesta hello avrebbe un `text/plain` intestazione Content-Type.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="f7f4c-132">Se si lavora con i dati che sono testo normale, ma non hanno un'intestazione specificata, è possibile impostare manualmente tootext dati hello utilizzando hello `@string()` funzione, ad esempio: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="f7f4c-133">Application/xml, Application/octet-stream e funzioni del convertitore</span><span class="sxs-lookup"><span data-stu-id="f7f4c-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="f7f4c-134">Hello logica App motore mantiene sempre hello `Content-Type` che è stato ricevuto nel hello HTTP richiesta o risposta.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="f7f4c-135">Pertanto, se il motore di hello riceve il contenuto con hello `Content-Type` di `application/octet-stream`, e si includono che è contenuto in un'azione successiva senza eseguire il cast, la richiesta in uscita hello è `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="f7f4c-136">In questo modo, il motore di hello in grado di garantire dati non vada perduti durante lo spostamento tramite flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="f7f4c-137">Tuttavia, lo stato di azione hello (input e output) verrà archiviato in un oggetto JSON come hello sposta lo stato tramite flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="f7f4c-138">Pertanto toopreserve alcuni tipi di dati, il motore di hello converte hello stringa con codifica base64 binaria tooa contenuto con i metadati appropriati che mantiene sia `$content` e `$content-type`, che vengono automaticamente convertiti.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="f7f4c-139">`@json()`-esegue il cast di dati troppo`application/json`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="f7f4c-140">`@xml()`-esegue il cast di dati troppo`application/xml`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="f7f4c-141">`@binary()`-esegue il cast di dati troppo`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="f7f4c-142">`@string()`-esegue il cast di dati troppo`text/plain`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="f7f4c-143">`@base64()`-Converte una stringa base64 tooa contenuto</span><span class="sxs-lookup"><span data-stu-id="f7f4c-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="f7f4c-144">`@base64toString()`-Converte una stringa con codificata base64 troppo`text/plain`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="f7f4c-145">`@base64toBinary()`-Converte una stringa con codificata base64 troppo`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="f7f4c-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="f7f4c-146">`@encodeDataUri()` : codifica una stringa come matrice di byte dataUri</span><span class="sxs-lookup"><span data-stu-id="f7f4c-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="f7f4c-147">`@decodeDataUri()` : decodifica un dataUri in una matrice di byte</span><span class="sxs-lookup"><span data-stu-id="f7f4c-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="f7f4c-148">Ad esempio, se si riceve una richiesta HTTP con `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="f7f4c-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="f7f4c-149">Si potrebbe eseguire il cast e usarlo in un secondo tempo con un elemento simile a `@xml(triggerBody())` o all'interno di una funzione come `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="f7f4c-150">Altri tipi di contenuto</span><span class="sxs-lookup"><span data-stu-id="f7f4c-150">Other content types</span></span>

<span data-ttu-id="f7f4c-151">Altri tipi di contenuto sono supportati e funziona con le app di logica, ma potrebbe essere necessario recuperare manualmente il corpo del messaggio hello dalla decodifica di hello `$content`.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="f7f4c-152">Si supponga ad esempio si attiva un `application/x-www-url-formencoded` richiesta where `$content` payload hello codificata come un toopreserve stringa base64 tutti i dati:</span><span class="sxs-lookup"><span data-stu-id="f7f4c-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="f7f4c-153">Poiché non è richiesta hello in testo normale o JSON, richiesta hello viene archiviato in azione hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f7f4c-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Attualmente, non è una funzione nativa per i dati del form, pertanto è possibile utilizzare questi dati in un flusso di lavoro manualmente l'accesso a dati hello con una funzione come `@string(body('formdataAction'))`. Se si desidera hello richiesta in uscita tooalso hanno hello `application/x-www-url-formencoded` intestazione di tipo di contenuto, è possibile aggiungere il corpo di hello richiesta toohello azione senza casting come `@body('formdataAction')`. Tuttavia, questo metodo funziona solo se il corpo di hello hello solo parametro hello `body` input. <span data-ttu-id="f7f4c-157">Se si tenta di toouse `@body('formdataAction')` in un `application/json` richiesta, verrà generato un errore di runtime perché il corpo codificato hello viene inviato.</span><span class="sxs-lookup"><span data-stu-id="f7f4c-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

