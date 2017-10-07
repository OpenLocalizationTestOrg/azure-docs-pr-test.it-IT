---
title: Integrazione di Universal App Engagement SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement con App universali di Windows
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
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="50fdf-103">Integrazione di Engagement SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="50fdf-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50fdf-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="50fdf-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="50fdf-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="50fdf-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="50fdf-106">iOS</span><span class="sxs-lookup"><span data-stu-id="50fdf-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="50fdf-107">Android</span><span class="sxs-lookup"><span data-stu-id="50fdf-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="50fdf-108">Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e il monitoraggio funzioni nell'applicazione Windows universale.</span><span class="sxs-lookup"><span data-stu-id="50fdf-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="50fdf-109">Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals.</span><span class="sxs-lookup"><span data-stu-id="50fdf-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="50fdf-110">Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) poiché Queste statistiche sono dipende dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="50fdf-111">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="50fdf-111">Supported versions</span></span>
<span data-ttu-id="50fdf-112">Hello Mobile Engagement SDK per App universali di Windows può essere integrato solo in Windows Runtime e nelle applicazioni di Universal Windows Platform destinazione:</span><span class="sxs-lookup"><span data-stu-id="50fdf-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="50fdf-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="50fdf-113">Windows 8</span></span>
* <span data-ttu-id="50fdf-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="50fdf-114">Windows 8.1</span></span>
* <span data-ttu-id="50fdf-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="50fdf-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="50fdf-116">Windows 10 (versioni per desktop e portatili)</span><span class="sxs-lookup"><span data-stu-id="50fdf-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="50fdf-117">Se si sono destinati a Windows Phone Silverlight, vedere toohello [procedura di integrazione di Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="50fdf-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="50fdf-118">Installare hello Mobile Engagement SDK di App universale</span><span class="sxs-lookup"><span data-stu-id="50fdf-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="50fdf-119">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="50fdf-119">All platforms</span></span>
<span data-ttu-id="50fdf-120">Hello Engagement SDK per Windows Universal App per dispositivi mobili è disponibile come pacchetto Nuget chiamato *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="50fdf-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="50fdf-121">È possibile installarlo dal hello Gestione pacchetti Nuget di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50fdf-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="50fdf-122">Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="50fdf-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="50fdf-123">NuGet consente di distribuire automaticamente le risorse SDK hello in hello `Resources` cartella hello radice del progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="50fdf-124">Applicazioni UWP di Windows 10</span><span class="sxs-lookup"><span data-stu-id="50fdf-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="50fdf-125">NuGet non distribuisce automaticamente le risorse SDK hello nell'applicazione UWP ancora.</span><span class="sxs-lookup"><span data-stu-id="50fdf-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="50fdf-126">È possibile toodo manualmente fino a ottenere la distribuzione di risorse viene reintrodotto in NuGet:</span><span class="sxs-lookup"><span data-stu-id="50fdf-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="50fdf-127">Aprire Esplora file.</span><span class="sxs-lookup"><span data-stu-id="50fdf-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="50fdf-128">Passare toohello seguente posizione (**x.x. x** versione hello di coinvolgimento che si sta installando): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x. x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="50fdf-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="50fdf-129">Trascinamento della selezione hello **risorse** cartella hello file Esplora toohello radice del progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50fdf-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="50fdf-130">In Visual Studio selezionare il progetto e attivare hello **Mostra tutti i file** icona sopra hello **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="50fdf-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="50fdf-131">Alcuni file non sono inclusi nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="50fdf-131">Some files are not included in hello project.</span></span> <span data-ttu-id="50fdf-132">tooimport li contemporaneamente, fare clic sul hello **risorse** cartella **Escludi dal progetto** quindi un altro a destra fare clic su hello **risorse** cartella **inclusione nel progetto** toore-includono l'intera cartella hello.</span><span class="sxs-lookup"><span data-stu-id="50fdf-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="50fdf-133">Tutti i file da hello **risorse** cartella sono ora inclusi nel progetto.</span><span class="sxs-lookup"><span data-stu-id="50fdf-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="50fdf-134">Aggiungere le funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="50fdf-134">Add hello capabilities</span></span>
<span data-ttu-id="50fdf-135">Hello Engagement SDK richiede alcune funzionalità di Windows SDK di hello in ordine toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="50fdf-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="50fdf-136">Aprire il `Package.appxmanifest` file e assicurarsi che vengono dichiarati tale hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="50fdf-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="50fdf-137">Inizializzare hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="50fdf-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="50fdf-138">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="50fdf-138">Engagement configuration</span></span>
<span data-ttu-id="50fdf-139">configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.</span><span class="sxs-lookup"><span data-stu-id="50fdf-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="50fdf-140">Modificare questo toospecify file:</span><span class="sxs-lookup"><span data-stu-id="50fdf-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="50fdf-141">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="50fdf-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="50fdf-142">Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="50fdf-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="50fdf-143">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="50fdf-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="50fdf-144">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="50fdf-144">Engagement initialization</span></span>
<span data-ttu-id="50fdf-145">Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="50fdf-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="50fdf-146">Questa classe eredita da `Application` e contiene molti metodi importanti.</span><span class="sxs-lookup"><span data-stu-id="50fdf-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="50fdf-147">Verrà inoltre utilizzato tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="50fdf-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="50fdf-148">Modificare hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="50fdf-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="50fdf-149">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="50fdf-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="50fdf-150">Definire un'inizializzazione di Engagement hello tooshare metodo una volta per tutte le chiamate:</span><span class="sxs-lookup"><span data-stu-id="50fdf-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="50fdf-151">Chiamare `InitEngagement` in hello `OnLaunched` metodo:</span><span class="sxs-lookup"><span data-stu-id="50fdf-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="50fdf-152">Quando l'applicazione viene avviata con uno schema personalizzato, un altro tipo di riga di comando dell'applicazione o hello hello quindi `OnActivated` metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="50fdf-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="50fdf-153">Quando viene attivato l'app, è inoltre necessario tooinitiate hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="50fdf-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="50fdf-154">toodo in tal caso, eseguire l'override `OnActivated` metodo:</span><span class="sxs-lookup"><span data-stu-id="50fdf-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="50fdf-155">Non è fortemente consigliabile è tooadd hello Engagement inizializzazione in un'altra posizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="50fdf-156">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="50fdf-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="50fdf-157">Metodo consigliato: eseguire l'overload delle classi `Page`</span><span class="sxs-lookup"><span data-stu-id="50fdf-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="50fdf-158">Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `Page` sottoclassi ereditano hello `EngagementPage` classi.</span><span class="sxs-lookup"><span data-stu-id="50fdf-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="50fdf-159">Di seguito è riportato un esempio di come toodo per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="50fdf-160">È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="50fdf-161">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="50fdf-161">C# Source file</span></span>
<span data-ttu-id="50fdf-162">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="50fdf-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="50fdf-163">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="50fdf-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="50fdf-164">Sostituire `Page` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="50fdf-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="50fdf-165">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="50fdf-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="50fdf-166">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="50fdf-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="50fdf-167">Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="50fdf-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="50fdf-168">In caso contrario, attività hello non verranno segnalati (hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="50fdf-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="50fdf-169">File XAML</span><span class="sxs-lookup"><span data-stu-id="50fdf-169">XAML file</span></span>
<span data-ttu-id="50fdf-170">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="50fdf-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="50fdf-171">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="50fdf-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="50fdf-172">Sostituire `Page` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="50fdf-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="50fdf-173">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="50fdf-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="50fdf-174">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="50fdf-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="50fdf-175">Eseguire l'override di comportamento predefinito di hello</span><span class="sxs-lookup"><span data-stu-id="50fdf-175">Override hello default behaviour</span></span>
<span data-ttu-id="50fdf-176">Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="50fdf-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="50fdf-177">Se la classe hello utilizza il suffisso "Pagina" hello, Engagement verrà inoltre rimosso.</span><span class="sxs-lookup"><span data-stu-id="50fdf-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="50fdf-178">Se si desidera il comportamento predefinito di hello toooverride per nome hello, è sufficiente aggiungere questo codice tooyour:</span><span class="sxs-lookup"><span data-stu-id="50fdf-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="50fdf-179">Se si desidera tooreport alcune informazioni aggiuntive con l'attività, è possibile aggiungere questo codice tooyour:</span><span class="sxs-lookup"><span data-stu-id="50fdf-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="50fdf-180">Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.</span><span class="sxs-lookup"><span data-stu-id="50fdf-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="50fdf-181">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="50fdf-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="50fdf-182">Se non è possibile o non si desidera toooverload il `Page` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="50fdf-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="50fdf-183">È consigliabile toocall `StartActivity` all'interno del `OnNavigatedTo` metodo della pagina.</span><span class="sxs-lookup"><span data-stu-id="50fdf-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="50fdf-184">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="50fdf-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="50fdf-185">SDK di Windows universale Hello chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="50fdf-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="50fdf-186">È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` (metodo), questo metodo invia tooEngagement server che l'utente corrente dispone di un'applicazione hello lasciare, ciò influisce su tutti i log dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="50fdf-187">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="50fdf-187">Advanced reporting</span></span>
<span data-ttu-id="50fdf-188">Facoltativamente, è opportuno tooreport eventi specifici di applicazione, gli errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="50fdf-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="50fdf-189">Hello Engagement API consente toouse tutte le funzionalità avanzate di Engagement.</span><span class="sxs-lookup"><span data-stu-id="50fdf-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="50fdf-190">Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="50fdf-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="50fdf-191">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="50fdf-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="50fdf-192">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="50fdf-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="50fdf-193">È possibile disabilitare hello automatica degli arresti anomali delle funzionalità di impegno report.</span><span class="sxs-lookup"><span data-stu-id="50fdf-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="50fdf-194">Quindi, quando si verifica un'eccezione non gestita, Engagement non effettuerà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="50fdf-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="50fdf-195">Se si prevede di toodisable questa funzionalità, tenere presente che quando si verifica un arresto anomalo del sistema non gestita nell'app, Engagement non invierà arresto anomalo di hello **AND** non comporta la chiusura della sessione hello e processi.</span><span class="sxs-lookup"><span data-stu-id="50fdf-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="50fdf-196">toodisable automatico segnalazioni di arresti anomali, personalizzare solo la configurazione a seconda della modalità di hello è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="50fdf-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="50fdf-197">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="50fdf-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="50fdf-198">Impostare i report dell'arresto anomalo troppo`false` tra `<reportCrash>` e `</reportCrash>` tag.</span><span class="sxs-lookup"><span data-stu-id="50fdf-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="50fdf-199">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="50fdf-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="50fdf-200">Impostare toofalse di arresto anomalo di report utilizzando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="50fdf-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="50fdf-201">Modalità burst</span><span class="sxs-lookup"><span data-stu-id="50fdf-201">Burst mode</span></span>
<span data-ttu-id="50fdf-202">Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="50fdf-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="50fdf-203">Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="50fdf-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="50fdf-204">toodo in tal caso, chiamare il metodo hello:</span><span class="sxs-lookup"><span data-stu-id="50fdf-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="50fdf-205">argomento Hello è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="50fdf-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="50fdf-206">In qualsiasi momento, se si desidera registrare in tempo reale di tooreactivate hello, chiamare solo metodo hello senza alcun parametro, o con valore 0 hello.</span><span class="sxs-lookup"><span data-stu-id="50fdf-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="50fdf-207">Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile).</span><span class="sxs-lookup"><span data-stu-id="50fdf-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="50fdf-208">È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="50fdf-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="50fdf-209">È necessario tenere presente che registri salvati sono elementi too300 limitato toobe.</span><span class="sxs-lookup"><span data-stu-id="50fdf-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="50fdf-210">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="50fdf-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="50fdf-211">soglia di potenziamento Hello non può essere configurata tooa periodo minore 1s.</span><span class="sxs-lookup"><span data-stu-id="50fdf-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="50fdf-212">Se si tenta pertanto toodo, hello SDK sarà visualizzare una traccia con l'errore hello e verrà automaticamente reimpostato valore predefinito di toohello, ad esempio, 0.</span><span class="sxs-lookup"><span data-stu-id="50fdf-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="50fdf-213">In questo modo verrà attivata hello SDK tooreport hello log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="50fdf-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

