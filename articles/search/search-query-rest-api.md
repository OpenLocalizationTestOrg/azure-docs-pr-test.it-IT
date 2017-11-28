---
title: aaa "Query di un indice (API REST - ricerca di Azure) | Documenti di Microsoft"
description: Compilare una query di ricerca in ricerca di Azure e usare i parametri toofilter e ordinamento ricerca risultati della ricerca.
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="a8174-103">Query sull'indice utilizzando hello API REST di ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a8174-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="a8174-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a8174-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="a8174-105">Portale</span><span class="sxs-lookup"><span data-stu-id="a8174-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="a8174-106">.NET</span><span class="sxs-lookup"><span data-stu-id="a8174-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="a8174-107">REST</span><span class="sxs-lookup"><span data-stu-id="a8174-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="a8174-108">Questo articolo viene illustrato come un indice utilizzando tooquery hello [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="a8174-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="a8174-109">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md) e [averlo popolato con dati](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="a8174-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="a8174-110">Per informazioni generali, vedere [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="a8174-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="a8174-111">Identificare la chiave API di query del servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a8174-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="a8174-112">Un componente chiave di ogni operazione di ricerca su hello API REST di ricerca di Azure è hello *chiave api* che è stato generato per il servizio di hello è effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a8174-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="a8174-113">Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.</span><span class="sxs-lookup"><span data-stu-id="a8174-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="a8174-114">toofind le chiavi del servizio api, è possibile accedere in toohello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a8174-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="a8174-115">Pannello del servizio di ricerca di Azure andare tooyour</span><span class="sxs-lookup"><span data-stu-id="a8174-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="a8174-116">Fare clic sull'icona "Chiavi" hello</span><span class="sxs-lookup"><span data-stu-id="a8174-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="a8174-117">Il servizio ha *chiavi amministratore* e *chiavi di query*.</span><span class="sxs-lookup"><span data-stu-id="a8174-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="a8174-118">Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici.</span><span class="sxs-lookup"><span data-stu-id="a8174-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="a8174-119">Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.</span><span class="sxs-lookup"><span data-stu-id="a8174-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="a8174-120">Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a8174-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="a8174-121">Ai fini di hello di query nell'indice, è possibile utilizzare una delle chiavi di query.</span><span class="sxs-lookup"><span data-stu-id="a8174-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="a8174-122">Le chiavi amministratore utilizzabile anche per le query, ma è necessario usare una chiave di query nel codice dell'applicazione, come segue meglio hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="a8174-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="a8174-123">Formulare la query</span><span class="sxs-lookup"><span data-stu-id="a8174-123">Formulate your query</span></span>
<span data-ttu-id="a8174-124">Esistono due modi troppo[l'indice utilizzando hello API REST di ricerca](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="a8174-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="a8174-125">È una richiesta HTTP POST tooissue in cui i parametri di query sono definiti in un oggetto JSON nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a8174-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="a8174-126">Hello viceversa è tooissue una richiesta HTTP GET in cui i parametri di query vengono definiti all'interno di hello URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a8174-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="a8174-127">POST contiene più [assoluta limiti](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) sulle dimensioni hello di parametri di query da GET.</span><span class="sxs-lookup"><span data-stu-id="a8174-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="a8174-128">Per questo motivo, è consigliabile usare POST, a meno di non avere circostanze particolari in cui l'uso di GET potrebbe essere più conveniente.</span><span class="sxs-lookup"><span data-stu-id="a8174-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="a8174-129">Per POST e GET, è necessario tooprovide il *nome servizio*, *nome indice*, hello appropriato e *versione API* (versione API corrente hello `2016-09-01` in fase di hello della pubblicazione di questo documento) in hello URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a8174-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="a8174-130">Per ottenere, hello *stringa di query* in hello fine dell'URL hello è possibile fornire parametri di query hello.</span><span class="sxs-lookup"><span data-stu-id="a8174-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="a8174-131">Per il formato di URL hello, vedere di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8174-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="a8174-132">Hello formato per POST è hello stesso, ma con solo api-version nei parametri di stringa di query hello.</span><span class="sxs-lookup"><span data-stu-id="a8174-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="a8174-133">Query di esempio</span><span class="sxs-lookup"><span data-stu-id="a8174-133">Example Queries</span></span>
<span data-ttu-id="a8174-134">Ecco alcuni esempi di query su un indice denominato "hotels".</span><span class="sxs-lookup"><span data-stu-id="a8174-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="a8174-135">Queste query vengono visualizzate in formato GET e POST.</span><span class="sxs-lookup"><span data-stu-id="a8174-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="a8174-136">Eseguire una ricerca hello intero indice per il termine hello "budget" e restituire solo hello `hotelName` campo:</span><span class="sxs-lookup"><span data-stu-id="a8174-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="a8174-137">Applicare un filtro toohello indice toofind gli hotel più economica rispetto alla 150 dollari notte e restituire hello `hotelId` e `description`:</span><span class="sxs-lookup"><span data-stu-id="a8174-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="a8174-138">Cerca nell'intero indice hello, ordine per un campo specifico (`lastRenovationDate`) in ordine decrescente, eseguire i primi due risultati di hello e Mostra solo `hotelName` e `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="a8174-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="a8174-139">Inviare la richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="a8174-139">Submit your HTTP request</span></span>
<span data-ttu-id="a8174-140">Dopo aver formulato la query come parte dell'URL della richiesta HTTP (per GET) o del corpo (per POST), è possibile definire le intestazioni delle richieste e inviare la query.</span><span class="sxs-lookup"><span data-stu-id="a8174-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="a8174-141">Richiesta e intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="a8174-141">Request and Request Headers</span></span>
<span data-ttu-id="a8174-142">È necessario definire due intestazioni della richiesta per GET o tre per POST:</span><span class="sxs-lookup"><span data-stu-id="a8174-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="a8174-143">Hello `api-key` intestazione deve essere impostata come chiave di query toohello trovato nel passaggio si precedente.</span><span class="sxs-lookup"><span data-stu-id="a8174-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="a8174-144">È inoltre possibile utilizzare una chiave amministratore come hello `api-key` intestazione, ma è consigliabile utilizzare una chiave di query come esclusivamente garantisce l'accesso in sola lettura tooindexes e documenti.</span><span class="sxs-lookup"><span data-stu-id="a8174-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="a8174-145">Hello `Accept` intestazione deve essere impostata troppo`application/json`.</span><span class="sxs-lookup"><span data-stu-id="a8174-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="a8174-146">Per i POST, hello `Content-Type` intestazione deve essere impostata troppo`application/json`.</span><span class="sxs-lookup"><span data-stu-id="a8174-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="a8174-147">Per un HTTP GET richiesta toosearch hello "Hotel" indice utilizzando l'API REST ricerca di Azure, utilizzando una query semplice che cerca il termine hello "motel" hello, vedere di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8174-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="a8174-148">Ecco hello stessa query di esempio, questa volta utilizzando HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="a8174-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="a8174-149">Una richiesta di query ha esito positivo comporterà un codice di stato `200 OK` e vengono restituiti i risultati della ricerca hello come JSON nel corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="a8174-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="a8174-150">Ecco i risultati dei quali hello per hello di sopra di query è simile, presupponendo che l'indice di hotel"hello" viene popolato con i dati di esempio hello in [importazione dei dati in ricerca di Azure tramite API REST di hello](search-import-data-rest-api.md) (si noti che hello JSON è stato formattato per maggiore chiarezza).</span><span class="sxs-lookup"><span data-stu-id="a8174-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="a8174-151">toolearn, visitare sezione "Risposta" hello [ricerca documenti](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="a8174-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="a8174-152">Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="a8174-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
