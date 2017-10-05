---
title: 'Informazioni di riferimento su ApplicationInsights.config: Azure | Documentazione Microsoft'
description: Abilitare o disabilitare i moduli di raccolta dati e aggiungere i contatori delle prestazioni e altri parametri.
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="c144b-103">Configurazione di Application Insights SDK con ApplicationInsights.config o .xml</span><span class="sxs-lookup"><span data-stu-id="c144b-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="c144b-104">Application Insights .NET SDK è costituito da alcuni pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="c144b-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="c144b-105">Il [pacchetto di base](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornisce l'API per l'invio di dati di telemetria ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c144b-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="c144b-106">[Altri pacchetti](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) forniscono *moduli* e *inizializzatori* di telemetria per il rilevamento automatico dei dati di telemetria dall'applicazione e dal rispettivo contesto.</span><span class="sxs-lookup"><span data-stu-id="c144b-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="c144b-107">Modificando il file di configurazione, è possibile abilitare o disabilitare i moduli e gli inizializzatori di telemetria e impostare parametri per alcuni di essi.</span><span class="sxs-lookup"><span data-stu-id="c144b-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="c144b-108">Il file di configurazione è denominato `ApplicationInsights.config` o `ApplicationInsights.xml`, a seconda del tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="c144b-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="c144b-109">Viene aggiunto automaticamente al progetto quando si [installano alcune versioni dell'SDK][start].</span><span class="sxs-lookup"><span data-stu-id="c144b-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="c144b-110">Viene anche aggiunto a un'app Web da [Status Monitor][redfield] in un server IIS o quando si seleziona l'[estensione Application Insights per un sito Web o una macchina virtuale di Azure](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="c144b-111">Non esiste un file equivalente per controllare l'[SDK in una pagina Web][client].</span><span class="sxs-lookup"><span data-stu-id="c144b-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="c144b-112">Questo documento illustra le sezioni visibili nel file di configurazione, il modo in cui esse controllano i componenti SDK, e quali pacchetti NuGet caricano questi componenti.</span><span class="sxs-lookup"><span data-stu-id="c144b-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="c144b-113">Moduli di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c144b-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="c144b-114">Ogni modulo di telemetria raccoglie un tipo specifico di dati e utilizza l’API principale per inviare i dati.</span><span class="sxs-lookup"><span data-stu-id="c144b-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="c144b-115">I moduli sono installati da diversi pacchetti NuGet che aggiungono anche le linee necessarie al file .config.</span><span class="sxs-lookup"><span data-stu-id="c144b-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="c144b-116">Nel file di configurazione è presente un nodo per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="c144b-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="c144b-117">Per disabilitare un modulo, eliminare il nodo o impostarlo come commento.</span><span class="sxs-lookup"><span data-stu-id="c144b-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="c144b-118">Rilevamento delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="c144b-118">Dependency Tracking</span></span>
<span data-ttu-id="c144b-119">[Rilevamento delle dipendenze](app-insights-asp-net-dependencies.md) raccoglie la telemetria delle chiamate effettuate dall’applicazione ai database e ai database e servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="c144b-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="c144b-120">Per far funzionare questo modulo in un server IIS, è necessario [installare Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="c144b-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="c144b-121">Per usarlo nelle app Web o nelle macchine virtuali di Azure, [selezionare l'estensione Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="c144b-122">È anche possibile scrivere codice personalizzato per il rilevamento delle dipendenze mediante l' [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="c144b-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="c144b-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="c144b-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="c144b-124">Agente di raccolta dati delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c144b-124">Performance collector</span></span>
<span data-ttu-id="c144b-125">[Raccoglie contatori delle prestazioni di sistema](app-insights-performance-counters.md) come CPU, memoria e rete caricate dalle istallazioni IIS.</span><span class="sxs-lookup"><span data-stu-id="c144b-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="c144b-126">E’ possibile specificare quali contatori raccogliere, inclusi i contatori delle prestazioni installati.</span><span class="sxs-lookup"><span data-stu-id="c144b-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="c144b-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="c144b-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="c144b-128">Telemetria delle diagnostiche Application Insights</span><span class="sxs-lookup"><span data-stu-id="c144b-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="c144b-129">Il modulo `DiagnosticsTelemetryModule` segnala errori nel codice di strumentazione stesso di Application Insights,</span><span class="sxs-lookup"><span data-stu-id="c144b-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="c144b-130">ad esempio, se il codice non è in grado di accedere ai contatori delle prestazioni o se un `ITelemetryInitializer` genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="c144b-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="c144b-131">La telemetria di traccia rilevata da questo modulo viene visualizzata nella [Ricerca diagnostica][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="c144b-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="c144b-132">Invia i dati di diagnostica a dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="c144b-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="c144b-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="c144b-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="c144b-134">Se si installa questo pacchetto, il file ApplicationInsights.config non viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c144b-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="c144b-135">Modalità di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c144b-135">Developer Mode</span></span>
<span data-ttu-id="c144b-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` impone a `TelemetryChannel` di Application Insights di inviare immediatamente i dati, un elemento di telemetria alla volta, quando un debugger viene collegato al processo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c144b-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="c144b-137">Ciò permette di ridurre la quantità di tempo tra il momento in cui l'applicazione rileva i dati di telemetria e il momento in cui vengono visualizzati nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c144b-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="c144b-138">Questo causa un costo significativo per la CPU e la larghezza di banda di rete.</span><span class="sxs-lookup"><span data-stu-id="c144b-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="c144b-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) </span><span class="sxs-lookup"><span data-stu-id="c144b-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="c144b-140">Rilevamento delle richieste web</span><span class="sxs-lookup"><span data-stu-id="c144b-140">Web Request Tracking</span></span>
<span data-ttu-id="c144b-141">Riporta il [tempo di risposta e il codice dei risultati](app-insights-asp-net.md) delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c144b-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="c144b-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="c144b-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="c144b-143">Rilevamento delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="c144b-143">Exception tracking</span></span>
<span data-ttu-id="c144b-144">`ExceptionTrackingTelemetryModule` rileva le eccezioni non gestite nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="c144b-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="c144b-145">Vedere [Errori ed eccezioni][exceptions].</span><span class="sxs-lookup"><span data-stu-id="c144b-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="c144b-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="c144b-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="c144b-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - rileva le [eccezioni delle attività non notate](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="c144b-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="c144b-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - rileva le eccezioni non gestite per i ruoli di lavoro, servizi windows, e applicazioni della console.</span><span class="sxs-lookup"><span data-stu-id="c144b-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="c144b-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="c144b-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="c144b-150">Rilevamento EventSource</span><span class="sxs-lookup"><span data-stu-id="c144b-150">EventSource Tracking</span></span>
<span data-ttu-id="c144b-151">`EventSourceTelemetryModule` consente di configurare eventi EventSource da inviare ad Application Insights come tracce.</span><span class="sxs-lookup"><span data-stu-id="c144b-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="c144b-152">Per informazioni su eventi EventSource di rilevamento, vedere [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events) (uso degli eventi EventSource).</span><span class="sxs-lookup"><span data-stu-id="c144b-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="c144b-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="c144b-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="c144b-154">Registrazione degli eventi ETW</span><span class="sxs-lookup"><span data-stu-id="c144b-154">ETW Event Tracking</span></span>
<span data-ttu-id="c144b-155">`EtwCollectorTelemetryModule` consente di configurare gli eventi dai provider ETW da inviare ad Application Insights come tracce.</span><span class="sxs-lookup"><span data-stu-id="c144b-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="c144b-156">Per informazioni sul rilevamento di eventi ETW, vedere [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events) (Uso di eventi ETW).</span><span class="sxs-lookup"><span data-stu-id="c144b-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="c144b-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="c144b-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="c144b-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="c144b-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="c144b-159">Il pacchetto Microsoft.ApplicationInsights include l' [API principale](https://msdn.microsoft.com/library/mt420197.aspx) dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="c144b-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="c144b-160">Gli altri moduli di telemetria utilizzano questo pacchetto, ed è possibile anche [utilizzarlo per definire la propria telemetria](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="c144b-161">Non ci sono voci in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="c144b-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="c144b-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="c144b-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="c144b-163">Se si installa questo NuGet, non viene generato nessun file .config.</span><span class="sxs-lookup"><span data-stu-id="c144b-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="c144b-164">Canale di telemetria</span><span class="sxs-lookup"><span data-stu-id="c144b-164">Telemetry Channel</span></span>
<span data-ttu-id="c144b-165">Il canale di telemetria gestisce i buffering e la trasmissione della telemetria al servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c144b-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="c144b-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` è il canale predefinito per i servizi.</span><span class="sxs-lookup"><span data-stu-id="c144b-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="c144b-167">Esegue il buffering dei dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="c144b-167">It buffers data in memory.</span></span>
* <span data-ttu-id="c144b-168">`Microsoft.ApplicationInsights.PersistenceChannel` è un’alternativa per le applicazioni della console.</span><span class="sxs-lookup"><span data-stu-id="c144b-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="c144b-169">Esso può salvare qualsiasi dato unflushed nell’archivio permanente quando si arresta l’applicazione, e lo invia quando la si riapre.</span><span class="sxs-lookup"><span data-stu-id="c144b-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="c144b-170">Inizializzatori di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c144b-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="c144b-171">Gli inizializzatori di telemetria impostano proprietà di contesto che vengono inviate insieme ad ogni elemento di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c144b-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="c144b-172">E’ possibile [scrivere i propri inizializzatori](app-insights-api-filtering-sampling.md#add-properties) per impostare proprietà di contesto.</span><span class="sxs-lookup"><span data-stu-id="c144b-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="c144b-173">Gli inizializzatori standard sono tutti impostati dal Web o dai pacchetti NuGet WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="c144b-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="c144b-174">`AccountIdTelemetryInitializer` imposta la proprietà AccountId.</span><span class="sxs-lookup"><span data-stu-id="c144b-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="c144b-175">`AuthenticatedUserIdTelemetryInitializer` imposta la proprietà AuthenticatedUserId come impostata dal SDK di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c144b-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="c144b-176">`AzureRoleEnvironmentTelemetryInitializer` aggiorna le proprietà `RoleName` e `RoleInstance` del contesto `Device` per tutti gli elementi di telemetria con le informazioni estratte dall'ambiente di runtime di Azure.</span><span class="sxs-lookup"><span data-stu-id="c144b-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="c144b-177">`BuildInfoConfigComponentVersionTelemetryInitializer` aggiorna la proprietà `Version` del contesto `Component` per tutti gli elementi di telemetria con il valore estratto dal file `BuildInfo.config` prodotto dalla compilazione MS.</span><span class="sxs-lookup"><span data-stu-id="c144b-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="c144b-178">`ClientIpHeaderTelemetryInitializer` aggiorna le proprietà `Ip` del contesto `Location` di tutti gli elementi di telemetria in base all'intestazione HTTP `X-Forwarded-For` della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c144b-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="c144b-179">`DeviceTelemetryInitializer` aggiorna le proprietà seguenti del contesto `Device` per tutti gli elementi di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c144b-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="c144b-180">`Type` viene impostato su "PC".</span><span class="sxs-lookup"><span data-stu-id="c144b-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="c144b-181">`Id` viene impostato sul nome di dominio del computer in cui è in esecuzione l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="c144b-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="c144b-182">`OemName` è impostato sul valore estratto dal campo `Win32_ComputerSystem.Manufacturer` mediante WMI.</span><span class="sxs-lookup"><span data-stu-id="c144b-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="c144b-183">`Model` è impostato sul valore estratto dal campo `Win32_ComputerSystem.Model` mediante WMI.</span><span class="sxs-lookup"><span data-stu-id="c144b-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="c144b-184">`NetworkType` è impostato sul valore estratto da `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="c144b-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="c144b-185">`Language` è impostato sul nome di `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="c144b-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="c144b-186">`DomainNameRoleInstanceTelemetryInitializer` aggiorna la proprietà `RoleInstance` del contesto `Device` per tutti gli elementi di telemetria con il nome di dominio del computer in cui è in esecuzione l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="c144b-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="c144b-187">`OperationNameTelemetryInitializer` aggiorna la proprietà `Name` di `RequestTelemetry` e la proprietà `Name` del contesto `Operation` di tutti gli elementi di telemetria in base al metodo HTTP, oltre ai nomi del controller MVC ASP.NET e all'azione richiamata per elaborare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="c144b-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="c144b-188">`OperationIdTelemetryInitializer` o `OperationCorrelationTelemetryInitializer` aggiorna la proprietà di contesto `Operation.Id` di tutti gli elementi di telemetria rilevati durante la gestione di una richiesta con il `RequestTelemetry.Id` generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c144b-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="c144b-189">`SessionTelemetryInitializer` aggiorna la proprietà `Id` del contesto `Session` per tutti gli elementi di telemetria con il valore estratto dal cookie `ai_session` generato dal codice di strumentazione JavaScript di Application Insights in esecuzione nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c144b-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="c144b-190">`SyntheticTelemetryInitializer` o `SyntheticUserAgentTelemetryInitializer` aggiorna le proprietà di contesto `User`, `Session` e `Operation` di tutti gli elementi di telemetria rilevati durante la gestione di una richiesta da un'origine sintetica, ad esempio un test di disponibilità o un robot del motore di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c144b-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="c144b-191">Per impostazione predefinita, [Esplora metriche](app-insights-metrics-explorer.md) non mostra la telemetria sintetica.</span><span class="sxs-lookup"><span data-stu-id="c144b-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="c144b-192">`<Filters>` imposta le proprietà di identificazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="c144b-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="c144b-193">`UserAgentTelemetryInitializer` aggiorna la proprietà `UserAgent` del contesto `User` di tutti gli elementi di telemetria in base all'intestazione HTTP `User-Agent` della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c144b-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="c144b-194">`UserTelemetryInitializer` aggiorna le proprietà `Id` e `AcquisitionDate` del contesto `User` per tutti gli elementi di telemetria con i valori estratti dal cookie `ai_user` generato dal codice di strumentazione JavaScript di Application Insights in esecuzione nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c144b-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="c144b-195">`WebTestTelemetryInitializer` imposta l'id utente, l'id di sessione e le proprietà di origine sintetica per le richieste HTTP che provengono da [test di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="c144b-196">`<Filters>` imposta le proprietà di identificazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="c144b-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="c144b-197">Per le applicazioni .NET in esecuzione in Service Fabric, è possibile includere il pacchetto NuGet `Microsoft.ApplicationInsights.ServiceFabric`.</span><span class="sxs-lookup"><span data-stu-id="c144b-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="c144b-198">Questo pacchetto include `FabricTelemetryInitializer`, che aggiunge le proprietà di Service Fabric per gli elementi di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c144b-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="c144b-199">Per ulteriori informazioni, vedere la [pagina GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sulle proprietà aggiunte dal pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="c144b-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="c144b-200">Processori di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c144b-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="c144b-201">I processori di telemetria possono filtrare e modificare ciascun elemento di telemetria prima di inviarlo dal SDK al portale.</span><span class="sxs-lookup"><span data-stu-id="c144b-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="c144b-202">E’ possibile [scrivere i propri processori di telemetria](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="c144b-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="c144b-203">Processore di telemetria di campionamento adattivo (da 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="c144b-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="c144b-204">Questa opzione è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c144b-204">This is enabled by default.</span></span> <span data-ttu-id="c144b-205">Se l'app invia molti dati di telemetria, questo processore rimuove alcune di esse.</span><span class="sxs-lookup"><span data-stu-id="c144b-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="c144b-206">Il parametro fornisce la destinazione che l'algoritmo tenta di ottenere.</span><span class="sxs-lookup"><span data-stu-id="c144b-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="c144b-207">Ogni istanza di SDK funziona in modo indipendente, pertanto se il server è un cluster di più computer, il volume dei dati di telemetria verrà di conseguenza moltiplicato.</span><span class="sxs-lookup"><span data-stu-id="c144b-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="c144b-208">[Altre informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="c144b-209">Processore di telemetria di campionamento adattivo (da 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="c144b-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="c144b-210">È inoltre disponibile un [processore di telemetria di campionamento](app-insights-api-filtering-sampling.md) standard (da 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="c144b-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="c144b-211">Parametri del canale (Java)</span><span class="sxs-lookup"><span data-stu-id="c144b-211">Channel parameters (Java)</span></span>
<span data-ttu-id="c144b-212">Questi parametri influiscono sul modo in cui l'SDK per Java deve archiviare e scaricare i dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="c144b-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="c144b-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="c144b-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="c144b-214">Indica il numero di elementi di telemetria che possono essere archiviati nella risorsa di archiviazione in memoria dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="c144b-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="c144b-215">Quando viene raggiunto questo numero, il buffer di telemetria viene scaricato, ovvero gli elementi di telemetria vengono inviati al server Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c144b-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="c144b-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c144b-216">Min: 1</span></span>
* <span data-ttu-id="c144b-217">Max: 1000</span><span class="sxs-lookup"><span data-stu-id="c144b-217">Max: 1000</span></span>
* <span data-ttu-id="c144b-218">Valore predefinito: 500</span><span class="sxs-lookup"><span data-stu-id="c144b-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="c144b-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="c144b-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="c144b-220">Determina la frequenza con cui vengono scaricati (inviati ad Application Insights) i dati nella risorsa di archiviazione in memoria.</span><span class="sxs-lookup"><span data-stu-id="c144b-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="c144b-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c144b-221">Min: 1</span></span>
* <span data-ttu-id="c144b-222">Max: 300</span><span class="sxs-lookup"><span data-stu-id="c144b-222">Max: 300</span></span>
* <span data-ttu-id="c144b-223">Valore predefinito: 5</span><span class="sxs-lookup"><span data-stu-id="c144b-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="c144b-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="c144b-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="c144b-225">Determina le dimensioni massime in MB assegnate all'archivio permanente sul disco locale.</span><span class="sxs-lookup"><span data-stu-id="c144b-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="c144b-226">Questo archivio viene usato per archiviare in modo permanente gli elementi di telemetria che non sono stati trasmessi all'endpoint di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c144b-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="c144b-227">Quando vengono raggiunte le dimensioni di archiviazione, i nuovi elementi di telemetria verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="c144b-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="c144b-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c144b-228">Min: 1</span></span>
* <span data-ttu-id="c144b-229">Max: 100</span><span class="sxs-lookup"><span data-stu-id="c144b-229">Max: 100</span></span>
* <span data-ttu-id="c144b-230">Valore predefinito: 10</span><span class="sxs-lookup"><span data-stu-id="c144b-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="c144b-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="c144b-231">InstrumentationKey</span></span>
<span data-ttu-id="c144b-232">Determina la risorsa di Application Insights in cui vengono visualizzati i dati.</span><span class="sxs-lookup"><span data-stu-id="c144b-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="c144b-233">In genere, viene creata una risorsa separata, con una chiave separata, per ognuna delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c144b-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="c144b-234">Se si vuole impostare la chiave in modo dinamico, ad esempio se si intende inviare i risultati dall'applicazione a diverse risorse, è possibile omettere la chiave dal file di configurazione e impostarla nel codice.</span><span class="sxs-lookup"><span data-stu-id="c144b-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="c144b-235">Per impostare la chiave per tutte le istanze di TelemetryClient, inclusi i moduli di telemetria standard, impostare la chiave in TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="c144b-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="c144b-236">Eseguire questa operazione in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c144b-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="c144b-237">Se si vuole inviare un set specifico di eventi a una risorsa diversa, è possibile impostare la chiave per un oggetto TelemetryClient specifico:</span><span class="sxs-lookup"><span data-stu-id="c144b-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="c144b-238">Per ottenere una nuova chiave, [creare una nuova risorsa nel portale di Application Insights][new].</span><span class="sxs-lookup"><span data-stu-id="c144b-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c144b-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c144b-239">Next steps</span></span>
<span data-ttu-id="c144b-240">[Altre informazioni sull'API][api].</span><span class="sxs-lookup"><span data-stu-id="c144b-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
