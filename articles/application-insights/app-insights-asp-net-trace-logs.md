---
title: Esplorare i log di traccia .NET in Application Insights
description: Cercare i log generati con Trace, NLog o Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="736b9-103">Esplorare i log di traccia .NET in Application Insights</span><span class="sxs-lookup"><span data-stu-id="736b9-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="736b9-104">Se si usa NLog, log4Net o System.Diagnostics.Trace per l'analisi diagnostica nell'applicazione ASP.NET, è possibile fare in modo che i log vengano inviati a [Application Insights di Azure][start], dove è possibile esplorarli ed eseguirvi ricerche.</span><span class="sxs-lookup"><span data-stu-id="736b9-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="736b9-105">I log verranno uniti con gli altri eventi di telemetria provenienti dall'applicazione, in modo da potere identificare le tracce associate alla gestione di ogni richiesta dell'utente e metterle in correlazione con altri eventi e i report di eccezioni.</span><span class="sxs-lookup"><span data-stu-id="736b9-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="736b9-106">Se è necessario un modulo di acquisizione dei log,</span><span class="sxs-lookup"><span data-stu-id="736b9-106">Do you need the log capture module?</span></span> <span data-ttu-id="736b9-107">questo adattatore è utile per i logger terze parti, ma se NLog, log4Net o System.Diagnostics.Trace non sono già in uso, chiamare direttamente [TrackTrace() di Application Insights](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="736b9-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="736b9-108">Installare la registrazione nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="736b9-108">Install logging on your app</span></span>
<span data-ttu-id="736b9-109">Installare il framework di registrazione scelto nel progetto.</span><span class="sxs-lookup"><span data-stu-id="736b9-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="736b9-110">Verrà inserita una voce nel file app.config o web.config.</span><span class="sxs-lookup"><span data-stu-id="736b9-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="736b9-111">Se si usa System.Diagnostics.Trace, è necessario aggiungere una voce a web.config:</span><span class="sxs-lookup"><span data-stu-id="736b9-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="736b9-112">Configurare Application Insights per la raccolta dei log</span><span class="sxs-lookup"><span data-stu-id="736b9-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="736b9-113">Se non è ancora stato fatto, **[aggiungere Application Insights al progetto](app-insights-asp-net.md)**.</span><span class="sxs-lookup"><span data-stu-id="736b9-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="736b9-114">Verrà visualizzata un'opzione per includere la raccolta dei log.</span><span class="sxs-lookup"><span data-stu-id="736b9-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="736b9-115">In alternativa, **configurare Application Insights** facendo clic con il pulsante destro del mouse in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="736b9-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="736b9-116">Selezionare l'opzione per **configurare la raccolta delle tracce**.</span><span class="sxs-lookup"><span data-stu-id="736b9-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="736b9-117">*Il menu di Application Insights o  l'opzione di raccolta non viene visualizzata?*</span><span class="sxs-lookup"><span data-stu-id="736b9-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="736b9-118">Vedere [Risoluzione dei problemi](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="736b9-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="736b9-119">Installazione manuale</span><span class="sxs-lookup"><span data-stu-id="736b9-119">Manual installation</span></span>
<span data-ttu-id="736b9-120">Usare questo metodo se il tipo di progetto non è supportato dal programma di installazione di Application Insights, ad esempio un progetto Desktop di Windows.</span><span class="sxs-lookup"><span data-stu-id="736b9-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="736b9-121">Se si intende usare log4Net o NLog, installarlo nel progetto.</span><span class="sxs-lookup"><span data-stu-id="736b9-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="736b9-122">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="736b9-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="736b9-123">Cercare "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="736b9-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="736b9-124">Selezionare il pacchetto appropriato tra:</span><span class="sxs-lookup"><span data-stu-id="736b9-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="736b9-125">Microsoft.ApplicationInsights.TraceListener (per acquisire le chiamate System.Diagnostics.Trace)</span><span class="sxs-lookup"><span data-stu-id="736b9-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="736b9-126">Microsoft.ApplicationInsights.EventSourceListener, per acquisire gli eventi EventSource</span><span class="sxs-lookup"><span data-stu-id="736b9-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="736b9-127">Microsoft.ApplicationInsights.EtwListener, per acquisire gli eventi ETW</span><span class="sxs-lookup"><span data-stu-id="736b9-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="736b9-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="736b9-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="736b9-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="736b9-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="736b9-130">Il pacchetto NuGet installa gli assembly necessari e modifica inoltre web.config o app.config.</span><span class="sxs-lookup"><span data-stu-id="736b9-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="736b9-131">Inserire chiamate di log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="736b9-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="736b9-132">Se si usa System.Diagnostics.Trace, una tipica chiamata sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="736b9-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="736b9-133">Se si preferisce log4net o NLog:</span><span class="sxs-lookup"><span data-stu-id="736b9-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="736b9-134">Uso degli eventi EventSource</span><span class="sxs-lookup"><span data-stu-id="736b9-134">Using EventSource events</span></span>
<span data-ttu-id="736b9-135">È possibile configurare eventi [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) da inviare ad Application Insights come tracce.</span><span class="sxs-lookup"><span data-stu-id="736b9-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="736b9-136">Installare innanzitutto il pacchetto NuGet `Microsoft.ApplicationInsights.EventSourceListener`.</span><span class="sxs-lookup"><span data-stu-id="736b9-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="736b9-137">Quindi modificare la sezione `TelemetryModules` del file [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="736b9-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="736b9-138">Per ogni origine è possibile impostare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="736b9-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="736b9-139">`Name` specifica il nome di EventSource da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="736b9-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="736b9-140">`Level` specifica il livello di registrazione da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="736b9-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="736b9-141">Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="736b9-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="736b9-142">`Keywords` è facoltativo e specifica il valore intero di combinazioni di parole chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="736b9-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="736b9-143">Uso degli eventi DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="736b9-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="736b9-144">È possibile configurare eventi [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) da inviare ad Application Insights come tracce.</span><span class="sxs-lookup"><span data-stu-id="736b9-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="736b9-145">Installare innanzitutto il pacchetto NuGet [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener).</span><span class="sxs-lookup"><span data-stu-id="736b9-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="736b9-146">Quindi modificare la sezione `TelemetryModules` del file [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="736b9-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="736b9-147">Per ogni DiagnosticSource che si desidera tracciare, aggiungere una voce con l'attributo `Name` impostato sul nome di DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="736b9-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="736b9-148">Uso degli eventi ETW</span><span class="sxs-lookup"><span data-stu-id="736b9-148">Using ETW events</span></span>
<span data-ttu-id="736b9-149">È possibile configurare eventi ETW da inviare ad Application Insights come tracce.</span><span class="sxs-lookup"><span data-stu-id="736b9-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="736b9-150">Installare innanzitutto il pacchetto NuGet `Microsoft.ApplicationInsights.EtwCollector`.</span><span class="sxs-lookup"><span data-stu-id="736b9-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="736b9-151">Quindi modificare la sezione `TelemetryModules` del file [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="736b9-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="736b9-152">Gli eventi ETW possono essere raccolti solo se il processo che ospita l'SDK viene eseguito in un'identità che è membro di "Performance Log Users" o amministratori.</span><span class="sxs-lookup"><span data-stu-id="736b9-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="736b9-153">Per ogni origine è possibile impostare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="736b9-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="736b9-154">`ProviderName` è il nome del provider ETW da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="736b9-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="736b9-155">`ProviderGuid` specifica il GUID del provider ETW da raccogliere, può essere usato al posto di `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="736b9-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="736b9-156">`Level` imposta il livello di registrazione da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="736b9-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="736b9-157">Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="736b9-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="736b9-158">`Keywords` è facoltativo e imposta il valore intero di combinazioni di parole chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="736b9-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="736b9-159">Uso diretto dell'API di traccia</span><span class="sxs-lookup"><span data-stu-id="736b9-159">Using the Trace API directly</span></span>
<span data-ttu-id="736b9-160">È possibile chiamare direttamente l'API di traccia di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="736b9-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="736b9-161">Gli adattatori di registrazione usano questa API.</span><span class="sxs-lookup"><span data-stu-id="736b9-161">The logging adapters use this API.</span></span>

<span data-ttu-id="736b9-162">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="736b9-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="736b9-163">Un vantaggio di TrackTrace è che è possibile inserire dati relativamente lunghi nel messaggio.</span><span class="sxs-lookup"><span data-stu-id="736b9-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="736b9-164">Ad esempio, è possibile codificare dati POST.</span><span class="sxs-lookup"><span data-stu-id="736b9-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="736b9-165">È anche possibile aggiungere al messaggio un livello di gravità.</span><span class="sxs-lookup"><span data-stu-id="736b9-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="736b9-166">E come per altri tipi di dati di telemetria, si possono aggiungere valori di proprietà che è possibile usare per filtrare o cercare set di tracce diversi,</span><span class="sxs-lookup"><span data-stu-id="736b9-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="736b9-167">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="736b9-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="736b9-168">Questo consentirà, in [Ricerca][diagnostic], di filtrare facilmente tutti i messaggi di un determinato livello di gravità relativi a un database specifico.</span><span class="sxs-lookup"><span data-stu-id="736b9-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="736b9-169">Esplorare i log</span><span class="sxs-lookup"><span data-stu-id="736b9-169">Explore your logs</span></span>
<span data-ttu-id="736b9-170">Eseguire l'app in modalità debug o distribuirla.</span><span class="sxs-lookup"><span data-stu-id="736b9-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="736b9-171">Nel pannello Panoramica dell'app nel [portale di Application Insights][portal] scegliere [Cerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="736b9-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![In Application Insights scegliere Cerca](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Cerca](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="736b9-174">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="736b9-174">You can, for example:</span></span>

* <span data-ttu-id="736b9-175">Filtrare in base alle tracce dei log o agli elementi con proprietà specifiche</span><span class="sxs-lookup"><span data-stu-id="736b9-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="736b9-176">Esaminare un elemento specifico in modo dettagliato</span><span class="sxs-lookup"><span data-stu-id="736b9-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="736b9-177">Trovare altri eventi di telemetria relativi alla stessa richiesta dell'utente (ovvero, con lo stesso valore OperationId)</span><span class="sxs-lookup"><span data-stu-id="736b9-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="736b9-178">Salvare la configurazione di questa pagina come preferita</span><span class="sxs-lookup"><span data-stu-id="736b9-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="736b9-179">**Campionamento.**</span><span class="sxs-lookup"><span data-stu-id="736b9-179">**Sampling.**</span></span> <span data-ttu-id="736b9-180">Se l'applicazione invia una grande quantità di dati e si sta utilizzando la versione 2.0.0-beta3 o versioni successive dell’SDK di Application Insights per ASP.NET, la funzionalità del campionamento adattivo può operare e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="736b9-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="736b9-181">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="736b9-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="736b9-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="736b9-182">Next steps</span></span>
<span data-ttu-id="736b9-183">[Diagnosticare errori ed eccezioni in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="736b9-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="736b9-184">[Altre informazioni sulla ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="736b9-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="736b9-185">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="736b9-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="736b9-186">Come procedere per Java?</span><span class="sxs-lookup"><span data-stu-id="736b9-186">How do I do this for Java?</span></span>
<span data-ttu-id="736b9-187">Usare gli [adattatori log Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="736b9-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="736b9-188">Non è disponibile alcuna opzione di Application Insights nel menu di scelta rapida del progetto</span><span class="sxs-lookup"><span data-stu-id="736b9-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="736b9-189">Verificare che Strumenti Application Insights sia installato nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="736b9-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="736b9-190">In Visual Studio, scegliere Strumenti, Estensioni e Aggiornamenti e cercare Strumenti Application Insights.</span><span class="sxs-lookup"><span data-stu-id="736b9-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="736b9-191">Se non è visualizzato nella scheda degli elementi installati, aprire la scheda Online e installarlo.</span><span class="sxs-lookup"><span data-stu-id="736b9-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="736b9-192">Potrebbe trattarsi di un tipo di progetto non supportato da Strumenti Application Insights.</span><span class="sxs-lookup"><span data-stu-id="736b9-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="736b9-193">Usare l' [installazione manuale](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="736b9-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="736b9-194">Nello strumento di configurazione non è disponibile alcuna opzione per l'adattatore log</span><span class="sxs-lookup"><span data-stu-id="736b9-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="736b9-195">È necessario installare innanzitutto il framework di registrazione.</span><span class="sxs-lookup"><span data-stu-id="736b9-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="736b9-196">Se si usa System.Diagnostics.Trace, verificare di [aver eseguito la configurazione in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="736b9-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="736b9-197">Si dispone della versione più recente di Application Insights?</span><span class="sxs-lookup"><span data-stu-id="736b9-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="736b9-198">Scegliere **Estensioni e aggiornamenti** dal menu **Strumenti** di Visual Studio e aprire la scheda **Aggiornamenti**. Se Developer Analytics Tools è presente, fare clic per eseguire l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="736b9-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="736b9-199"><a name="emptykey"></a>Viene visualizzato l'errore: "La chiave di strumentazione non può essere vuota"</span><span class="sxs-lookup"><span data-stu-id="736b9-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="736b9-200">Risulta che l'utente abbia installato il pacchetto NuGet dell'adattatore di registrazione senza aver installato Application Insights.</span><span class="sxs-lookup"><span data-stu-id="736b9-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="736b9-201">In Esplora soluzioni fare clic con il pulsante destro del mouse su `ApplicationInsights.config` e scegliere **Aggiorna Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="736b9-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="736b9-202">Verrà visualizzata una finestra di dialogo che invita ad accedere ad Azure e a creare una risorsa di Application Insights o a riusarne una esistente.</span><span class="sxs-lookup"><span data-stu-id="736b9-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="736b9-203">Il problema verrà in tal modo risolto.</span><span class="sxs-lookup"><span data-stu-id="736b9-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="736b9-204">Nella ricerca diagnostica vengono visualizzate le tracce ma non gli altri eventi</span><span class="sxs-lookup"><span data-stu-id="736b9-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="736b9-205">Talvolta la visualizzazione di tutti gli eventi e le richieste nella pipeline può richiedere un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="736b9-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="736b9-206"><a name="limits"></a>Quanti dati vengono conservati?</span><span class="sxs-lookup"><span data-stu-id="736b9-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="736b9-207">Diversi fattori influiscono sulla quantità di dati mantenuti.</span><span class="sxs-lookup"><span data-stu-id="736b9-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="736b9-208">Per altre informazioni, vedere la sezione dei [limiti](app-insights-api-custom-events-metrics.md#limits) della pagina delle metriche degli eventi dei clienti.</span><span class="sxs-lookup"><span data-stu-id="736b9-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="736b9-209">Non è possibile vedere alcune delle voci di log previste</span><span class="sxs-lookup"><span data-stu-id="736b9-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="736b9-210">Se l'applicazione invia una grande quantità di dati e si sta utilizzando la versione 2.0.0-beta3 o versioni successive dell’SDK di Application Insights per ASP.NET, la funzionalità del campionamento adattivo può operare e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="736b9-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="736b9-211">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="736b9-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="736b9-212"><a name="add"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="736b9-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="736b9-213">[Configurare i test di disponibilità e velocità di risposta][availability]</span><span class="sxs-lookup"><span data-stu-id="736b9-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="736b9-214">[Risoluzione dei problemi][qna]</span><span class="sxs-lookup"><span data-stu-id="736b9-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
