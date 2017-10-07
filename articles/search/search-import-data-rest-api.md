---
title: aaa "caricamento di dati (API REST - ricerca di Azure) | Documenti di Microsoft"
description: Informazioni su come indice di tooan tooupload dati in ricerca di Azure tramite hello API REST.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="e97b1-103">Caricamento dati tooAzure ricerca tramite hello API REST</span><span class="sxs-lookup"><span data-stu-id="e97b1-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="e97b1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e97b1-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="e97b1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e97b1-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="e97b1-106">REST</span><span class="sxs-lookup"><span data-stu-id="e97b1-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="e97b1-107">In questo articolo viene illustrato come hello toouse [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport dati in un indice di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="e97b1-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="e97b1-108">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="e97b1-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="e97b1-109">Nei documenti di ordine toopush nell'indice utilizzando l'API REST di hello, vengono emessi endpoint dell'URL del tooyour indice richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e97b1-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="e97b1-110">corpo Hello di hello richiesta HTTP corpo è un oggetto JSON che contengono i documenti hello toobe aggiunte, modificate o eliminate.</span><span class="sxs-lookup"><span data-stu-id="e97b1-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="e97b1-111">Identificare la chiave API amministratore del servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="e97b1-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="e97b1-112">Quando si inviano richieste HTTP per il servizio utilizzando l'API REST di hello *ogni* richiesta API deve includere hello chiave api che è stato generato per hello è effettuato il provisioning del servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e97b1-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="e97b1-113">Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.</span><span class="sxs-lookup"><span data-stu-id="e97b1-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="e97b1-114">toofind le chiavi del servizio api, è possibile accedere in toohello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e97b1-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="e97b1-115">Pannello del servizio di ricerca di Azure andare tooyour</span><span class="sxs-lookup"><span data-stu-id="e97b1-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="e97b1-116">Fare clic su hello icona "Chiavi"</span><span class="sxs-lookup"><span data-stu-id="e97b1-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="e97b1-117">Il servizio avrà *chiavi amministratore* e *chiavi di query*.</span><span class="sxs-lookup"><span data-stu-id="e97b1-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="e97b1-118">Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici.</span><span class="sxs-lookup"><span data-stu-id="e97b1-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="e97b1-119">Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.</span><span class="sxs-lookup"><span data-stu-id="e97b1-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="e97b1-120">Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e97b1-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="e97b1-121">Ai fini di hello di importazione di dati in un indice, è possibile utilizzare la chiave amministratore primaria o secondaria.</span><span class="sxs-lookup"><span data-stu-id="e97b1-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="e97b1-122">Decidere quali indicizzazione toouse azione</span><span class="sxs-lookup"><span data-stu-id="e97b1-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="e97b1-123">Quando si utilizza l'API REST di hello, vengono emessi richieste HTTP POST con l'URL dell'endpoint JSON richiesta corpi tooyour ricerca di Azure dell'indice.</span><span class="sxs-lookup"><span data-stu-id="e97b1-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="e97b1-124">oggetto JSON Hello nel corpo della richiesta HTTP contiene una matrice JSON denominato "value", che contiene oggetti JSON che rappresenta i documenti di cui si desidera tooadd tooyour indice, aggiornare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="e97b1-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="e97b1-125">Ogni oggetto JSON nella matrice di "value" hello rappresenta un toobe documento indicizzato.</span><span class="sxs-lookup"><span data-stu-id="e97b1-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="e97b1-126">Ognuno di questi oggetti contiene la chiave del documento hello e si specifica l'azione di indicizzazione hello desiderato (caricamento, unione, eliminazione e così via).</span><span class="sxs-lookup"><span data-stu-id="e97b1-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="e97b1-127">A seconda di quale dei hello si sceglie di azioni riportate di seguito, solo alcuni campi devono essere inclusi per ogni documento:</span><span class="sxs-lookup"><span data-stu-id="e97b1-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="e97b1-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e97b1-128">Description</span></span> | <span data-ttu-id="e97b1-129">Campi necessari per ogni documento</span><span class="sxs-lookup"><span data-stu-id="e97b1-129">Necessary fields for each document</span></span> | <span data-ttu-id="e97b1-130">Note</span><span class="sxs-lookup"><span data-stu-id="e97b1-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="e97b1-131">Un `upload` tooan simile "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello è intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e97b1-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="e97b1-132">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="e97b1-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="e97b1-133">Durante l'aggiornamento o la sostituzione di un documento esistente, qualsiasi campo che non è specificato nella richiesta di hello avrà il campo impostato troppo`null`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="e97b1-134">Questo errore si verifica anche quando il campo hello è stato impostato precedentemente valore non null tooa.</span><span class="sxs-lookup"><span data-stu-id="e97b1-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="e97b1-135">Gli aggiornamenti del documento esistente con hello specificati campi.</span><span class="sxs-lookup"><span data-stu-id="e97b1-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="e97b1-136">Se non esiste alcun documento hello nell'indice hello, merge hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e97b1-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="e97b1-137">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="e97b1-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="e97b1-138">Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello.</span><span class="sxs-lookup"><span data-stu-id="e97b1-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="e97b1-139">Sono inclusi anche i campi di tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="e97b1-140">Ad esempio, se hello documento contiene un campo `tags` con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per `tags`, il valore finale di hello hello `tags` campo sarà `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="e97b1-141">e non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="e97b1-142">Questa azione è analoga `merge` se esiste un documento con hello data già chiave nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="e97b1-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="e97b1-143">Se il documento hello non esiste, si comporta come `upload` con un nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="e97b1-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="e97b1-144">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="e97b1-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="e97b1-145">Rimozione di documento specificato hello dall'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="e97b1-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="e97b1-146">solo campo chiave</span><span class="sxs-lookup"><span data-stu-id="e97b1-146">key only</span></span> |<span data-ttu-id="e97b1-147">Tutti i campi specificare diverso hello chiave campo verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="e97b1-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="e97b1-148">Se si desidera tooremove un singolo campo da un documento, utilizzare `merge` invece e impostare semplicemente il campo hello in modo esplicito toonull.</span><span class="sxs-lookup"><span data-stu-id="e97b1-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="e97b1-149">Creare la richiesta HTTP e il corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="e97b1-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="e97b1-150">Ora che i valori dei campi necessari hello raccolti per le operazioni di indice, la richiesta HTTP effettiva di tooconstruct pronto hello e tooimport corpo della richiesta JSON i dati.</span><span class="sxs-lookup"><span data-stu-id="e97b1-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="e97b1-151">Richiesta e intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="e97b1-151">Request and Request Headers</span></span>
<span data-ttu-id="e97b1-152">Nell'URL hello, è necessario tooprovide il nome del servizio, il nome di indice ("Hotel" in questo caso), nonché la versione API appropriata hello (versione API corrente hello `2016-09-01` in fase di hello della pubblicazione di questo documento).</span><span class="sxs-lookup"><span data-stu-id="e97b1-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="e97b1-153">Sarà necessario hello toodefine `Content-Type` e `api-key` intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="e97b1-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="e97b1-154">Per quest'ultimo hello, usare una delle chiavi di amministratore del servizio.</span><span class="sxs-lookup"><span data-stu-id="e97b1-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="e97b1-155">Request Body</span><span class="sxs-lookup"><span data-stu-id="e97b1-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="e97b1-156">In questo caso, si useranno `upload`, `mergeOrUpload` e `delete` come azioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e97b1-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="e97b1-157">Si supponga che l'indice "hotels" di esempio sia già popolato con alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="e97b1-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="e97b1-158">Si noti come non è toospecify tutti i campi del documento possibili hello quando si utilizza `mergeOrUpload` e come viene specificata solo la chiave di documento hello (`hotelId`) quando si utilizza `delete`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="e97b1-159">Inoltre, si noti che è possibile includere solo i documenti too1000 (o 16 MB) in una singola richiesta di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="e97b1-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="e97b1-160">Informazioni sul codice di risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="e97b1-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="e97b1-161">200</span><span class="sxs-lookup"><span data-stu-id="e97b1-161">200</span></span>
<span data-ttu-id="e97b1-162">Dopo l'invio di una richiesta di indicizzazione riuscita, si riceverà una risposta HTTP con codice di stato `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="e97b1-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="e97b1-163">il corpo JSON di risposta HTTP hello Hello verrà modificato come segue:</span><span class="sxs-lookup"><span data-stu-id="e97b1-163">hello JSON body of hello HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="e97b1-164">207</span><span class="sxs-lookup"><span data-stu-id="e97b1-164">207</span></span>
<span data-ttu-id="e97b1-165">Quando almeno un elemento non è stato indicizzato correttamente, viene restituito il codice di stato `207` .</span><span class="sxs-lookup"><span data-stu-id="e97b1-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="e97b1-166">Hello corpo JSON di risposta HTTP hello conterrà informazioni sui documenti di hello non riuscito.</span><span class="sxs-lookup"><span data-stu-id="e97b1-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="e97b1-167">Spesso questo significa che il hello nella ricerca servizio sta raggiungendo un punto in cui le richieste di indicizzazione avranno inizio tooreturn `503` le risposte.</span><span class="sxs-lookup"><span data-stu-id="e97b1-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="e97b1-168">In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="e97b1-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="e97b1-169">Questa query fornirà sistema hello alcuni toorecover tempo, aumentare le opportunità hello che avrà esito positivo richieste future.</span><span class="sxs-lookup"><span data-stu-id="e97b1-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="e97b1-170">Ripetizione rapida delle richieste prolungherà semplicemente situazione hello.</span><span class="sxs-lookup"><span data-stu-id="e97b1-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="e97b1-171">429</span><span class="sxs-lookup"><span data-stu-id="e97b1-171">429</span></span>
<span data-ttu-id="e97b1-172">Il codice di stato `429` saranno restituite quando è stata superata la quota per il numero di hello di documenti per indice.</span><span class="sxs-lookup"><span data-stu-id="e97b1-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="e97b1-173">503</span><span class="sxs-lookup"><span data-stu-id="e97b1-173">503</span></span>
<span data-ttu-id="e97b1-174">Il codice di stato `503` verrà restituito se nessuno degli elementi di hello in hello richiesta sono state indicizzate correttamente.</span><span class="sxs-lookup"><span data-stu-id="e97b1-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="e97b1-175">Questo errore indica che sistema hello è sovraccarico e non può elaborare la richiesta in questo momento.</span><span class="sxs-lookup"><span data-stu-id="e97b1-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="e97b1-176">In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="e97b1-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="e97b1-177">Questa query fornirà sistema hello alcuni toorecover tempo, aumentare le opportunità hello che avrà esito positivo richieste future.</span><span class="sxs-lookup"><span data-stu-id="e97b1-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="e97b1-178">Ripetizione rapida delle richieste prolungherà semplicemente situazione hello.</span><span class="sxs-lookup"><span data-stu-id="e97b1-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="e97b1-179">Per altre informazioni su azioni sui documenti e risposte di esito positivo/errore, vedere [Aggiungere, aggiornare o eliminare documenti](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="e97b1-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="e97b1-180">Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="e97b1-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e97b1-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e97b1-181">Next steps</span></span>
<span data-ttu-id="e97b1-182">Dopo avere popolato l'indice di ricerca di Azure, sarà pronto toostart emittente toosearch query per i documenti.</span><span class="sxs-lookup"><span data-stu-id="e97b1-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="e97b1-183">Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="e97b1-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
