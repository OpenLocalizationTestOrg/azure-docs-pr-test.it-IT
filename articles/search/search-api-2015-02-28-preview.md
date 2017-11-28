---
title: Ricerca servizio REST API versione 2015-02-28-Preview aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="d28f6-103">API REST del servizio Ricerca di Azure: versione 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="d28f6-104">Questo articolo è la documentazione di riferimento hello per `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-105">Questa versione di anteprima estende hello in genere versione disponibile, [versione api = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornendo hello funzionalità sperimentali di seguito:</span><span class="sxs-lookup"><span data-stu-id="d28f6-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="d28f6-106">`moreLikeThis`parametro di hello query [ricerca documenti](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="d28f6-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="d28f6-107">Trova altri documenti che sono rilevanti tooanother documento specifico.</span><span class="sxs-lookup"><span data-stu-id="d28f6-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="d28f6-108">Alcune parti aggiuntive hello `2015-02-28-Preview` API REST sono documentate separatamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="d28f6-109">incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-109">These include:</span></span>

* [<span data-ttu-id="d28f6-110">Profili di punteggio</span><span class="sxs-lookup"><span data-stu-id="d28f6-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="d28f6-111">Indicizzatori</span><span class="sxs-lookup"><span data-stu-id="d28f6-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="d28f6-112">Ricerca di Azure è disponibile in più versioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="d28f6-113">Consultare troppo[controllo delle versioni del servizio di ricerca](http://msdn.microsoft.com/library/azure/dn864560.aspx) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d28f6-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="d28f6-114">API in questo documento</span><span class="sxs-lookup"><span data-stu-id="d28f6-114">APIs in this document</span></span>
<span data-ttu-id="d28f6-115">L'API del servizio Ricerca di Azure supporta due sintassi di URL per le operazioni dell'API, ovvero semplice e OData. Per informazioni dettagliate, vedere [Supporto per OData (Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="d28f6-116">Hello elenco seguente mostra la sintassi semplice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="d28f6-117">Creare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-118">Aggiornare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-119">Ottenere un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-120">Elencare gli indici</span><span class="sxs-lookup"><span data-stu-id="d28f6-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-121">Ottenere le statistiche di un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-122">Analizzatore di test</span><span class="sxs-lookup"><span data-stu-id="d28f6-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-123">Eliminare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-124">Aggiungere, aggiornare o eliminare documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-125">Eseguire ricerche nei documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-126">Cercare un documento</span><span class="sxs-lookup"><span data-stu-id="d28f6-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="d28f6-127">Contare i documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="d28f6-128">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="d28f6-129">Operazioni sugli indici</span><span class="sxs-lookup"><span data-stu-id="d28f6-129">Index Operations</span></span>
<span data-ttu-id="d28f6-130">È possibile creare e gestire gli indici in Ricerca di Azure tramite semplici richieste HTTP (POST, GET, PUT, DELETE) su una risorsa indice specifica.</span><span class="sxs-lookup"><span data-stu-id="d28f6-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="d28f6-131">toocreate un indice, è innanzitutto registrare un documento JSON che descrive hello schema di indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="d28f6-132">schema di Hello definisce i campi di hello di indice hello, i tipi di dati e come possono essere utilizzati (ad esempio, nelle ricerche full-text, filtri, ordinamento o facet).</span><span class="sxs-lookup"><span data-stu-id="d28f6-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="d28f6-133">Definisce inoltre i profili di punteggio, suggerimento e altri comportamenti di hello tooconfigure gli attributi dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="d28f6-134">Hello esempio seguente viene illustrato uno schema utilizzato per la ricerca di informazioni sugli alberghi con il campo di descrizione hello definito in due lingue.</span><span class="sxs-lookup"><span data-stu-id="d28f6-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="d28f6-135">Si noti come gli attributi controllino come campo hello è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="d28f6-136">Ad esempio hello `hotelId` viene utilizzata come chiave di documento hello (`"key": true`) e viene escluso dalla ricerca full-text (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="d28f6-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="d28f6-137">Dopo aver creato l'indice di hello, caricare documenti che popolano indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="d28f6-138">Per questo passaggio successivo, vedere [Aggiungere, aggiornare o eliminare documenti](#AddOrUpdateDocuments) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="d28f6-139">Per un video di introduzione tooindexing in ricerca di Azure, vedere hello [Channel 9 Cloud Cover, episodio in ricerca di Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="d28f6-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="d28f6-140">Creare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-140">Create Index</span></span>
<span data-ttu-id="d28f6-141">Un indice è hello mezzo principale per organizzare e cercare documenti in ricerca di Azure, simile toohow una tabella organizza i record in un database.</span><span class="sxs-lookup"><span data-stu-id="d28f6-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="d28f6-142">Ogni indice sono una raccolta di documenti tutti conformi toohello schema di indice (nomi di campo, i tipi di dati e proprietà) che gli indici specificano anche costrutti aggiuntivi (suggerimento, profili di punteggio e le opzioni CORS) che definiscono altri comportamenti di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="d28f6-143">È possibile creare un nuovo indice in Ricerca di Azure mediante una richiesta HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="d28f6-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="d28f6-144">il corpo di Hello della richiesta di hello è uno schema JSON che specifica le informazioni di indice e la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d28f6-145">In alternativa, è possibile usare PUT e specificare il nome di indice hello in hello URI.</span><span class="sxs-lookup"><span data-stu-id="d28f6-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="d28f6-146">Se non esiste alcun indice hello, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="d28f6-147">Creazione di un indice determina la struttura di hello di hello documenti archiviati e utilizzati nelle operazioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="d28f6-148">Il popolamento dell'indice hello è un'operazione separata.</span><span class="sxs-lookup"><span data-stu-id="d28f6-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="d28f6-149">Per questo passaggio, è possibile usare un [indicizzatore](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponibile per le origini dati supportate) o un'[operazione di aggiunta, aggiornamento o eliminazione di documenti](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="d28f6-150">indice invertito Hello viene generato quando i documenti hello vengono registrati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="d28f6-151">**Nota**: numero massimo di hello di indici consentito varia in base al livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="d28f6-152">servizio gratuito Hello consente backup too3 indici.</span><span class="sxs-lookup"><span data-stu-id="d28f6-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="d28f6-153">Nel servizio standard sono consentiti 50 indici per servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="d28f6-154">Per dettagli, vedere [Limitazioni e vincoli](http://msdn.microsoft.com/library/azure/dn798934.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="d28f6-155">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-155">**Request**</span></span>

<span data-ttu-id="d28f6-156">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d28f6-157">Hello **Create Index** richiesta può essere costruita utilizzando un metodo POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="d28f6-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="d28f6-158">Quando si usa POST, è necessario fornire un nome di indice nel corpo di richiesta hello insieme definizione dello schema di indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="d28f6-159">Con PUT, il nome dell'indice hello fa parte dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="d28f6-160">Se l'indice di hello non esiste, viene creato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="d28f6-161">Se esiste già, è aggiornato toohello nuova definizione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="d28f6-162">Nome indice Hello deve essere minuscola, iniziare con una lettera o un numero, avere senza barre o punti e minore di 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="d28f6-163">Dopo avere avviato il nome dell'indice hello con una lettera o un numero, il resto di hello del nome hello può includere qualsiasi lettera, numero e trattino, purché hello trattini non siano consecutivi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="d28f6-164">Hello `api-version` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-164">hello `api-version` is required.</span></span> <span data-ttu-id="d28f6-165">Per un elenco delle versioni disponibili, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="d28f6-166">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-166">**Request Headers**</span></span>

<span data-ttu-id="d28f6-167">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-168">`Content-Type`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-168">`Content-Type`: Required.</span></span> <span data-ttu-id="d28f6-169">Impostare questa proprietà troppo`application/json`</span><span class="sxs-lookup"><span data-stu-id="d28f6-169">Set this too`application/json`</span></span>
* <span data-ttu-id="d28f6-170">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-170">`api-key`: Required.</span></span> <span data-ttu-id="d28f6-171">Hello `api-key` viene utilizzato per</span><span class="sxs-lookup"><span data-stu-id="d28f6-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="d28f6-172">eseguire l'autenticazione del servizio di ricerca di hello richiesta tooyour.</span><span class="sxs-lookup"><span data-stu-id="d28f6-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-173">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-174">Hello **Create Index** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-175">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-176">È possibile ottenere nome servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-177">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-178"><a name="RequestData"></a>
**Sintassi del corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="d28f6-179">Hello corpo della richiesta di hello contiene una definizione di schema, che include l'elenco di hello dei campi di dati all'interno di documenti che verranno inseriti nell'indice, gli attributi, tipi di dati, nonché un elenco facoltativo di profili di punteggio è utilizzati tooscore documenti in corrispondenza ora di query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="d28f6-180">Si noti che per una richiesta POST, è necessario specificare il nome dell'indice hello nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="d28f6-181">Può esistere solo un campo chiave nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="d28f6-182">Toobe presenta un campo stringa.</span><span class="sxs-lookup"><span data-stu-id="d28f6-182">It has toobe a string field.</span></span> <span data-ttu-id="d28f6-183">Questo campo rappresenta l'identificatore univoco di hello per ogni documento archiviato all'interno dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="d28f6-184">le parti principali di un indice Hello includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="d28f6-185">`fields` : elementi che verranno inseriti nell'indice, tra cui il nome, il tipo di dati e le proprietà che definiscono le azioni consentite.</span><span class="sxs-lookup"><span data-stu-id="d28f6-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="d28f6-186">`suggesters` : elementi usati per le query con completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="d28f6-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="d28f6-187">`scoringProfiles` :elementi usati per la classificazione personalizzata dei punteggi di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="d28f6-188">Per informazioni dettagliate, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="d28f6-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilizzato toodefine come documenti/query sono suddivisi in token indicizzabile o disponibile per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="d28f6-190">Per i dettagli, vedere la pagina relativa all' [analisi in Ricerca di Azure](https://aka.ms//azsanalysis) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="d28f6-191">`defaultScoringProfile`Utilizzare i comportamenti di punteggio predefinito di toooverwrite hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="d28f6-192">`corsOptions`tooallow le query sull'indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="d28f6-193">sintassi di Hello per la struttura di payload della richiesta hello è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d28f6-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="d28f6-194">Più avanti in questo argomento è riportata una richiesta di esempio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="d28f6-195">**Attributi dell'indice**</span><span class="sxs-lookup"><span data-stu-id="d28f6-195">**Index Attributes**</span></span>

<span data-ttu-id="d28f6-196">Hello attributi seguenti possono essere impostati durante la creazione di un indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="d28f6-197">Per informazioni dettagliate sull'assegnazione dei punteggi e sui profili di punteggio, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="d28f6-198">`name`-Set hello nome del campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="d28f6-199">`type`-Set hello il tipo di dati per il campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="d28f6-200">`searchable`-Hello campo viene contrassegnato come full-text in grado di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="d28f6-201">Ciò significa che verrà sottoposto ad analisi, ad esempio la suddivisione in parole durante l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="d28f6-202">Se si imposta un `searchable` tooa valore del campo come "sunny day", internamente verrà suddiviso in singoli token hello "sunny" e "giorno".</span><span class="sxs-lookup"><span data-stu-id="d28f6-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="d28f6-203">È così possibile eseguire ricerche full-text di questi termini.</span><span class="sxs-lookup"><span data-stu-id="d28f6-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="d28f6-204">I campi di tipo `Edm.String` o `Collection(Edm.String)` sono `searchable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d28f6-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="d28f6-205">I campi di altri tipi non possono essere `searchable`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="d28f6-206">**Nota**: `searchable` campi utilizzano spazio aggiuntivo nell'indice poiché ricerca di Azure memorizzerà una versione in formato token aggiuntiva di valore del campo hello per le ricerche full-text.</span><span class="sxs-lookup"><span data-stu-id="d28f6-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="d28f6-207">Se si desidera che lo spazio toosave l'indice e non devono essere toobe un campo inclusi nella ricerca, impostare `searchable` troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="d28f6-208">`filterable`-Consente di hello toobe di campo a cui fa riferimento `$filter` query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="d28f6-209">`filterable` è diverso da `searchable` nella modalità di gestione delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="d28f6-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="d28f6-210">I campi di tipo `Edm.String` o `Collection(Edm.String)` che sono `filterable` non sono sottoposti a suddivisione delle parole e quindi i confronti riguardano solo le corrispondenze esatte.</span><span class="sxs-lookup"><span data-stu-id="d28f6-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="d28f6-211">Ad esempio, se si imposta tale campo `f` troppo "sunny day" `$filter=f eq 'sunny'` troverà alcuna corrispondenza, ma `$filter=f eq 'sunny day'` verrà.</span><span class="sxs-lookup"><span data-stu-id="d28f6-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="d28f6-212">Tutti i campi sono `filterable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d28f6-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="d28f6-213">`sortable`-Per impostazione predefinita sistema hello Ordina risultati in base al punteggio, ma in molti casi gli utenti verranno toosort dai campi nei documenti di hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="d28f6-214">I campi di tipo `Collection(Edm.String)` non possono essere `sortable`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="d28f6-215">Tutti gli altri campi sono `sortable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d28f6-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="d28f6-216">`facetable`: usato generalmente in una presentazione dei risultati di ricerca che include il numero di risultati per categoria (ad esempio, per cercare fotocamere digitali e visualizzare i risultati in base alla marca, ai megapixel, al prezzo e così via).</span><span class="sxs-lookup"><span data-stu-id="d28f6-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="d28f6-217">Questa opzione non può essere usata con i campi di tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="d28f6-218">Tutti gli altri campi sono `facetable` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d28f6-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="d28f6-219">**Nota**: i campi di tipo `Edm.String` che sono `filterable`, `sortable` o `facetable` possono avere al massimo una lunghezza di 32 KB.</span><span class="sxs-lookup"><span data-stu-id="d28f6-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="d28f6-220">In questo modo tali campi sono considerati un unico termine di ricerca e lunghezza massima di hello di un termine in ricerca di Azure è 32KB.</span><span class="sxs-lookup"><span data-stu-id="d28f6-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="d28f6-221">Se è necessario toostore più testo in un campo stringa singola, sarà necessario tooexplicitly impostare `filterable`, `sortable`, e `facetable` troppo`false` nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="d28f6-222">**Nota**: se un campo include nessuno dei precedente hello gli attributi impostati troppo`true` (`searchable`, `filterable`, `sortable`, o`facetable`) campo hello viene effettivamente isolato dall'indice invertito hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="d28f6-223">Questa opzione è utile per i campi che non vengono usati nelle query, ma che sono necessari nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="d28f6-224">Esclusione di tali campi dall'indice hello migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="d28f6-225">`key`-Contrassegni hello campo come contenente identificatori univoci per i documenti all'interno dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="d28f6-226">Un solo campo deve essere scelto come hello `key` campo e deve essere di tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="d28f6-227">I campi chiavi possono essere utilizzati toolook i documenti direttamente tramite hello [API di ricerca](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="d28f6-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="d28f6-228">`retrievable`-Imposta se il campo hello può essere restituito nei risultati di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="d28f6-229">Ciò è utile quando si vuole toouse un campo (ad esempio margine) come un filtro, ordinamento o punteggio meccanismo, ma non si desidera l'utente finale di hello campo toobe toohello visibile.</span><span class="sxs-lookup"><span data-stu-id="d28f6-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="d28f6-230">L'attributo deve essere `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="d28f6-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="d28f6-231">`analyzer`-Set hello Nome hello analyzer toouse per il campo hello in fase di indicizzazione e ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="d28f6-232">Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d28f6-233">Questa opzione può essere usata solo con campi `searchable` e non può essere impostata con `searchAnalyzer` o `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="d28f6-234">Una volta hello scelto, non può essere modificato per il campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="d28f6-235">`searchAnalyzer`-Set hello nome dell'analizzatore di hello utilizzato in fase di ricerca per il campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="d28f6-236">Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d28f6-237">Questa opzione può essere usata solo con i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="d28f6-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="d28f6-238">Deve essere impostato insieme a `indexAnalyzer` e non può essere impostato insieme a hello `analyzer` opzione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="d28f6-239">Questo analizzatore può essere aggiornato per un campo esistente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="d28f6-240">`indexAnalyzer`-Set hello nome dell'analizzatore di hello utilizzato in fase di indicizzazione per il campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="d28f6-241">Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d28f6-242">Questa opzione può essere usata solo con i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="d28f6-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="d28f6-243">Deve essere impostato insieme a `searchAnalyzer` e non può essere impostato insieme a hello `analyzer` opzione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="d28f6-244">Una volta hello scelto, non può essere modificato per il campo hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="d28f6-245">`suggesters`-Set hello in modalità di ricerca e campi che sono hello origine di contenuto hello per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="d28f6-246">Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="d28f6-247">`scoringProfiles` : definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati più in alto nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="d28f6-248">I profili di punteggio sono costituiti da funzioni e campi ponderati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="d28f6-249">Vedere [aggiungere i profili di punteggio](https://msdn.microsoft.com/library/azure/dn798928.aspx) per ulteriori informazioni sugli attributi hello utilizzato in un profilo di punteggio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="d28f6-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Supporto per le lingue**</span><span class="sxs-lookup"><span data-stu-id="d28f6-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="d28f6-251">I campi disponibili per la ricerca vengono sottoposti a un processo di analisi, che spesso comporta la suddivisione in parole, la normalizzazione del testo e l'esclusione di termini tramite filtro.</span><span class="sxs-lookup"><span data-stu-id="d28f6-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="d28f6-252">Per impostazione predefinita, i campi ricercabili in ricerca di Azure vengono analizzati con hello [analizzatore Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) che suddivide il testo in elementi di["Segmentazione di testo Unicode"](http://unicode.org/reports/tr29/) regole.</span><span class="sxs-lookup"><span data-stu-id="d28f6-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="d28f6-253">Inoltre, analizzatore standard hello converte tutti i form di lettere minuscole tootheir caratteri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="d28f6-254">I documenti indicizzati e i termini di ricerca passano tramite l'analisi di hello durante l'indicizzazione e l'elaborazione delle query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="d28f6-255">Ricerca di Azure supporta una varietà di linguaggi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="d28f6-256">Ogni lingua richiede un analizzatore di testo non standard che tenga conto delle caratteristiche specifiche della lingua.</span><span class="sxs-lookup"><span data-stu-id="d28f6-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="d28f6-257">Ricerca di Azure offre due tipi di analizzatori:</span><span class="sxs-lookup"><span data-stu-id="d28f6-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="d28f6-258">35 sono basati sulla tecnologia Lucene.</span><span class="sxs-lookup"><span data-stu-id="d28f6-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="d28f6-259">50 sono basati sulla tecnologia proprietaria di Microsoft per l'elaborazione del linguaggio naturale usata in Office e Bing.</span><span class="sxs-lookup"><span data-stu-id="d28f6-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="d28f6-260">Alcuni sviluppatori preferiscono hello Lucene soluzione open source, semplice e più familiare.</span><span class="sxs-lookup"><span data-stu-id="d28f6-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="d28f6-261">Gli analizzatori Lucene sono più veloci, ma gli analizzatori Microsoft hello dispone di funzionalità avanzate, ad esempio lemmatizzazione, decompounding (in linguaggi come il tedesco, danese, olandese, svedese, norvegese, estone, fine, ungherese, slovacco) e il riconoscimento di entità (URL di word messaggi di posta elettronica, date, numeri).</span><span class="sxs-lookup"><span data-stu-id="d28f6-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="d28f6-262">Se possibile, è necessario eseguire i confronti di entrambi hello Microsoft e Lucene analizzatori toodecide cui uno è una soluzione migliore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="d28f6-263">***Analizzatori a confronto***</span><span class="sxs-lookup"><span data-stu-id="d28f6-263">***How they compare***</span></span>

<span data-ttu-id="d28f6-264">analizzatore Lucene Hello per la lingua inglese estende l'analizzatore standard hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="d28f6-265">Rimuove il genitivo sassone (la 's finale) dalle parole, applica lo stemming in base all'[algoritmo Porter Stemming](http://tartarus.org/~martin/PorterStemmer/) e rimuove le parole [non significative](http://en.wikipedia.org/wiki/Stop_words) per la lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="d28f6-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="d28f6-266">In confronto, analizzatore Microsoft hello esegue lemmatizzazione anziché lo stemming.</span><span class="sxs-lookup"><span data-stu-id="d28f6-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="d28f6-267">Significa che è possibile gestire le forme lessicali flesse e irregolari in modo decisamente migliore, producendo risultati di ricerca più rilevanti. Guardare il modulo 7 della [presentazione di Ricerca di Azure MVA](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="d28f6-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="d28f6-268">L'indicizzazione con gli analizzatori Microsoft Media è due volte toothree inferiore equivalenti Lucene, a seconda del linguaggio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="d28f6-269">Le prestazioni della ricerca non devono essere influenzate in modo significativo per le query di dimensioni medie.</span><span class="sxs-lookup"><span data-stu-id="d28f6-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="d28f6-270">***Configurazione***</span><span class="sxs-lookup"><span data-stu-id="d28f6-270">***Configuration***</span></span>

<span data-ttu-id="d28f6-271">Per ogni campo nella definizione dell'indice hello, è possibile impostare hello `analyzer` nome analizzatore tooan della proprietà che specifica la lingua e fornitore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="d28f6-272">Hello analyzer stesso verranno applicate quando l'indicizzazione e ricerca per tale campo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="d28f6-273">Ad esempio, è possibile avere campi separati per inglese, francese e spagnola descrizioni di hotel side-by-side in hello stesso indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="d28f6-274">Hello utilizzare [parametro query 'searchFields'](#SearchQueryParameters) toospecify toosearch quale campo specifico della lingua base nelle query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="d28f6-275">È possibile esaminare gli esempi di query che includono hello `analyzer` proprietà [ricerca documenti](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="d28f6-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="d28f6-276">***Elenco di analizzatori***</span><span class="sxs-lookup"><span data-stu-id="d28f6-276">***Analyzer list***</span></span>

<span data-ttu-id="d28f6-277">Di seguito è elenco hello delle lingue supportate con i nomi di Analizzatore Lucene e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d28f6-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="d28f6-278">Lingua</span><span class="sxs-lookup"><span data-stu-id="d28f6-278">Language</span></span></th>
        <th><span data-ttu-id="d28f6-279">Nome analizzatore Microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="d28f6-280">Nome analizzatore Lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-281">Arabo</span><span class="sxs-lookup"><span data-stu-id="d28f6-281">Arabic</span></span></td>
        <td><span data-ttu-id="d28f6-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-284">Armeno</span><span class="sxs-lookup"><span data-stu-id="d28f6-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="d28f6-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="d28f6-286">Bengalese</span><span class="sxs-lookup"><span data-stu-id="d28f6-286">Bangla</span></span></td>
        <td><span data-ttu-id="d28f6-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="d28f6-288">Basco</span><span class="sxs-lookup"><span data-stu-id="d28f6-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="d28f6-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="d28f6-290">Bulgaro</span><span class="sxs-lookup"><span data-stu-id="d28f6-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="d28f6-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="d28f6-293">Catalano</span><span class="sxs-lookup"><span data-stu-id="d28f6-293">Catalan</span></span></td>
        <td><span data-ttu-id="d28f6-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="d28f6-296">Cinese semplificato</span><span class="sxs-lookup"><span data-stu-id="d28f6-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="d28f6-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-299">Cinese tradizionale</span><span class="sxs-lookup"><span data-stu-id="d28f6-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="d28f6-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="d28f6-302">Croato</span><span class="sxs-lookup"><span data-stu-id="d28f6-302">Croatian</span></span></td>
        <td><span data-ttu-id="d28f6-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-304">Ceco</span><span class="sxs-lookup"><span data-stu-id="d28f6-304">Czech</span></span></td>
        <td><span data-ttu-id="d28f6-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d28f6-307">Danese</span><span class="sxs-lookup"><span data-stu-id="d28f6-307">Danish</span></span></td>
        <td><span data-ttu-id="d28f6-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d28f6-310">Olandese</span><span class="sxs-lookup"><span data-stu-id="d28f6-310">Dutch</span></span></td>
        <td><span data-ttu-id="d28f6-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="d28f6-313">Inglese</span><span class="sxs-lookup"><span data-stu-id="d28f6-313">English</span></span></td>        
        <td><span data-ttu-id="d28f6-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-316">Estone</span><span class="sxs-lookup"><span data-stu-id="d28f6-316">Estonian</span></span></td>
        <td><span data-ttu-id="d28f6-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-318">Finlandese</span><span class="sxs-lookup"><span data-stu-id="d28f6-318">Finnish</span></span></td>
        <td><span data-ttu-id="d28f6-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d28f6-321">Francese</span><span class="sxs-lookup"><span data-stu-id="d28f6-321">French</span></span></td>
        <td><span data-ttu-id="d28f6-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-324">Gallego</span><span class="sxs-lookup"><span data-stu-id="d28f6-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="d28f6-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="d28f6-326">Tedesco</span><span class="sxs-lookup"><span data-stu-id="d28f6-326">German</span></span></td>
        <td><span data-ttu-id="d28f6-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-329">Greco</span><span class="sxs-lookup"><span data-stu-id="d28f6-329">Greek</span></span></td>
        <td><span data-ttu-id="d28f6-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="d28f6-332">Gujarati</span></span></td>
        <td><span data-ttu-id="d28f6-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-334">Ebraico</span><span class="sxs-lookup"><span data-stu-id="d28f6-334">Hebrew</span></span></td>
        <td><span data-ttu-id="d28f6-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="d28f6-336">Hindi</span></span></td>
        <td><span data-ttu-id="d28f6-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-339">Ungherese</span><span class="sxs-lookup"><span data-stu-id="d28f6-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="d28f6-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-342">Islandese</span><span class="sxs-lookup"><span data-stu-id="d28f6-342">Icelandic</span></span></td>
        <td><span data-ttu-id="d28f6-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-344">Indonesiano (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="d28f6-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="d28f6-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-347">Irlandese</span><span class="sxs-lookup"><span data-stu-id="d28f6-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="d28f6-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="d28f6-349">Italian</span></span></td>
        <td><span data-ttu-id="d28f6-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-352">Giapponese</span><span class="sxs-lookup"><span data-stu-id="d28f6-352">Japanese</span></span></td>
        <td><span data-ttu-id="d28f6-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="d28f6-355">Kannada</span></span></td>
        <td><span data-ttu-id="d28f6-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="d28f6-357">Korean</span></span></td>
        <td><span data-ttu-id="d28f6-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-360">Lettone</span><span class="sxs-lookup"><span data-stu-id="d28f6-360">Latvian</span></span></td>        
        <td><span data-ttu-id="d28f6-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="d28f6-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="d28f6-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="d28f6-365">Malayalam</span></span></td>
        <td><span data-ttu-id="d28f6-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-367">Malese (alfabeto latino)</span><span class="sxs-lookup"><span data-stu-id="d28f6-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="d28f6-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="d28f6-369">Marathi</span></span></td>
        <td><span data-ttu-id="d28f6-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-371">Norvegese</span><span class="sxs-lookup"><span data-stu-id="d28f6-371">Norwegian</span></span></td>
        <td><span data-ttu-id="d28f6-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="d28f6-374">Persiano</span><span class="sxs-lookup"><span data-stu-id="d28f6-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="d28f6-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="d28f6-376">Polacco</span><span class="sxs-lookup"><span data-stu-id="d28f6-376">Polish</span></span></td>
        <td><span data-ttu-id="d28f6-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-379">Portoghese (Brasile)</span><span class="sxs-lookup"><span data-stu-id="d28f6-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="d28f6-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-382">Portoghese (Portogallo)</span><span class="sxs-lookup"><span data-stu-id="d28f6-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="d28f6-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="d28f6-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="d28f6-385">Punjabi</span></span></td>
        <td><span data-ttu-id="d28f6-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-387">Romeno</span><span class="sxs-lookup"><span data-stu-id="d28f6-387">Romanian</span></span></td>
        <td><span data-ttu-id="d28f6-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-390">Russo</span><span class="sxs-lookup"><span data-stu-id="d28f6-390">Russian</span></span></td>
        <td><span data-ttu-id="d28f6-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-393">Serbo (alfabeto cirillico)</span><span class="sxs-lookup"><span data-stu-id="d28f6-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="d28f6-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-395">Serbo (alfabeto latino)</span><span class="sxs-lookup"><span data-stu-id="d28f6-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="d28f6-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-397">Slovacco</span><span class="sxs-lookup"><span data-stu-id="d28f6-397">Slovak</span></span></td>
        <td><span data-ttu-id="d28f6-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-399">Sloveno</span><span class="sxs-lookup"><span data-stu-id="d28f6-399">Slovenian</span></span></td>
        <td><span data-ttu-id="d28f6-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-401">Spagnolo</span><span class="sxs-lookup"><span data-stu-id="d28f6-401">Spanish</span></span></td>
        <td><span data-ttu-id="d28f6-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-404">Svedese</span><span class="sxs-lookup"><span data-stu-id="d28f6-404">Swedish</span></span></td>
        <td><span data-ttu-id="d28f6-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="d28f6-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="d28f6-407">Tamil</span></span></td>
        <td><span data-ttu-id="d28f6-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="d28f6-409">Telugu</span></span></td>
        <td><span data-ttu-id="d28f6-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-411">Thai</span><span class="sxs-lookup"><span data-stu-id="d28f6-411">Thai</span></span></td>
        <td><span data-ttu-id="d28f6-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-414">Turco</span><span class="sxs-lookup"><span data-stu-id="d28f6-414">Turkish</span></span></td>
        <td><span data-ttu-id="d28f6-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="d28f6-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-417">Ucraino</span><span class="sxs-lookup"><span data-stu-id="d28f6-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="d28f6-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="d28f6-419">Urdu</span></span></td>
        <td><span data-ttu-id="d28f6-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="d28f6-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="d28f6-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d28f6-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="d28f6-423">Ricerca di Azure fornisce inoltre configurazioni dell'analizzatore indipendenti dalla lingua</span><span class="sxs-lookup"><span data-stu-id="d28f6-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="d28f6-424">Riduzione ASCII standard</span><span class="sxs-lookup"><span data-stu-id="d28f6-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="d28f6-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="d28f6-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="d28f6-426">Segmentazione di testo Unicode (tokenizer standard)</span><span class="sxs-lookup"><span data-stu-id="d28f6-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="d28f6-427">Filtro di riduzione ASCII - converte i caratteri Unicode che non appartengono al set di toohello dei primi 127 caratteri ASCII nei rispettivi equivalenti ASCII.</span><span class="sxs-lookup"><span data-stu-id="d28f6-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="d28f6-428">Questo filtro è utile per la rimozione dei segni diacritici.</span><span class="sxs-lookup"><span data-stu-id="d28f6-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="d28f6-429">Tutti gli analizzatori con nomi contenenti la parola <i>lucene</i> sono basati sugli [analizzatori di lingua Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="d28f6-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="d28f6-430">Sono disponibili ulteriori informazioni sul filtro di riduzione ASCII di hello [qui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="d28f6-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="d28f6-431">**Componenti per il suggerimento**</span><span class="sxs-lookup"><span data-stu-id="d28f6-431">**Suggesters**</span></span>

<span data-ttu-id="d28f6-432">Oggetto `suggester` definisce i campi in un indice vengono utilizzati toosupport completamento automatico nelle ricerche.</span><span class="sxs-lookup"><span data-stu-id="d28f6-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="d28f6-433">In genere stringhe di ricerca parziali vengono inviate toohello [API suggerimenti](#Suggestions) hello utente digita una query di ricerca, mentre hello API restituisce un set di frasi suggerite.</span><span class="sxs-lookup"><span data-stu-id="d28f6-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="d28f6-434">Un strumento suggerimenti definite nell'indice hello determina quali campi sono termini di ricerca della digitazione di hello toobuild utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="d28f6-435">Per visualizzare i dettagli sulla configurazione, consultare [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="d28f6-436">**Profili di punteggio**</span><span class="sxs-lookup"><span data-stu-id="d28f6-436">**Scoring profiles**</span></span>

<span data-ttu-id="d28f6-437">Oggetto `scoringProfile` definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati nei risultati della ricerca hello superiore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="d28f6-438">I profili di punteggio sono costituiti da funzioni e campi ponderati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="d28f6-439">toouse loro, si specifica un profilo in base al nome nella stringa di query hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="d28f6-440">Un profilo di punteggio predefinito agisce dietro hello scene toocompute un punteggio di ricerca per ogni elemento in un set di risultati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="d28f6-441">È possibile utilizzare hello interne e senza nome, il profilo di punteggio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="d28f6-442">In alternativa, impostare `defaultScoringProfile` toouse un profilo personalizzato come valore predefinito di hello, viene richiamato ogni qualvolta un profilo personalizzato non è specificato nella stringa di query hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="d28f6-443">Vedere [tooa indice di ricerca (ricerca di Azure del servizio API REST) i profili di punteggio Aggiungi](search-api-scoring-profiles-2015-02-28-preview.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d28f6-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="d28f6-444">**Opzioni CORS**</span><span class="sxs-lookup"><span data-stu-id="d28f6-444">**CORS Options**</span></span>

<span data-ttu-id="d28f6-445">Javascript sul lato client non è possibile chiamare le API per impostazione predefinita poiché browser hello impedirà tutte le richieste cross-origin.</span><span class="sxs-lookup"><span data-stu-id="d28f6-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="d28f6-446">Per abilitare CORS (Cross-Origin Resource Sharing) impostando hello `corsOptions` indice tooyour query multiorigine tooallow di attributo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="d28f6-447">Si noti che, per motivi di sicurezza, solo le API di query supportano CORS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="d28f6-448">è possibile impostare per CORS Hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="d28f6-449">`allowedOrigins`(obbligatorio): si tratta di un elenco di origini che verrà concesso l'indice tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="d28f6-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="d28f6-450">Ciò significa che il codice Javascript servito da queste origini sarà consentito tooquery indice (presupponendo che venga fornita la chiave API corretta hello).</span><span class="sxs-lookup"><span data-stu-id="d28f6-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="d28f6-451">Ogni origine è in genere formato hello `protocol://fully-qualified-domain-name:port` Sebbene hello porta viene spesso omessa.</span><span class="sxs-lookup"><span data-stu-id="d28f6-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="d28f6-452">Per altri dettagli, vedere [questo articolo](http://go.microsoft.com/fwlink/?LinkId=330822) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="d28f6-453">Se si desidera tooallow le entità Origin tooall di accesso, includere `*` come un singolo elemento hello `allowedOrigins` matrice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="d28f6-454">Tenere presente che **questa non è la procedura consigliata per i servizi di ricerca di produzione.**</span><span class="sxs-lookup"><span data-stu-id="d28f6-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="d28f6-455">Può comunque essere utile per finalità di sviluppo o debug.</span><span class="sxs-lookup"><span data-stu-id="d28f6-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="d28f6-456">`maxAgeInSeconds`(facoltativo): i browser usano questo valore toodetermine hello durata (in secondi) toocache delle risposte preliminari CORS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="d28f6-457">Questo valore deve essere un intero non negativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-457">This must be a non-negative integer.</span></span> <span data-ttu-id="d28f6-458">Questo valore è, prestazioni migliori hello Hello più grande, ma hello più tempo che richiederà per effetto di tootake modifiche dei criteri CORS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="d28f6-459">Se questo valore non è impostato, viene usata una durata predefinita di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="d28f6-460"><a name="CreateUpdateIndexExample"></a>
**Esempio di corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="d28f6-461">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-461">**Response**</span></span>

<span data-ttu-id="d28f6-462">Per una richiesta con esito positivo: "201 Creato".</span><span class="sxs-lookup"><span data-stu-id="d28f6-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="d28f6-463">Per impostazione predefinita il corpo della risposta hello conterrà hello JSON per la definizione dell'indice hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="d28f6-464">Se hello `Prefer` intestazione della richiesta è troppo`return=minimal`, hello corpo della risposta sarà vuoto e codice di stato hello esito positivo sarà "204 Nessun contenuto" invece di "201 creato".</span><span class="sxs-lookup"><span data-stu-id="d28f6-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="d28f6-465">Questo vale indipendentemente dal fatto se PUT o POST è indice di hello toocreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="d28f6-466">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="d28f6-466">**Remarks**</span></span>

<span data-ttu-id="d28f6-467">Attualmente è previsto un supporto limitato per gli aggiornamenti dello schema di indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="d28f6-468">Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="d28f6-469">Sebbene i campi esistenti non possono essere modificati o eliminati, è possano aggiungere nuovi campi tooan di indice esistente in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="d28f6-470">Quando viene aggiunto un nuovo campo, tutti i documenti esistenti nell'indice hello avranno automaticamente un valore null per tale campo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="d28f6-471">Nessun ulteriore spazio di archiviazione verrà utilizzato fino a quando non verranno aggiunti toohello indice nuovi documenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="d28f6-472">Componenti per il suggerimento</span><span class="sxs-lookup"><span data-stu-id="d28f6-472">Suggesters</span></span>
<span data-ttu-id="d28f6-473">funzionalità dei suggerimenti Hello in ricerca di Azure è una funzionalità di query di digitazione o di completamento automatico, che fornisce un elenco di potenziali termini di ricerca nella risposta toopartial input di stringa in una casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="d28f6-474">I suggerimenti di query sono quelli visualizzati quando si usano i motori di ricerca commerciali: se si digita ".NET" in Bing, viene visualizzato un elenco di termini quali ".NET 4.5", ".NET Framework 3.5" e così via.</span><span class="sxs-lookup"><span data-stu-id="d28f6-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="d28f6-475">Quando si utilizza l'API REST del servizio ricerca hello, l'implementazione di suggerimenti in un'applicazione di ricerca di Azure personalizzata richiede seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="d28f6-476">Abilitare i suggerimenti aggiungendo un **dello strumento suggerimenti** costruzione nell'indice, offrendo digitazione nome hello, modalità di ricerca e un elenco di campi per il quale viene richiamata.</span><span class="sxs-lookup"><span data-stu-id="d28f6-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="d28f6-477">Ad esempio, se si specifica "NomeCittà" come un campo di origine, digitare una stringa di ricerca parziale del "Mare" comporterà "Seattle", "Milazzo" e "Militello" (tutti e tre sono nomi di città effettive) offerto come utente toohello suggerimenti di query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="d28f6-478">Richiamare i suggerimenti mediante chiamata hello [API suggerimenti](#Suggestions) nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="d28f6-479">In genere stringhe di ricerca parziali vengono inviate toohello servizio hello utente digita una query di ricerca, mentre l'API restituisce un set di frasi suggerite.</span><span class="sxs-lookup"><span data-stu-id="d28f6-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="d28f6-480">Questo articolo viene illustrato come tooconfigure un **dello strumento suggerimenti**.</span><span class="sxs-lookup"><span data-stu-id="d28f6-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="d28f6-481">È inoltre consigliabile esaminare hello [API suggerimenti](#Suggestions) per informazioni dettagliate sull'utilizzo di un strumento suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="d28f6-482">**Utilizzo**</span><span class="sxs-lookup"><span data-stu-id="d28f6-482">**Usage**</span></span>

<span data-ttu-id="d28f6-483">`Suggesters`vengono creati nell'indice hello e adatti per documenti specifici toosuggest invece che termini o frasi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="d28f6-484">campi di Hello migliori candidate sono titoli, nomi e altre frasi relativamente brevi che consentono di identificare un elemento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="d28f6-485">I campi meno efficaci sono quelli ripetitivi, come le categorie e i tag, o quelli molto lunghi, come le descrizioni o i commenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="d28f6-486">Come parte della definizione di indice hello, è possibile aggiungere un singolo strumento suggerimenti toohello `suggesters` insieme.</span><span class="sxs-lookup"><span data-stu-id="d28f6-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="d28f6-487">Le proprietà che definiscono un strumento suggerimenti includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="d28f6-488">`name`: nome hello di strumento suggerimenti hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="d28f6-489">Utilizza il nome di hello di strumento suggerimenti hello quando si chiama hello `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="d28f6-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="d28f6-490">`searchMode`: hello toosearch strategia utilizzata per ottenere frasi candidate.</span><span class="sxs-lookup"><span data-stu-id="d28f6-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="d28f6-491">Hello unica modalità attualmente supportata è `analyzingInfixMatching`, che esegue una corrispondenza flessibile di frasi all'inizio di hello o all'interno delle proposizioni hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="d28f6-492">`sourceFields`: Un elenco di uno o più campi che sono hello origine di contenuto hello per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="d28f6-493">Solo i campi di tipo `Edm.String` e `Collection(Edm.String)` possono essere origini per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="d28f6-494">È possibile usare solo campi per i quali non è impostato un analizzatore di lingua personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="d28f6-495">**Esempio di componente di suggerimento**</span><span class="sxs-lookup"><span data-stu-id="d28f6-495">**Suggester Example**</span></span>

<span data-ttu-id="d28f6-496">Un strumento suggerimenti è parte dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-496">A suggester is part of hello index.</span></span> <span data-ttu-id="d28f6-497">Può esistere un solo strumento suggerimenti in hello `suggesters` insieme fields raccolta nella versione corrente di hello, insieme a hello e `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="d28f6-498">Se è stata utilizzata la versione di anteprima pubblica hello di ricerca di Azure, `suggesters` sostituisce una proprietà booleana precedente (`"suggestions": false`) che supporta solo i suggerimenti di prefisso per stringhe brevi (da 3 a 25 caratteri).</span><span class="sxs-lookup"><span data-stu-id="d28f6-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="d28f6-499">Il relativo sostituto, `suggesters`, supporta infisso che trovano termini corrispondenti all'inizio di hello o centro hello del contenuto del campo, con una migliore tolleranza per gli errori nelle stringhe di ricerca di corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="d28f6-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="d28f6-500">Si è a partire dalla versione di hello in genere disponibili, ora hello unica implementazione di suggerimenti hello API.</span><span class="sxs-lookup"><span data-stu-id="d28f6-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="d28f6-501">Hello precedente `suggestions` proprietà che è stata introdotta in `api-version=2014-07-31-Preview` continua toowork in tale versione, ma non è operativa nella hello `2015-02-28` o versioni successive di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="d28f6-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="d28f6-502">Aggiornare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-502">Update Index</span></span>
<span data-ttu-id="d28f6-503">È possibile aggiornare un indice esistente in Ricerca di Azure usando una richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="d28f6-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="d28f6-504">Gli aggiornamenti possono includere l'aggiunta di nuovi campi toohello schema esistente, la modifica delle opzioni CORS e la modifica di profili di punteggio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="d28f6-505">Per altre informazioni, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="d28f6-506">Specificare il nome di hello di hello indice tooupdate nell'URI richiesta hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d28f6-507">**Importante:** il supporto per gli aggiornamenti dello schema di indice è toooperations limitato che non richiedono la ricompilazione di indice di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="d28f6-508">Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="d28f6-509">È possibile aggiungere nuovi campi in qualsiasi momento, anche se i campi esistenti non possono essere modificati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="d28f6-510">Hello vale troppo`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="d28f6-511">Possono aggiungere nuovi campi vengono aggiunti dello strumento suggerimenti tooa in campi di hello hello ora, ma non è possibile rimuovere campi da `suggesters` e non è possibile aggiungere campi esistenti troppo`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="d28f6-512">Quando si aggiunge un nuovo indice tooan campo, tutti i documenti esistenti nell'indice hello avranno automaticamente un valore null per tale campo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="d28f6-513">Nessun ulteriore spazio di archiviazione verrà utilizzato fino a quando non verranno aggiunti toohello indice nuovi documenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="d28f6-514">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-514">**Request**</span></span>

<span data-ttu-id="d28f6-515">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d28f6-516">Hello **indice ad aggiornamento in** richiesta viene costruita utilizzando HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="d28f6-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="d28f6-517">Con PUT, il nome dell'indice hello fa parte dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="d28f6-518">Se l'indice di hello non esiste, viene creato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="d28f6-519">Se l'indice hello esiste già, è aggiornato toohello nuova definizione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="d28f6-520">Nome indice Hello deve essere minuscola, iniziare con una lettera o un numero, avere senza barre o punti e minore di 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="d28f6-521">Dopo avere avviato il nome dell'indice hello con una lettera o un numero, il resto di hello del nome hello può includere qualsiasi lettera, numero e trattino, purché hello trattini non siano consecutivi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="d28f6-522">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-523">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-524">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-525">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-525">**Request Headers**</span></span>

<span data-ttu-id="d28f6-526">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-527">`Content-Type`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-527">`Content-Type`: Required.</span></span> <span data-ttu-id="d28f6-528">Impostare questa proprietà troppo`application/json`</span><span class="sxs-lookup"><span data-stu-id="d28f6-528">Set this too`application/json`</span></span>
* <span data-ttu-id="d28f6-529">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-529">`api-key`: Required.</span></span> <span data-ttu-id="d28f6-530">Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-531">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-532">Hello **indice ad aggiornamento in** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-533">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-534">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-535">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-536">**Sintassi del corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-536">**Request Body Syntax**</span></span>

<span data-ttu-id="d28f6-537">Quando si aggiorna un indice esistente, il corpo di hello deve includere definizione dello schema originale hello, nonché i nuovi campi hello che si aggiunge, nonché hello modificato i profili di punteggio, suggerimento e le opzioni CORS, se presente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="d28f6-538">Se non si modificano i profili di punteggio hello e le opzioni CORS, è necessario includere originali hello dalla creazione dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="d28f6-539">In genere hello migliore modello toouse per gli aggiornamenti è definizione dell'indice hello tooretrieve con un'operazione GET, modificarla, quindi aggiornarla mediante PUT.</span><span class="sxs-lookup"><span data-stu-id="d28f6-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="d28f6-540">sintassi dello schema Hello utilizzato toocreate che un indice viene riprodotto di seguito per praticità.</span><span class="sxs-lookup"><span data-stu-id="d28f6-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="d28f6-541">Per altri dettagli, vedere [Creare un indice](#CreateIndex) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="d28f6-542">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-542">**Response**</span></span>

<span data-ttu-id="d28f6-543">Per una richiesta con esito positivo: "204 Nessun contenuto".</span><span class="sxs-lookup"><span data-stu-id="d28f6-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="d28f6-544">Per impostazione predefinita hello corpo della risposta sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="d28f6-544">By default hello response body will be empty.</span></span> <span data-ttu-id="d28f6-545">Tuttavia, se hello `Prefer` intestazione della richiesta è troppo`return=representation`, corpo della risposta hello conterrà hello JSON per la definizione dell'indice hello che è stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="d28f6-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="d28f6-546">In questo caso, cui codice di stato di hello esito positivo sarà "200 OK".</span><span class="sxs-lookup"><span data-stu-id="d28f6-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="d28f6-547">**Aggiornamento della definizione dell'indice con analizzatori personalizzati**</span><span class="sxs-lookup"><span data-stu-id="d28f6-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="d28f6-548">Dopo che un analizzatore, un tokenizer, un filtro di token o un filtro di carattere è stato definito non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="d28f6-549">Nuovi possono essere aggiunto indice esistente tooan solo se hello `allowIndexDowntime` flag è impostato tootrue nella richiesta di aggiornamento di hello indice:</span><span class="sxs-lookup"><span data-stu-id="d28f6-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="d28f6-550">Si noti che questa operazione passerà l'indice offline per almeno alcuni secondi, causando l'indicizzazione e query richiede toofail.</span><span class="sxs-lookup"><span data-stu-id="d28f6-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="d28f6-551">Disponibilità delle prestazioni e di scrittura dell'indice hello può essere compromesso per alcuni minuti dopo aver aggiornato l'indice di hello, o più per gli indici di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="d28f6-552">Elencare gli indici</span><span class="sxs-lookup"><span data-stu-id="d28f6-552">List Indexes</span></span>
<span data-ttu-id="d28f6-553">Hello **indici dell'elenco** operazione restituisce un elenco di indici hello attualmente nel servizio di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="d28f6-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d28f6-554">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-554">**Request**</span></span>

<span data-ttu-id="d28f6-555">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d28f6-556">Hello **indici dell'elenco** richiesta può essere costruita utilizzando il metodo GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="d28f6-557">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-558">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-559">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-560">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-560">**Request Headers**</span></span>

<span data-ttu-id="d28f6-561">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-562">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-562">`api-key`: Required.</span></span> <span data-ttu-id="d28f6-563">Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-564">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-565">Hello **indici dell'elenco** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).</span><span class="sxs-lookup"><span data-stu-id="d28f6-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-566">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-567">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-568">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-569">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-569">**Request Body**</span></span>

<span data-ttu-id="d28f6-570">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-570">None.</span></span>

<span data-ttu-id="d28f6-571">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-571">**Response**</span></span>

<span data-ttu-id="d28f6-572">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d28f6-573">Di seguito è riportato il corpo di una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="d28f6-573">Here is an example response body:</span></span>

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

<span data-ttu-id="d28f6-574">Si noti che è possibile filtrare la risposta hello delle proprietà hello toojust che si è interessati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="d28f6-575">Ad esempio, se si desidera solo un elenco di nomi di indice, utilizzare hello OData `$select` opzione di query:</span><span class="sxs-lookup"><span data-stu-id="d28f6-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="d28f6-576">In questo caso, la risposta hello hello sopra riportato sarebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d28f6-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="d28f6-577">Si tratta di una larghezza di banda toosave tecnica utile se si dispone di un numero eccessivo di indici in servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="d28f6-578">Ottenere un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-578">Get Index</span></span>
<span data-ttu-id="d28f6-579">Hello **ottenere indice** operazione Ottiene la definizione di indice hello da ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="d28f6-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d28f6-580">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-580">**Request**</span></span>

<span data-ttu-id="d28f6-581">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-582">Hello **ottenere indice** richiesta può essere costruita utilizzando il metodo GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="d28f6-583">Hello [nome indice] nell'URI della richiesta hello specifica quali tooreturn indice dalla raccolta di indici hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="d28f6-584">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-585">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-586">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-587">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-587">**Request Headers**</span></span>

<span data-ttu-id="d28f6-588">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-589">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-590">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-591">Hello **ottenere indice** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).</span><span class="sxs-lookup"><span data-stu-id="d28f6-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-592">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-593">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-594">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-595">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-595">**Request Body**</span></span>

<span data-ttu-id="d28f6-596">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-596">None.</span></span>

<span data-ttu-id="d28f6-597">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-597">**Response**</span></span>

<span data-ttu-id="d28f6-598">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d28f6-599">Vedere l'esempio hello JSON in [la creazione e aggiornamento di un indice](#CreateUpdateIndexExample) per un esempio di payload di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="d28f6-600">Eliminare un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-600">Delete Index</span></span>
<span data-ttu-id="d28f6-601">Hello **Elimina indice** operazione rimuove un indice e i documenti associati al servizio di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="d28f6-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="d28f6-602">È possibile ottenere il nome dell'indice hello dal dashboard del servizio nel portale di Azure hello hello o da hello API.</span><span class="sxs-lookup"><span data-stu-id="d28f6-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="d28f6-603">Per informazioni dettagliate, vedere [Elencare gli indici](#ListIndexes) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d28f6-604">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-604">**Request**</span></span>

<span data-ttu-id="d28f6-605">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-606">Hello **Elimina indice** richiesta può essere costruita utilizzando il metodo DELETE hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="d28f6-607">Hello [nome indice] nell'URI della richiesta hello specifica quali toodelete indice dalla raccolta di indici hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="d28f6-608">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-609">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-610">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-611">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-611">**Request Headers**</span></span>

<span data-ttu-id="d28f6-612">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-613">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-613">`api-key`: Required.</span></span> <span data-ttu-id="d28f6-614">Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-615">È un valore di stringa, univoco tooyour URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="d28f6-616">Hello **Elimina indice** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-617">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-618">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-619">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-620">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-620">**Request Body**</span></span>

<span data-ttu-id="d28f6-621">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-621">None.</span></span>

<span data-ttu-id="d28f6-622">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-622">**Response**</span></span>

<span data-ttu-id="d28f6-623">Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.</span><span class="sxs-lookup"><span data-stu-id="d28f6-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="d28f6-624">Ottenere le statistiche di un indice</span><span class="sxs-lookup"><span data-stu-id="d28f6-624">Get Index Statistics</span></span>
<span data-ttu-id="d28f6-625">Hello **ottenere statistiche dell'indice** operazione restituisce da ricerca di Azure con un numero di documenti per indice corrente hello, nonché l'utilizzo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="d28f6-626">Le statistiche sul numero di documenti e le dimensioni vengono raccolte ad intervalli di pochi minuti, non in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d28f6-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="d28f6-627">Pertanto, statistiche hello restituite da questa API potrebbero non riflettere le modifiche è causato da operazioni di indicizzazione di recente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="d28f6-628">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-628">**Request**</span></span>

<span data-ttu-id="d28f6-629">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="d28f6-630">Hello **ottenere statistiche dell'indice** richiesta può essere costruita utilizzando il metodo GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="d28f6-631">Hello [nome indice] nell'URI della richiesta hello indica hello servizio tooreturn indice le statistiche per hello specificato indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="d28f6-632">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-633">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-634">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-635">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-635">**Request Headers**</span></span>

<span data-ttu-id="d28f6-636">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-637">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-638">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-639">Hello **ottenere statistiche dell'indice** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).</span><span class="sxs-lookup"><span data-stu-id="d28f6-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-640">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-641">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-642">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-643">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-643">**Request Body**</span></span>

<span data-ttu-id="d28f6-644">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-644">None.</span></span>

<span data-ttu-id="d28f6-645">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-645">**Response**</span></span>

<span data-ttu-id="d28f6-646">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d28f6-647">corpo della risposta Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="d28f6-648">Analizzatore di test</span><span class="sxs-lookup"><span data-stu-id="d28f6-648">Test Analyzer</span></span>
<span data-ttu-id="d28f6-649">Hello **analizzare API** viene illustrato come un analizzatore suddivide il testo in token.</span><span class="sxs-lookup"><span data-stu-id="d28f6-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d28f6-650">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-650">**Request**</span></span>

<span data-ttu-id="d28f6-651">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="d28f6-652">Hello **analizzare API** richiesta può essere costruita utilizzando il metodo POST hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="d28f6-653">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-654">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-655">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-656">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-656">**Request Headers**</span></span>

<span data-ttu-id="d28f6-657">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-658">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-659">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-660">Hello **analizzare API** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).</span><span class="sxs-lookup"><span data-stu-id="d28f6-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-661">È necessario anche il nome dell'indice hello e URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-662">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-663">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-664">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="d28f6-665">oppure</span><span class="sxs-lookup"><span data-stu-id="d28f6-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="d28f6-666">Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessario toobe nomi validi di analizzatori predefiniti o personalizzati, tokenizer, filtri di token e char per indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="d28f6-667">altre informazioni sul processo di hello dell'analisi lessicale vedere toolearn [Analysis in ricerca di Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="d28f6-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="d28f6-668">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-668">**Response**</span></span>

<span data-ttu-id="d28f6-669">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d28f6-670">corpo della risposta Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="d28f6-671">**Esempio dell'API di analisi**</span><span class="sxs-lookup"><span data-stu-id="d28f6-671">**Analyze API example**</span></span>

<span data-ttu-id="d28f6-672">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="d28f6-673">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="d28f6-674">Operazioni sui documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-674">Document Operations</span></span>
<span data-ttu-id="d28f6-675">In ricerca di Azure, un indice viene archiviato nel cloud hello e popolato con i documenti JSON caricare toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="d28f6-676">Tutti i documenti hello caricati costituiscono insieme hello dei dati di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="d28f6-677">I documenti includono campi, alcuni dei quali sono stati suddivisi in token corrispondenti a termini di ricerca durante il caricamento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="d28f6-678">Hello `/docs` segmento di URL in hello API di ricerca di Azure rappresenta l'insieme di hello di documenti in un indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="d28f6-679">Tutte le operazioni eseguite nella raccolta di hello, ad esempio caricamento, unione, eliminazione o l'esecuzione di query su documenti avvengono nel contesto di hello di un singolo indice, in tal caso hello URL per queste operazioni inizieranno sempre con `/indexes/[index name]/docs` per un nome dell'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="d28f6-680">Il codice dell'applicazione deve generare JSON documenti tooupload tooAzure ricerca o è possibile utilizzare un [indicizzatore](https://msdn.microsoft.com/library/dn946891.aspx) tooload documenti di origine di dati di hello è il Database di SQL Azure o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d28f6-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="d28f6-681">In genere, gli indici vengono popolati da un singolo set di dati specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="d28f6-682">È consigliabile pianificare sulla disponibilità di un documento per ogni elemento che si desidera toosearch.</span><span class="sxs-lookup"><span data-stu-id="d28f6-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="d28f6-683">Un'applicazione per il noleggio di film può avere un documento per ogni film, un'applicazione di tipo vetrina può avere un documento per ogni SKU, un'applicazione per corsi online può avere un documento per ogni corso oppure una società di ricerche può avere un documento per ogni articolo accademico disponibile nel proprio archivio e così via.</span><span class="sxs-lookup"><span data-stu-id="d28f6-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="d28f6-684">I documenti sono costituiti da uno o più campi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="d28f6-685">I campi possono contenere testo suddiviso da Ricerca di Azure in token corrispondenti a termini di ricerca, oltre a valori senza token o non di testo che possono essere usati nei filtri o nei profili di punteggio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="d28f6-686">Hello nomi, tipi di dati e le funzionalità di ricerca supportate per ogni campo sono determinate dallo schema di indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="d28f6-687">Uno dei campi di hello in ogni schema di indice deve essere designato come un ID e ogni documento deve avere un valore per il campo ID hello che identifica in modo univoco tale documento nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="d28f6-688">Tutti gli altri campi di documento sono facoltativi e verranno tooa null il valore predefinito se non specificato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="d28f6-689">Si noti che i valori null non occupano spazio nell'indice di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="d28f6-690">Prima di poter caricare documenti, è necessario avere già creato indice hello sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="d28f6-691">Per informazioni dettagliate su questo primo passaggio, vedere [Creare un indice](#CreateIndex) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="d28f6-692">aggiunta, aggiornamento o eliminazione di documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="d28f6-693">È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="d28f6-694">Per un numero elevato di aggiornamenti, è consigliabile l'invio in batch di documenti, documenti too1000 per ogni batch, o circa 16 MB per batch.</span><span class="sxs-lookup"><span data-stu-id="d28f6-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d28f6-695">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-695">**Request**</span></span>

<span data-ttu-id="d28f6-696">Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d28f6-697">È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="d28f6-698">Hello URI della richiesta include [nome indice], che specifica quali toopost indicizzare i documenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="d28f6-699">È possibile registrare solo indice tooone documenti alla volta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="d28f6-700">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-701">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-702">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-703">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-703">**Request Headers**</span></span>

<span data-ttu-id="d28f6-704">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-705">`Content-Type`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-705">`Content-Type`: Required.</span></span> <span data-ttu-id="d28f6-706">Impostare questa proprietà troppo`application/json`</span><span class="sxs-lookup"><span data-stu-id="d28f6-706">Set this too`application/json`</span></span>
* <span data-ttu-id="d28f6-707">`api-key`: elemento obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-707">`api-key`: Required.</span></span> <span data-ttu-id="d28f6-708">Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-709">È un valore stringa, il servizio tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="d28f6-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="d28f6-710">Hello **aggiungere documenti** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="d28f6-711">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-712">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-713">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-714">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-714">**Request Body**</span></span>

<span data-ttu-id="d28f6-715">corpo Hello della richiesta di hello contiene uno o più documenti toobe indicizzata.</span><span class="sxs-lookup"><span data-stu-id="d28f6-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="d28f6-716">I documenti sono identificati da una chiave univoca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="d28f6-717">Ogni documento è associato a un'azione: upload, merge, mergeOrUpload o delete.</span><span class="sxs-lookup"><span data-stu-id="d28f6-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="d28f6-718">Le richieste di caricamento deve includere i dati del documento hello come un set di coppie chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="d28f6-719">Le chiavi di documenti possono contenere solo lettere, numeri, trattini ("-"), caratteri di sottolineatura ("_") e segni di uguale ("=").</span><span class="sxs-lookup"><span data-stu-id="d28f6-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="d28f6-720">Per altre informazioni, vedere la pagina relativa alle [regole di denominazione](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="d28f6-721">**Azioni sui documenti**</span><span class="sxs-lookup"><span data-stu-id="d28f6-721">**Document Actions**</span></span>

* <span data-ttu-id="d28f6-722">`upload`: Un'azione upload è simile tooan "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="d28f6-723">Si noti che tutti i campi vengono sostituiti in caso di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="d28f6-724">`merge`: Merge aggiorna un'esistente il documento con hello specificati campi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="d28f6-725">Se il documento hello non esiste, l'unione di hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="d28f6-726">Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="d28f6-727">Sono inclusi anche i campi di tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="d28f6-728">Ad esempio, se hello documento contiene un campo "tags" con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per "tags", valore finale di hello del campo hello "tags" sarà `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="d28f6-729">e **non** sarà `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="d28f6-730">`mergeOrUpload`: si comporta come `merge` se esiste un documento con hello data già chiave nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="d28f6-731">Se il documento hello non esiste, si comporta come `upload` con un nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="d28f6-732">`delete`: Delete Elimina documento specificato hello indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="d28f6-733">Si noti che tutti i campi specificare un `delete` operazione diversa da quella campo chiave hello verrà ignorati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="d28f6-734">Se si desidera tooremove un singolo campo da un documento, utilizzare `merge` invece e impostare semplicemente il campo hello in modo esplicito troppo`null`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="d28f6-735">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-735">**Response**</span></span>

<span data-ttu-id="d28f6-736">Il codice di stato 200 (OK) viene restituito per una risposta con esito positivo, a indicare che tutti gli elementi sono stati indicizzati correttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="d28f6-737">In questo caso viene hello `status` proprietà impostata tootrue per tutti gli elementi, nonché hello `statusCode` proprietà impostata tooeither 201 (per i documenti appena caricati) o 200 (per i documenti uniti o eliminati):</span><span class="sxs-lookup"><span data-stu-id="d28f6-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="d28f6-738">Il codice di stato 207 (Multi-Status) viene restituito quando almeno un elemento non è stato indicizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="d28f6-739">Gli elementi che non sono stati indicizzati hanno hello `status` toofalse set di campi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="d28f6-740">Hello `errorMessage` e `statusCode` proprietà indicherà il motivo di hello dell'errore di indicizzazione hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="d28f6-741">Hello nella tabella seguente illustra vari documento i codici di stato che possono essere restituiti nella risposta hello hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="d28f6-742">Si noti che alcune indica problemi relativi alla richiesta di hello stesso, mentre altri indicare le condizioni di errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="d28f6-743">Hello quest'ultimo che si consiglia di riprovare dopo un ritardo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="d28f6-744">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="d28f6-744">Status code</span></span></th>
        <th><span data-ttu-id="d28f6-745">Significato</span><span class="sxs-lookup"><span data-stu-id="d28f6-745">Meaning</span></span></th>
        <th><span data-ttu-id="d28f6-746">Non irreversibile</span><span class="sxs-lookup"><span data-stu-id="d28f6-746">Retryable</span></span></th>
        <th><span data-ttu-id="d28f6-747">Note</span><span class="sxs-lookup"><span data-stu-id="d28f6-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-748">200</span><span class="sxs-lookup"><span data-stu-id="d28f6-748">200</span></span></td>
        <td><span data-ttu-id="d28f6-749">Il documento è stato modificato o eliminato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="d28f6-750">n/d</span><span class="sxs-lookup"><span data-stu-id="d28f6-750">n/a</span></span></td>
        <td><span data-ttu-id="d28f6-751">Le operazioni di eliminazione sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>.</span><span class="sxs-lookup"><span data-stu-id="d28f6-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="d28f6-752">Vale a dire, anche se non esiste una chiave di documento nell'indice hello, il tentativo di un'operazione di eliminazione con tale chiave comporterà un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-753">201</span><span class="sxs-lookup"><span data-stu-id="d28f6-753">201</span></span></td>
        <td><span data-ttu-id="d28f6-754">Il documento è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="d28f6-755">n/d</span><span class="sxs-lookup"><span data-stu-id="d28f6-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-756">400</span><span class="sxs-lookup"><span data-stu-id="d28f6-756">400</span></span></td>
        <td><span data-ttu-id="d28f6-757">Si è verificato un errore nel documento hello che ne ha impedito da indicizzare.</span><span class="sxs-lookup"><span data-stu-id="d28f6-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="d28f6-758">No</span><span class="sxs-lookup"><span data-stu-id="d28f6-758">No</span></span></td>
        <td><span data-ttu-id="d28f6-759">messaggio di errore Hello in risposta hello indicherà qual è il documento hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-760">404</span><span class="sxs-lookup"><span data-stu-id="d28f6-760">404</span></span></td>
        <td><span data-ttu-id="d28f6-761">Impossibile unire il documento Hello perché hello data chiave non esiste nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="d28f6-762">No</span><span class="sxs-lookup"><span data-stu-id="d28f6-762">No</span></span></td>
        <td><span data-ttu-id="d28f6-763">Questo errore non si verifica per i caricamenti perché questi creano nuovi documenti e non si verifica per le eliminazioni perché queste sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>.</span><span class="sxs-lookup"><span data-stu-id="d28f6-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-764">409</span><span class="sxs-lookup"><span data-stu-id="d28f6-764">409</span></span></td>
        <td><span data-ttu-id="d28f6-765">Quando si tenta di tooindex un documento, è stato rilevato un conflitto di versione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="d28f6-766">Sì</span><span class="sxs-lookup"><span data-stu-id="d28f6-766">Yes</span></span></td>
        <td><span data-ttu-id="d28f6-767">Ciò può verificarsi quando si cerca di hello tooindex stesso documento più di una volta contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-768">422</span><span class="sxs-lookup"><span data-stu-id="d28f6-768">422</span></span></td>
        <td><span data-ttu-id="d28f6-769">indice di Hello è temporaneamente non disponibile perché è stato aggiornato con too'true set di flag hello 'allowIndexDowntime' '.</span><span class="sxs-lookup"><span data-stu-id="d28f6-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="d28f6-770">Sì</span><span class="sxs-lookup"><span data-stu-id="d28f6-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d28f6-771">503</span><span class="sxs-lookup"><span data-stu-id="d28f6-771">503</span></span></td>
        <td><span data-ttu-id="d28f6-772">Il servizio di ricerca è temporaneamente non disponibile, probabilmente a causa di tooheavy carico.</span><span class="sxs-lookup"><span data-stu-id="d28f6-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="d28f6-773">Sì</span><span class="sxs-lookup"><span data-stu-id="d28f6-773">Yes</span></span></td>
        <td><span data-ttu-id="d28f6-774">Il codice deve attendere prima di ritentare in questo caso, o si rischia di prolungamento indisponibilità del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="d28f6-775">**Nota**: se il codice client riceve spesso una risposta 207, è possibile che il sistema di hello è sotto carico.</span><span class="sxs-lookup"><span data-stu-id="d28f6-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="d28f6-776">È possibile verificarlo controllando hello `statusCode` proprietà 503.</span><span class="sxs-lookup"><span data-stu-id="d28f6-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="d28f6-777">Se questo è il caso di hello, è consigliabile ***la limitazione delle richieste di indicizzazione***.</span><span class="sxs-lookup"><span data-stu-id="d28f6-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="d28f6-778">In caso contrario, se non si riduce il traffico di indicizzazione, hello sistema inizi a rifiutare tutte le richieste con 503 errori.</span><span class="sxs-lookup"><span data-stu-id="d28f6-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="d28f6-779">Il codice di stato 429 indica che è stata superata la quota per il numero di hello di documenti per indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="d28f6-780">È necessario creare un nuovo indice o effettuare l'aggiornamento per ottenere limiti di capacità più elevati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="d28f6-781">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="d28f6-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="d28f6-782">ricerca documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-782">Search Documents</span></span>
<span data-ttu-id="d28f6-783">Oggetto **ricerca** operazione viene eseguita come una richiesta GET o POST e specifica i parametri che consentono di criteri di hello per la selezione di documenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="d28f6-784">**Quando toouse registra anziché GET**</span><span class="sxs-lookup"><span data-stu-id="d28f6-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="d28f6-785">Quando si utilizza HTTP GET hello toocall **ricerca** API, è necessario tenere presente che la lunghezza hello dell'URL di richiesta di hello non può superare 8 KB toobe.</span><span class="sxs-lookup"><span data-stu-id="d28f6-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="d28f6-786">Di solito è sufficiente per la maggior parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-786">This is usually enough for most applications.</span></span> <span data-ttu-id="d28f6-787">Alcune applicazioni, tuttavia, generano query di dimensioni molto grandi o espressioni di filtro OData.</span><span class="sxs-lookup"><span data-stu-id="d28f6-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="d28f6-788">Per queste applicazioni è preferibile usare HTTP POST perché consente filtri e query di maggiori dimensioni rispetto a GET.</span><span class="sxs-lookup"><span data-stu-id="d28f6-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="d28f6-789">Con POST, il numero di hello di condizioni o le clausole in una query hello limitano fattore, non pari a hello query non elaborati di hello poiché il limite di dimensione richiesta di hello per POST è circa 16 MB.</span><span class="sxs-lookup"><span data-stu-id="d28f6-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-790">Anche se limite delle dimensioni richiesta POST hello è molto grande, le query di ricerca e filtro espressioni non possono essere arbitrariamente complesse.</span><span class="sxs-lookup"><span data-stu-id="d28f6-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="d28f6-791">Per altre informazioni sulle limitazioni della complessità dei filtri e delle query di ricerca, vedere [Sintassi delle query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="d28f6-792">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-792">**Request**</span></span>

<span data-ttu-id="d28f6-793">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-794">Hello **ricerca** richiesta può essere costruita usando i metodi POST o GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="d28f6-795">URI della richiesta Hello specifica quali tooquery di indice, per tutti i documenti corrispondenti ai parametri hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="d28f6-796">I parametri vengono specificati nella stringa di query hello in caso di hello di richieste GET, e nella richiesta di hello richiede il corpo nel caso di hello di POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="d28f6-797">Come procedura consigliata quando si creano le richieste GET, ricordare troppo[codifica URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) query specifica i parametri quando si chiama hello API REST direttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="d28f6-798">Per le operazioni **Search** sono inclusi i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="d28f6-799">La codifica URL è consigliata solo nei hello sopra i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="d28f6-800">Se si codifica URL inavvertitamente hello intera stringa di query (tutti gli elementi dopo hello?), le richieste si interromperanno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="d28f6-801">Inoltre, la codifica URL è necessaria solo quando si chiama direttamente tramite API REST di ottenere hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="d28f6-802">Non è necessaria alcuna codifica URL quando si chiama **ricerca** utilizzando POST, o quando si utilizza hello [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx), che gestisce la codifica URL per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="d28f6-803"><a name="SearchQueryParameters"></a>
**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="d28f6-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="d28f6-804">**Search** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="d28f6-805">Specificare questi parametri nell'URL hello stringa di query quando si chiama **ricerca** tramite GET e come proprietà JSON nel corpo della richiesta hello quando si chiama **ricerca** tramite POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="d28f6-806">la sintassi di Hello per alcuni parametri è leggermente diversa tra GET e POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="d28f6-807">Queste differenze sono riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="d28f6-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="d28f6-808">`search=[string]`(facoltativo): hello toosearch di testo per.</span><span class="sxs-lookup"><span data-stu-id="d28f6-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="d28f6-809">Per impostazione predefinita, la ricerca viene eseguita in tutti i campi `searchable` a meno che non sia specificato `searchFields`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="d28f6-810">Durante la ricerca `searchable` campi, testo di ricerca hello stesso vengono assegnati token, in modo più termini possono essere separati da spazi (ad esempio: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="d28f6-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="d28f6-811">utilizzare qualsiasi termine, toomatch `*` (può essere utile per query di filtro booleane).</span><span class="sxs-lookup"><span data-stu-id="d28f6-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="d28f6-812">Se si omette questo parametro ha lo stesso effetto dell'impostazione troppo hello`*`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="d28f6-813">Vedere [semplice sintassi di Query](https://msdn.microsoft.com/library/dn798920.aspx) per informazioni specifiche sulla sintassi di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="d28f6-814">**Nota**: risultati hello in alcuni casi possono essere sorprendenti quando si eseguono query su `searchable` campi.</span><span class="sxs-lookup"><span data-stu-id="d28f6-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="d28f6-815">tokenizer Hello include logica toohandle casi comuni tooEnglish testo, ad esempio apostrofi, virgole in numeri, e così via. Ad esempio, `search=123,456` corrisponderà a un singolo termine 123,456 invece hello singoli termini 123 e 456, poiché le virgole vengono utilizzate come separatore delle migliaia per i numeri di grandi dimensioni in inglese.</span><span class="sxs-lookup"><span data-stu-id="d28f6-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="d28f6-816">Per questo motivo, è consigliabile utilizzare lo spazio vuoto anziché termini tooseparate punteggiatura hello `search` parametro.</span><span class="sxs-lookup"><span data-stu-id="d28f6-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="d28f6-817">`searchMode=any|all`(facoltativo, valore predefinito è troppo`any`) - indica se uno o tutti i termini di ricerca hello devono corrispondere nel documento di ordine toocount hello come una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="d28f6-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="d28f6-818">`searchFields=[string]`(facoltativo): elenco di hello di toosearch di nomi di campo delimitati da virgole per hello il testo specificato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="d28f6-819">I campi di destinazione devono essere contrassegnati come `searchable`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="d28f6-820">`queryType=simple|full`(facoltativo, valore predefinito è troppo`simple`): quando il testo di ricerca troppo "semplice" set viene interpretato utilizzando un linguaggio di query semplice che consente di simboli, ad esempio +, * e "".</span><span class="sxs-lookup"><span data-stu-id="d28f6-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="d28f6-821">Per impostazione predefinita, le query vengono valutate in tutti i campi disponibili per la ricerca o nei campi indicati in `searchFields`in ogni documento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="d28f6-822">Quando il tipo di query hello è impostato troppo`full` testo di ricerca viene interpretato utilizzando linguaggio di query Lucene hello, che consente di cercare specifici di campo e ponderate.</span><span class="sxs-lookup"><span data-stu-id="d28f6-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="d28f6-823">Vedere [semplice sintassi di Query](https://msdn.microsoft.com/library/dn798920.aspx) e [sintassi delle Query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) per informazioni specifiche sulla sintassi di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="d28f6-824">Intervallo di ricerca in hello Lucene linguaggio di query non è supportato a favore $filter che offre funzionalità simili.</span><span class="sxs-lookup"><span data-stu-id="d28f6-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="d28f6-825">`moreLikeThis=[key]` (facoltativo) **Importante:** questa funzionalità è disponibile solo in `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-826">Questa opzione non può essere utilizzata in una query contenente parametri di ricerca di testo hello, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="d28f6-827">Hello `moreLikeThis` parametro consente di trovare documenti simili documento toohello specificato dalla chiave di documento hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="d28f6-828">Quando viene effettuata una richiesta di ricerca con `moreLikeThis`, viene generato un elenco di termini di ricerca in base a frequenza hello e delle condizioni nel documento di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="d28f6-829">Questi termini vengono quindi utilizzati toomake hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="d28f6-830">Per impostazione predefinita, hello contenuto di tutti i `searchable` campi sono considerati a meno che non `searchFields` è usato toorestrict campi a cui vengono eseguita la ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="d28f6-831">`$skip=#`(facoltativo): numero di hello della ricerca risultati tooskip; Non può essere maggiore di 100.000.</span><span class="sxs-lookup"><span data-stu-id="d28f6-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="d28f6-832">Se necessario tooscan documenti in sequenza, ma non è possibile utilizzare `$skip` scadenza toothis limitazione, è consigliabile utilizzare `$orderby` su una chiave totalmente ordinata e `$filter` con un intervallo di query alternativa.</span><span class="sxs-lookup"><span data-stu-id="d28f6-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-833">Quando si chiama **Search** con POST, questo parametro è denominato `skip` invece di `$skip`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="d28f6-834">`$top=#`(facoltativo): numero di hello della ricerca risultati tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="d28f6-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="d28f6-835">Può essere utilizzato in combinazione con `$skip` tooimplement il paging sul lato client dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-836">Quando si chiama **Search** con POST, questo parametro è denominato `top` invece di `$top`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="d28f6-837">`$count=true|false`(facoltativo, valore predefinito è troppo`false`)-specifica se toofetch hello conteggio totale dei risultati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="d28f6-838">Si tratta di hello conteggio di tutti i documenti corrispondenti hello `search` e `$filter` parametri, ignorando `$top` e `$skip`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="d28f6-839">Impostazione del valore troppo`true` può avere un impatto sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="d28f6-840">Si noti che il conteggio di hello restituito sono un'approssimazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-841">Quando si chiama **Search** con POST, questo parametro è denominato `count` invece di `$count`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="d28f6-842">`$orderby=[string]`(facoltativo): un elenco di espressioni delimitato da virgole toosort hello risultati da.</span><span class="sxs-lookup"><span data-stu-id="d28f6-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="d28f6-843">Ogni espressione può essere un nome di campo o una chiamata toohello `geo.distance()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="d28f6-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="d28f6-844">Ogni espressione può essere seguito da `asc` tooindicated crescente, e `desc` tooindicate decrescente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="d28f6-845">valore predefinito di Hello è l'ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-845">hello default is ascending order.</span></span> <span data-ttu-id="d28f6-846">Valori equivalenti verranno suddivise di punteggi di corrispondenza hello dei documenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="d28f6-847">Se non `$orderby` viene specificato, l'ordinamento predefinito hello sarà decrescente in base al punteggio di corrispondenza documento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="d28f6-848">È previsto un limite di 32 clausole per `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-849">Quando si chiama **Search** con POST, questo parametro è denominato `orderby` invece di `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="d28f6-850">`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="d28f6-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="d28f6-851">Se non viene specificato, sono inclusi tutti i campi contrassegnati come recuperabili nello schema di hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="d28f6-852">È anche possibile richiedere esplicitamente tutti i campi impostando questo parametro troppo`*`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-853">Quando si chiama **Search** con POST, questo parametro è denominato `select` invece di `$select`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="d28f6-854">`facet=[string]`(zero o più) - toofacet un campo da.</span><span class="sxs-lookup"><span data-stu-id="d28f6-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="d28f6-855">Facoltativamente è possibile che la stringa hello contenga facet di hello toocustomize parametri espresso come delimitato da virgole `name:value` coppie.</span><span class="sxs-lookup"><span data-stu-id="d28f6-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="d28f6-856">I parametri validi sono:</span><span class="sxs-lookup"><span data-stu-id="d28f6-856">Valid parameters are:</span></span>

* <span data-ttu-id="d28f6-857">`count`: numero massimo di termini facet. Il valore predefinito è 10.</span><span class="sxs-lookup"><span data-stu-id="d28f6-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="d28f6-858">Non vi è alcun valore massimo, ma i valori più alti comportano una riduzione delle prestazioni corrispondenti, soprattutto se campo con facet hello contiene un numero elevato di termini univoci.</span><span class="sxs-lookup"><span data-stu-id="d28f6-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="d28f6-859">Ad esempio: `facet=category,count:5` Ottiene hello prime cinque categorie nei risultati di facet.</span><span class="sxs-lookup"><span data-stu-id="d28f6-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="d28f6-860">**Nota**: se hello `count` parametro è minore di hello di termini univoci, risultati hello potrebbero non essere accurati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="d28f6-861">Questo è dovuto modo toohello query facet vengono distribuite tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="d28f6-862">Aumento `count` in genere aumenta hello precisione dei conteggi di termini hello, ma un calo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="d28f6-863">`sort`(uno dei `count` toosort *decrescente* dal conteggio, `-count` toosort *crescente* dal conteggio, `value` toosort *crescente* per valore, o `-value` toosort *decrescente* dal valore)</span><span class="sxs-lookup"><span data-stu-id="d28f6-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="d28f6-864">Ad esempio: `facet=category,count:3,sort:count` Ottiene hello prime tre categorie nei risultati di facet in ordine decrescente per il numero di hello di documenti con ogni nome di città.</span><span class="sxs-lookup"><span data-stu-id="d28f6-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="d28f6-865">Ad esempio, se hello prime tre categorie sono Budget, Motel e Luxury e 5 riscontri dispone di Budget, Motel ha 6 e lusso è 4, quindi hello bucket sarà nell'ordine di hello Motel, Budget, Luxury.</span><span class="sxs-lookup"><span data-stu-id="d28f6-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="d28f6-866">Esempio: `facet=rating,sort:-value` genera bucket per tutte le classificazioni possibili, in ordine decrescente in base al valore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="d28f6-867">Ad esempio, se le classificazioni di hello sono da 1 too5, hello bucket avranno l'ordine 5, 4, 3, 2, 1, indipendentemente dal numero di documenti corrispondenti a ogni classificazione.</span><span class="sxs-lookup"><span data-stu-id="d28f6-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="d28f6-868">`values` (valori numerici delimitati da pipe o valori `Edm.DateTimeOffset` che specificano un set dinamico di valori di immissione di facet)</span><span class="sxs-lookup"><span data-stu-id="d28f6-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="d28f6-869">Ad esempio: `facet=baseRate,values:10|20` produce tre bucket: uno per la tariffa di base 0 backup toobut 10 escluso, uno da 10 backup toobut non tra 20 e uno per 20 o superiore.</span><span class="sxs-lookup"><span data-stu-id="d28f6-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="d28f6-870">Esempio: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera due bucket, uno per hotel rinnovati prima del febbraio 2010 e uno per hotel rinnovati a partire dal 1° febbraio 2010.</span><span class="sxs-lookup"><span data-stu-id="d28f6-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="d28f6-871">`interval` (intervallo di tipo Integer maggiore di 0 per i numeri o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` per i valori di tipo data/ora)</span><span class="sxs-lookup"><span data-stu-id="d28f6-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="d28f6-872">Esempio: `facet=baseRate,interval:100` genera bucket in base agli intervalli di tariffe di base con dimensioni pari a 100.</span><span class="sxs-lookup"><span data-stu-id="d28f6-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="d28f6-873">Se le tariffe di base sono tutte comprese tra € 60 e € 600, saranno presenti bucket per 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.</span><span class="sxs-lookup"><span data-stu-id="d28f6-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="d28f6-874">Esempio: `facet=lastRenovationDate,interval:year` genera un bucket per ogni anno in cui gli hotel sono stati rinnovati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="d28f6-875">`timeoffset` ([+-]hh:mm, [+-]hhmm o [+-]hh) `timeoffset` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="d28f6-876">Possono essere combinata solo con hello `interval` opzione e solo quando applicata tooa campo di tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="d28f6-877">il valore di Hello specifica tooaccount offset UTC di hello di tempo per l'impostazione di limiti di tempo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="d28f6-878">Ad esempio: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utilizza hello limiti di giorno che inizia in corrispondenza UTC 01:00:00 (mezzanotte nel fuso orario di destinazione hello)</span><span class="sxs-lookup"><span data-stu-id="d28f6-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="d28f6-879">**Nota**: `count` e `sort` possono essere combinati in hello stessa specifica di facet, ma non può essere combinato con `interval` o `values`, e `interval` e `values` non possono essere combinati tra loro.</span><span class="sxs-lookup"><span data-stu-id="d28f6-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="d28f6-880">**Nota**: se `timeoffset` non è specificato, i facet di intervallo per data e ora vengono calcolati in base all'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="d28f6-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="d28f6-881">Ad esempio: per `facet=lastRenovationDate,interval:day`, limiti di giorno di hello inizia alle 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="d28f6-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="d28f6-882">Quando si chiama **Search** con POST, questo parametro è denominato `facets` invece di `facet`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="d28f6-883">Viene specificato anche come matrice di stringhe JSON, dove ogni stringa è un'espressione facet distinta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="d28f6-884">`$filter=[string]` (facoltativo): specifica un'espressione di ricerca strutturata nella sintassi standard di OData.</span><span class="sxs-lookup"><span data-stu-id="d28f6-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-885">Quando si chiama **Search** con POST, questo parametro è denominato `filter` invece di `$filter`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="d28f6-886">`highlight=[string]` (facoltativo): specifica un set di nomi di campo delimitati da virgole usati per evidenziare i risultati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="d28f6-887">Per l'evidenziazione dei risultati è possibile usare solo i campi `searchable` .</span><span class="sxs-lookup"><span data-stu-id="d28f6-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="d28f6-888">`highlightPreTag=[string]`(facoltativo, valore predefinito è troppo`<em>`): un tag che consente di anteporre evidenzia toohit di stringa.</span><span class="sxs-lookup"><span data-stu-id="d28f6-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="d28f6-889">Deve essere impostato con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-890">Quando si chiama **ricerca** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).</span><span class="sxs-lookup"><span data-stu-id="d28f6-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d28f6-891">`highlightPostTag=[string]`(facoltativo, valore predefinito è troppo`</em>`)-un tag di stringa che aggiunge toohit evidenzia.</span><span class="sxs-lookup"><span data-stu-id="d28f6-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="d28f6-892">Deve essere impostato con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-893">Quando si chiama **ricerca** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).</span><span class="sxs-lookup"><span data-stu-id="d28f6-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d28f6-894">`scoringProfile=[string]`(facoltativo): nome hello di un punteggio di profilo tooevaluate punteggi di corrispondenza per i documenti corrispondenti nei risultati di hello toosort ordine.</span><span class="sxs-lookup"><span data-stu-id="d28f6-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="d28f6-895">`scoringParameter=[string]`(zero o più) - indica i valori hello per ogni parametro definito in una funzione di punteggio (ad esempio, `referencePointParameter`) utilizzando il formato di hello `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="d28f6-896">Ad esempio, se hello profilo di punteggio definisce una funzione con un parametro denominato "mylocation" opzione stringa della query hello sarebbe `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="d28f6-897">trattino prima Hello separa nome hello da elenco di valori hello, mentre il secondo trattino hello fa parte del valore del primo hello (longitudine in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="d28f6-898">Per i parametri di punteggio, ad esempio per tag boosting che può contenere virgole, fare in modo che tutti i valori nell'elenco di hello utilizzando le virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="d28f6-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="d28f6-899">Se i valori di hello contengono virgolette singole, è possibile utilizzare caratteri di escape raddoppiando.</span><span class="sxs-lookup"><span data-stu-id="d28f6-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="d28f6-900">Ad esempio, se si dispone di un parametro denominato "mytag" aumento della priorità di tag e si desidera tooboost nel tag hello i valori "Hello, o ' Brien" e "Smith" query hello opzione stringa sarà `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="d28f6-901">Si noti che le virgolette sono necessarie solo per i valori che contengono virgole.</span><span class="sxs-lookup"><span data-stu-id="d28f6-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-902">Quando si chiama **Search** con POST, questo parametro è denominato `scoringParameters` invece di `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="d28f6-903">Viene specificato come matrice di stringhe JSON, dove ogni stringa è una coppia `name-values` separata.</span><span class="sxs-lookup"><span data-stu-id="d28f6-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="d28f6-904">`minimumCoverage`(facoltativo, per impostazione predefinita too100) - un numero compreso tra 0 e 100 che indica la percentuale hello dell'indice hello che deve essere analizzata da una query di ricerca affinché hello query toobe segnalati come completati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="d28f6-905">Per impostazione predefinita, un indice hello deve essere disponibile o `Search` restituirà il codice di stato HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="d28f6-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="d28f6-906">Se si imposta `minimumCoverage` e `Search` ha esito positivo, verrà restituito HTTP 200 e includere un `@search.coverage` valore nella risposta hello indicando la percentuale hello dell'indice hello che è stato incluso nella query hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-907">Se il valore di tooa di parametro è minore di 100 può risultare utile per garantire la disponibilità di ricerca neanche per i servizi con una sola replica.</span><span class="sxs-lookup"><span data-stu-id="d28f6-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="d28f6-908">Tuttavia, non tutti i documenti corrispondenti vengono garantiti toobe presenti nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="d28f6-909">Se il richiamo di ricerca più importanti dell'applicazione tooyour di disponibilità, allora è migliore tooleave `minimumCoverage` sul valore predefinito pari a 100.</span><span class="sxs-lookup"><span data-stu-id="d28f6-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="d28f6-910">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-911">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-912">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-913">Nota: Per questa operazione, hello `api-version` è specificato come un parametro di query nell'URL hello indipendentemente dal fatto se si chiama **ricerca** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="d28f6-914">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-914">**Request Headers**</span></span>

<span data-ttu-id="d28f6-915">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-916">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-917">È un valore di stringa, univoco tooyour URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="d28f6-918">Hello **ricerca** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d28f6-919">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-920">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-921">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-922">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-922">**Request Body**</span></span>

<span data-ttu-id="d28f6-923">Per GET: nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-923">For GET: None.</span></span>

<span data-ttu-id="d28f6-924">Per POST:</span><span class="sxs-lookup"><span data-stu-id="d28f6-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
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

<span data-ttu-id="d28f6-925">**Continuazione di risposte di ricerca parziali**</span><span class="sxs-lookup"><span data-stu-id="d28f6-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="d28f6-926">In alcuni casi ricerca di Azure non può restituire che tutti hello risultati richiesti in un'unica risposta di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="d28f6-927">Questa situazione può verificarsi per diversi motivi, ad esempio quando la query hello richiede molti documenti non specificando `$top` o specificando un valore per `$top` troppo grande.</span><span class="sxs-lookup"><span data-stu-id="d28f6-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="d28f6-928">In questi casi, ricerca di Azure includerà hello `@odata.nextLink` annotazione nel corpo della risposta hello, nonché `@search.nextPageParameters` se si trattasse di una richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="d28f6-929">È possibile utilizzare i valori hello di tooformulate queste annotazioni un'altra ricerca richiesta tooget hello parte successiva della risposta di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="d28f6-930">Si tratta di un ***continuazione*** di richiesta di ricerca originale hello e hello annotazioni vengono in genere chiamate ***i token di continuazione***.</span><span class="sxs-lookup"><span data-stu-id="d28f6-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="d28f6-931">Vedere [esempio hello seguente](#SearchResponse) per informazioni dettagliate sulla sintassi di hello di queste annotazioni e in cui appaiono nel corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="d28f6-932">motivi Hello perché ricerca di Azure potrebbe restituire i token di continuazione sono specifiche dell'implementazione e soggette toochange.</span><span class="sxs-lookup"><span data-stu-id="d28f6-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="d28f6-933">I client affidabili devono essere sempre pronti toohandle casi in cui vengono restituiti documenti meno del previsto e un token di continuazione è incluso toocontinue recupero di documenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="d28f6-934">Inoltre è necessario utilizzare hello stesso metodo HTTP della richiesta originale di hello in ordine toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d28f6-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="d28f6-935">Se ad esempio si invia una richiesta GET, anche le richieste di continuazione inviate devono usare il metodo GET e lo stesso vale per il metodo POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="d28f6-936"><a name="SearchResponse"></a>
**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="d28f6-937">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
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
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="d28f6-938">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="d28f6-938">**Examples:**</span></span>

<span data-ttu-id="d28f6-939">È possibile trovare esempi aggiuntivi nella hello [sintassi dell'espressione OData per ricerca di Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="d28f6-940">Hello ricerca dell'indice in ordine decrescente per Data.</span><span class="sxs-lookup"><span data-stu-id="d28f6-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="d28f6-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="d28f6-943">In una ricerca con facet, eseguire ricerche nell'indice hello e recuperare i facet per categorie, classificazioni, tag, nonché gli elementi con baseRate in intervalli specifici:</span><span class="sxs-lookup"><span data-stu-id="d28f6-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="d28f6-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="d28f6-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="d28f6-946">Utilizzando un filtro, restringere i risultati di query con facet precedenti hello dopo hello utente fa clic sulla classificazione 3 e della categoria "Motel":</span><span class="sxs-lookup"><span data-stu-id="d28f6-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="d28f6-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="d28f6-949">In una ricerca con facet, impostare un limite massimo per i termini univoci restituiti in una query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="d28f6-950">valore predefinito di Hello è 10, ma è possibile aumentare o ridurre questo valore utilizzando hello `count` parametro hello `facet` attributo:</span><span class="sxs-lookup"><span data-stu-id="d28f6-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="d28f6-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="d28f6-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="d28f6-953">Ricerca hello indice entro campi specifici; Ad esempio, un campo specifico del linguaggio:</span><span class="sxs-lookup"><span data-stu-id="d28f6-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="d28f6-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="d28f6-956">Indice di hello in più campi di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="d28f6-957">Ad esempio, è possibile archiviare e hello di eseguire query su campi ricercabili in più lingue, tutti all'interno dello stesso indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="d28f6-958">Se la lingua inglese e francese coesistono descrizioni in hello stesso documento, è possibile restituire hello in uno o tutti i risultati della query:</span><span class="sxs-lookup"><span data-stu-id="d28f6-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="d28f6-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="d28f6-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="d28f6-961">Si noti che è possibile eseguire query su un solo indice alla volta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="d28f6-962">Non creare più indici per ogni lingua, a meno che non si prevede di tooquery uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="d28f6-963">Paging - pagina 1 ° di hello Get di elementi (dimensioni di pagina sono 10):</span><span class="sxs-lookup"><span data-stu-id="d28f6-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="d28f6-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="d28f6-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="d28f6-966">Paging - pagina 2a di hello Get di elementi (dimensioni di pagina sono 10):</span><span class="sxs-lookup"><span data-stu-id="d28f6-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="d28f6-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="d28f6-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="d28f6-969">Recuperare un set specifico di campi:</span><span class="sxs-lookup"><span data-stu-id="d28f6-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="d28f6-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="d28f6-972">Recuperare i documenti corrispondenti a un'espressione di filtro specifica:</span><span class="sxs-lookup"><span data-stu-id="d28f6-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="d28f6-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="d28f6-975">Eseguire ricerche nell'indice hello e restituire frammenti con evidenziazioni di riscontri</span><span class="sxs-lookup"><span data-stu-id="d28f6-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="d28f6-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="d28f6-978">Eseguire ricerche nell'indice hello e restituire documenti ordinati dal più vicino toofarther lontano da una posizione di riferimento</span><span class="sxs-lookup"><span data-stu-id="d28f6-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="d28f6-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="d28f6-981">Ricerca hello indice presupponendo che non vi è un profilo di punteggio denominato "geo" con due funzioni di assegnazione dei punteggi di distanza, che definisce un parametro denominato "currentLocation" e una definizione di un parametro denominato "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="d28f6-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="d28f6-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="d28f6-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="d28f6-984">Trovare documenti nell'indice hello utilizzando [semplice sintassi di query](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="d28f6-985">Questa query restituisce gli hotel i cui campi ricercabili contengono hello termini "comfort" e "location" ma non "motel":</span><span class="sxs-lookup"><span data-stu-id="d28f6-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="d28f6-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d28f6-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d28f6-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="d28f6-988">Si noti hello utilizzo di `searchMode=all` sopra.</span><span class="sxs-lookup"><span data-stu-id="d28f6-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="d28f6-989">Inclusione di questo parametro esegue l'override predefinito hello `searchMode=any`e si assicura che `-motel` significa "AND NOT" invece di "OR NOT".</span><span class="sxs-lookup"><span data-stu-id="d28f6-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="d28f6-990">Senza `searchMode=all`, si ottiene "OR NOT" che vengono espansi anziché limitati i risultati della ricerca e può essere poco plausibile toosome utenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="d28f6-991">Trovare documenti nell'indice hello utilizzando [sintassi delle query lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28f6-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="d28f6-992">Questa query restituisce gli hotel in cui il campo categoria hello contiene termini hello "budget" e i campi ricercabili tutti contenente la frase hello "rinnovata recente".</span><span class="sxs-lookup"><span data-stu-id="d28f6-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="d28f6-993">Documenti che contengono la frase hello "recentemente rinnovata" rango più elevato in seguito a valore incremento del termine hello (3)</span><span class="sxs-lookup"><span data-stu-id="d28f6-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="d28f6-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="d28f6-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="d28f6-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="d28f6-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="d28f6-996">Cercare un documento</span><span class="sxs-lookup"><span data-stu-id="d28f6-996">Lookup Document</span></span>
<span data-ttu-id="d28f6-997">Hello **Lookup Document** operazione recupera un documento da ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="d28f6-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="d28f6-998">Ciò è utile quando un utente fa clic su un risultato di ricerca specifico e si desidera toolook i dettagli specifici su tale documento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="d28f6-999">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-999">**Request**</span></span>

<span data-ttu-id="d28f6-1000">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-1001">Hello **Lookup Document** richiesta può essere costruita come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="d28f6-1002">In alternativa, è possibile utilizzare sintassi di OData hello tradizionali per la ricerca della chiave:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="d28f6-1003">Hello URI della richiesta include [nome di un indice] e [key], che specifica quali tooretrieve documento da quale indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="d28f6-1004">È possibile recuperare un solo documento alla volta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1004">You can only get one document at a time.</span></span> <span data-ttu-id="d28f6-1005">Utilizzare **ricerca** tooget più documenti in una singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="d28f6-1006">**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1006">**Query Parameters**</span></span>

<span data-ttu-id="d28f6-1007">`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="d28f6-1008">Se non specificato o impostato troppo`*`, tutti i campi contrassegnati come recuperabili nello schema hello sono inclusi nella proiezione hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="d28f6-1009">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-1010">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-1011">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-1012">Nota: Per questa operazione, hello `api-version` viene specificato come un parametro di query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="d28f6-1013">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1013">**Request Headers**</span></span>

<span data-ttu-id="d28f6-1014">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-1015">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-1016">È un valore di stringa, univoco tooyour URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="d28f6-1017">Hello **Lookup Document** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d28f6-1018">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-1019">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-1020">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-1021">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1021">**Request Body**</span></span>

<span data-ttu-id="d28f6-1022">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1022">None.</span></span>

<span data-ttu-id="d28f6-1023">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1023">**Response**</span></span>

<span data-ttu-id="d28f6-1024">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="d28f6-1025">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1025">**Example**</span></span>

<span data-ttu-id="d28f6-1026">Documento hello ricerca con chiave '2'</span><span class="sxs-lookup"><span data-stu-id="d28f6-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="d28f6-1027">Documento hello ricerca con chiave '3' utilizzando la sintassi di OData:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="d28f6-1028">Contare i documenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-1028">Count Documents</span></span>
<span data-ttu-id="d28f6-1029">Hello **Count Documents** operazione recupera un conteggio del numero di hello di documenti in un indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="d28f6-1030">Hello `$count` sintassi fa parte di hello protocollo OData.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="d28f6-1031">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1031">**Request**</span></span>

<span data-ttu-id="d28f6-1032">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-1033">Hello **Count Documents** richiesta può essere costruita utilizzando il metodo GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="d28f6-1034">Hello [nome indice] nell'URI della richiesta hello hello servizio tooreturn indica un conteggio di tutti gli elementi nella raccolta documenti di hello dell'indice specificato di hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="d28f6-1035">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-1036">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-1037">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-1038">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1038">**Request Headers**</span></span>

<span data-ttu-id="d28f6-1039">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="d28f6-1040">`Accept`: Questo valore deve essere impostato troppo`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="d28f6-1041">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-1042">È un valore di stringa, univoco tooyour URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="d28f6-1043">Hello **Count Documents** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d28f6-1044">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-1045">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-1046">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-1047">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1047">**Request Body**</span></span>

<span data-ttu-id="d28f6-1048">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1048">None.</span></span>

<span data-ttu-id="d28f6-1049">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1049">**Response**</span></span>

<span data-ttu-id="d28f6-1050">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d28f6-1051">corpo della risposta Hello contiene il valore di count hello come un valore integer formattato in testo normale.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="d28f6-1052">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d28f6-1052">Suggestions</span></span>
<span data-ttu-id="d28f6-1053">Hello **suggerimenti** operazione recupera i suggerimenti in base a input di ricerca parziale.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="d28f6-1054">Viene in genere usato in suggerimenti di ricerca finestre tooprovide durante la digitazione, come gli utenti immettono i termini di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="d28f6-1055">Le richieste di suggerimenti hanno lo scopo di suggerire documenti di destinazione, in modo hello suggerito testo può essere ripetuto se corrispondano a più documenti hello stesso input di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="d28f6-1056">È possibile utilizzare `$select` tooretrieve altri campi (inclusa chiave documento hello) del documento in modo che è possibile stabilire quale documento è origine hello per ogni suggerimento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="d28f6-1057">Un'operazione **Suggestions** viene generata come richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="d28f6-1058">**Quando toouse registra anziché GET**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="d28f6-1059">Quando si utilizza HTTP GET hello toocall **suggerimenti** API, è necessario tenere presente che la lunghezza hello dell'URL di richiesta di hello non può superare 8 KB toobe.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="d28f6-1060">Di solito è sufficiente per la maggior parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="d28f6-1061">Alcune applicazioni generano tuttavia query di dimensioni molto grandi, specialmente le espressioni di filtro OData.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="d28f6-1062">Per queste applicazioni è preferibile usare HTTP POST perché consente filtri di maggiori dimensioni rispetto a GET.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="d28f6-1063">Con POST, un numero di clausole in un filtro hello fattore limitante hello, hello non dimensioni della stringa di filtro non elaborato hello poiché il limite di dimensione richiesta di hello per POST è circa 16 MB.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1064">Anche se limite delle dimensioni richiesta POST hello è molto grande, le espressioni di filtro non possono essere arbitrariamente complesse.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="d28f6-1065">Per altre informazioni sulle limitazioni della complessità dei filtri vedere [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="d28f6-1066">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1066">**Request**</span></span>

<span data-ttu-id="d28f6-1067">Per le richieste del servizio, è necessario usare il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="d28f6-1068">Hello **suggerimenti** richiesta può essere costruita usando i metodi POST o GET hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="d28f6-1069">URI della richiesta Hello Specifica nome hello di hello tooquery di indice.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="d28f6-1070">Parametri, ad esempio al termine di ricerca immesso parzialmente hello, vengono specificati nella stringa di query hello in caso di hello di richieste GET, e nella richiesta di hello richiede il corpo nel caso di hello di POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="d28f6-1071">Come procedura consigliata quando si creano le richieste GET, ricordare troppo[codifica URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) query specifica i parametri quando si chiama hello API REST direttamente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="d28f6-1072">Per le operazioni **Suggestions** sono inclusi i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="d28f6-1073">La codifica URL è consigliata solo nei hello sopra i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="d28f6-1074">Se si codifica URL inavvertitamente hello intera stringa di query (tutti gli elementi dopo hello?), le richieste si interromperanno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="d28f6-1075">Inoltre, la codifica URL è necessaria solo quando si chiama direttamente tramite API REST di ottenere hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="d28f6-1076">Non è necessaria alcuna codifica URL quando si chiama **suggerimenti** utilizzando POST, o quando si utilizza hello [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx), che gestisce la codifica URL per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="d28f6-1077">**Parametri della query**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1077">**Query Parameters**</span></span>

<span data-ttu-id="d28f6-1078">**Suggestions** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="d28f6-1079">Specificare questi parametri nell'URL hello stringa di query quando si chiama **suggerimenti** tramite GET e come proprietà JSON nel corpo della richiesta hello quando si chiama **suggerimenti** tramite POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="d28f6-1080">la sintassi di Hello per alcuni parametri è leggermente diversa tra GET e POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="d28f6-1081">Queste differenze sono riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="d28f6-1082">`search=[string]`-hello toosuggest toouse di testo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="d28f6-1083">Deve essere composto da un minimo di 1 carattere e da un massimo di 100 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="d28f6-1084">`highlightPreTag=[string]`(facoltativo): un tag di stringa che viene aggiunto toosearch riscontri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="d28f6-1085">Deve essere impostato con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1086">Quando si chiama **suggerimenti** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d28f6-1087">`highlightPostTag=[string]`(facoltativo): un tag di stringa che aggiunge toosearch riscontri.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="d28f6-1088">Deve essere impostato con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1089">Quando si chiama **suggerimenti** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d28f6-1090">`suggesterName=[string]`-nome hello di strumento suggerimenti hello come specificato in hello `suggesters` raccolta che fa parte della definizione di indice hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="d28f6-1091">Un elemento `suggester` determina i campi analizzati per i termini di query suggeriti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="d28f6-1092">Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="d28f6-1093">`fuzzy=[boolean]`(facoltativo, il valore predefinito = false), quando questa opzione impostata tootrue API trova i suggerimenti anche se è presente un carattere sostituto o manca nel testo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="d28f6-1094">Anche se offre un'esperienza migliore in alcuni scenari, influisce negativamente sulle prestazioni poiché le ricerche con suggerimenti fuzzy sono più lente e utilizzano più risorse.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="d28f6-1095">`searchFields=[string]`(facoltativo): elenco hello di toosearch di nomi di campo delimitati da virgole per hello il testo di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="d28f6-1096">I campi di destinazione devono essere abilitati per suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="d28f6-1097">`$top=#`(facoltativo, il valore predefinito = 5)-numero di suggerimenti tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="d28f6-1098">Deve essere un numero compreso tra 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1099">Quando si chiama **Suggestions** con POST, questo parametro è denominato `top` invece di `$top`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="d28f6-1100">`$filter=[string]`(facoltativo): un'espressione che filtra i documenti hello considerati per i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1101">Quando si chiama **Suggestions** con POST, questo parametro è denominato `filter` invece di `$filter`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="d28f6-1102">`$orderby=[string]`(facoltativo): un elenco di espressioni delimitato da virgole toosort hello risultati da.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="d28f6-1103">Ogni espressione può essere un nome di campo o una chiamata toohello `geo.distance()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="d28f6-1104">Ogni espressione può essere seguito da `asc` tooindicated crescente, e `desc` tooindicate decrescente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="d28f6-1105">valore predefinito di Hello è l'ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1105">hello default is ascending order.</span></span> <span data-ttu-id="d28f6-1106">È previsto un limite di 32 clausole per `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1107">Quando si chiama **Suggestions** con POST, questo parametro è denominato `orderby` invece di `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="d28f6-1108">`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="d28f6-1109">Se non viene specificato, solo hello chiave di documento e viene restituito il testo di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="d28f6-1110">È possibile richiedere in modo esplicito tutti i campi impostando questo parametro troppo`*`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1111">Quando si chiama **Suggestions** con POST, questo parametro è denominato `select` invece di `$select`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="d28f6-1112">`minimumCoverage`(facoltativo, per impostazione predefinita too80) - un numero compreso tra 0 e 100 che indica la percentuale hello dell'indice hello che deve essere analizzata da una query di suggerimenti affinché hello query toobe segnalati come completati.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="d28f6-1113">Per impostazione predefinita, deve essere disponibile almeno l'80% di indice hello o `Suggest` restituirà il codice di stato HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="d28f6-1114">Se si imposta `minimumCoverage` e `Suggest` ha esito positivo, verrà restituito HTTP 200 e includere un `@search.coverage` valore nella risposta hello indicando la percentuale hello dell'indice hello che è stato incluso nella query hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="d28f6-1115">Se il valore di tooa di parametro è minore di 100 può risultare utile per garantire la disponibilità di ricerca neanche per i servizi con una sola replica.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="d28f6-1116">Tuttavia, non tutti i suggerimenti corrispondenti vengono garantiti toobe presenti nei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="d28f6-1117">Tenere presente è più importante tooyour di disponibilità, quindi di procedure non toolower `minimumCoverage` sotto il relativo valore predefinito 80.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="d28f6-1118">`api-version=[string]` (elemento obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="d28f6-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="d28f6-1119">versione di anteprima Hello è `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d28f6-1120">Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d28f6-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d28f6-1121">Nota: Per questa operazione, hello `api-version` è specificato come un parametro di query nell'URL hello indipendentemente dal fatto se si chiama **suggerimenti** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="d28f6-1122">**Intestazioni della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1122">**Request Headers**</span></span>

<span data-ttu-id="d28f6-1123">Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo</span><span class="sxs-lookup"><span data-stu-id="d28f6-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="d28f6-1124">`api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="d28f6-1125">È un valore di stringa, univoco tooyour URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="d28f6-1126">Hello **suggerimenti** richiesta può specificare una chiave amministratore o una chiave di query come hello `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="d28f6-1127">È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="d28f6-1128">È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="d28f6-1129">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d28f6-1130">**Corpo della richiesta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1130">**Request Body**</span></span>

<span data-ttu-id="d28f6-1131">Per GET: nessuno.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1131">For GET: None.</span></span>

<span data-ttu-id="d28f6-1132">Per POST:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="d28f6-1133">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1133">**Response**</span></span>

<span data-ttu-id="d28f6-1134">Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d28f6-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="d28f6-1135">Se l'opzione di proiezione di hello tooretrieve utilizzato i campi che sono inclusi in ogni elemento della matrice hello:</span><span class="sxs-lookup"><span data-stu-id="d28f6-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="d28f6-1136">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="d28f6-1136">**Example**</span></span>

<span data-ttu-id="d28f6-1137">Recuperare 5 suggerimenti, in cui hello input di ricerca parziale è "lux"</span><span class="sxs-lookup"><span data-stu-id="d28f6-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
