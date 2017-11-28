---
title: aaaSearch Analitica di traffico per la ricerca di Azure | Documenti Microsoft
description: Abilitare analitica di traffico di ricerca per un servizio di ricerca cloud ospitato in Microsoft Azure, approfondimenti toounlock su utenti e i dati di ricerca di Azure.
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="0a57d-103">Analisi del traffico di ricerca</span><span class="sxs-lookup"><span data-stu-id="0a57d-103">What is search traffic analytics</span></span>
<span data-ttu-id="0a57d-104">Analisi del traffico di ricerca è un modello per l'implementazione di un ciclo di feedback per il servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="0a57d-105">Questo modello viene descritto come toocollect con Application Insights, leader del settore per il monitoraggio di servizi in più piattaforme e i dati necessari hello.</span><span class="sxs-lookup"><span data-stu-id="0a57d-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="0a57d-106">Analisi del traffico di ricerca consente di ottenere visibilità nel servizio di ricerca e informazioni dettagliate su utenti e relativo comportamento.</span><span class="sxs-lookup"><span data-stu-id="0a57d-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="0a57d-107">Con i dati relativi a ciò che gli utenti potranno scegliere, è possibile toomake decisioni che consentono di migliorare ulteriormente l'esperienza di ricerca e tooback off quando i risultati di hello sono non previsto.</span><span class="sxs-lookup"><span data-stu-id="0a57d-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="0a57d-108">Ricerca di Azure offre una soluzione di telemetria che integra Azure Application Insights e Power BI tooprovide approfondita di monitoraggio e rilevamento.</span><span class="sxs-lookup"><span data-stu-id="0a57d-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="0a57d-109">Poiché l'interazione con ricerca di Azure solo tramite le API, dati di telemetria hello deve essere implementata dagli sviluppatori di hello utilizzo della ricerca, attenendosi alle istruzioni hello in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="0a57d-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="0a57d-110">Identificare i dati di ricerca rilevanti hello</span><span class="sxs-lookup"><span data-stu-id="0a57d-110">Identify hello relevant search data</span></span>

<span data-ttu-id="0a57d-111">le metriche di ricerca utili di toohave, è necessario toolog alcuni segnali da utenti hello hello applicazione di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="0a57d-112">Questi segnali indicano il contenuto che gli utenti sono interessati a e che essi considerano deve tootheir pertinente.</span><span class="sxs-lookup"><span data-stu-id="0a57d-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="0a57d-113">I segnali necessari per Analisi del traffico di ricerca sono due:</span><span class="sxs-lookup"><span data-stu-id="0a57d-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="0a57d-114">Eventi di ricerca generati dagli utenti. Sono interessanti solo le query di ricerca avviate da un utente.</span><span class="sxs-lookup"><span data-stu-id="0a57d-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="0a57d-115">Ricerca richieste utilizzate toopopulate facet, contenuto aggiuntivo o qualsiasi informazione interne, non sono importanti e inclinare e definire i risultati.</span><span class="sxs-lookup"><span data-stu-id="0a57d-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="0a57d-116">Eventi click generato dall'utente: eseguiti i clic in questo documento, si fa riferimento tooa utente la selezione di un risultato di ricerca particolare restituito da una query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="0a57d-117">Un clic in genere indica che un documento è un risultato rilevante per una specifica query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="0a57d-118">Collegando gli eventi di ricerca e fare clic con un id di correlazione, è possibile tooanalyze i comportamenti di hello di utenti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a57d-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="0a57d-119">Queste informazioni di ricerca sono tooobtain impossibili con solo i log di traffico di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="0a57d-120">Come tooimplement ricerca analitica di traffico</span><span class="sxs-lookup"><span data-stu-id="0a57d-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="0a57d-121">segnali Hello riportato in hello precedente sezione deve essere raccolti da un'applicazione hello ricerca come hello utente interagisce con esso.</span><span class="sxs-lookup"><span data-stu-id="0a57d-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="0a57d-122">Application Insights è una soluzione di monitoraggio estensibile, disponibile per più piattaforme, con opzioni di strumentazione flessibili.</span><span class="sxs-lookup"><span data-stu-id="0a57d-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="0a57d-123">Utilizzo di Application Insights consente di sfruttare i vantaggi dei report di ricerca di Power BI hello creato da un'analisi dei dati hello toomake ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a57d-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="0a57d-124">In hello [portale](https://portal.azure.com) pagina per il servizio di ricerca di Azure, pannello di hello Analitica di traffico di ricerca contiene un foglio informativo per questo modello di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="0a57d-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="0a57d-125">È anche possibile selezionare o creare una risorsa di Application Insights e visualizzare i dati necessari hello, in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="0a57d-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Istruzioni per Analisi del traffico di ricerca][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="0a57d-127">1. Selezionare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a57d-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="0a57d-128">È necessario tooselect un toouse di risorsa di Application Insights o crearne uno, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="0a57d-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="0a57d-129">È possibile utilizzare una risorsa che è già in uso toolog hello richiesto eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0a57d-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="0a57d-130">Quando si crea una nuova risorsa di Application Insights, sono validi tutti i tipi di applicazione per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="0a57d-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="0a57d-131">Selezionare hello uno che meglio si adatta piattaforma hello in uso.</span><span class="sxs-lookup"><span data-stu-id="0a57d-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="0a57d-132">Chiave di strumentazione hello è necessaria per la creazione di client di telemetria hello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a57d-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="0a57d-133">È possibile ottenerlo dal dashboard del portale Application Insights hello oppure è possibile ottenere dalla pagina di ricerca traffico Analitica hello, selezione istanza hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="0a57d-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="0a57d-134">2. Instrumentare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="0a57d-134">2. Instrument your application</span></span>

<span data-ttu-id="0a57d-135">Questa fase è dove instrumentare un'applicazione di ricerca personalizzato, utilizzando una risorsa di Application Insights hello il hello creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0a57d-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="0a57d-136">Esistono quattro passaggi processo toothis:</span><span class="sxs-lookup"><span data-stu-id="0a57d-136">There are four steps toothis process:</span></span>

<span data-ttu-id="0a57d-137">**I. Creare un client di telemetria** oggetto hello che invia gli eventi toohello risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0a57d-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="0a57d-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="0a57d-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="0a57d-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0a57d-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="0a57d-140">Per altri linguaggi e piattaforme, vedere hello completo [elenco](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="0a57d-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="0a57d-141">**II. Un ID di ricerca per la correlazione richiesta** ricerca toocorrelate richieste con clic, è necessario toohave un id di correlazione che si riferisce a questi due eventi distinti.</span><span class="sxs-lookup"><span data-stu-id="0a57d-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="0a57d-142">Ricerca di Azure offre un ID di ricerca quando viene richiesto con l'intestazione seguente:</span><span class="sxs-lookup"><span data-stu-id="0a57d-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="0a57d-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="0a57d-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="0a57d-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0a57d-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="0a57d-145">**III. Registrazione degli eventi di ricerca**</span><span class="sxs-lookup"><span data-stu-id="0a57d-145">**III. Log Search events**</span></span>

<span data-ttu-id="0a57d-146">Ogni volta che una richiesta di ricerca viene eseguita da un utente, è consigliabile registrare che come un evento di ricerca con hello seguente schema di un evento personalizzato di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="0a57d-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="0a57d-147">**ServiceName**: nome del servizio di ricerca (string) **il SearchId**: identificatore (guid) della query di ricerca hello (disponibile in risposta alla ricerca hello) **IndexName**: indice del servizio di ricerca (string) toobe query **QueryTerms**: i termini di ricerca (stringa) immessi dall'utente hello **ResultCount**: (int) numero di documenti che sono stati restituiti (disponibile in risposta alla ricerca hello)  **ScoringProfile**: nome (string) di hello punteggio profilo utilizzato, se presente</span><span class="sxs-lookup"><span data-stu-id="0a57d-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="0a57d-148">Numero di richieste per le query generato dall'utente tramite l'aggiunta di $count = true tooyour query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="0a57d-149">Ulteriori informazioni sono disponibili [qui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request).</span><span class="sxs-lookup"><span data-stu-id="0a57d-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="0a57d-150">Tenere presente che le query di ricerca log tooonly generati dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="0a57d-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="0a57d-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="0a57d-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="0a57d-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0a57d-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="0a57d-153">**IV. Registrazione degli eventi clic**</span><span class="sxs-lookup"><span data-stu-id="0a57d-153">**IV. Log Click events**</span></span>

<span data-ttu-id="0a57d-154">Ogni clic di un utente su un documento è un segnale che deve essere registrato a scopo di analisi delle ricerche.</span><span class="sxs-lookup"><span data-stu-id="0a57d-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="0a57d-155">Utilizzare questi eventi di Application Insights eventi personalizzati toolog con hello seguente schema:</span><span class="sxs-lookup"><span data-stu-id="0a57d-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="0a57d-156">**ServiceName**: nome del servizio di ricerca (string) **il SearchId**: identificatore (guid) della query di ricerca correlata hello **DocId**: identificatore documento (string) **posizione** : pagina di risultati di priorità del documento hello nella ricerca hello (int)</span><span class="sxs-lookup"><span data-stu-id="0a57d-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="0a57d-157">Posizione fa riferimento l'ordine di tipo cardinal toohello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a57d-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="0a57d-158">Si è gratuita tooset questo numero, purché ha sempre hello stesso, tooallow per il confronto.</span><span class="sxs-lookup"><span data-stu-id="0a57d-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="0a57d-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="0a57d-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="0a57d-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0a57d-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="0a57d-161">3. Eseguire l'analisi con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0a57d-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="0a57d-162">Dopo aver instrumentata dell'applicazione e verificare che l'applicazione sia correttamente connesso tooApplication Insights, è possibile utilizzare un modello predefinito creato da ricerca di Azure per Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="0a57d-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="0a57d-163">Il modello contiene grafici e tabelle che consentono di rendono tooimprove decisioni più informate le prestazioni di ricerca e pertinenza.</span><span class="sxs-lookup"><span data-stu-id="0a57d-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="0a57d-164">tooinstantiate hello Power BI modello di desktop, è necessario tre tipi di informazioni su Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0a57d-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="0a57d-165">Questi dati sono reperibile nella pagina di ricerca traffico Analitica hello, quando si seleziona hello risorse toouse</span><span class="sxs-lookup"><span data-stu-id="0a57d-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Dati di Insights di applicazioni nel Pannello di hello Analitica di traffico di ricerca][2]

<span data-ttu-id="0a57d-167">Metrica inclusa nel modello di hello Power BI desktop:</span><span class="sxs-lookup"><span data-stu-id="0a57d-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="0a57d-168">Fare clic su tramite velocità (CTRL): rapporto tra l'utente fa clic su un numero di ricerche totali toohello di documento specifico.</span><span class="sxs-lookup"><span data-stu-id="0a57d-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="0a57d-169">Ricerche senza clic: termini delle query principali per i quali non sono registrati clic.</span><span class="sxs-lookup"><span data-stu-id="0a57d-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="0a57d-170">Selezionato più documenti: selezionato più documenti da ID in hello ultime 24 ore, 7 giorni e 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="0a57d-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="0a57d-171">Coppie di documenti termini comuni: condizioni che comportano hello fa clic sul documento stesso, ordinati in base al clic.</span><span class="sxs-lookup"><span data-stu-id="0a57d-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="0a57d-172">Tempo tooclick: clic riportato per volta dalla query di ricerca hello</span><span class="sxs-lookup"><span data-stu-id="0a57d-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Modello di Power BI per la lettura da Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="0a57d-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a57d-174">Next Steps</span></span>
<span data-ttu-id="0a57d-175">Instrumentare i dati di ricerca applicazione tooget potente e utili informazioni sul servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0a57d-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="0a57d-176">Ulteriori informazioni su Application Insights sono disponibili [qui](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="0a57d-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="0a57d-177">Visitare Application Insights [pagina dei prezzi](https://azure.microsoft.com/pricing/details/application-insights/) toolearn ulteriori informazioni sulla loro diversi livelli di servizio.</span><span class="sxs-lookup"><span data-stu-id="0a57d-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="0a57d-178">Altre informazioni sulla creazione di report utili</span><span class="sxs-lookup"><span data-stu-id="0a57d-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="0a57d-179">Per informazioni dettagliate, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="0a57d-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
