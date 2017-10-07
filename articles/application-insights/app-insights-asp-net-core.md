---
title: Application Insights per ASP.NET Core aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="926d8-103">Application Insights per ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="926d8-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="926d8-104">[Application Insights](app-insights-overview.md) consente di monitorare la disponibilità, le prestazioni e l'uso dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="926d8-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="926d8-105">Con il feedback hello che è ottenere sulle prestazioni di hello e l'efficacia dell'app in hello wild, è possibile prendere decisioni informate sulla direzione hello della progettazione hello in ogni ciclo di vita di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="926d8-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Esempio](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="926d8-107">È necessaria una sottoscrizione con [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="926d8-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="926d8-108">È possibile accedere con un account Microsoft, che in genere si ottiene per Windows, XBox Live o altri servizi cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="926d8-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="926d8-109">Il team potrebbe avere un tooAzure sottoscrizione aziendale: chiedere hello proprietario tooadd tooit con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="926d8-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="926d8-110">introduttiva</span><span class="sxs-lookup"><span data-stu-id="926d8-110">Getting started</span></span>

* <span data-ttu-id="926d8-111">In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sul progetto e selezionare **Configura Application Insights** oppure **Aggiungi > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="926d8-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="926d8-112">[Altre informazioni](app-insights-asp-net.md)</span><span class="sxs-lookup"><span data-stu-id="926d8-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="926d8-113">Se i comandi di menu non viene visualizzata, seguire hello [manuale Guida introduttiva recupero](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="926d8-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="926d8-114">Potrebbe essere necessario toodo questo se il progetto è stato creato con una versione di Visual Studio prima 2017.</span><span class="sxs-lookup"><span data-stu-id="926d8-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="926d8-115">Utilizzo di Application Insights</span><span class="sxs-lookup"><span data-stu-id="926d8-115">Using Application Insights</span></span>
<span data-ttu-id="926d8-116">Sign in hello [portale Microsoft Azure](https://portal.azure.com)selezionare **tutte le risorse** o **Application Insights**, quindi selezionare risorsa hello creato toomonitor l'app.</span><span class="sxs-lookup"><span data-stu-id="926d8-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="926d8-117">In una finestra separata dal browser, usare l'app per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="926d8-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="926d8-118">Si noterà che i dati visualizzati nei grafici di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="926d8-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="926d8-119">(Potrebbe essere tooclick aggiornamento). Ci sarà solo una piccola quantità di dati al momento dello sviluppo, ma questi grafici si attiveranno davvero quando si pubblicherà l'app e si avranno numerosi utenti.</span><span class="sxs-lookup"><span data-stu-id="926d8-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="926d8-120">pagina di panoramica Hello vengono visualizzati grafici di prestazioni chiave: tempo di risposta server, il tempo di caricamento pagina e il numero di richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="926d8-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="926d8-121">Fare clic su qualsiasi toosee grafico più grafici e dati.</span><span class="sxs-lookup"><span data-stu-id="926d8-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="926d8-122">Visualizzazioni nel portale di hello rientrano in tre categorie principali:</span><span class="sxs-lookup"><span data-stu-id="926d8-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="926d8-123">[Esplora metriche](app-insights-metrics-explorer.md) Mostra grafici e tabelle di metrica e i conteggi, ad esempio tempi di risposta, percentuale degli errori o metriche personalizzate con hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="926d8-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="926d8-124">Filtro e segmento dati hello da tooget di valori di proprietà una comprensione migliore dell'app e i relativi utenti.</span><span class="sxs-lookup"><span data-stu-id="926d8-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="926d8-125">[Ricerca di Esplora](app-insights-diagnostic-search.md) Elenca gli eventi singoli, ad esempio richieste specifiche, eccezioni, le tracce di log o eventi creato personalmente con hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="926d8-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="926d8-126">Filtrare e cercare gli eventi di hello e spostarsi tra i problemi di tooinvestigate eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="926d8-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="926d8-127">[Analisi](app-insights-analytics.md) consente di eseguire query simili a SQL sui dati di telemetria ed è un potente strumento di analisi e diagnostica.</span><span class="sxs-lookup"><span data-stu-id="926d8-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="926d8-128">Avvisi</span><span class="sxs-lookup"><span data-stu-id="926d8-128">Alerts</span></span>
* <span data-ttu-id="926d8-129">Si ottengono automaticamente [avvisi di diagnostica proattivi](app-insights-proactive-diagnostics.md) che informano su modifiche anomale alle frequenze di errori o ad altre metriche.</span><span class="sxs-lookup"><span data-stu-id="926d8-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="926d8-130">Impostare [disponibilità test](app-insights-monitor-web-app-availability.md) tootest un sito Web continuamente da parte del mondo e si invia tramite posta elettronica non appena un test ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="926d8-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="926d8-131">Impostare [metrici avvisi](app-insights-monitor-web-app-availability.md) tooknow se metriche, ad esempio tempi di risposta o tariffe eccezione compresa nei limiti accettabili.</span><span class="sxs-lookup"><span data-stu-id="926d8-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="926d8-132">Video</span><span class="sxs-lookup"><span data-stu-id="926d8-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="926d8-133">Aprire origine</span><span class="sxs-lookup"><span data-stu-id="926d8-133">Open source</span></span>
[<span data-ttu-id="926d8-134">Leggere e fornire codice toohello</span><span class="sxs-lookup"><span data-stu-id="926d8-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="926d8-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="926d8-135">Next steps</span></span>
* <span data-ttu-id="926d8-136">[Aggiungere le pagine web di telemetria tooyour](app-insights-javascript.md) toomonitor pagina informazioni sull'utilizzo e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="926d8-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="926d8-137">[Monitoraggio dipendenze](app-insights-asp-net-dependencies.md) toosee se REST, SQL o altre risorse esterne rallentano è.</span><span class="sxs-lookup"><span data-stu-id="926d8-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="926d8-138">[Utilizzare l'API di hello](app-insights-api-custom-events-metrics.md) toosend di eventi e le metriche per una visualizzazione più dettagliata dell'utilizzo e delle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="926d8-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="926d8-139">[Test disponibilità](app-insights-monitor-web-app-availability.md) controllare app costantemente dal mondo hello.</span><span class="sxs-lookup"><span data-stu-id="926d8-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

