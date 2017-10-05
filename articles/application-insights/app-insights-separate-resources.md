---
title: Separazione della telemetria da sviluppo, test e rilascio in Azure Application Insights | Microsoft Docs
description: Telemetria diretta a risorse diverse per indicatori di sviluppo, test e produzione.
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
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="6501d-103">Separazione della telemetria da sviluppo, test e produzione</span><span class="sxs-lookup"><span data-stu-id="6501d-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="6501d-104">Quando si sviluppa la versione successiva di un'applicazione Web, non è desiderabile combinare la telemetria di [Application Insights](app-insights-overview.md) della nuova versione con quella della versione già rilasciata.</span><span class="sxs-lookup"><span data-stu-id="6501d-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="6501d-105">Per evitare confusione, inviare i dati di telemetria da diverse fasi di sviluppo per separare le risorse di Application Insights, con chiavi di strumentazione separate (iKey).</span><span class="sxs-lookup"><span data-stu-id="6501d-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="6501d-106">Per rendere più semplice la modifica della chiave di strumentazione man mano che una versione si sposta da una fase all'altra, può essere utile impostare il valore ikey nel codice anziché nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6501d-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="6501d-107">Se il sistema è un servizio cloud di Azure, è disponibile [un altro metodo di impostazione di valori iKey separati](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="6501d-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="6501d-108">Sulle risorse e le chiavi di strumentazione</span><span class="sxs-lookup"><span data-stu-id="6501d-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="6501d-109">Quando si configura il monitoraggio di Application Insights per l'app Web, viene creata una *risorsa* di Application Insights in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6501d-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="6501d-110">Aprire questa risorsa nel portale di Azure per visualizzare e analizzare i dati di telemetria raccolti dall'app.</span><span class="sxs-lookup"><span data-stu-id="6501d-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="6501d-111">La risorsa viene identificata da una *chiave di strumentazione* (iKey).</span><span class="sxs-lookup"><span data-stu-id="6501d-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="6501d-112">Quando si installa il pacchetto Application Insights per monitorare l'applicazione, questo viene configurato con la chiave di strumentazione, in modo che sappia dove inviare la telemetria.</span><span class="sxs-lookup"><span data-stu-id="6501d-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="6501d-113">In genere si sceglie di usare risorse separate o una singola risorsa condivisa in scenari diversi:</span><span class="sxs-lookup"><span data-stu-id="6501d-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="6501d-114">Diverse applicazioni indipendenti: usare una risorsa separata e l'iKey per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="6501d-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="6501d-115">Più componenti o ruoli di un'applicazione aziendale: usare una [singola risorsa condivisa](app-insights-monitor-multi-role-apps.md) per tutte le applicazioni componente.</span><span class="sxs-lookup"><span data-stu-id="6501d-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="6501d-116">È possibile filtrare o segmentare i dati di telemetria tramite la proprietà cloud_RoleName.</span><span class="sxs-lookup"><span data-stu-id="6501d-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="6501d-117">Sviluppo, test e rilascio: usare una risorsa separata e l'iKey per le versioni del sistema in 'stamp' o in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="6501d-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="6501d-118">Test A | B: usare una singola risorsa.</span><span class="sxs-lookup"><span data-stu-id="6501d-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="6501d-119">Creare un oggetto TelemetryInitializer per aggiungere una proprietà alla telemetria che identifica le varianti.</span><span class="sxs-lookup"><span data-stu-id="6501d-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="6501d-120"><a name="dynamic-ikey"></a> Chiave di strumentazione dinamica</span><span class="sxs-lookup"><span data-stu-id="6501d-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="6501d-121">Per rendere più semplice la modifica del valore ikey man mano che il codice attraversa le fasi di produzione, impostarlo nel codice anziché nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6501d-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="6501d-122">Impostare la chiave in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="6501d-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="6501d-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="6501d-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="6501d-124">In questo esempio i valori ikey per le diverse risorse vengono inseriti in versioni diverse del file di configurazione Web.</span><span class="sxs-lookup"><span data-stu-id="6501d-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="6501d-125">Lo scambio del file di configurazione Web, che è possibile eseguire nell'ambito dello script di rilascio, consente di scambiare la risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6501d-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="6501d-126">Pagina Web</span><span class="sxs-lookup"><span data-stu-id="6501d-126">Web pages</span></span>
<span data-ttu-id="6501d-127">Il valore iKey viene usato anche nelle pagine Web dell'app, nello [script ottenuto dal pannello Avvio rapido](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="6501d-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="6501d-128">Invece di codificarlo letteralmente nello script, generarlo dallo stato del server.</span><span class="sxs-lookup"><span data-stu-id="6501d-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="6501d-129">Ad esempio, in un'app ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="6501d-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="6501d-130">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="6501d-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="6501d-131">Creare risorse di Application Insights aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6501d-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="6501d-132">Per separare i dati di telemetria per componenti diversi dell'applicazione o per indicatori diversi (sviluppo, test o produzione) dello stesso componente, è necessario creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6501d-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="6501d-133">In [portal.azure.com](https://portal.azure.com)aggiungere una nuova risorsa di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="6501d-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="6501d-135">**tipo di applicazione** influisce sul contenuto del pannello Panoramica e sulle proprietà disponibili in [Esplora metriche](app-insights-metrics-explorer.md)di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6501d-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="6501d-136">Se il tipo dell'app non è visualizzato, scegliere uno dei tipi Web per le pagine Web.</span><span class="sxs-lookup"><span data-stu-id="6501d-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="6501d-137">**gruppo di risorse** è utile per gestire le proprietà come il [controllo di accesso](app-insights-resources-roles-access-control.md)di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6501d-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="6501d-138">È possibile usare gruppi di risorse separati per lo sviluppo, i test e la produzione.</span><span class="sxs-lookup"><span data-stu-id="6501d-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="6501d-139">**sottoscrizione** è il proprio account di pagamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="6501d-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="6501d-140">Il **percorso** è la posizione in cui vengono conservati i dati.</span><span class="sxs-lookup"><span data-stu-id="6501d-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="6501d-141">e attualmente non è modificabile.</span><span class="sxs-lookup"><span data-stu-id="6501d-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="6501d-142">**Aggiungi al dashboard** inserisce un riquadro di accesso rapido alla propria risorsa nella pagina iniziale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6501d-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="6501d-143">La creazione della risorsa richiede pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="6501d-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="6501d-144">Al termine della creazione verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="6501d-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="6501d-145">È possibile scrivere uno [script di PowerShell](app-insights-powershell-script-create-resource.md) per creare automaticamente una risorsa.</span><span class="sxs-lookup"><span data-stu-id="6501d-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="6501d-146">Ottenere la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="6501d-146">Getting the instrumentation key</span></span>
<span data-ttu-id="6501d-147">La chiave di strumentazione identifica la risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="6501d-147">The instrumentation key identifies the resource that you created.</span></span> 

![Fare clic su Informazioni di base, quindi sulla chiave di strumentazione e infine premere CTRL+C.](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="6501d-149">Sono necessarie le chiavi di strumentazione di tutte le risorse a cui l'app invierà dati.</span><span class="sxs-lookup"><span data-stu-id="6501d-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="6501d-150">Filtrare in base al numero di build</span><span class="sxs-lookup"><span data-stu-id="6501d-150">Filter on build number</span></span>
<span data-ttu-id="6501d-151">Quando si pubblica una nuova versione dell'app, potrebbe essere opportuno separare i dati telemetrici delle diverse build.</span><span class="sxs-lookup"><span data-stu-id="6501d-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="6501d-152">È possibile impostare la proprietà della versione dell'applicazione in modo che sia possibile filtrare i risultati della [ricerca](app-insights-diagnostic-search.md) e di [Esplora metriche](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6501d-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtro su una proprietà](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="6501d-154">Esistono diversi metodi di impostazione della proprietà della versione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6501d-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="6501d-155">Impostare direttamente:</span><span class="sxs-lookup"><span data-stu-id="6501d-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="6501d-156">Eseguire il wrapping di tale riga in un [inizializzatore di telemetria](app-insights-api-custom-events-metrics.md#defaults) per assicurarsi che tutte le istanze di TelemetryClient siano impostate in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="6501d-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="6501d-157">[ASP.NET] Impostare la versione `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="6501d-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="6501d-158">Il modulo Web selezionerà la versione dal nodo BuildLabel.</span><span class="sxs-lookup"><span data-stu-id="6501d-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="6501d-159">Includere questo file nel progetto e ricordarsi di impostare la proprietà Copia sempre in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="6501d-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

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
* <span data-ttu-id="6501d-160">[ASP.NET] Generare automaticamente BuildInfo.config in MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6501d-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="6501d-161">A tale scopo, aggiungere alcune righe al file `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="6501d-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="6501d-162">Viene generato un file denominato *NomeProgetto*.BuildInfo.config. Il processo di pubblicazione rinomina il file in BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="6501d-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="6501d-163">L'etichetta di compilazione contiene un segnaposto (AutoGen_) se la compilazione viene eseguita in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6501d-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="6501d-164">Se la compilazione viene eseguita con MSBuild, viene inserito il numero di versione corretto.</span><span class="sxs-lookup"><span data-stu-id="6501d-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="6501d-165">Per consentire a MSBuild di generare i numeri di versione, in AssemblyReference.cs impostare la versione come, ad esempio, `1.0.*` .</span><span class="sxs-lookup"><span data-stu-id="6501d-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="6501d-166">Verifica della versione</span><span class="sxs-lookup"><span data-stu-id="6501d-166">Version and release tracking</span></span>
<span data-ttu-id="6501d-167">Per tenere traccia della versione dell'applicazione, assicurarsi che il processo di Microsoft Build Engine generi `buildinfo.config`.</span><span class="sxs-lookup"><span data-stu-id="6501d-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="6501d-168">Nel file con estensione csproj, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="6501d-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="6501d-169">Quando ha le informazioni di compilazione, il modulo Web di Application Insights aggiunge automaticamente la **versione dell'applicazione** come proprietà a ogni elemento dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6501d-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="6501d-170">Questo consente di applicare filtri in base alla versione quando si eseguono [ricerche diagnostiche](app-insights-diagnostic-search.md) o quando si [esaminano le metriche](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6501d-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="6501d-171">Si noti tuttavia che il numero di versione della build viene generato solo da Microsoft Build Engine, non dalla build dello sviluppatore in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6501d-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="6501d-172">Annotazioni sulle versioni</span><span class="sxs-lookup"><span data-stu-id="6501d-172">Release annotations</span></span>
<span data-ttu-id="6501d-173">Se si usa Visual Studio Team Services, è possibile [aggiungere un marcatore di annotazione](app-insights-annotations.md) ai grafici quando si rilascia una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="6501d-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="6501d-174">L'immagine seguente illustra come viene visualizzato il marcatore.</span><span class="sxs-lookup"><span data-stu-id="6501d-174">The following image shows how this marker appears.</span></span>

![Screenshot di annotazione sulla versione di esempio in un grafico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="6501d-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6501d-176">Next steps</span></span>

* [<span data-ttu-id="6501d-177">Risorse condivise da più ruoli</span><span class="sxs-lookup"><span data-stu-id="6501d-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="6501d-178">Creare un inizializzatore di telemetria per distinguere le varianti A|B</span><span class="sxs-lookup"><span data-stu-id="6501d-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
