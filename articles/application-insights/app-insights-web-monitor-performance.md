---
title: "aaaMonitor integrità dell'applicazione e l'utilizzo con Application Insights"
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
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="d4da9-104">Monitorare le prestazioni di applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="d4da9-104">Monitor performance in web applications</span></span>


<span data-ttu-id="d4da9-105">Questo prodotto consente di accertarsi che le prestazioni della propria applicazione siano ottimali e di scoprire rapidamente eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="d4da9-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="d4da9-106">[Application Insights] [ start] informare eventuali problemi di prestazioni e le eccezioni e consentono di trovare e diagnosticare hello cause principali.</span><span class="sxs-lookup"><span data-stu-id="d4da9-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="d4da9-107">Application Insights può monitorare sia le applicazioni web Java e ASP.NET che i servizi, i servizi WCF.</span><span class="sxs-lookup"><span data-stu-id="d4da9-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="d4da9-108">Possono essere ospitati in locale, su macchine virtuali o come siti Web di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d4da9-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="d4da9-109">Sul lato client hello, Application Insights può richiedere dati di telemetria di pagine web e un'ampia gamma di dispositivi tra cui iOS, Android e App di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="d4da9-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="d4da9-110">È ora disponibile una nuova funzionalità per la ricerca delle pagine a basse prestazioni nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d4da9-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="d4da9-111">Se non si dispone di accesso tooit, abilitarla per la configurazione delle opzioni di anteprima con hello [pannello Anteprima](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="d4da9-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="d4da9-112">Informazioni su questa nuova esperienza in [individuare e correggere eventuali colli di bottiglia con analisi delle prestazioni interattivo hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="d4da9-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="d4da9-113"><a name="setup"></a>Configurare il monitoraggio delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d4da9-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="d4da9-114">Se non sono ancora stati aggiunti tooyour Application Insights (ovvero, se non dispone di Applicationinsights) del progetto, scegliere uno dei seguenti modi tooget avviato:</span><span class="sxs-lookup"><span data-stu-id="d4da9-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="d4da9-115">App Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d4da9-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="d4da9-116">Aggiungere il monitoraggio delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="d4da9-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="d4da9-117">Aggiungere il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="d4da9-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="d4da9-118">App web J2EE</span><span class="sxs-lookup"><span data-stu-id="d4da9-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="d4da9-119">Aggiungere il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="d4da9-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="d4da9-120"><a name="view"></a>Esplorare le metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d4da9-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="d4da9-121">In [hello Azure portal](https://portal.azure.com), Sfoglia risorsa di Application Insights toohello configurati per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4da9-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="d4da9-122">pannello della panoramica Hello Mostra i dati sulle prestazioni di base:</span><span class="sxs-lookup"><span data-stu-id="d4da9-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="d4da9-123">Fare clic su qualsiasi toosee grafico ulteriori dettagli e toosee risultati per un periodo più lungo.</span><span class="sxs-lookup"><span data-stu-id="d4da9-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="d4da9-124">Ad esempio, fare clic sul riquadro di richieste di hello e quindi selezionare un intervallo di tempo:</span><span class="sxs-lookup"><span data-stu-id="d4da9-124">For example, click hello Requests tile and then select a time range:</span></span>

![Fare clic sui dati toomore e selezionare un intervallo di tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="d4da9-126">Fare clic su un grafico toochoose le metriche Visualizza, o aggiungere un nuovo grafico e selezionare la metrica:</span><span class="sxs-lookup"><span data-stu-id="d4da9-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Scegliere una metrica toochoose grafico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="d4da9-128">**Deselezionare tutte le metriche di hello** toosee hello selezione completa che è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d4da9-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="d4da9-129">le metriche Hello rientrano in gruppi. Quando viene selezionato qualsiasi membro di un gruppo, hello altri membri del gruppo vengono visualizzate solo.</span><span class="sxs-lookup"><span data-stu-id="d4da9-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="d4da9-130"><a name="metrics"></a>Interpretazione dei dati</span><span class="sxs-lookup"><span data-stu-id="d4da9-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="d4da9-131">riquadri e report sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d4da9-131">Performance tiles and reports</span></span>
<span data-ttu-id="d4da9-132">È possibile ottenere diverse metriche delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d4da9-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="d4da9-133">Iniziamo con quelli che vengono visualizzati per impostazione predefinita nel pannello applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="d4da9-134">Requests</span><span class="sxs-lookup"><span data-stu-id="d4da9-134">Requests</span></span>
<span data-ttu-id="d4da9-135">numero di Hello di richieste HTTP ricevute in un periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="d4da9-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="d4da9-136">Confrontare i risultati di hello sui toosee altri report come app si comporta come carico hello varia.</span><span class="sxs-lookup"><span data-stu-id="d4da9-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="d4da9-137">Le richieste HTTP includono tutte le richieste GET o POST di pagine, dati e immagini.</span><span class="sxs-lookup"><span data-stu-id="d4da9-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="d4da9-138">Fare clic sui conteggi di hello riquadro tooget URL specifici.</span><span class="sxs-lookup"><span data-stu-id="d4da9-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="d4da9-139">Tempo di risposta medio</span><span class="sxs-lookup"><span data-stu-id="d4da9-139">Average response time</span></span>
<span data-ttu-id="d4da9-140">Tempo di hello misure tra una richiesta web immettere la risposta dell'applicazione e hello restituita.</span><span class="sxs-lookup"><span data-stu-id="d4da9-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="d4da9-141">Hello punti indicano Media mobile.</span><span class="sxs-lookup"><span data-stu-id="d4da9-141">hello points show a moving average.</span></span> <span data-ttu-id="d4da9-142">Se sono presenti numerose richieste, potrebbero esserci alcune si discostano da Media hello senza un picco ovvio o calo grafico hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="d4da9-143">Cercare picchi inconsueti.</span><span class="sxs-lookup"><span data-stu-id="d4da9-143">Look for unusual peaks.</span></span> <span data-ttu-id="d4da9-144">In generale, è probabile che toorise tempo di risposta con un aumento delle richieste.</span><span class="sxs-lookup"><span data-stu-id="d4da9-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="d4da9-145">Se aumento hello è eccessivo, l'app potrebbe raggiungere un limite di risorse, ad esempio CPU o hello capacità di un servizio che viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d4da9-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="d4da9-146">Fare clic su tempi di hello riquadro tooget per URL specifici.</span><span class="sxs-lookup"><span data-stu-id="d4da9-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="d4da9-147">Richieste lente</span><span class="sxs-lookup"><span data-stu-id="d4da9-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="d4da9-148">Mostra quali richieste potrebbero necessitare di un'ottimizzazione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d4da9-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="d4da9-149">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="d4da9-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="d4da9-150">La quantità di richieste che hanno restituito eccezioni non rilevate.</span><span class="sxs-lookup"><span data-stu-id="d4da9-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="d4da9-151">Fare clic su hello riquadro toosee hello dettagli degli errori specifici e selezionare toosee una singola richiesta di dettagli.</span><span class="sxs-lookup"><span data-stu-id="d4da9-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="d4da9-152">Viene conservato solo un campione di errori rappresentativi per l'analisi individuale.</span><span class="sxs-lookup"><span data-stu-id="d4da9-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="d4da9-153">Altre metriche</span><span class="sxs-lookup"><span data-stu-id="d4da9-153">Other metrics</span></span>
<span data-ttu-id="d4da9-154">toosee quali altre metriche, è possibile visualizzare, fare clic su un grafico e quindi deselezionare tutte hello metriche toosee hello completo insieme disponibile.</span><span class="sxs-lookup"><span data-stu-id="d4da9-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="d4da9-155">Fare clic su (i) toosee definizione di ogni metrica.</span><span class="sxs-lookup"><span data-stu-id="d4da9-155">Click (i) toosee each metric's definition.</span></span>

![Deselezionare tutte le metriche toosee hello intero insieme](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="d4da9-157">Selezionando qualsiasi hello Disabilita metrica ad altri utenti che non possono comparire in hello stesso grafico.</span><span class="sxs-lookup"><span data-stu-id="d4da9-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="d4da9-158">Impostazione di avvisi</span><span class="sxs-lookup"><span data-stu-id="d4da9-158">Set alerts</span></span>
<span data-ttu-id="d4da9-159">toobe una notifica tramite posta elettronica di valori insoliti per le metriche, aggiungere un avviso.</span><span class="sxs-lookup"><span data-stu-id="d4da9-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="d4da9-160">È possibile scegliere gli amministratori degli account toohello toosend hello posta elettronica o toospecific indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="d4da9-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="d4da9-161">Impostare altre proprietà di risorsa hello prima hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="d4da9-162">Non scegliere risorse webtest hello se si desidera ricevere avvisi di tooset relativi alle prestazioni o metrica di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="d4da9-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="d4da9-163">Essere unità hello toonote attenzione in cui viene chiesto di valore di soglia tooenter hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="d4da9-164">*Pulsante di hello Aggiungi avviso non è presente.*</span><span class="sxs-lookup"><span data-stu-id="d4da9-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="d4da9-165">-Si tratta di un toowhich di account di gruppo si dispone di accesso in sola lettura?</span><span class="sxs-lookup"><span data-stu-id="d4da9-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="d4da9-166">Contattare l'amministratore account hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="d4da9-167"><a name="diagnosis"></a>Diagnosi dei problemi</span><span class="sxs-lookup"><span data-stu-id="d4da9-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="d4da9-168">Di seguito vengono riportati alcuni suggerimenti su come trovare e diagnosticare i problemi di prestazioni:</span><span class="sxs-lookup"><span data-stu-id="d4da9-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="d4da9-169">Impostare [test web] [ availability] toobe ricevere un avviso se il sito web diventa inattivo o risponde in modo non corretto o lenta.</span><span class="sxs-lookup"><span data-stu-id="d4da9-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="d4da9-170">Se gli errori o rallentamento della risposta è correlati tooload, confrontare il numero di richieste hello con toosee altre metriche.</span><span class="sxs-lookup"><span data-stu-id="d4da9-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="d4da9-171">[Inserire e le istruzioni di traccia di ricerca] [ diagnostic] in toohelp il codice, individuare i problemi.</span><span class="sxs-lookup"><span data-stu-id="d4da9-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="d4da9-172">Monitorare l'applicazione Web in esecuzione con [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="d4da9-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="d4da9-173">Acquisire lo stato di hello dell'applicazione .net con [Debugger Snapshot][snapshot].</span><span class="sxs-lookup"><span data-stu-id="d4da9-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="d4da9-174">Individuare e risolvere i colli di bottiglia delle prestazioni con l'analisi interattiva delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d4da9-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="d4da9-175">È possibile utilizzare hello nuovo Application Insights prestazioni interattivo analisi toolocate aree dell'app Web che rallentano le prestazioni complessive.</span><span class="sxs-lookup"><span data-stu-id="d4da9-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="d4da9-176">È possibile eseguire rapidamente queste pagine specifiche di ricerca che rallentano e utilizzare hello [dello strumento di profilatura](app-insights-profiler.md) toosee se è presente una correlazione tra le pagine.</span><span class="sxs-lookup"><span data-stu-id="d4da9-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="d4da9-177">Creare un elenco delle pagine lente</span><span class="sxs-lookup"><span data-stu-id="d4da9-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="d4da9-178">Hello primo passaggio per la ricerca di problemi di prestazioni consiste tooget un elenco di hello lenta risponde pagine.</span><span class="sxs-lookup"><span data-stu-id="d4da9-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="d4da9-179">schermata di Hello seguito viene illustrato come utilizzare hello prestazioni pannello tooget un elenco di potenziali ulteriormente tooinvestigate di pagine.</span><span class="sxs-lookup"><span data-stu-id="d4da9-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="d4da9-180">È possibile visualizzare rapidamente da questa pagina che si è verificato un rallentamento hello tempi di risposta dell'applicazione hello a circa 6:00 PM e nuovamente a circa 10 PM.</span><span class="sxs-lookup"><span data-stu-id="d4da9-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="d4da9-181">È anche possibile vedere che hello/dettagli cliente operazione hanno operazioni a esecuzione prolungata alcune con un tempo di risposta mediano di 507.05 millisecondi.</span><span class="sxs-lookup"><span data-stu-id="d4da9-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Analisi interattiva delle prestazioni di Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="d4da9-183">Eseguire il drill-down in pagine specifiche</span><span class="sxs-lookup"><span data-stu-id="d4da9-183">Drill down on specific pages</span></span>

<span data-ttu-id="d4da9-184">Dopo aver ottenuto uno snapshot delle prestazioni dell'app, è possibile visualizzare altri dettagli sulle singole operazioni lente.</span><span class="sxs-lookup"><span data-stu-id="d4da9-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="d4da9-185">Fare clic su qualsiasi operazione nel hello toosee hello i dettagli dell'elenco come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4da9-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="d4da9-186">Tipo di grafico hello è possibile vedere se le prestazioni di hello sono basata su una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d4da9-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="d4da9-187">È inoltre possibile visualizzare quanti hello esperti di utenti diversi tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="d4da9-187">You can also see how many users experienced hello various response times.</span></span> 

![Pannello delle operazioni di Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="d4da9-189">Eseguire il drill-in un periodo di tempo specifico</span><span class="sxs-lookup"><span data-stu-id="d4da9-189">Drill down on a specific time period</span></span>

<span data-ttu-id="d4da9-190">Dopo aver identificato un punto nel tempo tooinvestigate, eseguire il drill-down toolook ulteriormente a operazioni specifiche di hello che potrebbero aver causato l'errore rallentamento delle prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="d4da9-191">Quando si fa clic su uno specifico punto nel tempo recuperare i dettagli di hello della pagina di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4da9-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="d4da9-192">In hello esempio riportato di seguito è possibile visualizzare le operazioni di hello elencate per un determinato periodo di tempo insieme ai codici di risposta server hello e durata dell'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="d4da9-193">È inoltre possibile hello url per l'apertura di un elemento di lavoro TFS se è necessario toosend il team di sviluppo tooyour informazioni.</span><span class="sxs-lookup"><span data-stu-id="d4da9-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Intervallo di tempo di Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="d4da9-195">Eseguire il drill-in un'operazione specifica</span><span class="sxs-lookup"><span data-stu-id="d4da9-195">Drill down on a specific operation</span></span>

<span data-ttu-id="d4da9-196">Dopo aver identificato un punto nel tempo tooinvestigate, eseguire il drill-down toolook ulteriormente a operazioni specifiche di hello che potrebbero aver causato l'errore rallentamento delle prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="d4da9-197">Fare clic su un'operazione da hello toosee hello i dettagli dell'elenco dell'operazione di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4da9-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="d4da9-198">In questo esempio che è possibile vedere che hello operazione non riuscita e ha fornito le informazioni di hello di hello per Application Insights ha generato un'applicazione hello eccezione.</span><span class="sxs-lookup"><span data-stu-id="d4da9-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="d4da9-199">È di nuovo possibile creare un elemento di lavoro TFS da questo pannello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Pannello dell'operazione di Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="d4da9-201"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4da9-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="d4da9-202">[Test Web] [ availability] -sono le richieste web inviate applicazione tooyour a intervalli regolari dal mondo hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="d4da9-203">[Acquisire e cercare le tracce di diagnostica] [ diagnostic] : inserire chiamate di traccia e tra i problemi di toopinpoint risultati hello.</span><span class="sxs-lookup"><span data-stu-id="d4da9-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="d4da9-204">[Monitorare l'utilizzo][usage]: possibilità di scoprire come le persone usano l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4da9-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="d4da9-205">[Domande e risposte e risoluzione dei problemi][qna]</span><span class="sxs-lookup"><span data-stu-id="d4da9-205">[Troubleshooting][qna] - and Q & A</span></span>



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



