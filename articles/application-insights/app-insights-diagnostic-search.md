---
title: Ricerca in Azure Application Insights aaaUsing | Documenti Microsoft
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
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="58d65-103">Utilizzo della funzionalità Ricerca in Application Insights</span><span class="sxs-lookup"><span data-stu-id="58d65-103">Using Search in Application Insights</span></span>
<span data-ttu-id="58d65-104">Ricerca è una funzionalità di [Application Insights](app-insights-overview.md) utilizzare toofind e di esplorare gli elementi di telemetria singole, ad esempio le visualizzazioni di pagina, le eccezioni o di richieste web.</span><span class="sxs-lookup"><span data-stu-id="58d65-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="58d65-105">È possibile visualizzare le tracce del log e gli eventi codificati.</span><span class="sxs-lookup"><span data-stu-id="58d65-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="58d65-106">Per le query più complesse sui dati, utilizzare [Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="58d65-107">Dove si trova Ricerca?</span><span class="sxs-lookup"><span data-stu-id="58d65-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="58d65-108">Nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="58d65-108">In hello Azure portal</span></span>
<span data-ttu-id="58d65-109">È possibile aprire una ricerca di diagnostica in modo esplicito dal Pannello di Application Insights Overview hello dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="58d65-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="58d65-111">Viene anche aperta quando si fa clic su alcuni grafici ed elementi della griglia.</span><span class="sxs-lookup"><span data-stu-id="58d65-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="58d65-112">In questo caso, i filtri pre-sono toofocus tipo hello dell'elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="58d65-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="58d65-113">Ad esempio, nel pannello della panoramica hello, vi è un grafico a barre di richieste classificati in base al tempo di risposta.</span><span class="sxs-lookup"><span data-stu-id="58d65-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="58d65-114">Fare clic su un toosee intervallo prestazioni un elenco delle singole richieste in tale intervallo di tempo di risposta:</span><span class="sxs-lookup"><span data-stu-id="58d65-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Fare clic sulle prestazioni della richiesta](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="58d65-116">Hello corpo principale della diagnostica di ricerca è un elenco di elementi di dati di telemetria - richieste di server, pagina viste, eventi personalizzati che è stato codificato e così via.</span><span class="sxs-lookup"><span data-stu-id="58d65-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="58d65-117">Inizio dell'elenco di hello hello è un grafico di riepilogo che mostra i conteggi di eventi nel tempo.</span><span class="sxs-lookup"><span data-stu-id="58d65-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="58d65-118">Fare clic su Aggiorna tooget nuovi eventi.</span><span class="sxs-lookup"><span data-stu-id="58d65-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="58d65-119">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58d65-119">In Visual Studio</span></span>

<span data-ttu-id="58d65-120">In Visual Studio è inoltre disponibile una finestra Ricerca di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58d65-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="58d65-121">È particolarmente utile per la visualizzazione di eventi di telemetria generati da un'applicazione hello che si esegue il debug.</span><span class="sxs-lookup"><span data-stu-id="58d65-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="58d65-122">Tuttavia, inoltre possibile visualizzare gli eventi di hello raccolti dall'app pubblicate nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="58d65-123">Aprire la finestra di ricerca hello in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="58d65-123">Open hello Search window in Visual Studio:</span></span>

![Funzionalità di ricerca di Application Insights aperta in Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="58d65-125">finestra di ricerca Hello dispone di funzionalità simile toohello web portale:</span><span class="sxs-lookup"><span data-stu-id="58d65-125">hello Search window has features similar toohello web portal:</span></span>

![Finestra di ricerca di Application Insights in Visual Studio](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="58d65-127">scheda di operazione di rilevamento Hello è disponibile quando si apre una richiesta o una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="58d65-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="58d65-128">Un ' operazione ' è una sequenza di eventi che è associata a tooa singola richiesta o pagina di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="58d65-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="58d65-129">Ad esempio, chiamate di dipendenza, eccezioni, log di traccia ed eventi personalizzati potrebbero far parte di una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="58d65-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="58d65-130">Mostra scheda operazione di rilevamento di Hello hello graficamente intervallo e la durata di questi eventi nella relazione di toohello richiesta o la pagina di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="58d65-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="58d65-131">Controllare i singoli elementi</span><span class="sxs-lookup"><span data-stu-id="58d65-131">Inspect individual items</span></span>
<span data-ttu-id="58d65-132">Selezionare tutti i campi chiave di dati di telemetria elemento toosee ed elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="58d65-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="58d65-133">Set completo di hello toosee dei campi, fare clic su "…".</span><span class="sxs-lookup"><span data-stu-id="58d65-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Fare clic su nuovo elemento di lavoro, modificare i campi di hello e quindi fare clic su OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="58d65-135">I tipi di eventi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="58d65-135">Filter event types</span></span>
<span data-ttu-id="58d65-136">Aprire Pannello filtro hello e scegliere i tipi di evento hello si desidera toosee.</span><span class="sxs-lookup"><span data-stu-id="58d65-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="58d65-137">(Se, successivamente, si desidera filtri hello toorestore con cui è stato aperto il pannello hello, fare clic su Reimposta).</span><span class="sxs-lookup"><span data-stu-id="58d65-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Scegliere il filtro e selezionare i tipi di telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="58d65-139">tipi di evento Hello sono:</span><span class="sxs-lookup"><span data-stu-id="58d65-139">hello event types are:</span></span>

* <span data-ttu-id="58d65-140">**Traccia**:  - [log di diagnostica](app-insights-asp-net-trace-logs.md) con chiamate TrackTrace, log4Net, NLog e System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="58d65-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="58d65-141">**Richiesta**: richieste HTTP ricevute dall'applicazione server, tra cui pagine, script, immagini, file di stile e dati.</span><span class="sxs-lookup"><span data-stu-id="58d65-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="58d65-142">Questi eventi sono grafici Cenni preliminari sulla richiesta e risposta utilizzati toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="58d65-143">**Visualizzazione della pagina** - [telemetria inviati dal client web hello](app-insights-javascript.md), utilizzato toocreate pagina Visualizza report.</span><span class="sxs-lookup"><span data-stu-id="58d65-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="58d65-144">**Evento personalizzato** : se è stato inserito tooTrackEvent() chiamate in ordine troppo[monitorare l'utilizzo](app-insights-api-custom-events-metrics.md), è possibile cercare di seguito.</span><span class="sxs-lookup"><span data-stu-id="58d65-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="58d65-145">**Eccezione** - non rilevata [eccezioni nel server di hello](app-insights-asp-net-exceptions.md)e quelle che si accede tramite trackexception () effettuate.</span><span class="sxs-lookup"><span data-stu-id="58d65-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="58d65-146">**Dipendenza** - [chiamate dall'applicazione server](app-insights-asp-net-dependencies.md) tooother servizi, ad esempio le API REST o i database e chiamate AJAX dal [codice client](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="58d65-147">**Disponibilità**: risultati dei [test di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="58d65-148">Filtrare in base ai valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="58d65-148">Filter on property values</span></span>
<span data-ttu-id="58d65-149">È possibile filtrare gli eventi ai valori hello delle relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="58d65-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="58d65-150">proprietà di Hello disponibili dipendono dai tipi di evento hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="58d65-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="58d65-151">Ad esempio, selezionare le richieste con un codice di risposta specifico.</span><span class="sxs-lookup"><span data-stu-id="58d65-151">For example, pick out requests with a specific response code.</span></span> 

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="58d65-153">Non scelta di alcun valore di una determinata proprietà ha lo stesso effetto delle scelta tutti i valori hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="58d65-154">Viene disattivata l'applicazione dei filtri per quella proprietà.</span><span class="sxs-lookup"><span data-stu-id="58d65-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="58d65-155">Limitare la ricerca</span><span class="sxs-lookup"><span data-stu-id="58d65-155">Narrow your search</span></span>
<span data-ttu-id="58d65-156">Si noti che hello conta toohello a destra dei valori di filtro hello mostrare il numero di occorrenze sono set filtrato di hello corrente.</span><span class="sxs-lookup"><span data-stu-id="58d65-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="58d65-157">In questo esempio è chiaro che la richiesta ' Rpt/Employees' hello risultati nella maggior parte degli errori di hello '500':</span><span class="sxs-lookup"><span data-stu-id="58d65-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="58d65-159">Trovare gli eventi con hello stessa proprietà</span><span class="sxs-lookup"><span data-stu-id="58d65-159">Find events with hello same property</span></span>
<span data-ttu-id="58d65-160">Trova hello tutti gli elementi con hello stesso valore della proprietà:</span><span class="sxs-lookup"><span data-stu-id="58d65-160">Find all hello items with hello same property value:</span></span>

![Fare clic con il pulsante destro del mouse su una proprietà](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="58d65-162">La ricerca di dati hello</span><span class="sxs-lookup"><span data-stu-id="58d65-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="58d65-163">toowrite query più complesse, aprire [ **Analitica** ](app-insights-analytics-tour.md) dalla parte superiore di hello del Pannello di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="58d65-164">È possibile cercare i termini in uno dei valori di proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="58d65-165">Ciò è particolarmente utile se sono stati scritti [eventi personalizzati](app-insights-api-custom-events-metrics.md) con i valori della proprietà.</span><span class="sxs-lookup"><span data-stu-id="58d65-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="58d65-166">È possibile tooset un intervallo di tempo, come le ricerche di un intervallo più breve è più veloce.</span><span class="sxs-lookup"><span data-stu-id="58d65-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="58d65-168">Cercare parole complete, non sottostringhe.</span><span class="sxs-lookup"><span data-stu-id="58d65-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="58d65-169">Utilizzare i caratteri speciali tooenclose tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="58d65-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="58d65-170">string</span><span class="sxs-lookup"><span data-stu-id="58d65-170">string</span></span> | <span data-ttu-id="58d65-171">*non* si trova con</span><span class="sxs-lookup"><span data-stu-id="58d65-171">is *not* found by</span></span> | <span data-ttu-id="58d65-172">ma si trova con</span><span class="sxs-lookup"><span data-stu-id="58d65-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58d65-173">ControllerHome.Info</span><span class="sxs-lookup"><span data-stu-id="58d65-173">HomeController.About</span></span> |<span data-ttu-id="58d65-174">home</span><span class="sxs-lookup"><span data-stu-id="58d65-174">home</span></span><br/><span data-ttu-id="58d65-175">controller</span><span class="sxs-lookup"><span data-stu-id="58d65-175">controller</span></span><br/><span data-ttu-id="58d65-176">fo</span><span class="sxs-lookup"><span data-stu-id="58d65-176">out</span></span> | <span data-ttu-id="58d65-177">controllerhome</span><span class="sxs-lookup"><span data-stu-id="58d65-177">homecontroller</span></span><br/><span data-ttu-id="58d65-178">info</span><span class="sxs-lookup"><span data-stu-id="58d65-178">about</span></span><br/><span data-ttu-id="58d65-179">"homecontroller.info"</span><span class="sxs-lookup"><span data-stu-id="58d65-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="58d65-180">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="58d65-180">United States</span></span>|<span data-ttu-id="58d65-181">Uni</span><span class="sxs-lookup"><span data-stu-id="58d65-181">Uni</span></span><br/><span data-ttu-id="58d65-182">ti</span><span class="sxs-lookup"><span data-stu-id="58d65-182">ted</span></span>|<span data-ttu-id="58d65-183">uniti</span><span class="sxs-lookup"><span data-stu-id="58d65-183">united</span></span><br/><span data-ttu-id="58d65-184">stati</span><span class="sxs-lookup"><span data-stu-id="58d65-184">states</span></span><br/><span data-ttu-id="58d65-185">uniti AND stati</span><span class="sxs-lookup"><span data-stu-id="58d65-185">united AND states</span></span><br/><span data-ttu-id="58d65-186">"stati uniti"</span><span class="sxs-lookup"><span data-stu-id="58d65-186">"united states"</span></span>

<span data-ttu-id="58d65-187">Di seguito sono espressioni di ricerca hello che è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="58d65-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="58d65-188">Query di esempio</span><span class="sxs-lookup"><span data-stu-id="58d65-188">Sample query</span></span> | <span data-ttu-id="58d65-189">Effetto</span><span class="sxs-lookup"><span data-stu-id="58d65-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="58d65-190">Trova tutti gli eventi nell'intervallo di tempo hello i cui campi includono la parola hello "apple"</span><span class="sxs-lookup"><span data-stu-id="58d65-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="58d65-191">Individuazione di eventi che contengono entrambe le parole.</span><span class="sxs-lookup"><span data-stu-id="58d65-191">Find events that contain both words.</span></span> <span data-ttu-id="58d65-192">Usare "AND" in lettere maiuscole, non "and".</span><span class="sxs-lookup"><span data-stu-id="58d65-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="58d65-193">Individuazione degli eventi che contengono una delle parole.</span><span class="sxs-lookup"><span data-stu-id="58d65-193">Find events that contain either word.</span></span> <span data-ttu-id="58d65-194">Usare "OR", non "or".</span><span class="sxs-lookup"><span data-stu-id="58d65-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="58d65-195">Forma breve.</span><span class="sxs-lookup"><span data-stu-id="58d65-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="58d65-196">Individuare gli eventi che contengono una parola, ma non hello altri.</span><span class="sxs-lookup"><span data-stu-id="58d65-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="58d65-197">campionamento</span><span class="sxs-lookup"><span data-stu-id="58d65-197">Sampling</span></span>
<span data-ttu-id="58d65-198">Se l'applicazione genera un grande quantità di dati di telemetria (e si sta utilizzando ASP.NET SDK versione 2.0.0-beta3 hello o versione successiva), il modulo di campionamento adattivo hello riduce automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="58d65-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="58d65-199">Tuttavia, gli eventi che sono correlato toohello stessa richiesta vengono selezionate o deselezionate come gruppo, in modo che è possibile spostarsi tra gli eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="58d65-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="58d65-200">[Informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="58d65-201">Creare un elemento di lavoro</span><span class="sxs-lookup"><span data-stu-id="58d65-201">Create work item</span></span>
<span data-ttu-id="58d65-202">È possibile creare un bug in GitHub o Visual Studio Team Services con i dettagli di hello da qualsiasi elemento di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58d65-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Fare clic su nuovo elemento di lavoro, modificare i campi di hello e quindi fare clic su OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="58d65-204">Hello prima volta, viene chiesto tooconfigure tooyour un collegamento Team Services account e del progetto.</span><span class="sxs-lookup"><span data-stu-id="58d65-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Immettere l'URL hello del server di Team Services e il nome di progetto hello, quindi fare clic su autorizza](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="58d65-206">(È inoltre possibile configurare il collegamento hello nel Pannello di elementi di lavoro hello.)</span><span class="sxs-lookup"><span data-stu-id="58d65-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="58d65-207">Salvare la ricerca</span><span class="sxs-lookup"><span data-stu-id="58d65-207">Save your search</span></span>
<span data-ttu-id="58d65-208">Dopo avere impostato tutti i filtri di hello desiderato, è possibile salvare la ricerca hello come preferito.</span><span class="sxs-lookup"><span data-stu-id="58d65-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="58d65-209">Se si utilizza un account aziendale, è possibile scegliere se tooshare con altri membri del team.</span><span class="sxs-lookup"><span data-stu-id="58d65-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Fare clic su preferito, impostare il nome di hello e fare clic su Salva](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="58d65-211">ricerca di hello toosee nuovamente, **pannello della panoramica passare toohello** e aprire Preferiti:</span><span class="sxs-lookup"><span data-stu-id="58d65-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Sezione Preferiti](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="58d65-213">Se è stato salvato con l'intervallo di tempo relativo, dati più recenti hello pannello riaperto hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="58d65-214">Se è stato salvato con l'intervallo di tempo assoluto, vedrai hello stessi dati ogni volta.</span><span class="sxs-lookup"><span data-stu-id="58d65-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="58d65-215">(Se 'Relative' non è disponibile quando si desidera toosave Preferiti, fare clic su intervallo di tempo nell'intestazione hello e impostare un intervallo di tempo che non è un intervallo personalizzato.)</span><span class="sxs-lookup"><span data-stu-id="58d65-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="58d65-216">Inviare ulteriori dati di telemetria tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="58d65-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="58d65-217">In aggiunta toohello di dialogo dati di telemetria inviato da Application Insights SDK, è possibile:</span><span class="sxs-lookup"><span data-stu-id="58d65-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="58d65-218">Acquisire le tracce del log dal framework di registrazione preferito in [.NET](app-insights-asp-net-trace-logs.md) o [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="58d65-219">Ciò significa che è possibile cercare le tracce del log e metterle in correlazione con le visualizzazioni pagina, le eccezioni e altri eventi.</span><span class="sxs-lookup"><span data-stu-id="58d65-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="58d65-220">[Scrivere codice](app-insights-api-custom-events-metrics.md) toosend eventi personalizzati, le visualizzazioni di pagina e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="58d65-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="58d65-221">[Informazioni su come toosend log e dati di telemetria personalizzati tooApplication Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="58d65-222"><a name="questions"></a>Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="58d65-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="58d65-223"><a name="limits"></a>Quanti dati vengono conservati?</span><span class="sxs-lookup"><span data-stu-id="58d65-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="58d65-224">Vedere hello [riepilogo limiti](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="58d65-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="58d65-225">Come è possibile visualizzare dati POST nelle richieste server?</span><span class="sxs-lookup"><span data-stu-id="58d65-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="58d65-226">È non registra i dati POST hello automaticamente, ma è possibile utilizzare [chiamate a TrackTrace o log](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="58d65-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="58d65-227">Inserire i dati POST hello nel parametro messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="58d65-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="58d65-228">Non è possibile filtrare il messaggio hello in hello stesso modo è possibile filtrare le proprietà, ma il limite di dimensioni di hello è più lungo.</span><span class="sxs-lookup"><span data-stu-id="58d65-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="58d65-229">Video</span><span class="sxs-lookup"><span data-stu-id="58d65-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="58d65-230"><a name="add"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58d65-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="58d65-231">Scrivere query complesse in Analytics</span><span class="sxs-lookup"><span data-stu-id="58d65-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="58d65-232">Inviare i log e dati di telemetria personalizzati tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="58d65-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="58d65-233">Configurare i test di disponibilità e velocità di risposta</span><span class="sxs-lookup"><span data-stu-id="58d65-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="58d65-234">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="58d65-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
