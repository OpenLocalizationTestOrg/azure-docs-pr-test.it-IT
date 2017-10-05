---
title: Eseguire il debug delle applicazioni con Azure Application Insights in Visual Studio | Microsoft Docs
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
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="2022f-103">Eseguire il debug delle applicazioni con Azure Application Insights in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2022f-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="2022f-104">In Visual Studio 2015 e versioni successive è possibile analizzare le prestazioni e diagnosticare i problemi nell'app Web ASP.NET sia durante il debug che nell'ambiente di produzione, usando i dati di telemetria di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2022f-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="2022f-105">Se l'app web ASP.NET è stata creata con Visual Studio 2017 o versioni successive, include già Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="2022f-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="2022f-106">In caso contrario, se non è ancora stato fatto, [aggiungere Application Insights all'app](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="2022f-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="2022f-107">Per monitorare l'app quando è in produzione, in genere si visualizzano i dati di telemetria di Application Insights nel [portale di Azure](https://portal.azure.com), che permette di impostare gli avvisi e applicare strumenti di monitoraggio efficaci.</span><span class="sxs-lookup"><span data-stu-id="2022f-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="2022f-108">Per il debug, invece, è anche possibile cercare e analizzare i dati di telemetria in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2022f-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="2022f-109">È possibile usare Visual Studio per analizzare i dati di telemetria sia dal sito di produzione che dalle esecuzioni di debug nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2022f-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="2022f-110">Nel secondo caso, è possibile analizzare le esecuzioni di debug anche se non è ancora stato configurato l'SDK per l'invio dei dati di telemetria al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2022f-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="2022f-111"><a name="run"></a> Eseguire il debug del progetto</span><span class="sxs-lookup"><span data-stu-id="2022f-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="2022f-112">Per eseguire l'app Web in modalità di debug locale, premere F5.</span><span class="sxs-lookup"><span data-stu-id="2022f-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="2022f-113">Aprire pagine diverse per generare alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2022f-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="2022f-114">In Visual Studio viene visualizzato un conteggio degli eventi registrati dal modulo di Application Insights nel progetto.</span><span class="sxs-lookup"><span data-stu-id="2022f-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![In Visual Studio il pulsante Application Insights viene visualizzato durante il debug.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="2022f-116">Fare clic su questo pulsante per cercare nei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2022f-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="2022f-117">Ricerca in Application Insights</span><span class="sxs-lookup"><span data-stu-id="2022f-117">Application Insights search</span></span>
<span data-ttu-id="2022f-118">La finestra di ricerca di Application Insights mostra gli eventi che sono stati registrati.</span><span class="sxs-lookup"><span data-stu-id="2022f-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="2022f-119">Se è stato eseguito l'accesso ad Azure durante la configurazione di Application Insights, è possibile cercare gli stessi eventi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2022f-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Fare clic con il pulsante destro del mouse sul progetto e scegliere Application Insights, Cerca.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="2022f-121">Dopo aver selezionato o deselezionato i filtri, fare clic sul pulsante di ricerca alla fine del campo di ricerca di testo.</span><span class="sxs-lookup"><span data-stu-id="2022f-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="2022f-122">La ricerca di testo libero funziona in tutti i campi degli eventi.</span><span class="sxs-lookup"><span data-stu-id="2022f-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="2022f-123">Ad esempio, è possibile cercare parte dell'URL di una pagina, il valore di una proprietà, come la città del client, o parole specifiche in un log di traccia.</span><span class="sxs-lookup"><span data-stu-id="2022f-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="2022f-124">Fare clic su qualsiasi evento per visualizzarne le proprietà dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2022f-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="2022f-125">Per le richieste all'app Web, è possibile fare clic per visualizzare il codice.</span><span class="sxs-lookup"><span data-stu-id="2022f-125">For requests to your web app, you can click through to the code.</span></span>

![In Dettagli richiesta fare clic per visualizzare il codice](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="2022f-127">È anche possibile aprire gli elementi correlati per diagnosticare le richieste non riuscite o le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="2022f-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![In Dettagli richiesta scorrere fino agli elementi correlati](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="2022f-129">Visualizzare le eccezioni e le richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="2022f-129">View exceptions and failed requests</span></span>
<span data-ttu-id="2022f-130">I report delle eccezioni vengono visualizzati nella finestra di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2022f-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="2022f-131">In alcuni tipi di applicazioni ASP.NET meno recenti è necessario [configurare il monitoraggio delle eccezioni](app-insights-asp-net-exceptions.md) per visualizzare le eccezioni gestite dal framework.</span><span class="sxs-lookup"><span data-stu-id="2022f-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="2022f-132">Fare clic su un'eccezione per ottenere un'analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="2022f-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="2022f-133">Se il codice dell'app è aperto in Visual Studio, è possibile fare clic nell'analisi dello stack per visualizzare la relativa riga del codice.</span><span class="sxs-lookup"><span data-stu-id="2022f-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="2022f-135">Visualizzare i riepiloghi delle richieste ed eccezioni nel codice</span><span class="sxs-lookup"><span data-stu-id="2022f-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="2022f-136">Nella riga CodeLens sopra ogni metodo del gestore viene visualizzato un conteggio delle richieste e delle eccezioni registrate da Application Insights nelle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="2022f-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="2022f-138">CodeLens mostra i dati di Application Insights unicamente se l'[app è configurata per l'invio dei dati di telemetria al portale di Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="2022f-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="2022f-139">Altre informazioni su Application Insights in CodeLens</span><span class="sxs-lookup"><span data-stu-id="2022f-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="2022f-140">Tendenze</span><span class="sxs-lookup"><span data-stu-id="2022f-140">Trends</span></span>
<span data-ttu-id="2022f-141">Tendenze è uno strumento che permette di visualizzare il comportamento dell'app nel tempo.</span><span class="sxs-lookup"><span data-stu-id="2022f-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="2022f-142">Scegliere **Esplora tendenze di telemetria** usando il pulsante della barra degli strumenti di Application Insights o la finestra di ricerca di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2022f-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="2022f-143">Scegliere una delle cinque query più comuni per iniziare.</span><span class="sxs-lookup"><span data-stu-id="2022f-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="2022f-144">È possibile analizzare set di dati diversi in base ai tipi di dati di telemetria, agli intervalli di tempo e ad altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="2022f-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="2022f-145">Per trovare le anomalie nei dati, scegliere una delle opzioni relative alle anomalie nell'elenco a discesa del tipo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="2022f-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="2022f-146">Le opzioni di filtro nella parte inferiore della finestra permettono di trovare facilmente subset specifici dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2022f-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Tendenze](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="2022f-148">[Altre informazioni su Tendenze](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="2022f-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="2022f-149">Monitoraggio locale</span><span class="sxs-lookup"><span data-stu-id="2022f-149">Local monitoring</span></span>
<span data-ttu-id="2022f-150">(Da Visual Studio 2015 Update 2) Se l'SDK non è stato configurato per l'invio della telemetria al portale di Application Insights (e quindi non è presente nessuna chiave di strumentazione in ApplicationInsights.config), la finestra di diagnostica visualizza la telemetria dalla sessione di debug più recente.</span><span class="sxs-lookup"><span data-stu-id="2022f-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="2022f-151">Questo è consigliabile se è già stata pubblicata una versione precedente dell'app.</span><span class="sxs-lookup"><span data-stu-id="2022f-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="2022f-152">Si vuole però evitare di combinare la telemetria delle sessioni di debug con la telemetria nel portale di Application Insights dell'app pubblicata.</span><span class="sxs-lookup"><span data-stu-id="2022f-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="2022f-153">È utile anche se si vuole eseguire il debug di alcuni [dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md) prima di inviarli al portale.</span><span class="sxs-lookup"><span data-stu-id="2022f-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="2022f-154">*Inizialmente, Application Insights è stato interamente configurato per inviare i dati di telemetria al portale. Ora però si vuole fare in modo che i dati di telemetria vengano visualizzati solo in Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="2022f-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="2022f-155">Nelle impostazioni della finestra di ricerca è disponibile un'opzione per cercare la diagnostica locale anche se l'app invia la telemetria al portale.</span><span class="sxs-lookup"><span data-stu-id="2022f-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="2022f-156">Per arrestare l'invio dei dati di telemetria al portale, impostare come commento la riga `<instrumentationkey>...` di ApplicationInsights.config. Quando si è pronti a inviare nuovamente i dati di telemetria al portale, rimuovere il commento.</span><span class="sxs-lookup"><span data-stu-id="2022f-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2022f-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2022f-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="2022f-158">**[Aggiungere altri dati](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="2022f-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="2022f-159">Monitorare l'utilizzo, la disponibilità, le dipendenze e le eccezioni,</span><span class="sxs-lookup"><span data-stu-id="2022f-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="2022f-160">integrare le tracce dei framework di registrazione</span><span class="sxs-lookup"><span data-stu-id="2022f-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="2022f-161">e scrivere telemetria personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2022f-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="2022f-163">**[Uso del portale Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="2022f-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="2022f-164">Visualizzare i dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, una mappa attiva delle dipendenze dell'applicazione e i dati di telemetria esportati.</span><span class="sxs-lookup"><span data-stu-id="2022f-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

