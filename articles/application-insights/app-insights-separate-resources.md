---
title: telemetria aaaSeparating dallo sviluppo, test e rilascio in Azure Application Insights | Documenti Microsoft
description: Risorse di toodifferent diretto telemetria per gli indicatori di sviluppo, test e produzione.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="c626c-103">Separazione della telemetria da sviluppo, test e produzione</span><span class="sxs-lookup"><span data-stu-id="c626c-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="c626c-104">Quando si sviluppa prossima versione di hello di un'applicazione web, non si desidera toomix backup hello [Application Insights](app-insights-overview.md) telemetria dalla nuova versione di hello e hello già rilasciato.</span><span class="sxs-lookup"><span data-stu-id="c626c-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="c626c-105">tooavoid confusione, trasmissione hello telemetria dallo sviluppo diverso fasi di risorse di Application Insights tooseparate, con chiavi di strumentazione separato (ikeys).</span><span class="sxs-lookup"><span data-stu-id="c626c-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="c626c-106">toomake si sposta da una fase tooanother, chiave di strumentazione hello toochange più semplice come una versione può essere utile tooset hello ikey nel codice anziché in file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="c626c-107">Se il sistema è un servizio cloud di Azure, è disponibile [un altro metodo di impostazione di valori iKey separati](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="c626c-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="c626c-108">Sulle risorse e le chiavi di strumentazione</span><span class="sxs-lookup"><span data-stu-id="c626c-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="c626c-109">Quando si configura il monitoraggio di Application Insights per l'app Web, viene creata una *risorsa* di Application Insights in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c626c-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="c626c-110">Aprire questa risorsa nel portale di Azure in ordine toosee hello e analizzare dati di telemetria hello raccolti dall'app.</span><span class="sxs-lookup"><span data-stu-id="c626c-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="c626c-111">risorsa Hello è identificato da un *chiave di strumentazione* (ikey).</span><span class="sxs-lookup"><span data-stu-id="c626c-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="c626c-112">Quando si installa hello Application Insights pacchetto toomonitor dell'app, si configura con chiave di strumentazione hello, in modo che rilevi dove toosend hello telemetria.</span><span class="sxs-lookup"><span data-stu-id="c626c-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="c626c-113">È in genere scegliere risorse diverse toouse o una singola risorsa condivisa in scenari diversi:</span><span class="sxs-lookup"><span data-stu-id="c626c-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="c626c-114">Diverse applicazioni indipendenti: usare una risorsa separata e l'iKey per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="c626c-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="c626c-115">Utilizzare più componenti o i ruoli dell'applicazione di una business - un [singola risorsa condivisa](app-insights-monitor-multi-role-apps.md) per tutte le app di componente di hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="c626c-116">Dati di telemetria può essere filtrato o segmentate per proprietà cloud_RoleName hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="c626c-117">Sviluppo, Test e rilascio: utilizzare una risorsa distinta e ikey per le versioni del sistema hello in 'timestamp' o una fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="c626c-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="c626c-118">Test A | B: usare una singola risorsa.</span><span class="sxs-lookup"><span data-stu-id="c626c-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="c626c-119">È possibile creare un tooadd TelemetryInitializer telemetria di toohello una proprietà che identifica le varianti hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="c626c-120"><a name="dynamic-ikey"></a> Chiave di strumentazione dinamica</span><span class="sxs-lookup"><span data-stu-id="c626c-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="c626c-121">toomake che più semplice toochange hello ikey come codice hello si sposta tra le diverse fasi di produzione, impostati nel codice anziché nel file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="c626c-122">Impostare la chiave di hello in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c626c-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="c626c-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="c626c-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="c626c-124">In questo esempio, ikeys hello per le diverse risorse hello vengono posizionate in diverse versioni del file di configurazione web hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="c626c-125">File di configurazione web hello scambio, che è possibile eseguire come parte dello script di versione di hello - scambiano risorsa di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="c626c-126">Pagina Web</span><span class="sxs-lookup"><span data-stu-id="c626c-126">Web pages</span></span>
<span data-ttu-id="c626c-127">iKey Hello viene utilizzato anche nelle pagine web dell'app, in hello [script che è stato ottenuto dal pannello avvio rapido hello](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="c626c-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="c626c-128">Anziché nel codice viene letteralmente in script hello, generati dallo stato del server hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="c626c-129">Ad esempio, in un'app ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c626c-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="c626c-130">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="c626c-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="c626c-131">Creare risorse di Application Insights aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c626c-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="c626c-132">dati di telemetria tooseparate per componenti diversi dell'applicazione o per timbri differenti (sviluppo/test o produzione) di hello stesso componente, sarà necessario toocreate una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c626c-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="c626c-133">In hello [portal.azure.com](https://portal.azure.com), aggiungere una risorsa di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c626c-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="c626c-135">**Tipo di applicazione** influisce su ciò che viene visualizzato nel pannello della panoramica hello e le proprietà di hello disponibili in [Esplora metrica](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="c626c-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="c626c-136">Se non viene visualizzato il tipo di app, scegliere uno dei tipi di web hello per le pagine web.</span><span class="sxs-lookup"><span data-stu-id="c626c-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="c626c-137">**gruppo di risorse** è utile per gestire le proprietà come il [controllo di accesso](app-insights-resources-roles-access-controldi Microsoft Azure.md)di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c626c-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="c626c-138">È possibile usare gruppi di risorse separati per lo sviluppo, i test e la produzione.</span><span class="sxs-lookup"><span data-stu-id="c626c-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="c626c-139">**sottoscrizione** è il proprio account di pagamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="c626c-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="c626c-140">Il **percorso** è la posizione in cui vengono conservati i dati.</span><span class="sxs-lookup"><span data-stu-id="c626c-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="c626c-141">e attualmente non è modificabile.</span><span class="sxs-lookup"><span data-stu-id="c626c-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="c626c-142">**Aggiungere toodashboard** assegna un riquadro di accesso rapido per la risorsa per la Home page di Azure.</span><span class="sxs-lookup"><span data-stu-id="c626c-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="c626c-143">Creazione di risorse hello richiede pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="c626c-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="c626c-144">Al termine della creazione verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="c626c-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="c626c-145">(È possibile scrivere un [script di PowerShell](app-insights-powershell-script-create-resource.md) toocreate una risorsa automaticamente.)</span><span class="sxs-lookup"><span data-stu-id="c626c-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="c626c-146">Ottenere la chiave di strumentazione hello</span><span class="sxs-lookup"><span data-stu-id="c626c-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="c626c-147">chiave di strumentazione Hello identifica risorse hello creato.</span><span class="sxs-lookup"><span data-stu-id="c626c-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Essentials fare clic su hello chiave di strumentazione, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="c626c-149">Sono necessarie le chiavi di strumentazione hello di tutti i toowhich risorse hello l'app verrà inviato alcun dato.</span><span class="sxs-lookup"><span data-stu-id="c626c-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="c626c-150">Filtrare in base al numero di build</span><span class="sxs-lookup"><span data-stu-id="c626c-150">Filter on build number</span></span>
<span data-ttu-id="c626c-151">Quando si pubblica una nuova versione dell'app, è opportuno telemetria di hello in grado di tooseparate toobe dalle build diverse.</span><span class="sxs-lookup"><span data-stu-id="c626c-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="c626c-152">È possibile impostare proprietà di versione dell'applicazione hello in modo che è possibile filtrare [ricerca](app-insights-diagnostic-search.md) e [Esplora metrica](app-insights-metrics-explorer.md) risultati.</span><span class="sxs-lookup"><span data-stu-id="c626c-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtro su una proprietà](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="c626c-154">Esistono diversi metodi di impostazione di proprietà di versione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="c626c-155">Impostare direttamente:</span><span class="sxs-lookup"><span data-stu-id="c626c-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="c626c-156">Eseguire il wrapping di tale riga in un [inizializzatore telemetria](app-insights-api-custom-events-metrics.md#defaults) tooensure che tutte le istanze di TelemetryClient sono impostate in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="c626c-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="c626c-157">[ASP.NET] La versione di hello in `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="c626c-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="c626c-158">il modulo web Hello selezionerà versione hello dal nodo BuildLabel hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="c626c-159">Includere questo file nel progetto e ricordare di proprietà di tooset Copia sempre hello in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="c626c-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="c626c-160">[ASP.NET] Generare automaticamente BuildInfo.config in MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c626c-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="c626c-161">toodo, aggiungere alcune righe tooyour `.csproj` file:</span><span class="sxs-lookup"><span data-stu-id="c626c-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="c626c-162">Verrà generato un file denominato *yourProjectName*. Hello Buildinfo. processo di pubblicazione viene rinominato tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="c626c-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="c626c-163">etichetta di compilazione Hello contiene un segnaposto (autogen _) durante la compilazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c626c-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="c626c-164">Tuttavia, quando viene compilato con MSBuild, viene popolata con il numero di versione corretto hello.</span><span class="sxs-lookup"><span data-stu-id="c626c-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="c626c-165">ad esempio la versione di hello tooallow numeri di versione di MSBuild toogenerate, `1.0.*` in AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="c626c-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="c626c-166">Verifica della versione</span><span class="sxs-lookup"><span data-stu-id="c626c-166">Version and release tracking</span></span>
<span data-ttu-id="c626c-167">versione dell'applicazione hello tootrack, assicurarsi che `buildinfo.config` viene generato dal processo di Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="c626c-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="c626c-168">Nel file con estensione csproj, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="c626c-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="c626c-169">Quando si dispone di informazioni di compilazione hello, modulo web di Application Insights hello aggiunge automaticamente **versione dell'applicazione** come elemento proprietà tooevery di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c626c-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="c626c-170">Che consente di toofilter dalla versione quando si eseguono [ricerche diagnostica](app-insights-diagnostic-search.md), o quando si [Esplora metriche](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="c626c-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="c626c-171">Si noti tuttavia che il numero di versione build hello viene generato solo dal hello Microsoft Build Engine, non dallo sviluppatore di hello compilati in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c626c-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="c626c-172">Annotazioni sulle versioni</span><span class="sxs-lookup"><span data-stu-id="c626c-172">Release annotations</span></span>
<span data-ttu-id="c626c-173">Se si utilizza Visual Studio Team Services, è possibile [ottenere un marcatore di annotazione](app-insights-annotations.md) aggiunti tooyour grafici quando si rilascia una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="c626c-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="c626c-174">Hello immagine seguente mostra come viene visualizzato l'indicatore.</span><span class="sxs-lookup"><span data-stu-id="c626c-174">hello following image shows how this marker appears.</span></span>

![Screenshot di annotazione sulla versione di esempio in un grafico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="c626c-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c626c-176">Next steps</span></span>

* [<span data-ttu-id="c626c-177">Risorse condivise da più ruoli</span><span class="sxs-lookup"><span data-stu-id="c626c-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="c626c-178">Creare toodistinguish un inizializzatore di telemetria A | Varianti B</span><span class="sxs-lookup"><span data-stu-id="c626c-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
