---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentazione preliminare per la funzionalità relativa ai sinonimi (anteprima) esposta nell'API REST di Ricerca di Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="e909a-102">Sinonimi in Ricerca di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="e909a-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="e909a-103">La funzionalità relativa ai sinonimi nei motori di ricerca associa termini equivalenti, che espandono in modo implicito l'ambito di una query, senza che l'utente debba fornire effettivamente il termine.</span><span class="sxs-lookup"><span data-stu-id="e909a-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="e909a-104">Ad esempio, dato il termine "cane" e le associazioni sinonimiche "canino" e "cucciolo", tutti i documenti contenenti "cane", "canino" o "cucciolo" saranno inclusi nella query.</span><span class="sxs-lookup"><span data-stu-id="e909a-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="e909a-105">In Ricerca di Azure l'espansione sinonimica viene eseguita in fase di query.</span><span class="sxs-lookup"><span data-stu-id="e909a-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="e909a-106">È possibile aggiungere mappe sinonimiche a un servizio senza compromettere le operazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="e909a-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="e909a-107">La proprietà **synonymMaps** può essere aggiunta alla definizione di un campo senza dover ricompilare l'indice.</span><span class="sxs-lookup"><span data-stu-id="e909a-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="e909a-108">Per altre informazioni, vedere [Aggiornare un indice](https://docs.microsoft.com/rest/api/searchservice/update-index) .</span><span class="sxs-lookup"><span data-stu-id="e909a-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="e909a-109">Disponibilità delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="e909a-109">Feature availability</span></span>

<span data-ttu-id="e909a-110">La funzionalità relativa ai sinonimi è attualmente disponibile in anteprima ed è supportata solo nelle versioni API di anteprima più recenti (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="e909a-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="e909a-111">Non è attualmente disponibile alcun supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e909a-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="e909a-112">Poiché la versione dell'API è specificata nella richiesta, è possibile combinare API disponibili a livello generale (GA) e di anteprima nella stessa applicazione.</span><span class="sxs-lookup"><span data-stu-id="e909a-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="e909a-113">Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="e909a-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="e909a-114">Come usare i sinonimi in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="e909a-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="e909a-115">In Ricerca di Azure il supporto dei sinonimi si basa sulle mappe sinonimiche definite e caricate nel servizio.</span><span class="sxs-lookup"><span data-stu-id="e909a-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="e909a-116">Queste mappe costituiscono una risorsa indipendente (ad esempio indici o origini dati) e possono essere utilizzate da qualsiasi campo ricercabile in qualsiasi indice nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e909a-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="e909a-117">Le mappe sinonimiche e gli indici vengono mantenuti in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="e909a-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="e909a-118">Dopo aver definito una mappa sinonimica e averla caricata nel servizio, è possibile abilitare la funzionalità relativa ai sinonimi per un campo tramite l'aggiunta della nuova proprietà **synonymMaps** nella definizione del campo.</span><span class="sxs-lookup"><span data-stu-id="e909a-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="e909a-119">La creazione, l'aggiornamento e l'eliminazione di una mappa sinonimica è sempre un'operazione che riguarda l'intero documento, perciò non è possibile creare, aggiornare o eliminare parti della mappa sinonimica in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="e909a-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="e909a-120">Se si aggiorna anche una singola voce è necessario ripetere il caricamento.</span><span class="sxs-lookup"><span data-stu-id="e909a-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="e909a-121">L'aggiunta di sinonimi in un'applicazione di ricerca è una procedura in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="e909a-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="e909a-122">Aggiungere una mappa sinonimica al servizio di ricerca tramite le API indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="e909a-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="e909a-123">Configurare un campo ricercabile per l'uso della mappa sinonimica nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="e909a-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="e909a-124">API di risorsa SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="e909a-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="e909a-125">Aggiungere o aggiornare una mappa sinonimica nel servizio tramite POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="e909a-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="e909a-126">Le mappe sinonimiche vengono caricate nel servizio tramite POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="e909a-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="e909a-127">Ogni regola deve essere delimitata dal carattere nuova riga ('\n').</span><span class="sxs-lookup"><span data-stu-id="e909a-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="e909a-128">È possibile definire fino a 5.000 regole per ogni mappa sinonimica in un servizio gratuito e 10.000 regole in tutti gli altri SKU.</span><span class="sxs-lookup"><span data-stu-id="e909a-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="e909a-129">Ogni regola può avere fino a 20 espansioni.</span><span class="sxs-lookup"><span data-stu-id="e909a-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="e909a-130">In questa anteprima le mappe sinonimiche devono essere nel formato Apache Solr descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="e909a-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="e909a-131">Se si ha un dizionario di sinonimi in un formato diverso e si desidera usarlo direttamente, segnalarlo mediante [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="e909a-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="e909a-132">È possibile creare una nuova mappa sinonimica usando HTTP POST, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e909a-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="e909a-133">In alternativa è possibile usare PUT e specificare il nome della mappa sinonimica nell'URI.</span><span class="sxs-lookup"><span data-stu-id="e909a-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="e909a-134">Se la mappa sinonimica non esiste, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="e909a-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="e909a-135">Formato dei sinonimi Apache Solr</span><span class="sxs-lookup"><span data-stu-id="e909a-135">Apache Solr synonym format</span></span>

<span data-ttu-id="e909a-136">Il formato Solr supporta il mapping sinonimico equivalente ed esplicito.</span><span class="sxs-lookup"><span data-stu-id="e909a-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="e909a-137">Le regole del mapping aderiscono alla specifica di filtro dei sinonimi open source di Apache Solr descritta in questo documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="e909a-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="e909a-138">Di seguito è riportata una regola di esempio per sinonimi equivalenti.</span><span class="sxs-lookup"><span data-stu-id="e909a-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="e909a-139">Con la regola precedente, la query di ricerca "USA" si espanderà in "USA" OR "Stati Uniti" OR "Stati Uniti d'America".</span><span class="sxs-lookup"><span data-stu-id="e909a-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="e909a-140">Il mapping esplicito è indicato da una freccia "=>".</span><span class="sxs-lookup"><span data-stu-id="e909a-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="e909a-141">Quando è specificato, una sequenza di termini di una query di ricerca che corrisponde al lato sinistro di "= >" verrà sostituita con le alternative sul lato destro.</span><span class="sxs-lookup"><span data-stu-id="e909a-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="e909a-142">Data la regola seguente, le query di ricerca "Washington", "Wash."</span><span class="sxs-lookup"><span data-stu-id="e909a-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="e909a-143">o "WA" saranno riscritte tutte come "WA".</span><span class="sxs-lookup"><span data-stu-id="e909a-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="e909a-144">Il mapping esplicito si applica solo nella direzione specificata e, in questo caso, non riscrivere la query "WA" come "Washington".</span><span class="sxs-lookup"><span data-stu-id="e909a-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="e909a-145">Elencare le mappe sinonimiche del proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="e909a-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="e909a-146">Aggiungere una mappa sinonimica al proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="e909a-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="e909a-147">Eliminare una mappa sinonimica dal proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="e909a-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="e909a-148">Configurare un campo ricercabile per l'uso della mappa sinonimica nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="e909a-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="e909a-149">La nuova proprietà di campo **synonymMaps** consente di specificare una mappa sinonimica da usare per un campo ricercabile.</span><span class="sxs-lookup"><span data-stu-id="e909a-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="e909a-150">Le mappe sinonimiche sono risorse a livello di servizio e possono essere referenziate da qualsiasi campo di un indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="e909a-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="e909a-151">È possibile specificare **synonymMaps** per i campi ricercabili di tipo "Edm. String" o "Collection".</span><span class="sxs-lookup"><span data-stu-id="e909a-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="e909a-152">In questa versione di anteprima è possibile avere solo una mappa sinonimica per campo.</span><span class="sxs-lookup"><span data-stu-id="e909a-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="e909a-153">Se si vuole usare più mappe sinonimiche, segnalarlo tramite [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="e909a-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="e909a-154">Impatto dei sinonimi sulle altre funzionalità di ricerca</span><span class="sxs-lookup"><span data-stu-id="e909a-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="e909a-155">La funzionalità relativa ai sinonimi riscrive la query originale con sinonimi usando l'operatore OR.</span><span class="sxs-lookup"><span data-stu-id="e909a-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="e909a-156">Per questo motivo, l'evidenziazione dei risultati e i profili di punteggio trattano il termine originale e i sinonimi come equivalenti.</span><span class="sxs-lookup"><span data-stu-id="e909a-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="e909a-157">La funzionalità relativa ai sinonimi si applica alle query di ricerca e non ai filtri o ai facet.</span><span class="sxs-lookup"><span data-stu-id="e909a-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="e909a-158">Analogamente, i suggerimenti sono basati solo sul termine originale; le corrispondenze sinonimiche non compaiono nella risposta.</span><span class="sxs-lookup"><span data-stu-id="e909a-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="e909a-159">Le espansioni dei sinonimi non si applicano ai termini di ricerca con caratteri jolly; i termini con prefisso, fuzzy e regex non vengono espansi.</span><span class="sxs-lookup"><span data-stu-id="e909a-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="e909a-160">Suggerimenti per la creazione di una mappa sinonimica</span><span class="sxs-lookup"><span data-stu-id="e909a-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="e909a-161">Una mappa sinonimica concisa e ben progettata è più efficiente rispetto a un elenco completo delle possibili corrispondenze.</span><span class="sxs-lookup"><span data-stu-id="e909a-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="e909a-162">I dizionari eccessivamente grandi o complessi richiedono più tempo di analisi e influenzano la latenza della query se la query si espande in molti sinonimi.</span><span class="sxs-lookup"><span data-stu-id="e909a-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="e909a-163">Invece di indovinare quali termini potrebbero essere usati, è possibile ottenere i termini effettivi tramite un [report di analisi del traffico di ricerca](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="e909a-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="e909a-164">Come esercizio sia preliminare che di convalida, abilitare e usare questo report per determinare con precisione quali termini trarranno vantaggio da una corrispondenza sinonimica e quindi continuare a usarlo per verificare che la mappa sinonimica sta generando risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="e909a-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="e909a-165">Nel report predefinito il riquadro delle query di ricerca più comuni e il riquadro delle query di ricerca senza risultati forniranno le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="e909a-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="e909a-166">È possibile creare più mappe sinonimiche per l'applicazione di ricerca (ad esempio in base alla lingua se l'applicazione supporta clienti multilingue).</span><span class="sxs-lookup"><span data-stu-id="e909a-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="e909a-167">Attualmente un campo può usarne una sola.</span><span class="sxs-lookup"><span data-stu-id="e909a-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="e909a-168">È possibile aggiornare la proprietà synonymMaps di un campo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e909a-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e909a-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e909a-169">Next Steps</span></span>

- <span data-ttu-id="e909a-170">Se si ha un indice esistente in un ambiente di sviluppo (non di produzione), provare con un piccolo dizionario per vedere come l'aggiunta di sinonimi cambia l'esperienza di ricerca, compreso l'impatto sui profili di punteggio, l'evidenziazione dei risultati e i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="e909a-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="e909a-171">[Abilitare l'analisi del traffico di ricerca](search-traffic-analytics.md) e usare i report predefiniti di Power BI per ottenere informazioni su quali termini sono più utilizzati e quali non restituiscono documenti.</span><span class="sxs-lookup"><span data-stu-id="e909a-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="e909a-172">In base a queste informazioni, modificare il dizionario per includere i sinonimi per le query improduttive che devono risolversi in documenti nell'indice.</span><span class="sxs-lookup"><span data-stu-id="e909a-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
