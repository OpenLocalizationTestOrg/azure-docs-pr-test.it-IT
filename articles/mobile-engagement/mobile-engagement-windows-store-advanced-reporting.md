---
title: Segnalazione avanzata di Windows universale con MobileApps Engagement
description: Come integrare Azure Mobile Engagement con le app universali di Windows
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
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="79bfe-103">Segnalazione avanzata con Engagement SDK per le app di Windows universali</span><span class="sxs-lookup"><span data-stu-id="79bfe-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79bfe-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="79bfe-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="79bfe-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="79bfe-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="79bfe-106">iOS</span><span class="sxs-lookup"><span data-stu-id="79bfe-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="79bfe-107">Android</span><span class="sxs-lookup"><span data-stu-id="79bfe-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="79bfe-108">Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione di Windows universale.</span><span class="sxs-lookup"><span data-stu-id="79bfe-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="79bfe-109">Questi scenari includono le opzioni che è possibile scegliere di applicare all'app creata nell'esercitazione [introduttiva](mobile-engagement-windows-store-dotnet-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="79bfe-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79bfe-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79bfe-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="79bfe-111">Prima di iniziare questa esercitazione, è necessario completare l'esercitazione [introduttiva](mobile-engagement-windows-store-dotnet-get-started.md) che è intenzionalmente diretta e semplice .</span><span class="sxs-lookup"><span data-stu-id="79bfe-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="79bfe-112">Questa esercitazione illustra le opzioni aggiuntive disponibili.</span><span class="sxs-lookup"><span data-stu-id="79bfe-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="79bfe-113">Specifica della configurazione di Engagement in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="79bfe-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="79bfe-114">La configurazione di Engagement è centralizzata nel file `Resources\EngagementConfiguration.xml` del progetto, ovvero quello in cui è stata specificata nell'argomento [introduttivo](mobile-engagement-windows-store-dotnet-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="79bfe-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="79bfe-115">Se si vuole specificarlo in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="79bfe-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="79bfe-116">Metodo consigliato: eseguire l'overload delle classi `Page`</span><span class="sxs-lookup"><span data-stu-id="79bfe-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="79bfe-117">Per attivare la segnalazione di tutti i log richiesti da Engagement per calcolare utenti, sessioni, attività, arresti anomali e statistiche tecniche, fare in modo che tutte le sottoclassi `Page` ereditino dalle classi `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="79bfe-118">Di seguito è riportato un esempio per una pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="79bfe-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="79bfe-119">È possibile procedere allo stesso modo per tutte le pagine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="79bfe-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="79bfe-120">File di origine C#</span><span class="sxs-lookup"><span data-stu-id="79bfe-120">C# Source file</span></span>
<span data-ttu-id="79bfe-121">Modificare il file `.xaml.cs` della pagina:</span><span class="sxs-lookup"><span data-stu-id="79bfe-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="79bfe-122">Aggiungere quanto segue alle istruzioni `using`:</span><span class="sxs-lookup"><span data-stu-id="79bfe-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="79bfe-123">Sostituire `Page` con `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="79bfe-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="79bfe-124">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="79bfe-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="79bfe-125">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="79bfe-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="79bfe-126">Se la pagina esegue l'override del metodo `OnNavigatedTo`, accertarsi di chiamare `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="79bfe-127">In caso contrario, l'attività non verrà segnalata, ovvero `EngagementPage` chiama `StartActivity` all'interno del relativo metodo `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="79bfe-128">File XAML</span><span class="sxs-lookup"><span data-stu-id="79bfe-128">XAML file</span></span>
<span data-ttu-id="79bfe-129">Modificare il file `.xaml` della pagina:</span><span class="sxs-lookup"><span data-stu-id="79bfe-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="79bfe-130">Aggiungere le dichiarazioni di spazi dei nomi:</span><span class="sxs-lookup"><span data-stu-id="79bfe-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="79bfe-131">Sostituire `Page` con `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="79bfe-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="79bfe-132">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="79bfe-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="79bfe-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="79bfe-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="79bfe-134">Eseguire l'override del comportamento predefinito</span><span class="sxs-lookup"><span data-stu-id="79bfe-134">Override the default behaviour</span></span>
<span data-ttu-id="79bfe-135">Per impostazione predefinita, il nome della classe della pagina viene indicato come nome dell'attività, senza elementi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="79bfe-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="79bfe-136">Se la classe usa il suffisso "Page", Engagement rimuoverà questo elemento.</span><span class="sxs-lookup"><span data-stu-id="79bfe-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="79bfe-137">Per sostituire il comportamento predefinito per il nome, aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="79bfe-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="79bfe-138">Per segnalare informazioni aggiuntive con l'attività, aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="79bfe-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="79bfe-139">Questi metodi vengono chiamati dall'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="79bfe-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="79bfe-140">Metodo alternativo: chiamare `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="79bfe-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="79bfe-141">Se non si può o non si vuole eseguire l'overload delle classi `Page`, in alternativa è possibile avviare le attività chiamando direttamente i metodi `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="79bfe-142">È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` della pagina.</span><span class="sxs-lookup"><span data-stu-id="79bfe-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="79bfe-143">Assicurarsi che la sessione venga terminata correttamente.</span><span class="sxs-lookup"><span data-stu-id="79bfe-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="79bfe-144">Windows Universal SDK chiama automaticamente il metodo `EndActivity` quando l'applicazione viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="79bfe-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="79bfe-145">È quindi **ALTAMENTE** consigliabile chiamare il metodo `StartActivity` ogni volta che l'attività dell'utente cambia e non chiamare **MAI** il metodo `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="79bfe-146">Questo metodo notifica al server di Engagement che l'utente ha chiuso l'applicazione e ciò influirà su tutti i log delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="79bfe-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="79bfe-147">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="79bfe-147">Advanced reporting</span></span>
<span data-ttu-id="79bfe-148">Facoltativamente, è possibile segnalare eventi specifici dell'applicazione, errori e processi. A tale scopo, usare gli altri metodi disponibili nella classe `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="79bfe-149">L'API di Engagement consente di usare tutte le funzionalità avanzate di Engagement.</span><span class="sxs-lookup"><span data-stu-id="79bfe-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="79bfe-150">Per altre informazioni, vedere [Come usare l'API di Engagement in un'app di Windows universale](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="79bfe-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

