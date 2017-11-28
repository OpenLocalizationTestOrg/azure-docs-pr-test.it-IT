---
title: "Utilizzo della funzionalità Ricerca in Azure Application Insights | Microsoft Docs"
description: Ricercare e filtrare elementi di telemetria non elaborata inviata da App Web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e2d12f807756b778a64920b12a66fba184a99844
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="31187-103">Utilizzo della funzionalità Ricerca in Application Insights</span><span class="sxs-lookup"><span data-stu-id="31187-103">Using Search in Application Insights</span></span>
<span data-ttu-id="31187-104">Ricerca è una funzionalità di [Application Insights](app-insights-overview.md) che consente di trovare ed esplorare elementi singoli di telemetria, ad esempio visualizzazioni pagine, eccezioni o richieste Web.</span><span class="sxs-lookup"><span data-stu-id="31187-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="31187-105">È possibile visualizzare le tracce del log e gli eventi codificati.</span><span class="sxs-lookup"><span data-stu-id="31187-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="31187-106">Per le query più complesse sui dati, utilizzare [Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="31187-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="31187-107">Dove si trova Ricerca?</span><span class="sxs-lookup"><span data-stu-id="31187-107">Where do you see Search?</span></span>
### <a name="in-the-azure-portal"></a><span data-ttu-id="31187-108">Nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31187-108">In the Azure portal</span></span>
<span data-ttu-id="31187-109">È possibile aprire la ricerca diagnostica in modo esplicito dal pannello Panoramica di Application Insights dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="31187-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span></span>

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="31187-111">Viene anche aperta quando si fa clic su alcuni grafici ed elementi della griglia.</span><span class="sxs-lookup"><span data-stu-id="31187-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="31187-112">In questo caso, i filtri sono preimpostati per concentrarsi sul tipo di elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="31187-112">In this case, its filters are pre-set to focus on the type of item you selected.</span></span> 

<span data-ttu-id="31187-113">Ad esempio, nel pannello Panoramica, è presente un grafico a barre di richieste classificate per tempo di risposta.</span><span class="sxs-lookup"><span data-stu-id="31187-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="31187-114">Fare clic in un intervallo di prestazioni per visualizzare un elenco delle singole richieste nell'intervallo di tempo di risposta:</span><span class="sxs-lookup"><span data-stu-id="31187-114">Click through a performance range to see a list of individual requests in that response time range:</span></span>

![Fare clic sulle prestazioni della richiesta](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="31187-116">Il corpo principale della Ricerca diagnostica è un elenco di elementi di telemetria: richieste del server, visualizzazioni pagina, eventi personalizzati che sono stati codificati e così via.</span><span class="sxs-lookup"><span data-stu-id="31187-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="31187-117">Nella parte superiore dell'elenco è disponibile un grafico di riepilogo che mostra il numero di eventi nel tempo.</span><span class="sxs-lookup"><span data-stu-id="31187-117">At the top of the list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="31187-118">Fare clic su Aggiorna per ottenere nuovi eventi.</span><span class="sxs-lookup"><span data-stu-id="31187-118">Click Refresh to get new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="31187-119">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31187-119">In Visual Studio</span></span>

<span data-ttu-id="31187-120">In Visual Studio è inoltre disponibile una finestra Ricerca di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31187-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="31187-121">È più utile per visualizzare gli eventi di telemetria generati dall'applicazione di cui si esegue il debug.</span><span class="sxs-lookup"><span data-stu-id="31187-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span></span> <span data-ttu-id="31187-122">È inoltre possibile visualizzare gli eventi raccolti dall'app pubblicata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="31187-122">But it can also show the events collected from your published app at the Azure portal.</span></span>

<span data-ttu-id="31187-123">Aprire la finestra Cerca in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="31187-123">Open the Search window in Visual Studio:</span></span>

![Funzionalità di ricerca di Application Insights aperta in Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="31187-125">La finestra di ricerca ha funzionalità simili al portale Web:</span><span class="sxs-lookup"><span data-stu-id="31187-125">The Search window has features similar to the web portal:</span></span>

![Finestra di ricerca di Application Insights in Visual Studio](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="31187-127">La scheda Track Operation (Traccia operazione) è disponibile quando si apre una richiesta o una visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="31187-127">The Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="31187-128">Con "operazione" si intende una sequenza di eventi associata a una singola richiesta o visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="31187-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span></span> <span data-ttu-id="31187-129">Ad esempio, chiamate di dipendenza, eccezioni, log di traccia ed eventi personalizzati potrebbero far parte di una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="31187-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="31187-130">La scheda Track Operation (Traccia operazione) mostra graficamente l'intervallo e la durata di questi eventi in relazione alla richiesta o alla visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="31187-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="31187-131">Controllare i singoli elementi</span><span class="sxs-lookup"><span data-stu-id="31187-131">Inspect individual items</span></span>
<span data-ttu-id="31187-132">Selezionare qualsiasi elemento di dati di telemetria per visualizzare i campi chiave e gli elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="31187-132">Select any telemetry item to see key fields and related items.</span></span> <span data-ttu-id="31187-133">Se si intende visualizzare il set completo di campi, fare clic su "...".</span><span class="sxs-lookup"><span data-stu-id="31187-133">If you want to see the full set of fields, click "...".</span></span> 

![Fare clic su Nuovo elemento di lavoro, modificare i campi e quindi fare clic su OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="31187-135">I tipi di eventi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="31187-135">Filter event types</span></span>
<span data-ttu-id="31187-136">Aprire il pannello Filtro e scegliere i tipi di evento che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="31187-136">Open the Filter blade and choose the event types you want to see.</span></span> <span data-ttu-id="31187-137">Se, in seguito, si vogliono ripristinare i filtri con cui è stato aperto il pannello, fare clic su Reimposta.</span><span class="sxs-lookup"><span data-stu-id="31187-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span></span>

![Scegliere il filtro e selezionare i tipi di telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="31187-139">I tipi di eventi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="31187-139">The event types are:</span></span>

* <span data-ttu-id="31187-140">**Traccia**:  - [log di diagnostica](app-insights-asp-net-trace-logs.md) con chiamate TrackTrace, log4Net, NLog e System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="31187-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="31187-141">**Richiesta**: richieste HTTP ricevute dall'applicazione server, tra cui pagine, script, immagini, file di stile e dati.</span><span class="sxs-lookup"><span data-stu-id="31187-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="31187-142">Questi eventi vengono usati per creare grafici di panoramica di richieste e risposte.</span><span class="sxs-lookup"><span data-stu-id="31187-142">These events are used to create the request and response overview charts.</span></span>
* <span data-ttu-id="31187-143">**Visualizzazione pagina**: -  [i dati di telemetria inviati al client Web](app-insights-javascript.md), usati per creare report di visualizzazioni pagine.</span><span class="sxs-lookup"><span data-stu-id="31187-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span></span> 
* <span data-ttu-id="31187-144">**Evento personalizzato**: se sono state inserite chiamate in TrackEvent() per [tenere traccia dell'utilizzo](app-insights-api-custom-events-metrics.md), è possibile cercarle qui.</span><span class="sxs-lookup"><span data-stu-id="31187-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="31187-145">**Eccezione**: [eccezioni non rilevate nel server](app-insights-asp-net-exceptions.md) e quelle che si registrano con TrackException().</span><span class="sxs-lookup"><span data-stu-id="31187-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="31187-146">**Dipendenza**:  - [chiamate dall'applicazione server](app-insights-asp-net-dependencies.md) ad altri servizi, ad esempio le API REST o i database, e chiamate AJAX dal [codice client](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="31187-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="31187-147">**Disponibilità**: risultati dei [test di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="31187-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="31187-148">Filtrare in base ai valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="31187-148">Filter on property values</span></span>
<span data-ttu-id="31187-149">È possibile filtrare gli eventi in base ai valori delle relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="31187-149">You can filter events on the values of their properties.</span></span> <span data-ttu-id="31187-150">Le proprietà disponibili dipendono dai tipi di eventi selezionati.</span><span class="sxs-lookup"><span data-stu-id="31187-150">The available properties depend on the event types you selected.</span></span> 

<span data-ttu-id="31187-151">Ad esempio, selezionare le richieste con un codice di risposta specifico.</span><span class="sxs-lookup"><span data-stu-id="31187-151">For example, pick out requests with a specific response code.</span></span> 

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="31187-153">La mancata scelta dei valori di una determinata proprietà ha lo stesso effetto della scelta di tutti i valori.</span><span class="sxs-lookup"><span data-stu-id="31187-153">Choosing no values of a particular property has the same effect as choosing all values.</span></span> <span data-ttu-id="31187-154">Viene disattivata l'applicazione dei filtri per quella proprietà.</span><span class="sxs-lookup"><span data-stu-id="31187-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="31187-155">Limitare la ricerca</span><span class="sxs-lookup"><span data-stu-id="31187-155">Narrow your search</span></span>
<span data-ttu-id="31187-156">Si noti che il numero a destra dei valori di filtro mostra quante occorrenze sono incluse nel set filtrato corrente.</span><span class="sxs-lookup"><span data-stu-id="31187-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span></span> 

<span data-ttu-id="31187-157">In questo esempio è evidente che la richiesta "Rpt/Employees" produce la maggior parte dei "500" errori:</span><span class="sxs-lookup"><span data-stu-id="31187-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span></span>

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-the-same-property"></a><span data-ttu-id="31187-159">Trovare gli eventi con la stessa proprietà</span><span class="sxs-lookup"><span data-stu-id="31187-159">Find events with the same property</span></span>
<span data-ttu-id="31187-160">Trovare tutti gli elementi con lo stesso valore della proprietà:</span><span class="sxs-lookup"><span data-stu-id="31187-160">Find all the items with the same property value:</span></span>

![Fare clic con il pulsante destro del mouse su una proprietà](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-the-data"></a><span data-ttu-id="31187-162">Eseguire ricerche nei dati</span><span class="sxs-lookup"><span data-stu-id="31187-162">Search the data</span></span>

> [!NOTE]
> <span data-ttu-id="31187-163">Per scrivere query più complesse, aprire [**Analytics**](app-insights-analytics-tour.md) nella parte superiore del pannello Ricerca.</span><span class="sxs-lookup"><span data-stu-id="31187-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span></span>
> 

<span data-ttu-id="31187-164">È possibile cercare i termini in uno dei valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="31187-164">You can search for terms in any of the property values.</span></span> <span data-ttu-id="31187-165">Ciò è particolarmente utile se sono stati scritti [eventi personalizzati](app-insights-api-custom-events-metrics.md) con i valori della proprietà.</span><span class="sxs-lookup"><span data-stu-id="31187-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="31187-166">È possibile che si voglia impostare un intervallo di tempo, poiché le ricerche di un intervallo più breve sono più veloci.</span><span class="sxs-lookup"><span data-stu-id="31187-166">You might want to set a time range, as searches over a shorter range are faster.</span></span> 

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="31187-168">Cercare parole complete, non sottostringhe.</span><span class="sxs-lookup"><span data-stu-id="31187-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="31187-169">Utilizzare le virgolette per racchiudere i caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="31187-169">Use quotation marks to enclose special characters.</span></span>

| <span data-ttu-id="31187-170">string</span><span class="sxs-lookup"><span data-stu-id="31187-170">string</span></span> | <span data-ttu-id="31187-171">*non* si trova con</span><span class="sxs-lookup"><span data-stu-id="31187-171">is *not* found by</span></span> | <span data-ttu-id="31187-172">ma si trova con</span><span class="sxs-lookup"><span data-stu-id="31187-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31187-173">ControllerHome.Info</span><span class="sxs-lookup"><span data-stu-id="31187-173">HomeController.About</span></span> |<span data-ttu-id="31187-174">home</span><span class="sxs-lookup"><span data-stu-id="31187-174">home</span></span><br/><span data-ttu-id="31187-175">controller</span><span class="sxs-lookup"><span data-stu-id="31187-175">controller</span></span><br/><span data-ttu-id="31187-176">fo</span><span class="sxs-lookup"><span data-stu-id="31187-176">out</span></span> | <span data-ttu-id="31187-177">controllerhome</span><span class="sxs-lookup"><span data-stu-id="31187-177">homecontroller</span></span><br/><span data-ttu-id="31187-178">info</span><span class="sxs-lookup"><span data-stu-id="31187-178">about</span></span><br/><span data-ttu-id="31187-179">"homecontroller.info"</span><span class="sxs-lookup"><span data-stu-id="31187-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="31187-180">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="31187-180">United States</span></span>|<span data-ttu-id="31187-181">Uni</span><span class="sxs-lookup"><span data-stu-id="31187-181">Uni</span></span><br/><span data-ttu-id="31187-182">ti</span><span class="sxs-lookup"><span data-stu-id="31187-182">ted</span></span>|<span data-ttu-id="31187-183">uniti</span><span class="sxs-lookup"><span data-stu-id="31187-183">united</span></span><br/><span data-ttu-id="31187-184">stati</span><span class="sxs-lookup"><span data-stu-id="31187-184">states</span></span><br/><span data-ttu-id="31187-185">uniti AND stati</span><span class="sxs-lookup"><span data-stu-id="31187-185">united AND states</span></span><br/><span data-ttu-id="31187-186">"stati uniti"</span><span class="sxs-lookup"><span data-stu-id="31187-186">"united states"</span></span>

<span data-ttu-id="31187-187">È possibile usare espressioni di ricerca quali le seguenti:</span><span class="sxs-lookup"><span data-stu-id="31187-187">Here are the search expressions you can use:</span></span>

| <span data-ttu-id="31187-188">Query di esempio</span><span class="sxs-lookup"><span data-stu-id="31187-188">Sample query</span></span> | <span data-ttu-id="31187-189">Effetto</span><span class="sxs-lookup"><span data-stu-id="31187-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="31187-190">Individuazione di tutti gli eventi nell'intervallo di tempo i cui campi includono la parola "mela"</span><span class="sxs-lookup"><span data-stu-id="31187-190">Find all events in the time range whose fields include the word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="31187-191">Individuazione di eventi che contengono entrambe le parole.</span><span class="sxs-lookup"><span data-stu-id="31187-191">Find events that contain both words.</span></span> <span data-ttu-id="31187-192">Usare "AND" in lettere maiuscole, non "and".</span><span class="sxs-lookup"><span data-stu-id="31187-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="31187-193">Individuazione degli eventi che contengono una delle parole.</span><span class="sxs-lookup"><span data-stu-id="31187-193">Find events that contain either word.</span></span> <span data-ttu-id="31187-194">Usare "OR", non "or".</span><span class="sxs-lookup"><span data-stu-id="31187-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="31187-195">Forma breve.</span><span class="sxs-lookup"><span data-stu-id="31187-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="31187-196">Individua eventi che contengono una parola ma non l'altra.</span><span class="sxs-lookup"><span data-stu-id="31187-196">Find events that contain one word but not the other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="31187-197">campionamento</span><span class="sxs-lookup"><span data-stu-id="31187-197">Sampling</span></span>
<span data-ttu-id="31187-198">Se l'app genera molti dati di telemetria (e si usa ASP.NET SDK versione 2.0.0-beta3 o successiva), il modulo di campionamento adattivo riduce automaticamente il volume che viene inviato al portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="31187-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="31187-199">Tuttavia, gli eventi che fanno parte della stessa richiesta vengono selezionati o deselezionati come gruppo, per rendere possibile lo spostamento tra eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="31187-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="31187-200">[Informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="31187-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="31187-201">Creare un elemento di lavoro</span><span class="sxs-lookup"><span data-stu-id="31187-201">Create work item</span></span>
<span data-ttu-id="31187-202">È possibile creare un bug in GitHub o Visual Studio Team Services con i dettagli provenienti da qualsiasi elemento di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="31187-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span></span> 

![Fare clic su Nuovo elemento di lavoro, modificare i campi e quindi fare clic su OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="31187-204">La prima volta che si esegue questa operazione viene chiesto di configurare un collegamento all'account e al progetto di Team Services.</span><span class="sxs-lookup"><span data-stu-id="31187-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span></span>

![Immettere l'URL del server di Team Services e il nome del progetto, quindi fare clic su Autorizza.](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="31187-206">(È anche possibile configurare il collegamento al pannello Elementi di lavoro).</span><span class="sxs-lookup"><span data-stu-id="31187-206">(You can also configure the link on the Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="31187-207">Salvare la ricerca</span><span class="sxs-lookup"><span data-stu-id="31187-207">Save your search</span></span>
<span data-ttu-id="31187-208">Dopo aver impostato tutti i filtri desiderati, è possibile salvare la ricerca come preferita.</span><span class="sxs-lookup"><span data-stu-id="31187-208">When you've set all the filters you want, you can save the search as a favorite.</span></span> <span data-ttu-id="31187-209">Se si usa un account aziendale, è possibile scegliere se condividerlo con altri membri del team.</span><span class="sxs-lookup"><span data-stu-id="31187-209">If you work in an organizational account, you can choose whether to share it with other team members.</span></span>

![Fare clic su Preferiti, impostare il nome e fare clic su Salva](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="31187-211">Per visualizzare nuovamente la ricerca, **andare al pannello Panoramica** e aprire Preferiti:</span><span class="sxs-lookup"><span data-stu-id="31187-211">To see the search again, **go to the overview blade** and open Favorites:</span></span>

![Sezione Preferiti](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="31187-213">Se è stato salvato con intervallo di tempo Relativo, il pannello riaperto presenterà i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="31187-213">If you saved with Relative time range, the re-opened blade has the latest data.</span></span> <span data-ttu-id="31187-214">Se è stato salvato con intervallo di tempo Assoluto,verranno visualizzati gli stessi dati ogni volta.</span><span class="sxs-lookup"><span data-stu-id="31187-214">If you saved with Absolute time range, you see the same data every time.</span></span> <span data-ttu-id="31187-215">Se "Relativo" non è disponibile quando si desidera salvare un elemento come preferito, fare clic su Intervallo di tempo nell'intestazione e impostare un intervallo di tempo che non sia personalizzato.</span><span class="sxs-lookup"><span data-stu-id="31187-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-to-application-insights"></a><span data-ttu-id="31187-216">Inviare altri dati di telemetria ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="31187-216">Send more telemetry to Application Insights</span></span>
<span data-ttu-id="31187-217">Oltre la telemetria predefinita inviata da Application Insights SDK, è possibile:</span><span class="sxs-lookup"><span data-stu-id="31187-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="31187-218">Acquisire le tracce del log dal framework di registrazione preferito in [.NET](app-insights-asp-net-trace-logs.md) o [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="31187-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="31187-219">Ciò significa che è possibile cercare le tracce del log e metterle in correlazione con le visualizzazioni pagina, le eccezioni e altri eventi.</span><span class="sxs-lookup"><span data-stu-id="31187-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="31187-220">[Scrivere codice](app-insights-api-custom-events-metrics.md) per inviare eventi personalizzati, visualizzazioni pagina ed eccezioni.</span><span class="sxs-lookup"><span data-stu-id="31187-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="31187-221">[Informazioni su come inviare log e telemetria personalizzata ad Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="31187-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="31187-222"><a name="questions"></a>Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="31187-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="31187-223"><a name="limits"></a>Quanti dati vengono conservati?</span><span class="sxs-lookup"><span data-stu-id="31187-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="31187-224">Vedere il [Riepilogo dei limiti](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="31187-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="31187-225">Come è possibile visualizzare dati POST nelle richieste server?</span><span class="sxs-lookup"><span data-stu-id="31187-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="31187-226">I dati POST non vengono registrati automaticamente, ma è possibile usare [TrackTrace o chiamate di log](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="31187-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="31187-227">Inserire i dati POST nel parametro del messaggio.</span><span class="sxs-lookup"><span data-stu-id="31187-227">Put the POST data in the message parameter.</span></span> <span data-ttu-id="31187-228">Non è possibile filtrare in base al messaggio nello stesso modo delle proprietà, ma il limite delle dimensioni è maggiore.</span><span class="sxs-lookup"><span data-stu-id="31187-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="31187-229">Video</span><span class="sxs-lookup"><span data-stu-id="31187-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="31187-230"><a name="add"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31187-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="31187-231">Scrivere query complesse in Analytics</span><span class="sxs-lookup"><span data-stu-id="31187-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="31187-232">Inviare log e dati di telemetria personalizzati ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="31187-232">Send logs and custom telemetry to Application Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="31187-233">Configurare i test di disponibilità e velocità di risposta</span><span class="sxs-lookup"><span data-stu-id="31187-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="31187-234">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="31187-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
