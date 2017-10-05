---
title: Snapshot Debugger di Azure Application Insights per app .NET | Microsoft Docs
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="66f10-103">Snapshot di debug per le eccezioni nelle app .NET</span><span class="sxs-lookup"><span data-stu-id="66f10-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="66f10-104">Quando si verifica un'eccezione, è possibile raccogliere automaticamente uno snapshot di debug dall'applicazione Web live.</span><span class="sxs-lookup"><span data-stu-id="66f10-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="66f10-105">Lo snapshot mostra lo stato del codice sorgente e delle variabili nel momento in cui è stata generata l'eccezione.</span><span class="sxs-lookup"><span data-stu-id="66f10-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="66f10-106">Snapshot Debugger (anteprima) di [Azure Application Insights](app-insights-overview.md) monitora la telemetria delle eccezioni dall'app Web.</span><span class="sxs-lookup"><span data-stu-id="66f10-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="66f10-107">Raccoglie snapshot per le eccezioni generate più frequentemente in modo che l'utente possa avere le informazioni necessarie per diagnosticare i problemi nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="66f10-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="66f10-108">Includere il [pacchetto NuGet Snapshot Collector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'applicazione e configurare facoltativamente i parametri di raccolta in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Gli snapshot vengono visualizzati per le [eccezioni](app-insights-asp-net-exceptions.md) nel portale Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="66f10-109">È possibile visualizzare gli snapshot di debug nel portale per vedere lo stack di chiamate e ispezionare le variabili in ogni stack frame di chiamate.</span><span class="sxs-lookup"><span data-stu-id="66f10-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="66f10-110">Per eseguire più efficacemente il debug del codice sorgente, aprire gli snapshot con Visual Studio 2017 Enterprise [scaricando l'estensione Snapshot Debugger per Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="66f10-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="66f10-111">La raccolta di snapshot è disponibile per:</span><span class="sxs-lookup"><span data-stu-id="66f10-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="66f10-112">Applicazioni .NET Framework e ASP.NET che eseguono .NET Framework 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="66f10-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="66f10-113">Applicazioni .NET Core 2.0 e ASP.NET Core 2.0 in esecuzione in Windows.</span><span class="sxs-lookup"><span data-stu-id="66f10-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="66f10-114">Configurare la raccolta di snapshot per le applicazioni ASP.NET</span><span class="sxs-lookup"><span data-stu-id="66f10-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="66f10-115">[Abilitare Application Insights nell'app Web](app-insights-asp-net.md) se non è ancora stato fatto.</span><span class="sxs-lookup"><span data-stu-id="66f10-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="66f10-116">Includere il pacchetto NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'app.</span><span class="sxs-lookup"><span data-stu-id="66f10-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="66f10-117">Esaminare le opzioni predefinite che il pacchetto ha aggiunto ad [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="66f10-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="66f10-118">Gli snapshot vengono raccolti solo per le eccezioni segnalate ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="66f10-119">In alcuni casi (ad esempio, versioni precedenti della piattaforma .NET), potrebbe essere necessario [configurare la raccolta di eccezioni](app-insights-asp-net-exceptions.md#exceptions) per visualizzare le eccezioni con gli snapshot nel portale.</span><span class="sxs-lookup"><span data-stu-id="66f10-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="66f10-120">Configurare la raccolta di snapshot per le applicazioni ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="66f10-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="66f10-121">[Abilitare Application Insights nell'app Web ASP.NET Core](app-insights-asp-net-core.md) se non è ancora stato fatto.</span><span class="sxs-lookup"><span data-stu-id="66f10-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="66f10-122">Includere il pacchetto NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'app.</span><span class="sxs-lookup"><span data-stu-id="66f10-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="66f10-123">Modificare il metodo `ConfigureServices` nella classe `Startup` dell'applicazione per aggiungere il processore di telemetria dell'agente di raccolta snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="66f10-124">Il codice da aggiungere dipende dalla versione referenziata del pacchetto Microsoft.ApplicationInsights.ASPNETCore NuGet.</span><span class="sxs-lookup"><span data-stu-id="66f10-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="66f10-125">Per Microsoft.ApplicationInsights.AspNetCore 2.1.0 aggiungere:</span><span class="sxs-lookup"><span data-stu-id="66f10-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="66f10-126">Per Microsoft.ApplicationInsights.AspNetCore 2.1.1 aggiungere:</span><span class="sxs-lookup"><span data-stu-id="66f10-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="66f10-127">Configurare la raccolta di snapshot per le altre applicazioni .NET</span><span class="sxs-lookup"><span data-stu-id="66f10-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="66f10-128">Se l'applicazione non è già instrumentata con Application Insights, iniziare [abilitando Application Insights e impostando la chiave di strumentazione](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="66f10-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="66f10-129">Aggiungere il pacchetto NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'app.</span><span class="sxs-lookup"><span data-stu-id="66f10-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="66f10-130">Gli snapshot vengono raccolti solo per le eccezioni segnalate ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="66f10-131">Potrebbe essere necessario modificare il codice per segnalarle.</span><span class="sxs-lookup"><span data-stu-id="66f10-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="66f10-132">Anche se il codice di gestione delle eccezioni dipende dalla struttura dell'applicazione, di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="66f10-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="66f10-133">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="66f10-133">Grant permissions</span></span>

<span data-ttu-id="66f10-134">Gli snapshot possono essere ispezionati dai proprietari della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f10-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="66f10-135">Agli altri utenti deve essere concessa l'autorizzazione da un proprietario.</span><span class="sxs-lookup"><span data-stu-id="66f10-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="66f10-136">Per concedere l'autorizzazione, assegnare il ruolo `Application Insights Snapshot Debugger` agli utenti che ispezioneranno gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="66f10-137">Questo ruolo può essere assegnato a singoli utenti o gruppi dai proprietari della sottoscrizione per la risorsa di Application Insights di destinazione oppure per il gruppo di risorse o la sottoscrizione di tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="66f10-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="66f10-138">Aprire il pannello Controllo di accesso (IAM).</span><span class="sxs-lookup"><span data-stu-id="66f10-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="66f10-139">Fare clic sul pulsante +Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="66f10-139">Click the +Add button.</span></span>
1. <span data-ttu-id="66f10-140">Selezionare Debugger di snapshot di Application Insights nell'elenco a discesa Ruoli.</span><span class="sxs-lookup"><span data-stu-id="66f10-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="66f10-141">Cercare e immettere un nome per l'utente da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="66f10-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="66f10-142">Fare clic sul pulsante Salva per aggiungere l'utente al ruolo.</span><span class="sxs-lookup"><span data-stu-id="66f10-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="66f10-143">Gli snapshot possono contenere informazioni personali e altre informazioni riservate nei valori delle variabili e dei parametri.</span><span class="sxs-lookup"><span data-stu-id="66f10-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="66f10-144">Snapshot di debug nel portale di Application Insights</span><span class="sxs-lookup"><span data-stu-id="66f10-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="66f10-145">Se è disponibile uno snapshot per una determinata eccezione o un determinato ID problema, viene visualizzato il pulsante **Open Debug Snapshot** (Apri snapshot di debug) per l'[eccezione](app-insights-asp-net-exceptions.md) nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Pulsante Open Debug Snapshot per l'eccezione](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="66f10-147">Nella vista Debug Snapshot (Snapshot di debug) vengono visualizzati uno stack di chiamate e un riquadro delle variabili.</span><span class="sxs-lookup"><span data-stu-id="66f10-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="66f10-148">Quando si selezionano frame dello stack di chiamate nel riquadro corrispondente, è possibile visualizzare i parametri e le variabili locali per la chiamata di funzione nel riquadro delle variabili.</span><span class="sxs-lookup"><span data-stu-id="66f10-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Visualizzare uno snapshot di debug nel portale](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="66f10-150">Gli snapshot potrebbero contenere informazioni riservate e per impostazione predefinita non sono visibili.</span><span class="sxs-lookup"><span data-stu-id="66f10-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="66f10-151">Per visualizzare gli snapshot, è necessario che all'utente sia stato assegnato il ruolo `Application Insights Snapshot Debugger`.</span><span class="sxs-lookup"><span data-stu-id="66f10-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="66f10-152">Snapshot di debug con Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="66f10-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="66f10-153">Fare clic sul pulsante **Download Snapshot** (Scarica snapshot) per scaricare un file `.diagsession` che può essere aperto con Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="66f10-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="66f10-154">Per aprire il file `.diagsession`, è necessario prima di tutto [scaricare e installare l'estensione Snapshot Debugger per Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="66f10-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="66f10-155">Quando si apre il file di snapshot, in Visual Studio viene visualizzata la pagina per il debug di minidump.</span><span class="sxs-lookup"><span data-stu-id="66f10-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="66f10-156">Fare clic su **Debug Managed Code** (Debug codice gestito) per avviare il debug dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="66f10-157">Lo snapshot viene aperto alla riga di codice in cui è stata generata l'eccezione in modo da consentire il debug dello stato corrente del processo.</span><span class="sxs-lookup"><span data-stu-id="66f10-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Visualizzare lo snapshot di debug in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="66f10-159">Lo snapshot scaricato contiene tutti file di simboli trovati nel server applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="66f10-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="66f10-160">Questi file di simboli sono necessari per associare i dati degli snapshot al codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="66f10-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="66f10-161">Per le app del servizio app, assicurarsi di abilitare la distribuzione dei simboli al momento della pubblicazione delle app Web.</span><span class="sxs-lookup"><span data-stu-id="66f10-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="66f10-162">Funzionamento degli snapshot</span><span class="sxs-lookup"><span data-stu-id="66f10-162">How snapshots work</span></span>

<span data-ttu-id="66f10-163">All'avvio dell'applicazione viene creato un processo di caricamento degli snapshot separato che monitora le richieste di snapshot nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="66f10-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="66f10-164">Quando viene richiesto uno snapshot, viene creata una copia shadow del processo in esecuzione in circa 10-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="66f10-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="66f10-165">Il processo shadow viene quindi analizzato e viene creato uno snapshot mentre il processo principale rimane in esecuzione e continua a gestire il traffico verso gli utenti.</span><span class="sxs-lookup"><span data-stu-id="66f10-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="66f10-166">Lo snapshot viene quindi caricato in Application Insights insieme agli eventuali file di simboli pertinenti (con estensione pdb) che sono necessari per visualizzare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="66f10-167">Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="66f10-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="66f10-168">Pubblicare i simboli</span><span class="sxs-lookup"><span data-stu-id="66f10-168">Publish symbols</span></span>
<span data-ttu-id="66f10-169">Per poter decodificare le variabili e offrire un'esperienza di debug in Visual Studio, Snapshot Debugger richiede la presenza dei file di simboli nel server di produzione.</span><span class="sxs-lookup"><span data-stu-id="66f10-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="66f10-170">Per impostazione predefinita, la versione 15.2 di Visual Studio 2017 pubblica i simboli per le build di versione durante la pubblicazione nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="66f10-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="66f10-171">Nelle versioni precedenti è necessario aggiungere la riga seguente al file `.pubxml` del profilo di pubblicazione per pubblicare i simboli in modalità versione:</span><span class="sxs-lookup"><span data-stu-id="66f10-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="66f10-172">Per Calcolo di Azure e altri tipi di calcoli, verificare che i file di simboli si trovino nella stessa cartella della DLL dell'applicazione principale (generalmente `wwwroot/bin`) o che siano disponibili nel percorso corrente.</span><span class="sxs-lookup"><span data-stu-id="66f10-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="66f10-173">Compilazioni ottimizzate</span><span class="sxs-lookup"><span data-stu-id="66f10-173">Optimized builds</span></span>
<span data-ttu-id="66f10-174">In alcuni casi le variabili locali non possono essere visualizzate nelle build di versione a causa delle ottimizzazioni applicate durante il processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="66f10-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="66f10-175">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="66f10-175">Troubleshooting</span></span>

<span data-ttu-id="66f10-176">Questi suggerimenti consentono di risolvere i problemi relativi al debugger di snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="66f10-177">Verificare la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="66f10-177">Verify the instrumentation key</span></span>

<span data-ttu-id="66f10-178">Verificare di usare la chiave di strumentazione corretta nell'applicazione pubblicata.</span><span class="sxs-lookup"><span data-stu-id="66f10-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="66f10-179">Application Insights in genere legge la chiave di strumentazione dal file ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="66f10-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="66f10-180">Verificare che il valore sia lo stesso della chiave di strumentazione per la risorsa di Application Insights visualizzata nel portale.</span><span class="sxs-lookup"><span data-stu-id="66f10-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="66f10-181">Controllare i log dell'utilità di caricamento</span><span class="sxs-lookup"><span data-stu-id="66f10-181">Check the uploader logs</span></span>

<span data-ttu-id="66f10-182">Dopo la creazione di uno snapshot, un file di minidump (DMP) viene creato sul disco.</span><span class="sxs-lookup"><span data-stu-id="66f10-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="66f10-183">Un processo di caricamento separato prende il file di minidump e lo carica, con i file PDB associati, nella risorsa di archiviazione Debugger di snapshot di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="66f10-184">Il minidump, dopo essere stato correttamente caricato, viene eliminato dal disco.</span><span class="sxs-lookup"><span data-stu-id="66f10-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="66f10-185">I file di log dell'utilità di caricamento del minidump vengono conservati sul disco.</span><span class="sxs-lookup"><span data-stu-id="66f10-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="66f10-186">In un ambiente del servizio app questi log si trovano in `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="66f10-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="66f10-187">Usare il sito di gestione di Kudu per il servizio app per trovare questi file di log.</span><span class="sxs-lookup"><span data-stu-id="66f10-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="66f10-188">Aprire l'applicazione del servizio app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f10-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="66f10-189">Selezionare il pannello **Strumenti avanzati** o cercare **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="66f10-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="66f10-190">Fare clic su **Vai**.</span><span class="sxs-lookup"><span data-stu-id="66f10-190">Click **Go**.</span></span>
4. <span data-ttu-id="66f10-191">Nell'elenco a discesa **Console di debug** selezionare **CMD**.</span><span class="sxs-lookup"><span data-stu-id="66f10-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="66f10-192">Fare clic su **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="66f10-192">Click **LogFiles**.</span></span>

<span data-ttu-id="66f10-193">Verrà visualizzato almeno un file con il nome che inizia con `Uploader_` e l'estensione `.log`.</span><span class="sxs-lookup"><span data-stu-id="66f10-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="66f10-194">Fare clic sull'icona appropriata per scaricare i file di log o aprirli in un browser.</span><span class="sxs-lookup"><span data-stu-id="66f10-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="66f10-195">Il nome file include il nome del computer.</span><span class="sxs-lookup"><span data-stu-id="66f10-195">The file name includes the machine name.</span></span> <span data-ttu-id="66f10-196">Se l'istanza del servizio app è ospitata in più di un computer, è presente un file di log separato per ogni computer.</span><span class="sxs-lookup"><span data-stu-id="66f10-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="66f10-197">Quando l'utilità di caricamento rileva un nuovo file di minidump file, il file viene registrato nel file di log.</span><span class="sxs-lookup"><span data-stu-id="66f10-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="66f10-198">Ecco un esempio di caricamento corretto:</span><span class="sxs-lookup"><span data-stu-id="66f10-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="66f10-199">Nell'esempio precedente la chiave di strumentazione è `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="66f10-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="66f10-200">Questo valore deve corrispondere alla chiave di strumentazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="66f10-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="66f10-201">Il minidump è associato a uno snapshot con l'ID `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="66f10-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="66f10-202">Sarà possibile usare questo ID in seguito per individuare i dati di telemetria delle eccezioni associati in Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="66f10-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="66f10-203">L'utilità di caricamento cerca i nuovi file PDB ogni 15 minuti circa.</span><span class="sxs-lookup"><span data-stu-id="66f10-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="66f10-204">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="66f10-204">Here's an example:</span></span>

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

<span data-ttu-id="66f10-205">Per le applicazioni _non_ ospitate nel servizio app, i log di caricamento sono nella stessa cartella dei minidump: `%TEMP%\Dumps\<ikey>` (dove `<ikey>` è la chiave di strumentazione).</span><span class="sxs-lookup"><span data-stu-id="66f10-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="66f10-206">Usare la ricerca di Application Insights per trovare le eccezioni con gli snapshot</span><span class="sxs-lookup"><span data-stu-id="66f10-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="66f10-207">Quando viene creato uno snapshot, l'eccezione generata viene contrassegnata con un ID snapshot.</span><span class="sxs-lookup"><span data-stu-id="66f10-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="66f10-208">Quando i dati di telemetria dell'eccezione vengono segnalati ad Application Insights, tale ID snapshot viene incluso come proprietà personalizzata.</span><span class="sxs-lookup"><span data-stu-id="66f10-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="66f10-209">Usando il pannello Ricerca in Application Insights, è possibile trovare tutti i dati di telemetria con la proprietà personalizzata `ai.snapshot.id`.</span><span class="sxs-lookup"><span data-stu-id="66f10-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="66f10-210">Passare alla risorsa di Application Insights nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="66f10-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="66f10-211">Fare clic su **Search**(Cerca).</span><span class="sxs-lookup"><span data-stu-id="66f10-211">Click **Search**.</span></span>
3. <span data-ttu-id="66f10-212">Digitare `ai.snapshot.id` nella casella di testo di ricerca e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="66f10-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Cercare i dati di telemetria con i ID snapshot nel portale](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="66f10-214">Se questa ricerca non restituisce risultati, significa che nessuno snapshot è stato segnalato ad Application Insights per l'applicazione nell'intervallo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="66f10-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="66f10-215">Per cercare uno specifico ID snapshot dei log di caricamento, digitare tale ID nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="66f10-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="66f10-216">Se non è possibile trovare dati di telemetria per uno snapshot che è stato sicuramente caricato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="66f10-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="66f10-217">Controllare di esaminare la risorsa di Application Insights corretta verificando la chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="66f10-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="66f10-218">Usando il timestamp del log di caricamento, modificare il filtro Intervallo di tempo della ricerca per coprire tale intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="66f10-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="66f10-219">Se ancora non vengono visualizzate eccezioni con tale ID snapshot, significa che i dati di telemetria dell'eccezione non sono stati segnalati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="66f10-220">Questa situazione si può verificare se l'applicazione ha subito un arresto anomalo del sistema dopo avere acquisito lo snapshot, ma prima di segnalare i dati di telemetria dell'eccezione.</span><span class="sxs-lookup"><span data-stu-id="66f10-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="66f10-221">In questo caso, controllare i log del servizio app in `Diagnose and solve problems` per accertare se si sono verificati riavvi non previsti o eccezioni non gestite.</span><span class="sxs-lookup"><span data-stu-id="66f10-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66f10-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66f10-222">Next steps</span></span>

* <span data-ttu-id="66f10-223">[Impostare punti di ancoraggio nel codice](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) per ottenere gli snapshot senza attendere un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="66f10-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="66f10-224">L'articolo [Diagnosticare eccezioni nelle app Web](app-insights-asp-net-exceptions.md) spiega come rendere visibile un maggior numero di eccezioni in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66f10-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="66f10-225">Il [rilevamento intelligente](app-insights-proactive-diagnostics.md) rileva automaticamente le anomalie delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="66f10-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
