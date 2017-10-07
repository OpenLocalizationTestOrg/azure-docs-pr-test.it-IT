---
title: utilizzo di aaaMonitoring e le prestazioni per le app desktop di Windows
description: Analizzare l'utilizzo e le prestazioni dell'applicazione desktop di Windows con HockeyApp e Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="a2fe4-103">Monitoraggio dell'utilizzo e delle prestazioni nelle applicazioni desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="a2fe4-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="a2fe4-104">[Application Insights di Azure](app-insights-overview.md) e [HockeyApp](https://hockeyapp.net) consentono di monitorare l'utilizzo e le prestazioni dell'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2fe4-105">È consigliabile [HockeyApp](https://hockeyapp.net) toodistribute e monitorare le app desktop e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="a2fe4-106">Con HockeyApp è possibile gestire la distribuzione, i test live e i commenti degli utenti, oltre a monitorare i report di utilizzo e di arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="a2fe4-107">È anche possibile [esportare ed eseguire una query sui dati di telemetria con Analisi](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="a2fe4-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="a2fe4-108">Anche se i dati di telemetria possono essere inviati tooApplication Insights da un'applicazione desktop, si tratta principalmente utile ai fini di debug e sperimentale.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="a2fe4-109">toosend telemetria tooApplication Insights da un'applicazione Windows</span><span class="sxs-lookup"><span data-stu-id="a2fe4-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="a2fe4-110">In hello [portale di Azure](https://portal.azure.com), [creare una risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a2fe4-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="a2fe4-111">Scegliere l'app ASP.NET per il tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="a2fe4-112">Eseguire una copia della chiave di strumentazione hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="a2fe4-113">Trovare la chiave di hello in hello Essentials elenco a discesa della nuova risorsa hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="a2fe4-114">In Visual Studio, modificare i pacchetti NuGet hello del progetto dell'app e aggiungere Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="a2fe4-115">In alternativa, scegliere Microsoft. applicationinsights, se si desidera hello API bare, senza i moduli di raccolta dati di telemetria standard hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="a2fe4-116">Impostare la chiave di strumentazione hello nel codice:</span><span class="sxs-lookup"><span data-stu-id="a2fe4-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="a2fe4-117">`TelemetryConfiguration.Active.InstrumentationKey = "`*nome della chiave*`";`</span><span class="sxs-lookup"><span data-stu-id="a2fe4-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="a2fe4-118">o in Applicationinsights (se è installato uno dei pacchetti di dati di telemetria standard hello):</span><span class="sxs-lookup"><span data-stu-id="a2fe4-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="a2fe4-119">`<InstrumentationKey>`*chiave*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="a2fe4-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="a2fe4-120">Se si utilizza Applicationinsights, assicurarsi che le relative proprietà in Esplora soluzioni vengono impostate troppo**Build Action = il contenuto, copia tooOutput Directory = copia**.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="a2fe4-121">[Utilizzare l'API di hello](app-insights-api-custom-events-metrics.md) toosend telemetria.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="a2fe4-122">Eseguire l'app e visualizzare i dati di telemetria hello nella risorsa hello creato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe4-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="a2fe4-123"><a name="telemetry"></a>Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="a2fe4-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="a2fe4-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2fe4-124">Next steps</span></span>
* [<span data-ttu-id="a2fe4-125">Creare un dashboard</span><span class="sxs-lookup"><span data-stu-id="a2fe4-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="a2fe4-126">Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="a2fe4-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a2fe4-127">Esplorare le metriche</span><span class="sxs-lookup"><span data-stu-id="a2fe4-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="a2fe4-128">Scrivere query di Analisi</span><span class="sxs-lookup"><span data-stu-id="a2fe4-128">Write Analytics queries</span></span>](app-insights-analytics.md)

