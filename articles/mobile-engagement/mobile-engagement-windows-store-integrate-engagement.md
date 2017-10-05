---
title: Integrazione di Engagement SDK per app universali di Windows
description: Come integrare Azure Mobile Engagement con le app universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="b8ad8-103">Integrazione di Engagement SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="b8ad8-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8ad8-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="b8ad8-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="b8ad8-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b8ad8-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="b8ad8-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b8ad8-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="b8ad8-107">Android</span><span class="sxs-lookup"><span data-stu-id="b8ad8-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="b8ad8-108">Questa procedura descrive il modo più semplice per attivare le funzioni di analisi e monitoraggio di Engagement in un'applicazione universale di Windows.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="b8ad8-109">I passaggi seguenti sono sufficienti per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="b8ad8-110">La segnalazione dei log necessari per calcolare altre statistiche quali eventi, errori e processi deve essere eseguita manualmente mediante l'API di Engagement (vedere [Come usare l'API di Engagement in un'app universale di Windows](mobile-engagement-windows-store-use-engagement-api.md) ) poiché queste statistiche dipendono dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="b8ad8-111">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="b8ad8-111">Supported versions</span></span>
<span data-ttu-id="b8ad8-112">Mobile Engagement SDK per app universali di Windows può essere integrato solo nelle applicazioni Windows Runtime e UWP (Universal Windows Platform) per:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="b8ad8-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="b8ad8-113">Windows 8</span></span>
* <span data-ttu-id="b8ad8-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b8ad8-114">Windows 8.1</span></span>
* <span data-ttu-id="b8ad8-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b8ad8-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="b8ad8-116">Windows 10 (versioni per desktop e portatili)</span><span class="sxs-lookup"><span data-stu-id="b8ad8-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="b8ad8-117">Se si usa Windows Phone Silverlight come piattaforma di destinazione, fare riferimento alla [procedura per l'integrazione di Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="b8ad8-117">If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="b8ad8-118">Installare Mobile Engagement SDK per app universali</span><span class="sxs-lookup"><span data-stu-id="b8ad8-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="b8ad8-119">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="b8ad8-119">All platforms</span></span>
<span data-ttu-id="b8ad8-120">Mobile Engagement SDK per app di Windows universali è disponibile come pacchetto NuGet denominato *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="b8ad8-121">È possibile installarlo da Gestione pacchetti NuGet di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="b8ad8-122">Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b8ad8-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="b8ad8-123">NuGet distribuisce automaticamente le risorse SDK nella cartella `Resources` nella radice del progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="b8ad8-124">Applicazioni UWP di Windows 10</span><span class="sxs-lookup"><span data-stu-id="b8ad8-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="b8ad8-125">NuGet non esegue ancora la distribuzione automatica di risorse SDK in applicazioni UWP.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="b8ad8-126">Fino a quando la funzione di distribuzione delle risorse non verrà reintrodotta in NuGet, sarà necessario eseguire questa operazione manualmente:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="b8ad8-127">Aprire Esplora file.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="b8ad8-128">Passare al percorso seguente (**x.x.x** è la versione di Mobile Engagement che si sta installando): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="b8ad8-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="b8ad8-129">Trascinare la cartella **Risorse** da Esplora file alla radice del progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="b8ad8-130">In Visual Studio selezionare il progetto e attivare l'icona **Mostra tutti i file** nella parte superiore di **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="b8ad8-131">Alcuni file non sono inclusi nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-131">Some files are not included in the project.</span></span> <span data-ttu-id="b8ad8-132">Per importarli tutti contemporaneamente, fare clic con il pulsante destro del mouse su **Risorse** e scegliere **Escludi dal progetto**, quindi fare nuovamente clic con il pulsante destro del mouse su **Risorse** e scegliere **Includi nel progetto** per includere l'intera cartella.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="b8ad8-133">Tutti i file della cartella **Risorse** sono ora inclusi nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="b8ad8-134">Aggiungere le funzionalità</span><span class="sxs-lookup"><span data-stu-id="b8ad8-134">Add the capabilities</span></span>
<span data-ttu-id="b8ad8-135">Engagement SDK richiede alcune funzionalità di Windows SDK per funzionare correttamente.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="b8ad8-136">Aprire il file `Package.appxmanifest` e assicurarsi che le seguenti funzionalità siano dichiarate:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="b8ad8-137">Inizializzare Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="b8ad8-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="b8ad8-138">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="b8ad8-138">Engagement configuration</span></span>
<span data-ttu-id="b8ad8-139">La configurazione di Engagement è centralizzata nel file `Resources\EngagementConfiguration.xml` del progetto.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b8ad8-140">Modificare questo file per specificare:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-140">Edit this file to specify:</span></span>

* <span data-ttu-id="b8ad8-141">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="b8ad8-142">Se si desidera specificarla in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="b8ad8-143">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="b8ad8-144">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="b8ad8-144">Engagement initialization</span></span>
<span data-ttu-id="b8ad8-145">Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="b8ad8-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="b8ad8-146">Questa classe eredita da `Application` e contiene molti metodi importanti.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="b8ad8-147">Verrà inoltre usata per inizializzare Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="b8ad8-148">Modificare il file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="b8ad8-149">Aggiungere quanto segue alle istruzioni `using` :</span><span class="sxs-lookup"><span data-stu-id="b8ad8-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="b8ad8-150">Definire un metodo per condividere l'inizializzazione di Engagement una sola volta per tutte le chiamate:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="b8ad8-151">Chiamare `InitEngagement` nel metodo `OnLaunched`:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="b8ad8-152">Quando l'applicazione viene avviata usando uno schema personalizzato, un'altra applicazione o la riga di comando, viene chiamato il metodo `OnActivated`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="b8ad8-153">È inoltre necessario avviare l'SDK di Engagement quando viene attivata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="b8ad8-154">A tale scopo, eseguire l'override del metodo `OnActivated` :</span><span class="sxs-lookup"><span data-stu-id="b8ad8-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="b8ad8-155">È altamente sconsigliata l'aggiunta dell'inizializzazione di Engagement in un altro punto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-155">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="b8ad8-156">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="b8ad8-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="b8ad8-157">Metodo consigliato: eseguire l'overload delle classi `Page`</span><span class="sxs-lookup"><span data-stu-id="b8ad8-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="b8ad8-158">Per attivare la segnalazione di tutti i log richiesti da Engagement per calcolare utenti, sessioni, attività, arresti anomali e statistiche tecniche, è possibile fare in modo che tutte le sottoclassi `Page` ereditino dalle classi `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="b8ad8-159">Di seguito è riportato un esempio di come ottenere questo risultato per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="b8ad8-160">È possibile procedere allo stesso modo per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="b8ad8-161">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="b8ad8-161">C# Source file</span></span>
<span data-ttu-id="b8ad8-162">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="b8ad8-163">Aggiungere quanto segue alle istruzioni `using`:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="b8ad8-164">Sostituire `Page` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="b8ad8-165">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="b8ad8-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="b8ad8-166">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="b8ad8-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="b8ad8-167">Se la pagina esegue l'override del metodo `OnNavigatedTo`, accertarsi di chiamare `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-167">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="b8ad8-168">In caso contrario, l'attività non verrà segnalata (`EngagementPage` chiama `StartActivity` all'interno del relativo metodo `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="b8ad8-168">Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="b8ad8-169">File XAML</span><span class="sxs-lookup"><span data-stu-id="b8ad8-169">XAML file</span></span>
<span data-ttu-id="b8ad8-170">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="b8ad8-171">Aggiungere le dichiarazioni di spazi dei nomi:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="b8ad8-172">Sostituire `Page` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="b8ad8-173">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="b8ad8-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="b8ad8-174">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="b8ad8-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="b8ad8-175">Eseguire l'override del comportamento predefinito</span><span class="sxs-lookup"><span data-stu-id="b8ad8-175">Override the default behaviour</span></span>
<span data-ttu-id="b8ad8-176">Per impostazione predefinita, il nome della classe della pagina viene indicato come nome dell'attività, senza elementi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="b8ad8-177">Se la classe usa il suffisso "Page", Engagement rimuoverà anche questo elemento.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="b8ad8-178">Se si desidera eseguire l'override del comportamento predefinito per il nome, aggiungere quanto segue al codice:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="b8ad8-179">Se si desidera segnalare alcune informazioni aggiuntive con l'attività, è possibile aggiungere quanto segue al codice:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="b8ad8-180">Questi metodi vengono chiamati dall'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="b8ad8-181">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="b8ad8-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="b8ad8-182">Se non si può o non si vuole eseguire l'overload delle classi `Page`, in alternativa è possibile avviare le attività chiamando direttamente i metodi `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="b8ad8-183">È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="b8ad8-184">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="b8ad8-185">Windows Universal SDK chiama automaticamente il metodo `EndActivity` quando l'applicazione viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-185">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="b8ad8-186">È quindi **ALTAMENTE** consigliabile chiamare il metodo `StartActivity` ogni volta che l'attività dell'utente subisce modifiche e non chiamare **MAI** il metodo `EndActivity`, che segnala al server di Engagement che l'utente ha chiuso l'applicazione e influisce così su tutti i log delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-186">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="b8ad8-187">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="b8ad8-187">Advanced reporting</span></span>
<span data-ttu-id="b8ad8-188">Facoltativamente, è possibile segnalare eventi specifici dell'applicazione, errori e processi. A tale scopo, usare gli altri metodi disponibili nella classe `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="b8ad8-189">L'API di Engagement consente di usare tutte le funzionalità avanzate di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="b8ad8-190">Per altre informazioni, vedere [Come usare l'API di Engagement in un'app di Windows universale](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="b8ad8-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="b8ad8-191">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="b8ad8-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="b8ad8-192">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="b8ad8-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="b8ad8-193">È possibile disabilitare la funzionalità di segnalazione automatica degli arresti anomali di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="b8ad8-194">Quindi, quando si verifica un'eccezione non gestita, Engagement non effettuerà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="b8ad8-195">Se si prevede di disabilitare questa funzionalità, tenere presente che quando si verifica un arresto anomalo non gestito nell'app, Engagement non lo invierà **E** non chiuderà la sessione e i processi.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-195">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="b8ad8-196">Per disabilitare la segnalazione automatica degli arresti anomali, personalizzare la configurazione in base al modo in cui che è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="b8ad8-197">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="b8ad8-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="b8ad8-198">Impostare la segnalazione degli arresti anomali su `false` tra i tag `<reportCrash>` e `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="b8ad8-199">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="b8ad8-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="b8ad8-200">Impostare la segnalazione degli arresti anomali su false usando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="b8ad8-201">Modalità burst</span><span class="sxs-lookup"><span data-stu-id="b8ad8-201">Burst mode</span></span>
<span data-ttu-id="b8ad8-202">Per impostazione predefinita, il servizio Engagement segnala i log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="b8ad8-203">Se l'applicazione segnala i log molto spesso, è consigliabile memorizzarli nel buffer e segnalarli tutti insieme a intervalli regolari (in "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="b8ad8-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="b8ad8-204">A tale scopo, chiamare il metodo:</span><span class="sxs-lookup"><span data-stu-id="b8ad8-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="b8ad8-205">L'argomento è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="b8ad8-206">In qualsiasi momento, se si desidera riattivare la registrazione in tempo reale, chiamare il metodo senza alcun parametro o con il valore 0.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="b8ad8-207">La modalità burst aumenta lievemente la durata della batteria ma ha un impatto su Monitor di Engagement: la durata di tutte le sessioni e di tutti i processi verrà arrotondata alla soglia di burst (di conseguenza, le sessioni e i processi inferiori alla soglia di burst potrebbero non essere visibili).</span><span class="sxs-lookup"><span data-stu-id="b8ad8-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="b8ad8-208">Si consiglia di usare una soglia di burst non maggiore di 30000 (30 secondi).</span><span class="sxs-lookup"><span data-stu-id="b8ad8-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="b8ad8-209">Occorre notare che per i log salvati è previsto un limite di 300 elementi.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="b8ad8-210">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="b8ad8-211">Non è possibile configurare la soglia di burst per un periodo inferiore a 1s.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-211">The burst threshold cannot be configured to a period lesser than 1s.</span></span> <span data-ttu-id="b8ad8-212">Se si tenta di impostare un valore minore, l'SDK mostrerà una traccia con l'errore e verrà reimpostato automaticamente sul valore predefinito, vale a dire, 0s.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-212">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s.</span></span> <span data-ttu-id="b8ad8-213">In questo modo verrà attivato l'SDK per la segnalazione dei log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b8ad8-213">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

