---
title: Azure Application Insights per Windows Server e ruoli di lavoro | Microsoft Docs
description: "Aggiungere manualmente Application Insights SDK all'applicazione ASP.NET per analizzare utilizzo, disponibilità e prestazioni."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="eb92e-103">Configurare manualmente Application Insights per applicazioni .NET</span><span class="sxs-lookup"><span data-stu-id="eb92e-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="eb92e-104">È possibile configurare [Application Insights](app-insights-overview.md) per monitorare un'ampia gamma di applicazioni o componenti, microservizi o ruoli applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb92e-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="eb92e-105">Per i servizi e le app Web, Visual Studio offre una [configurazione in un solo passaggio](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="eb92e-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="eb92e-106">Per altri tipi di applicazione .NET, come ruoli server back-end o applicazioni desktop, è possibile configurare Application Insights manualmente.</span><span class="sxs-lookup"><span data-stu-id="eb92e-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="eb92e-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="eb92e-108">Before you start</span></span>

<span data-ttu-id="eb92e-109">È necessario:</span><span class="sxs-lookup"><span data-stu-id="eb92e-109">You need:</span></span>

* <span data-ttu-id="eb92e-110">Una sottoscrizione a [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="eb92e-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="eb92e-111">Se il team o l'organizzazione ha una sottoscrizione di Azure, il proprietario potrà aggiungere l'utente alla sottoscrizione usando il rispettivo [account Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="eb92e-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="eb92e-112">Visual Studio 2013 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="eb92e-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="eb92e-113"><a name="add"></a>1. Scegliere una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="eb92e-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="eb92e-114">La "risorsa" è la posizione in cui verranno raccolti e visualizzati i dati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb92e-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="eb92e-115">È necessario decidere se crearne una nuova oppure condividerne una esistente.</span><span class="sxs-lookup"><span data-stu-id="eb92e-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="eb92e-116">Parte di un'app più grande: usare una risorsa esistente</span><span class="sxs-lookup"><span data-stu-id="eb92e-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="eb92e-117">Se l'applicazione Web include diversi componenti, ad esempio un'app Web front-end e uno o più servizi back-end, è consigliabile inviare i dati di telemetria di tutti i componenti alla stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb92e-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="eb92e-118">In questo modo potranno essere visualizzati in una singola mappa delle applicazioni e sarà possibile tracciare una richiesta da un componente a un altro.</span><span class="sxs-lookup"><span data-stu-id="eb92e-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="eb92e-119">Se vengono già monitorati altri componenti dell'app, usare quindi la stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb92e-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="eb92e-120">Aprire la risorsa nel [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb92e-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="eb92e-121">App completa: creare una nuova risorsa</span><span class="sxs-lookup"><span data-stu-id="eb92e-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="eb92e-122">Se la nuova app non è correlata ad altre applicazioni, dovrà avere una propria risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb92e-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="eb92e-123">Accedere al [portale di Azure](https://portal.azure.com/)e creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eb92e-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="eb92e-124">Scegliere ASP.NET come tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb92e-124">Choose ASP.NET as the application type.</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="eb92e-126">La scelta del tipo di applicazione determina l'impostazione del contenuto predefinito dei pannelli della risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb92e-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="eb92e-127">2. Eseguire una copia della chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="eb92e-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="eb92e-128">La chiave identifica la risorsa</span><span class="sxs-lookup"><span data-stu-id="eb92e-128">The key identifies the resource.</span></span> <span data-ttu-id="eb92e-129">e verrà installata nell'SDK per indirizzare i dati alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb92e-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![Fare clic su Proprietà, selezionare il tasto e premere CTRL+C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="eb92e-131"><a name="sdk"></a>3. Installare il pacchetto Application Insights nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="eb92e-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="eb92e-132">L'installazione e la configurazione del pacchetto Application Insights variano a seconda della piattaforma in cui si lavora.</span><span class="sxs-lookup"><span data-stu-id="eb92e-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="eb92e-133">In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eb92e-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Fare clic con il pulsante destro del mouse sul progetto e selezionare Gestisci pacchetti NuGet](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="eb92e-135">Installare il pacchetto Application Insights per le app di Windows Server, "Microsoft.ApplicationInsights.WindowsServer".</span><span class="sxs-lookup"><span data-stu-id="eb92e-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Cercare "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="eb92e-137">*Quale versione?*</span><span class="sxs-lookup"><span data-stu-id="eb92e-137">*Which version?*</span></span>

    <span data-ttu-id="eb92e-138">Per provare le funzionalità più recenti, selezionare **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="eb92e-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="eb92e-139">I documenti o i blog pertinenti indicano se è necessaria una versione preliminare.</span><span class="sxs-lookup"><span data-stu-id="eb92e-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="eb92e-140">*È possibile usare altri pacchetti?*</span><span class="sxs-lookup"><span data-stu-id="eb92e-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="eb92e-141">Sì.</span><span class="sxs-lookup"><span data-stu-id="eb92e-141">Yes.</span></span> <span data-ttu-id="eb92e-142">Se si vuole solo usare l'API per inviare i propri dati di telemetria, scegliere "Microsoft.ApplicationInsights".</span><span class="sxs-lookup"><span data-stu-id="eb92e-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="eb92e-143">Il pacchetto per Windows Server include l'API e diversi altri pacchetti, ad esempio la raccolta dei contatori delle prestazioni e il monitoraggio delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="eb92e-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="eb92e-144">Per eseguire l'aggiornamento a future versioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="eb92e-144">To upgrade to future package versions</span></span>
<span data-ttu-id="eb92e-145">Si rilascerà una nuova versione del SDK di tanto in tanto.</span><span class="sxs-lookup"><span data-stu-id="eb92e-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="eb92e-146">Per eseguire l'aggiornamento a una [nuova versione del pacchetto](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), riaprire Gestione pacchetti NuGet e filtrare i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="eb92e-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="eb92e-147">Selezionare **Microsoft.ApplicationInsights.WindowsServer** e scegliere **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="eb92e-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="eb92e-148">Se sono state eseguite tutte le personalizzazioni apportate al file ApplicationInsights.config, salvarne una copia prima di eseguire l'aggiornamento e, successivamente, unire le modifiche nella nuova versione.</span><span class="sxs-lookup"><span data-stu-id="eb92e-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="eb92e-149">4. Inviare dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="eb92e-149">4. Send telemetry</span></span>
<span data-ttu-id="eb92e-150">**Se è stato installato solo il pacchetto dell'API:**</span><span class="sxs-lookup"><span data-stu-id="eb92e-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="eb92e-151">Impostare la chiave di strumentazione nel codice, ad esempio in `main()`:</span><span class="sxs-lookup"><span data-stu-id="eb92e-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="eb92e-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *nome della chiave* `";`</span><span class="sxs-lookup"><span data-stu-id="eb92e-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="eb92e-153">[Scrivere dati di telemetria usando l'API](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="eb92e-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="eb92e-154">**Se sono installati altri pacchetti di Application Insights** è possibile, se si preferisce, usare il file config per impostare la chiave di strumentazione:</span><span class="sxs-lookup"><span data-stu-id="eb92e-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="eb92e-155">Modificare ApplicationInsights.config (che è stato aggiunto dall'installazione di NuGet).</span><span class="sxs-lookup"><span data-stu-id="eb92e-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="eb92e-156">Inserire questo comando immediatamente prima del tag di chiusura:</span><span class="sxs-lookup"><span data-stu-id="eb92e-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="eb92e-157">`<InstrumentationKey>` *chiave di strumentazione copiata* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="eb92e-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="eb92e-158">Verificare che le proprietà di ApplicationInsights.config in Esplora soluzioni siano impostate su **= Contenuto, Copia nella directory di output = Copia**.</span><span class="sxs-lookup"><span data-stu-id="eb92e-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="eb92e-159">È utile impostare la chiave di strumentazione nel codice se si vuole [cambiare la chiave per configurazioni della build diverse](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="eb92e-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="eb92e-160">Se si imposta la chiave nel codice, non è necessario impostarla nel file `.config`.</span><span class="sxs-lookup"><span data-stu-id="eb92e-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="eb92e-161"><a name="run"></a> Eseguire il progetto</span><span class="sxs-lookup"><span data-stu-id="eb92e-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="eb92e-162">Eseguire l'applicazione premendo **F5** e provarla aprendo pagine diverse per generare alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="eb92e-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="eb92e-163">In Visual Studio verrà visualizzato il conteggio degli eventi che sono stati inviati.</span><span class="sxs-lookup"><span data-stu-id="eb92e-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Conteggio degli eventi in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="eb92e-165"><a name="monitor"></a> Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="eb92e-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="eb92e-166">Tornare al [portale di Azure](https://portal.azure.com/) e passare alla risorsa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eb92e-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="eb92e-167">Cercare i dati nei grafici Panoramica.</span><span class="sxs-lookup"><span data-stu-id="eb92e-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="eb92e-168">All'inizio si vedranno solo uno o due punti.</span><span class="sxs-lookup"><span data-stu-id="eb92e-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="eb92e-169">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="eb92e-169">For example:</span></span>

![Fare clic per visualizzare altri dati.](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="eb92e-171">Fare clic su qualsiasi grafico per visualizzare metriche più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="eb92e-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="eb92e-172">Altre informazioni sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="eb92e-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="eb92e-173">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="eb92e-173">No data?</span></span>
* <span data-ttu-id="eb92e-174">Usare l'applicazione, aprendo pagine diverse in modo da generare alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="eb92e-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="eb92e-175">Aprire il riquadro [Ricerca](app-insights-diagnostic-search.md) per visualizzare i singoli eventi.</span><span class="sxs-lookup"><span data-stu-id="eb92e-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="eb92e-176">Talvolta agli eventi ci vuole un po' più di tempo per passare attraverso la pipeline delle metriche.</span><span class="sxs-lookup"><span data-stu-id="eb92e-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="eb92e-177">Attendere alcuni secondi e fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="eb92e-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="eb92e-178">I grafici si aggiornano periodicamente, ma è possibile aggiornare manualmente se si è in attesa di alcuni dati da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="eb92e-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="eb92e-179">Vedere [Domande su Application Insights per ASP.NET](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="eb92e-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="eb92e-180">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="eb92e-180">Publish your app</span></span>
<span data-ttu-id="eb92e-181">Distribuire ora l'applicazione nel server o in Azure e osservare l'accumulo dei dati.</span><span class="sxs-lookup"><span data-stu-id="eb92e-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Utilizzare Visual Studio per pubblicare l'app](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="eb92e-183">Quando si esegue la modalità debug, la telemetria viene velocizzata nella pipeline, quindi i dati vengono visualizzati in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="eb92e-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="eb92e-184">Quando si distribuisce l'applicazione nella configurazione Release, i dati si accumulano più lentamente.</span><span class="sxs-lookup"><span data-stu-id="eb92e-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="eb92e-185">Nessun dato dopo la pubblicazione nel server?</span><span class="sxs-lookup"><span data-stu-id="eb92e-185">No data after you publish to your server?</span></span>
<span data-ttu-id="eb92e-186">Aprire le porte per il traffico in uscita nel firewall del server.</span><span class="sxs-lookup"><span data-stu-id="eb92e-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="eb92e-187">Per l'elenco degli indirizzi necessari, vedere [questa pagina](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="eb92e-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="eb92e-188">Problemi del server di compilazione</span><span class="sxs-lookup"><span data-stu-id="eb92e-188">Trouble on your build server?</span></span>
<span data-ttu-id="eb92e-189">Vedere [questa sezione sulla risoluzione dei problemi](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="eb92e-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="eb92e-190">Se l’app genera molti dati di telemetria, il modulo di campionamento adattivo riduce automaticamente il volume che viene inviato al portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="eb92e-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="eb92e-191">Tuttavia, gli eventi che fanno parte della stessa richiesta verranno selezionati o deselezionati come gruppo, per rendere possibile lo spostamento tra eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="eb92e-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="eb92e-192">[Informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="eb92e-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="eb92e-193">Video</span><span class="sxs-lookup"><span data-stu-id="eb92e-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="eb92e-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb92e-194">Next steps</span></span>
* <span data-ttu-id="eb92e-195">[Aggiungere altri dati di telemetria](app-insights-asp-net-more.md) per un quadro completo a 360 gradi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb92e-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

