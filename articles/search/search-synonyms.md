---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentazione preliminare per funzionalità di sinonimi (anteprima) hello, esposte in hello API REST di ricerca di Azure."
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
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="0d952-102">Sinonimi in Ricerca di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="0d952-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="0d952-103">Sinonimi nei motori di ricerca associano equivalente termini che si espandono in modo implicito ambito hello di una query, senza utente hello con tooactually fornire termine hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="0d952-104">Ad esempio, il termine specificato hello "dog" e le associazioni di sinonimi di "canino" e "Cucciolo", tutti i documenti contenenti "dog", "canino" o "Cucciolo" saranno compreso ambito hello di query di hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="0d952-105">In Ricerca di Azure l'espansione sinonimica viene eseguita in fase di query.</span><span class="sxs-lookup"><span data-stu-id="0d952-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="0d952-106">È possibile aggiungere sinonimo mappe tooa servizio senza operazioni tooexisting interruzioni.</span><span class="sxs-lookup"><span data-stu-id="0d952-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="0d952-107">È possibile aggiungere un **synonymMaps** definizione di campo di proprietà tooa senza indice hello toorebuild.</span><span class="sxs-lookup"><span data-stu-id="0d952-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="0d952-108">Per altre informazioni, vedere [Aggiornare un indice](https://docs.microsoft.com/rest/api/searchservice/update-index) .</span><span class="sxs-lookup"><span data-stu-id="0d952-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="0d952-109">Disponibilità delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="0d952-109">Feature availability</span></span>

<span data-ttu-id="0d952-110">sinonimi Hello funzionalità è attualmente in anteprima e solo supportati in hello api-versione di anteprima più recente (api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="0d952-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="0d952-111">Non è attualmente disponibile alcun supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d952-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="0d952-112">Poiché viene specificata una versione di hello API richiesta hello, è possibile toocombine disponibile a livello generale (GA) e le API in anteprima in hello stessa app.</span><span class="sxs-lookup"><span data-stu-id="0d952-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="0d952-113">Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="0d952-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="0d952-114">La modalità di ricerca di sinonimi toouse in Azure</span><span class="sxs-lookup"><span data-stu-id="0d952-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="0d952-115">In ricerca di Azure, supporto di sinonimi è basato sulle mappe sinonimo di definire e caricare il servizio tooyour.</span><span class="sxs-lookup"><span data-stu-id="0d952-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="0d952-116">Queste mappe costituiscono una risorsa indipendente (ad esempio indici o origini dati) e possono essere utilizzate da qualsiasi campo ricercabile in qualsiasi indice nel servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0d952-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="0d952-117">Le mappe sinonimiche e gli indici vengono mantenuti in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="0d952-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="0d952-118">Dopo aver definito una mappa di sinonimo e caricarlo tooyour servizio, è possibile abilitare funzionalità di sinonimo hello su un campo tramite l'aggiunta di una nuova proprietà denominata **synonymMaps** nella definizione di campo hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="0d952-119">Creazione, aggiornamento ed eliminazione di che una mappa di sinonimo è sempre un'operazione dell'intero documento, vale a dire che è possibile creare, aggiornare o eliminare le parti della mappa sinonimo hello in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="0d952-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="0d952-120">Se si aggiorna anche una singola voce è necessario ripetere il caricamento.</span><span class="sxs-lookup"><span data-stu-id="0d952-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="0d952-121">L'aggiunta di sinonimi in un'applicazione di ricerca è una procedura in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="0d952-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="0d952-122">Aggiungere un servizio di ricerca sinonimo mappa tooyour tramite hello API riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d952-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="0d952-123">Nella definizione dell'indice hello, configurare una mappa di sinonimo hello toouse campo ricercabile.</span><span class="sxs-lookup"><span data-stu-id="0d952-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="0d952-124">API di risorsa SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="0d952-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="0d952-125">Aggiungere o aggiornare una mappa sinonimica nel servizio tramite POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="0d952-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="0d952-126">Vengono caricate sinonimo mappe servizio toohello tramite POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="0d952-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="0d952-127">Ogni regola deve essere delimitato da hello carattere di nuova riga ('\n').</span><span class="sxs-lookup"><span data-stu-id="0d952-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="0d952-128">È possibile definire too5, 000 regole per ogni sinonimo mappa in un servizio gratuito e 10.000 regole in tutti gli altri SKU.</span><span class="sxs-lookup"><span data-stu-id="0d952-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="0d952-129">Ogni regola può essere composto too20 espansioni.</span><span class="sxs-lookup"><span data-stu-id="0d952-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="0d952-130">In questa versione di anteprima mappe sinonimo devono essere nel formato Solr Apache hello viene spiegato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d952-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="0d952-131">Se si dispone di un dizionario di sinonimo esistente in un formato diverso e si desidera toouse direttamente, Saremmo lieti di sapere su [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="0d952-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="0d952-132">È possibile creare una nuova mappa sinonimo utilizzando POST HTTP, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0d952-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="0d952-133">In alternativa, è possibile usare PUT e specificare nome della mappa sinonimo hello in hello URI.</span><span class="sxs-lookup"><span data-stu-id="0d952-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="0d952-134">Se hello sinonimo mappa non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="0d952-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="0d952-135">Formato dei sinonimi Apache Solr</span><span class="sxs-lookup"><span data-stu-id="0d952-135">Apache Solr synonym format</span></span>

<span data-ttu-id="0d952-136">formato Solr Hello supporta i mapping di sinonimo equivalente ed esplicite.</span><span class="sxs-lookup"><span data-stu-id="0d952-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="0d952-137">Specifica del filtro toohello Apri origine sinonimo di Solr Apache, descritte in questo documento di rispettare le regole di mapping: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="0d952-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="0d952-138">Di seguito è riportata una regola di esempio per sinonimi equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0d952-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="0d952-139">Con la regola di hello è precedente, una query di ricerca 'USA' espanderà troppo "USA" o "United States" o "Stati Uniti d'America".</span><span class="sxs-lookup"><span data-stu-id="0d952-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="0d952-140">Il mapping esplicito è indicato da una freccia "=>".</span><span class="sxs-lookup"><span data-stu-id="0d952-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="0d952-141">Quando specificato, una sequenza di termine di una query di ricerca che corrisponde a hello lato sinistro di "= >" verrà sostituito con alternative hello sul lato destro hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="0d952-142">Dato regola hello, "Washington", "Washington" query di ricerca</span><span class="sxs-lookup"><span data-stu-id="0d952-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="0d952-143">o "WA" verrà tutti riscritto troppo "WA".</span><span class="sxs-lookup"><span data-stu-id="0d952-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="0d952-144">Mapping esplicito applica in direzione hello specificata e non riscrivere la query di hello "WA" troppo "Washington" in questo caso.</span><span class="sxs-lookup"><span data-stu-id="0d952-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="0d952-145">Elencare le mappe sinonimiche del proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="0d952-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="0d952-146">Aggiungere una mappa sinonimica al proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="0d952-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="0d952-147">Eliminare una mappa sinonimica dal proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="0d952-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="0d952-148">Nella definizione dell'indice hello, configurare una mappa di sinonimo hello toouse campo ricercabile.</span><span class="sxs-lookup"><span data-stu-id="0d952-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="0d952-149">Una nuova proprietà di campo **synonymMaps** può essere utilizzato toospecify toouse di mappa un sinonimo per un campo ricercabile.</span><span class="sxs-lookup"><span data-stu-id="0d952-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="0d952-150">Le mappe di sinonimo sono risorse a livello di servizio e a cui fa riferimento da qualsiasi campo di un indice nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

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

<span data-ttu-id="0d952-151">**synonymMaps** può essere specificato per i campi ricercabili hello tipo di 'Edm. String' o 'Collection'.</span><span class="sxs-lookup"><span data-stu-id="0d952-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="0d952-152">In questa versione di anteprima è possibile avere solo una mappa sinonimica per campo.</span><span class="sxs-lookup"><span data-stu-id="0d952-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="0d952-153">Se si desidera toouse più mappe sinonimo, Saremmo lieti di sapere su [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="0d952-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="0d952-154">Impatto dei sinonimi sulle altre funzionalità di ricerca</span><span class="sxs-lookup"><span data-stu-id="0d952-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="0d952-155">funzionalità di sinonimi Hello riscrive query originale di hello con sinonimi con hello operatore OR.</span><span class="sxs-lookup"><span data-stu-id="0d952-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="0d952-156">Per questo motivo, hit evidenziazione e i profili di punteggio considerano termine originale hello e sinonimi come equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0d952-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="0d952-157">Funzionalità di sinonimo applica toosearch query e non si applica toofilters o i facet.</span><span class="sxs-lookup"><span data-stu-id="0d952-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="0d952-158">Analogamente, i suggerimenti sono basati solo sul termine originale hello; sinonimo corrispondenze non vengono visualizzati in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0d952-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="0d952-159">Non sono applicabili toowildcard i termini di ricerca; espansioni sinonimo prefisso, fuzzy e i termini di regex non sono espansi.</span><span class="sxs-lookup"><span data-stu-id="0d952-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="0d952-160">Suggerimenti per la creazione di una mappa sinonimica</span><span class="sxs-lookup"><span data-stu-id="0d952-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="0d952-161">Una mappa sinonimica concisa e ben progettata è più efficiente rispetto a un elenco completo delle possibili corrispondenze.</span><span class="sxs-lookup"><span data-stu-id="0d952-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="0d952-162">Dizionari eccessivamente grandi dimensioni o complessi richiedere più tempo tooparse e influiscono sulla latenza delle query hello se query hello espande toomany sinonimi.</span><span class="sxs-lookup"><span data-stu-id="0d952-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="0d952-163">Invece di stima in cui potrebbero essere utilizzati i termini, è possibile ottenere termini hello tramite un [report di analisi del traffico di ricerca](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="0d952-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="0d952-164">Come esercizio preliminary sia una convalida, abilitare e quindi verrà trarre vantaggio da una corrispondenza di sinonimo, questo tooprecisely report determinare quali condizioni di utilizzo e quindi continuare toouse come convalida che la mappa di sinonimo produce un risultato migliore.</span><span class="sxs-lookup"><span data-stu-id="0d952-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="0d952-165">Nel report hello predefinito, hello riquadri "query di ricerca più comuni" e "query di ricerca Zero risultati" fornirà hello le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="0d952-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="0d952-166">È possibile creare più mappe sinonimiche per l'applicazione di ricerca (ad esempio in base alla lingua se l'applicazione supporta clienti multilingue).</span><span class="sxs-lookup"><span data-stu-id="0d952-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="0d952-167">Attualmente un campo può usarne una sola.</span><span class="sxs-lookup"><span data-stu-id="0d952-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="0d952-168">È possibile aggiornare la proprietà synonymMaps di un campo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="0d952-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d952-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d952-169">Next Steps</span></span>

- <span data-ttu-id="0d952-170">Se si dispone di un indice esistente in un ambiente di sviluppo (non di produzione), provare a utilizzare toosee un dizionario di piccole dimensioni come aggiunta hello di sinonimi cambia hello un'esperienza di ricerca, compreso l'impatto sui profili di punteggio, hit evidenziazione e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="0d952-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="0d952-171">[Abilita ricerca traffico analitica](search-traffic-analytics.md) e utilizzare hello predefinite di report di Power BI toolearn le parole usate hello la maggior parte e quali quelli restituito zero documenti.</span><span class="sxs-lookup"><span data-stu-id="0d952-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="0d952-172">Grazie a queste informazioni, rivedere i sinonimi tooinclude dizionario hello per le query produttivo che devono essere risoluzione toodocuments nell'indice.</span><span class="sxs-lookup"><span data-stu-id="0d952-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
