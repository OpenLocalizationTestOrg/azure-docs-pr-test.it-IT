---
title: 'Caricare dati: API REST e Ricerca di Azure | Microsoft Docs'
description: Informazioni su come caricare dati in un indice di Ricerca di Azure tramite l'API REST.
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
ms.openlocfilehash: f22a33ed86fbfc46dfa732239263a49f34c4afee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="fa256-103">Caricare dati in Ricerca di Azure tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="fa256-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="fa256-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fa256-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="fa256-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fa256-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="fa256-106">REST</span><span class="sxs-lookup"><span data-stu-id="fa256-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="fa256-107">Questo articolo illustra come usare l' [API REST di Ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/) per importare dati in un indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa256-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="fa256-108">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="fa256-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="fa256-109">Per effettuare il push dei documenti nell'indice con l'API REST, inviare una richiesta HTTP POST all'endpoint dell'URL dell'indice.</span><span class="sxs-lookup"><span data-stu-id="fa256-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="fa256-110">Il corpo della richiesta HTTP è un oggetto JSON che contiene i documenti da aggiungere, modificare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="fa256-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="fa256-111">Identificare la chiave API amministratore del servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="fa256-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="fa256-112">Quando si inviano richieste HTTP al servizio tramite l'API REST, *ogni* richiesta API deve includere la chiave API generata per il servizio di ricerca di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="fa256-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="fa256-113">La presenza di una chiave valida stabilisce una relazione di trust, in base alle singole richieste, tra l'applicazione che invia la richiesta e il servizio che la gestisce.</span><span class="sxs-lookup"><span data-stu-id="fa256-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="fa256-114">Per trovare le chiavi API del servizio, è possibile accedere al [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="fa256-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="fa256-115">Passare al pannello del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa256-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="fa256-116">Fare clic sull'icona "Chiavi".</span><span class="sxs-lookup"><span data-stu-id="fa256-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="fa256-117">Il servizio avrà *chiavi amministratore* e *chiavi di query*.</span><span class="sxs-lookup"><span data-stu-id="fa256-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="fa256-118">Le *chiavi amministratore* primarie e secondarie concedono diritti completi a tutte le operazioni, inclusa la possibilità di gestire il servizio, creare ed eliminare indici, indicizzatori e origini dati.</span><span class="sxs-lookup"><span data-stu-id="fa256-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="fa256-119">Sono disponibili due chiavi, quindi è possibile continuare a usare la chiave secondaria se si decide di rigenerare la chiave primaria e viceversa.</span><span class="sxs-lookup"><span data-stu-id="fa256-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="fa256-120">Le *chiavi di query* concedono l'accesso in sola lettura agli indici e ai documenti e vengono in genere distribuite alle applicazioni client che inviano richieste di ricerca.</span><span class="sxs-lookup"><span data-stu-id="fa256-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="fa256-121">Per l'importazione di dati in un indice è possibile usare la chiave amministratore primaria o secondaria.</span><span class="sxs-lookup"><span data-stu-id="fa256-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="fa256-122">Decidere quale azione di indicizzazione usare</span><span class="sxs-lookup"><span data-stu-id="fa256-122">Decide which indexing action to use</span></span>
<span data-ttu-id="fa256-123">Quando si usa l'API REST, si inviano richieste HTTP POST con corpi delle richieste JSON all'URL dell'endpoint dell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa256-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="fa256-124">L'oggetto JSON nel corpo della richiesta HTTP contiene una matrice JSON denominata "value" che include oggetti JSON che rappresentano i documenti da aggiungere all'indice, aggiornare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="fa256-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="fa256-125">Ogni oggetto JSON nella matrice "value" rappresenta un documento da indicizzare.</span><span class="sxs-lookup"><span data-stu-id="fa256-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="fa256-126">Ognuno di questi oggetti contiene la chiave del documento e specifica l'azione di indicizzazione desiderata, ovvero caricamento, unione, eliminazione e così via.</span><span class="sxs-lookup"><span data-stu-id="fa256-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="fa256-127">A seconda delle azioni scelte tra le seguenti, per ogni documento devono essere inclusi solo campi specifici:</span><span class="sxs-lookup"><span data-stu-id="fa256-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="fa256-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa256-128">Description</span></span> | <span data-ttu-id="fa256-129">Campi necessari per ogni documento</span><span class="sxs-lookup"><span data-stu-id="fa256-129">Necessary fields for each document</span></span> | <span data-ttu-id="fa256-130">Note</span><span class="sxs-lookup"><span data-stu-id="fa256-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="fa256-131">L'azione `upload` è simile a "upsert", in cui il documento viene inserito se è nuovo e aggiornato o sostituito se esiste già.</span><span class="sxs-lookup"><span data-stu-id="fa256-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="fa256-132">chiave, oltre a tutti gli altri campi da definire</span><span class="sxs-lookup"><span data-stu-id="fa256-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="fa256-133">Quando si aggiorna o si sostituisce un documento esistente, qualsiasi campo non specificato nella richiesta avrà il campo impostato su `null`.</span><span class="sxs-lookup"><span data-stu-id="fa256-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="fa256-134">Ciò si verifica anche quando il campo è stato precedentemente impostato su un valore diverso da null.</span><span class="sxs-lookup"><span data-stu-id="fa256-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="fa256-135">Aggiorna un documento esistente con i campi specificati.</span><span class="sxs-lookup"><span data-stu-id="fa256-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="fa256-136">Se il documento non esiste nell'indice, l'unione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="fa256-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="fa256-137">chiave, oltre a tutti gli altri campi da definire</span><span class="sxs-lookup"><span data-stu-id="fa256-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="fa256-138">I campi specificati in un'azione di unione sostituiscono i campi esistenti nel documento.</span><span class="sxs-lookup"><span data-stu-id="fa256-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="fa256-139">Sono inclusi anche i campi di tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="fa256-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="fa256-140">Ad esempio, se il documento contiene un campo `tags` con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per `tags`, il valore finale del campo `tags` sarà `["economy", "pool"]`</span><span class="sxs-lookup"><span data-stu-id="fa256-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="fa256-141">e non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fa256-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="fa256-142">Questa azione si comporta come `merge` se nell'indice esiste già un documento con la chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="fa256-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="fa256-143">Se il documento non esiste, si comporta come `upload` con un nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="fa256-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="fa256-144">chiave, oltre a tutti gli altri campi da definire</span><span class="sxs-lookup"><span data-stu-id="fa256-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="fa256-145">Rimuove il documento specificato dall'indice.</span><span class="sxs-lookup"><span data-stu-id="fa256-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="fa256-146">solo campo chiave</span><span class="sxs-lookup"><span data-stu-id="fa256-146">key only</span></span> |<span data-ttu-id="fa256-147">Tutti i campi diversi dal campo chiave specificati verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="fa256-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="fa256-148">Se si vuole rimuovere un singolo campo da un documento, usare invece `merge` e impostare il campo su Null in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="fa256-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="fa256-149">Creare la richiesta HTTP e il corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="fa256-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="fa256-150">Ora che sono stati raccolti i valori dei campi necessari per le operazioni sull'indice, si è pronti per creare la richiesta HTTP effettiva e il corpo della richiesta JSON per importare i dati.</span><span class="sxs-lookup"><span data-stu-id="fa256-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="fa256-151">Richiesta e intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="fa256-151">Request and Request Headers</span></span>
<span data-ttu-id="fa256-152">Nell'URL è necessario fornire il nome del servizio, il nome dell'indice, in questo caso "hotels", nonché la versione corretta dell'API. Al momento della pubblicazione di questo documento la versione dell'API corrente è `2016-09-01`.</span><span class="sxs-lookup"><span data-stu-id="fa256-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2016-09-01` at the time of publishing this document).</span></span> <span data-ttu-id="fa256-153">È necessario definire le intestazioni della richiesta `Content-Type` e `api-key`.</span><span class="sxs-lookup"><span data-stu-id="fa256-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="fa256-154">Nel secondo caso, usare una delle chiavi amministratore del servizio.</span><span class="sxs-lookup"><span data-stu-id="fa256-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="fa256-155">Request Body</span><span class="sxs-lookup"><span data-stu-id="fa256-155">Request Body</span></span>
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
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="fa256-156">In questo caso, si useranno `upload`, `mergeOrUpload` e `delete` come azioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="fa256-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="fa256-157">Si supponga che l'indice "hotels" di esempio sia già popolato con alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="fa256-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="fa256-158">Si noti che non è stato necessario specificare tutti i possibili campi dei documenti quando si usa `mergeOrUpload` e come viene specificata solo la chiave del documento (`hotelId`) quando si usa `delete`.</span><span class="sxs-lookup"><span data-stu-id="fa256-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="fa256-159">Si noti anche che è possibile includere solo fino a 1000 documenti, o 16 MB, in una singola richiesta di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="fa256-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="fa256-160">Informazioni sul codice di risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="fa256-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="fa256-161">200</span><span class="sxs-lookup"><span data-stu-id="fa256-161">200</span></span>
<span data-ttu-id="fa256-162">Dopo l'invio di una richiesta di indicizzazione riuscita, si riceverà una risposta HTTP con codice di stato `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="fa256-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="fa256-163">Il corpo JSON della risposta HTTP sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="fa256-163">The JSON body of the HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="fa256-164">207</span><span class="sxs-lookup"><span data-stu-id="fa256-164">207</span></span>
<span data-ttu-id="fa256-165">Quando almeno un elemento non è stato indicizzato correttamente, viene restituito il codice di stato `207` .</span><span class="sxs-lookup"><span data-stu-id="fa256-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="fa256-166">Il corpo JSON della risposta HTTP contiene informazioni sui documenti la cui richiesta di indicizzazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fa256-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="fa256-167">Spesso questo significa che il carico sul servizio di ricerca sta per raggiungere un punto in cui le richieste di indicizzazione inizieranno a restituire risposte `503`.</span><span class="sxs-lookup"><span data-stu-id="fa256-167">This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses.</span></span> <span data-ttu-id="fa256-168">In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="fa256-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="fa256-169">Il sistema avrà così tempo per recuperare, aumentando le probabilità che le future richieste siano soddisfatte.</span><span class="sxs-lookup"><span data-stu-id="fa256-169">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="fa256-170">La ripetizione rapida delle richieste prolungherà semplicemente il tempo necessario per risolvere la situazione.</span><span class="sxs-lookup"><span data-stu-id="fa256-170">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="fa256-171">429</span><span class="sxs-lookup"><span data-stu-id="fa256-171">429</span></span>
<span data-ttu-id="fa256-172">Il codice di stato `429` viene restituito quando è stata superata la quota del numero di documenti per indice.</span><span class="sxs-lookup"><span data-stu-id="fa256-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="fa256-173">503</span><span class="sxs-lookup"><span data-stu-id="fa256-173">503</span></span>
<span data-ttu-id="fa256-174">Il codice di stato `503` viene restituito se nessuno degli elementi nella richiesta è stato indicizzato.</span><span class="sxs-lookup"><span data-stu-id="fa256-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="fa256-175">Questo errore indica che il sistema è sovraccarico e non può elaborare la richiesta in questo momento.</span><span class="sxs-lookup"><span data-stu-id="fa256-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="fa256-176">In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="fa256-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="fa256-177">Il sistema avrà così tempo per recuperare, aumentando le probabilità che le future richieste siano soddisfatte.</span><span class="sxs-lookup"><span data-stu-id="fa256-177">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="fa256-178">La ripetizione rapida delle richieste prolungherà semplicemente il tempo necessario per risolvere la situazione.</span><span class="sxs-lookup"><span data-stu-id="fa256-178">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

<span data-ttu-id="fa256-179">Per altre informazioni su azioni sui documenti e risposte di esito positivo/errore, vedere [Aggiungere, aggiornare o eliminare documenti](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="fa256-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="fa256-180">Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="fa256-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa256-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa256-181">Next steps</span></span>
<span data-ttu-id="fa256-182">Dopo il popolamento dell'indice di Ricerca di Azure, si potrà iniziare a eseguire una query per la ricerca di documenti.</span><span class="sxs-lookup"><span data-stu-id="fa256-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="fa256-183">Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="fa256-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
