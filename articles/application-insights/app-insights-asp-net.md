---
title: Configurare l'analisi di app Web per ASP.NET con Azure Application Insights | Microsoft Docs
description: "Configurare l'analisi delle prestazioni, della disponibilità e dell'utilizzo per un sito Web ASP.NET, ospitato in locale o in Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="58a17-103">Installare Application Insights per un sito Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="58a17-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="58a17-104">Questa procedura consente di configurare un'app Web ASP.NET per l'invio di dati di telemetria al servizio [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58a17-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="58a17-105">È valida per le app ASP.NET ospitate nel server IIS o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="58a17-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="58a17-106">Offre grafici e un linguaggio di query avanzato che permettono di comprendere le prestazioni dell'app e il suo utilizzo da parte degli utenti, oltre ad avvisi automatici in caso di errori o problemi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="58a17-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="58a17-107">Molti sviluppatori trovano utili queste funzionalità così come sono, ma è anche possibile estendere e personalizzare i dati di telemetria, se necessario.</span><span class="sxs-lookup"><span data-stu-id="58a17-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="58a17-108">Il programma di installazione richiede pochi clic in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58a17-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="58a17-109">Per evitare addebiti è possibile limitare il volume dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58a17-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="58a17-110">In questo modo è possibile provare le funzionalità ed eseguire il debug o monitorare un sito con un numero di utenti limitato.</span><span class="sxs-lookup"><span data-stu-id="58a17-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="58a17-111">Se si decide di monitorare l'intero sito di produzione, è facile aumentare il limite in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="58a17-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="58a17-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="58a17-112">Before you start</span></span>
<span data-ttu-id="58a17-113">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="58a17-113">You need:</span></span>

* <span data-ttu-id="58a17-114">Visual Studio 2013 Update 3 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="58a17-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="58a17-115">È preferibile una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="58a17-115">Later is better.</span></span>
* <span data-ttu-id="58a17-116">Una sottoscrizione a [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="58a17-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="58a17-117">Se il team o l'organizzazione ha una sottoscrizione di Azure, il proprietario potrà aggiungere l'utente alla sottoscrizione usando il rispettivo [account Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="58a17-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="58a17-118">Se si è interessati, vedere gli argomenti alternativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="58a17-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="58a17-119">Strumentazione di un'app Web in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="58a17-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="58a17-120">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="58a17-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="58a17-121"><a name="ide"></a>Passaggio 1: Aggiungere Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="58a17-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="58a17-122">Fare clic con il pulsante destro del mouse sul progetto dell'app Web in Esplora soluzioni e scegliere **Aggiungi** > **Application Insights Telemetry** oppure **Configura Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="58a17-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Screenshot di Esplora soluzioni con le opzioni Aggiungi e Application Insights Telemetry evidenziate](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="58a17-124">In Visual Studio 2015, un'opzione per l'aggiunta di Application Insights è disponibile anche nella finestra di dialogo Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="58a17-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="58a17-125">Passare alla pagina di configurazione di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="58a17-125">Continue to the Application Insights configuration page:</span></span>

![Screenshot della pagina Registra l'app con Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="58a17-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="58a17-127">**a.**</span></span> <span data-ttu-id="58a17-128">Selezionare l'account e la sottoscrizione usati per accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="58a17-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="58a17-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="58a17-129">**b.**</span></span> <span data-ttu-id="58a17-130">Selezionare la risorsa in Azure in cui si vogliono visualizzare i dati dell'app.</span><span class="sxs-lookup"><span data-stu-id="58a17-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="58a17-131">In genere:</span><span class="sxs-lookup"><span data-stu-id="58a17-131">Usually:</span></span>

* <span data-ttu-id="58a17-132">Usare un'[unica risorsa per diversi componenti](app-insights-monitor-multi-role-apps.md) di una singola applicazione.</span><span class="sxs-lookup"><span data-stu-id="58a17-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="58a17-133">Creare risorse separate per applicazioni non correlate.</span><span class="sxs-lookup"><span data-stu-id="58a17-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="58a17-134">Se si vuole impostare il gruppo di risorse o la località in cui verranno archiviati i dati, fare clic su **Configura impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="58a17-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="58a17-135">I gruppi di risorse vengono usati per controllare l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="58a17-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="58a17-136">Se si hanno diverse app che fanno parte dello stesso sistema, ad esempio, è possibile inserire i relativi dati di Application Insights nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="58a17-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="58a17-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="58a17-137">**c.**</span></span> <span data-ttu-id="58a17-138">Impostare un tetto massimo al limite del volume di dati gratuito, per evitare eventuali addebiti.</span><span class="sxs-lookup"><span data-stu-id="58a17-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="58a17-139">Application Insights è gratuito fino a un determinato volume di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58a17-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="58a17-140">Dopo aver creato la risorsa, è possibile modificare la selezione nel portale aprendo **Funzionalità + prezzi** > **Gestione del volume dati** > **Limite di utilizzo volume giornaliero**.</span><span class="sxs-lookup"><span data-stu-id="58a17-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="58a17-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="58a17-141">**d.**</span></span> <span data-ttu-id="58a17-142">Fare clic su **Registra** per proseguire e configurare Application Insights per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="58a17-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="58a17-143">I dati di telemetria verranno inviati al [portale di Azure](https://portal.azure.com), sia durante il debug che dopo la pubblicazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="58a17-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="58a17-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="58a17-144">**e.**</span></span> <span data-ttu-id="58a17-145">Per non inviare i dati di telemetria al portale durante il debug, è possibile aggiungere Application Insights SDK all'app senza configurare una risorsa nel portale.</span><span class="sxs-lookup"><span data-stu-id="58a17-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="58a17-146">Si potranno visualizzare i dati di telemetria in Visual Studio durante il debug.</span><span class="sxs-lookup"><span data-stu-id="58a17-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="58a17-147">Successivamente, è possibile tornare a questa pagina di configurazione oppure attendere di aver distribuito l'app e quindi [attivare la telemetria in fase di esecuzione](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="58a17-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="58a17-148"><a name="run"></a>Passaggio 2: Eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="58a17-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="58a17-149">Eseguire l'app con F5.</span><span class="sxs-lookup"><span data-stu-id="58a17-149">Run your app with F5.</span></span> <span data-ttu-id="58a17-150">Aprire pagine diverse per generare alcuni dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58a17-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="58a17-151">In Visual Studio verrà visualizzato il conteggio degli eventi che sono stati registrati.</span><span class="sxs-lookup"><span data-stu-id="58a17-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Screenshot di Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="58a17-154">Passaggio 3: Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="58a17-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="58a17-155">È possibile visualizzare i dati di telemetria in Visual Studio o nel portale Web di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a17-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="58a17-156">Cercare i dati di telemetria in Visual Studio per eseguire il debug dell'app.</span><span class="sxs-lookup"><span data-stu-id="58a17-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="58a17-157">Monitorare le prestazioni e l'utilizzo nel portale Web quando il sistema è attivo.</span><span class="sxs-lookup"><span data-stu-id="58a17-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="58a17-158">Visualizzare i dati di telemetria in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58a17-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="58a17-159">In Visual Studio aprire la finestra di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a17-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="58a17-160">Fare clic sul pulsante **Application Insights** oppure fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Application Insights** e quindi fare clic su **Cerca nei dati di telemetria attivi**.</span><span class="sxs-lookup"><span data-stu-id="58a17-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="58a17-161">Nella finestra Ricerca di Application Insights di Visual Studio esaminare i dati di telemetria generati sul lato server dell'app nella visualizzazione **Dati di Dati di telemetria della sessione di debug**.</span><span class="sxs-lookup"><span data-stu-id="58a17-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="58a17-162">Sperimentare i filtri e fare clic su qualsiasi evento per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="58a17-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Screenshot della visualizzazione Dati di Dati di telemetria della sessione di debug nella finestra di Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="58a17-164">Se non vengono visualizzati dati, verificare che l'intervallo di tempo sia corretto e fare clic sull'icona di ricerca.</span><span class="sxs-lookup"><span data-stu-id="58a17-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="58a17-165">[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="58a17-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="58a17-166">Visualizzare i dati di telemetria nel portale Web</span><span class="sxs-lookup"><span data-stu-id="58a17-166">See telemetry in web portal</span></span>

<span data-ttu-id="58a17-167">Se non si è scelto di installare solo l'SDK, è possibile visualizzare i dati di telemetria anche nel portale Web di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a17-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="58a17-168">Il portale offre un maggior numero di grafici, strumenti di analisi e viste di più componenti rispetto a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58a17-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="58a17-169">Nel portale sono anche disponibili avvisi.</span><span class="sxs-lookup"><span data-stu-id="58a17-169">The portal also provides alerts.</span></span>

<span data-ttu-id="58a17-170">Aprire la risorsa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a17-170">Open your Application Insights resource.</span></span> <span data-ttu-id="58a17-171">Accedere al [portale di Azure](https://portal.azure.com/) per cercarla o fare clic con il pulsante destro del mouse sul progetto in Visual Studio e scegliere la risorsa.</span><span class="sxs-lookup"><span data-stu-id="58a17-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Screenshot di Visual Studio che mostra come aprire il portale di Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="58a17-173">Se viene visualizzato un errore di accesso, è possibile che si abbiano più set di credenziali Microsoft e che l'accesso sia stato eseguito con il set sbagliato.</span><span class="sxs-lookup"><span data-stu-id="58a17-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="58a17-174">Nel portale disconnettersi e accedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="58a17-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="58a17-175">Nel portale verrà visualizzata la telemetria dell'app.</span><span class="sxs-lookup"><span data-stu-id="58a17-175">The portal opens on a view of the telemetry from your app.</span></span>

![Screenshot della pagina Panoramica di Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="58a17-177">Per visualizzare altri dettagli nel portale, fare clic su qualsiasi riquadro o grafico.</span><span class="sxs-lookup"><span data-stu-id="58a17-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="58a17-178">[Altre informazioni sull'uso di Application Insights nel portale di Azure](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="58a17-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="58a17-179">Passaggio 4: Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="58a17-179">Step 4: Publish your app</span></span>
<span data-ttu-id="58a17-180">Pubblicare l'app nel server IIS o in Azure.</span><span class="sxs-lookup"><span data-stu-id="58a17-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="58a17-181">Verificare in [Flusso metriche attive](app-insights-metrics-explorer.md#live-metrics-stream) che tutto funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="58a17-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="58a17-182">La telemetria viene creata nel portale di Application Insights, in cui è possibile monitorare le metriche, eseguire ricerche sui dati di telemetria e configurare i [dashboard](app-insights-dashboards.md),</span><span class="sxs-lookup"><span data-stu-id="58a17-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="58a17-183">nonché usare l'avanzato [linguaggio di query di Log Analytics](https://docs.loganalytics.io/) per analizzare l'utilizzo e le prestazioni o trovare eventi specifici.</span><span class="sxs-lookup"><span data-stu-id="58a17-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="58a17-184">È anche possibile continuare ad analizzare i dati di telemetria in [Visual Studio](app-insights-visual-studio.md) con strumenti come la ricerca diagnostica e le [tendenze](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="58a17-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58a17-185">Se la quantità di dati di telemetria inviata dall'app sta per raggiungere le [limitazioni](app-insights-pricing.md#limits-summary), viene attivato il [campionamento](app-insights-sampling.md) automatico.</span><span class="sxs-lookup"><span data-stu-id="58a17-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="58a17-186">Il campionamento riduce la quantità di dati di telemetria inviata dall'app mantenendo i dati correlati per scopi diagnostici.</span><span class="sxs-lookup"><span data-stu-id="58a17-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="58a17-187"><a name="land"></a> Le impostazioni sono state completate.</span><span class="sxs-lookup"><span data-stu-id="58a17-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="58a17-188">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="58a17-188">Congratulations!</span></span> <span data-ttu-id="58a17-189">Il pacchetto Application Insights è stato installato nell'app e configurato per l'invio di dati di telemetria al servizio Application Insights in Azure.</span><span class="sxs-lookup"><span data-stu-id="58a17-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagramma dello spostamento dei dati di telemetria](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="58a17-191">La risorsa di Azure che riceve i dati di telemetria dell'app è identificata da una *chiave di strumentazione*,</span><span class="sxs-lookup"><span data-stu-id="58a17-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="58a17-192">disponibile nel file ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="58a17-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="58a17-193">Eseguire l'aggiornamento alle versioni future dell'SDK</span><span class="sxs-lookup"><span data-stu-id="58a17-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="58a17-194">Per eseguire l'aggiornamento a una [nuova versione dell'SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), aprire di nuovo **Gestione pacchetti NuGet** e filtrare i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="58a17-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="58a17-195">Selezionare **Microsoft.ApplicationInsights.Web** e scegliere **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="58a17-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="58a17-196">Se sono state apportate personalizzazioni a ApplicationInsights.config, salvarne una copia prima di eseguire l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="58a17-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="58a17-197">Successivamente, unire le modifiche nella nuova versione.</span><span class="sxs-lookup"><span data-stu-id="58a17-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="58a17-198">Video</span><span class="sxs-lookup"><span data-stu-id="58a17-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="58a17-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58a17-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="58a17-200">Altri dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="58a17-200">More telemetry</span></span>

* <span data-ttu-id="58a17-201">**[Dati sul browser e sul caricamento di pagine](app-insights-javascript.md)**: inserire un frammento di codice nelle pagine Web.</span><span class="sxs-lookup"><span data-stu-id="58a17-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="58a17-202">**[Ottenere un monitoraggio più dettagliato di dipendenze ed eccezioni](app-insights-monitor-performance-live-website-now.md)**: installare Status Monitor nel server.</span><span class="sxs-lookup"><span data-stu-id="58a17-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="58a17-203">**[Scrivere codice per gli eventi personalizzati](app-insights-api-custom-events-metrics.md)**: ottenere conteggi, orari o misurazioni delle azioni utente.</span><span class="sxs-lookup"><span data-stu-id="58a17-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="58a17-204">**[Ottenere dati di log](app-insights-asp-net-trace-logs.md)**: correlare i dati di log con i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58a17-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="58a17-205">Analisi</span><span class="sxs-lookup"><span data-stu-id="58a17-205">Analysis</span></span>

* <span data-ttu-id="58a17-206">**[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="58a17-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="58a17-207">Include informazioni su debug con telemetria, ricerca diagnostica e drill-through nel codice.</span><span class="sxs-lookup"><span data-stu-id="58a17-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="58a17-208">**[Uso del portale Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="58a17-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="58a17-209">Include informazioni su dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, mappa attiva delle dipendenze dell'applicazione ed esportazione dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="58a17-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="58a17-210">**[Analytics](app-insights-analytics-tour.md)**: linguaggio di query avanzato.</span><span class="sxs-lookup"><span data-stu-id="58a17-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="58a17-211">Avvisi</span><span class="sxs-lookup"><span data-stu-id="58a17-211">Alerts</span></span>

* <span data-ttu-id="58a17-212">[Test di disponibilità](app-insights-monitor-web-app-availability.md): creare test per verificare che il sito sia visibile sul Web.</span><span class="sxs-lookup"><span data-stu-id="58a17-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="58a17-213">[Diagnostica intelligente](app-insights-proactive-diagnostics.md): questi test vengono eseguiti automaticamente e non è quindi necessario effettuare alcuna operazione per configurarli.</span><span class="sxs-lookup"><span data-stu-id="58a17-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="58a17-214">Se l'app ha una frequenza insolita di richieste non riuscite, verrà comunicato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="58a17-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="58a17-215">[Avvisi per le metriche](app-insights-alerts.md): impostare questi avvisi per essere avvertiti se una metrica supera una soglia.</span><span class="sxs-lookup"><span data-stu-id="58a17-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="58a17-216">È possibile impostarli nelle metriche personalizzate di cui si scrive il codice nell'app.</span><span class="sxs-lookup"><span data-stu-id="58a17-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="58a17-217">Automazione</span><span class="sxs-lookup"><span data-stu-id="58a17-217">Automation</span></span>

* [<span data-ttu-id="58a17-218">Automatizzare la creazione di risorse di Application Insights</span><span class="sxs-lookup"><span data-stu-id="58a17-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
