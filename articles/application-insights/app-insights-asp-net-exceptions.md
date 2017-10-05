---
title: Errori ed eccezioni di diagnosi nelle app Web con Azure Application Insights | Microsoft Docs
description: Acquisire le eccezioni da app ASP.NET insieme ai dati di telemetria della richiesta.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="2ddfa-103">Diagnosticare eccezioni nelle app Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="2ddfa-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="2ddfa-104">Le eccezioni nell'applicazione Web attiva vengono segnalate da [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2ddfa-105">È possibile correlare le richieste non riuscite con le eccezioni e altri eventi nel client e nel server, in modo da poter diagnosticare rapidamente le cause.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="2ddfa-106">Configurare la creazione di report sulle eccezioni</span><span class="sxs-lookup"><span data-stu-id="2ddfa-106">Set up exception reporting</span></span>
* <span data-ttu-id="2ddfa-107">Per segnalare le eccezioni dall'app del server:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="2ddfa-108">Installare [Application Insights SDK](app-insights-asp-net.md) nel codice dell'app, oppure</span><span class="sxs-lookup"><span data-stu-id="2ddfa-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="2ddfa-109">Server Web IIS: eseguire l'[Agente di Application Insights](app-insights-monitor-performance-live-website-now.md); o</span><span class="sxs-lookup"><span data-stu-id="2ddfa-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="2ddfa-110">App Web di Azure: aggiungere l'[estensione di Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="2ddfa-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="2ddfa-111">App Web Java: installare l'[agente Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="2ddfa-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="2ddfa-112">Installare il [frammento di JavaScript](app-insights-javascript.md) nelle pagine Web per intercettare le eccezioni del browser.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="2ddfa-113">In certi framework applicazione o con alcune impostazioni è necessario eseguire alcuni passaggi aggiuntivi per intercettare più eccezioni:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="2ddfa-114">Web Form</span><span class="sxs-lookup"><span data-stu-id="2ddfa-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="2ddfa-115">MVC</span><span class="sxs-lookup"><span data-stu-id="2ddfa-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="2ddfa-116">API Web 1.*</span><span class="sxs-lookup"><span data-stu-id="2ddfa-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="2ddfa-117">API Web 2.*</span><span class="sxs-lookup"><span data-stu-id="2ddfa-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="2ddfa-118">WCF</span><span class="sxs-lookup"><span data-stu-id="2ddfa-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="2ddfa-119">Diagnosticare le eccezioni con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="2ddfa-120">Aprire la soluzione dell'app in Visual Studio per facilitare il debug.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="2ddfa-121">Eseguire l'app nel server o nel computer di sviluppo usando F5.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="2ddfa-122">Aprire la finestra di ricerca di Application Insights in Visual Studio e impostare la visualizzazione degli eventi dall'app.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="2ddfa-123">A questo scopo, durante il debug è sufficiente fare clic sul pulsante Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Fare clic con il pulsante destro del mouse sul progetto e scegliere Application Insights, Apri.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="2ddfa-125">Si noti che è possibile filtrare il report per visualizzare solo le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="2ddfa-126">*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="2ddfa-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="2ddfa-127">Fare clic su un report di eccezione per visualizzarne l'analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="2ddfa-128">Fare clic su un riferimento di riga nell'analisi dello stack per aprire il relativo file.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="2ddfa-129">Nel codice, si noti che CodeLens mostra i dati relativi alle eccezioni:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Notifica CodeLens di eccezioni.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="2ddfa-131">Diagnosi degli errori con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2ddfa-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="2ddfa-132">Il riquadro Errori nel pannello di panoramica dell'app in Application Insights mostra i grafici delle eccezioni e delle richieste HTTP non riuscite, insieme a un elenco di URL delle richieste che causano gli errori più frequenti.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Selezionare Impostazioni, Errori.](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="2ddfa-134">Fare clic su uno dei tipi di eccezione con errori nell'elenco per visualizzare le singole occorrenze dell'eccezione, in cui è possibile visualizzare i dettagli e l'analisi dello stack:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Selezionare un'istanza di una richiesta non riuscita e nei dettagli dell'eccezione visualizzare le istanze dell'eccezione.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="2ddfa-136">**In alternativa,** è possibile iniziare dall'elenco di richieste e individuare le eccezioni correlate.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="2ddfa-137">*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="2ddfa-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="2ddfa-138">Dati di traccia e di log personalizzati</span><span class="sxs-lookup"><span data-stu-id="2ddfa-138">Custom tracing and log data</span></span>
<span data-ttu-id="2ddfa-139">Per ottenere dati di diagnostica specifici per l'app, è possibile inserire codice per l'invio di dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="2ddfa-140">Questi dati vengono visualizzati nella ricerca diagnostica insieme alla richiesta, alla visualizzazione di pagina e ad altri dati raccolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="2ddfa-141">Sono disponibili diverse opzioni:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-141">You have several options:</span></span>

* <span data-ttu-id="2ddfa-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) viene usato in genere per il monitoraggio dei modelli di utilizzo, ma i dati inviati vengono visualizzati anche in Eventi personalizzati nella ricerca diagnostica.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="2ddfa-143">Gli eventi sono denominati e possono includere proprietà di stringa e metriche numeriche, in base alle quali è possibile [filtrare le ricerche diagnostiche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="2ddfa-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permette di inviare dati più lunghi, ad esempio informazioni POST.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="2ddfa-145">[TrackException()](#exceptions) invia analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="2ddfa-146">[Altre informazioni sulle eccezioni](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="2ddfa-147">Se si usa già un framework di registrazione come Log4Net o NLog, è possibile [acquisire tali log](app-insights-asp-net-trace-logs.md) e visualizzarli nella ricerca diagnostica insieme ai dati relativi alle richieste e alle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="2ddfa-148">Per visualizzare questi eventi, aprire [Cerca](app-insights-diagnostic-search.md), quindi Filtro e infine scegliere Evento personalizzato, Traccia o Eccezione.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="2ddfa-150">Se l’app genera molti dati di telemetria, il modulo di campionamento adattivo riduce automaticamente il volume che viene inviato al portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="2ddfa-151">Gli eventi che fanno parte della stessa operazione verranno selezionati o deselezionati come gruppo, per rendere possibile lo spostamento tra eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="2ddfa-152">Informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="2ddfa-153">Come visualizzare i dati POST di una richiesta</span><span class="sxs-lookup"><span data-stu-id="2ddfa-153">How to see request POST data</span></span>
<span data-ttu-id="2ddfa-154">I dettagli della richiesta non includono i dati inviati all'app in una chiamata POST.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="2ddfa-155">Per poter ottenere questi dati:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-155">To have this data reported:</span></span>

* <span data-ttu-id="2ddfa-156">[Installare l'SDK](app-insights-asp-net.md) nel progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="2ddfa-157">Inserire il codice nell'applicazione per chiamare [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="2ddfa-158">Inviare i dati POST nel parametro del messaggio.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="2ddfa-159">Esiste un limite per le dimensioni consentite, quindi è consigliabile provare a inviare solo i dati essenziali.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="2ddfa-160">Quando si esamina una richiesta non riuscita, trovare le tracce associate.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-160">When you investigate a failed request, find the associated traces.</span></span>  

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="2ddfa-162"><a name="exceptions"></a> Acquisizione delle eccezioni e dei relativi dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="2ddfa-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="2ddfa-163">Inizialmente, nel portale non verranno visualizzate tutte le eccezioni che causano errori nell'app.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="2ddfa-164">Verranno visualizzate tutte le eccezioni del browser (se si usa [JavaScript SDK](app-insights-javascript.md) nelle pagine Web).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="2ddfa-165">La maggior parte delle eccezioni del server viene rilevata da IIS, ma è necessario scrivere qualche riga di codice per visualizzarle.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="2ddfa-166">È possibile:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-166">You can:</span></span>

* <span data-ttu-id="2ddfa-167">**Registrare le eccezioni in modo esplicito** inserendo il codice nei gestori di eccezioni per segnalare le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="2ddfa-168">**Acquisire automaticamente le eccezioni** configurando il framework di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="2ddfa-169">Gli elementi da aggiungere variano a seconda dei diversi tipi di framework.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="2ddfa-170">Segnalazione di eccezioni in modo esplicito</span><span class="sxs-lookup"><span data-stu-id="2ddfa-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="2ddfa-171">Il modo più semplice consiste nell'inserire una chiamata a TrackException() in un gestore di eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="2ddfa-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2ddfa-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="2ddfa-173">C#</span><span class="sxs-lookup"><span data-stu-id="2ddfa-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="2ddfa-174">VB</span><span class="sxs-lookup"><span data-stu-id="2ddfa-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="2ddfa-175">I parametri delle proprietà e delle misurazioni sono facoltativi, ma sono utili per [filtrare e aggiungere](app-insights-diagnostic-search.md) altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="2ddfa-176">Ad esempio, per un'app in grado di eseguire diversi giochi, è possibile trovare tutti i report di eccezione correlati a un gioco specifico.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="2ddfa-177">È possibile aggiungere qualsiasi numero di elementi a ogni dizionario.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="2ddfa-178">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="2ddfa-178">Browser exceptions</span></span>
<span data-ttu-id="2ddfa-179">Viene segnalata la maggior parte delle eccezioni del browser.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="2ddfa-180">Se la pagina Web include file di script provenienti da reti per la distribuzione di contenuti o da altri domini, verificare che il tag dello script contenga l'attributo ```crossorigin="anonymous"```e che il server invii [intestazioni CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="2ddfa-181">Ciò consentirà di ottenere un'analisi dello stack e i dettagli per le eccezioni JavaScript non gestite da queste risorse.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="2ddfa-182">Web Form</span><span class="sxs-lookup"><span data-stu-id="2ddfa-182">Web forms</span></span>
<span data-ttu-id="2ddfa-183">Per Web Form, il modulo HTTP potrà raccogliere le eccezioni quando non sono configurati reindirizzamenti con CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="2ddfa-184">Se però sono presenti reindirizzamenti attivi, aggiungere le righe seguenti alla funzione Application_Error in Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="2ddfa-185">Aggiungere un file Global.asax se non ne esiste già uno.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="2ddfa-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="2ddfa-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="2ddfa-187">MVC</span><span class="sxs-lookup"><span data-stu-id="2ddfa-187">MVC</span></span>
<span data-ttu-id="2ddfa-188">Se la configurazione di [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) è `Off`, le eccezioni potranno essere raccolte dal [modulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ddfa-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="2ddfa-189">Se tuttavia è `RemoteOnly` (impostazione predefinita) o `On`, l'eccezione verrà cancellata e non potrà essere raccolta automaticamente da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="2ddfa-190">È possibile risolvere questo problema eseguendo l'override della [classe System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) e applicando la classe di cui è stato eseguito l'override, come illustrato per le diverse versioni MVC riportate di seguito ([origine github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="2ddfa-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="2ddfa-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="2ddfa-191">MVC 2</span></span>
<span data-ttu-id="2ddfa-192">Sostituire l'attributo HandleError con il nuovo attributo nei controller.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="2ddfa-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="2ddfa-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="2ddfa-194">MVC 3</span></span>
<span data-ttu-id="2ddfa-195">Registrare `AiHandleErrorAttribute` come filtro globale in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="2ddfa-196">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="2ddfa-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="2ddfa-197">MVC 4, MVC5</span></span>
<span data-ttu-id="2ddfa-198">Registrare AiHandleErrorAttribute come filtro globale in FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="2ddfa-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="2ddfa-200">API Web 1.x</span><span class="sxs-lookup"><span data-stu-id="2ddfa-200">Web API 1.x</span></span>
<span data-ttu-id="2ddfa-201">Eseguire l'override di System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="2ddfa-202">Sarà possibile aggiungere questo attributo di cui è stato eseguito l'override ai controller specifici o alla configurazione del filtro globale nella classe WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="2ddfa-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="2ddfa-204">Alcuni casi non possono essere gestiti dai filtri eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="2ddfa-205">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-205">For example:</span></span>

* <span data-ttu-id="2ddfa-206">Eccezioni generate dai costruttori dei controller.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="2ddfa-207">Eccezioni generate dai gestori di messaggi.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="2ddfa-208">Eccezioni generate durante il routing.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="2ddfa-209">Eccezioni generate durante la serializzazione del contenuto della risposta.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="2ddfa-210">API Web 2.x</span><span class="sxs-lookup"><span data-stu-id="2ddfa-210">Web API 2.x</span></span>
<span data-ttu-id="2ddfa-211">Aggiungere un'implementazione di IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="2ddfa-212">Aggiungere il codice seguente ai servizi in WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-212">Add this to the services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="2ddfa-213">}</span><span class="sxs-lookup"><span data-stu-id="2ddfa-213">}</span></span>

[<span data-ttu-id="2ddfa-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="2ddfa-215">In alternativa, è possibile:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="2ddfa-216">Sostituire ExceptionHandler con un'implementazione personalizzata di IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="2ddfa-217">Questo elemento viene chiamato solo quando il framework può ancora scegliere il messaggio di risposta da inviare, non quando la connessione viene interrotta.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="2ddfa-218">Come descritto nella sezione relativa ai controller Web API 1.x precedente, i filtri eccezioni non vengono chiamati in tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="2ddfa-219">WCF</span><span class="sxs-lookup"><span data-stu-id="2ddfa-219">WCF</span></span>
<span data-ttu-id="2ddfa-220">Aggiungere una classe che estenda Attribute e implementi IErrorHandler e IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="2ddfa-221">Aggiungere l'attributo alle implementazioni del servizio:</span><span class="sxs-lookup"><span data-stu-id="2ddfa-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="2ddfa-222">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ddfa-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="2ddfa-223">Contatori delle prestazioni delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="2ddfa-223">Exception performance counters</span></span>
<span data-ttu-id="2ddfa-224">L'installazione [dell'Agente di Application Insights](app-insights-monitor-performance-live-website-now.md) nel server permette di ottenere un grafico della frequenza delle eccezioni, misurata da .NET.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="2ddfa-225">Il grafico include le eccezioni .NET gestite e non gestite.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="2ddfa-226">Aprire un pannello Esplora metrica, aggiungere un nuovo grafico e selezionare **Frequenza eccezione**, elencata sotto a Contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="2ddfa-227">.NET framework calcola la frequenza contando il numero delle eccezioni in un intervallo e dividendolo per la lunghezza dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="2ddfa-228">Si noti che questo conteggio è diverso dal conteggio delle "Eccezioni" calcolato dal portale di Application Insights che conteggia i report TrackException.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="2ddfa-229">Gli intervalli di campionamento sono diversi e il SDK non invia report di TrackException per tutte le eccezioni gestite e non gestite.</span><span class="sxs-lookup"><span data-stu-id="2ddfa-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="2ddfa-230">Video</span><span class="sxs-lookup"><span data-stu-id="2ddfa-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="2ddfa-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ddfa-231">Next steps</span></span>
* [<span data-ttu-id="2ddfa-232">Monitorare REST, SQL e altre chiamate alle dipendenze</span><span class="sxs-lookup"><span data-stu-id="2ddfa-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="2ddfa-233">Monitorare i tempi di caricamento delle pagina, le eccezioni del browser e le chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="2ddfa-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="2ddfa-234">Monitorare i contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="2ddfa-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
