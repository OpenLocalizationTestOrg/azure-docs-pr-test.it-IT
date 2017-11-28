---
title: aaaWindows universale avanzate Reporting con MobileApps Engagement
description: Come tooIntegrate Azure Mobile Engagement con App universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="20401-103">Creazione di report avanzate con hello Windows Universal App Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="20401-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20401-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="20401-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="20401-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="20401-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="20401-106">iOS</span><span class="sxs-lookup"><span data-stu-id="20401-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="20401-107">Android</span><span class="sxs-lookup"><span data-stu-id="20401-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="20401-108">Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione di Windows universale.</span><span class="sxs-lookup"><span data-stu-id="20401-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="20401-109">Questi scenari includono opzioni che è possibile selezionare app toohello tooapply creato in hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="20401-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20401-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20401-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="20401-111">Prima di iniziare questa esercitazione, è necessario prima completare hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) esercitazione, è intenzionalmente semplice e diretto.</span><span class="sxs-lookup"><span data-stu-id="20401-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="20401-112">Questa esercitazione illustra le opzioni aggiuntive disponibili.</span><span class="sxs-lookup"><span data-stu-id="20401-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="20401-113">Specifica della configurazione di Engagement in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="20401-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="20401-114">configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto, in cui è stato specificato in hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="20401-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="20401-115">Ma è possibile inoltre specificare in fase di esecuzione: è possibile chiamare hello al metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="20401-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="20401-116">Metodo consigliato: eseguire l'overload delle classi `Page`</span><span class="sxs-lookup"><span data-stu-id="20401-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="20401-117">tooactivate hello reporting di tutti i log di hello richiesti da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, apportare tutte le `Page` sottoclassi ereditano hello `EngagementPage` classi.</span><span class="sxs-lookup"><span data-stu-id="20401-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="20401-118">Di seguito è riportato un esempio per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="20401-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="20401-119">È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="20401-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="20401-120">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="20401-120">C# Source file</span></span>
<span data-ttu-id="20401-121">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="20401-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="20401-122">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="20401-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="20401-123">Sostituire `Page` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="20401-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="20401-124">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="20401-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="20401-125">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="20401-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="20401-126">Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="20401-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="20401-127">In caso contrario, attività hello non venga segnalato (hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="20401-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="20401-128">File XAML</span><span class="sxs-lookup"><span data-stu-id="20401-128">XAML file</span></span>
<span data-ttu-id="20401-129">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="20401-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="20401-130">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="20401-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="20401-131">Sostituire `Page` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="20401-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="20401-132">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="20401-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="20401-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="20401-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="20401-134">Eseguire l'override di comportamento predefinito di hello</span><span class="sxs-lookup"><span data-stu-id="20401-134">Override hello default behaviour</span></span>
<span data-ttu-id="20401-135">Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="20401-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="20401-136">Se la classe hello utilizza il suffisso "Pagina" hello, Engagement lo rimuove.</span><span class="sxs-lookup"><span data-stu-id="20401-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="20401-137">comportamento predefinito di hello toooverride per nome hello, aggiungere questo codice:</span><span class="sxs-lookup"><span data-stu-id="20401-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="20401-138">tooreport informazioni aggiuntive con l'attività, aggiungere il seguente codice:</span><span class="sxs-lookup"><span data-stu-id="20401-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="20401-139">Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.</span><span class="sxs-lookup"><span data-stu-id="20401-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="20401-140">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="20401-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="20401-141">Se non è possibile o non si desidera toooverload il `Page` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="20401-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="20401-142">È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="20401-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="20401-143">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="20401-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="20401-144">SDK di Windows universale Hello chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="20401-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="20401-145">È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` metodo.</span><span class="sxs-lookup"><span data-stu-id="20401-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="20401-146">Questo metodo notifica server Engagement hello che l'utente corrente hello ha lasciato l'applicazione hello, che avrà un impatto tutti i log dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="20401-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="20401-147">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="20401-147">Advanced reporting</span></span>
<span data-ttu-id="20401-148">Facoltativamente, è opportuno eventi specifici dell'applicazione tooreport, errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="20401-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="20401-149">Hello Engagement API consente l'utilizzo delle funzionalità avanzate di Engagement tutti.</span><span class="sxs-lookup"><span data-stu-id="20401-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="20401-150">Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="20401-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

