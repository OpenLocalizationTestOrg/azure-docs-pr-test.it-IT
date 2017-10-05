---
title: Cosa fare in Azure Application Insights | Microsoft Docs
description: Domande frequenti in Application Insights
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="42355-103">Cosa fare in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="42355-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="42355-104">Per ricevere un messaggio di posta elettronica quando...</span><span class="sxs-lookup"><span data-stu-id="42355-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="42355-105">Inviare un messaggio di posta elettronica se il sito non è disponibile</span><span class="sxs-lookup"><span data-stu-id="42355-105">Email if my site goes down</span></span>
<span data-ttu-id="42355-106">Impostare un [test web di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="42355-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="42355-107">Inviare un messaggio di posta elettronica se il sito è sovraccarico</span><span class="sxs-lookup"><span data-stu-id="42355-107">Email if my site is overloaded</span></span>
<span data-ttu-id="42355-108">Impostare un [avviso](app-insights-alerts.md) per il **tempo di risposta del server**.</span><span class="sxs-lookup"><span data-stu-id="42355-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="42355-109">Una soglia compresa tra 1 e 2 secondi dovrebbe risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="42355-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="42355-110">L'applicazione potrebbe inoltre dare segni di difficoltà tramite la restituzione di codici di errore.</span><span class="sxs-lookup"><span data-stu-id="42355-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="42355-111">Impostare un avviso per le **richieste non riuscite**.</span><span class="sxs-lookup"><span data-stu-id="42355-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="42355-112">Se si desidera impostare un avviso per le **eccezioni del server**, è necessario effettuare [alcune impostazioni aggiuntive](app-insights-asp-net-exceptions.md) per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="42355-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="42355-113">Inviare un messaggio di posta elettronica in caso di eccezioni</span><span class="sxs-lookup"><span data-stu-id="42355-113">Email on exceptions</span></span>
1. [<span data-ttu-id="42355-114">Configurare il monitoraggio delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="42355-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="42355-115">[Impostare un avviso](app-insights-alerts.md) sulla metrica relativa al conteggio del numero di eccezioni</span><span class="sxs-lookup"><span data-stu-id="42355-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="42355-116">Inviare un messaggio di posta elettronica per un evento generato dall'app</span><span class="sxs-lookup"><span data-stu-id="42355-116">Email on an event in my app</span></span>
<span data-ttu-id="42355-117">Si supponga che si desidera ricevere un messaggio di posta elettronica quando si verifica un evento specifico.</span><span class="sxs-lookup"><span data-stu-id="42355-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="42355-118">Application Insights non fornisce direttamente questa funzionalità, ma è possibile [inviare un avviso quando una metrica supera una soglia](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="42355-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="42355-119">Gli avvisi possono essere impostati per [metriche personalizzate](app-insights-api-custom-events-metrics.md#trackmetric), anche se non per gli eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="42355-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="42355-120">Scrivere codice per potenziare una metrica quando si verifica l'evento:</span><span class="sxs-lookup"><span data-stu-id="42355-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="42355-121">oppure:</span><span class="sxs-lookup"><span data-stu-id="42355-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="42355-122">Poiché gli avvisi possono avere due stati, è necessario inviare un valore basso quando si presume che l'avviso sia terminato:</span><span class="sxs-lookup"><span data-stu-id="42355-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="42355-123">Creare un grafico in [Esplora metriche](app-insights-metrics-explorer.md) per visualizzare l'allarme:</span><span class="sxs-lookup"><span data-stu-id="42355-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="42355-124">Impostare un avviso da attivare quando la metrica supera un valore medio per un breve periodo:</span><span class="sxs-lookup"><span data-stu-id="42355-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="42355-125">Impostare il periodo medio sul valore minimo.</span><span class="sxs-lookup"><span data-stu-id="42355-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="42355-126">Verranno ricevuti messaggi di posta elettronica quando la metrica è maggiore o minore della soglia.</span><span class="sxs-lookup"><span data-stu-id="42355-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="42355-127">Alcune informazioni da considerare:</span><span class="sxs-lookup"><span data-stu-id="42355-127">Some points to consider:</span></span>

* <span data-ttu-id="42355-128">Un avviso dispone di due stati: "Avviso" e "Integro".</span><span class="sxs-lookup"><span data-stu-id="42355-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="42355-129">Lo stato viene valutato solo quando viene ricevuta una metrica.</span><span class="sxs-lookup"><span data-stu-id="42355-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="42355-130">Un messaggio di posta elettronica viene inviato solo quando lo stato cambia.</span><span class="sxs-lookup"><span data-stu-id="42355-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="42355-131">Questo è il motivo per cui è necessario inviare sia metriche con valori alti che metriche con valori bassi.</span><span class="sxs-lookup"><span data-stu-id="42355-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="42355-132">Per valutare l'avviso, viene eseguita la media dei valori ricevuti nel periodo precedente.</span><span class="sxs-lookup"><span data-stu-id="42355-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="42355-133">Ciò si verifica ogni volta che viene ricevuta una metrica. Per questo motivo è possibile che i messaggi di posta elettronica vengano inviati più frequentemente rispetto al periodo impostato.</span><span class="sxs-lookup"><span data-stu-id="42355-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="42355-134">Poiché vengono inviati messaggi di posta elettronica sia per avvisi con stato "Avviso" e che per avvisi con stato "Integro", è possibile riconsiderare l'evento unico come una condizione con due stati.</span><span class="sxs-lookup"><span data-stu-id="42355-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="42355-135">Ad esempio, anziché un evento "processo completato", creare una condizione "processo in corso", dove è possibile ricevere messaggi di posta elettronica all'inizio e alla fine di un processo.</span><span class="sxs-lookup"><span data-stu-id="42355-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="42355-136">Impostare automaticamente gli avvisi</span><span class="sxs-lookup"><span data-stu-id="42355-136">Set up alerts automatically</span></span>
[<span data-ttu-id="42355-137">Usare PowerShell per creare nuovi avvisi</span><span class="sxs-lookup"><span data-stu-id="42355-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="42355-138">Usare PowerShell per gestire Application Insights</span><span class="sxs-lookup"><span data-stu-id="42355-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="42355-139">Creare nuove risorse</span><span class="sxs-lookup"><span data-stu-id="42355-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="42355-140">Creare nuovi avvisi</span><span class="sxs-lookup"><span data-stu-id="42355-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="42355-141">Separare la telemetria da diverse versioni</span><span class="sxs-lookup"><span data-stu-id="42355-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="42355-142">Più ruoli in un'app: usare una singola risorsa di Application Insights e filtrare su cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="42355-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="42355-143">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="42355-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="42355-144">Separazione di sviluppo, test e versioni di rilascio: usare diverse risorse di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="42355-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="42355-145">Acquisire le chiavi di strumentazione da web.config. [Altre informazioni](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="42355-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="42355-146">Creazione di rapporti sulle versioni di compilazione: aggiungere una proprietà usando un inizializzatore di telemetria.</span><span class="sxs-lookup"><span data-stu-id="42355-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="42355-147">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="42355-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="42355-148">Monitorare i server back-end e le app desktop</span><span class="sxs-lookup"><span data-stu-id="42355-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="42355-149">[Usare il modulo di Windows Server SDK](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="42355-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="42355-150">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="42355-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="42355-151">Dashboard con metriche da più app</span><span class="sxs-lookup"><span data-stu-id="42355-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="42355-152">In [Esplora metriche](app-insights-metrics-explorer.md)personalizzare il grafico e salvarlo come preferito.</span><span class="sxs-lookup"><span data-stu-id="42355-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="42355-153">Aggiungerlo al dashboard di Azure.</span><span class="sxs-lookup"><span data-stu-id="42355-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="42355-154">Dashboard con dati provenienti da altre fonti e Application Insights</span><span class="sxs-lookup"><span data-stu-id="42355-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="42355-155">[Esportare dati di telemetria in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="42355-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="42355-156">Or</span><span class="sxs-lookup"><span data-stu-id="42355-156">Or</span></span>

* <span data-ttu-id="42355-157">Usare SharePoint come dashboard, dove i dati vengono visualizzati in Web part di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42355-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="42355-158">[Usare l'esportazione continua e l'analisi dei flussi per eseguire l'esportazione in SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="42355-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="42355-159">Usare PowerView per esaminare il database e creare una Web part di SharePoint per PowerView.</span><span class="sxs-lookup"><span data-stu-id="42355-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="42355-160">Filtrare gli utenti anonimi o autenticati</span><span class="sxs-lookup"><span data-stu-id="42355-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="42355-161">Se gli utenti effettuano l'accesso, è possibile impostare l' [ID dell'utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users). Questa operazione non viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42355-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="42355-162">È quindi possibile:</span><span class="sxs-lookup"><span data-stu-id="42355-162">You can then:</span></span>

* <span data-ttu-id="42355-163">Eseguire ricerche in base a ID utente specifici</span><span class="sxs-lookup"><span data-stu-id="42355-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="42355-164">Filtrare le metriche in base a utenti anonimi o autenticati</span><span class="sxs-lookup"><span data-stu-id="42355-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="42355-165">Modificare i nomi della proprietà o i valori</span><span class="sxs-lookup"><span data-stu-id="42355-165">Modify property names or values</span></span>
<span data-ttu-id="42355-166">Creare un [filtro](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="42355-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="42355-167">Consente di modificare o filtrare la telemetria prima che venga inviata dall'app ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="42355-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="42355-168">Elencare utenti specifici e il relativo uso</span><span class="sxs-lookup"><span data-stu-id="42355-168">List specific users and their usage</span></span>
<span data-ttu-id="42355-169">Se si desidera [cercare utenti specifici](#search-specific-users), è possibile impostare l'[ID dell'utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="42355-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="42355-170">Se si desidera un elenco di utenti con i dati quali, ad esempio, le pagine visualizzate o la frequenza di accesso, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="42355-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="42355-171">[Impostare l'ID dell'utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users), [eseguire l'esportazione in un database](app-insights-code-sample-export-sql-stream-analytics.md) e usare gli strumenti appropriati per analizzare i dati utente.</span><span class="sxs-lookup"><span data-stu-id="42355-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="42355-172">Se si dispone solo di un numero limitato di utenti, inviare gli eventi o le metriche personalizzati usando i dati di interesse quali, ad esempio, il valore della metrica o il nome dell'evento, quindi impostando l'ID utente come proprietà.</span><span class="sxs-lookup"><span data-stu-id="42355-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="42355-173">Per analizzare le visualizzazioni di pagina, sostituire la chiamata standard JavaScript trackPageView.</span><span class="sxs-lookup"><span data-stu-id="42355-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="42355-174">Per analizzare i dati di telemetria sul lato server, usare un inizializzatore di telemetria per aggiungere l'ID utente a tutti i dati di telemetria del server.</span><span class="sxs-lookup"><span data-stu-id="42355-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="42355-175">È quindi possibile filtrare e segmentare le metriche e le ricerche in base all'ID utente.</span><span class="sxs-lookup"><span data-stu-id="42355-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="42355-176">Ridurre il traffico dall'app ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="42355-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="42355-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)disabilitare tutti i moduli non necessari, come gli agenti di raccolta del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="42355-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="42355-178">Usare [Campionamento e filtri](app-insights-api-filtering-sampling.md) nell’SDK.</span><span class="sxs-lookup"><span data-stu-id="42355-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="42355-179">Nelle pagine Web limitare il numero di chiamate Ajax segnalato per ogni visualizzazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="42355-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="42355-180">Nel frammento di script dopo `instrumentationKey:...` inserire: `,maxAjaxCallsPerView:3` (o un numero adatto).</span><span class="sxs-lookup"><span data-stu-id="42355-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="42355-181">Se si usa [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), calcolare l'aggregazione di batch di valori delle metriche prima di inviare il risultato.</span><span class="sxs-lookup"><span data-stu-id="42355-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="42355-182">Un overload di TrackMetric() esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="42355-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="42355-183">Altre informazioni su [prezzi e quote](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="42355-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="42355-184">Disabilitare telemetria</span><span class="sxs-lookup"><span data-stu-id="42355-184">Disable telemetry</span></span>
<span data-ttu-id="42355-185">Per **avviare e arrestare in modo dinamico** la raccolta e la trasmissione di dati di telemetria dal server:</span><span class="sxs-lookup"><span data-stu-id="42355-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="42355-186">Per **disabilitare gli agenti di raccolta standard selezionati** - ad esempio, i contatori delle prestazioni, delle richieste HTTP o delle dipendenze - eliminare o impostare come commento le righe pertinenti in [Applicationinsights.config](app-insights-api-custom-events-metrics.md). È possibile eseguire questa operazione, ad esempio, se si vogliono inviare i propri dati TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="42355-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="42355-187">Visualizzare i contatori delle prestazioni di sistema</span><span class="sxs-lookup"><span data-stu-id="42355-187">View system performance counters</span></span>
<span data-ttu-id="42355-188">Tra le metriche che è possibile visualizzare in Esplora metriche è disponibile un set di contatori delle prestazioni di sistema.</span><span class="sxs-lookup"><span data-stu-id="42355-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="42355-189">Esiste un pannello predefinito denominato **Server** in cui sono visualizzati alcuni set.</span><span class="sxs-lookup"><span data-stu-id="42355-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Aprire la risorsa Application Insights e fare clic su Server.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="42355-191">Se non vengono visualizzati dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="42355-191">If you see no performance counter data</span></span>
* <span data-ttu-id="42355-192">**Server IIS** sul proprio computer o in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="42355-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="42355-193">[Installare Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="42355-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="42355-194">**Sito Web di Azure** - i contatori delle prestazioni non sono ancora supportati.</span><span class="sxs-lookup"><span data-stu-id="42355-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="42355-195">Esistono diverse metriche che è possibile ottenere come una parte standard del Pannello di controllo del sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="42355-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="42355-196">**Server Unix** - [Installare collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="42355-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="42355-197">Per visualizzare altri contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="42355-197">To display more performance counters</span></span>
* <span data-ttu-id="42355-198">Innanzitutto [aggiungere un nuovo grafico](app-insights-metrics-explorer.md) e verificare che il contatore sia incluso nel set di base offerto.</span><span class="sxs-lookup"><span data-stu-id="42355-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="42355-199">In caso contrario, [aggiungere il contatore al set raccolto dal modulo del contatore delle prestazioni](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="42355-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
