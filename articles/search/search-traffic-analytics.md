---
title: Analisi del traffico di ricerca per Ricerca di Azure | Documentazione Microsoft
description: Abilitare Analisi del traffico di ricerca per Ricerca di Azure, un servizio di ricerca cloud ospitato in Microsoft Azure, per sbloccare informazioni dettagliate su utenti e dati.
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
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="17f59-103">Analisi del traffico di ricerca</span><span class="sxs-lookup"><span data-stu-id="17f59-103">What is search traffic analytics</span></span>
<span data-ttu-id="17f59-104">Analisi del traffico di ricerca è un modello per l'implementazione di un ciclo di feedback per il servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="17f59-105">Questo modello descrive i dati necessari e come raccoglierli utilizzando Application Insights, uno strumento leader di settore per il monitoraggio dei servizi in più piattaforme.</span><span class="sxs-lookup"><span data-stu-id="17f59-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="17f59-106">Analisi del traffico di ricerca consente di ottenere visibilità nel servizio di ricerca e informazioni dettagliate su utenti e relativo comportamento.</span><span class="sxs-lookup"><span data-stu-id="17f59-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="17f59-107">La possibilità di accedere ai dati correlati alle scelte effettuate dagli utenti è utile per prendere decisioni in grado di migliorare ulteriormente l'esperienza di ricerca e per fare un passo indietro se i risultati non sono quelli previsti.</span><span class="sxs-lookup"><span data-stu-id="17f59-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="17f59-108">Ricerca di Azure offre una soluzione di telemetria che integra Azure Application Insights e Power BI per offrire funzionalità di rilevamento e monitoraggio avanzate.</span><span class="sxs-lookup"><span data-stu-id="17f59-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="17f59-109">Poiché l'interazione con Ricerca di Azure avviene solo tramite le API, la telemetria deve essere implementata dagli sviluppatori che utilizzano la funzionalità di ricerca, seguendo le istruzioni riportate in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="17f59-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="17f59-110">Identificare i dati di ricerca rilevanti</span><span class="sxs-lookup"><span data-stu-id="17f59-110">Identify the relevant search data</span></span>

<span data-ttu-id="17f59-111">Per ottenere metriche di ricerca utili, è necessario registrare alcuni segnali provenienti dagli utenti dell'applicazione di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="17f59-112">Questi segnali indicano contenuti che gli utenti trovano interessanti e considerano rilevanti per le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="17f59-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="17f59-113">I segnali necessari per Analisi del traffico di ricerca sono due:</span><span class="sxs-lookup"><span data-stu-id="17f59-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="17f59-114">Eventi di ricerca generati dagli utenti. Sono interessanti solo le query di ricerca avviate da un utente.</span><span class="sxs-lookup"><span data-stu-id="17f59-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="17f59-115">Le richieste di ricerca utilizzate per popolare facet, contenuti aggiuntivi o informazioni interne non sono rilevanti e anzi pregiudicano la correttezza dei risultati.</span><span class="sxs-lookup"><span data-stu-id="17f59-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="17f59-116">Eventi generati dai clic degli utenti. Il termine "clic" in questo documento si riferisce alla selezione, da parte di un utente, di un determinato risultato di ricerca restituito da una query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="17f59-117">Un clic in genere indica che un documento è un risultato rilevante per una specifica query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="17f59-118">Il collegamento degli eventi di ricerca e degli eventi clic mediante un ID di correlazione consente di analizzare i comportamenti degli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17f59-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="17f59-119">I registri del traffico di ricerca non sono in grado di offrire informazioni sulla ricerca così dettagliate.</span><span class="sxs-lookup"><span data-stu-id="17f59-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="17f59-120">Come implementare Analisi del traffico di ricerca</span><span class="sxs-lookup"><span data-stu-id="17f59-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="17f59-121">I segnali menzionati nella sezione precedente devono essere raccolti dall'applicazione di ricerca quando l'utente interagisce con essa.</span><span class="sxs-lookup"><span data-stu-id="17f59-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="17f59-122">Application Insights è una soluzione di monitoraggio estensibile, disponibile per più piattaforme, con opzioni di strumentazione flessibili.</span><span class="sxs-lookup"><span data-stu-id="17f59-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="17f59-123">L'uso di Application Insights consente di usufruire dei report di ricerca Power BI creati da Ricerca di Azure per semplificare l'analisi dei dati.</span><span class="sxs-lookup"><span data-stu-id="17f59-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="17f59-124">Nella pagina del [portale](https://portal.azure.com) del servizio Ricerca di Azure il pannello Analisi del traffico di ricerca contiene un foglio informativo utile per seguire questo modello di telemetria.</span><span class="sxs-lookup"><span data-stu-id="17f59-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="17f59-125">È anche possibile selezionare o creare una risorsa di Application Insights e visualizzare i dati necessari, tutti raccolti in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="17f59-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Istruzioni per Analisi del traffico di ricerca][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="17f59-127">1. Selezionare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="17f59-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="17f59-128">È necessario selezionare una risorsa di Application Insights da usare o crearne una se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="17f59-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="17f59-129">È possibile usare una risorsa già in uso per registrare gli eventi personalizzati necessari.</span><span class="sxs-lookup"><span data-stu-id="17f59-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="17f59-130">Quando si crea una nuova risorsa di Application Insights, sono validi tutti i tipi di applicazione per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="17f59-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="17f59-131">Selezionare quella che meglio si adatta alla piattaforma in uso.</span><span class="sxs-lookup"><span data-stu-id="17f59-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="17f59-132">Per creare il client di telemetria per l'applicazione, è necessario disporre della chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="17f59-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="17f59-133">È possibile ottenerla dal dashboard del portale di Application Insights oppure dalla pagina Analisi del traffico di ricerca selezionando l'istanza che si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="17f59-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="17f59-134">2. Instrumentare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="17f59-134">2. Instrument your application</span></span>

<span data-ttu-id="17f59-135">Questa è la fase in cui si esegue la strumentazione della propria applicazione di ricerca, utilizzando la risorsa di Application Insights creata al passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="17f59-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="17f59-136">Questo processo è suddiviso in quattro passaggi:</span><span class="sxs-lookup"><span data-stu-id="17f59-136">There are four steps to this process:</span></span>

<span data-ttu-id="17f59-137">**I. Creazione di un client di telemetria** Si tratta dell'oggetto che invia eventi alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="17f59-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="17f59-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="17f59-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="17f59-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="17f59-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="17f59-140">Per altre piattaforme e altri linguaggi, vedere l'[elenco](https://docs.microsoft.com/azure/application-insights/app-insights-platforms) completo.</span><span class="sxs-lookup"><span data-stu-id="17f59-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="17f59-141">**II. Richiesta di un ID di ricerca per la correlazione** Per correlare le richieste di ricerca con i clic, è necessario disporre di un ID di correlazione che metta in correlazione questi due eventi distinti.</span><span class="sxs-lookup"><span data-stu-id="17f59-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="17f59-142">Ricerca di Azure offre un ID di ricerca quando viene richiesto con l'intestazione seguente:</span><span class="sxs-lookup"><span data-stu-id="17f59-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="17f59-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="17f59-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="17f59-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="17f59-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="17f59-145">**III. Registrazione degli eventi di ricerca**</span><span class="sxs-lookup"><span data-stu-id="17f59-145">**III. Log Search events**</span></span>

<span data-ttu-id="17f59-146">Ogni volta che un utente esegue una richiesta di ricerca, è necessario registrarla come evento di ricerca con lo schema seguente in un evento personalizzato di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="17f59-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="17f59-147">**ServiceName**: (string) nome del servizio di ricerca **SearchId**: (guid) identificatore univoco della query di ricerca (incluso nella risposta alla ricerca) **IndexName**: (string) indice del servizio di ricerca da sottoporre a query **QueryTerms**: (string) termini di ricerca immessi dall'utente **ResultCount**: (int) numero di documenti restituiti (incluso nella risposta alla ricerca) **ScoringProfile**: (string) nome del profilo di punteggio usato, se disponibile</span><span class="sxs-lookup"><span data-stu-id="17f59-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="17f59-148">Richiedere il conteggio nelle query generate dall'utente mediante l'aggiunta di $count=true alla query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="17f59-149">Ulteriori informazioni sono disponibili [qui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request).</span><span class="sxs-lookup"><span data-stu-id="17f59-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="17f59-150">Ricordarsi di registrare solo le query di ricerca generate dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="17f59-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="17f59-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="17f59-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="17f59-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="17f59-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="17f59-153">**IV. Registrazione degli eventi clic**</span><span class="sxs-lookup"><span data-stu-id="17f59-153">**IV. Log Click events**</span></span>

<span data-ttu-id="17f59-154">Ogni clic di un utente su un documento è un segnale che deve essere registrato a scopo di analisi delle ricerche.</span><span class="sxs-lookup"><span data-stu-id="17f59-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="17f59-155">Utilizzare gli eventi personalizzati di Application Insights per registrare questi eventi con lo schema seguente:</span><span class="sxs-lookup"><span data-stu-id="17f59-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="17f59-156">**ServiceName**: (string) nome del servizio di ricerca**SearchId**: (guid) identificatore univoco della query di ricerca correlata **DocId**: (string) identificatore del documento **Position**: (int) posizione del documento nella pagina dei risultati della ricerca</span><span class="sxs-lookup"><span data-stu-id="17f59-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="17f59-157">Position fa riferimento all'ordine cardinale nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17f59-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="17f59-158">È possibile impostare questo numero, purché si tratti sempre dello stesso, per consentire il confronto.</span><span class="sxs-lookup"><span data-stu-id="17f59-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="17f59-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="17f59-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="17f59-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="17f59-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="17f59-161">3. Eseguire l'analisi con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="17f59-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="17f59-162">Dopo avere instrumentato l'app e averne verificata la corretta connessione ad Application Insights, è possibile utilizzare un modello predefinito creato da Ricerca di Azure per Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="17f59-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="17f59-163">Questo modello contiene grafici e tabelle che consentono di prendere decisioni più informate per migliorare le prestazioni di ricerca e la rilevanza.</span><span class="sxs-lookup"><span data-stu-id="17f59-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="17f59-164">Per creare un'istanza del modello di Power BI Desktop, sono necessarie tre informazioni su Application Insights.</span><span class="sxs-lookup"><span data-stu-id="17f59-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="17f59-165">Questi dati sono reperibili nella pagina Analisi del traffico di ricerca, quando si seleziona la risorsa da usare.</span><span class="sxs-lookup"><span data-stu-id="17f59-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Dati di Application Insights nel pannello Analisi del traffico di ricerca][2]

<span data-ttu-id="17f59-167">Metriche incluse nel modello di Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="17f59-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="17f59-168">Tasso di clic (CTR): rapporto tra utenti che fanno clic su un documento specifico e numero di ricerche totali.</span><span class="sxs-lookup"><span data-stu-id="17f59-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="17f59-169">Ricerche senza clic: termini delle query principali per i quali non sono registrati clic.</span><span class="sxs-lookup"><span data-stu-id="17f59-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="17f59-170">Documenti con più clic: documenti con più clic suddivisi per ID nelle ultime 24 ore e negli ultimi 7 e 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="17f59-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="17f59-171">Coppie termine-documento più comuni: termini che producono lo stesso documento selezionato, ordinati per clic.</span><span class="sxs-lookup"><span data-stu-id="17f59-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="17f59-172">Tempo dei clic: clic con bucket definiti in base al tempo dopo la query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-172">Time to click: clicks bucketed by time since the search query</span></span>

![Modello di Power BI per la lettura da Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="17f59-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17f59-174">Next Steps</span></span>
<span data-ttu-id="17f59-175">Instrumentare l'applicazione di ricerca per ottenere dati estremamente utili e dettagliati relativi al servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17f59-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="17f59-176">Ulteriori informazioni su Application Insights sono disponibili [qui](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="17f59-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="17f59-177">Per ulteriori informazioni sui diversi livelli di servizio, visitare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/application-insights/) di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="17f59-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="17f59-178">Altre informazioni sulla creazione di report utili</span><span class="sxs-lookup"><span data-stu-id="17f59-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="17f59-179">Per informazioni dettagliate, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="17f59-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
