---
title: risultati della ricerca di toopage aaaHow in ricerca di Azure | Documenti Microsoft
description: "L’impaginazione in Ricerca di Azure, un servizio di ricerca ospitato sul cloud in Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="9b3b7-103">La vista dei risultati ricerca toopage in ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="9b3b7-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="9b3b7-104">Questo articolo fornisce istruzioni su come toouse hello API REST di Azure ricerca tooimplement elementi standard di una ricerca di pagina dei risultati, ad esempio nei conteggi totali, il recupero di documenti, ordinamento e la navigazione.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="9b3b7-105">In ogni caso riportato di seguito, le opzioni relative alla pagina che contribuiscono a dati o pagina di risultati di ricerca tooyour vengono specificate mediante hello [ricerca nel documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour le richieste inviate il servizio di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="9b3b7-106">Le richieste includono un comando GET, percorso e che servizio hello ciò che viene richiesto di indicare i parametri di query e come tooformulate hello risposta.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b7-107">Una richiesta valida include diversi elementi, ad esempio URL e percorso del servizio, verbo HTTP, `api-version`, e così via.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="9b3b7-108">Per ragioni di brevità, ci tagliati hello esempi toohighlight hello solo la sintassi toopagination pertinente.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="9b3b7-109">Vedere hello [API REST di Azure ricerca](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentazione per informazioni dettagliate sulla sintassi della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="9b3b7-110">Corrispondenze totali e conteggi delle pagine</span><span class="sxs-lookup"><span data-stu-id="9b3b7-110">Total hits and Page Counts</span></span>
<span data-ttu-id="9b3b7-111">Visualizzazione hello totale numero di risultati restituiti da una query e quindi vengono restituiti i risultati in blocchi più piccoli, è fondamentale toovirtually tutte le pagine di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="9b3b7-112">In ricerca di Azure, utilizzare hello `$count`, `$top`, e `$skip` tooreturn parametri questi valori.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="9b3b7-113">Hello esempio seguente viene illustrato un esempio di richiesta per Totale riscontri, restituito come `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="9b3b7-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="9b3b7-114">Recuperare i documenti in gruppi di 15 e visualizzare Totale riscontri hello, a partire dalla prima pagina hello:</span><span class="sxs-lookup"><span data-stu-id="9b3b7-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="9b3b7-115">L'impaginazione risultati richiede entrambi `$top` e `$skip`, dove `$top` specifica quanti elementi tooreturn in un batch, e `$skip` specifica quanti elementi tooskip.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="9b3b7-116">In hello seguente esempio, ogni pagina sono visualizzati hello elementi successivamente 15, indicato da salti incrementale di hello in hello `$skip` parametro.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="9b3b7-117">Layout</span><span class="sxs-lookup"><span data-stu-id="9b3b7-117">Layout</span></span>
<span data-ttu-id="9b3b7-118">In una pagina di risultati di ricerca, è opportuno tooshow un'immagine di anteprima, un sottoinsieme dei campi e una pagina di collegamento tooa completa del prodotto.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="9b3b7-119">In ricerca di Azure, è consigliabile usare `$select` e una ricerca dei comandi tooimplement questa esperienza.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="9b3b7-120">tooreturn un sottoinsieme dei campi per un layout affiancato:</span><span class="sxs-lookup"><span data-stu-id="9b3b7-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="9b3b7-121">Le immagini e file multimediali non sono direttamente ricercabili e devono essere archiviati in un'altra piattaforma di archiviazione, ad esempio l'archiviazione Blob di Azure, i costi tooreduce.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="9b3b7-122">Indice di hello e documenti, definire un campo che archivia l'indirizzo URL hello di contenuto esterno hello.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="9b3b7-123">È quindi possibile utilizzare il campo hello come riferimento a un'immagine.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="9b3b7-124">immagine di toohello Hello URL deve essere nel documento hello.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="9b3b7-125">tooretrieve pagina una descrizione del prodotto per un **onClick** evento, utilizzare [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass nella chiave hello di hello documento tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="9b3b7-126">Hello è di tipo chiave hello `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="9b3b7-127">In questo esempio è *246810*.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="9b3b7-128">Ordinare per pertinenza, classificazione o prezzo</span><span class="sxs-lookup"><span data-stu-id="9b3b7-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="9b3b7-129">Tipi di ordinamento spesso toorelevance predefinito, ma è comuni tipi di ordinamento alternativo toomake immediatamente disponibili in modo che i clienti possono riassegnare rapidamente risultati esistenti in un ordine di rango diverso.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="9b3b7-130">In ricerca di Azure, ordinamento si basa su hello `$orderby` per tutti i campi indicizzati come espressione`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="9b3b7-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="9b3b7-131">La pertinenza è fortemente associata ai profili di punteggio.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="9b3b7-132">È possibile utilizzare hello punteggio predefinito, che si basa sull'ordinamento di toorank statistiche e di analisi del testo, tutti i risultati con punteggi maggiori succedendo toodocuments con corrispondenze più o maggiore di un termine di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="9b3b7-133">Sono in genere associati tipi di ordinamento alternativo **onClick** gli eventi che chiamano il metodo tooa che compila ordinamento hello.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="9b3b7-134">Si consideri, ad esempio, questo elemento di pagina:</span><span class="sxs-lookup"><span data-stu-id="9b3b7-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="9b3b7-135">Creare un metodo che accetta l'opzione di ordinamento hello selezionata come input e restituisce un elenco ordinato per i criteri di hello associata a tale opzione.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="9b3b7-136">Mentre il punteggio predefinito hello è sufficiente per molti scenari, è consigliabile basare pertinenza su un profilo di punteggio personalizzato invece.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="9b3b7-137">Un profilo di punteggio personalizzato offre un modo tooboost, gli elementi che sono più conveniente tooyour business.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="9b3b7-138">Vedere [Aggiungere un profilo di punteggio](http://msdn.microsoft.com/library/azure/dn798928.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="9b3b7-139">Esplorazione in base a facet</span><span class="sxs-lookup"><span data-stu-id="9b3b7-139">Faceted navigation</span></span>
<span data-ttu-id="9b3b7-140">Spostamento di ricerca è comune in una pagina di risultati, che spesso si trova nel lato hello o superiore di una pagina.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="9b3b7-141">In Ricerca di Azure, l’esplorazione basata su facet fornisce una ricerca autoindirizzata in base a filtri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="9b3b7-142">Per maggiori informazioni vendere [Esplorazione basata su facet in Ricerca di Azure](search-faceted-navigation.md) .</span><span class="sxs-lookup"><span data-stu-id="9b3b7-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="9b3b7-143">Filtri a livello di pagina hello</span><span class="sxs-lookup"><span data-stu-id="9b3b7-143">Filters at hello page level</span></span>
<span data-ttu-id="9b3b7-144">Se la progettazione della soluzione include pagine di ricerca dedicato per tipi specifici di contenuto (ad esempio, un'applicazione di vendita al dettaglio online con reparti elencati nella parte superiore di hello della pagina hello), è possibile inserire un'espressione di filtro insieme a un **onClick** evento tooopen una pagina in uno stato prefiltrato.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="9b3b7-145">È possibile inviare un filtro con o senza espressione di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="9b3b7-146">Ad esempio, hello richiesta seguente filtrerà marca, restituendo solo i documenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="9b3b7-147">Vedere [Ricerca nei documenti (API di Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) per altre informazioni sulle espressioni `$filter`.</span><span class="sxs-lookup"><span data-stu-id="9b3b7-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="9b3b7-148">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9b3b7-148">See Also</span></span>
* [<span data-ttu-id="9b3b7-149">API REST per il servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="9b3b7-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="9b3b7-150">Operazioni sugli indici</span><span class="sxs-lookup"><span data-stu-id="9b3b7-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="9b3b7-151">Operazioni sui documenti</span><span class="sxs-lookup"><span data-stu-id="9b3b7-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="9b3b7-152">Video ed esercitazioni su Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="9b3b7-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="9b3b7-153">Esplorazione in base a facet in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="9b3b7-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
