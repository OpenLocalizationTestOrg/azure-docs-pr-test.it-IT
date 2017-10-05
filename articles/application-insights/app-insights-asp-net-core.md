---
title: Azure Application Insights per ASP.NET Core | Microsoft Docs
description: "Monitorare la disponibilità, le prestazioni e l'utilizzo delle applicazioni Web."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="70a25-103">Application Insights per ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="70a25-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="70a25-104">[Application Insights](app-insights-overview.md) consente di monitorare la disponibilità, le prestazioni e l'uso dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="70a25-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="70a25-105">Con il feedback ottenuto sulle prestazioni e sull'efficacia dell'app in circostanze normali, è possibile prendere decisioni informate sulla direzione della progettazione in ogni ciclo di vita di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="70a25-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Esempio](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="70a25-107">È necessaria una sottoscrizione con [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="70a25-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="70a25-108">È possibile accedere con un account Microsoft, che in genere si ottiene per Windows, XBox Live o altri servizi cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70a25-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="70a25-109">Se il team ha una sottoscrizione di Azure per l'organizzazione, chiedere al proprietario di aggiungere l'utente alla sottoscrizione usando il rispettivo account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70a25-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="70a25-110">Introduzione</span><span class="sxs-lookup"><span data-stu-id="70a25-110">Getting started</span></span>

* <span data-ttu-id="70a25-111">In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sul progetto e selezionare **Configura Application Insights** oppure **Aggiungi > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="70a25-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="70a25-112">[Altre informazioni](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="70a25-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="70a25-113">Se questi comandi non sono disponibili, seguire la [guida introduttiva manuale](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="70a25-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="70a25-114">Questa operazione potrebbe essere necessaria se il progetto è stato creato con una versione di Visual Studio precedente alla versione 2017.</span><span class="sxs-lookup"><span data-stu-id="70a25-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="70a25-115">Utilizzo di Application Insights</span><span class="sxs-lookup"><span data-stu-id="70a25-115">Using Application Insights</span></span>
<span data-ttu-id="70a25-116">Accedere al [portale di Microsoft Azure](https://portal.azure.com), selezionare **Tutte le risorse** o **Application Insights** e quindi selezionare la risorsa creata per monitorare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70a25-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="70a25-117">In una finestra separata dal browser, usare l'app per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="70a25-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="70a25-118">Verranno visualizzati dati nei grafici di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70a25-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="70a25-119">(Potrebbe essere necessario fare clic su Aggiorna.) Ci sarà solo una piccola quantità di dati al momento dello sviluppo, ma questi grafici si attiveranno davvero quando si pubblicherà l'app e si avranno numerosi utenti.</span><span class="sxs-lookup"><span data-stu-id="70a25-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="70a25-120">La pagina di panoramica mostra i grafici delle prestazioni più importanti: tempo di risposta del server, tempo di caricamento della pagina e conteggi delle richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="70a25-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="70a25-121">Fare clic su qualsiasi grafico per visualizzare altri grafici e dati.</span><span class="sxs-lookup"><span data-stu-id="70a25-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="70a25-122">Le visualizzazioni nel portale rientrano in tre categorie principali:</span><span class="sxs-lookup"><span data-stu-id="70a25-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="70a25-123">[Esplora metriche](app-insights-metrics-explorer.md) mostra grafici e tabelle di metriche e conteggi, come tempi di risposta, frequenze di errori o metriche create dall'utente con l'[API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="70a25-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="70a25-124">Filtrare e segmentare i dati dai valori della proprietà per ottenere una migliore comprensione dell'app e dei relativi utenti.</span><span class="sxs-lookup"><span data-stu-id="70a25-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="70a25-125">[Esplora ricerche](app-insights-diagnostic-search.md) elenca i singoli eventi, come richieste specifiche, eccezioni, tracce di log o eventi creati dall'utente con l'[API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="70a25-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="70a25-126">Filtrare e cercare negli eventi, e spostarsi tra gli eventi correlati per analizzare i problemi.</span><span class="sxs-lookup"><span data-stu-id="70a25-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="70a25-127">[Analisi](app-insights-analytics.md) consente di eseguire query simili a SQL sui dati di telemetria ed è un potente strumento di analisi e diagnostica.</span><span class="sxs-lookup"><span data-stu-id="70a25-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="70a25-128">Avvisi</span><span class="sxs-lookup"><span data-stu-id="70a25-128">Alerts</span></span>
* <span data-ttu-id="70a25-129">Si ottengono automaticamente [avvisi di diagnostica proattivi](app-insights-proactive-diagnostics.md) che informano su modifiche anomale alle frequenze di errori o ad altre metriche.</span><span class="sxs-lookup"><span data-stu-id="70a25-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="70a25-130">Impostare i [test di disponibilità](app-insights-monitor-web-app-availability.md) per testare il sito Web continuamente da varie parti del mondo e ottenere messaggi di posta elettronica non appena un test ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="70a25-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="70a25-131">Impostare [avvisi di metrica](app-insights-monitor-web-app-availability.md) per sapere se delle metriche quali tempi di risposta o frequenza di eccezioni superano i limiti accettabili.</span><span class="sxs-lookup"><span data-stu-id="70a25-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="70a25-132">Video</span><span class="sxs-lookup"><span data-stu-id="70a25-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="70a25-133">Aprire origine</span><span class="sxs-lookup"><span data-stu-id="70a25-133">Open source</span></span>
[<span data-ttu-id="70a25-134">Leggere e contribuire al codice</span><span class="sxs-lookup"><span data-stu-id="70a25-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="70a25-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70a25-135">Next steps</span></span>
* <span data-ttu-id="70a25-136">[Aggiungere i dati di telemetria alle pagine Web](app-insights-javascript.md) per monitorare l'uso e le prestazioni delle pagine.</span><span class="sxs-lookup"><span data-stu-id="70a25-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="70a25-137">[Monitoraggio delle dipendenze](app-insights-asp-net-dependencies.md) per vedere se REST, SQL o altre risorse esterne rallentano l’utente.</span><span class="sxs-lookup"><span data-stu-id="70a25-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="70a25-138">[Utilizzare l'API](app-insights-api-custom-events-metrics.md) per inviare gli eventi e le metriche per una visualizzazione più dettagliata dell'utilizzo e delle prestazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="70a25-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="70a25-139">[Test di disponibilità](app-insights-monitor-web-app-availability.md) controlla costantemente l’app da tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="70a25-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

