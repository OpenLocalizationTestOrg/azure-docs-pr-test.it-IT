---
title: ruoli di server e di lavoro di Application Insights per Windows aaaAzure | Documenti Microsoft
description: "Aggiungere manualmente le prestazioni, disponibilità e utilizzo di Application Insights SDK tooyour ASP.NET dell'applicazione tooanalyze hello."
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
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="d9cd2-103">Configurare manualmente Application Insights per applicazioni .NET</span><span class="sxs-lookup"><span data-stu-id="d9cd2-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="d9cd2-104">È possibile configurare [Application Insights](app-insights-overview.md) toomonitor un'ampia gamma di applicazioni o i ruoli applicazione, componenti o microservizi.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="d9cd2-105">Per i servizi e le app Web, Visual Studio offre una [configurazione in un solo passaggio](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="d9cd2-106">Per altri tipi di applicazione .NET, come ruoli server back-end o applicazioni desktop, è possibile configurare Application Insights manualmente.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="d9cd2-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d9cd2-108">Before you start</span></span>

<span data-ttu-id="d9cd2-109">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="d9cd2-109">You need:</span></span>

* <span data-ttu-id="d9cd2-110">Una sottoscrizione troppo[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="d9cd2-111">Se il team o l'organizzazione dispone di una sottoscrizione di Azure, il proprietario di hello può aggiungere l'utente tooit, utilizzando il [account Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="d9cd2-112">Visual Studio 2013 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="d9cd2-113"><a name="add"></a>1. Scegliere una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="d9cd2-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="d9cd2-114">risorsa' Hello' è in cui i dati vengono raccolti e visualizzati nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="d9cd2-115">È necessario se toodecide toocreate uno nuovo, o una condivisione esistente.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="d9cd2-116">Parte di un'app più grande: usare una risorsa esistente</span><span class="sxs-lookup"><span data-stu-id="d9cd2-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="d9cd2-117">Se l'applicazione web dispone di diversi componenti, ad esempio, un'applicazione web front-end e uno o più servizi back-end - quindi inviare i dati di telemetria da tutti i toohello componenti hello stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="d9cd2-118">Verrà abilitarli toobe visualizzato in un singolo mapping di applicazioni e rendere possibili tootrace una richiesta da un componente tooanother.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="d9cd2-119">In tal caso, se si sta già monitorando altri componenti di questa app, quindi utilizza solo hello stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="d9cd2-120">Aprire la risorsa hello in hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="d9cd2-121">App completa: creare una nuova risorsa</span><span class="sxs-lookup"><span data-stu-id="d9cd2-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="d9cd2-122">Se le applicazioni non correlate tooother hello nuova app, deve essere la propria risorsa.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="d9cd2-123">Accedi toohello [portale di Azure](https://portal.azure.com/)e creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="d9cd2-124">Scegliere ASP.NET come tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-124">Choose ASP.NET as hello application type.</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="d9cd2-126">tipo di applicazione scelto Hello imposta contenuto predefinito hello dei pannelli risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="d9cd2-127">2. Copiare hello chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="d9cd2-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="d9cd2-128">chiave di Hello identifica risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-128">hello key identifies hello resource.</span></span> <span data-ttu-id="d9cd2-129">Verrà installato appena in hello SDK, nella risorsa toohello dati toodirect di ordine.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Fare clic su proprietà, selezionare la chiave hello e premere ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="d9cd2-131"><a name="sdk"></a>3. Installare il pacchetto Application Insights hello nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d9cd2-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="d9cd2-132">Installazione e configurazione di hello Application Insights pacchetto varia a seconda della piattaforma hello che stai lavorando.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="d9cd2-133">In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Fare clic sul progetto hello e scegliere Gestisci pacchetti Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="d9cd2-135">Installare il pacchetto Application Insights hello per le app di Windows server, "Microsoft.ApplicationInsights.WindowsServer".</span><span class="sxs-lookup"><span data-stu-id="d9cd2-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Cercare "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="d9cd2-137">*Quale versione?*</span><span class="sxs-lookup"><span data-stu-id="d9cd2-137">*Which version?*</span></span>

    <span data-ttu-id="d9cd2-138">Controllare **Includi versione preliminare** se si desidera tootry funzionalità più recenti.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="d9cd2-139">documenti rilevanti Hello o blog Nota Se è necessaria una versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="d9cd2-140">*È possibile usare altri pacchetti?*</span><span class="sxs-lookup"><span data-stu-id="d9cd2-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="d9cd2-141">Sì.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-141">Yes.</span></span> <span data-ttu-id="d9cd2-142">Se si desidera toouse hello API toosend propri dati di telemetria, scegliere "Microsoft. applicationinsights".</span><span class="sxs-lookup"><span data-stu-id="d9cd2-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="d9cd2-143">pacchetto di Windows Server Hello include hello API più una serie di altri pacchetti, ad esempio la raccolta dei contatori delle prestazioni e il monitoraggio della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="d9cd2-144">versioni del pacchetto toofuture tooupgrade</span><span class="sxs-lookup"><span data-stu-id="d9cd2-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="d9cd2-145">Microsoft rilasciare una nuova versione di hello SDK da tootime ora.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="d9cd2-146">tooupgrade tooa [nuova versione del pacchetto di hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), riaprire Gestione pacchetti NuGet e filtrare i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="d9cd2-147">Selezionare **Microsoft.ApplicationInsights.WindowsServer** e scegliere **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="d9cd2-148">Se sono state tooApplicationInsights.config eventuali personalizzazioni, salvare una copia prima di eseguire l'aggiornamento, nella nuova versione di hello in seguito il merge delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="d9cd2-149">4. Inviare dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="d9cd2-149">4. Send telemetry</span></span>
<span data-ttu-id="d9cd2-150">**Se è installato solo il pacchetto hello API:**</span><span class="sxs-lookup"><span data-stu-id="d9cd2-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="d9cd2-151">Impostare la chiave di strumentazione hello nel codice, ad esempio `main()`:</span><span class="sxs-lookup"><span data-stu-id="d9cd2-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="d9cd2-152">`TelemetryConfiguration.Active.InstrumentationKey = "`*nome della chiave*`";`</span><span class="sxs-lookup"><span data-stu-id="d9cd2-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="d9cd2-153">[Scrivere i propri dati di telemetria usando API hello](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="d9cd2-154">**Se sono installati altri pacchetti di Application Insights,** è possibile utilizzare in se si preferisce, chiave di strumentazione hello tooset file config hello:</span><span class="sxs-lookup"><span data-stu-id="d9cd2-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="d9cd2-155">Modificare Applicationinsights (che è stato aggiunto per installare NuGet hello).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="d9cd2-156">Inserire questa istruzione prima hello tag di chiusura:</span><span class="sxs-lookup"><span data-stu-id="d9cd2-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="d9cd2-157">`<InstrumentationKey>`*chiave di strumentazione hello copiato*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="d9cd2-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="d9cd2-158">Verificare che la proprietà hello di Applicationinsights in Esplora soluzioni è impostata troppo**Build Action = il contenuto, copia tooOutput Directory = copia**.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="d9cd2-159">È utile tooset hello strumentazione chiave nel codice se si desidera troppo[chiave hello commutatore per diverse configurazioni della build](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="d9cd2-160">Se si imposta la chiave hello nel codice, non è necessario tooset in hello `.config` file.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="d9cd2-161"><a name="run"></a> Eseguire il progetto</span><span class="sxs-lookup"><span data-stu-id="d9cd2-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="d9cd2-162">Hello utilizzare **F5** toorun l'applicazione e per provarlo: Apri diverse pagine toogenerate alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="d9cd2-163">In Visual Studio, verrà visualizzato un conteggio di eventi di hello che sono stati inviati.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Conteggio degli eventi in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="d9cd2-165"><a name="monitor"></a> Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="d9cd2-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="d9cd2-166">Restituire toohello [portale di Azure](https://portal.azure.com/) e individuare la risorsa di Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="d9cd2-167">Cercare i dati nei grafici Panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="d9cd2-168">All'inizio si vedranno solo uno o due punti.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="d9cd2-169">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d9cd2-169">For example:</span></span>

![Fare clic sui dati toomore](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="d9cd2-171">Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="d9cd2-172">Altre informazioni sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="d9cd2-173">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="d9cd2-173">No data?</span></span>
* <span data-ttu-id="d9cd2-174">Utilizzare l'applicazione hello, apertura di pagine diverse in modo che generi alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="d9cd2-175">Aprire hello [ricerca](app-insights-diagnostic-search.md) riquadro, toosee singoli eventi.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="d9cd2-176">In alcuni casi accetta eventi poco mentre più tooget tramite pipeline metriche hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="d9cd2-177">Attendere alcuni secondi e fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="d9cd2-178">Grafici Aggiorna periodicamente se stessi, ma è possibile aggiornare manualmente, se in attesa per tooshow alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="d9cd2-179">Vedere [Domande su Application Insights per ASP.NET](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="d9cd2-180">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="d9cd2-180">Publish your app</span></span>
<span data-ttu-id="d9cd2-181">Ora di distribuire il server di applicazioni tooyour o accumulano dati hello tooAzure ed espressioni di controllo.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Uso di Visual Studio toopublish dell'app](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="d9cd2-183">Quando si esegue in modalità di debug, dati di telemetria viene avviata tramite pipeline hello, in modo che verranno visualizzati i dati visualizzati in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="d9cd2-184">Quando si distribuisce l'applicazione nella configurazione Release, i dati si accumulano più lentamente.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="d9cd2-185">Nessun dato dopo la pubblicazione tooyour server?</span><span class="sxs-lookup"><span data-stu-id="d9cd2-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="d9cd2-186">Aprire le porte per il traffico in uscita nel firewall del server.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="d9cd2-187">Vedere [questa pagina](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) per elenco hello di indirizzi richiesti</span><span class="sxs-lookup"><span data-stu-id="d9cd2-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="d9cd2-188">Problemi del server di compilazione</span><span class="sxs-lookup"><span data-stu-id="d9cd2-188">Trouble on your build server?</span></span>
<span data-ttu-id="d9cd2-189">Vedere [questa sezione sulla risoluzione dei problemi](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="d9cd2-190">Se l'applicazione genera un grande quantità di dati di telemetria, modulo di campionamento adattivo hello ridurrà automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="d9cd2-191">Tuttavia, gli eventi che sono correlato toohello stessa richiesta verrà selezionata o deselezionata come gruppo, in modo che è possibile spostarsi tra gli eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="d9cd2-192">[Informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd2-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="d9cd2-193">Video</span><span class="sxs-lookup"><span data-stu-id="d9cd2-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d9cd2-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9cd2-194">Next steps</span></span>
* <span data-ttu-id="d9cd2-195">[Aggiungere ulteriori dati di telemetria](app-insights-asp-net-more.md) tooget hello 360 gradi di visualizzazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d9cd2-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

