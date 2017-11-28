---
title: riferimento aaaApplicationInsights.config - Azure | Documenti Microsoft
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
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="c310a-103">Configurazione di Application Insights SDK hello con Applicationinsights o. Xml</span><span class="sxs-lookup"><span data-stu-id="c310a-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="c310a-104">Hello Application Insights .NET SDK è costituito da un numero di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="c310a-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="c310a-105">Il [pacchetto core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornisce hello API per l'invio di dati di telemetria relativi a messaggi hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c310a-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="c310a-106">[Altri pacchetti](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) forniscono *moduli* e *inizializzatori* di telemetria per il rilevamento automatico dei dati di telemetria dall'applicazione e dal rispettivo contesto.</span><span class="sxs-lookup"><span data-stu-id="c310a-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="c310a-107">Modificando il file di configurazione di hello, è possibile abilitare o disabilitare inizializzatori e i moduli di telemetria e impostare i parametri per alcune di esse.</span><span class="sxs-lookup"><span data-stu-id="c310a-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="c310a-108">file di configurazione Hello `ApplicationInsights.config` o `ApplicationInsights.xml`, a seconda del tipo di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c310a-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="c310a-109">Viene aggiunta automaticamente tooyour progetto quando si [installare la maggior parte delle versioni di hello SDK][start].</span><span class="sxs-lookup"><span data-stu-id="c310a-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="c310a-110">Viene inoltre aggiunto app web tooa da [Status Monitor in un server IIS][redfield], o quando si seleziona hello termini Insights [estensione per una macchina virtuale o un sito Web di Azure](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c310a-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="c310a-111">Non è un hello toocontrol file equivalente [SDK in una pagina web][client].</span><span class="sxs-lookup"><span data-stu-id="c310a-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="c310a-112">Questo documento descrive le sezioni di hello che vedere nella configurazione di hello, file, come controllano componenti hello del SDK, hello e i pacchetti NuGet caricare tali componenti.</span><span class="sxs-lookup"><span data-stu-id="c310a-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="c310a-113">Moduli di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c310a-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="c310a-114">Ogni modulo di telemetria raccoglie un tipo specifico di dati e le Usa core hello dati hello toosend di API.</span><span class="sxs-lookup"><span data-stu-id="c310a-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="c310a-115">i moduli di Hello vengono installati per diversi pacchetti NuGet, aggiungere anche i file con estensione config toohello hello righe richieste.</span><span class="sxs-lookup"><span data-stu-id="c310a-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="c310a-116">È presente un nodo nel file di configurazione hello per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="c310a-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="c310a-117">un modulo, toodisable Elimina nodo hello o impostarlo come commento.</span><span class="sxs-lookup"><span data-stu-id="c310a-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="c310a-118">Rilevamento delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="c310a-118">Dependency Tracking</span></span>
<span data-ttu-id="c310a-119">[Rilevamento delle dipendenze](app-insights-asp-net-dependencies.md) raccoglie dati di telemetria sulle chiamate l'app invia toodatabases e i servizi esterni e database.</span><span class="sxs-lookup"><span data-stu-id="c310a-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="c310a-120">tooallow toowork questo modulo in un server IIS, è necessario troppo[installa Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="c310a-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="c310a-121">toouse in App web di Azure o le macchine virtuali, [selezionare l'estensione Application Insights hello](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c310a-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="c310a-122">È anche possibile scrivere la propria dipendenza rilevamento codice utilizzando hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="c310a-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="c310a-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="c310a-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="c310a-124">Agente di raccolta dati delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c310a-124">Performance collector</span></span>
<span data-ttu-id="c310a-125">[Raccoglie contatori delle prestazioni di sistema](app-insights-performance-counters.md) come CPU, memoria e rete caricate dalle istallazioni IIS.</span><span class="sxs-lookup"><span data-stu-id="c310a-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="c310a-126">È possibile specificare quali toocollect contatori, inclusi i contatori delle prestazioni che è stato configurato manualmente.</span><span class="sxs-lookup"><span data-stu-id="c310a-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="c310a-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="c310a-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="c310a-128">Telemetria delle diagnostiche Application Insights</span><span class="sxs-lookup"><span data-stu-id="c310a-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="c310a-129">Hello `DiagnosticsTelemetryModule` segnala gli errori nel codice di strumentazione di Application Insights stesso hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="c310a-130">Ad esempio, se i contatori delle prestazioni non è possibile accedere a codice hello o un `ITelemetryInitializer` genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="c310a-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="c310a-131">Dati di telemetria di traccia rilevati da questo modulo viene visualizzata in hello [ricerca diagnostica][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="c310a-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="c310a-132">Invia dati di diagnostica toodc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="c310a-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="c310a-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="c310a-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="c310a-134">Se si installa solo questo pacchetto, il file Applicationinsights config hello non viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c310a-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="c310a-135">Modalità di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c310a-135">Developer Mode</span></span>
<span data-ttu-id="c310a-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`forza hello Application Insights `TelemetryChannel` toosend dati immediatamente, elemento dati di uno telemetria alla volta, quando un debugger è collegato toohello processo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c310a-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="c310a-137">Questo riduce hello periodo di tempo tra il momento di hello quando l'applicazione tiene traccia di telemetria e quando viene visualizzato nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="c310a-138">Questo causa un costo significativo per la CPU e la larghezza di banda di rete.</span><span class="sxs-lookup"><span data-stu-id="c310a-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="c310a-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)</span><span class="sxs-lookup"><span data-stu-id="c310a-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="c310a-140">Rilevamento delle richieste web</span><span class="sxs-lookup"><span data-stu-id="c310a-140">Web Request Tracking</span></span>
<span data-ttu-id="c310a-141">Hello report [codice di tempo e il risultato della risposta](app-insights-asp-net.md) di richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c310a-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="c310a-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="c310a-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="c310a-143">Rilevamento delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="c310a-143">Exception tracking</span></span>
<span data-ttu-id="c310a-144">`ExceptionTrackingTelemetryModule` rileva le eccezioni non gestite nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="c310a-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="c310a-145">Vedere [Errori ed eccezioni][exceptions].</span><span class="sxs-lookup"><span data-stu-id="c310a-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="c310a-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="c310a-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="c310a-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - rileva le [eccezioni delle attività non notate](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="c310a-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="c310a-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - rileva le eccezioni non gestite per i ruoli di lavoro, servizi windows, e applicazioni della console.</span><span class="sxs-lookup"><span data-stu-id="c310a-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="c310a-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="c310a-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="c310a-150">Rilevamento EventSource</span><span class="sxs-lookup"><span data-stu-id="c310a-150">EventSource Tracking</span></span>
<span data-ttu-id="c310a-151">`EventSourceTelemetryModule`Consente di tooconfigure toobe eventi EventSource inviato tooApplication informazioni come le tracce.</span><span class="sxs-lookup"><span data-stu-id="c310a-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="c310a-152">Per informazioni su eventi EventSource di rilevamento, vedere [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events) (uso degli eventi EventSource).</span><span class="sxs-lookup"><span data-stu-id="c310a-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="c310a-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="c310a-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="c310a-154">Registrazione degli eventi ETW</span><span class="sxs-lookup"><span data-stu-id="c310a-154">ETW Event Tracking</span></span>
<span data-ttu-id="c310a-155">`EtwCollectorTelemetryModule`consente eventi tooconfigure toobe provider ETW inviato tooApplication informazioni come le tracce.</span><span class="sxs-lookup"><span data-stu-id="c310a-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="c310a-156">Per informazioni sul rilevamento di eventi ETW, vedere [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events) (Uso di eventi ETW).</span><span class="sxs-lookup"><span data-stu-id="c310a-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="c310a-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="c310a-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="c310a-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="c310a-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="c310a-159">pacchetto di Microsoft. applicationinsights Hello fornisce hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c310a-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="c310a-160">è anche possibile e Hello altri moduli di telemetria utilizzano questo [usarlo toodefine propria telemetria](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c310a-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="c310a-161">Non ci sono voci in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="c310a-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="c310a-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="c310a-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="c310a-163">Se si installa questo NuGet, non viene generato nessun file .config.</span><span class="sxs-lookup"><span data-stu-id="c310a-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="c310a-164">Canale di telemetria</span><span class="sxs-lookup"><span data-stu-id="c310a-164">Telemetry Channel</span></span>
<span data-ttu-id="c310a-165">canale dati di telemetria Hello gestisce il buffer e la trasmissione di dati di telemetria toohello servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c310a-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="c310a-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`è il canale predefinito hello per i servizi.</span><span class="sxs-lookup"><span data-stu-id="c310a-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="c310a-167">Esegue il buffering dei dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="c310a-167">It buffers data in memory.</span></span>
* <span data-ttu-id="c310a-168">`Microsoft.ApplicationInsights.PersistenceChannel` è un’alternativa per le applicazioni della console.</span><span class="sxs-lookup"><span data-stu-id="c310a-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="c310a-169">Consente di risparmiare spazio di archiviazione toopersistent unflushed dati quando si chiude l'app e verrà inviato quando l'applicazione hello viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="c310a-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="c310a-170">Inizializzatori di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c310a-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="c310a-171">Gli inizializzatori di telemetria impostano proprietà di contesto che vengono inviate insieme ad ogni elemento di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c310a-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="c310a-172">È possibile [scrivere il propria inizializzatori](app-insights-api-filtering-sampling.md#add-properties) tooset le proprietà di contesto.</span><span class="sxs-lookup"><span data-stu-id="c310a-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="c310a-173">gli inizializzatori di Hello standard sono impostati tramite hello Web o WindowsServer NuGet pacchetti:</span><span class="sxs-lookup"><span data-stu-id="c310a-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="c310a-174">`AccountIdTelemetryInitializer`Imposta proprietà AccountId hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="c310a-175">`AuthenticatedUserIdTelemetryInitializer`Imposta proprietà AuthenticatedUserId hello come set da hello SDK per JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c310a-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="c310a-176">`AzureRoleEnvironmentTelemetryInitializer`hello aggiornamenti `RoleName` e `RoleInstance` le proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria con le informazioni estratte dall'ambiente di runtime di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="c310a-177">`BuildInfoConfigComponentVersionTelemetryInitializer`hello aggiornamenti `Version` proprietà di hello `Component` contesto per tutti gli elementi di dati di telemetria con valore hello estratto dalla hello `BuildInfo.config` file prodotto da Microsoft Build.</span><span class="sxs-lookup"><span data-stu-id="c310a-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="c310a-178">`ClientIpHeaderTelemetryInitializer`aggiornamenti `Ip` proprietà di hello `Location` basata sul contesto di tutti gli elementi di dati di telemetria su hello `X-Forwarded-For` intestazione HTTP della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="c310a-179">`DeviceTelemetryInitializer`hello gli aggiornamenti seguenti proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c310a-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="c310a-180">`Type`è stato impostato troppo "PC"</span><span class="sxs-lookup"><span data-stu-id="c310a-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="c310a-181">`Id`è impostato toohello nome di dominio hello computer in cui è in esecuzione un'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="c310a-182">`OemName`è impostato un valore toohello estratto da hello `Win32_ComputerSystem.Manufacturer` campo tramite WMI.</span><span class="sxs-lookup"><span data-stu-id="c310a-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="c310a-183">`Model`è impostato un valore toohello estratto da hello `Win32_ComputerSystem.Model` campo tramite WMI.</span><span class="sxs-lookup"><span data-stu-id="c310a-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="c310a-184">`NetworkType`è impostato un valore toohello estratto da hello `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="c310a-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="c310a-185">`Language`è impostato il nome toohello di hello `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="c310a-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="c310a-186">`DomainNameRoleInstanceTelemetryInitializer`hello aggiornamenti `RoleInstance` proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria con il nome di dominio di hello del computer hello in cui è in esecuzione un'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="c310a-187">`OperationNameTelemetryInitializer`hello aggiornamenti `Name` proprietà di hello `RequestTelemetry` hello e `Name` proprietà di hello `Operation` basata sul contesto di tutti gli elementi di dati di telemetria nel metodo hello HTTP, nonché i nomi di hello tooprocess richiamato azione e del controller di ASP.NET MVC richiesta.</span><span class="sxs-lookup"><span data-stu-id="c310a-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="c310a-188">`OperationIdTelemetryInitializer`o `OperationCorrelationTelemetryInitializer` hello aggiornamenti `Operation.Id` proprietà di contesto di tutti gli elementi di dati di telemetria rilevati durante la gestione di una richiesta con hello generato automaticamente `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="c310a-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="c310a-189">`SessionTelemetryInitializer`hello aggiornamenti `Id` proprietà di hello `Session` contesto per tutti gli elementi di dati di telemetria con valore estratto dalla hello `ai_session` cookie generati da hello codice strumentazione ApplicationInsights JavaScript in esecuzione nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="c310a-190">`SyntheticTelemetryInitializer`o `SyntheticUserAgentTelemetryInitializer` hello aggiornamenti `User`, `Session` e `Operation` proprietà di contesti di tutti gli elementi di dati di telemetria rilevate quando si gestisce una richiesta da un'origine sintetica, ad esempio una disponibilità test o un bot motore di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c310a-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="c310a-191">Per impostazione predefinita, [Esplora metriche](app-insights-metrics-explorer.md) non mostra la telemetria sintetica.</span><span class="sxs-lookup"><span data-stu-id="c310a-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="c310a-192">Hello `<Filters>` impostare proprietà delle richieste di hello di identificazione.</span><span class="sxs-lookup"><span data-stu-id="c310a-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="c310a-193">`UserAgentTelemetryInitializer`hello aggiornamenti `UserAgent` proprietà di hello `User` basata sul contesto di tutti gli elementi di dati di telemetria su hello `User-Agent` intestazione HTTP della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="c310a-194">`UserTelemetryInitializer`hello aggiornamenti `Id` e `AcquisitionDate` le proprietà di `User` contesto per tutti gli elementi di dati di telemetria con i valori estratti da hello `ai_user` cookie generati dal codice di strumentazione di Application Insights JavaScript hello in esecuzione in hello browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c310a-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="c310a-195">`WebTestTelemetryInitializer`set di hello user id, id di sessione e le proprietà dell'origine sintetiche per HTTP richieste che provengono da [disponibilità test](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="c310a-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="c310a-196">Hello `<Filters>` impostare proprietà delle richieste di hello di identificazione.</span><span class="sxs-lookup"><span data-stu-id="c310a-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="c310a-197">Per le applicazioni .NET in esecuzione nell'infrastruttura del servizio, è possibile includere hello `Microsoft.ApplicationInsights.ServiceFabric` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="c310a-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="c310a-198">Il pacchetto include un `FabricTelemetryInitializer`, che aggiunge gli elementi tootelemetry di proprietà di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c310a-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="c310a-199">Per ulteriori informazioni, vedere hello [pagina GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sulle proprietà hello aggiunte dal pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="c310a-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="c310a-200">Processori di telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c310a-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="c310a-201">Processori di telemetria è possono filtrare e modificare ogni elemento di dati di telemetria appena prima che venga inviata dal portale di toohello hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c310a-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="c310a-202">E’ possibile [scrivere i propri processori di telemetria](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="c310a-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="c310a-203">Processore di telemetria di campionamento adattivo (da 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="c310a-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="c310a-204">Questa opzione è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c310a-204">This is enabled by default.</span></span> <span data-ttu-id="c310a-205">Se l'app invia molti dati di telemetria, questo processore rimuove alcune di esse.</span><span class="sxs-lookup"><span data-stu-id="c310a-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="c310a-206">il parametro Hello fornisce destinazione hello hello algoritmo tenta tooachieve.</span><span class="sxs-lookup"><span data-stu-id="c310a-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="c310a-207">Ogni istanza di hello SDK funziona in modo indipendente, quindi se il server è un cluster di più computer, volume hello dei dati di telemetria verrà moltiplicati conseguenza.</span><span class="sxs-lookup"><span data-stu-id="c310a-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="c310a-208">[Altre informazioni sul campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c310a-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="c310a-209">Processore di telemetria di campionamento adattivo (da 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="c310a-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="c310a-210">È inoltre disponibile un [processore di telemetria di campionamento](app-insights-api-filtering-sampling.md) standard (da 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="c310a-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="c310a-211">Parametri del canale (Java)</span><span class="sxs-lookup"><span data-stu-id="c310a-211">Channel parameters (Java)</span></span>
<span data-ttu-id="c310a-212">Questi parametri influiscono sulle modalità hello SDK per Java deve archiviare e scaricare i dati di telemetria hello da esso raccolti.</span><span class="sxs-lookup"><span data-stu-id="c310a-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="c310a-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="c310a-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="c310a-214">numero di Hello di elementi di dati di telemetria che possono essere archiviati in archiviazione in memoria hello del SDK.</span><span class="sxs-lookup"><span data-stu-id="c310a-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="c310a-215">Quando viene raggiunto il numero, viene svuotato il buffer di dati di telemetria hello:, ovvero gli elementi di dati di telemetria hello vengono inviati i server di Application Insights toohello.</span><span class="sxs-lookup"><span data-stu-id="c310a-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="c310a-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c310a-216">Min: 1</span></span>
* <span data-ttu-id="c310a-217">Max: 1000</span><span class="sxs-lookup"><span data-stu-id="c310a-217">Max: 1000</span></span>
* <span data-ttu-id="c310a-218">Valore predefinito: 500</span><span class="sxs-lookup"><span data-stu-id="c310a-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="c310a-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="c310a-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="c310a-220">Determina la frequenza con cui hello dati archiviati nel servizio di archiviazione in memoria hello devono essere scaricato (inviato tooApplication Insights).</span><span class="sxs-lookup"><span data-stu-id="c310a-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="c310a-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c310a-221">Min: 1</span></span>
* <span data-ttu-id="c310a-222">Max: 300</span><span class="sxs-lookup"><span data-stu-id="c310a-222">Max: 300</span></span>
* <span data-ttu-id="c310a-223">Valore predefinito: 5</span><span class="sxs-lookup"><span data-stu-id="c310a-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="c310a-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="c310a-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="c310a-225">Determina hello la dimensione massima in MB assegnato toohello nell'archivio permanente sul disco locale hello.</span><span class="sxs-lookup"><span data-stu-id="c310a-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="c310a-226">Questa risorsa di archiviazione viene utilizzato per salvare in modo permanente gli elementi di telemetria non è stato possibile toobe trasmesso toohello Application Insights endpoint.</span><span class="sxs-lookup"><span data-stu-id="c310a-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="c310a-227">Quando sono stato raggiunto dimensioni di archiviazione hello, nuovi elementi di dati di telemetria verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="c310a-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="c310a-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="c310a-228">Min: 1</span></span>
* <span data-ttu-id="c310a-229">Max: 100</span><span class="sxs-lookup"><span data-stu-id="c310a-229">Max: 100</span></span>
* <span data-ttu-id="c310a-230">Valore predefinito: 10</span><span class="sxs-lookup"><span data-stu-id="c310a-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="c310a-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="c310a-231">InstrumentationKey</span></span>
<span data-ttu-id="c310a-232">Ciò determina la risorsa di Application Insights hello in cui i dati verranno visualizzati.</span><span class="sxs-lookup"><span data-stu-id="c310a-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="c310a-233">In genere, viene creata una risorsa separata, con una chiave separata, per ognuna delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c310a-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="c310a-234">Se si desidera chiave hello tooset in modo dinamico, ad esempio se si desidera che i risultati di toosend dalle risorse dell'applicazione - toodifferent omettere chiave hello dal file di configurazione hello e impostarlo nel codice.</span><span class="sxs-lookup"><span data-stu-id="c310a-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="c310a-235">chiave di hello tooset per tutte le istanze di TelemetryClient, inclusi i moduli di telemetria standard, imposta la chiave hello TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="c310a-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="c310a-236">Eseguire questa operazione in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c310a-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="c310a-237">Se si desidera toosend un set specifico di risorse diverso tooa di eventi, è possibile impostare chiave hello per un TelemetryClient specifico:</span><span class="sxs-lookup"><span data-stu-id="c310a-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="c310a-238">una nuova chiave, tooget [creare una nuova risorsa nel portale Application Insights hello][new].</span><span class="sxs-lookup"><span data-stu-id="c310a-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c310a-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c310a-239">Next steps</span></span>
<span data-ttu-id="c310a-240">[Altre informazioni sulle API hello][api].</span><span class="sxs-lookup"><span data-stu-id="c310a-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
