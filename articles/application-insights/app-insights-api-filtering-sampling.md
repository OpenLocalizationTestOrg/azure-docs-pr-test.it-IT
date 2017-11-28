---
title: aaaFiltering e pre-elaborazione hello Azure Application Insights SDK | Documenti Microsoft
description: "Scrivere processori di telemetria e gli inizializzatori di telemetria per hello SDK toofilter o aggiungere dati di proprietà toohello prima dell'invio portale Application Insights toohello telemetria hello."
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
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="a35e7-103">Applicazione di filtri e pre-elaborazione di dati di telemetria di Application Insights SDK hello</span><span class="sxs-lookup"><span data-stu-id="a35e7-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="a35e7-104">È possibile scrivere e configurare i plug-in per hello Application Insights SDK toocustomize come dati di telemetria vengono acquisiti ed elaborati prima che venga inviato toohello servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a35e7-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="a35e7-105">[Campionamento](app-insights-sampling.md) riduce volume hello di telemetria senza alterare le statistiche.</span><span class="sxs-lookup"><span data-stu-id="a35e7-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="a35e7-106">Tiene insieme i punti dati correlati per poter passare da uno all'altro quando si diagnostica un problema.</span><span class="sxs-lookup"><span data-stu-id="a35e7-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="a35e7-107">Nel portale di hello nei conteggi totali hello sono toocompensate moltiplicato per il campionamento hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="a35e7-108">Applicazione di filtri con processori di telemetria [per ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) consente di selezionare o modificare i dati di telemetria in hello SDK prima di inviarlo toohello server.</span><span class="sxs-lookup"><span data-stu-id="a35e7-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="a35e7-109">Ad esempio, è possibile ridurre il volume di hello di telemetria escludendo le richieste da robot.</span><span class="sxs-lookup"><span data-stu-id="a35e7-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="a35e7-110">Ma il filtro è un traffico di tooreducing approccio più semplice di campionamento.</span><span class="sxs-lookup"><span data-stu-id="a35e7-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="a35e7-111">Consente un controllo maggiore su ciò che viene trasmesso, ma si dispone di toobe tenere presente che influisce sulle statistiche, ad esempio, se si esclude tutte le richieste riuscite.</span><span class="sxs-lookup"><span data-stu-id="a35e7-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="a35e7-112">[Gli inizializzatori di telemetria aggiungono proprietà](#add-properties) tooany telemetria inviato dall'app, inclusi i dati di telemetria dai moduli standard hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="a35e7-113">Ad esempio, è possibile aggiungere valori calcolati. o i numeri di versione per i dati di hello toofilter nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="a35e7-114">[Hello API SDK](app-insights-api-custom-events-metrics.md) è usato toosend di eventi personalizzati e le metriche.</span><span class="sxs-lookup"><span data-stu-id="a35e7-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="a35e7-115">Prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="a35e7-115">Before you start:</span></span>

* <span data-ttu-id="a35e7-116">Installare hello Application Insights [SDK per ASP.NET](app-insights-asp-net.md) o [SDK per Java](app-insights-java-get-started.md) nell'app.</span><span class="sxs-lookup"><span data-stu-id="a35e7-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="a35e7-117">Filtro: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="a35e7-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="a35e7-118">Questa tecnica consente di controllare più direttamente su ciò che è incluso o escluso dal flusso di dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="a35e7-119">È possibile usarla insieme al campionamento oppure separatamente.</span><span class="sxs-lookup"><span data-stu-id="a35e7-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="a35e7-120">telemetria toofilter, scrivere un processore di dati di telemetria e registrarlo con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a35e7-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="a35e7-121">Tutti i dati di telemetria passa attraverso il processore, ed è possibile scegliere toodrop dalla hello stream o aggiungere proprietà.</span><span class="sxs-lookup"><span data-stu-id="a35e7-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="a35e7-122">Include dati di telemetria dai moduli standard di hello come agente di raccolta richiesta HTTP hello e agente di raccolta dipendenza hello e telemetria che è stato scritto personalmente.</span><span class="sxs-lookup"><span data-stu-id="a35e7-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="a35e7-123">È possibile, ad esempio, filtrare la telemetria sulle richieste dei robot o le chiamate di dipendenza riuscite.</span><span class="sxs-lookup"><span data-stu-id="a35e7-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="a35e7-124">Il filtro di dati di telemetria hello inviati da hello SDK usando processori può distorcere statistiche hello viene visualizzata nel portale di hello e renderlo difficile toofollow elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="a35e7-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="a35e7-125">In alternativa, valutare la possibilità di usare il [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="a35e7-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="a35e7-126">Creare un processore di telemetria (C#)</span><span class="sxs-lookup"><span data-stu-id="a35e7-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="a35e7-127">Verificare che hello Application Insights SDK nel progetto è versione 2.0.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a35e7-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="a35e7-128">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni di Visual Studio e scegliere Gestisci pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="a35e7-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="a35e7-129">In Gestione pacchetti NuGet selezionare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="a35e7-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="a35e7-130">toocreate un filtro, implementare ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="a35e7-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="a35e7-131">un altro punto di estendibilità come il modulo di telemetria, l'inizializzatore di telemetria e il canale di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a35e7-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="a35e7-132">Si noti che i processori di telemetria creano una catena di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a35e7-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="a35e7-133">Quando si crea un'istanza di un processore di dati di telemetria, si passa un processore di collegamento toohello successivo nella catena di hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="a35e7-134">Quando un punto dati di telemetria viene passato a metodo Process toohello, esegue il proprio lavoro e quindi chiama hello processore telemetria successivo nella catena di hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
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
1. <span data-ttu-id="a35e7-135">Inserirlo in ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="a35e7-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="a35e7-136">(Si tratta di hello stessa sezione utilizzato per inizializzare un filtro di campionamento.)</span><span class="sxs-lookup"><span data-stu-id="a35e7-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="a35e7-137">È possibile passare i valori stringa da file con estensione config hello fornendo proprietà denominate pubblica nella classe.</span><span class="sxs-lookup"><span data-stu-id="a35e7-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="a35e7-138">Prestare attenzione toomatch hello nome e tipo tutti i nomi delle proprietà nella classe toohello del file hello. config e i nomi delle proprietà nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="a35e7-139">Se il file con estensione config hello fa riferimento a un tipo inesistente o una proprietà, hello SDK invisibile all'utente non riesca toosend eventuali dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a35e7-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="a35e7-140">**In alternativa,** è possibile inizializzare il filtro hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="a35e7-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="a35e7-141">Inserire il processore in una classe di inizializzazione adatto, ad esempio AppStart in Global.asax.cs - catena hello:</span><span class="sxs-lookup"><span data-stu-id="a35e7-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="a35e7-142">Gli elementi TelemetryClient creati dopo questo punto useranno i processori dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a35e7-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="a35e7-143">Filtri di esempio</span><span class="sxs-lookup"><span data-stu-id="a35e7-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="a35e7-144">Richieste sintetiche</span><span class="sxs-lookup"><span data-stu-id="a35e7-144">Synthetic requests</span></span>
<span data-ttu-id="a35e7-145">Filtrare i robot e i test Web.</span><span class="sxs-lookup"><span data-stu-id="a35e7-145">Filter out bots and web tests.</span></span> <span data-ttu-id="a35e7-146">Sebbene un Esplora metriche hello toofilter opzione out origini sintetiche, questa opzione riduce il traffico di filtrarli in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a35e7-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="a35e7-147">Autenticazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="a35e7-147">Failed authentication</span></span>
<span data-ttu-id="a35e7-148">Filtrare le richieste con una risposta "401".</span><span class="sxs-lookup"><span data-stu-id="a35e7-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="a35e7-149">Filtrare le chiamate di dipendenza remote rapide</span><span class="sxs-lookup"><span data-stu-id="a35e7-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="a35e7-150">Se si desidera solo chiamate toodiagnose che risultano lente, escludere quelli fast hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="a35e7-151">Questo alteri statistiche hello che viene visualizzato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="a35e7-152">grafico delle dipendenze Hello apparirà come se tutti gli errori di chiamate a dipendenze hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="a35e7-153">Diagnosticare i problemi di dipendenza</span><span class="sxs-lookup"><span data-stu-id="a35e7-153">Diagnose dependency issues</span></span>
<span data-ttu-id="a35e7-154">[In questo blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) problemi di un progetto toodiagnose dipendenza inviando automaticamente toodependencies ping regolare.</span><span class="sxs-lookup"><span data-stu-id="a35e7-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="a35e7-155">Aggiungere proprietà: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="a35e7-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="a35e7-156">Utilizzare i dati di telemetria inizializzatori toodefine le proprietà globali che vengono inviate con tutti i dati di telemetria; e il comportamento di toooverride selezionato di moduli standard telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="a35e7-157">Ad esempio, hello Application Insights per il pacchetto Web raccoglie dati di telemetria sulle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="a35e7-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="a35e7-158">per impostazione predefinita, contrassegna come non riuscita qualsiasi richiesta con un codice di risposta > = 400.</span><span class="sxs-lookup"><span data-stu-id="a35e7-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="a35e7-159">Tuttavia se si desidera tootreat 400 come esito positivo, è possibile specificare un inizializzatore di telemetria che imposta proprietà Success hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="a35e7-160">Se viene fornito un inizializzatore di telemetria, viene chiamato ogni volta che uno qualsiasi dei hello Track*() metodi viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="a35e7-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="a35e7-161">Sono inclusi i metodi chiamati dai moduli di telemetria standard hello.</span><span class="sxs-lookup"><span data-stu-id="a35e7-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="a35e7-162">Per convenzione, questi moduli non impostano le proprietà che sono già state impostate da un inizializzatore.</span><span class="sxs-lookup"><span data-stu-id="a35e7-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="a35e7-163">**Definire l'inizializzatore**</span><span class="sxs-lookup"><span data-stu-id="a35e7-163">**Define your initializer**</span></span>

<span data-ttu-id="a35e7-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="a35e7-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
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
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

<span data-ttu-id="a35e7-165">**Caricare l'inizializzatore**</span><span class="sxs-lookup"><span data-stu-id="a35e7-165">**Load your initializer**</span></span>

<span data-ttu-id="a35e7-166">In ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="a35e7-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="a35e7-167">*In alternativa,* è possibile creare un'istanza di inizializzatore hello nel codice, ad esempio in Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="a35e7-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="a35e7-168">Vedere questo esempio nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="a35e7-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="a35e7-169">Inizializzatori di telemetria JavaScript</span><span class="sxs-lookup"><span data-stu-id="a35e7-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="a35e7-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="a35e7-170">*JavaScript*</span></span>

<span data-ttu-id="a35e7-171">Inserire un inizializzatore di telemetria immediatamente dopo il codice di inizializzazione hello che è stato ottenuto dal portale hello:</span><span class="sxs-lookup"><span data-stu-id="a35e7-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="a35e7-172">Per un riepilogo delle proprietà non personalizzata hello disponibile in telemetryItem hello, vedere [modello dati esportazione dell'applicazione Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a35e7-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="a35e7-173">È possibile aggiungere tutti gli inizializzatori desiderati.</span><span class="sxs-lookup"><span data-stu-id="a35e7-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="a35e7-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="a35e7-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="a35e7-175">Qual è la differenza hello tra i processori di telemetria e gli inizializzatori di telemetria?</span><span class="sxs-lookup"><span data-stu-id="a35e7-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="a35e7-176">Esistono alcune sovrapposizioni in operazioni eseguibili con tali: entrambi possono essere utilizzati tooadd tootelemetry di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a35e7-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="a35e7-177">Gli inizializzatori di telemetria vengono sempre eseguiti prima dei processori di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a35e7-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="a35e7-178">TelemetryProcessors consentono toocompletely sostituire o eliminare un elemento di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a35e7-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="a35e7-179">I processori di telemetria non elaborano dati di telemetria dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a35e7-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="a35e7-180">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="a35e7-180">Reference docs</span></span>
* [<span data-ttu-id="a35e7-181">Panoramica API</span><span class="sxs-lookup"><span data-stu-id="a35e7-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="a35e7-182">Riferimento ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a35e7-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="a35e7-183">Codice SDK</span><span class="sxs-lookup"><span data-stu-id="a35e7-183">SDK Code</span></span>
* [<span data-ttu-id="a35e7-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="a35e7-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="a35e7-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="a35e7-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="a35e7-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="a35e7-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="a35e7-187"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a35e7-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="a35e7-188">Ricerca di eventi e log</span><span class="sxs-lookup"><span data-stu-id="a35e7-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a35e7-189">Campionamento</span><span class="sxs-lookup"><span data-stu-id="a35e7-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="a35e7-190">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a35e7-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
