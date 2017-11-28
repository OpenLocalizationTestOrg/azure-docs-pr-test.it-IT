---
title: Integrazione di Phone Silverlight Engagement SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement con le app di Windows Phone Silverlight
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
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="5c65c-103">Integrazione di Mobile Engagement SDK per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5c65c-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c65c-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="5c65c-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="5c65c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5c65c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="5c65c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5c65c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="5c65c-107">Android</span><span class="sxs-lookup"><span data-stu-id="5c65c-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="5c65c-108">Questa procedura descrive hello più semplice modo tooactivate Azure Mobile Engagement Analitica e funzioni nell'applicazione Windows Phone Silverlight di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="5c65c-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="5c65c-109">Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals.</span><span class="sxs-lookup"><span data-stu-id="5c65c-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="5c65c-110">Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API nelle applicazioni Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) di seguito) poiché queste statistiche sono dipendenti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c65c-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="5c65c-111">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="5c65c-111">Supported versions</span></span>
<span data-ttu-id="5c65c-112">Hello Mobile Engagement SDK per Silverlight per Windows può essere integrato solo in applicazioni destinate a:</span><span class="sxs-lookup"><span data-stu-id="5c65c-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="5c65c-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="5c65c-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="5c65c-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="5c65c-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="5c65c-115">Se si sono destinati a Windows Phone 8.1 (non Silverlight), fare riferimento toohello [procedura di integrazione di Windows universale](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="5c65c-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="5c65c-116">Installare hello Mobile Engagement Silverlight SDK</span><span class="sxs-lookup"><span data-stu-id="5c65c-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="5c65c-117">Hello Mobile Engagement SDK per Silverlight per Windows è disponibile come pacchetto Nuget chiamato *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="5c65c-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="5c65c-118">È possibile installarlo dal hello Gestione pacchetti Nuget di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c65c-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="5c65c-119">Aggiungere le funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="5c65c-119">Add hello capabilities</span></span>
<span data-ttu-id="5c65c-120">Hello Engagement SDK richiede alcune funzionalità di Windows Phone Silverlight SDK di hello in ordine toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="5c65c-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="5c65c-121">Aprire il `WMAppManifest.xml` file e assicurarsi che tale hello seguenti funzionalità vengono dichiarati in hello `Capabilities` pannello:</span><span class="sxs-lookup"><span data-stu-id="5c65c-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="5c65c-122">Inizializzare hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="5c65c-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="5c65c-123">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="5c65c-123">Engagement configuration</span></span>
<span data-ttu-id="5c65c-124">configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.</span><span class="sxs-lookup"><span data-stu-id="5c65c-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="5c65c-125">Modificare questo toospecify file:</span><span class="sxs-lookup"><span data-stu-id="5c65c-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="5c65c-126">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="5c65c-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="5c65c-127">Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="5c65c-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="5c65c-128">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="5c65c-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="5c65c-129">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="5c65c-129">Engagement initialization</span></span>
<span data-ttu-id="5c65c-130">Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="5c65c-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="5c65c-131">Questa classe eredita da `Application` e contiene molti metodi importanti.</span><span class="sxs-lookup"><span data-stu-id="5c65c-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="5c65c-132">Verrà inoltre utilizzato tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="5c65c-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="5c65c-133">Modificare hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="5c65c-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="5c65c-134">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="5c65c-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5c65c-135">Inserisci `EngagementAgent.Instance.Init` in hello `Application_Launching` metodo:</span><span class="sxs-lookup"><span data-stu-id="5c65c-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="5c65c-136">Inserisci `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` metodo:</span><span class="sxs-lookup"><span data-stu-id="5c65c-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="5c65c-137">Non è fortemente consigliabile è tooadd hello Engagement inizializzazione in un'altra posizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c65c-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="5c65c-138">Tuttavia, tenere presente che hello `EngagementAgent.Instance.Init` metodo viene eseguito in un thread dedicato e non su hello thread dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="5c65c-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="5c65c-139">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="5c65c-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="5c65c-140">Metodo consigliato: eseguire l'overload delle classi `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="5c65c-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="5c65c-141">Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `PhoneApplicationPage` sottoclassi ereditano hello `EngagementPage` classi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="5c65c-142">Di seguito è riportato un esempio di come toodo per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c65c-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="5c65c-143">È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c65c-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="5c65c-144">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="5c65c-144">C# Source file</span></span>
<span data-ttu-id="5c65c-145">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="5c65c-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="5c65c-146">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="5c65c-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5c65c-147">Sostituire `PhoneApplicationPage` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="5c65c-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="5c65c-148">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5c65c-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="5c65c-149">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5c65c-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="5c65c-150">Se la pagina eredita da hello `OnNavigatedTo` (metodo), essere hello toolet attenzione `base.OnNavigatedTo(e)` chiamare.</span><span class="sxs-lookup"><span data-stu-id="5c65c-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="5c65c-151">In caso contrario, non verranno segnalati attività hello.</span><span class="sxs-lookup"><span data-stu-id="5c65c-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="5c65c-152">In effetti, hello `EngagementPage` chiama `StartActivity` all'interno di hello `OnNavigatedTo` metodo.</span><span class="sxs-lookup"><span data-stu-id="5c65c-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="5c65c-153">File XAML</span><span class="sxs-lookup"><span data-stu-id="5c65c-153">XAML file</span></span>
<span data-ttu-id="5c65c-154">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="5c65c-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="5c65c-155">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="5c65c-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="5c65c-156">Sostituire `phone:PhoneApplicationPage` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="5c65c-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="5c65c-157">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5c65c-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="5c65c-158">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5c65c-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="5c65c-159">Ignorare il comportamento predefinito di hello</span><span class="sxs-lookup"><span data-stu-id="5c65c-159">Override hello default behavior</span></span>
<span data-ttu-id="5c65c-160">Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="5c65c-161">Se la classe hello utilizza il suffisso "Pagina" hello, Engagement verrà inoltre rimosso.</span><span class="sxs-lookup"><span data-stu-id="5c65c-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="5c65c-162">Se si desidera il comportamento predefinito di hello toooverride per nome hello, è sufficiente aggiungere questo codice tooyour:</span><span class="sxs-lookup"><span data-stu-id="5c65c-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="5c65c-163">Se si desiderano tooreport alcune informazioni aggiuntive con l'attività, è possibile aggiungere questo codice tooyour:</span><span class="sxs-lookup"><span data-stu-id="5c65c-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="5c65c-164">Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.</span><span class="sxs-lookup"><span data-stu-id="5c65c-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="5c65c-165">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="5c65c-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="5c65c-166">Se non è possibile o non si desidera toooverload il `PhoneApplicationPage` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="5c65c-167">È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` di PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="5c65c-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="5c65c-168">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="5c65c-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="5c65c-169">Hello SDK chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="5c65c-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="5c65c-170">È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` metodo.</span><span class="sxs-lookup"><span data-stu-id="5c65c-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="5c65c-171">Questo metodo invia un server di Engagement toohello di messaggio che l'utente corrente hello ha lasciato l'applicazione hello e ciò influisce su tutti i log applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5c65c-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="5c65c-172">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="5c65c-172">Advanced reporting</span></span>
<span data-ttu-id="5c65c-173">Facoltativamente, è opportuno tooreport eventi specifici di applicazione, gli errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="5c65c-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="5c65c-174">Hello Engagement API consente toouse tutte le funzionalità avanzate di Engagement.</span><span class="sxs-lookup"><span data-stu-id="5c65c-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="5c65c-175">Per ulteriori informazioni, vedere [come toouse hello avanzate Mobile Engagement tag API nelle applicazioni Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="5c65c-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="5c65c-176">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="5c65c-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="5c65c-177">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="5c65c-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="5c65c-178">È possibile disabilitare hello automatica degli arresti anomali delle funzionalità di impegno report.</span><span class="sxs-lookup"><span data-stu-id="5c65c-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="5c65c-179">Quindi, quando si verifica un'eccezione non gestita, Engagement non effettuerà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="5c65c-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="5c65c-180">Se si prevede di toodisable questa funzionalità, tenere presente che quando si verifica un arresto anomalo del sistema non gestita nell'app, Engagement non invierà arresto anomalo di hello **AND** non comporta la chiusura della sessione hello e processi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="5c65c-181">toodisable automatico segnalazioni di arresti anomali, personalizzare solo la configurazione a seconda della modalità di hello è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="5c65c-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="5c65c-182">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="5c65c-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="5c65c-183">Impostare i report dell'arresto anomalo troppo`false` tra `<reportCrash>` e `</reportCrash>` tag.</span><span class="sxs-lookup"><span data-stu-id="5c65c-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="5c65c-184">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="5c65c-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="5c65c-185">Impostare toofalse di arresto anomalo di report utilizzando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="5c65c-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="5c65c-186">Modalità burst</span><span class="sxs-lookup"><span data-stu-id="5c65c-186">Burst mode</span></span>
<span data-ttu-id="5c65c-187">Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="5c65c-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="5c65c-188">Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="5c65c-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="5c65c-189">toodo in tal caso, chiamare il metodo hello:</span><span class="sxs-lookup"><span data-stu-id="5c65c-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="5c65c-190">argomento Hello è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="5c65c-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="5c65c-191">In qualsiasi momento, se si desidera registrare in tempo reale di tooreactivate hello, chiamare solo metodo hello senza alcun parametro, o con valore 0 hello.</span><span class="sxs-lookup"><span data-stu-id="5c65c-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="5c65c-192">Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile).</span><span class="sxs-lookup"><span data-stu-id="5c65c-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="5c65c-193">È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="5c65c-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="5c65c-194">È necessario tenere presente che registri salvati sono elementi too300 limitato toobe.</span><span class="sxs-lookup"><span data-stu-id="5c65c-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="5c65c-195">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="5c65c-196">Hello soglia burst non può essere configurata tooa periodo inferiore rispetto a un secondo.</span><span class="sxs-lookup"><span data-stu-id="5c65c-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="5c65c-197">Se si tenta pertanto toodo, hello SDK sarà visualizzare una traccia con l'errore hello e verrà automaticamente reimpostato toohello valore predefinito, ovvero zero secondi.</span><span class="sxs-lookup"><span data-stu-id="5c65c-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="5c65c-198">In questo modo verrà attivata hello SDK tooreport hello log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="5c65c-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

