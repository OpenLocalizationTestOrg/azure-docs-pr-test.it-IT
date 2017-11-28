---
title: aaaHow posso... in Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="a34f8-103">Cosa fare in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="a34f8-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="a34f8-104">Per ricevere un messaggio di posta elettronica quando...</span><span class="sxs-lookup"><span data-stu-id="a34f8-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="a34f8-105">Inviare un messaggio di posta elettronica se il sito non è disponibile</span><span class="sxs-lookup"><span data-stu-id="a34f8-105">Email if my site goes down</span></span>
<span data-ttu-id="a34f8-106">Impostare un [test web di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="a34f8-107">Inviare un messaggio di posta elettronica se il sito è sovraccarico</span><span class="sxs-lookup"><span data-stu-id="a34f8-107">Email if my site is overloaded</span></span>
<span data-ttu-id="a34f8-108">Impostare un [avviso](app-insights-alerts.md) per il **tempo di risposta del server**.</span><span class="sxs-lookup"><span data-stu-id="a34f8-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="a34f8-109">Una soglia compresa tra 1 e 2 secondi dovrebbe risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a34f8-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="a34f8-110">L'applicazione potrebbe inoltre dare segni di difficoltà tramite la restituzione di codici di errore.</span><span class="sxs-lookup"><span data-stu-id="a34f8-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="a34f8-111">Impostare un avviso per le **richieste non riuscite**.</span><span class="sxs-lookup"><span data-stu-id="a34f8-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="a34f8-112">Se si desidera un avviso tooset **eccezioni Server**, potrebbe essere toodo [alcune impostazioni aggiuntive](app-insights-asp-net-exceptions.md) dati toosee degli ordini.</span><span class="sxs-lookup"><span data-stu-id="a34f8-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="a34f8-113">Inviare un messaggio di posta elettronica in caso di eccezioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-113">Email on exceptions</span></span>
1. [<span data-ttu-id="a34f8-114">Configurare il monitoraggio delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="a34f8-115">[Impostare un avviso](app-insights-alerts.md) su hello eccezione conteggio metrica</span><span class="sxs-lookup"><span data-stu-id="a34f8-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="a34f8-116">Inviare un messaggio di posta elettronica per un evento generato dall'app</span><span class="sxs-lookup"><span data-stu-id="a34f8-116">Email on an event in my app</span></span>
<span data-ttu-id="a34f8-117">Si supponga che desideri tooget un messaggio di posta elettronica quando si verifica un evento specifico.</span><span class="sxs-lookup"><span data-stu-id="a34f8-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="a34f8-118">Application Insights non fornisce direttamente questa funzionalità, ma è possibile [inviare un avviso quando una metrica supera una soglia](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="a34f8-119">Gli avvisi possono essere impostati per [metriche personalizzate](app-insights-api-custom-events-metrics.md#trackmetric), anche se non per gli eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a34f8-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="a34f8-120">Scrivere alcuni tooincrease codice una metrica, quando si verifica l'evento hello:</span><span class="sxs-lookup"><span data-stu-id="a34f8-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="a34f8-121">oppure:</span><span class="sxs-lookup"><span data-stu-id="a34f8-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="a34f8-122">Poiché gli avvisi hanno due stati, occorre toosend un valore basso quando si considera l'avviso hello toohave terminato:</span><span class="sxs-lookup"><span data-stu-id="a34f8-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="a34f8-123">Creare un grafico in [Esplora metrica](app-insights-metrics-explorer.md) toosee l'allarme:</span><span class="sxs-lookup"><span data-stu-id="a34f8-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="a34f8-124">Impostare ora toofire un avviso quando la metrica hello supera un valore medio per un breve periodo:</span><span class="sxs-lookup"><span data-stu-id="a34f8-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="a34f8-125">Impostare hello toohello periodo minimo di una Media.</span><span class="sxs-lookup"><span data-stu-id="a34f8-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="a34f8-126">Messaggi di posta elettronica viene visualizzato quando la metrica hello supera il numero sia inferiore alla soglia hello.</span><span class="sxs-lookup"><span data-stu-id="a34f8-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="a34f8-127">Tooconsider alcuni punti:</span><span class="sxs-lookup"><span data-stu-id="a34f8-127">Some points tooconsider:</span></span>

* <span data-ttu-id="a34f8-128">Un avviso dispone di due stati: "Avviso" e "Integro".</span><span class="sxs-lookup"><span data-stu-id="a34f8-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="a34f8-129">stato Hello viene valutato solo quando viene ricevuta una metrica.</span><span class="sxs-lookup"><span data-stu-id="a34f8-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="a34f8-130">Un messaggio di posta elettronica viene inviato solo quando cambia lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="a34f8-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="a34f8-131">È per questo motivo è toosend metriche sia alte e basso valore.</span><span class="sxs-lookup"><span data-stu-id="a34f8-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="a34f8-132">avviso hello tooevaluate, Media hello viene eseguito di valori hello ricevuto su hello precedente.</span><span class="sxs-lookup"><span data-stu-id="a34f8-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="a34f8-133">Ciò si verifica ogni volta che viene ricevuta una metrica, in modo da messaggi di posta elettronica possono essere inviati più frequentemente rispetto al periodo di hello che è impostato.</span><span class="sxs-lookup"><span data-stu-id="a34f8-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="a34f8-134">Poiché i messaggi di posta elettronica vengono inviati "avviso" e "Integro", è opportuno tooconsider pensiero nuovamente l'evento monofase come una condizione di due stati.</span><span class="sxs-lookup"><span data-stu-id="a34f8-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="a34f8-135">Ad esempio, anziché un evento "processo completato", avere una condizione "processo in corso", in cui si ricevono messaggi di posta elettronica nella hello iniziale e finale di un processo.</span><span class="sxs-lookup"><span data-stu-id="a34f8-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="a34f8-136">Impostare automaticamente gli avvisi</span><span class="sxs-lookup"><span data-stu-id="a34f8-136">Set up alerts automatically</span></span>
[<span data-ttu-id="a34f8-137">Utilizzare PowerShell toocreate nuovi avvisi</span><span class="sxs-lookup"><span data-stu-id="a34f8-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="a34f8-138">Usare PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="a34f8-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="a34f8-139">Creare nuove risorse</span><span class="sxs-lookup"><span data-stu-id="a34f8-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="a34f8-140">Creare nuovi avvisi</span><span class="sxs-lookup"><span data-stu-id="a34f8-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="a34f8-141">Separare la telemetria da diverse versioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="a34f8-142">Più ruoli in un'app: usare una singola risorsa di Application Insights e filtrare su cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="a34f8-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="a34f8-143">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="a34f8-144">Separazione di sviluppo, test e versioni di rilascio: usare diverse risorse di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a34f8-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="a34f8-145">Selezionare le chiavi di strumentazione hello da Web. config. [Altre informazioni](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a34f8-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="a34f8-146">Creazione di rapporti sulle versioni di compilazione: aggiungere una proprietà usando un inizializzatore di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a34f8-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="a34f8-147">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="a34f8-148">Monitorare i server back-end e le app desktop</span><span class="sxs-lookup"><span data-stu-id="a34f8-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="a34f8-149">[Modulo di Windows Server SDK hello utilizzare](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="a34f8-150">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="a34f8-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="a34f8-151">Dashboard con metriche da più app</span><span class="sxs-lookup"><span data-stu-id="a34f8-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="a34f8-152">In [Esplora metriche](app-insights-metrics-explorer.md)personalizzare il grafico e salvarlo come preferito.</span><span class="sxs-lookup"><span data-stu-id="a34f8-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="a34f8-153">Aggiungerlo toohello dashboard di Azure.</span><span class="sxs-lookup"><span data-stu-id="a34f8-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="a34f8-154">Dashboard con dati provenienti da altre fonti e Application Insights</span><span class="sxs-lookup"><span data-stu-id="a34f8-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="a34f8-155">[Esportare i dati di telemetria tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="a34f8-156">Or</span><span class="sxs-lookup"><span data-stu-id="a34f8-156">Or</span></span>

* <span data-ttu-id="a34f8-157">Usare SharePoint come dashboard, dove i dati vengono visualizzati in Web part di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a34f8-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="a34f8-158">[Utilizzare l'esportazione continua e Analitica flusso tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="a34f8-159">Utilizzare PowerView tooexamine hello database e creare una web part di SharePoint per PowerView.</span><span class="sxs-lookup"><span data-stu-id="a34f8-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="a34f8-160">Filtrare gli utenti anonimi o autenticati</span><span class="sxs-lookup"><span data-stu-id="a34f8-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="a34f8-161">Se gli utenti ad accedere, è possibile impostare hello [id utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users). Questa operazione non viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a34f8-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="a34f8-162">È quindi possibile:</span><span class="sxs-lookup"><span data-stu-id="a34f8-162">You can then:</span></span>

* <span data-ttu-id="a34f8-163">Eseguire ricerche in base a ID utente specifici</span><span class="sxs-lookup"><span data-stu-id="a34f8-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="a34f8-164">Filtrare gli utenti anonimi e autenticati tooeither metriche</span><span class="sxs-lookup"><span data-stu-id="a34f8-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="a34f8-165">Modificare i nomi della proprietà o i valori</span><span class="sxs-lookup"><span data-stu-id="a34f8-165">Modify property names or values</span></span>
<span data-ttu-id="a34f8-166">Creare un [filtro](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="a34f8-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="a34f8-167">Ciò consente di modificare o filtrare i dati di telemetria prima che venga inviato dal tooApplication app Insights.</span><span class="sxs-lookup"><span data-stu-id="a34f8-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="a34f8-168">Elencare utenti specifici e il relativo uso</span><span class="sxs-lookup"><span data-stu-id="a34f8-168">List specific users and their usage</span></span>
<span data-ttu-id="a34f8-169">Se si desidera troppo[cercare utenti specifici](#search-specific-users), è possibile impostare hello [id utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="a34f8-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="a34f8-170">Se si desidera un elenco di utenti con i dati quali, ad esempio, le pagine visualizzate o la frequenza di accesso, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="a34f8-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="a34f8-171">[Id dell'utente autenticato insieme](app-insights-api-custom-events-metrics.md#authenticated-users), [esportare database tooa](app-insights-code-sample-export-sql-stream-analytics.md) e utilizzare adatto strumenti tooanalyze sono i dati utente.</span><span class="sxs-lookup"><span data-stu-id="a34f8-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="a34f8-172">Se si dispone solo di un numero ridotto di utenti, è possibile inviare eventi personalizzati o metriche, usando i dati di hello di interesse come hello valore metrico o nome dell'evento e l'id utente hello impostazione come proprietà.</span><span class="sxs-lookup"><span data-stu-id="a34f8-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="a34f8-173">visualizzazioni di pagina tooanalyze, sostituire hello standard JavaScript trackPageView chiamata.</span><span class="sxs-lookup"><span data-stu-id="a34f8-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="a34f8-174">dati di telemetria di tooanalyze sul lato server, utilizzare una telemetria inizializzatore tooadd hello utente id tooall telemetria server.</span><span class="sxs-lookup"><span data-stu-id="a34f8-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="a34f8-175">È quindi possibile metriche di filtro e di segmento e ricerche basate sull'id utente hello.</span><span class="sxs-lookup"><span data-stu-id="a34f8-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="a34f8-176">Ridurre il traffico da my tooApplication app Insights</span><span class="sxs-lookup"><span data-stu-id="a34f8-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="a34f8-177">In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), disabilitare tutti i moduli non è necessario, tale agente di raccolta hello contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a34f8-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="a34f8-178">Utilizzare [campionamento e il filtraggio](app-insights-api-filtering-sampling.md) in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a34f8-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="a34f8-179">Nelle pagine web, limitare il numero di hello di chiamate Ajax segnalati per ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="a34f8-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="a34f8-180">Nel frammento di script hello dopo `instrumentationKey:...` , inserire: `,maxAjaxCallsPerView:3` (o un numero).</span><span class="sxs-lookup"><span data-stu-id="a34f8-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="a34f8-181">Se si utilizza [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), calcolo di aggregazione hello di batch di valori della metrica prima di inviare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="a34f8-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="a34f8-182">Un overload di TrackMetric() esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="a34f8-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="a34f8-183">Altre informazioni su [prezzi e quote](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="a34f8-184">Disabilitare telemetria</span><span class="sxs-lookup"><span data-stu-id="a34f8-184">Disable telemetry</span></span>
<span data-ttu-id="a34f8-185">troppo**dinamicamente arrestare e avviare** hello raccolta e la trasmissione di dati di telemetria da server hello:</span><span class="sxs-lookup"><span data-stu-id="a34f8-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="a34f8-186">troppo**disabilitare gli agenti di raccolta standard selezionati** : ad esempio, i contatori delle prestazioni, le richieste HTTP o dipendenze, eliminare o impostare come commento le righe rilevanti hello in [Applicationinsights](app-insights-api-custom-events-metrics.md). È possibile farlo, ad esempio, se si desidera toosend TrackRequest dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a34f8-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="a34f8-187">Visualizzare i contatori delle prestazioni di sistema</span><span class="sxs-lookup"><span data-stu-id="a34f8-187">View system performance counters</span></span>
<span data-ttu-id="a34f8-188">Tra hello metriche è possibile visualizzare in Esplora metriche sono un set di contatori delle prestazioni di sistema.</span><span class="sxs-lookup"><span data-stu-id="a34f8-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="a34f8-189">Esiste un pannello predefinito denominato **Server** in cui sono visualizzati alcuni set.</span><span class="sxs-lookup"><span data-stu-id="a34f8-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Aprire la risorsa Application Insights e fare clic su Server.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="a34f8-191">Se non vengono visualizzati dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-191">If you see no performance counter data</span></span>
* <span data-ttu-id="a34f8-192">**Server IIS** sul proprio computer o in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a34f8-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="a34f8-193">[Installare Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="a34f8-194">**Sito Web di Azure** - i contatori delle prestazioni non sono ancora supportati.</span><span class="sxs-lookup"><span data-stu-id="a34f8-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="a34f8-195">Esistono alcune metriche è possibile ottenere come una parte standard del Pannello di controllo sito web di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a34f8-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="a34f8-196">**Server Unix** - [Installare collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="a34f8-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="a34f8-197">toodisplay più contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a34f8-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="a34f8-198">Prima di tutto, [aggiungere un nuovo grafico](app-insights-metrics-explorer.md) e visualizzare se il contatore hello in hello base impostato da offrire.</span><span class="sxs-lookup"><span data-stu-id="a34f8-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="a34f8-199">In caso contrario, [aggiungere hello contatore toohello set raccolti dal modulo del contatore delle prestazioni hello](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="a34f8-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
