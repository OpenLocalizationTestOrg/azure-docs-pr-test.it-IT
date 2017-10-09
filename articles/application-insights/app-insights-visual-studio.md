---
title: le applicazioni con Azure Application Insights in Visual Studio aaaDebug | Documenti Microsoft
description: Diagnostica e analisi delle prestazioni delle app Web durante il debug e nell'ambiente di produzione.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="6f5f3-103">Eseguire il debug delle applicazioni con Azure Application Insights in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f5f3-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="6f5f3-104">In Visual Studio 2015 e versioni successive è possibile analizzare le prestazioni e diagnosticare i problemi nell'app Web ASP.NET sia durante il debug che nell'ambiente di produzione, usando i dati di telemetria di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f5f3-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="6f5f3-105">Se è stato creato l'app web ASP.NET utilizzando Visual Studio 2017 o versioni successive, ha già hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="6f5f3-106">In caso contrario, se non è già fatto, [aggiungere Application Insights tooyour app](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6f5f3-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="6f5f3-107">toomonitor l'app quando è in produzione, è in genere visualizzare telemetria di Application Insights hello in hello [portale di Azure](https://portal.azure.com), in cui è possibile impostare gli avvisi e applicare i potenti strumenti di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="6f5f3-108">Ma per il debug, è inoltre possibile cercare e analizzare dati di telemetria hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="6f5f3-109">È possibile utilizzare i dati di telemetria di Visual Studio tooanalyze dal sito di produzione e di debug viene eseguito nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="6f5f3-110">In quest'ultimo caso hello, è possibile analizzare il debug viene eseguito anche se è ancora stata configurata hello SDK toosend telemetria toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="6f5f3-111"><a name="run"></a> Eseguire il debug del progetto</span><span class="sxs-lookup"><span data-stu-id="6f5f3-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="6f5f3-112">Per eseguire l'app Web in modalità di debug locale, premere F5.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="6f5f3-113">Aprire pagine diverse toogenerate alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="6f5f3-114">In Visual Studio, viene visualizzato un conteggio di eventi di hello che sono stati registrati dal modulo di Application Insights hello nel progetto.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![In Visual Studio, hello Application Insights è raffigurata durante il debug.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="6f5f3-116">Fare clic su questo pulsante toosearch dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="6f5f3-117">Ricerca in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6f5f3-117">Application Insights search</span></span>
<span data-ttu-id="6f5f3-118">finestra di ricerca di Application Insights Hello Mostra gli eventi che sono stati registrati.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="6f5f3-119">(Se non hai effettuato tooAzure quando si configura Application Insights, è possibile cercare hello stessi eventi nel portale di Azure hello.)</span><span class="sxs-lookup"><span data-stu-id="6f5f3-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Fare clic sul progetto hello e scegliere di Application Insights, ricerca](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="6f5f3-121">Dopo aver selezionare o deselezionare i filtri, fare clic su pulsante di ricerca hello alla fine di hello del campo di ricerca di testo hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="6f5f3-122">ricerca di testo libero Hello funziona su tutti i campi negli eventi hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="6f5f3-123">Ad esempio, cercare parte di hello URL di una pagina. il valore di hello di una proprietà, ad esempio città client; o o parole specifiche in un log di traccia.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="6f5f3-124">Fare clic su qualsiasi toosee evento le proprietà dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="6f5f3-125">Per le richieste tooyour web app, è possibile fare clic su tramite codice toohello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-125">For requests tooyour web app, you can click through toohello code.</span></span>

![In Dettagli richiesta, fare clic su tramite codice toohello](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="6f5f3-127">È inoltre possibile aprire elementi correlati toohelp diagnosticare le richieste non riuscite o le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![In Dettagli richiesta, scorrere verso il basso toorelated elementi](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="6f5f3-129">Visualizzare le eccezioni e le richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="6f5f3-129">View exceptions and failed requests</span></span>
<span data-ttu-id="6f5f3-130">Mostra i report di eccezione nella finestra di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="6f5f3-131">(In alcuni tipi precedenti dell'applicazione ASP.NET, è necessario troppo[impostare il monitoraggio di eccezione](app-insights-asp-net-exceptions.md) toosee eccezioni gestite da framework hello.)</span><span class="sxs-lookup"><span data-stu-id="6f5f3-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="6f5f3-132">Fare clic su un tooget eccezione una traccia dello stack.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="6f5f3-133">Se il codice hello dell'applicazione hello è aperto in Visual Studio, è possibile fare clic hello stack traccia toohello rilevanti riga di codice hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="6f5f3-135">Visualizzare i riepiloghi di richiesta e l'eccezione nel codice hello</span><span class="sxs-lookup"><span data-stu-id="6f5f3-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="6f5f3-136">In hello riga Codelens sopra ogni metodo del gestore, viene visualizzato un conteggio di hello richieste e le eccezioni registrate da Application Insights in hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="6f5f3-138">Codelens Mostra i dati di Application Insights solo se è necessario [configurato il portale di Application Insights app toosend telemetria toohello](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6f5f3-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="6f5f3-139">Altre informazioni su Application Insights in CodeLens</span><span class="sxs-lookup"><span data-stu-id="6f5f3-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="6f5f3-140">Tendenze</span><span class="sxs-lookup"><span data-stu-id="6f5f3-140">Trends</span></span>
<span data-ttu-id="6f5f3-141">Tendenze è uno strumento che permette di visualizzare il comportamento dell'app nel tempo.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="6f5f3-142">Scegliere **esplorare le tendenze di telemetria** dal pulsante della barra degli strumenti di Application Insights hello o nella finestra di ricerca di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="6f5f3-143">Scegliere uno dei cinque tooget query comuni avviato.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="6f5f3-144">È possibile analizzare set di dati diversi in base ai tipi di dati di telemetria, agli intervalli di tempo e ad altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="6f5f3-145">toofind anomalie nei dati, scegliere una delle opzioni di anomalie hello in elenco a discesa "Tipo di visualizzazione" hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="6f5f3-146">opzioni di filtro nella parte inferiore di hello della finestra hello Hello rendono semplice toohone in base a subset specifici dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Tendenze](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="6f5f3-148">[Altre informazioni su Tendenze](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="6f5f3-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="6f5f3-149">Monitoraggio locale</span><span class="sxs-lookup"><span data-stu-id="6f5f3-149">Local monitoring</span></span>
<span data-ttu-id="6f5f3-150">(Da Visual Studio 2015 Update 2) Se non è configurato il portale di Application Insights toohello hello SDK toosend telemetria (in modo che non è presente alcuna chiave di strumentazione in Applicationinsights) finestra diagnostica hello Visualizza dati di telemetria da una sessione di debug più recenti.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="6f5f3-151">Questo è consigliabile se è già stata pubblicata una versione precedente dell'app.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="6f5f3-152">Per evitare che il debug di sessioni toobe dati telemetria hello confuse con dati di telemetria relativi hello hello portale Application Insights da app pubblicata hello.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="6f5f3-153">È inoltre utile se si dispone di un [telemetria personalizzata](app-insights-api-custom-events-metrics.md) che si desidera toodebug prima dell'invio portale toohello telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="6f5f3-154">*Inizialmente configurato completamente portale toohello telemetria di Application Insights toosend. Ma ora telemetria hello toosee solo in Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="6f5f3-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="6f5f3-155">Nelle impostazioni della finestra di ricerca hello, è una diagnostica locale toosearch di opzione, anche se l'app invia portale toohello telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="6f5f3-156">dati di telemetria toostop inviati toohello portal, impostare come commento la riga hello `<instrumentationkey>...` da Applicationinsights. Quando si passa nuovamente portale toohello di telemetria toosend pronto, rimuovere i commenti.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f5f3-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f5f3-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="6f5f3-158">**[Aggiungere altri dati](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="6f5f3-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="6f5f3-159">Monitorare l'utilizzo, la disponibilità, le dipendenze e le eccezioni,</span><span class="sxs-lookup"><span data-stu-id="6f5f3-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="6f5f3-160">integrare le tracce dei framework di registrazione</span><span class="sxs-lookup"><span data-stu-id="6f5f3-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="6f5f3-161">e scrivere telemetria personalizzata.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="6f5f3-163">**[Utilizzo di portale Application Insights hello](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="6f5f3-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="6f5f3-164">Visualizzare i dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, una mappa attiva delle dipendenze dell'applicazione e i dati di telemetria esportati.</span><span class="sxs-lookup"><span data-stu-id="6f5f3-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

