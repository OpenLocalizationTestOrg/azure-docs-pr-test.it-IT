---
title: aaaAzure Application Insights Snapshot Debugger per le app .NET | Documenti Microsoft
description: Gli snapshot di debug vengono raccolti automaticamente quando vengono generate eccezioni nelle app di produzione .NET
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="9df2e-103">Snapshot di debug per le eccezioni nelle app .NET</span><span class="sxs-lookup"><span data-stu-id="9df2e-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="9df2e-104">Quando si verifica un'eccezione, è possibile raccogliere automaticamente uno snapshot di debug dall'applicazione Web live.</span><span class="sxs-lookup"><span data-stu-id="9df2e-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="9df2e-105">lo snapshot di Hello Mostra lo stato di hello del codice sorgente e le variabili a eccezione di hello hello momento in cui è stata generata.</span><span class="sxs-lookup"><span data-stu-id="9df2e-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="9df2e-106">Hello Debugger Snapshot (anteprima) in [Azure Application Insights](app-insights-overview.md) monitora telemetria delle eccezioni dall'app web.</span><span class="sxs-lookup"><span data-stu-id="9df2e-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="9df2e-107">Raccolta di snapshot nella generazione superiore eccezioni in modo da disporre di informazioni hello necessarie toodiagnose problemi nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9df2e-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="9df2e-108">Includere hello [pacchetto NuGet di agente di raccolta dati dello Snapshot](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'applicazione e, facoltativamente, configurare i parametri della raccolta in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Snapshot sono visualizzati in [eccezioni](app-insights-asp-net-exceptions.md) portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="9df2e-109">È possibile visualizzare gli snapshot di debug nello stack di chiamate di hello toosee portale hello e controllare le variabili in ogni frame dello stack di chiamate.</span><span class="sxs-lookup"><span data-stu-id="9df2e-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="9df2e-110">un'esperienza di debug più potente con codice sorgente, open snapshot con Visual Studio 2017 Enterprise da tooget [il download di estensione del Debugger Snapshot hello per Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="9df2e-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="9df2e-111">La raccolta di snapshot è disponibile per:</span><span class="sxs-lookup"><span data-stu-id="9df2e-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="9df2e-112">Applicazioni .NET Framework e ASP.NET che eseguono .NET Framework 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9df2e-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="9df2e-113">Applicazioni .NET Core 2.0 e ASP.NET Core 2.0 in esecuzione in Windows.</span><span class="sxs-lookup"><span data-stu-id="9df2e-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="9df2e-114">Configurare la raccolta di snapshot per le applicazioni ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9df2e-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="9df2e-115">[Abilitare Application Insights nell'app Web](app-insights-asp-net.md) se non è ancora stato fatto.</span><span class="sxs-lookup"><span data-stu-id="9df2e-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="9df2e-116">Includere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app.</span><span class="sxs-lookup"><span data-stu-id="9df2e-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="9df2e-117">Esaminare le opzioni predefinite hello hello pacchetto aggiunto troppo[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="9df2e-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="9df2e-118">Gli snapshot vengono raccolti solo sulle eccezioni che vengono segnalati tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="9df2e-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="9df2e-119">In alcuni casi (ad esempio, versioni precedenti della piattaforma .NET hello), potrebbe essere troppo[configurare la raccolta di eccezioni](app-insights-asp-net-exceptions.md#exceptions) toosee eccezioni con gli snapshot nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="9df2e-120">Configurare la raccolta di snapshot per le applicazioni ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="9df2e-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="9df2e-121">[Abilitare Application Insights nell'app Web ASP.NET Core](app-insights-asp-net-core.md) se non è ancora stato fatto.</span><span class="sxs-lookup"><span data-stu-id="9df2e-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="9df2e-122">Includere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app.</span><span class="sxs-lookup"><span data-stu-id="9df2e-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="9df2e-123">Modificare hello `ConfigureServices` metodo dell'applicazione `Startup` classe del processore di tooadd hello Snapshot dell'agente di raccolta dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="9df2e-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="9df2e-124">è consigliabile aggiungere codice di Hello dipende dalla versione di cui viene fatto riferimento hello del pacchetto Microsoft.ApplicationInsights.ASPNETCore NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="9df2e-125">Per Microsoft.ApplicationInsights.AspNetCore 2.1.0 aggiungere:</span><span class="sxs-lookup"><span data-stu-id="9df2e-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="9df2e-126">Per Microsoft.ApplicationInsights.AspNetCore 2.1.1 aggiungere:</span><span class="sxs-lookup"><span data-stu-id="9df2e-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="9df2e-127">Configurare la raccolta di snapshot per le altre applicazioni .NET</span><span class="sxs-lookup"><span data-stu-id="9df2e-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="9df2e-128">Se l'applicazione non è già instrumentato con Application Insights, è possibile iniziare [l'abilitazione di Application Insights e chiave di strumentazione hello impostazione](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="9df2e-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="9df2e-129">Aggiungere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app.</span><span class="sxs-lookup"><span data-stu-id="9df2e-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="9df2e-130">Gli snapshot vengono raccolti solo sulle eccezioni che vengono segnalati tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="9df2e-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="9df2e-131">Potrebbe essere necessario toomodify tooreport il codice li.</span><span class="sxs-lookup"><span data-stu-id="9df2e-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="9df2e-132">gestione delle eccezioni Hello dipende dalla struttura hello dell'applicazione, ma è un esempio di seguito:</span><span class="sxs-lookup"><span data-stu-id="9df2e-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="9df2e-133">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="9df2e-133">Grant permissions</span></span>

<span data-ttu-id="9df2e-134">I proprietari di hello sottoscrizione di Azure è possono esaminare gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9df2e-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="9df2e-135">Agli altri utenti deve essere concessa l'autorizzazione da un proprietario.</span><span class="sxs-lookup"><span data-stu-id="9df2e-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="9df2e-136">autorizzazione toogrant, assegnare hello `Application Insights Snapshot Debugger` toousers di ruolo che esamina gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9df2e-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="9df2e-137">Questo ruolo può essere assegnato tooindividual utenti o gruppi per i proprietari di sottoscrizioni per la destinazione di hello risorsa di Application Insights oppure il suo gruppo di risorse o sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9df2e-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="9df2e-138">Aprire il pannello di controllo di accesso (IAM) hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="9df2e-139">Fare clic su hello + pulsante Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="9df2e-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="9df2e-140">Selezionare Application Insights Snapshot Debugger dall'elenco a discesa hello ruoli.</span><span class="sxs-lookup"><span data-stu-id="9df2e-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="9df2e-141">Cercare e immettere un nome per tooadd utente hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="9df2e-142">Fare clic su ruolo toohello hello Salva pulsante tooadd hello utente.</span><span class="sxs-lookup"><span data-stu-id="9df2e-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="9df2e-143">Gli snapshot possono contenere informazioni personali e altre informazioni riservate nei valori delle variabili e dei parametri.</span><span class="sxs-lookup"><span data-stu-id="9df2e-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="9df2e-144">Eseguire il debug di snapshot nel portale Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="9df2e-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="9df2e-145">Se uno snapshot è disponibile per una determinata eccezione o un ID problema, un **Apri Snapshot Debug** pulsante viene visualizzato in hello [eccezione](app-insights-asp-net-exceptions.md) portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Pulsante Open Debug Snapshot per l'eccezione](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="9df2e-147">In visualizzazione di Snapshot di eseguire il Debug di hello, viene visualizzato uno stack di chiamate e un riquadro variabili.</span><span class="sxs-lookup"><span data-stu-id="9df2e-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="9df2e-148">Quando si seleziona dello stack frame di chiamata hello nel riquadro dello stack di chiamate hello, è possibile visualizzare le variabili locali e parametri per la funzione chiamata nel riquadro variabili hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Visualizzazione Debug Snapshot nel portale di hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="9df2e-150">Gli snapshot potrebbero contenere informazioni riservate e per impostazione predefinita non sono visibili.</span><span class="sxs-lookup"><span data-stu-id="9df2e-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="9df2e-151">tooview snapshot, è necessario disporre di hello `Application Insights Snapshot Debugger` tooyou ruolo assegnato.</span><span class="sxs-lookup"><span data-stu-id="9df2e-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="9df2e-152">Snapshot di debug con Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="9df2e-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="9df2e-153">Fare clic su hello **scaricare Snapshot** toodownload pulsante un `.diagsession` file, che può essere aperta da Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="9df2e-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="9df2e-154">hello tooopen `.diagsession` file, è innanzitutto necessario [scaricare e installare l'estensione del Debugger Snapshot hello per Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="9df2e-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="9df2e-155">Dopo aver aperto il file di snapshot hello, verrà visualizzata la pagina di debug di Minidump hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9df2e-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="9df2e-156">Fare clic su **eseguire il Debug di codice gestito** toostart debug snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="9df2e-157">snapshot Hello apre toohello riga di codice in cui è stata generata l'eccezione di hello in modo che è possibile eseguire il debug dello stato corrente di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Visualizzare lo snapshot di debug in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="9df2e-159">snapshot scaricato Hello contiene tutti i file di simboli che sono stati trovati nel server applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="9df2e-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="9df2e-160">Questi file di simboli sono necessari tooassociate dati di snapshot con codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="9df2e-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="9df2e-161">Per le applicazioni di servizio App, verificare la distribuzione di simboli che tooenable quando si pubblica l'App web.</span><span class="sxs-lookup"><span data-stu-id="9df2e-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="9df2e-162">Funzionamento degli snapshot</span><span class="sxs-lookup"><span data-stu-id="9df2e-162">How snapshots work</span></span>

<span data-ttu-id="9df2e-163">All'avvio dell'applicazione viene creato un processo di caricamento degli snapshot separato che monitora le richieste di snapshot nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9df2e-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="9df2e-164">Quando viene richiesto uno snapshot, viene effettuata una copia shadow di hello esecuzione processo di circa 10 minuti di too20.</span><span class="sxs-lookup"><span data-stu-id="9df2e-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="9df2e-165">processo shadow Hello viene quindi analizzata e uno snapshot viene creato durante il processo principale hello continua toorun e non hanno toousers traffico.</span><span class="sxs-lookup"><span data-stu-id="9df2e-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="9df2e-166">Hello snapshot viene quindi caricato tooApplication Insights insieme a eventuali file rilevanti simboli (PDB) che sono necessari tooview snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="9df2e-167">Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="9df2e-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="9df2e-168">Pubblicare i simboli</span><span class="sxs-lookup"><span data-stu-id="9df2e-168">Publish symbols</span></span>
<span data-ttu-id="9df2e-169">Hello Debugger Snapshot richiede i file di simboli in variabili toodecode server di produzione hello e tooprovide un'esperienza di debug in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9df2e-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="9df2e-170">versione di Hello 15.2 di Visual Studio 2017 pubblica i simboli per le build di rilascio per impostazione predefinita quando pubblica tooApp servizio.</span><span class="sxs-lookup"><span data-stu-id="9df2e-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="9df2e-171">Nelle versioni precedenti, è necessario seguente hello tooadd profilo di pubblicazione riga tooyour `.pubxml` file in modo che i simboli vengono pubblicati in modalità di rilascio:</span><span class="sxs-lookup"><span data-stu-id="9df2e-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="9df2e-172">Per altri tipi e calcolo di Azure, verificare che i file di simboli hello siano in hello stessa cartella della DLL principale dell'applicazione hello (in genere, `wwwroot/bin`) o sono disponibili nel percorso corrente hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="9df2e-173">Compilazioni ottimizzate</span><span class="sxs-lookup"><span data-stu-id="9df2e-173">Optimized builds</span></span>
<span data-ttu-id="9df2e-174">In alcuni casi, le variabili locali non possono essere visualizzate nelle build di rilascio a causa di ottimizzazioni che vengono applicate durante il processo di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9df2e-175">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9df2e-175">Troubleshooting</span></span>

<span data-ttu-id="9df2e-176">Questi suggerimenti sulla risoluzione di problemi con hello Debugger Snapshot.</span><span class="sxs-lookup"><span data-stu-id="9df2e-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="9df2e-177">Verificare la chiave di strumentazione hello</span><span class="sxs-lookup"><span data-stu-id="9df2e-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="9df2e-178">Assicurarsi che si usi chiave di strumentazione corretta hello nell'applicazione pubblicata.</span><span class="sxs-lookup"><span data-stu-id="9df2e-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="9df2e-179">In genere, Application Insights legge la chiave di strumentazione hello dal file Applicationinsights config hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="9df2e-180">Verificare che il valore di hello è hello stesso come chiave di strumentazione hello per la risorsa di Application Insights hello che sia visualizzato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="9df2e-181">Controllare i registri uploader hello</span><span class="sxs-lookup"><span data-stu-id="9df2e-181">Check hello uploader logs</span></span>

<span data-ttu-id="9df2e-182">Dopo la creazione di uno snapshot, un file di minidump (DMP) viene creato sul disco.</span><span class="sxs-lookup"><span data-stu-id="9df2e-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="9df2e-183">Un processo separato uploader accetta file minidump e lo carica, insieme a qualsiasi file PDB associato, tooApplication archiviazione Insights Snapshot Debugger.</span><span class="sxs-lookup"><span data-stu-id="9df2e-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="9df2e-184">Dopo il minidump hello è caricato correttamente, viene eliminato dal disco.</span><span class="sxs-lookup"><span data-stu-id="9df2e-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="9df2e-185">file di log Hello per uploader minidump hello vengono mantenuti su disco.</span><span class="sxs-lookup"><span data-stu-id="9df2e-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="9df2e-186">In un ambiente del servizio app questi log si trovano in `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="9df2e-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="9df2e-187">Sito di gestione di utilizzare hello Kudu per servizio App toofind i file di registro.</span><span class="sxs-lookup"><span data-stu-id="9df2e-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="9df2e-188">Aprire l'applicazione di servizio App in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9df2e-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="9df2e-189">Seleziona hello **strumenti avanzati** pannello oppure cercare **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="9df2e-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="9df2e-190">Fare clic su **Vai**.</span><span class="sxs-lookup"><span data-stu-id="9df2e-190">Click **Go**.</span></span>
4. <span data-ttu-id="9df2e-191">In hello **console Debug** casella di riepilogo a discesa, seleziona **CMD**.</span><span class="sxs-lookup"><span data-stu-id="9df2e-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="9df2e-192">Fare clic su **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="9df2e-192">Click **LogFiles**.</span></span>

<span data-ttu-id="9df2e-193">Verrà visualizzato almeno un file con il nome che inizia con `Uploader_` e l'estensione `.log`.</span><span class="sxs-lookup"><span data-stu-id="9df2e-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="9df2e-194">Fare clic su qualsiasi file di log toodownload sull'icona appropriata hello o aperti in un browser.</span><span class="sxs-lookup"><span data-stu-id="9df2e-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="9df2e-195">nome del file Hello include il nome di computer hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="9df2e-196">Se l'istanza del servizio app è ospitata in più di un computer, è presente un file di log separato per ogni computer.</span><span class="sxs-lookup"><span data-stu-id="9df2e-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="9df2e-197">Quando il caricatore di hello rileva un nuovo file di minidump, vengono registrate nel file di log hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="9df2e-198">Ecco un esempio di caricamento corretto:</span><span class="sxs-lookup"><span data-stu-id="9df2e-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="9df2e-199">Nell'esempio precedente hello è la chiave di strumentazione hello `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="9df2e-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="9df2e-200">Questo valore deve corrispondere la chiave di strumentazione hello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9df2e-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="9df2e-201">minidump Hello è associata a uno snapshot con ID hello `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="9df2e-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="9df2e-202">È possibile utilizzare questo ID successive hello toolocate associata telemetria delle eccezioni in Application Insights Analitica.</span><span class="sxs-lookup"><span data-stu-id="9df2e-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="9df2e-203">caricatore di Hello esegue l'analisi dei file PDB di nuovo su una sola volta ogni 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="9df2e-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="9df2e-204">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9df2e-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="9df2e-205">Per le applicazioni che sono _non_ ospitato nel servizio App, hello uploader log presenti hello stessa cartella minidump hello: `%TEMP%\Dumps\<ikey>` (dove `<ikey>` è la chiave di strumentazione).</span><span class="sxs-lookup"><span data-stu-id="9df2e-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="9df2e-206">Usare Application Insights ricerca toofind eccezioni con gli snapshot</span><span class="sxs-lookup"><span data-stu-id="9df2e-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="9df2e-207">Quando viene creato uno snapshot, hello eccezioni è contrassegnato con un ID dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="9df2e-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="9df2e-208">Quando telemetria delle eccezioni hello è segnalato tooApplication Insights, l'ID dello snapshot è incluso come una proprietà personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9df2e-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="9df2e-209">Tramite il pannello di ricerca hello in Application Insights, è possibile trovare tutti i dati di telemetria con hello `ai.snapshot.id` proprietà personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9df2e-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="9df2e-210">Sfoglia risorsa di Application Insights tooyour in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9df2e-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="9df2e-211">Fare clic su **Search**(Cerca).</span><span class="sxs-lookup"><span data-stu-id="9df2e-211">Click **Search**.</span></span>
3. <span data-ttu-id="9df2e-212">Tipo `ai.snapshot.id` in hello casella di testo di ricerca e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9df2e-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Ricerca di dati di telemetria con un ID dello snapshot nel portale di hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="9df2e-214">Se la ricerca non restituisce alcun risultato, Nessuno snapshot sono stati segnalati tooApplication Insights per l'applicazione nell'intervallo di tempo hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="9df2e-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="9df2e-215">toosearch per un ID di uno snapshot specifico da log Uploader hello, digitare l'ID nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="9df2e-216">Se non è possibile trovare dati di telemetria per uno snapshot che è stato sicuramente caricato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9df2e-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="9df2e-217">Verificare che si sta consultando risorsa di Application Insights destra hello verificando la chiave di strumentazione hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="9df2e-218">Utilizza timestamp hello dal log Uploader hello, filtro di intervallo di tempo hello di hello ricerca toocover regolare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="9df2e-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="9df2e-219">Se un'eccezione con tale ID dello snapshot non viene ancora visualizzato, telemetria delle eccezioni hello non è stata segnalata tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="9df2e-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="9df2e-220">Questa situazione può verificarsi se l'applicazione di arresto anomalo dopo impiegato snapshot hello ma prima che ha segnalato la telemetria delle eccezioni hello.</span><span class="sxs-lookup"><span data-stu-id="9df2e-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="9df2e-221">In questo caso, verificare hello log di servizio App in `Diagnose and solve problems` toosee se fossero imprevisto riavvia o le eccezioni non gestite.</span><span class="sxs-lookup"><span data-stu-id="9df2e-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9df2e-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9df2e-222">Next steps</span></span>

* <span data-ttu-id="9df2e-223">[Impostare snappoints nel codice](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshot senza attendere che un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9df2e-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="9df2e-224">[Diagnosi delle eccezioni nelle App web](app-insights-asp-net-exceptions.md) spiega come toomake altre eccezioni visibili tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="9df2e-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="9df2e-225">Il [rilevamento intelligente](app-insights-proactive-diagnostics.md) rileva automaticamente le anomalie delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9df2e-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
