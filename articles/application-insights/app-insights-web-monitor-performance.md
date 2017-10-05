---
title: "Monitoraggio dell'integrità e dell'utilizzo di un'app con Application Insights"
description: "Introduzione a Application Insights. Analizzare l'uso, la disponibilità e le prestazioni delle applicazioni locali o Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="7cf03-104">Monitorare le prestazioni di applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="7cf03-104">Monitor performance in web applications</span></span>


<span data-ttu-id="7cf03-105">Questo prodotto consente di accertarsi che le prestazioni della propria applicazione siano ottimali e di scoprire rapidamente eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="7cf03-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="7cf03-106">[Application Insights][start] rileverà eventuali eccezioni e problemi relativi alle prestazioni e aiuterà a individuare e diagnosticare le cause principali.</span><span class="sxs-lookup"><span data-stu-id="7cf03-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="7cf03-107">Application Insights può monitorare sia le applicazioni web Java e ASP.NET che i servizi, i servizi WCF.</span><span class="sxs-lookup"><span data-stu-id="7cf03-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="7cf03-108">Possono essere ospitati in locale, su macchine virtuali o come siti Web di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7cf03-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="7cf03-109">Sul lato client, Application Insights può richiedere dati di telemetria di pagine web e un'ampia gamma di dispositivi, tra l’app Store iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="7cf03-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="7cf03-110">È ora disponibile una nuova funzionalità per la ricerca delle pagine a basse prestazioni nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="7cf03-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="7cf03-111">Se non si ha accesso alla funzionalità, abilitarla configurando le opzioni di anteprima usando il [pannello Anteprima](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="7cf03-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="7cf03-112">Leggere le informazioni su questa nuova funzionalità in [Individuare e risolvere i colli di bottiglia delle prestazioni con l'analisi interattiva delle prestazioni](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="7cf03-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="7cf03-113"><a name="setup"></a>Configurare il monitoraggio delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7cf03-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="7cf03-114">Se Application Insights non è stato ancora aggiunto al progetto (vale a dire, se ApplicationInsights.config non è presente), scegliere uno dei modi seguenti per iniziare:</span><span class="sxs-lookup"><span data-stu-id="7cf03-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="7cf03-115">App Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7cf03-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="7cf03-116">Aggiungere il monitoraggio delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="7cf03-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="7cf03-117">Aggiungere il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7cf03-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="7cf03-118">App web J2EE</span><span class="sxs-lookup"><span data-stu-id="7cf03-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="7cf03-119">Aggiungere il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7cf03-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="7cf03-120"><a name="view"></a>Esplorare le metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7cf03-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="7cf03-121">Nel [portale di Azure](https://portal.azure.com), passare alla risorsa di Application Insights impostata per la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cf03-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="7cf03-122">Il pannello della panoramica mostra i dati delle prestazioni di base:</span><span class="sxs-lookup"><span data-stu-id="7cf03-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="7cf03-123">Fare clic su un riquadro qualsiasi per visualizzare altri dettagli e per vedere i risultati relativi a un periodo più lungo.</span><span class="sxs-lookup"><span data-stu-id="7cf03-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="7cf03-124">Ad esempio, fare clic sul riquadro delle richieste e quindi selezionare un intervallo di tempo:</span><span class="sxs-lookup"><span data-stu-id="7cf03-124">For example, click the Requests tile and then select a time range:</span></span>

![Fare clic per visualizzare più dati e selezionare un intervallo di tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="7cf03-126">Fare clic su un grafico per scegliere quali metriche visualizzare oppure aggiungere un nuovo grafico e selezionarne le metriche:</span><span class="sxs-lookup"><span data-stu-id="7cf03-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Fare clic su un grafico per scegliere le metriche](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="7cf03-128">**Deselezionare tutte le metriche** per visualizzare la selezione completa disponibile.</span><span class="sxs-lookup"><span data-stu-id="7cf03-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="7cf03-129">Le metriche sono suddivise in gruppi; quando si seleziona qualsiasi membro di un gruppo, vengono visualizzati solo gli altri membri di quel gruppo.</span><span class="sxs-lookup"><span data-stu-id="7cf03-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="7cf03-130"><a name="metrics"></a>Interpretazione dei dati</span><span class="sxs-lookup"><span data-stu-id="7cf03-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="7cf03-131">riquadri e report sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7cf03-131">Performance tiles and reports</span></span>
<span data-ttu-id="7cf03-132">È possibile ottenere diverse metriche delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7cf03-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="7cf03-133">Vengono analizzate innanzitutto quelle visualizzate per impostazione predefinita nel pannello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cf03-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="7cf03-134">Richieste</span><span class="sxs-lookup"><span data-stu-id="7cf03-134">Requests</span></span>
<span data-ttu-id="7cf03-135">Il numero di richieste HTTP ricevute in un periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="7cf03-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="7cf03-136">Confrontare questo numero con i risultati di altri report per analizzare il comportamento dell'app al variare del carico.</span><span class="sxs-lookup"><span data-stu-id="7cf03-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="7cf03-137">Le richieste HTTP includono tutte le richieste GET o POST di pagine, dati e immagini.</span><span class="sxs-lookup"><span data-stu-id="7cf03-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="7cf03-138">Fare clic sul riquadro per visualizzare i conteggi per URL specifici.</span><span class="sxs-lookup"><span data-stu-id="7cf03-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="7cf03-139">Tempo medio di risposta</span><span class="sxs-lookup"><span data-stu-id="7cf03-139">Average response time</span></span>
<span data-ttu-id="7cf03-140">Misura il tempo intercorso tra la ricezione di una richiesta Web da parte dell'applicazione e la risposta restituita.</span><span class="sxs-lookup"><span data-stu-id="7cf03-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="7cf03-141">I punti mostrano una media mobile.</span><span class="sxs-lookup"><span data-stu-id="7cf03-141">The points show a moving average.</span></span> <span data-ttu-id="7cf03-142">Se le richieste sono numerose, alcune di queste potrebbero deviare dalla media senza mostrare un picco o un calo evidente nel grafico.</span><span class="sxs-lookup"><span data-stu-id="7cf03-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="7cf03-143">Cercare picchi inconsueti.</span><span class="sxs-lookup"><span data-stu-id="7cf03-143">Look for unusual peaks.</span></span> <span data-ttu-id="7cf03-144">In genere, il tempo di risposta aumenta con l'aumento delle richieste.</span><span class="sxs-lookup"><span data-stu-id="7cf03-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="7cf03-145">Se l'aumento è sproporzionato, l'app potrebbe aver raggiunto un limite di risorsa, ad esempio dovuto alla CPU o alla capacità di un servizio che utilizza.</span><span class="sxs-lookup"><span data-stu-id="7cf03-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="7cf03-146">Fare clic sul riquadro per visualizzare i tempi per URL specifici.</span><span class="sxs-lookup"><span data-stu-id="7cf03-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="7cf03-147">Richieste lente</span><span class="sxs-lookup"><span data-stu-id="7cf03-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="7cf03-148">Mostra quali richieste potrebbero necessitare di un'ottimizzazione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7cf03-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="7cf03-149">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="7cf03-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="7cf03-150">La quantità di richieste che hanno restituito eccezioni non rilevate.</span><span class="sxs-lookup"><span data-stu-id="7cf03-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="7cf03-151">Fare clic sul riquadro per visualizzare i dettagli di errori specifici e selezionare una singola richiesta per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="7cf03-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="7cf03-152">Viene conservato solo un campione di errori rappresentativi per l'analisi individuale.</span><span class="sxs-lookup"><span data-stu-id="7cf03-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="7cf03-153">Altre metriche</span><span class="sxs-lookup"><span data-stu-id="7cf03-153">Other metrics</span></span>
<span data-ttu-id="7cf03-154">Per sapere quali altri metriche è possibile visualizzare, fare clic su un grafico e deselezionare tutte le metriche per vedere l'intero set disponibile.</span><span class="sxs-lookup"><span data-stu-id="7cf03-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="7cf03-155">Fare clic su (i) per visualizzare la definizione di ciascuna metrica.</span><span class="sxs-lookup"><span data-stu-id="7cf03-155">Click (i) to see each metric's definition.</span></span>

![Deselezionare tutte le metriche per visualizzare l'intero set](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="7cf03-157">La selezione di una metrica disabilita le altre metriche che non possono essere visualizzate nello stesso grafico.</span><span class="sxs-lookup"><span data-stu-id="7cf03-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="7cf03-158">Impostazione di avvisi</span><span class="sxs-lookup"><span data-stu-id="7cf03-158">Set alerts</span></span>
<span data-ttu-id="7cf03-159">Per ricevere tramite posta elettronica una notifica relativa a valori insoliti di una metrica, aggiungere un avviso.</span><span class="sxs-lookup"><span data-stu-id="7cf03-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="7cf03-160">È possibile scegliere di inviare il messaggio di posta elettronica agli amministratori di account o a indirizzi di posta elettronica specifici.</span><span class="sxs-lookup"><span data-stu-id="7cf03-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="7cf03-161">Impostare la risorsa prima delle altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="7cf03-161">Set the resource before the other properties.</span></span> <span data-ttu-id="7cf03-162">Non scegliere le risorse webtest se si desidera impostare avvisi sulle metriche relative a prestazioni o utilizzo.</span><span class="sxs-lookup"><span data-stu-id="7cf03-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="7cf03-163">Prendere nota delle unità in cui viene chiesto di immettere il valore soglia.</span><span class="sxs-lookup"><span data-stu-id="7cf03-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="7cf03-164">*Il pulsante Aggiungi avviso non è visibile.*</span><span class="sxs-lookup"><span data-stu-id="7cf03-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="7cf03-165">Si tratta di un account di gruppo al quale è possibile accedere in sola lettura?</span><span class="sxs-lookup"><span data-stu-id="7cf03-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="7cf03-166">Rivolgersi all'amministratore dell'account.</span><span class="sxs-lookup"><span data-stu-id="7cf03-166">Check with the account administrator.</span></span>

## <span data-ttu-id="7cf03-167"><a name="diagnosis"></a>Diagnosi dei problemi</span><span class="sxs-lookup"><span data-stu-id="7cf03-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="7cf03-168">Di seguito vengono riportati alcuni suggerimenti su come trovare e diagnosticare i problemi di prestazioni:</span><span class="sxs-lookup"><span data-stu-id="7cf03-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="7cf03-169">Configurare i [test Web][availability] in modo da ricevere un avviso se il sito Web non risponde o risponde in maniera non corretta o lentamente.</span><span class="sxs-lookup"><span data-stu-id="7cf03-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="7cf03-170">Confrontare il conteggio delle richieste con altre metriche per verificare se gli errori o la risposta lenta sono collegati al carico.</span><span class="sxs-lookup"><span data-stu-id="7cf03-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="7cf03-171">[Inserire e cercare istruzioni di traccia][diagnostic] nel codice per individuare i problemi.</span><span class="sxs-lookup"><span data-stu-id="7cf03-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="7cf03-172">Monitorare l'applicazione Web in esecuzione con [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="7cf03-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="7cf03-173">Acquisire lo stato dell'applicazione .Net con il [debugger di snapshot][snapshot].</span><span class="sxs-lookup"><span data-stu-id="7cf03-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="7cf03-174">Individuare e risolvere i colli di bottiglia delle prestazioni con l'analisi interattiva delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7cf03-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="7cf03-175">È possibile usare la nuova analisi interattiva delle prestazioni di Application Insights per individuare le aree dell'app Web che riducono le prestazioni generali.</span><span class="sxs-lookup"><span data-stu-id="7cf03-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="7cf03-176">È possibile individuare rapidamente le singole pagine lente e usare lo [strumento di profilatura](app-insights-profiler.md) per verificare la presenza di una correlazione tra le pagine.</span><span class="sxs-lookup"><span data-stu-id="7cf03-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="7cf03-177">Creare un elenco delle pagine lente</span><span class="sxs-lookup"><span data-stu-id="7cf03-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="7cf03-178">La prima operazione da eseguire per individuare i problemi di prestazioni consiste nell'ottenere un elenco delle pagine che rispondono lentamente.</span><span class="sxs-lookup"><span data-stu-id="7cf03-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="7cf03-179">Lo screenshot seguente illustra l'uso del pannello Prestazioni per ottenere un elenco delle possibili pagine che meritano un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="7cf03-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="7cf03-180">Nella pagina è immediatamente evidente che si è verificato un rallentamento nel tempo di risposta dell'app alle 18:00 e di nuovo alle 22:00.</span><span class="sxs-lookup"><span data-stu-id="7cf03-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="7cf03-181">È anche possibile osservare che l'operazione GET customer/details (Ottieni clienti/dettagli) ha incluso operazioni di lunga durata con un tempo di risposta medio di 507,05 millisecondi.</span><span class="sxs-lookup"><span data-stu-id="7cf03-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Analisi interattiva delle prestazioni di Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="7cf03-183">Eseguire il drill-down in pagine specifiche</span><span class="sxs-lookup"><span data-stu-id="7cf03-183">Drill down on specific pages</span></span>

<span data-ttu-id="7cf03-184">Dopo aver ottenuto uno snapshot delle prestazioni dell'app, è possibile visualizzare altri dettagli sulle singole operazioni lente.</span><span class="sxs-lookup"><span data-stu-id="7cf03-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="7cf03-185">Fare clic su un'operazione nell'elenco per visualizzare i dettagli come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cf03-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="7cf03-186">Dal grafico è possibile determinare se le prestazioni erano basate su una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="7cf03-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="7cf03-187">È anche possibile visualizzare il numero di utenti per i quali si sono verificati i diversi tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="7cf03-187">You can also see how many users experienced the various response times.</span></span> 

![Pannello delle operazioni di Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="7cf03-189">Eseguire il drill-in un periodo di tempo specifico</span><span class="sxs-lookup"><span data-stu-id="7cf03-189">Drill down on a specific time period</span></span>

<span data-ttu-id="7cf03-190">Dopo aver identificato un periodo di tempo da analizzare, eseguire il drill-down per visualizzare le operazioni specifiche che potrebbero aver causato il rallentamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7cf03-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="7cf03-191">Quando si fa clic in un periodo di tempo specifico vengono visualizzati i dettagli della pagina come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cf03-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="7cf03-192">Nell'esempio seguente sono elencate le operazioni per ogni periodo di tempo con i codici di risposta del server e la durata dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="7cf03-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="7cf03-193">È disponibile anche l'URL per aprire un elemento di lavoro TFS per inviare queste informazioni al team di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="7cf03-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Intervallo di tempo di Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="7cf03-195">Eseguire il drill-in un'operazione specifica</span><span class="sxs-lookup"><span data-stu-id="7cf03-195">Drill down on a specific operation</span></span>

<span data-ttu-id="7cf03-196">Dopo aver identificato un periodo di tempo da analizzare, eseguire il drill-down per visualizzare le operazioni specifiche che potrebbero aver causato il rallentamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7cf03-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="7cf03-197">Fare clic su un'operazione nell'elenco per visualizzare i dettagli dell'operazione, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cf03-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="7cf03-198">In questo esempio l'operazione non è stata eseguita e Application Insights ha visualizzato i dettagli dell'eccezione generata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cf03-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="7cf03-199">È di nuovo possibile creare un elemento di lavoro TFS da questo pannello.</span><span class="sxs-lookup"><span data-stu-id="7cf03-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Pannello dell'operazione di Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="7cf03-201"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cf03-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="7cf03-202">[Test Web][availability]: possibilità di inviare richieste Web all'applicazione a intervalli regolari da tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="7cf03-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="7cf03-203">[Acquisire e cercare tracce diagnostiche][diagnostic]: possibilità di inserire chiamate di traccia ed esaminare i risultati per individuare i problemi.</span><span class="sxs-lookup"><span data-stu-id="7cf03-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="7cf03-204">[Monitorare l'utilizzo][usage]: possibilità di scoprire come le persone usano l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cf03-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="7cf03-205">[Domande e risposte e risoluzione dei problemi][qna]</span><span class="sxs-lookup"><span data-stu-id="7cf03-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



