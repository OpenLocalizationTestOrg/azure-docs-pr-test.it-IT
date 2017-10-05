---
title: API REST di Ricerca di Azure versione 2015-02-28-Preview | Documentazione Microsoft
description: "L'API REST di Ricerca di Azure versione 2015-02-28-Preview include funzionalità sperimentali come gli analizzatori del linguaggio naturale e le ricerche moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="eb67a-103">API REST del servizio Ricerca di Azure: versione 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="eb67a-104">Questo articolo è la documentazione di riferimento per `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-105">Questa versione di anteprima estende l'attuale versione disponibile per il pubblico, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), con le seguenti funzionalità sperimentali:</span><span class="sxs-lookup"><span data-stu-id="eb67a-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="eb67a-106">`moreLikeThis` parametro query nell'API di [ricerca documenti](#SearchDocs) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="eb67a-107">Trova altri documenti rilevanti per un altro documento specifico.</span><span class="sxs-lookup"><span data-stu-id="eb67a-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="eb67a-108">Alcune parti aggiuntive dell'API REST `2015-02-28-Preview` sono documentate separatamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="eb67a-109">incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb67a-109">These include:</span></span>

* [<span data-ttu-id="eb67a-110">Profili di punteggio</span><span class="sxs-lookup"><span data-stu-id="eb67a-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="eb67a-111">Indicizzatori</span><span class="sxs-lookup"><span data-stu-id="eb67a-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="eb67a-112">Ricerca di Azure è disponibile in più versioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="eb67a-113">Per informazioni dettagliate, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="eb67a-114">API in questo documento</span><span class="sxs-lookup"><span data-stu-id="eb67a-114">APIs in this document</span></span>
<span data-ttu-id="eb67a-115">L'API del servizio Ricerca di Azure supporta due sintassi di URL per le operazioni dell'API, ovvero semplice e OData. Per informazioni dettagliate, vedere [Supporto per OData (Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="eb67a-116">L'elenco seguente mostra la sintassi semplice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="eb67a-117">Creare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-118">Aggiornare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-119">Ottenere un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-120">Elencare gli indici</span><span class="sxs-lookup"><span data-stu-id="eb67a-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-121">Ottenere le statistiche di un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-122">Analizzatore di test</span><span class="sxs-lookup"><span data-stu-id="eb67a-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-123">Eliminare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-124">Aggiungere, aggiornare o eliminare documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-125">Eseguire ricerche nei documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-126">Cercare un documento</span><span class="sxs-lookup"><span data-stu-id="eb67a-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="eb67a-127">Contare i documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="eb67a-128">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="eb67a-129">Operazioni sugli indici</span><span class="sxs-lookup"><span data-stu-id="eb67a-129">Index Operations</span></span>
<span data-ttu-id="eb67a-130">È possibile creare e gestire gli indici in Ricerca di Azure tramite semplici richieste HTTP (POST, GET, PUT, DELETE) su una risorsa indice specifica.</span><span class="sxs-lookup"><span data-stu-id="eb67a-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="eb67a-131">Per creare un indice, eseguire innanzitutto la richiesta POST di un documento JSON che descrive lo schema dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="eb67a-132">Lo schema definisce i campi dell'indice, i relativi tipi di dati e la modalità d'uso, ad esempio ricerche full-text, filtri, ordinamento o uso di facet.</span><span class="sxs-lookup"><span data-stu-id="eb67a-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="eb67a-133">Definisce anche i profili di punteggio, i componenti per il suggerimento e altri attributi per configurare il comportamento dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="eb67a-134">L'esempio seguente illustra uno schema usato per la ricerca di informazioni sugli hotel, con il campo relativo alla descrizione definito in due lingue.</span><span class="sxs-lookup"><span data-stu-id="eb67a-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="eb67a-135">Si noti come gli attributi controllano la modalità d'uso del campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="eb67a-136">Ad esempio, `hotelId` viene usato come chiave del documento (`"key": true`) ed è escluso dalle ricerche full-text (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="eb67a-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="eb67a-137">Dopo la creazione dell'indice, si caricano i documenti per popolarlo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="eb67a-138">Per questo passaggio successivo, vedere [Aggiungere, aggiornare o eliminare documenti](#AddOrUpdateDocuments) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="eb67a-139">Per un video introduttivo all'indicizzazione di Ricerca di Azure, vedere l' [episodio di Channel 9 Cloud Cover relativo a Ricerca di Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="eb67a-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="eb67a-140">Creare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-140">Create Index</span></span>
<span data-ttu-id="eb67a-141">Un indice è il mezzo principale per organizzare documenti ed eseguirvi ricerche con Ricerca di Azure, così come una tabella organizza i record in un database.</span><span class="sxs-lookup"><span data-stu-id="eb67a-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="eb67a-142">Ogni indice include una raccolta di documenti che sono tutti conformi al relativo schema (nomi di campi, tipi di dati e proprietà), ma gli indici specificano anche costrutti aggiuntivi (componenti per il suggerimento, profili di punteggio e opzioni CORS) che definiscono altri comportamenti di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="eb67a-143">È possibile creare un nuovo indice in Ricerca di Azure mediante una richiesta HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="eb67a-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="eb67a-144">Il corpo della richiesta è uno schema JSON che specifica le informazioni di indice e configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="eb67a-145">In alternativa, è possibile usare PUT e specificare il nome dell'indice nell'URI.</span><span class="sxs-lookup"><span data-stu-id="eb67a-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="eb67a-146">Se l'indice non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="eb67a-147">La creazione di un indice determina la struttura dei documenti archiviati e usati nelle operazioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="eb67a-148">Il popolamento dell'indice è un'operazione separata.</span><span class="sxs-lookup"><span data-stu-id="eb67a-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="eb67a-149">Per questo passaggio, è possibile usare un [indicizzatore](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponibile per le origini dati supportate) o un'[operazione di aggiunta, aggiornamento o eliminazione di documenti](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="eb67a-150">L'indice invertito viene generato quando i documenti vengono pubblicati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="eb67a-151">**Nota**: il numero massimo di indici consentiti varia in base al livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="eb67a-152">Nel servizio gratuito sono consentiti fino a 3 indici.</span><span class="sxs-lookup"><span data-stu-id="eb67a-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="eb67a-153">Nel servizio standard sono consentiti 50 indici per servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="eb67a-154">Per dettagli, vedere [Limitazioni e vincoli](http://msdn.microsoft.com/library/azure/dn798934.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="eb67a-155">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-155">**Request**</span></span>

<span data-ttu-id="eb67a-156">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="eb67a-157">La richiesta di **creazione di un indice** può essere creata mediante il metodo POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="eb67a-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="eb67a-158">Se si usa il metodo POST, è necessario specificare nel corpo della richiesta il nome di un indice e la definizione del relativo schema.</span><span class="sxs-lookup"><span data-stu-id="eb67a-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="eb67a-159">Nel caso di PUT, il nome dell'indice fa parte dell'URL.</span><span class="sxs-lookup"><span data-stu-id="eb67a-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="eb67a-160">Se l'indice non esiste, viene creato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="eb67a-161">Se esiste già, viene aggiornato in base alla nuova definizione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="eb67a-162">Il nome dell'indice deve essere scritto in caratteri minuscoli, deve iniziare con una lettera o un numero, non deve contenere barre o punti e deve avere una lunghezza inferiore ai 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="eb67a-163">Dopo l'iniziale costituita da una lettera o un numero, il resto del nome può contenere lettere, numeri e trattini, purché i trattini non siano consecutivi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="eb67a-164">L'elemento `api-version` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-164">The `api-version` is required.</span></span> <span data-ttu-id="eb67a-165">Per un elenco delle versioni disponibili, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="eb67a-166">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-166">**Request Headers**</span></span>

<span data-ttu-id="eb67a-167">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-168">`Content-Type`: richiesto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-168">`Content-Type`: Required.</span></span> <span data-ttu-id="eb67a-169">Impostare il valore su `application/json`</span><span class="sxs-lookup"><span data-stu-id="eb67a-169">Set this to `application/json`</span></span>
* <span data-ttu-id="eb67a-170">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-170">`api-key`: Required.</span></span> <span data-ttu-id="eb67a-171">L'elemento `api-key` viene usato per</span><span class="sxs-lookup"><span data-stu-id="eb67a-171">The `api-key` is used to</span></span>
* <span data-ttu-id="eb67a-172">per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-173">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-174">La richiesta di **creazione dell'indice** deve includere un'intestazione `api-key` impostata sulla chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-175">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-176">È possibile ottenere sia il nome del servizio sia `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-177">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-178"><a name="RequestData"></a>
**Sintassi del corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="eb67a-179">Il corpo della richiesta contiene una definizione di schema che include l'elenco dei campi dati all'interno dei documenti che verranno inseriti nell'indice, i tipi di dati, gli attributi e un elenco facoltativo dei profili di punteggio che vengono usati per assegnare un punteggio ai documenti corrispondenti quando si esegue la query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="eb67a-180">Si noti che per una richiesta POST, è necessario specificare il nome dell'indice nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="eb67a-181">Può essere presente un solo campo chiave nell'indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-181">There can only be one key field in the index.</span></span> <span data-ttu-id="eb67a-182">e tale campo deve essere di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="eb67a-182">It has to be a string field.</span></span> <span data-ttu-id="eb67a-183">Il campo rappresenta l'identificatore univoco per ogni documento archiviato all'interno dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="eb67a-184">Le parti principali di un indice includono quanto segue:</span><span class="sxs-lookup"><span data-stu-id="eb67a-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="eb67a-185">`fields` : elementi che verranno inseriti nell'indice, tra cui il nome, il tipo di dati e le proprietà che definiscono le azioni consentite.</span><span class="sxs-lookup"><span data-stu-id="eb67a-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="eb67a-186">`suggesters` : elementi usati per le query con completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="eb67a-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="eb67a-187">`scoringProfiles` :elementi usati per la classificazione personalizzata dei punteggi di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="eb67a-188">Per informazioni dettagliate, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="eb67a-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` usati per definire in che modo i documenti/query sono suddivisi in token indicizzabili/ricercabile.</span><span class="sxs-lookup"><span data-stu-id="eb67a-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="eb67a-190">Per i dettagli, vedere la pagina relativa all' [analisi in Ricerca di Azure](https://aka.ms//azsanalysis) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="eb67a-191">`defaultScoringProfile` : elemento usato per sovrascrivere i comportamenti relativi ai punteggi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="eb67a-192">`corsOptions`: elemento usato per consentire query nell'indice basate su più origini.</span><span class="sxs-lookup"><span data-stu-id="eb67a-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="eb67a-193">La sintassi per la strutturazione del payload della richiesta è la seguente:</span><span class="sxs-lookup"><span data-stu-id="eb67a-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="eb67a-194">Più avanti in questo argomento è riportata una richiesta di esempio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="eb67a-195">**Attributi dell'indice**</span><span class="sxs-lookup"><span data-stu-id="eb67a-195">**Index Attributes**</span></span>

<span data-ttu-id="eb67a-196">Quando si crea un indice, è possibile impostare gli attributi seguenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="eb67a-197">Per informazioni dettagliate sull'assegnazione dei punteggi e sui profili di punteggio, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="eb67a-198">`name` : imposta il nome del campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="eb67a-199">`type` : imposta il tipo di dati per il campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="eb67a-200">`searchable` : contrassegna il campo come disponibile per la ricerca full-text.</span><span class="sxs-lookup"><span data-stu-id="eb67a-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="eb67a-201">Ciò significa che verrà sottoposto ad analisi, ad esempio la suddivisione in parole durante l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="eb67a-202">Se si imposta un campo `searchable` su un valore come "sunny day", questo viene suddiviso internamente nei singoli token "sunny" e "day".</span><span class="sxs-lookup"><span data-stu-id="eb67a-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="eb67a-203">È così possibile eseguire ricerche full-text di questi termini.</span><span class="sxs-lookup"><span data-stu-id="eb67a-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="eb67a-204">I campi di tipo `Edm.String` o `Collection(Edm.String)` sono `searchable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb67a-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="eb67a-205">I campi di altri tipi non possono essere `searchable`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="eb67a-206">**Nota**: i campi `searchable` usano spazio aggiuntivo nell'indice perché Ricerca di Azure archivia una versione supplementare in formato token del valore del campo per le ricerche full-text.</span><span class="sxs-lookup"><span data-stu-id="eb67a-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="eb67a-207">Se si vuole risparmiare spazio nell'indice e non è necessario includere un campo nelle ricerche, impostare `searchable` su `false`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="eb67a-208">`filterable`: consente ai campi di essere usati come riferimento nelle query `$filter`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="eb67a-209">`filterable` è diverso da `searchable` nella modalità di gestione delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="eb67a-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="eb67a-210">I campi di tipo `Edm.String` o `Collection(Edm.String)` che sono `filterable` non sono sottoposti a suddivisione delle parole e quindi i confronti riguardano solo le corrispondenze esatte.</span><span class="sxs-lookup"><span data-stu-id="eb67a-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="eb67a-211">Se ad esempio si imposta un campo `f` su "sunny day", `$filter=f eq 'sunny'` non troverà corrispondenze, mentre `$filter=f eq 'sunny day'` ne troverà.</span><span class="sxs-lookup"><span data-stu-id="eb67a-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="eb67a-212">Tutti i campi sono `filterable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb67a-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="eb67a-213">`sortable` : per impostazione predefinita, il sistema ordina i risultati in base al punteggio, ma in molti casi gli utenti preferiscono eseguire l'ordinamento in base ai campi nei documenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="eb67a-214">I campi di tipo `Collection(Edm.String)` non possono essere `sortable`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="eb67a-215">Tutti gli altri campi sono `sortable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb67a-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="eb67a-216">`facetable`: usato generalmente in una presentazione dei risultati di ricerca che include il numero di risultati per categoria (ad esempio, per cercare fotocamere digitali e visualizzare i risultati in base alla marca, ai megapixel, al prezzo e così via).</span><span class="sxs-lookup"><span data-stu-id="eb67a-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="eb67a-217">Questa opzione non può essere usata con i campi di tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="eb67a-218">Tutti gli altri campi sono `facetable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb67a-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="eb67a-219">**Nota**: i campi di tipo `Edm.String` che sono `filterable`, `sortable` o `facetable` possono avere al massimo una lunghezza di 32 KB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="eb67a-220">Questa limitazione è dovuta al fatto che questi campi sono considerati un unico termine di ricerca e la lunghezza massima di un termine in Ricerca di Azure è 32 KB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="eb67a-221">Se è necessario archiviare più testo in un campo a stringa singola, impostare esplicitamente `filterable`, `sortable` e `facetable` su `false` nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="eb67a-222">**Nota**: se per un campo nessuno degli attributi elencati è impostato su `true` (`searchable`, `filterable`, `sortable` o `facetable`), il campo viene effettivamente escluso dall'indice invertito.</span><span class="sxs-lookup"><span data-stu-id="eb67a-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="eb67a-223">Questa opzione è utile per i campi che non vengono usati nelle query, ma che sono necessari nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="eb67a-224">L'esclusione di tali campi dall'indice consente di ottenere migliori prestazioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="eb67a-225">`key` : contrassegna il campo come contenente identificatori univoci per i documenti all'interno dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="eb67a-226">È necessario scegliere un singolo campo come `key` e questo deve essere di tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="eb67a-227">I campi chiave possono essere usati per la ricerca diretta di documenti tramite l' [API di ricerca](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="eb67a-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="eb67a-228">`retrievable` : specifica se il campo può essere restituito nel risultato di una ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="eb67a-229">Questo attributo è utile quando si vuole usare un campo, ad esempio quello relativo al margine, come meccanismo di filtro, ordinamento o punteggio ma si preferisce che il campo non sia visibile all'utente finale.</span><span class="sxs-lookup"><span data-stu-id="eb67a-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="eb67a-230">L'attributo deve essere `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="eb67a-231">`analyzer` : imposta il nome dell'analizzatore da usare per il campo durante la ricerca e l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="eb67a-232">Per il set di valori consentito, vedere [Analisi in ricerca di Azure](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="eb67a-233">Questa opzione può essere usata solo con campi `searchable` e non può essere impostata con `searchAnalyzer` o `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="eb67a-234">Una volta scelto, l'analizzatore non può essere cambiato per il campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="eb67a-235">`searchAnalyzer` : imposta il nome dell'analizzatore usato per il campo durante la ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="eb67a-236">Per il set di valori consentito, vedere [Analisi in ricerca di Azure](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="eb67a-237">Questa opzione può essere usata solo con i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="eb67a-238">Questa opzione deve essere impostata con `indexAnalyzer` e non può essere impostata con l'opzione `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="eb67a-239">Questo analizzatore può essere aggiornato per un campo esistente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="eb67a-240">`indexAnalyzer` : imposta il nome dell'analizzatore usato per il campo durante l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="eb67a-241">Per il set di valori consentito, vedere [Analisi in ricerca di Azure](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="eb67a-242">Questa opzione può essere usata solo con i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="eb67a-243">Questa opzione deve essere impostata con `searchAnalyzer` e non può essere impostata con l'opzione `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="eb67a-244">Una volta scelto, l'analizzatore non può essere cambiato per il campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="eb67a-245">`suggesters` : imposta la modalità di ricerca e i campi che sono l'origine del contenuto per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="eb67a-246">Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="eb67a-247">`scoringProfiles` : definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati più in alto nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="eb67a-248">I profili di punteggio sono costituiti da funzioni e campi ponderati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="eb67a-249">Per altre informazioni sugli attributi usati in un profilo di punteggio, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="eb67a-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Supporto per le lingue**</span><span class="sxs-lookup"><span data-stu-id="eb67a-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="eb67a-251">I campi disponibili per la ricerca vengono sottoposti a un processo di analisi, che spesso comporta la suddivisione in parole, la normalizzazione del testo e l'esclusione di termini tramite filtro.</span><span class="sxs-lookup"><span data-stu-id="eb67a-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="eb67a-252">Per impostazione predefinita, i campi disponibili per la ricerca in Ricerca di Azure vengono analizzati con l'[analizzatore Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html), che suddivide il testo in elementi sulla base delle [regole di segmentazione del testo Unicode](http://unicode.org/reports/tr29/).</span><span class="sxs-lookup"><span data-stu-id="eb67a-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="eb67a-253">L'analizzatore standard, inoltre, converte tutti i caratteri nel rispettivo formato minuscolo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="eb67a-254">I documenti indicizzati e i termini di ricerca vengono sottoposti ad analisi durante l'indicizzazione e l'elaborazione delle query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="eb67a-255">Ricerca di Azure supporta una varietà di linguaggi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="eb67a-256">Ogni lingua richiede un analizzatore di testo non standard che tenga conto delle caratteristiche specifiche della lingua.</span><span class="sxs-lookup"><span data-stu-id="eb67a-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="eb67a-257">Ricerca di Azure offre due tipi di analizzatori:</span><span class="sxs-lookup"><span data-stu-id="eb67a-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="eb67a-258">35 sono basati sulla tecnologia Lucene.</span><span class="sxs-lookup"><span data-stu-id="eb67a-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="eb67a-259">50 sono basati sulla tecnologia proprietaria di Microsoft per l'elaborazione del linguaggio naturale usata in Office e Bing.</span><span class="sxs-lookup"><span data-stu-id="eb67a-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="eb67a-260">Alcuni sviluppatori potrebbero preferire la soluzione open source di Lucene, più semplice e familiare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="eb67a-261">Gli analizzatori Lucene sono più veloci, ma gli analizzatori Microsoft dispongono di funzionalità avanzate, ad esempio lemmatizzazione, scomposizione delle parole (in lingue come tedesco, danese, olandese, svedese, norvegese, estone, finlandese, ungherese, slovacco) e riconoscimento di entità (URL, messaggi di posta elettronica, date, numeri).</span><span class="sxs-lookup"><span data-stu-id="eb67a-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="eb67a-262">Si consiglia di confrontare, se possibile, gli analizzatori Microsoft e Lucene per scegliere la soluzione più adatta al proprio caso.</span><span class="sxs-lookup"><span data-stu-id="eb67a-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="eb67a-263">***Analizzatori a confronto***</span><span class="sxs-lookup"><span data-stu-id="eb67a-263">***How they compare***</span></span>

<span data-ttu-id="eb67a-264">L'analizzatore Lucene per la lingua inglese estende l'analizzatore standard.</span><span class="sxs-lookup"><span data-stu-id="eb67a-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="eb67a-265">Rimuove il genitivo sassone (la 's finale) dalle parole, applica lo stemming in base all'[algoritmo Porter Stemming](http://tartarus.org/~martin/PorterStemmer/) e rimuove le parole [non significative](http://en.wikipedia.org/wiki/Stop_words) per la lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="eb67a-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="eb67a-266">In confronto, l'analizzatore Microsoft esegue la lemmatizzazione anziché lo stemming.</span><span class="sxs-lookup"><span data-stu-id="eb67a-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="eb67a-267">Significa che è possibile gestire le forme lessicali flesse e irregolari in modo decisamente migliore, producendo risultati di ricerca più rilevanti. Guardare il modulo 7 della [presentazione di Ricerca di Azure MVA](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="eb67a-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="eb67a-268">L'indicizzazione con gli analizzatori Microsoft è in media da due a tre volte più lenta rispetto agli analizzatori Lucene corrispondenti, a seconda della lingua.</span><span class="sxs-lookup"><span data-stu-id="eb67a-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="eb67a-269">Le prestazioni della ricerca non devono essere influenzate in modo significativo per le query di dimensioni medie.</span><span class="sxs-lookup"><span data-stu-id="eb67a-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="eb67a-270">***Configurazione***</span><span class="sxs-lookup"><span data-stu-id="eb67a-270">***Configuration***</span></span>

<span data-ttu-id="eb67a-271">Per ogni campo nella definizione dell'indice, è possibile impostare la proprietà `analyzer` su un nome di analizzatore che specifica la lingua e il fornitore.</span><span class="sxs-lookup"><span data-stu-id="eb67a-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="eb67a-272">Lo stesso analizzatore verrà applicato per l'indicizzazione e la ricerca di tale campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="eb67a-273">Ad esempio, nello stesso indice possono essere presenti campi separati per le descrizioni di hotel in lingua inglese, francese e spagnola.</span><span class="sxs-lookup"><span data-stu-id="eb67a-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="eb67a-274">Usare il [parametro di query 'searchFields'](#SearchQueryParameters) per indicare il campo specifico della lingua da ricercare nelle query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="eb67a-275">È possibile esaminare gli esempi di query che includono la proprietà `analyzer` nella sezione [Eseguire ricerche nei documenti](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="eb67a-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="eb67a-276">***Elenco di analizzatori***</span><span class="sxs-lookup"><span data-stu-id="eb67a-276">***Analyzer list***</span></span>

<span data-ttu-id="eb67a-277">Di seguito è riportato l'elenco delle lingue supportate con i nomi degli analizzatori Lucene e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eb67a-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="eb67a-278">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="eb67a-278">Language</span></span></th>
        <th><span data-ttu-id="eb67a-279">Nome analizzatore Microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="eb67a-280">Nome analizzatore Lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-281">Arabo</span><span class="sxs-lookup"><span data-stu-id="eb67a-281">Arabic</span></span></td>
        <td><span data-ttu-id="eb67a-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-284">Armeno</span><span class="sxs-lookup"><span data-stu-id="eb67a-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="eb67a-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="eb67a-286">Bengalese</span><span class="sxs-lookup"><span data-stu-id="eb67a-286">Bangla</span></span></td>
        <td><span data-ttu-id="eb67a-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="eb67a-288">Basco</span><span class="sxs-lookup"><span data-stu-id="eb67a-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="eb67a-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="eb67a-290">Bulgaro</span><span class="sxs-lookup"><span data-stu-id="eb67a-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="eb67a-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="eb67a-293">Catalano</span><span class="sxs-lookup"><span data-stu-id="eb67a-293">Catalan</span></span></td>
        <td><span data-ttu-id="eb67a-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="eb67a-296">Cinese semplificato</span><span class="sxs-lookup"><span data-stu-id="eb67a-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="eb67a-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-299">Cinese tradizionale</span><span class="sxs-lookup"><span data-stu-id="eb67a-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="eb67a-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="eb67a-302">Croato</span><span class="sxs-lookup"><span data-stu-id="eb67a-302">Croatian</span></span></td>
        <td><span data-ttu-id="eb67a-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-304">Ceco</span><span class="sxs-lookup"><span data-stu-id="eb67a-304">Czech</span></span></td>
        <td><span data-ttu-id="eb67a-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="eb67a-307">Danese</span><span class="sxs-lookup"><span data-stu-id="eb67a-307">Danish</span></span></td>
        <td><span data-ttu-id="eb67a-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="eb67a-310">Olandese</span><span class="sxs-lookup"><span data-stu-id="eb67a-310">Dutch</span></span></td>
        <td><span data-ttu-id="eb67a-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="eb67a-313">Inglese</span><span class="sxs-lookup"><span data-stu-id="eb67a-313">English</span></span></td>        
        <td><span data-ttu-id="eb67a-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-316">Estone</span><span class="sxs-lookup"><span data-stu-id="eb67a-316">Estonian</span></span></td>
        <td><span data-ttu-id="eb67a-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-318">Finlandese</span><span class="sxs-lookup"><span data-stu-id="eb67a-318">Finnish</span></span></td>
        <td><span data-ttu-id="eb67a-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="eb67a-321">Francese</span><span class="sxs-lookup"><span data-stu-id="eb67a-321">French</span></span></td>
        <td><span data-ttu-id="eb67a-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-324">Gallego</span><span class="sxs-lookup"><span data-stu-id="eb67a-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="eb67a-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="eb67a-326">Tedesco</span><span class="sxs-lookup"><span data-stu-id="eb67a-326">German</span></span></td>
        <td><span data-ttu-id="eb67a-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-329">Greco</span><span class="sxs-lookup"><span data-stu-id="eb67a-329">Greek</span></span></td>
        <td><span data-ttu-id="eb67a-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="eb67a-332">Gujarati</span></span></td>
        <td><span data-ttu-id="eb67a-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-334">Ebraico</span><span class="sxs-lookup"><span data-stu-id="eb67a-334">Hebrew</span></span></td>
        <td><span data-ttu-id="eb67a-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="eb67a-336">Hindi</span></span></td>
        <td><span data-ttu-id="eb67a-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-339">Ungherese</span><span class="sxs-lookup"><span data-stu-id="eb67a-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="eb67a-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-342">Islandese</span><span class="sxs-lookup"><span data-stu-id="eb67a-342">Icelandic</span></span></td>
        <td><span data-ttu-id="eb67a-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-344">Indonesiano (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="eb67a-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="eb67a-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-347">Irlandese</span><span class="sxs-lookup"><span data-stu-id="eb67a-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="eb67a-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="eb67a-349">Italian</span></span></td>
        <td><span data-ttu-id="eb67a-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-352">Giapponese</span><span class="sxs-lookup"><span data-stu-id="eb67a-352">Japanese</span></span></td>
        <td><span data-ttu-id="eb67a-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="eb67a-355">Kannada</span></span></td>
        <td><span data-ttu-id="eb67a-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="eb67a-357">Korean</span></span></td>
        <td><span data-ttu-id="eb67a-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-360">Lettone</span><span class="sxs-lookup"><span data-stu-id="eb67a-360">Latvian</span></span></td>        
        <td><span data-ttu-id="eb67a-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="eb67a-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="eb67a-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="eb67a-365">Malayalam</span></span></td>
        <td><span data-ttu-id="eb67a-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-367">Malese (alfabeto latino)</span><span class="sxs-lookup"><span data-stu-id="eb67a-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="eb67a-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="eb67a-369">Marathi</span></span></td>
        <td><span data-ttu-id="eb67a-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-371">Norvegese</span><span class="sxs-lookup"><span data-stu-id="eb67a-371">Norwegian</span></span></td>
        <td><span data-ttu-id="eb67a-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="eb67a-374">Persiano</span><span class="sxs-lookup"><span data-stu-id="eb67a-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="eb67a-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="eb67a-376">Polacco</span><span class="sxs-lookup"><span data-stu-id="eb67a-376">Polish</span></span></td>
        <td><span data-ttu-id="eb67a-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-379">Portoghese (Brasile)</span><span class="sxs-lookup"><span data-stu-id="eb67a-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="eb67a-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-382">Portoghese (Portogallo)</span><span class="sxs-lookup"><span data-stu-id="eb67a-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="eb67a-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="eb67a-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="eb67a-385">Punjabi</span></span></td>
        <td><span data-ttu-id="eb67a-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-387">Romeno</span><span class="sxs-lookup"><span data-stu-id="eb67a-387">Romanian</span></span></td>
        <td><span data-ttu-id="eb67a-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-390">Russo</span><span class="sxs-lookup"><span data-stu-id="eb67a-390">Russian</span></span></td>
        <td><span data-ttu-id="eb67a-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-393">Serbo (alfabeto cirillico)</span><span class="sxs-lookup"><span data-stu-id="eb67a-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="eb67a-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-395">Serbo (alfabeto latino)</span><span class="sxs-lookup"><span data-stu-id="eb67a-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="eb67a-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-397">Slovacco</span><span class="sxs-lookup"><span data-stu-id="eb67a-397">Slovak</span></span></td>
        <td><span data-ttu-id="eb67a-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-399">Sloveno</span><span class="sxs-lookup"><span data-stu-id="eb67a-399">Slovenian</span></span></td>
        <td><span data-ttu-id="eb67a-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-401">Spagnolo</span><span class="sxs-lookup"><span data-stu-id="eb67a-401">Spanish</span></span></td>
        <td><span data-ttu-id="eb67a-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-404">Svedese</span><span class="sxs-lookup"><span data-stu-id="eb67a-404">Swedish</span></span></td>
        <td><span data-ttu-id="eb67a-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="eb67a-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="eb67a-407">Tamil</span></span></td>
        <td><span data-ttu-id="eb67a-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="eb67a-409">Telugu</span></span></td>
        <td><span data-ttu-id="eb67a-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-411">Thai</span><span class="sxs-lookup"><span data-stu-id="eb67a-411">Thai</span></span></td>
        <td><span data-ttu-id="eb67a-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-414">Turco</span><span class="sxs-lookup"><span data-stu-id="eb67a-414">Turkish</span></span></td>
        <td><span data-ttu-id="eb67a-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="eb67a-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-417">Ucraino</span><span class="sxs-lookup"><span data-stu-id="eb67a-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="eb67a-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="eb67a-419">Urdu</span></span></td>
        <td><span data-ttu-id="eb67a-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="eb67a-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="eb67a-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="eb67a-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="eb67a-423">Ricerca di Azure fornisce inoltre configurazioni dell'analizzatore indipendenti dalla lingua</span><span class="sxs-lookup"><span data-stu-id="eb67a-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="eb67a-424">Riduzione ASCII standard</span><span class="sxs-lookup"><span data-stu-id="eb67a-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="eb67a-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="eb67a-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="eb67a-426">Segmentazione di testo Unicode (tokenizer standard)</span><span class="sxs-lookup"><span data-stu-id="eb67a-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="eb67a-427">Filtro di riduzione ASCII: converte i caratteri Unicode che non appartengono al set dei primi 127 caratteri ASCII nei rispettivi equivalenti ASCII.</span><span class="sxs-lookup"><span data-stu-id="eb67a-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="eb67a-428">Questo filtro è utile per la rimozione dei segni diacritici.</span><span class="sxs-lookup"><span data-stu-id="eb67a-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="eb67a-429">Tutti gli analizzatori con nomi contenenti la parola <i>lucene</i> sono basati sugli [analizzatori di lingua Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="eb67a-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="eb67a-430">Altre informazioni sul filtro di riduzione ASCII sono disponibili [qui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="eb67a-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="eb67a-431">**Componenti per il suggerimento**</span><span class="sxs-lookup"><span data-stu-id="eb67a-431">**Suggesters**</span></span>

<span data-ttu-id="eb67a-432">Un `suggester` definisce i campi di un indice che vengono utilizzati come supporto per il completamento automatico nelle ricerche.</span><span class="sxs-lookup"><span data-stu-id="eb67a-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="eb67a-433">In genere le stringhe di ricerca parziali vengono inviate all' [API per i suggerimenti](#Suggestions) mentre l'utente digita la query di ricerca e l'API restituisce un set di espressioni suggerite.</span><span class="sxs-lookup"><span data-stu-id="eb67a-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="eb67a-434">Un componente per il suggerimento definito dall'utente nell'indice consente di determinare i campi utilizzati per creare i termini di ricerca a completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="eb67a-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="eb67a-435">Per visualizzare i dettagli sulla configurazione, consultare [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="eb67a-436">**Profili di punteggio**</span><span class="sxs-lookup"><span data-stu-id="eb67a-436">**Scoring profiles**</span></span>

<span data-ttu-id="eb67a-437">Un `scoringProfile` definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati più in alto nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="eb67a-438">I profili di punteggio sono costituiti da funzioni e campi ponderati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="eb67a-439">Per utilizzarli, è necessario specificare il nome di un profilo nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="eb67a-440">Un profilo di punteggio predefinito viene eseguito in background al fine di calcolare un punteggio di ricerca per ogni elemento visualizzato in un set di risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="eb67a-441">È possibile utilizzare un profilo di punteggio interno, senza nome.</span><span class="sxs-lookup"><span data-stu-id="eb67a-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="eb67a-442">In alternativa, è possibile impostare il `defaultScoringProfile` affinché usi un profilo personalizzato come predefinito. Tale profilo può essere richiamato ogni volta in cui un profilo personalizzato non viene specificato nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="eb67a-443">Per ulteriori dettagli, vedere [Aggiungere profili di punteggio a un indice di ricerca (API REST di Ricerca di Azure)](search-api-scoring-profiles-2015-02-28-preview.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="eb67a-444">**Opzioni CORS**</span><span class="sxs-lookup"><span data-stu-id="eb67a-444">**CORS Options**</span></span>

<span data-ttu-id="eb67a-445">JavaScript sul lato client non può chiamare API per impostazione predefinita perché il browser impedisce tutte le richieste con origini diverse.</span><span class="sxs-lookup"><span data-stu-id="eb67a-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="eb67a-446">Per consentire query con origini diverse nell'indice, abilitare CORS (Cross-Origin Resource Sharing) impostando l'attributo `corsOptions` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="eb67a-447">Si noti che, per motivi di sicurezza, solo le API di query supportano CORS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="eb67a-448">Per CORS è possibile impostare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb67a-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="eb67a-449">`allowedOrigins` (obbligatoria): si tratta di un elenco di origini a cui verrà concesso l'accesso all'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="eb67a-450">Questo significa che al codice JavaScript servito da queste origini sarà consentito eseguire query sull'indice, purché fornisca la chiave API corretta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="eb67a-451">Ogni origine è in genere nel formato `protocol://fully-qualified-domain-name:port` anche se spesso la porta viene omessa.</span><span class="sxs-lookup"><span data-stu-id="eb67a-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="eb67a-452">Per altri dettagli, vedere [questo articolo](http://go.microsoft.com/fwlink/?LinkId=330822) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="eb67a-453">Per consentire l'accesso a tutte le origini, includere `*` come unico elemento nella matrice `allowedOrigins`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="eb67a-454">Tenere presente che **questa non è la procedura consigliata per i servizi di ricerca di produzione.**</span><span class="sxs-lookup"><span data-stu-id="eb67a-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="eb67a-455">Può comunque essere utile per finalità di sviluppo o debug.</span><span class="sxs-lookup"><span data-stu-id="eb67a-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="eb67a-456">`maxAgeInSeconds` (facoltativa): i browser usano questo valore per determinare la durata (in secondi) di memorizzazione nella cache delle risposte preliminari CORS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="eb67a-457">Questo valore deve essere un intero non negativo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-457">This must be a non-negative integer.</span></span> <span data-ttu-id="eb67a-458">A un valore più grande corrispondono prestazioni migliori, ma deve trascorrere più tempo prima che le modifiche dei criteri CORS diventino effettive.</span><span class="sxs-lookup"><span data-stu-id="eb67a-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="eb67a-459">Se questo valore non è impostato, viene usata una durata predefinita di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="eb67a-460"><a name="CreateUpdateIndexExample"></a>
**Esempio di corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="eb67a-461">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-461">**Response**</span></span>

<span data-ttu-id="eb67a-462">Per una richiesta con esito positivo: "201 Creato".</span><span class="sxs-lookup"><span data-stu-id="eb67a-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="eb67a-463">Per impostazione predefinita, il corpo della risposta contiene il codice JSON per la definizione di indice creata.</span><span class="sxs-lookup"><span data-stu-id="eb67a-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="eb67a-464">Se l'intestazione della richiesta `Prefer` è impostata su `return=minimal`, il corpo della risposta sarà vuoto e il codice di stato per l'esito positivo sarà "204 Nessun contenuto" anziché "201 Creato".</span><span class="sxs-lookup"><span data-stu-id="eb67a-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="eb67a-465">Questo vale indipendentemente dall'uso del metodo PUT o POST per creare l'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="eb67a-466">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="eb67a-466">**Remarks**</span></span>

<span data-ttu-id="eb67a-467">Attualmente è previsto un supporto limitato per gli aggiornamenti dello schema di indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="eb67a-468">Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="eb67a-469">È possibile aggiungere nuovi campi a un indice esistente in qualsiasi momento, anche se i campi esistenti non possono essere modificati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="eb67a-470">Quando si aggiunge un nuovo campo, tutti i documenti esistenti nell'indice avranno automaticamente un valore Null per tale campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="eb67a-471">Non verrà utilizzato ulteriore spazio di archiviazione finché non verranno aggiunti nuovi documenti all'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="eb67a-472">Componenti per il suggerimento</span><span class="sxs-lookup"><span data-stu-id="eb67a-472">Suggesters</span></span>
<span data-ttu-id="eb67a-473">Il suggerimento di Ricerca di Azure rappresenta una funzionalità di query a completamento automatico o a digitazione automatica, che offre un elenco di possibili termini di ricerca in risposta a input della stringa parziali e immessi nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="eb67a-474">I suggerimenti di query sono quelli visualizzati quando si usano i motori di ricerca commerciali: se si digita ".NET" in Bing, viene visualizzato un elenco di termini quali ".NET 4.5", ".NET Framework 3.5" e così via.</span><span class="sxs-lookup"><span data-stu-id="eb67a-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="eb67a-475">Quando si utilizza l'API REST di Ricerca di Azure, l'implementazione dei suggerimenti in un'applicazione di Ricerca di Azure richiede che vengano eseguite le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="eb67a-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="eb67a-476">Abilitare i suggerimenti aggiungendo una costruzione **suggester** nell'indice, assegnandole un nome, una modalità di ricerca e un elenco di campi nei quali richiamare la digitazione automatica.</span><span class="sxs-lookup"><span data-stu-id="eb67a-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="eb67a-477">Ad esempio, se si specifica "cityName" come campo di origine e si digita la stringa di ricerca parziale "Sea", verranno visualizzati nomi di città quali "Seattle", "Seaside" e "Seatac". Questi tre nomi rappresentano i suggerimenti di query offerti all'utente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="eb67a-478">Richiamare i suggerimenti utilizzando l' [API per i suggerimenti](#Suggestions) nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="eb67a-479">In genere, le stringhe di ricerca parziali vengono inviate al servizio mentre l'utente digita la query di ricerca e tale l'API restituisce un set di espressioni suggerite.</span><span class="sxs-lookup"><span data-stu-id="eb67a-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="eb67a-480">In questo articolo viene spiegato come configurare un **componente per il suggerimento**.</span><span class="sxs-lookup"><span data-stu-id="eb67a-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="eb67a-481">Inoltre, è necessario consultare l'articolo [API per i suggerimenti](#Suggestions) per informazioni dettagliate sulla modalità di utilizzo di un componente per il suggerimento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="eb67a-482">**Utilizzo**</span><span class="sxs-lookup"><span data-stu-id="eb67a-482">**Usage**</span></span>

<span data-ttu-id="eb67a-483">`Suggesters` vengono creati nell'indice e funzionano in modo ottimale quando vengono usati per suggerire documenti specifici anziché espressioni o termini separati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="eb67a-484">I campi che rappresentano i candidati migliori sono i titoli, i nomi e le altre frasi relativamente brevi che possono identificare un elemento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="eb67a-485">I campi meno efficaci sono quelli ripetitivi, come le categorie e i tag, o quelli molto lunghi, come le descrizioni o i commenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="eb67a-486">Come parte della definizione dell'indice è possibile aggiungere un solo componente per il suggerimento alla raccolta `suggesters` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="eb67a-487">Un componente per il suggerimento è definito dalle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb67a-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="eb67a-488">`name`: nome del componente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="eb67a-489">Questo nome viene usato nelle chiamate all'API `suggest` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="eb67a-490">`searchMode`: strategia usata per la ricerca di espressioni candidate.</span><span class="sxs-lookup"><span data-stu-id="eb67a-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="eb67a-491">L'unica modalità attualmente supportata è `analyzingInfixMatching`, che ricerca una corrispondenza flessibile di espressioni all'inizio o all'interno di frasi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="eb67a-492">`sourceFields`: elenco di uno o più campi che sono l'origine del contenuto per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="eb67a-493">Solo i campi di tipo `Edm.String` e `Collection(Edm.String)` possono essere origini per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="eb67a-494">È possibile usare solo campi per i quali non è impostato un analizzatore di lingua personalizzato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="eb67a-495">**Esempio di componente di suggerimento**</span><span class="sxs-lookup"><span data-stu-id="eb67a-495">**Suggester Example**</span></span>

<span data-ttu-id="eb67a-496">Un componente di suggerimento fa parte dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-496">A suggester is part of the index.</span></span> <span data-ttu-id="eb67a-497">Nella versione attuale della raccolta `suggesters` può essere presente un solo componente per il suggerimento, insieme alla raccolta dei campi e dei `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="eb67a-498">Se è stata usata la versione di anteprima pubblica di Ricerca di Azure, `suggesters` sostituisce una proprietà booleana precedente (`"suggestions": false`) che supporta solo suggerimenti di tipo prefisso per le stringhe brevi (da 3 a 25 caratteri).</span><span class="sxs-lookup"><span data-stu-id="eb67a-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="eb67a-499">Il relativo sostituto, `suggesters`, supporta la corrispondenza di infissi che trova termini corrispondenti all'inizio o all'interno del contenuto del campo, con una migliore tolleranza per gli errori nelle stringhe di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="eb67a-500">A partire dalla versione disponibile al pubblico, questa è la sola implementazione dell'API Suggestions.</span><span class="sxs-lookup"><span data-stu-id="eb67a-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="eb67a-501">La proprietà `suggestions` precedente introdotta in `api-version=2014-07-31-Preview` continua a funzionare in tale versione, ma non è operativa nella versione `2015-02-28` o successiva di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="eb67a-502">Aggiornare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-502">Update Index</span></span>
<span data-ttu-id="eb67a-503">È possibile aggiornare un indice esistente in Ricerca di Azure usando una richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="eb67a-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="eb67a-504">Le operazioni di aggiornamento valide includono l'aggiunta di nuovi campi allo schema esistente, la modifica delle opzioni CORS e la modifica dei profili di punteggio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="eb67a-505">Per altre informazioni, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="eb67a-506">È necessario specificare il nome dell'indice da aggiornare nell'URI della richiesta:</span><span class="sxs-lookup"><span data-stu-id="eb67a-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="eb67a-507">**Importante** : il supporto per gli aggiornamenti dello schema di indice è limitato alle operazioni che non richiedono la ricompilazione dell'indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="eb67a-508">Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="eb67a-509">È possibile aggiungere nuovi campi in qualsiasi momento, anche se i campi esistenti non possono essere modificati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="eb67a-510">Lo stesso vale per `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="eb67a-511">È possibile aggiungere nuovi campi a un componente di questo tipo, ma non è possibile rimuoverli da `suggesters` né aggiungere campi esistenti a `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="eb67a-512">Quando si aggiunge un nuovo campo a un indice, tutti i documenti esistenti nell'indice avranno automaticamente un valore Null per tale campo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="eb67a-513">Non verrà utilizzato ulteriore spazio di archiviazione finché non verranno aggiunti nuovi documenti all'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="eb67a-514">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-514">**Request**</span></span>

<span data-ttu-id="eb67a-515">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="eb67a-516">La richiesta di **aggiornamento di un indice** viene creata mediante HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="eb67a-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="eb67a-517">Nel caso di PUT, il nome dell'indice fa parte dell'URL.</span><span class="sxs-lookup"><span data-stu-id="eb67a-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="eb67a-518">Se l'indice non esiste, viene creato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="eb67a-519">Se esiste già, viene aggiornato in base alla nuova definizione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="eb67a-520">Il nome dell'indice deve essere scritto in caratteri minuscoli, deve iniziare con una lettera o un numero, non deve contenere barre o punti e deve avere una lunghezza inferiore ai 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="eb67a-521">Dopo l'iniziale costituita da una lettera o un numero, il resto del nome può contenere lettere, numeri e trattini, purché i trattini non siano consecutivi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="eb67a-522">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-523">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-524">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-525">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-525">**Request Headers**</span></span>

<span data-ttu-id="eb67a-526">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-527">`Content-Type`: richiesto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-527">`Content-Type`: Required.</span></span> <span data-ttu-id="eb67a-528">Impostare il valore su `application/json`</span><span class="sxs-lookup"><span data-stu-id="eb67a-528">Set this to `application/json`</span></span>
* <span data-ttu-id="eb67a-529">`api-key`: richiesto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-529">`api-key`: Required.</span></span> <span data-ttu-id="eb67a-530">L'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-531">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-532">La richiesta di **aggiornamento dell'indice** deve includere un'intestazione `api-key` impostata sulla chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-533">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-534">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-535">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-536">**Sintassi del corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-536">**Request Body Syntax**</span></span>

<span data-ttu-id="eb67a-537">Quando si aggiorna un indice esistente, il corpo deve includere la definizione di schema originale e i nuovi campi aggiunti, nonché i profili di punteggio modificati, i componenti per il suggerimento e le opzioni CORS, se presenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="eb67a-538">Se non si modificano i profili di punteggio e le opzioni CORS, è necessario includere i valori originali da quando è stato creato l'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="eb67a-539">In generale, la procedura ottimale per gli aggiornamenti consiste nel recuperare la definizione dell'indice mediante GET, modificarla e quindi aggiornarla mediante PUT.</span><span class="sxs-lookup"><span data-stu-id="eb67a-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="eb67a-540">Per comodità, di seguito è riprodotta la sintassi dello schema usata per creare un indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="eb67a-541">Per altri dettagli, vedere [Creare un indice](#CreateIndex) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="eb67a-542">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-542">**Response**</span></span>

<span data-ttu-id="eb67a-543">Per una richiesta con esito positivo: "204 Nessun contenuto".</span><span class="sxs-lookup"><span data-stu-id="eb67a-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="eb67a-544">Per impostazione predefinita, il corpo della risposta è vuoto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-544">By default the response body will be empty.</span></span> <span data-ttu-id="eb67a-545">Se invece l'intestazione della richiesta `Prefer` è impostata su `return=representation`, il corpo della risposta conterrà il codice JSON per la definizione di indice aggiornata.</span><span class="sxs-lookup"><span data-stu-id="eb67a-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="eb67a-546">In questo caso, il codice di stato di esito positivo sarà "200 OK".</span><span class="sxs-lookup"><span data-stu-id="eb67a-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="eb67a-547">**Aggiornamento della definizione dell'indice con analizzatori personalizzati**</span><span class="sxs-lookup"><span data-stu-id="eb67a-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="eb67a-548">Dopo che un analizzatore, un tokenizer, un filtro di token o un filtro di carattere è stato definito non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="eb67a-549">È possibile aggiungerne di nuovi a un indice esistente solo se il flag `allowIndexDowntime` è impostato su true nella richiesta di aggiornamento dell'indice:</span><span class="sxs-lookup"><span data-stu-id="eb67a-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="eb67a-550">Si noti che questa operazione metterà l'indice offline almeno per alcuni secondi, causando la mancata riuscita dell'indicizzazione e delle richieste di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="eb67a-551">Le prestazioni e la disponibilità alla scrittura dell'indice possono risultare inferiori per vari minuti dopo che l'indice è stato aggiornato o più a lungo per gli indici molto grandi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="eb67a-552">Elencare gli indici</span><span class="sxs-lookup"><span data-stu-id="eb67a-552">List Indexes</span></span>
<span data-ttu-id="eb67a-553">L'operazione per **elencare gli indici** restituisce un elenco degli indici attualmente disponibili in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="eb67a-554">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-554">**Request**</span></span>

<span data-ttu-id="eb67a-555">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="eb67a-556">La richiesta per **elencare gli indici** può essere creata mediante il metodo GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="eb67a-557">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-558">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-559">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-560">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-560">**Request Headers**</span></span>

<span data-ttu-id="eb67a-561">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-562">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-562">`api-key`: Required.</span></span> <span data-ttu-id="eb67a-563">L'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-564">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-565">La richiesta per **elencare gli indici** deve includere un'intestazione `api-key` impostata su una chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-566">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-567">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-568">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-569">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-569">**Request Body**</span></span>

<span data-ttu-id="eb67a-570">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-570">None.</span></span>

<span data-ttu-id="eb67a-571">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-571">**Response**</span></span>

<span data-ttu-id="eb67a-572">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="eb67a-573">Di seguito è riportato il corpo di una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="eb67a-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="eb67a-574">Si noti che è possibile filtrare la risposta fino a visualizzare solo le proprietà a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="eb67a-575">Ad esempio, se si vuole solo un elenco di nomi di indice, usare l'opzione di query `$select` di OData:</span><span class="sxs-lookup"><span data-stu-id="eb67a-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="eb67a-576">In questo caso, la risposta dell'esempio precedente sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="eb67a-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="eb67a-577">Questa è una tecnica utile per risparmiare larghezza di banda, se nel servizio di ricerca sono presenti numerosi indici.</span><span class="sxs-lookup"><span data-stu-id="eb67a-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="eb67a-578">Ottenere un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-578">Get Index</span></span>
<span data-ttu-id="eb67a-579">L'operazione per **ottenere un indice** recupera la definizione dell'indice da Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="eb67a-580">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-580">**Request**</span></span>

<span data-ttu-id="eb67a-581">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-582">La richiesta per **ottenere un indice** può essere creata mediante il metodo GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="eb67a-583">Il valore [index name] nell'URI della richiesta specifica l'indice da restituire dalla raccolta di indici.</span><span class="sxs-lookup"><span data-stu-id="eb67a-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="eb67a-584">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-585">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-586">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-587">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-587">**Request Headers**</span></span>

<span data-ttu-id="eb67a-588">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-589">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-590">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-591">La richiesta per **ottenere un indice** deve includere un'intestazione `api-key` impostata su una chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-592">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-593">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-594">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-595">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-595">**Request Body**</span></span>

<span data-ttu-id="eb67a-596">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-596">None.</span></span>

<span data-ttu-id="eb67a-597">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-597">**Response**</span></span>

<span data-ttu-id="eb67a-598">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="eb67a-599">Per un esempio di payload di risposta, vedere l'esempio JSON nella sezione relativa alla [creazione di un indice](#CreateUpdateIndexExample) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="eb67a-600">Eliminare un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-600">Delete Index</span></span>
<span data-ttu-id="eb67a-601">L'operazione di **eliminazione di un indice** rimuove un indice e i documenti associati da Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="eb67a-602">È possibile ottenere il nome dell'indice dal dashboard servizi nel portale di Azure oppure dall'API.</span><span class="sxs-lookup"><span data-stu-id="eb67a-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="eb67a-603">Per informazioni dettagliate, vedere [Elencare gli indici](#ListIndexes) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="eb67a-604">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-604">**Request**</span></span>

<span data-ttu-id="eb67a-605">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-606">La richiesta di **eliminazione di un indice** può essere creata mediante il metodo DELETE.</span><span class="sxs-lookup"><span data-stu-id="eb67a-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="eb67a-607">Il valore [index name] nell'URI della richiesta specifica l'indice da eliminare dalla raccolta di indici.</span><span class="sxs-lookup"><span data-stu-id="eb67a-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="eb67a-608">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-609">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-610">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-611">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-611">**Request Headers**</span></span>

<span data-ttu-id="eb67a-612">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-613">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-613">`api-key`: Required.</span></span> <span data-ttu-id="eb67a-614">L'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-615">È un valore stringa univoco per l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="eb67a-616">La richiesta di **eliminazione di un indice** deve includere un'intestazione `api-key` impostata sulla chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-617">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-618">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-619">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-620">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-620">**Request Body**</span></span>

<span data-ttu-id="eb67a-621">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-621">None.</span></span>

<span data-ttu-id="eb67a-622">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-622">**Response**</span></span>

<span data-ttu-id="eb67a-623">Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="eb67a-624">Ottenere le statistiche di un indice</span><span class="sxs-lookup"><span data-stu-id="eb67a-624">Get Index Statistics</span></span>
<span data-ttu-id="eb67a-625">L'operazione per **ottenere le statistiche di un indice** restituisce il numero dei documenti per l'indice corrente da Ricerca di Azure, oltre all'utilizzo dello spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="eb67a-626">Le statistiche sul numero di documenti e le dimensioni vengono raccolte ad intervalli di pochi minuti, non in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="eb67a-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="eb67a-627">Di conseguenza, le statistiche restituite da questa API potrebbero non riflettere le modifiche apportate da operazioni di indicizzazione recenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="eb67a-628">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-628">**Request**</span></span>

<span data-ttu-id="eb67a-629">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="eb67a-630">La richiesta per **ottenere le statistiche di un indice** può essere creata mediante il metodo GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="eb67a-631">Il valore [index name] nell'URI della richiesta indica al servizio di restituire le statistiche per l'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="eb67a-632">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-633">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-634">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-635">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-635">**Request Headers**</span></span>

<span data-ttu-id="eb67a-636">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-637">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-638">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-639">La richiesta per ottenere le **statistiche di un indice** deve includere un'intestazione `api-key` impostata su una chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-640">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-641">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-642">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-643">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-643">**Request Body**</span></span>

<span data-ttu-id="eb67a-644">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-644">None.</span></span>

<span data-ttu-id="eb67a-645">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-645">**Response**</span></span>

<span data-ttu-id="eb67a-646">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="eb67a-647">Il corpo della risposta è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="eb67a-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="eb67a-648">Analizzatore di test</span><span class="sxs-lookup"><span data-stu-id="eb67a-648">Test Analyzer</span></span>
<span data-ttu-id="eb67a-649">L' **API di analisi** illustra come un analizzatore suddivide il testo in token.</span><span class="sxs-lookup"><span data-stu-id="eb67a-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="eb67a-650">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-650">**Request**</span></span>

<span data-ttu-id="eb67a-651">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="eb67a-652">La richiesta dell' **API di analisi** può essere creata con il metodo POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="eb67a-653">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-654">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-655">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-656">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-656">**Request Headers**</span></span>

<span data-ttu-id="eb67a-657">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-658">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-659">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-660">La richiesta dell'**API di analisi** deve includere un'intestazione `api-key` impostata su una chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-661">Per creare l'URL della richiesta, sono necessari anche il nome dell'indice e il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-662">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-663">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-664">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="eb67a-665">oppure</span><span class="sxs-lookup"><span data-stu-id="eb67a-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="eb67a-666">`analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` devono essere nomi validi di analizzatori, tokenizer, filtri di token e filtri char predefiniti o personalizzati per l'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="eb67a-667">Per altre informazioni sul processo di analisi lessicale vedere la pagina relativa all' [analisi in Ricerca di Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="eb67a-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="eb67a-668">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-668">**Response**</span></span>

<span data-ttu-id="eb67a-669">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="eb67a-670">Il corpo della risposta è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="eb67a-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="eb67a-671">**Esempio dell'API di analisi**</span><span class="sxs-lookup"><span data-stu-id="eb67a-671">**Analyze API example**</span></span>

<span data-ttu-id="eb67a-672">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="eb67a-673">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="eb67a-674">Operazioni sui documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-674">Document Operations</span></span>
<span data-ttu-id="eb67a-675">In Ricerca di Azure un indice viene archiviato nel cloud e popolato usando i documenti JSON che vengono caricati nel servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="eb67a-676">Tutti i documenti caricati costituiscono l'insieme dei dati di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="eb67a-677">I documenti includono campi, alcuni dei quali sono stati suddivisi in token corrispondenti a termini di ricerca durante il caricamento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="eb67a-678">Il segmento `/docs` dell'URL nell'API di Ricerca di Azure rappresenta la raccolta di documenti in un indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="eb67a-679">Tutte le operazioni sulla raccolta, ad esempio caricamento, unione, eliminazione o query nei documenti, vengono eseguite nel contesto di un singolo indice e quindi gli URL per queste operazioni inizieranno sempre con `/indexes/[index name]/docs` per un nome di indice specifico.</span><span class="sxs-lookup"><span data-stu-id="eb67a-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="eb67a-680">Il codice dell'applicazione deve generare documenti JSON da caricare in Ricerca di Azure oppure è possibile usare un [indicizzatore](https://msdn.microsoft.com/library/dn946891.aspx) per caricare documenti se l'origine dati è il database SQL di Azure o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="eb67a-681">In genere, gli indici vengono popolati da un singolo set di dati specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="eb67a-682">È consigliabile avere a disposizione un documento per ogni elemento da cercare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="eb67a-683">Un'applicazione per il noleggio di film può avere un documento per ogni film, un'applicazione di tipo vetrina può avere un documento per ogni SKU, un'applicazione per corsi online può avere un documento per ogni corso oppure una società di ricerche può avere un documento per ogni articolo accademico disponibile nel proprio archivio e così via.</span><span class="sxs-lookup"><span data-stu-id="eb67a-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="eb67a-684">I documenti sono costituiti da uno o più campi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="eb67a-685">I campi possono contenere testo suddiviso da Ricerca di Azure in token corrispondenti a termini di ricerca, oltre a valori senza token o non di testo che possono essere usati nei filtri o nei profili di punteggio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="eb67a-686">I nomi, i tipi di dati e le funzionalità di ricerca supportati per ogni campo sono determinati dallo schema dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="eb67a-687">Uno dei campi in ogni schema di indice deve essere designato come ID e ogni documento deve avere un valore per il campo ID che identifica in modo univoco tale documento nell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="eb67a-688">Tutti gli altri campi dei documenti sono facoltativi e, se non è specificato alcun valore, viene usato il valore predefinito Null.</span><span class="sxs-lookup"><span data-stu-id="eb67a-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="eb67a-689">Si noti che i valori Null non occupano spazio nell'indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="eb67a-690">Prima di poter caricare documenti, è necessario aver creato l'indice nel servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="eb67a-691">Per informazioni dettagliate su questo primo passaggio, vedere [Creare un indice](#CreateIndex) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="eb67a-692">aggiunta, aggiornamento o eliminazione di documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="eb67a-693">È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="eb67a-694">Per un numero elevato di aggiornamenti, è consigliabile creare batch di documenti (fino a 1000 documenti per batch o circa 16 MB per batch).</span><span class="sxs-lookup"><span data-stu-id="eb67a-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="eb67a-695">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-695">**Request**</span></span>

<span data-ttu-id="eb67a-696">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="eb67a-697">È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="eb67a-698">L'URI della richiesta include [index name], che specifica l'indice su cui eseguire l'operazione POST sui documenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="eb67a-699">Questa operazione può essere eseguita su un solo indice alla volta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="eb67a-700">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-701">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-702">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-703">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-703">**Request Headers**</span></span>

<span data-ttu-id="eb67a-704">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-705">`Content-Type`: richiesto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-705">`Content-Type`: Required.</span></span> <span data-ttu-id="eb67a-706">Impostare il valore su `application/json`</span><span class="sxs-lookup"><span data-stu-id="eb67a-706">Set this to `application/json`</span></span>
* <span data-ttu-id="eb67a-707">`api-key`: richiesto.</span><span class="sxs-lookup"><span data-stu-id="eb67a-707">`api-key`: Required.</span></span> <span data-ttu-id="eb67a-708">L'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-709">È un valore stringa univoco per il servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="eb67a-710">La richiesta di **aggiunta di documenti** deve includere un'intestazione `api-key` impostata sulla chiave amministratore, anziché su una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="eb67a-711">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-712">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-713">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-714">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-714">**Request Body**</span></span>

<span data-ttu-id="eb67a-715">Il corpo della richiesta contiene uno o più documenti da indicizzare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="eb67a-716">I documenti sono identificati da una chiave univoca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="eb67a-717">Ogni documento è associato a un'azione: upload, merge, mergeOrUpload o delete.</span><span class="sxs-lookup"><span data-stu-id="eb67a-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="eb67a-718">Le richieste di caricamento devono includere i dati del documento sotto forma di coppie chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="eb67a-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="eb67a-719">Le chiavi di documenti possono contenere solo lettere, numeri, trattini ("-"), caratteri di sottolineatura ("_") e segni di uguale ("=").</span><span class="sxs-lookup"><span data-stu-id="eb67a-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="eb67a-720">Per altre informazioni, vedere la pagina relativa alle [regole di denominazione](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="eb67a-721">**Azioni sui documenti**</span><span class="sxs-lookup"><span data-stu-id="eb67a-721">**Document Actions**</span></span>

* <span data-ttu-id="eb67a-722">`upload`: questa azione è simile a "upsert", in cui il documento viene inserito se è nuovo e aggiornato o sostituito se già esistente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="eb67a-723">Si noti che nel caso dell'aggiornamento vengono sostituiti tutti i campi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="eb67a-724">`merge`: questa azione aggiorna un documento esistente con i campi specificati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="eb67a-725">Se il documento non esiste, l'unione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="eb67a-726">I campi specificati in un'azione di unione sostituiscono i campi esistenti nel documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="eb67a-727">Sono inclusi anche i campi di tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="eb67a-728">Ad esempio, se il documento contiene un campo "tags" con valore `["budget"]` e si esegue un'azione di unione con valore `["economy", "pool"]` per "tags", il valore finale del campo "tag" sarà `["economy", "pool"]`</span><span class="sxs-lookup"><span data-stu-id="eb67a-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="eb67a-729">e **non** sarà `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="eb67a-730">`mergeOrUpload`: questa azione si comporta come `merge` se nell'indice esiste già un documento con la chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="eb67a-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="eb67a-731">Se invece il documento non è presente, l'azione si comporta come `upload` con un nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="eb67a-732">`delete`: questa azione rimuove il documento specificato dall'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="eb67a-733">Si noti che tutti i campi diversi dal campo chiave specificati in un'operazione `delete` verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="eb67a-734">Se si vuole rimuovere un singolo campo da un documento, usare invece `merge` e impostare il campo su `null` in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="eb67a-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="eb67a-735">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-735">**Response**</span></span>

<span data-ttu-id="eb67a-736">Il codice di stato 200 (OK) viene restituito per una risposta con esito positivo, a indicare che tutti gli elementi sono stati indicizzati correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="eb67a-737">In questo caso, la proprietà `status` viene impostata su true per tutti gli elementi e la proprietà `statusCode` viene impostata su 201 per i documenti appena caricati o su 200 per i documenti uniti o eliminati:</span><span class="sxs-lookup"><span data-stu-id="eb67a-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="eb67a-738">Il codice di stato 207 (Multi-Status) viene restituito quando almeno un elemento non è stato indicizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="eb67a-739">Gli elementi non indicizzati hanno il campo `status` impostato su false.</span><span class="sxs-lookup"><span data-stu-id="eb67a-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="eb67a-740">Le proprietà `errorMessage` e `statusCode` indicheranno il motivo dell'errore di indicizzazione:</span><span class="sxs-lookup"><span data-stu-id="eb67a-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="eb67a-741">La tabella seguente descrive i diversi codici di stato di ogni documento che possono essere restituiti nella risposta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="eb67a-742">Si noti che alcuni indicano problemi con la richiesta, mentre altri indicano condizioni di errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="eb67a-743">Per queste ultime è necessario riprovare dopo un breve intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="eb67a-744">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="eb67a-744">Status code</span></span></th>
        <th><span data-ttu-id="eb67a-745">Significato</span><span class="sxs-lookup"><span data-stu-id="eb67a-745">Meaning</span></span></th>
        <th><span data-ttu-id="eb67a-746">Non irreversibile</span><span class="sxs-lookup"><span data-stu-id="eb67a-746">Retryable</span></span></th>
        <th><span data-ttu-id="eb67a-747">Note</span><span class="sxs-lookup"><span data-stu-id="eb67a-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-748">200</span><span class="sxs-lookup"><span data-stu-id="eb67a-748">200</span></span></td>
        <td><span data-ttu-id="eb67a-749">Il documento è stato modificato o eliminato correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="eb67a-750">n/d</span><span class="sxs-lookup"><span data-stu-id="eb67a-750">n/a</span></span></td>
        <td><span data-ttu-id="eb67a-751">Le operazioni di eliminazione sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>.</span><span class="sxs-lookup"><span data-stu-id="eb67a-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="eb67a-752">In altre parole, anche se non esiste una chiave del documento nell'indice, il tentativo di eseguire un'operazione di eliminazione con quella chiave produrrà un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="eb67a-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-753">201</span><span class="sxs-lookup"><span data-stu-id="eb67a-753">201</span></span></td>
        <td><span data-ttu-id="eb67a-754">Il documento è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="eb67a-755">n/d</span><span class="sxs-lookup"><span data-stu-id="eb67a-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-756">400</span><span class="sxs-lookup"><span data-stu-id="eb67a-756">400</span></span></td>
        <td><span data-ttu-id="eb67a-757">Si è verificato un errore nel documento che ne ha impedito l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="eb67a-758">No</span><span class="sxs-lookup"><span data-stu-id="eb67a-758">No</span></span></td>
        <td><span data-ttu-id="eb67a-759">Il messaggio di errore nella risposta indicherà il problema del documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-760">404</span><span class="sxs-lookup"><span data-stu-id="eb67a-760">404</span></span></td>
        <td><span data-ttu-id="eb67a-761">Non è stato possibile unire il documento perché la chiave specificata non esiste nell'indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="eb67a-762">No</span><span class="sxs-lookup"><span data-stu-id="eb67a-762">No</span></span></td>
        <td><span data-ttu-id="eb67a-763">Questo errore non si verifica per i caricamenti perché questi creano nuovi documenti e non si verifica per le eliminazioni perché queste sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>.</span><span class="sxs-lookup"><span data-stu-id="eb67a-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-764">409</span><span class="sxs-lookup"><span data-stu-id="eb67a-764">409</span></span></td>
        <td><span data-ttu-id="eb67a-765">È stato rilevato un conflitto di versione nel tentativo di indicizzare un documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="eb67a-766">Sì</span><span class="sxs-lookup"><span data-stu-id="eb67a-766">Yes</span></span></td>
        <td><span data-ttu-id="eb67a-767">Ciò può verificarsi quando si prova a indicizzare lo stesso documento più di una volta contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-768">422</span><span class="sxs-lookup"><span data-stu-id="eb67a-768">422</span></span></td>
        <td><span data-ttu-id="eb67a-769">L'indice è temporaneamente non disponibile perché è stato aggiornato con il flag 'allowIndexDowntime' impostato su 'true'.</span><span class="sxs-lookup"><span data-stu-id="eb67a-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="eb67a-770">Sì</span><span class="sxs-lookup"><span data-stu-id="eb67a-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb67a-771">503</span><span class="sxs-lookup"><span data-stu-id="eb67a-771">503</span></span></td>
        <td><span data-ttu-id="eb67a-772">Il servizio di ricerca è temporaneamente non disponibile, probabilmente a causa di un sovraccarico.</span><span class="sxs-lookup"><span data-stu-id="eb67a-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="eb67a-773">Sì</span><span class="sxs-lookup"><span data-stu-id="eb67a-773">Yes</span></span></td>
        <td><span data-ttu-id="eb67a-774">In questo caso, il codice deve attendere prima di riprovare o si rischia di prolungare la non disponibilità del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="eb67a-775">**Nota**: se il codice del client riceve spesso una risposta 207, il problema può dipendere dal carico eccessivo del sistema.</span><span class="sxs-lookup"><span data-stu-id="eb67a-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="eb67a-776">Per una conferma verificare se la proprietà `statusCode` contiene 503.</span><span class="sxs-lookup"><span data-stu-id="eb67a-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="eb67a-777">Se si verifica questo problema, è consigliabile ***limitare le richieste di indicizzazione***.</span><span class="sxs-lookup"><span data-stu-id="eb67a-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="eb67a-778">Se non si riduce il traffico di indicizzazione, è possibile che il sistema inizi a rifiutare tutte le richieste con errori 503.</span><span class="sxs-lookup"><span data-stu-id="eb67a-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="eb67a-779">Il codice di stato 429 indica che è stata superata la quota del numero di documenti per indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="eb67a-780">È necessario creare un nuovo indice o effettuare l'aggiornamento per ottenere limiti di capacità più elevati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="eb67a-781">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="eb67a-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="eb67a-782">ricerca documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-782">Search Documents</span></span>
<span data-ttu-id="eb67a-783">Un'operazione **Search** viene generata come richiesta GET o POST e specifica i parametri che forniscono i criteri per la selezione dei documenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="eb67a-784">**Quando usare POST invece di GET**</span><span class="sxs-lookup"><span data-stu-id="eb67a-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="eb67a-785">Quando si usa HTTP GET per chiamare l'API di **Ricerca** , è necessario tenere presente che la lunghezza dell'URL della richiesta non può superare 8 KB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="eb67a-786">Di solito è sufficiente per la maggior parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-786">This is usually enough for most applications.</span></span> <span data-ttu-id="eb67a-787">Alcune applicazioni, tuttavia, generano query di dimensioni molto grandi o espressioni di filtro OData.</span><span class="sxs-lookup"><span data-stu-id="eb67a-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="eb67a-788">Per queste applicazioni è preferibile usare HTTP POST perché consente filtri e query di maggiori dimensioni rispetto a GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="eb67a-789">Con POST il fattore limitante è il numero di condizioni o di clausole in una query , non la dimensione della query non elaborata, poiché il limite delle dimensioni della richiesta per POST è di circa 16 MB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-790">Anche se il limite della dimensione della richiesta POST è molto grande, le query di ricerca e le espressioni di filtro non possono essere arbitrariamente complesse.</span><span class="sxs-lookup"><span data-stu-id="eb67a-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="eb67a-791">Per altre informazioni sulle limitazioni della complessità dei filtri e delle query di ricerca, vedere [Sintassi delle query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="eb67a-792">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-792">**Request**</span></span>

<span data-ttu-id="eb67a-793">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-794">La richiesta **Search** può essere creata con il metodo GET o POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="eb67a-795">L'URI della richiesta specifica l'indice in cui eseguire la query per tutti i documenti corrispondenti ai parametri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="eb67a-796">I parametri vengono specificati nella stringa di query per le richieste GET e nel corpo della richiesta nel caso di richieste POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="eb67a-797">Come procedura consigliata per la creazione di richieste GET, usare la [codifica dell'URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) per i parametri di query specifici quando si chiama direttamente l'API REST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="eb67a-798">Per le operazioni **Search** sono inclusi i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb67a-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="eb67a-799">La codifica con URL è consigliata solo per questi parametri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="eb67a-800">Se inavvertitamente si codifica con URL l'intera stringa della query (ossia tutti gli elementi che seguono il punto interrogativo), le richieste verranno interrotte.</span><span class="sxs-lookup"><span data-stu-id="eb67a-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="eb67a-801">La codifica dell'URL è necessaria solo quando si chiama direttamente l'API REST con GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="eb67a-802">La codifica dell'URL non è invece necessaria quando si chiama **Search** con POST o quando si usa la [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx)che gestisce automaticamente la codifica dell'URL.</span><span class="sxs-lookup"><span data-stu-id="eb67a-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="eb67a-803"><a name="SearchQueryParameters"></a>
**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="eb67a-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="eb67a-804">**Search** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="eb67a-805">Specificare questi parametri nella stringa di query dell'URL quando si chiama **Search** con GET e come proprietà JSON nel corpo della richiesta quando si chiama **Search** con POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="eb67a-806">La sintassi per alcuni parametri è leggermente diversa tra GET e POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="eb67a-807">Queste differenze sono riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="eb67a-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="eb67a-808">`search=[string]` (facoltativo): specifica il testo da cercare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="eb67a-809">Per impostazione predefinita, la ricerca viene eseguita in tutti i campi `searchable` a meno che non sia specificato `searchFields`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="eb67a-810">Quando si esegue la ricerca nei campi `searchable`, il testo della ricerca viene suddiviso in token. In questo modo, più termini possono essere separati con uno spazio vuoto, ad esempio `search=hello world`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="eb67a-811">Per trovare corrispondenze con qualsiasi termine, usare `*`, che può essere utile per le query con filtro booleano.</span><span class="sxs-lookup"><span data-stu-id="eb67a-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="eb67a-812">L'omissione di questo parametro equivale a impostarlo su `*`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="eb67a-813">Per le specifiche della sintassi di ricerca, vedere [Semplice sintassi di query nella Ricerca di Azure](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="eb67a-814">**Nota**: quando si eseguono query sui campi `searchable`, talvolta si possono ottenere risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="eb67a-815">Il tokenizer include logica per la gestione di casi comuni nel testo inglese, ad esempio apostrofi, virgole nei numeri e così via. Ad esempio, `search=123,456` corrisponde a un singolo termine 123,456 invece che ai termini separati 123 e 456, poiché in inglese le virgole vengono usate come separatore delle migliaia per i numeri di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="eb67a-816">È quindi consigliabile usare uno spazio vuoto in sostituzione dei segni di punteggiatura per separare i termini nel parametro `search`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="eb67a-817">`searchMode=any|all` (facoltativo, il valore predefinito è `any`): specifica se è necessario trovare una corrispondenza con tutti i termini di ricerca o con uno qualsiasi per includere il documento nelle corrispondenze.</span><span class="sxs-lookup"><span data-stu-id="eb67a-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="eb67a-818">`searchFields=[string]` (facoltativo): specifica l'elenco di nomi di campo delimitati da virgole in cui cercare il testo specificato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="eb67a-819">I campi di destinazione devono essere contrassegnati come `searchable`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="eb67a-820">`queryType=simple|full` (facoltativo, il valore predefinito è `simple`): se impostato su testo di ricerca "semplice", viene interpretato mediante un semplice linguaggio di query che consente l'uso di simboli come +, * e "".</span><span class="sxs-lookup"><span data-stu-id="eb67a-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="eb67a-821">Per impostazione predefinita, le query vengono valutate in tutti i campi disponibili per la ricerca o nei campi indicati in `searchFields`in ogni documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="eb67a-822">Quando il tipo di query è impostato su `full` , il testo di ricerca viene interpretato mediante il linguaggio di query Lucene, che consente ricerche specifiche del campo e ponderate.</span><span class="sxs-lookup"><span data-stu-id="eb67a-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="eb67a-823">Per le specifiche delle sintassi di ricerca, vedere [Sintassi di query semplice](https://msdn.microsoft.com/library/dn798920.aspx) e [Sintassi delle query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) nella ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb67a-824">La ricerca in un intervallo non è supportata nel linguaggio di query Lucene ed è sostituita da $filter, che offre funzionalità analoghe.</span><span class="sxs-lookup"><span data-stu-id="eb67a-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="eb67a-825">`moreLikeThis=[key]` (facoltativo) **Importante:** questa funzionalità è disponibile solo in `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-826">Non è possibile usare questa opzione in una query che contiene il parametro di ricerca di testo `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="eb67a-827">Il parametro `moreLikeThis` trova documenti che sono simili al documento specificato dalla chiave del documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="eb67a-828">Quando viene effettuata una richiesta di ricerca con `moreLikeThis`, viene generato un elenco di termini di ricerca in base alla frequenza e alla rarità dei termini nel documento di origine.</span><span class="sxs-lookup"><span data-stu-id="eb67a-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="eb67a-829">Questi termini vengono quindi usati per effettuare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="eb67a-830">Per impostazione predefinita, viene considerato il contenuto di tutti i campi `searchable` a meno che non si usi `searchFields` per limitare i campi in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="eb67a-831">`$skip=#` (facoltativo): specifica il numero di risultati della ricerca da ignorare. Non può essere maggiore di 100.000.</span><span class="sxs-lookup"><span data-stu-id="eb67a-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="eb67a-832">Se è necessario analizzare i documenti in sequenza, ma non è possibile usare `$skip` a causa di questa limitazione, prendere in considerazione l'uso di `$orderby` su una chiave totalmente ordinata e `$filter` con una query di intervallo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-833">Quando si chiama **Search** con POST, questo parametro è denominato `skip` invece di `$skip`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="eb67a-834">`$top=#` (facoltativo): numero di risultati della ricerca da recuperare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="eb67a-835">Può essere usato insieme a `$skip` per implementare il paging sul lato client dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-836">Quando si chiama **Search** con POST, questo parametro è denominato `top` invece di `$top`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="eb67a-837">`$count=true|false` (facoltativo, il valore predefinito è `false`): specifica se recuperare il conteggio totale dei risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="eb67a-838">Si tratta del conteggio di tutti i documenti che corrispondono ai parametri `search` e `$filter`, ignorando `$top` e `$skip`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="eb67a-839">L'impostazione di questo valore su `true` può influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="eb67a-840">Si noti che il conteggio restituito è un'approssimazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-841">Quando si chiama **Search** con POST, questo parametro è denominato `count` invece di `$count`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="eb67a-842">`$orderby=[string]` (facoltativo): specifica un elenco di espressioni delimitate da virgole in base alle quali ordinare i risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="eb67a-843">Ogni espressione può essere un nome campo o una chiamata alla funzione `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="eb67a-844">Ogni espressione può essere seguita da `asc` per indicare l'ordine crescente e da `desc` per indicare l'ordine decrescente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="eb67a-845">Per impostazione predefinita, l'ordinamento è crescente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-845">The default is ascending order.</span></span> <span data-ttu-id="eb67a-846">Le situazioni di parità di priorità vengono risolte in base ai punteggi di corrispondenza dei documenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="eb67a-847">Se `$orderby` non è specificato, l'ordine predefinito è decrescente in base al punteggio di corrispondenza dei documenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="eb67a-848">È previsto un limite di 32 clausole per `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-849">Quando si chiama **Search** con POST, questo parametro è denominato `orderby` invece di `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="eb67a-850">`$select=[string]` (facoltativo): specifica un elenco di campi delimitati da virgole da recuperare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="eb67a-851">Se non è specificato, vengono inclusi tutti i campi contrassegnati come recuperabili nello schema.</span><span class="sxs-lookup"><span data-stu-id="eb67a-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="eb67a-852">È anche possibile richiedere in modo esplicito tutti i campi impostando questo parametro su `*`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-853">Quando si chiama **Search** con POST, questo parametro è denominato `select` invece di `$select`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="eb67a-854">`facet=[string]` (zero o più): specifica un campo da usare per l'esplorazione in base a facet.</span><span class="sxs-lookup"><span data-stu-id="eb67a-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="eb67a-855">La stringa può contenere parametri per personalizzare l'esplorazione in base a facet, espressi come coppie `name:value` delimitate da virgole.</span><span class="sxs-lookup"><span data-stu-id="eb67a-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="eb67a-856">I parametri validi sono:</span><span class="sxs-lookup"><span data-stu-id="eb67a-856">Valid parameters are:</span></span>

* <span data-ttu-id="eb67a-857">`count`: numero massimo di termini facet. Il valore predefinito è 10.</span><span class="sxs-lookup"><span data-stu-id="eb67a-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="eb67a-858">Non è previsto alcun limite massimo per il numero di termini, ma i valori elevati potrebbero influire negativamente sulle prestazioni, soprattutto se il campo con facet include un numero elevato di termini univoci.</span><span class="sxs-lookup"><span data-stu-id="eb67a-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="eb67a-859">Esempio: `facet=category,count:5` ottiene le prime cinque categorie nei risultati dell'esplorazione in base a facet.</span><span class="sxs-lookup"><span data-stu-id="eb67a-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="eb67a-860">**Nota**: se il parametro `count` è inferiore al numero di termini univoci, è possibile che i risultati non siano precisi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="eb67a-861">Ciò è dovuto al modo in cui le query di esplorazione in base a facet vengono distribuite nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="eb67a-862">Se si aumenta il valore di `count` , si ottengono conteggi di termini più precisi, ma le prestazioni possono essere ridotte.</span><span class="sxs-lookup"><span data-stu-id="eb67a-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="eb67a-863">`sort` (uno dei valori `count` per ordinare in modo *decrescente* in base al conteggio, `-count` per ordinare in modo *crescente* in base al conteggio, `value` per ordinare in modo *crescente* in base al valore o `-value` per ordinare in modo *decrescente* in base al valore)</span><span class="sxs-lookup"><span data-stu-id="eb67a-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="eb67a-864">Esempio: `facet=category,count:3,sort:count` ottiene le prime tre categorie nei risultati dell'esplorazione in base a facet in ordine decrescente secondo il numero di documenti che includono ogni nome di città.</span><span class="sxs-lookup"><span data-stu-id="eb67a-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="eb67a-865">Se le prime tre categorie sono Budget, Motel e Luxury e sono stati trovati 5 risultati per Budget, 6 per Motel e 4 per Luxury, l'ordine dei bucket sarà Motel, Budget, Luxury.</span><span class="sxs-lookup"><span data-stu-id="eb67a-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="eb67a-866">Esempio: `facet=rating,sort:-value` genera bucket per tutte le classificazioni possibili, in ordine decrescente in base al valore.</span><span class="sxs-lookup"><span data-stu-id="eb67a-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="eb67a-867">Se le classificazioni sono da 1 a 5, i bucket avranno l'ordine 5, 4, 3, 2, 1, indipendentemente dal numero di documenti corrispondenti a ogni classificazione.</span><span class="sxs-lookup"><span data-stu-id="eb67a-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="eb67a-868">`values` (valori numerici delimitati da pipe o valori `Edm.DateTimeOffset` che specificano un set dinamico di valori di immissione di facet)</span><span class="sxs-lookup"><span data-stu-id="eb67a-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="eb67a-869">Esempio: `facet=baseRate,values:10|20` genera tre bucket, uno per la tariffa di base da 0 a 10 escluso, uno da 10 a 20 escluso e uno per 20 e oltre.</span><span class="sxs-lookup"><span data-stu-id="eb67a-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="eb67a-870">Esempio: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera due bucket, uno per hotel rinnovati prima del febbraio 2010 e uno per hotel rinnovati a partire dal 1° febbraio 2010.</span><span class="sxs-lookup"><span data-stu-id="eb67a-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="eb67a-871">`interval` (intervallo di tipo Integer maggiore di 0 per i numeri o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` per i valori di tipo data/ora)</span><span class="sxs-lookup"><span data-stu-id="eb67a-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="eb67a-872">Esempio: `facet=baseRate,interval:100` genera bucket in base agli intervalli di tariffe di base con dimensioni pari a 100.</span><span class="sxs-lookup"><span data-stu-id="eb67a-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="eb67a-873">Se le tariffe di base sono tutte comprese tra € 60 e € 600, saranno presenti bucket per 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.</span><span class="sxs-lookup"><span data-stu-id="eb67a-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="eb67a-874">Esempio: `facet=lastRenovationDate,interval:year` genera un bucket per ogni anno in cui gli hotel sono stati rinnovati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="eb67a-875">`timeoffset` ([+-]hh:mm, [+-]hhmm o [+-]hh) `timeoffset` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="eb67a-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="eb67a-876">Può essere combinato solo con l'opzione `interval` e solo se applicato a un campo di tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="eb67a-877">Il valore specifica la differenza dell'ora UTC di cui tenere conto nell'impostazione dei limiti di ora.</span><span class="sxs-lookup"><span data-stu-id="eb67a-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="eb67a-878">Ad esempio, `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa il limite del giorno che inizia alle 01:00:00 UTC (mezzanotte nel fuso orario di destinazione)</span><span class="sxs-lookup"><span data-stu-id="eb67a-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="eb67a-879">**Nota**: `count` e `sort` possono essere combinati nella stessa specifica di facet, ma non possono essere combinati con `interval` o `values` e inoltre `interval` e `values` non possono essere combinati tra loro.</span><span class="sxs-lookup"><span data-stu-id="eb67a-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="eb67a-880">**Nota**: se `timeoffset` non è specificato, i facet di intervallo per data e ora vengono calcolati in base all'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="eb67a-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="eb67a-881">Ad esempio, per `facet=lastRenovationDate,interval:day`il limite del giorno inizia alle 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="eb67a-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb67a-882">Quando si chiama **Search** con POST, questo parametro è denominato `facets` invece di `facet`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="eb67a-883">Viene specificato anche come matrice di stringhe JSON, dove ogni stringa è un'espressione facet distinta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="eb67a-884">`$filter=[string]` (facoltativo): specifica un'espressione di ricerca strutturata nella sintassi standard di OData.</span><span class="sxs-lookup"><span data-stu-id="eb67a-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-885">Quando si chiama **Search** con POST, questo parametro è denominato `filter` invece di `$filter`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="eb67a-886">`highlight=[string]` (facoltativo): specifica un set di nomi di campo delimitati da virgole usati per evidenziare i risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="eb67a-887">Per l'evidenziazione dei risultati è possibile usare solo i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="eb67a-888">`highlightPreTag=[string]` (facoltativo, il valore predefinito è `<em>`): specifica un tag di stringa che viene aggiunto all'inizio delle evidenziazioni dei risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="eb67a-889">Deve essere impostato con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-890">Quando si chiama **Search** con GET, i caratteri riservati nell'URL devono essere codificati in percentuale (ad esempio %23 anziché #).</span><span class="sxs-lookup"><span data-stu-id="eb67a-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="eb67a-891">`highlightPostTag=[string]` (facoltativo, il valore predefinito è `</em>`): specifica un tag di stringa che viene aggiunto alla fine delle evidenziazioni dei risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="eb67a-892">Deve essere impostato con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-893">Quando si chiama **Search** con GET, i caratteri riservati nell'URL devono essere codificati in percentuale (ad esempio %23 anziché #).</span><span class="sxs-lookup"><span data-stu-id="eb67a-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="eb67a-894">`scoringProfile=[string]` (facoltativo): specifica il nome di un profilo di punteggio da usare per valutare i punteggi di corrispondenza per i documenti trovati, in modo da ordinare i risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="eb67a-895">`scoringParameter=[string]` (zero o più): indica i valori per ogni parametro definito in una funzione di assegnazione di punteggio, ad esempio `referencePointParameter`, con il formato `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="eb67a-896">Se ad esempio il profilo di punteggio definisce una funzione con un parametro denominato "mylocation", l'opzione della stringa di query sarà `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="eb67a-897">Il primo trattino separa il nome dall'elenco di valori, mentre il secondo fa parte del primo valore, in questo esempio la longitudine.</span><span class="sxs-lookup"><span data-stu-id="eb67a-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="eb67a-898">Per i parametri di assegnazione dei punteggi, ad esempio per tag boosting che può contenere virgole, è possibile eseguire l'escape dei valori nell'elenco usando virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="eb67a-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="eb67a-899">Se i valori stessi contengono virgolette singole è possibile eseguire l'escape raddoppiandole.</span><span class="sxs-lookup"><span data-stu-id="eb67a-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="eb67a-900">Se ad esempio è presente un parametro di tag boosting denominato "mytag" e si vuole eseguire il boosting sui valori di tag "Hello, O'Brien" e "Smith", l'opzione della stringa di query sarà `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="eb67a-901">Si noti che le virgolette sono necessarie solo per i valori che contengono virgole.</span><span class="sxs-lookup"><span data-stu-id="eb67a-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-902">Quando si chiama **Search** con POST, questo parametro è denominato `scoringParameters` invece di `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="eb67a-903">Viene specificato come matrice di stringhe JSON, dove ogni stringa è una coppia `name-values` separata.</span><span class="sxs-lookup"><span data-stu-id="eb67a-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="eb67a-904">`minimumCoverage` (facoltativo, valore predefinito pari a 100): un numero compreso tra 0 e 100 che indica la percentuale di indice che deve essere inclusa nella query di ricerca in modo che l'esecuzione di quest'ultima venga segnalata come corretta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="eb67a-905">Per impostazione predefinita, deve essere disponibile l'intero indice. In caso contrario, `Search` restituirà il codice di stato HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="eb67a-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="eb67a-906">Se si imposta `minimumCoverage` e `Search` ha esito positivo, verrà restituito HTTP 200 che include un valore `@search.coverage` nella risposta; quest'ultimo indica la percentuale dell'indice che è stata inclusa nella query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-907">L'impostazione di questo parametro su un valore inferiore a 100 può essere utile per garantire la disponibilità di ricerca anche per i servizi che dispongono di una sola replica.</span><span class="sxs-lookup"><span data-stu-id="eb67a-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="eb67a-908">Tuttavia, non si assicura che tutti i documenti corrispondenti siano presenti nei risultati di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="eb67a-909">Se la funzionalità di richiamo della ricerca è più importante rispetto a quella di disponibilità, mantenere il valore predefinito di 100 per `minimumCoverage` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="eb67a-910">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-911">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-912">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-913">Nota: per questa operazione il valore `api-version` viene specificato come parametro di query nell'URL, indipendentemente dal fatto che si chiami **Search** con GET o con POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="eb67a-914">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-914">**Request Headers**</span></span>

<span data-ttu-id="eb67a-915">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-916">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-917">È un valore stringa univoco per l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="eb67a-918">La richiesta di **ricerca** può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="eb67a-919">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-920">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-921">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-922">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-922">**Request Body**</span></span>

<span data-ttu-id="eb67a-923">Per GET: nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-923">For GET: None.</span></span>

<span data-ttu-id="eb67a-924">Per POST:</span><span class="sxs-lookup"><span data-stu-id="eb67a-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="eb67a-925">**Continuazione di risposte di ricerca parziali**</span><span class="sxs-lookup"><span data-stu-id="eb67a-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="eb67a-926">A volte Ricerca di Azure non può restituire tutti i risultati richiesti in un'unica risposta di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="eb67a-927">Ciò può verificarsi per diversi motivi, ad esempio quando la query richiede troppi documenti senza specificare `$top` o specificando un valore troppo grande per `$top`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="eb67a-928">In questi casi Ricerca di Azure includerà nel corpo della risposta l'annotazione `@odata.nextLink` e anche `@search.nextPageParameters` se si tratta di una richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="eb67a-929">È possibile usare i valori di queste annotazioni per formulare un'altra richiesta di ricerca per ottenere la parte successiva della risposta di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="eb67a-930">Tale operazione è denominata ***continuazione*** della richiesta di ricerca originale e le annotazioni vengono in genere chiamate ***token di continuazione***.</span><span class="sxs-lookup"><span data-stu-id="eb67a-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="eb67a-931">Vedere [l'esempio seguente](#SearchResponse) per informazioni dettagliate sulla sintassi di queste annotazioni e sulla posizione in cui vengono visualizzate nel corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="eb67a-932">I motivi per cui Ricerca di Azure potrebbe restituire token di continuazione sono specifici dell'implementazione e soggetti a variazioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="eb67a-933">I client affidabili devono essere sempre pronti a gestire i casi in cui viene restituito un numero di documenti inferiore al previsto e in cui viene incluso un token di continuazione per continuare il recupero dei documenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="eb67a-934">Si noti inoltre che per poter continuare è necessario usare lo stesso metodo HTTP della richiesta originale.</span><span class="sxs-lookup"><span data-stu-id="eb67a-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="eb67a-935">Se ad esempio si invia una richiesta GET, anche le richieste di continuazione inviate devono usare il metodo GET e lo stesso vale per il metodo POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="eb67a-936"><a name="SearchResponse"></a>
**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="eb67a-937">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="eb67a-938">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="eb67a-938">**Examples:**</span></span>

<span data-ttu-id="eb67a-939">È possibile trovare altri esempi nella pagina relativa alla [sintassi delle espressioni OData per Ricerca di Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="eb67a-940">Eseguire una ricerca nell'indice ordinato in modo decrescente in base alla data.</span><span class="sxs-lookup"><span data-stu-id="eb67a-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="eb67a-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="eb67a-943">In una ricerca con facet, eseguire una ricerca nell'indice e recuperare i facet per categorie, classificazioni, tag, oltre a elementi con baseRate in intervalli specifici:</span><span class="sxs-lookup"><span data-stu-id="eb67a-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="eb67a-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="eb67a-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="eb67a-946">Usando un filtro, limitare i risultati della precedente query con facet dopo che l'utente ha fatto clic su Rating 3 e sulla categoria "Motel":</span><span class="sxs-lookup"><span data-stu-id="eb67a-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="eb67a-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="eb67a-949">In una ricerca con facet, impostare un limite massimo per i termini univoci restituiti in una query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="eb67a-950">Il valore predefinito è 10, ma è possibile aumentare o ridurre questo valore usando il parametro `count` nell'attributo `facet`:</span><span class="sxs-lookup"><span data-stu-id="eb67a-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="eb67a-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="eb67a-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="eb67a-953">Eseguire una ricerca nell'indice entro campi specifici, ad esempio un campo relativo alla lingua:</span><span class="sxs-lookup"><span data-stu-id="eb67a-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="eb67a-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="eb67a-956">Eseguire una ricerca nell'indice in più campi.</span><span class="sxs-lookup"><span data-stu-id="eb67a-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="eb67a-957">Ad esempio, è possibile archiviare ed eseguire query nei campi disponibili per la ricerca in più lingue, all'interno dello stesso indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="eb67a-958">Se nello stesso documento coesistono descrizioni in inglese e in francese, sarà possibile restituirle tutte, o solo alcune, nei risultati della query:</span><span class="sxs-lookup"><span data-stu-id="eb67a-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="eb67a-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="eb67a-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="eb67a-961">Si noti che è possibile eseguire query su un solo indice alla volta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="eb67a-962">Non creare più indici per una lingua a meno che non si preveda di eseguire query su un indice alla volta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="eb67a-963">Paging: ottenere la prima pagina degli elementi (la dimensione di pagina è 10):</span><span class="sxs-lookup"><span data-stu-id="eb67a-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="eb67a-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="eb67a-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="eb67a-966">Paging: ottenere la seconda pagina degli elementi (la dimensione di pagina è 10):</span><span class="sxs-lookup"><span data-stu-id="eb67a-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="eb67a-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="eb67a-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="eb67a-969">Recuperare un set specifico di campi:</span><span class="sxs-lookup"><span data-stu-id="eb67a-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="eb67a-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="eb67a-972">Recuperare i documenti corrispondenti a un'espressione di filtro specifica:</span><span class="sxs-lookup"><span data-stu-id="eb67a-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="eb67a-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="eb67a-975">Eseguire una ricerca nell'indice e restituire frammenti con evidenziazioni dei risultati</span><span class="sxs-lookup"><span data-stu-id="eb67a-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="eb67a-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="eb67a-978">Eseguire una ricerca nell'indice e restituire documenti ordinati dal più vicino al più lontano rispetto a una posizione di riferimento</span><span class="sxs-lookup"><span data-stu-id="eb67a-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="eb67a-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="eb67a-981">Eseguire una ricerca nell'indice presupponendo che sia disponibile un profilo di punteggio denominato "geo" con due funzioni di assegnazione di punteggio in base alla distanza, che definiscono rispettivamente i parametri "currentLocation" e "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="eb67a-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="eb67a-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="eb67a-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="eb67a-984">Trovare documenti nell'indice usando una [sintassi di query semplice](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="eb67a-985">Questa query restituisce gli hotel i cui campi disponibili per la ricerca contengono i termini "comfort" e "location" ma non "motel":</span><span class="sxs-lookup"><span data-stu-id="eb67a-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="eb67a-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="eb67a-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="eb67a-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="eb67a-988">Si noti l'uso di `searchMode=all` nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="eb67a-989">Se si include questo parametro, viene eseguito l'override del valore predefinito `searchMode=any`. In questo modo, si ha la sicurezza che `-motel` significa "AND NOT" anziché "OR NOT".</span><span class="sxs-lookup"><span data-stu-id="eb67a-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="eb67a-990">Senza `searchMode=all`, si ottiene "OR NOT" che espande i risultati della ricerca anziché limitarli e questo può essere poco intuitivo per alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="eb67a-991">Trovare documenti nell'indice usando una [sintassi delle query Lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb67a-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="eb67a-992">Questa query restituisce gli hotel in cui il campo categoria contiene il termine "budget" e tutti i campi disponibili per la ricerca contengono la frase "recently renovated".</span><span class="sxs-lookup"><span data-stu-id="eb67a-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="eb67a-993">I documenti contenenti la frase "recently renovated" avranno una posizione superiore nella classifica, come risultato del valore di incremento dell'importanza di un termine (3)</span><span class="sxs-lookup"><span data-stu-id="eb67a-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="eb67a-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="eb67a-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="eb67a-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="eb67a-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="eb67a-996">Cercare un documento</span><span class="sxs-lookup"><span data-stu-id="eb67a-996">Lookup Document</span></span>
<span data-ttu-id="eb67a-997">L'operazione di **ricerca di un documento** recupera un documento da Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="eb67a-998">È utile quando un utente fa clic su un risultato della ricerca e si desidera cercare dettagli specifici su tale documento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="eb67a-999">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-999">**Request**</span></span>

<span data-ttu-id="eb67a-1000">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-1001">La richiesta di **ricerca di un documento** può essere creata nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="eb67a-1002">In alternativa, è possibile usare la sintassi tradizionale di OData per la ricerca delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="eb67a-1003">L'URI della richiesta include i valori [index name] e [key], che specificano il documento da recuperare da un determinato indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="eb67a-1004">È possibile recuperare un solo documento alla volta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1004">You can only get one document at a time.</span></span> <span data-ttu-id="eb67a-1005">Per ottenere più documenti con una singola richiesta, eseguire l'operazione di **ricerca nei documenti** .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="eb67a-1006">**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1006">**Query Parameters**</span></span>

<span data-ttu-id="eb67a-1007">`$select=[string]` (facoltativo): specifica un elenco di campi delimitati da virgole da recuperare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="eb67a-1008">Se non è specificato o se è impostato su `*`, nella proiezione vengono inclusi tutti i campi contrassegnati come recuperabili nello schema.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="eb67a-1009">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-1010">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-1011">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-1012">Nota: per questa operazione, l'elemento `api-version` è specificato come parametro di query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="eb67a-1013">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1013">**Request Headers**</span></span>

<span data-ttu-id="eb67a-1014">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-1015">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-1016">È un valore stringa univoco per l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="eb67a-1017">La **richiesta di ricerca** di un documento può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="eb67a-1018">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-1019">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-1020">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-1021">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1021">**Request Body**</span></span>

<span data-ttu-id="eb67a-1022">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1022">None.</span></span>

<span data-ttu-id="eb67a-1023">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1023">**Response**</span></span>

<span data-ttu-id="eb67a-1024">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="eb67a-1025">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1025">**Example**</span></span>

<span data-ttu-id="eb67a-1026">Cercare il documento con chiave '2':</span><span class="sxs-lookup"><span data-stu-id="eb67a-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="eb67a-1027">Cercare il documento con chiave '3' usando la sintassi di OData:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="eb67a-1028">Contare i documenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-1028">Count Documents</span></span>
<span data-ttu-id="eb67a-1029">L'operazione di **conteggio dei documenti** recupera un conteggio del numero di documenti in un indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="eb67a-1030">La sintassi `$count` fa parte del protocollo OData.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="eb67a-1031">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1031">**Request**</span></span>

<span data-ttu-id="eb67a-1032">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-1033">La richiesta di **conteggio dei documenti** può essere creata mediante il metodo GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="eb67a-1034">Il valore [index name] nell'URI della richiesta indica al servizio di restituire un conteggio di tutti gli elementi disponibili nella raccolta di documenti dell'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="eb67a-1035">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-1036">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-1037">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-1038">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1038">**Request Headers**</span></span>

<span data-ttu-id="eb67a-1039">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="eb67a-1040">`Accept`: questo valore deve essere impostato su `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="eb67a-1041">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-1042">È un valore stringa univoco per l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="eb67a-1043">La richiesta di **conteggio dei documenti** può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="eb67a-1044">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-1045">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-1046">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-1047">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1047">**Request Body**</span></span>

<span data-ttu-id="eb67a-1048">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1048">None.</span></span>

<span data-ttu-id="eb67a-1049">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1049">**Response**</span></span>

<span data-ttu-id="eb67a-1050">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="eb67a-1051">Il corpo della risposta include il valore count sotto forma di Integer formattato in testo normale.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="eb67a-1052">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="eb67a-1052">Suggestions</span></span>
<span data-ttu-id="eb67a-1053">L'operazione di recupero dei **suggerimenti** ottiene i suggerimenti in base a un input di ricerca parziale.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="eb67a-1054">In genere, viene usata nelle caselle di ricerca per fornire suggerimenti durante la digitazione quando gli utenti immettono i termini di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="eb67a-1055">Le richieste di suggerimenti hanno lo scopo di suggerire documenti di destinazione, pertanto il testo suggerito può essere ripetuto se più documenti corrispondono allo stesso input di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="eb67a-1056">È possibile usare `$select` per recuperare altri campi di documento (inclusa la chiave) in modo da poter determinare quale documento è l'origine di ogni suggerimento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="eb67a-1057">Un'operazione **Suggestions** viene generata come richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="eb67a-1058">**Quando usare POST invece di GET**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="eb67a-1059">Quando si usa HTTP GET per chiamare l'API **Suggestions** , è necessario tenere presente che la lunghezza dell'URL della richiesta non può superare 8 KB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="eb67a-1060">Di solito è sufficiente per la maggior parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="eb67a-1061">Alcune applicazioni generano tuttavia query di dimensioni molto grandi, specialmente le espressioni di filtro OData.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="eb67a-1062">Per queste applicazioni è preferibile usare HTTP POST perché consente filtri di maggiori dimensioni rispetto a GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="eb67a-1063">Con POST il fattore limitante è il numero di clausole in un filtro, non la dimensione della stringa di filtro non elaborata, poiché il limite delle dimensioni della richiesta per POST è di circa 16 MB.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1064">Anche se il limite della dimensione della richiesta POST è molto grande, le espressioni di filtro non possono essere arbitrariamente complesse.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="eb67a-1065">Per altre informazioni sulle limitazioni della complessità dei filtri vedere [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="eb67a-1066">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1066">**Request**</span></span>

<span data-ttu-id="eb67a-1067">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="eb67a-1068">La richiesta **Suggestions** può essere creata con il metodo GET o POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="eb67a-1069">L'URI della richiesta specifica il nome dell'indice su cui eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="eb67a-1070">I parametri, come il termine di ricerca immesso parzialmente, vengono specificati nella stringa di query per le richieste GET e nel corpo della richiesta nel caso di richieste POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="eb67a-1071">Come procedura consigliata per la creazione di richieste GET, usare la [codifica dell'URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) per i parametri di query specifici quando si chiama direttamente l'API REST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="eb67a-1072">Per le operazioni **Suggestions** sono inclusi i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="eb67a-1073">La codifica con URL è consigliata solo per questi parametri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="eb67a-1074">Se inavvertitamente si codifica con URL l'intera stringa della query (ossia tutti gli elementi che seguono il punto interrogativo), le richieste verranno interrotte.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="eb67a-1075">La codifica dell'URL è necessaria solo quando si chiama direttamente l'API REST con GET.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="eb67a-1076">La codifica dell'URL non è invece necessaria quando si chiama **Suggestions** con POST o quando si usa la [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx)che gestisce automaticamente la codifica dell'URL.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="eb67a-1077">**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1077">**Query Parameters**</span></span>

<span data-ttu-id="eb67a-1078">**Suggestions** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="eb67a-1079">Specificare questi parametri nella stringa di query dell'URL quando si chiama **Suggestions** con GET e come proprietà JSON nel corpo della richiesta quando si chiama **Suggestions** con POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="eb67a-1080">La sintassi per alcuni parametri è leggermente diversa tra GET e POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="eb67a-1081">Queste differenze sono riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="eb67a-1082">`search=[string]` : specifica il testo della ricerca da usare per i suggerimenti per le query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="eb67a-1083">Deve essere composto da un minimo di 1 carattere e da un massimo di 100 caratteri.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="eb67a-1084">`highlightPreTag=[string]` (facoltativo): specifica un tag di stringa che viene aggiunto all'inizio dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="eb67a-1085">Deve essere impostato con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1086">Quando si chiama **Suggestions** con GET, i caratteri riservati nell'URL devono essere codificati in percentuale, ad esempio %23 anziché #.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="eb67a-1087">`highlightPostTag=[string]` (facoltativo): specifica un tag di stringa che viene aggiunto alla fine dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="eb67a-1088">Deve essere impostato con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1089">Quando si chiama **Suggestions** con GET, i caratteri riservati nell'URL devono essere codificati in percentuale, ad esempio %23 anziché #.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="eb67a-1090">`suggesterName=[string]`: specifica il nome del componente per il suggerimento, come definito nella raccolta `suggesters` che fa parte della definizione di indice.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="eb67a-1091">Un elemento `suggester` determina i campi analizzati per i termini di query suggeriti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="eb67a-1092">Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="eb67a-1093">`fuzzy=[boolean]` (facoltativo, il valore predefinito è false): quando il valore è true, questa API trova i suggerimenti anche in caso di carattere sostituito o mancante nel testo della ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="eb67a-1094">Anche se offre un'esperienza migliore in alcuni scenari, influisce negativamente sulle prestazioni poiché le ricerche con suggerimenti fuzzy sono più lente e utilizzano più risorse.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="eb67a-1095">`searchFields=[string]` (facoltativo): specifica l'elenco di nomi di campo delimitati da virgole in cui cercare il testo specificato.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="eb67a-1096">I campi di destinazione devono essere abilitati per suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="eb67a-1097">`$top=#` (facoltativo, il valore predefinito è 5): specifica il numero di suggerimenti da recuperare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="eb67a-1098">Deve essere un numero compreso tra 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1099">Quando si chiama **Suggestions** con POST, questo parametro è denominato `top` invece di `$top`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="eb67a-1100">`$filter=[string]` (facoltativo): specifica un'espressione che filtra i documenti considerati per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1101">Quando si chiama **Suggestions** con POST, questo parametro è denominato `filter` invece di `$filter`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="eb67a-1102">`$orderby=[string]` (facoltativo): specifica un elenco di espressioni delimitate da virgole in base alle quali ordinare i risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="eb67a-1103">Ogni espressione può essere un nome campo o una chiamata alla funzione `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="eb67a-1104">Ogni espressione può essere seguita da `asc` per indicare l'ordine crescente e da `desc` per indicare l'ordine decrescente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="eb67a-1105">Per impostazione predefinita, l'ordinamento è crescente.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1105">The default is ascending order.</span></span> <span data-ttu-id="eb67a-1106">È previsto un limite di 32 clausole per `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1107">Quando si chiama **Suggestions** con POST, questo parametro è denominato `orderby` invece di `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="eb67a-1108">`$select=[string]` (facoltativo): specifica un elenco di campi delimitati da virgole da recuperare.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="eb67a-1109">Se non è specificato, vengono restituiti solo la chiave del documento e il testo del suggerimento.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="eb67a-1110">È possibile richiedere in modo esplicito tutti i campi impostando questo parametro su `*`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1111">Quando si chiama **Suggestions** con POST, questo parametro è denominato `select` invece di `$select`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="eb67a-1112">`minimumCoverage` (facoltativo, valore predefinito pari a 80): un numero compreso tra 0 e 100 che indica la percentuale di indice che deve essere inclusa nella query di suggerimento in modo che l'esecuzione di quest'ultima venga segnalata come corretta.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="eb67a-1113">Per impostazione predefinita, deve essere disponibile almeno l'80% del codice. In caso contrario, `Suggest` restituirà il codice di stato HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="eb67a-1114">Se si imposta `minimumCoverage` e `Suggest` ha esito positivo, verrà restituito HTTP 200 che include un valore `@search.coverage` nella risposta; quest'ultimo indica la percentuale dell'indice che è stata inclusa nella query.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="eb67a-1115">L'impostazione di questo parametro su un valore inferiore a 100 può essere utile per garantire la disponibilità di ricerca anche per i servizi che dispongono di una sola replica.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="eb67a-1116">Tuttavia, non si assicura che tutti i suggerimenti corrispondenti siano presenti nei risultati.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="eb67a-1117">Se la funzionalità di richiamo della ricerca è più importante rispetto a quella di disponibilità, non impostare un valore predefinito inferiore a 80 per `minimumCoverage` .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="eb67a-1118">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="eb67a-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="eb67a-1119">La versione di anteprima è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="eb67a-1120">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="eb67a-1121">Nota: per questa operazione il valore `api-version` viene specificato come parametro di query nell'URL, indipendentemente dal fatto che si chiami **Suggestions** con GET o con POST.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="eb67a-1122">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1122">**Request Headers**</span></span>

<span data-ttu-id="eb67a-1123">L'elenco seguente descrive le intestazioni della richiesta obbligatorie e facoltative.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="eb67a-1124">`api-key`: l'elemento `api-key` viene usato per autenticare la richiesta nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="eb67a-1125">È un valore stringa univoco per l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="eb67a-1126">La richiesta di recupero dei **suggerimenti** può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="eb67a-1127">Per creare l'URL della richiesta, è necessario anche il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="eb67a-1128">È possibile ottenere il nome del servizio e `api-key` dal dashboard servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="eb67a-1129">Per informazioni, vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="eb67a-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="eb67a-1130">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1130">**Request Body**</span></span>

<span data-ttu-id="eb67a-1131">Per GET: nessuno.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1131">For GET: None.</span></span>

<span data-ttu-id="eb67a-1132">Per POST:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="eb67a-1133">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1133">**Response**</span></span>

<span data-ttu-id="eb67a-1134">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="eb67a-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="eb67a-1135">Se per recuperare i campi viene usata l'opzione di proiezione, tali campi vengono inclusi in ogni elemento della matrice:</span><span class="sxs-lookup"><span data-stu-id="eb67a-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="eb67a-1136">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="eb67a-1136">**Example**</span></span>

<span data-ttu-id="eb67a-1137">Recuperare 5 suggerimenti per cui l'input di ricerca parziale è 'lux':</span><span class="sxs-lookup"><span data-stu-id="eb67a-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
