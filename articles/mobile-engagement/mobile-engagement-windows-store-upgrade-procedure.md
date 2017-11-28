---
title: le procedure di aggiornamento SDK di Universal App aaaWindows
description: Procedure di aggiornamento di Windows Universal Apps SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="50f28-103">Procedure di aggiornamento di Windows Universal Apps SDK</span><span class="sxs-lookup"><span data-stu-id="50f28-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="50f28-104">Se è già stata integrata una versione precedente di Engagement all'interno dell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.</span><span class="sxs-lookup"><span data-stu-id="50f28-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="50f28-105">È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="50f28-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="50f28-106">Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.</span><span class="sxs-lookup"><span data-stu-id="50f28-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="50f28-107">Da 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="50f28-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="50f28-108">Log di test</span><span class="sxs-lookup"><span data-stu-id="50f28-108">Test logs</span></span>
<span data-ttu-id="50f28-109">Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato.</span><span class="sxs-lookup"><span data-stu-id="50f28-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="50f28-110">toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="50f28-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="50f28-111">Risorse</span><span class="sxs-lookup"><span data-stu-id="50f28-111">Resources</span></span>
<span data-ttu-id="50f28-112">sovrapposizione di copertura Hello è stata migliorata.</span><span class="sxs-lookup"><span data-stu-id="50f28-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="50f28-113">È parte di risorse del pacchetto NuGet SDK hello.</span><span class="sxs-lookup"><span data-stu-id="50f28-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="50f28-114">Durante l'aggiornamento toohello nuova versione di hello SDK è possibile scegliere che se si desidera tookeep i file esistenti da hello sovrapposizione cartella delle risorse o non:</span><span class="sxs-lookup"><span data-stu-id="50f28-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="50f28-115">Se sovrapposizione precedente hello è alle proprie esigenze o se si sta integrando hello `WebView` elementi manualmente, quindi è possibile decidere tookeep i file esistenti, continuerà a funzionare.</span><span class="sxs-lookup"><span data-stu-id="50f28-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="50f28-116">Se si desidera tooupdate toohello nuovo sovrapposizione, sostituire semplicemente hello intero `overlay` cartella dalle risorse con hello uno nuovo dal pacchetto SDK hello (app UWP: dopo l'aggiornamento di hello, è possibile ottenere la nuova cartella sovrapposizione di hello da % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="50f28-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="50f28-117">Utilizzando sovrapposizione nuovo hello sovrascriverà le personalizzazioni apportate in una versione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="50f28-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="50f28-118">Da 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="50f28-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="50f28-119">Risorse</span><span class="sxs-lookup"><span data-stu-id="50f28-119">Resources</span></span>
<span data-ttu-id="50f28-120">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="50f28-120">This step concerns customized resources only.</span></span> <span data-ttu-id="50f28-121">Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.</span><span class="sxs-lookup"><span data-stu-id="50f28-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="50f28-122">Da 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="50f28-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="50f28-123">Risorse</span><span class="sxs-lookup"><span data-stu-id="50f28-123">Resources</span></span>
<span data-ttu-id="50f28-124">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="50f28-124">This step concerns customized resources only.</span></span> <span data-ttu-id="50f28-125">Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.</span><span class="sxs-lookup"><span data-stu-id="50f28-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="50f28-126">l'integrazione di visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="50f28-126">Webview integration</span></span>
<span data-ttu-id="50f28-127">In questa versione, sono stati introdotti alcuni miglioramenti toomatch diversi form factor.</span><span class="sxs-lookup"><span data-stu-id="50f28-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="50f28-128">Assicurarsi che l'integrazione di webview hello corrisponda esempio hello:</span><span class="sxs-lookup"><span data-stu-id="50f28-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="50f28-129">Nella pagina XAML ():</span><span class="sxs-lookup"><span data-stu-id="50f28-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="50f28-130">E nel file con estensione cs associato:</span><span class="sxs-lookup"><span data-stu-id="50f28-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="50f28-131">Da 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="50f28-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="50f28-132">Risorse</span><span class="sxs-lookup"><span data-stu-id="50f28-132">Resources</span></span>
<span data-ttu-id="50f28-133">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="50f28-133">This step concerns customized resources only.</span></span> <span data-ttu-id="50f28-134">Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.</span><span class="sxs-lookup"><span data-stu-id="50f28-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="50f28-135">Da 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="50f28-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="50f28-136">Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="50f28-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="50f28-137">Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="50f28-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="50f28-138">Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="50f28-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="50f28-139">Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.1.1 quindi applicare hello procedura</span><span class="sxs-lookup"><span data-stu-id="50f28-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="50f28-140">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="50f28-140">Nuget package</span></span>
<span data-ttu-id="50f28-141">Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="50f28-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="50f28-142">Applicazione di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="50f28-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="50f28-143">Hello SDK viene utilizzato il termine hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="50f28-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="50f28-144">È necessario tooupdate toomatch il progetto questa modifica.</span><span class="sxs-lookup"><span data-stu-id="50f28-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="50f28-145">È necessario toouninstall il pacchetto nuget Capptain corrente.</span><span class="sxs-lookup"><span data-stu-id="50f28-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="50f28-146">Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain.</span><span class="sxs-lookup"><span data-stu-id="50f28-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="50f28-147">Se si desidera tookeep tali file, creare una copia di essi.</span><span class="sxs-lookup"><span data-stu-id="50f28-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="50f28-148">Successivamente, installare il pacchetto di hello nuovo impegno di Microsoft Azure nuget nel progetto.</span><span class="sxs-lookup"><span data-stu-id="50f28-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="50f28-149">È possibile trovarlo direttamente su [sito Web di NuGet]</span><span class="sxs-lookup"><span data-stu-id="50f28-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="50f28-150">o nell'indice qui.</span><span class="sxs-lookup"><span data-stu-id="50f28-150">or here index.</span></span> <span data-ttu-id="50f28-151">Sostituisce questa azione, tutti i file di risorse utilizzate da Engagement e hello nuova DLL Engagement tooyour aggiunge i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="50f28-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="50f28-152">Hai tooclean riferimenti del progetto eliminando i riferimenti DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="50f28-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="50f28-153">Se non si apporta questa, versione di hello di Capptain è in conflitto e si verificheranno gli errori.</span><span class="sxs-lookup"><span data-stu-id="50f28-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="50f28-154">Se è stato personalizzato Capptain risorse, copiare il contenuto del file precedente e incollarli in nuovi file di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="50f28-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="50f28-155">Si noti che i file xaml sia cs toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="50f28-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="50f28-156">Dopo avere completato questi passaggi è sufficiente tooreplace precedente Capptain i riferimenti basati sui nuovi riferimenti di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="50f28-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="50f28-157">Tutti gli spazi dei nomi di Capptain avere toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="50f28-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="50f28-158">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="50f28-159">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="50f28-160">Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".</span><span class="sxs-lookup"><span data-stu-id="50f28-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="50f28-161">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="50f28-162">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="50f28-163">Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.</span><span class="sxs-lookup"><span data-stu-id="50f28-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="50f28-164">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="50f28-165">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="50f28-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="50f28-166">Modifiche alle pagine di sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="50f28-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="50f28-167">Anche la sovrimpressione cambia.</span><span class="sxs-lookup"><span data-stu-id="50f28-167">Overlay also changes.</span></span> <span data-ttu-id="50f28-168">Il nuovo spazio dei nomi è `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="50f28-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="50f28-169">Ha toobe utilizzato nei file xaml e cs.</span><span class="sxs-lookup"><span data-stu-id="50f28-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="50f28-170">Inoltre `CapptainGrid` toobe denominato `EngagementGrid`, `capptain_notification_content` e `capptain_announcement_content` sono denominati `engagement_notification_content` e `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="50f28-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="50f28-171">Per la sovrimpressione:</span><span class="sxs-lookup"><span data-stu-id="50f28-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="50f28-172">Diventa:</span><span class="sxs-lookup"><span data-stu-id="50f28-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="50f28-173">Per hello altre risorse quali immagini Capptain e file HTML, si noti che sono anche stati rinominati toouse "Engagement".</span><span class="sxs-lookup"><span data-stu-id="50f28-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="50f28-174">Dichiarazione di progetto</span><span class="sxs-lookup"><span data-stu-id="50f28-174">Project declaration</span></span>
<span data-ttu-id="50f28-175">In Package.appxmanifest `File Type Associations` è stato aggiornato da:</span><span class="sxs-lookup"><span data-stu-id="50f28-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="50f28-176">capptain\_raggiungere\_tooengagement contenuto\_raggiungere\_contenuto</span><span class="sxs-lookup"><span data-stu-id="50f28-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="50f28-177">capptain\_log\_file tooengagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="50f28-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="50f28-178">ID applicazione / chiave SDK</span><span class="sxs-lookup"><span data-stu-id="50f28-178">Application ID / SDK Key</span></span>
<span data-ttu-id="50f28-179">Engagement utilizza una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="50f28-179">Engagement uses a connection string.</span></span> <span data-ttu-id="50f28-180">Non si dispone toospecify un ID applicazione e una chiave SDK con Engagement Mobile, è sufficiente toospecify una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="50f28-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="50f28-181">È possibile configurarla nel file EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="50f28-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="50f28-182">configurazione di Engagement Hello può essere impostate nel `Resources\EngagementConfiguration.xml` file del progetto.</span><span class="sxs-lookup"><span data-stu-id="50f28-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="50f28-183">Modificare questo toospecify file:</span><span class="sxs-lookup"><span data-stu-id="50f28-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="50f28-184">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="50f28-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="50f28-185">Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="50f28-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="50f28-186">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="50f28-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="50f28-187">Modifica del nome di elementi</span><span class="sxs-lookup"><span data-stu-id="50f28-187">Items name change</span></span>
<span data-ttu-id="50f28-188">Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*.</span><span class="sxs-lookup"><span data-stu-id="50f28-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="50f28-189">Analogamente, per *Capptain* troppo*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="50f28-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="50f28-190">Esempi di elementi di Capptain di uso comune:</span><span class="sxs-lookup"><span data-stu-id="50f28-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="50f28-191">CapptainConfiguration è diventato EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="50f28-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="50f28-192">CapptainAgent è diventato EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="50f28-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="50f28-193">CapptainReach è diventato EngagementReach</span><span class="sxs-lookup"><span data-stu-id="50f28-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="50f28-194">CapptainHttpConfig è diventato EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="50f28-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="50f28-195">GetCapptainPageName è diventato GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="50f28-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="50f28-196">Si noti la ridenominazione influisce anche sui metodi sottoposti a override.</span><span class="sxs-lookup"><span data-stu-id="50f28-196">Note that rename also affects overridden methods.</span></span>

