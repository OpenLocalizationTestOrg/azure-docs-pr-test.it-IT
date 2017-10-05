---
title: Filtri e pre-elaborazione in Azure Application Insights SDK | Microsoft Docs
description: "Scrivere processori e inizializzatori di telemetria per l'SDK per filtrare i dati o aggiungere proprietà prima dell'invio della telemetria al portale di Application Insights."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="269e8-103">Filtri e pre-elaborazione della telemetria in Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="269e8-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="269e8-104">È possibile scrivere e configurare plug-in per Application Insights SDK per personalizzare l'acquisizione e l'elaborazione della telemetria prima che venga inviata al servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="269e8-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="269e8-105">[campionamento](app-insights-sampling.md) riduce il volume della telemetria senza effetti sulle statistiche.</span><span class="sxs-lookup"><span data-stu-id="269e8-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="269e8-106">Tiene insieme i punti dati correlati per poter passare da uno all'altro quando si diagnostica un problema.</span><span class="sxs-lookup"><span data-stu-id="269e8-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="269e8-107">Nel portale i conteggi totali vengono moltiplicati per compensare il campionamento.</span><span class="sxs-lookup"><span data-stu-id="269e8-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="269e8-108">L'applicazione di filtri con processori di telemetria [per ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) consente di selezionare o di modificare i dati di telemetria nell'SDK prima che vengano inviati al server.</span><span class="sxs-lookup"><span data-stu-id="269e8-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="269e8-109">È possibile, ad esempio, ridurre il volume della telemetria escludendo le richieste dei robot.</span><span class="sxs-lookup"><span data-stu-id="269e8-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="269e8-110">L'applicazione di filtri è però un approccio di riduzione del traffico più semplice rispetto al campionamento.</span><span class="sxs-lookup"><span data-stu-id="269e8-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="269e8-111">Offre un controllo maggiore su ciò che viene trasmesso, ma è necessario tenere presente che influisce sulle statistiche, ad esempio se si filtrano tutte le richieste riuscite.</span><span class="sxs-lookup"><span data-stu-id="269e8-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="269e8-112">[inizializzatori di telemetria aggiungono proprietà](#add-properties) a tutti i dati di telemetria inviati dall'app, inclusi quelli dei moduli standard.</span><span class="sxs-lookup"><span data-stu-id="269e8-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="269e8-113">È possibile, ad esempio, aggiungere valori calcolati oppure i numeri di versione in base a cui filtrare i dati nel portale.</span><span class="sxs-lookup"><span data-stu-id="269e8-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="269e8-114">[L'API SDK](app-insights-api-custom-events-metrics.md) viene usata per inviare metriche ed eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="269e8-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="269e8-115">Prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="269e8-115">Before you start:</span></span>

* <span data-ttu-id="269e8-116">Installare Application Insights [SDK per ASP.NET](app-insights-asp-net.md) o [SDK per Java](app-insights-java-get-started.md) nell'app.</span><span class="sxs-lookup"><span data-stu-id="269e8-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="269e8-117">Filtro: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="269e8-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="269e8-118">Questa tecnica offre un controllo più diretto su ciò che viene incluso o escluso dal flusso di telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="269e8-119">È possibile usarla insieme al campionamento oppure separatamente.</span><span class="sxs-lookup"><span data-stu-id="269e8-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="269e8-120">Per filtrare la telemetria, scrivere un processore di telemetria e registrarlo con l'SDK.</span><span class="sxs-lookup"><span data-stu-id="269e8-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="269e8-121">Tutta la telemetria passa attraverso il processore ed è possibile scegliere di eliminarla dal flusso o di aggiungere le proprietà.</span><span class="sxs-lookup"><span data-stu-id="269e8-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="269e8-122">È inclusa la telemetria dei moduli standard, ad esempio l'agente di raccolta delle richieste HTTP e l'agente di raccolta delle dipendenze, oltre alla telemetria scritta manualmente.</span><span class="sxs-lookup"><span data-stu-id="269e8-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="269e8-123">È possibile, ad esempio, filtrare la telemetria sulle richieste dei robot o le chiamate di dipendenza riuscite.</span><span class="sxs-lookup"><span data-stu-id="269e8-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="269e8-124">Se si filtra la telemetria inviata dall'SDK usando i processori, le statistiche visualizzate nel portale possono essere alterate e può risultare difficile seguire gli elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="269e8-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="269e8-125">In alternativa, valutare la possibilità di usare il [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="269e8-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="269e8-126">Creare un processore di telemetria (C#)</span><span class="sxs-lookup"><span data-stu-id="269e8-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="269e8-127">Verificare che la versione di Application Insights SDK usata nel progetto sia 2.0.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="269e8-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="269e8-128">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni di Visual Studio e scegliere Gestisci pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="269e8-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="269e8-129">In Gestione pacchetti NuGet selezionare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="269e8-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="269e8-130">Per creare un filtro, implementare ITelemetryProcessor,</span><span class="sxs-lookup"><span data-stu-id="269e8-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="269e8-131">un altro punto di estendibilità come il modulo di telemetria, l'inizializzatore di telemetria e il canale di telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="269e8-132">Si noti che i processori di telemetria creano una catena di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="269e8-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="269e8-133">Quando si crea un'istanza di un processore di telemetria, si passa un collegamento al processore successivo nella catena.</span><span class="sxs-lookup"><span data-stu-id="269e8-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="269e8-134">Quando un punto dati della telemetria viene passato al metodo Process, esegue le operazioni necessarie e quindi chiama il processore di telemetria successivo nella catena.</span><span class="sxs-lookup"><span data-stu-id="269e8-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. <span data-ttu-id="269e8-135">Inserirlo in ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="269e8-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="269e8-136">È la stessa sezione in cui viene inizializzato un filtro di campionamento.</span><span class="sxs-lookup"><span data-stu-id="269e8-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="269e8-137">È possibile passare i valori della stringa dal file .config fornendo proprietà denominate come pubbliche nella classe.</span><span class="sxs-lookup"><span data-stu-id="269e8-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="269e8-138">Prestare attenzione a fare corrispondere il nome del tipo e i nomi delle proprietà nel file. config ai nomi di classe e di proprietà nel codice.</span><span class="sxs-lookup"><span data-stu-id="269e8-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="269e8-139">Se il file. config fa riferimento a un tipo inesistente o una proprietà, l’SDK potrebbe automaticamente non riuscire a inviare nessuna telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="269e8-140">**In alternativa** , è possibile inizializzare il filtro nel codice.</span><span class="sxs-lookup"><span data-stu-id="269e8-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="269e8-141">In una classe di inizializzazione adatta, ad esempio AppStart in Global.asax.cs, inserire il processore nella catena:</span><span class="sxs-lookup"><span data-stu-id="269e8-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="269e8-142">Gli elementi TelemetryClient creati dopo questo punto useranno i processori dell'utente.</span><span class="sxs-lookup"><span data-stu-id="269e8-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="269e8-143">Filtri di esempio</span><span class="sxs-lookup"><span data-stu-id="269e8-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="269e8-144">Richieste sintetiche</span><span class="sxs-lookup"><span data-stu-id="269e8-144">Synthetic requests</span></span>
<span data-ttu-id="269e8-145">Filtrare i robot e i test Web.</span><span class="sxs-lookup"><span data-stu-id="269e8-145">Filter out bots and web tests.</span></span> <span data-ttu-id="269e8-146">Anche se Esplora metriche consente di filtrare le origini sintetiche, questa opzione riduce il traffico filtrandole nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="269e8-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="269e8-147">Autenticazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="269e8-147">Failed authentication</span></span>
<span data-ttu-id="269e8-148">Filtrare le richieste con una risposta "401".</span><span class="sxs-lookup"><span data-stu-id="269e8-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="269e8-149">Filtrare le chiamate di dipendenza remote rapide</span><span class="sxs-lookup"><span data-stu-id="269e8-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="269e8-150">Per diagnosticare solo le chiamate lente, filtrare quelle rapide.</span><span class="sxs-lookup"><span data-stu-id="269e8-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="269e8-151">In questo modo le statistiche visualizzate nel portale verranno modificate.</span><span class="sxs-lookup"><span data-stu-id="269e8-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="269e8-152">Il grafico delle dipendenze apparirà come se tutte le chiamate di dipendenza fossero non riuscite.</span><span class="sxs-lookup"><span data-stu-id="269e8-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="269e8-153">Diagnosticare i problemi di dipendenza</span><span class="sxs-lookup"><span data-stu-id="269e8-153">Diagnose dependency issues</span></span>
<span data-ttu-id="269e8-154">[Questo blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) descrive un progetto per diagnosticare i problemi di dipendenza con l'invio automatico di ping regolari alle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="269e8-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="269e8-155">Aggiungere proprietà: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="269e8-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="269e8-156">Utilizzare gli inizializzatori di telemetria per definire le proprietà globali che vengono inviate con tutti i dati di telemetria; eseguire l'override del comportamento selezionato dei moduli di telemetria standard.</span><span class="sxs-lookup"><span data-stu-id="269e8-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="269e8-157">Ad esempio, il pacchetto Application Insights per il Web raccoglie dati di telemetria relativi alle richieste HTTP e,</span><span class="sxs-lookup"><span data-stu-id="269e8-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="269e8-158">per impostazione predefinita, contrassegna come non riuscita qualsiasi richiesta con un codice di risposta > = 400.</span><span class="sxs-lookup"><span data-stu-id="269e8-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="269e8-159">Tuttavia, se si vuole considerare 400 come un risultato positivo, è possibile fornire un inizializzatore di telemetria che imposti la proprietà Success.</span><span class="sxs-lookup"><span data-stu-id="269e8-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="269e8-160">In tal modo, verrà chiamato ogni volta che viene chiamato il metodo Track*().</span><span class="sxs-lookup"><span data-stu-id="269e8-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="269e8-161">Sono inclusi i metodi chiamati dai moduli di telemetria standard.</span><span class="sxs-lookup"><span data-stu-id="269e8-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="269e8-162">Per convenzione, questi moduli non impostano le proprietà che sono già state impostate da un inizializzatore.</span><span class="sxs-lookup"><span data-stu-id="269e8-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="269e8-163">**Definire l'inizializzatore**</span><span class="sxs-lookup"><span data-stu-id="269e8-163">**Define your initializer**</span></span>

<span data-ttu-id="269e8-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="269e8-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="269e8-165">**Caricare l'inizializzatore**</span><span class="sxs-lookup"><span data-stu-id="269e8-165">**Load your initializer**</span></span>

<span data-ttu-id="269e8-166">In ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="269e8-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="269e8-167">*In alternativa,* è possibile creare un'istanza dell'inizializzatore nel codice, ad esempio nel file Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="269e8-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="269e8-168">Vedere questo esempio nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="269e8-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="269e8-169">Inizializzatori di telemetria JavaScript</span><span class="sxs-lookup"><span data-stu-id="269e8-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="269e8-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="269e8-170">*JavaScript*</span></span>

<span data-ttu-id="269e8-171">Inserire un inizializzatore di telemetria immediatamente dopo il codice di inizializzazione ottenuto dal portale:</span><span class="sxs-lookup"><span data-stu-id="269e8-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="269e8-172">Per un riepilogo delle proprietà non personalizzate disponibili in telemetryItem, vedere [Modello di dati di esportazione di Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="269e8-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="269e8-173">È possibile aggiungere tutti gli inizializzatori desiderati.</span><span class="sxs-lookup"><span data-stu-id="269e8-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="269e8-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="269e8-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="269e8-175">Qual è la differenza tra processori di telemetria e inizializzatori di telemetria?</span><span class="sxs-lookup"><span data-stu-id="269e8-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="269e8-176">Alcune funzioni si sovrappongono: entrambi possono essere usati per aggiungere proprietà a dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="269e8-177">Gli inizializzatori di telemetria vengono sempre eseguiti prima dei processori di telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="269e8-178">I processori di telemetria consentono di sostituire o rimuovere completamente un elemento di telemetria.</span><span class="sxs-lookup"><span data-stu-id="269e8-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="269e8-179">I processori di telemetria non elaborano dati di telemetria dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="269e8-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="269e8-180">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="269e8-180">Reference docs</span></span>
* [<span data-ttu-id="269e8-181">Panoramica API</span><span class="sxs-lookup"><span data-stu-id="269e8-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="269e8-182">Riferimento ASP.NET</span><span class="sxs-lookup"><span data-stu-id="269e8-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="269e8-183">Codice SDK</span><span class="sxs-lookup"><span data-stu-id="269e8-183">SDK Code</span></span>
* [<span data-ttu-id="269e8-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="269e8-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="269e8-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="269e8-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="269e8-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="269e8-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="269e8-187"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="269e8-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="269e8-188">Ricerca di eventi e log</span><span class="sxs-lookup"><span data-stu-id="269e8-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="269e8-189">Campionamento</span><span class="sxs-lookup"><span data-stu-id="269e8-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="269e8-190">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="269e8-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
