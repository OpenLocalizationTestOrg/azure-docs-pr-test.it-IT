---
title: Integrazione di Mobile Engagement SDK per Windows Phone Silverlight
description: Come integrare Azure Mobile Engagement con le app per Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="8fcf2-103">Integrazione di Mobile Engagement SDK per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8fcf2-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fcf2-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8fcf2-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="8fcf2-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8fcf2-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="8fcf2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="8fcf2-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="8fcf2-107">Android</span><span class="sxs-lookup"><span data-stu-id="8fcf2-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="8fcf2-108">Questa procedura descrive il modo più semplice per attivare le funzioni di analisi e monitoraggio di Azure Mobile Engagement in un'applicazione per Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="8fcf2-109">I passaggi seguenti sono sufficienti per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="8fcf2-110">La segnalazione dei log necessari per calcolare altre statistiche quali eventi, errori e processi deve essere eseguita manualmente mediante l'API di Engagement (vedere [Come usare l'API di Mobile Engagement in Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) ) poiché queste statistiche dipendono dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="8fcf2-111">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="8fcf2-111">Supported versions</span></span>
<span data-ttu-id="8fcf2-112">Mobile Engagement SDK per Windows Silverlight può essere integrato solo nelle applicazioni per:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="8fcf2-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="8fcf2-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="8fcf2-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="8fcf2-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="8fcf2-115">Se si usa Windows Phone 8.1 (non Silverlight) come piattaforma di destinazione, fare riferimento alla [procedura per l'integrazione nelle app universali di Windows](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8fcf2-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="8fcf2-116">Installare Mobile Engagement SDK per Windows Silverlight</span><span class="sxs-lookup"><span data-stu-id="8fcf2-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="8fcf2-117">Mobile Engagement SDK per Windows Silverlight è disponibile come pacchetto NuGet denominato *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="8fcf2-118">È possibile installarlo da Gestione pacchetti NuGet di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="8fcf2-119">Aggiungere le funzionalità</span><span class="sxs-lookup"><span data-stu-id="8fcf2-119">Add the capabilities</span></span>
<span data-ttu-id="8fcf2-120">Engagement SDK richiede alcune funzionalità di Windows SDK per funzionare correttamente. richiede alcune funzionalità di Windows Phone Silverlight SDK per funzionare correttamente.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="8fcf2-121">Aprire il file `WMAppManifest.xml` e assicurarsi che le funzionalità seguenti siano dichiarate nel pannello `Capabilities`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="8fcf2-122">Inizializzare Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="8fcf2-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="8fcf2-123">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="8fcf2-123">Engagement configuration</span></span>
<span data-ttu-id="8fcf2-124">La configurazione di Engagement è centralizzata nel file `Resources\EngagementConfiguration.xml` del progetto.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="8fcf2-125">Modificare questo file per specificare:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-125">Edit this file to specify :</span></span>

* <span data-ttu-id="8fcf2-126">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="8fcf2-127">Se si desidera specificarla in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="8fcf2-128">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="8fcf2-129">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="8fcf2-129">Engagement initialization</span></span>
<span data-ttu-id="8fcf2-130">Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="8fcf2-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="8fcf2-131">Questa classe eredita da `Application` e contiene molti metodi importanti.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="8fcf2-132">Verrà inoltre usata per inizializzare Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="8fcf2-133">Modificare il file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="8fcf2-134">Aggiungere quanto segue alle istruzioni `using`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="8fcf2-135">Inserire `EngagementAgent.Instance.Init` nel metodo `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="8fcf2-136">Inserire `EngagementAgent.Instance.OnActivated` nel metodo `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="8fcf2-137">È altamente sconsigliata l'aggiunta dell'inizializzazione di Engagement in un altro punto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="8fcf2-138">Tenere tuttavia presente che il metodo `EngagementAgent.Instance.Init` viene eseguito in un thread dedicato e non nel thread dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="8fcf2-139">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="8fcf2-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="8fcf2-140">Metodo consigliato: eseguire l'overload delle classi `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="8fcf2-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="8fcf2-141">Per attivare la segnalazione di tutti i log richiesti da Engagement per calcolare utenti, sessioni, attività, arresti anomali e statistiche tecniche, è possibile fare in modo che tutte le sottoclassi `PhoneApplicationPage` ereditino dalle classi `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="8fcf2-142">Di seguito è riportato un esempio di come ottenere questo risultato per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="8fcf2-143">È possibile procedere allo stesso modo per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="8fcf2-144">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="8fcf2-144">C# Source file</span></span>
<span data-ttu-id="8fcf2-145">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="8fcf2-146">Aggiungere quanto segue alle istruzioni `using`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="8fcf2-147">Sostituire `PhoneApplicationPage` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="8fcf2-148">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8fcf2-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="8fcf2-149">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8fcf2-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="8fcf2-150">Se la pagina eredita dal metodo `OnNavigatedTo`, fare attenzione a consentire la chiamata `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="8fcf2-151">In caso contrario, l'attività non verrà segnalata.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="8fcf2-152">In effetti, `EngagementPage` chiama `StartActivity` all'interno del metodo `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="8fcf2-153">File XAML</span><span class="sxs-lookup"><span data-stu-id="8fcf2-153">XAML file</span></span>
<span data-ttu-id="8fcf2-154">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="8fcf2-155">Aggiungere quanto segue alle dichiarazioni di spazi dei nomi:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="8fcf2-156">Sostituire `phone:PhoneApplicationPage` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="8fcf2-157">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8fcf2-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="8fcf2-158">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8fcf2-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="8fcf2-159">Sostituire il comportamento predefinito</span><span class="sxs-lookup"><span data-stu-id="8fcf2-159">Override the default behavior</span></span>
<span data-ttu-id="8fcf2-160">Per impostazione predefinita, il nome della classe della pagina viene indicato come nome dell'attività, senza elementi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="8fcf2-161">Se la classe usa il suffisso "Page", Engagement rimuoverà anche questo elemento.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="8fcf2-162">Se si desidera eseguire l'override del comportamento predefinito per il nome, aggiungere quanto segue al codice:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="8fcf2-163">Se si desidera segnalare alcune informazioni aggiuntive con l'attività, è possibile aggiungere quanto segue al codice:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="8fcf2-164">Questi metodi vengono chiamati dall'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="8fcf2-165">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="8fcf2-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="8fcf2-166">Se non si può o non si vuole eseguire l'overload delle classi `PhoneApplicationPage`, in alternativa è possibile avviare le attività chiamando direttamente i metodi `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="8fcf2-167">È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` di PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="8fcf2-168">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="8fcf2-169">L'SDK chiama automaticamente il metodo `EndActivity` quando viene chiusa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="8fcf2-170">È quindi **ALTAMENTE** consigliabile chiamare il metodo `StartActivity` ogni volta che l'attività dell'utente cambia e non chiamare **MAI** il metodo `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="8fcf2-171">Questo metodo invia un messaggio al server di Engagement che segnala che l'utente ha chiuso l'applicazione e ciò influirà su tutti i log delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="8fcf2-172">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="8fcf2-172">Advanced reporting</span></span>
<span data-ttu-id="8fcf2-173">Facoltativamente, è possibile segnalare eventi specifici dell'applicazione, errori e processi. A tale scopo, usare gli altri metodi disponibili nella classe `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="8fcf2-174">L'API di Engagement consente di usare tutte le funzionalità avanzate di Engagement.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="8fcf2-175">Per altre informazioni, vedere [Come usare l'API di Engagement in Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="8fcf2-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="8fcf2-176">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="8fcf2-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="8fcf2-177">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="8fcf2-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="8fcf2-178">È possibile disabilitare la funzionalità di segnalazione automatica degli arresti anomali di Engagement.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="8fcf2-179">Quindi, quando si verifica un'eccezione non gestita, Engagement non effettuerà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="8fcf2-180">Se si prevede di disabilitare questa funzionalità, tenere presente che in caso di arresto anomalo non gestito nell'app, Engagement non lo invierà **E** non chiuderà la sessione e i processi.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="8fcf2-181">Per disabilitare la segnalazione automatica degli arresti anomali, personalizzare la configurazione a seconda del modo in cui è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="8fcf2-182">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="8fcf2-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="8fcf2-183">Impostare la segnalazione degli arresti anomali su `false` tra i tag `<reportCrash>` e `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="8fcf2-184">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="8fcf2-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="8fcf2-185">Impostare la segnalazione degli arresti anomali su false usando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="8fcf2-186">Modalità burst</span><span class="sxs-lookup"><span data-stu-id="8fcf2-186">Burst mode</span></span>
<span data-ttu-id="8fcf2-187">Per impostazione predefinita, il servizio Engagement segnala i log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="8fcf2-188">Se l'applicazione segnala i log molto spesso, è consigliabile memorizzarli nel buffer e segnalarli tutti insieme a intervalli regolari (in "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="8fcf2-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="8fcf2-189">A tale scopo, chiamare il metodo:</span><span class="sxs-lookup"><span data-stu-id="8fcf2-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="8fcf2-190">L'argomento è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="8fcf2-191">In qualsiasi momento, se si desidera riattivare la registrazione in tempo reale, chiamare il metodo senza alcun parametro o con il valore 0.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="8fcf2-192">La modalità burst aumenta lievemente la durata della batteria ma ha un impatto su Monitor di Engagement: la durata di tutte le sessioni e di tutti i processi verrà arrotondata alla soglia di burst (di conseguenza, le sessioni e i processi inferiori alla soglia di burst potrebbero non essere visibili).</span><span class="sxs-lookup"><span data-stu-id="8fcf2-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="8fcf2-193">Si consiglia di usare una soglia di burst non maggiore di 30000 (30 secondi).</span><span class="sxs-lookup"><span data-stu-id="8fcf2-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="8fcf2-194">Occorre notare che per i log salvati è previsto un limite di 300 elementi.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="8fcf2-195">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="8fcf2-196">La soglia di burst non può essere configurata per un periodo inferiore a un secondo.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="8fcf2-197">Se si tenta di impostare un valore minore, l'SDK mostrerà una traccia con l'errore e verrà ripristinato automaticamente il valore predefinito, ovvero zero secondi.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="8fcf2-198">In questo modo verrà attivato l'SDK per la segnalazione dei log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="8fcf2-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

