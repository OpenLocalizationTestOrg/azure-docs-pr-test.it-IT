---
title: registri di traccia di .NET aaaExplore in Application Insights
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
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="86492-103">Esplorare i log di traccia .NET in Application Insights</span><span class="sxs-lookup"><span data-stu-id="86492-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="86492-104">Se si utilizza NLog, log4Net o Trace per la traccia diagnostica nell'applicazione ASP.NET, è possibile disporre i log inviati troppo[Azure Application Insights][start], in cui è possibile esplorare ed eseguire ricerche essi.</span><span class="sxs-lookup"><span data-stu-id="86492-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="86492-105">I log verranno uniti hello altri dati di telemetria provenienti dall'applicazione, in modo che sia possibile identificare hello tracce associate a ogni richiesta dell'utente di manutenzione e correlarli con altri eventi e i report sulle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="86492-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="86492-106">È necessario un modulo di acquisizione registro hello?</span><span class="sxs-lookup"><span data-stu-id="86492-106">Do you need hello log capture module?</span></span> <span data-ttu-id="86492-107">questo adattatore è utile per i logger terze parti, ma se NLog, log4Net o System.Diagnostics.Trace non sono già in uso, chiamare direttamente [TrackTrace() di Application Insights](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="86492-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="86492-108">Installare la registrazione nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="86492-108">Install logging on your app</span></span>
<span data-ttu-id="86492-109">Installare il framework di registrazione scelto nel progetto.</span><span class="sxs-lookup"><span data-stu-id="86492-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="86492-110">Verrà inserita una voce nel file app.config o web.config.</span><span class="sxs-lookup"><span data-stu-id="86492-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="86492-111">Se si utilizza Trace, è necessario tooadd tooweb.config una voce:</span><span class="sxs-lookup"><span data-stu-id="86492-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="86492-112">Configura Application Insights toocollect log</span><span class="sxs-lookup"><span data-stu-id="86492-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="86492-113">**[Aggiungere Application Insights tooyour progetto](app-insights-asp-net.md)**  se non è che ancora.</span><span class="sxs-lookup"><span data-stu-id="86492-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="86492-114">Verrà visualizzata un'opzione tooinclude hello log agente di raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="86492-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="86492-115">In alternativa, **configurare Application Insights** facendo clic con il pulsante destro del mouse in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="86492-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="86492-116">L'opzione hello troppo**configurare la traccia raccolta**.</span><span class="sxs-lookup"><span data-stu-id="86492-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="86492-117">*Il menu di Application Insights o  l'opzione di raccolta non viene visualizzata?*</span><span class="sxs-lookup"><span data-stu-id="86492-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="86492-118">Vedere [Risoluzione dei problemi](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="86492-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="86492-119">Installazione manuale</span><span class="sxs-lookup"><span data-stu-id="86492-119">Manual installation</span></span>
<span data-ttu-id="86492-120">Utilizzare questo metodo se il tipo di progetto non è supportato dal programma di installazione di hello Application Insights (ad esempio un desktop progetto Windows).</span><span class="sxs-lookup"><span data-stu-id="86492-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="86492-121">Se si intende toouse log4Net o NLog, installarlo nel progetto.</span><span class="sxs-lookup"><span data-stu-id="86492-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="86492-122">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="86492-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="86492-123">Cercare "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="86492-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="86492-124">Selezionare pacchetto appropriato hello - uno di:</span><span class="sxs-lookup"><span data-stu-id="86492-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="86492-125">Microsoft.ApplicationInsights.TraceListener (toocapture Trace chiamate)</span><span class="sxs-lookup"><span data-stu-id="86492-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="86492-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventi)</span><span class="sxs-lookup"><span data-stu-id="86492-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="86492-127">Microsoft.ApplicationInsights.EtwListener (eventi ETW toocapture)</span><span class="sxs-lookup"><span data-stu-id="86492-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="86492-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="86492-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="86492-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="86492-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="86492-130">pacchetto NuGet Hello installa gli assembly necessari hello e anche di modificare il file Web. config o App. config.</span><span class="sxs-lookup"><span data-stu-id="86492-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="86492-131">Inserire chiamate di log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="86492-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="86492-132">Se si usa System.Diagnostics.Trace, una tipica chiamata sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="86492-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="86492-133">Se si preferisce log4net o NLog:</span><span class="sxs-lookup"><span data-stu-id="86492-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="86492-134">Uso degli eventi EventSource</span><span class="sxs-lookup"><span data-stu-id="86492-134">Using EventSource events</span></span>
<span data-ttu-id="86492-135">È possibile configurare [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe inviati eventi informazioni come le tracce.</span><span class="sxs-lookup"><span data-stu-id="86492-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="86492-136">Installare innanzitutto hello `Microsoft.ApplicationInsights.EventSourceListener` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="86492-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="86492-137">Modificare quindi `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="86492-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="86492-138">Per ogni origine, è possibile impostare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="86492-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="86492-139">`Name`Specifica il nome di hello di hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="86492-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="86492-140">`Level`Specifica hello toocollect livello di registrazione.</span><span class="sxs-lookup"><span data-stu-id="86492-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="86492-141">Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="86492-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="86492-142">`Keywords`(Facoltativo) specifica il valore intero hello di toouse combinazioni di parole chiave.</span><span class="sxs-lookup"><span data-stu-id="86492-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="86492-143">Uso degli eventi DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="86492-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="86492-144">È possibile configurare [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe inviati eventi informazioni come le tracce.</span><span class="sxs-lookup"><span data-stu-id="86492-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="86492-145">Installare innanzitutto hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="86492-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="86492-146">Modificare quindi hello `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="86492-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="86492-147">Per ogni DiagnosticSource desiderato tootrace, aggiungere una voce con hello `Name` toohello nome del DiagnosticSource del set di attributi.</span><span class="sxs-lookup"><span data-stu-id="86492-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="86492-148">Uso degli eventi ETW</span><span class="sxs-lookup"><span data-stu-id="86492-148">Using ETW events</span></span>
<span data-ttu-id="86492-149">È possibile configurare toobe eventi ETW inviato tooApplication informazioni come le tracce.</span><span class="sxs-lookup"><span data-stu-id="86492-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="86492-150">Installare innanzitutto hello `Microsoft.ApplicationInsights.EtwCollector` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="86492-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="86492-151">Modificare quindi `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="86492-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="86492-152">Eventi ETW possono essere raccolti solo se hello di hosting processo hello SDK è in esecuzione in un'identità che è un membro di "Performance Log Users" o gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="86492-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="86492-153">Per ogni origine, è possibile impostare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="86492-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="86492-154">`ProviderName`è il nome di hello del toocollect di provider ETW hello.</span><span class="sxs-lookup"><span data-stu-id="86492-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="86492-155">`ProviderGuid`Specifica hello GUID di hello toocollect di provider ETW, può essere utilizzato al posto di `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="86492-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="86492-156">`Level`Imposta hello toocollect livello di registrazione.</span><span class="sxs-lookup"><span data-stu-id="86492-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="86492-157">Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="86492-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="86492-158">`Keywords`(Facoltativo) set hello intero toouse combinazioni di parole chiave.</span><span class="sxs-lookup"><span data-stu-id="86492-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="86492-159">Utilizzo diretto di hello traccia API</span><span class="sxs-lookup"><span data-stu-id="86492-159">Using hello Trace API directly</span></span>
<span data-ttu-id="86492-160">È possibile chiamare API di traccia di Application Insights hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="86492-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="86492-161">adattatori di registrazione Hello usare questa API.</span><span class="sxs-lookup"><span data-stu-id="86492-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="86492-162">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86492-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="86492-163">Un vantaggio TrackTrace è possibile inserire dati relativamente lunghi nel messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="86492-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="86492-164">Ad esempio, è possibile codificare dati POST.</span><span class="sxs-lookup"><span data-stu-id="86492-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="86492-165">Inoltre, è possibile aggiungere un messaggio tooyour livello di gravità.</span><span class="sxs-lookup"><span data-stu-id="86492-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="86492-166">E, come gli altri dati di telemetria, è possibile aggiungere i valori delle proprietà che è possibile utilizzare il filtro toohelp o ricerca per diversi set di tracce.</span><span class="sxs-lookup"><span data-stu-id="86492-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="86492-167">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86492-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="86492-168">In tal modo, [ricerca][diagnostic], tooeasily escludere tutti i messaggi hello di un livello di gravità specifico relative tooa particolare database.</span><span class="sxs-lookup"><span data-stu-id="86492-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="86492-169">Esplorare i log</span><span class="sxs-lookup"><span data-stu-id="86492-169">Explore your logs</span></span>
<span data-ttu-id="86492-170">Eseguire l'app in modalità debug o distribuirla.</span><span class="sxs-lookup"><span data-stu-id="86492-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="86492-171">Nel pannello della panoramica dell'app in [portale Application Insights hello][portal], scegliere [ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="86492-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![In Application Insights scegliere Cerca](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Cerca](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="86492-174">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="86492-174">You can, for example:</span></span>

* <span data-ttu-id="86492-175">Filtrare in base alle tracce dei log o agli elementi con proprietà specifiche</span><span class="sxs-lookup"><span data-stu-id="86492-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="86492-176">Esaminare un elemento specifico in modo dettagliato</span><span class="sxs-lookup"><span data-stu-id="86492-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="86492-177">Trovare altri dati di telemetria relativi toohello stessa richiesta dell'utente (ovvero, con hello stesso OperationId)</span><span class="sxs-lookup"><span data-stu-id="86492-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="86492-178">Salvare la configurazione hello di questa pagina come preferito</span><span class="sxs-lookup"><span data-stu-id="86492-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="86492-179">**Campionamento.**</span><span class="sxs-lookup"><span data-stu-id="86492-179">**Sampling.**</span></span> <span data-ttu-id="86492-180">Se l'applicazione invia una grande quantità di dati e si utilizza hello Application Insights SDK per ASP.NET versione 2.0.0-beta3 o versione successiva, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="86492-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="86492-181">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="86492-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="86492-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86492-182">Next steps</span></span>
<span data-ttu-id="86492-183">[Diagnosticare errori ed eccezioni in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="86492-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="86492-184">[Altre informazioni sulla ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="86492-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="86492-185">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="86492-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="86492-186">Come procedere per Java?</span><span class="sxs-lookup"><span data-stu-id="86492-186">How do I do this for Java?</span></span>
<span data-ttu-id="86492-187">Hello utilizzare [schede log Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="86492-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="86492-188">Non sono disponibili opzioni di Application Insights nel menu di scelta rapida progetto hello</span><span class="sxs-lookup"><span data-stu-id="86492-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="86492-189">Verificare che Strumenti Application Insights sia installato nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="86492-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="86492-190">In Visual Studio, scegliere Strumenti, Estensioni e Aggiornamenti e cercare Strumenti Application Insights.</span><span class="sxs-lookup"><span data-stu-id="86492-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="86492-191">Se non si trova in scheda installati hello, aprire hello Online scheda e installarlo.</span><span class="sxs-lookup"><span data-stu-id="86492-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="86492-192">Potrebbe trattarsi di un tipo di progetto non supportato da Strumenti Application Insights.</span><span class="sxs-lookup"><span data-stu-id="86492-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="86492-193">Usare l' [installazione manuale](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="86492-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="86492-194">Nessuna opzione adapter log nello strumento di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="86492-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="86492-195">È necessario prima registrazione hello tooinstall framework.</span><span class="sxs-lookup"><span data-stu-id="86492-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="86492-196">Se si usa System.Diagnostics.Trace, verificare di [aver eseguito la configurazione in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="86492-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="86492-197">È stato ottenuto versione più recente di hello di Application Insights?</span><span class="sxs-lookup"><span data-stu-id="86492-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="86492-198">In Visual Studio **strumenti** menu, scegliere **estensioni e aggiornamenti**, aprire hello e **aggiornamenti** scheda. Se gli strumenti per sviluppatori Analitica è presente, fare clic su tooupdate è.</span><span class="sxs-lookup"><span data-stu-id="86492-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="86492-199"><a name="emptykey"></a>Viene visualizzato l'errore: "La chiave di strumentazione non può essere vuota"</span><span class="sxs-lookup"><span data-stu-id="86492-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="86492-200">Sembra che è stato installato hello registrazione pacchetto Nuget adapter senza installare Application Insights.</span><span class="sxs-lookup"><span data-stu-id="86492-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="86492-201">In Esplora soluzioni fare clic con il pulsante destro del mouse su `ApplicationInsights.config` e scegliere **Aggiorna Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="86492-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="86492-202">Si otterrà una finestra di dialogo Invita toosign in tooAzure e creare una risorsa di Application Insights, o riutilizzare uno esistente.</span><span class="sxs-lookup"><span data-stu-id="86492-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="86492-203">Il problema verrà in tal modo risolto.</span><span class="sxs-lookup"><span data-stu-id="86492-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="86492-204">È possibile vedere tracce in ricerca di diagnostica, ma non hello altri eventi</span><span class="sxs-lookup"><span data-stu-id="86492-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="86492-205">In alcuni casi può richiedere un po' di tempo per tutti hello tooget di eventi e le richieste tramite pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="86492-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="86492-206"><a name="limits"></a>Quanti dati vengono conservati?</span><span class="sxs-lookup"><span data-stu-id="86492-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="86492-207">Molti fattori influiscono quantità hello dei dati da mantenere.</span><span class="sxs-lookup"><span data-stu-id="86492-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="86492-208">Vedere hello [limiti](app-insights-api-custom-events-metrics.md#limits) sezione della pagina di metriche di hello cliente eventi per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="86492-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="86492-209">Non vengono visualizzati alcuni hello voci di log previsti</span><span class="sxs-lookup"><span data-stu-id="86492-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="86492-210">Se l'applicazione invia una grande quantità di dati e si utilizza hello Application Insights SDK per ASP.NET versione 2.0.0-beta3 o versione successiva, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="86492-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="86492-211">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="86492-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="86492-212"><a name="add"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86492-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="86492-213">[Configurare i test di disponibilità e velocità di risposta][availability]</span><span class="sxs-lookup"><span data-stu-id="86492-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="86492-214">[Risoluzione dei problemi][qna]</span><span class="sxs-lookup"><span data-stu-id="86492-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
