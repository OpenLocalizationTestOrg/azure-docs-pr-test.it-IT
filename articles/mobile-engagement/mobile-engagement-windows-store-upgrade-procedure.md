---
title: Procedure di aggiornamento di Windows Universal Apps SDK
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="b88e6-103">Procedure di aggiornamento di Windows Universal Apps SDK</span><span class="sxs-lookup"><span data-stu-id="b88e6-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="b88e6-104">Se nell'applicazione è già stata integrata una versione precedente dell'SDK, è necessario considerare i seguenti punti quando si aggiorna l'SDK.</span><span class="sxs-lookup"><span data-stu-id="b88e6-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="b88e6-105">Se non sono state applicate alcune versioni dell'SDK, potrebbe essere necessario eseguire più procedure.</span><span class="sxs-lookup"><span data-stu-id="b88e6-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="b88e6-106">Se ad esempio si esegue la migrazione dalla versione 0.10.1 alla 0.11.0, sarà prima di tutto necessario eseguire la procedura per la migrazione "dalla 0.9.0 alla 0.10.1" e quindi la procedura per la migrazione "dalla 0.10.1 alla 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="b88e6-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="b88e6-107">Dalla versione 3.3.0 alla 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b88e6-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="b88e6-108">Log di test</span><span class="sxs-lookup"><span data-stu-id="b88e6-108">Test logs</span></span>
<span data-ttu-id="b88e6-109">I log della console generati da SDK possono essere abilitati/disattivati/filtrati.</span><span class="sxs-lookup"><span data-stu-id="b88e6-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="b88e6-110">Per eseguire una personalizzazione, aggiornare la proprietà `EngagementAgent.Instance.TestLogEnabled` scegliendo uno dei valori disponibili nell'enumerazione `EngagementTestLogLevel`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b88e6-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="b88e6-111">Risorse</span><span class="sxs-lookup"><span data-stu-id="b88e6-111">Resources</span></span>
<span data-ttu-id="b88e6-112">La sovrimpressione Reach è stata migliorata.</span><span class="sxs-lookup"><span data-stu-id="b88e6-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="b88e6-113">Fa parte delle risorse del pacchetto NuGet di SDK.</span><span class="sxs-lookup"><span data-stu-id="b88e6-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="b88e6-114">Durante l'aggiornamento alla nuova versione di SDK, è possibile scegliere se mantenere i file esistenti contenuti nella cartella della sovrimpressione delle risorse o meno:</span><span class="sxs-lookup"><span data-stu-id="b88e6-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="b88e6-115">Se la sovrimpressione precedente è in funzione o si stanno integrando manualmente gli elementi `WebView`, è possibile decidere di mantenere i file esistenti per poter proseguire.</span><span class="sxs-lookup"><span data-stu-id="b88e6-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="b88e6-116">Se invece si vuole passare alla sovrimpressione nuova, è sufficiente sostituire l'intera cartella `overlay` delle risorse con quella nuova disponibile nel pacchetto SDK. Dopo aver completato l'aggiornamento, nelle app UWP è possibile ottenere la cartella della nuova sovrimpressione da %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="b88e6-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="b88e6-117">Se si usa la sovrimpressione nuova, le personalizzazioni eseguite con la versione precedente saranno sovrascritte.</span><span class="sxs-lookup"><span data-stu-id="b88e6-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="b88e6-118">Dalla versione 3.2.0 alla 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b88e6-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="b88e6-119">Risorse</span><span class="sxs-lookup"><span data-stu-id="b88e6-119">Resources</span></span>
<span data-ttu-id="b88e6-120">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-120">This step concerns customized resources only.</span></span> <span data-ttu-id="b88e6-121">Se sono state personalizzate le risorse fornite dall'SDK (html, immagini, sovrimpressioni) è necessario eseguirne il backup prima dell'aggiornamento e riapplicare la personalizzazione alle risorse aggiornate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="b88e6-122">Dalla versione 3.1.0 alla 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b88e6-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="b88e6-123">Risorse</span><span class="sxs-lookup"><span data-stu-id="b88e6-123">Resources</span></span>
<span data-ttu-id="b88e6-124">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-124">This step concerns customized resources only.</span></span> <span data-ttu-id="b88e6-125">Se sono state personalizzate le risorse fornite dall'SDK (html, immagini, sovrimpressioni) è necessario eseguirne il backup prima dell'aggiornamento e riapplicare la personalizzazione alle risorse aggiornate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="b88e6-126">l'integrazione di visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="b88e6-126">Webview integration</span></span>
<span data-ttu-id="b88e6-127">In questa versione sono stati introdotti alcuni miglioramenti per la corrispondenza dei fattori di forma del dispositivo diversi.</span><span class="sxs-lookup"><span data-stu-id="b88e6-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="b88e6-128">Assicurarsi che l'integrazione delle webview corrisponda a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b88e6-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="b88e6-129">Nella pagina XAML ():</span><span class="sxs-lookup"><span data-stu-id="b88e6-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="b88e6-130">E nel file con estensione cs associato:</span><span class="sxs-lookup"><span data-stu-id="b88e6-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="b88e6-131">Dalla versione 2.0.0 alla 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b88e6-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="b88e6-132">Risorse</span><span class="sxs-lookup"><span data-stu-id="b88e6-132">Resources</span></span>
<span data-ttu-id="b88e6-133">Questo passaggio riguarda solo le risorse personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-133">This step concerns customized resources only.</span></span> <span data-ttu-id="b88e6-134">Se sono state personalizzate le risorse fornite dall'SDK (html, immagini, sovrimpressioni) è necessario eseguirne il backup prima dell'aggiornamento e riapplicare la personalizzazione alle risorse aggiornate.</span><span class="sxs-lookup"><span data-stu-id="b88e6-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="b88e6-135">Dalla versione 1.1.1 alla 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b88e6-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="b88e6-136">La sezione seguente illustra come eseguire la migrazione di un'integrazione dell'SDK dal servizio Capptain offerto da Capptain SAS a un'app basata su Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b88e6-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b88e6-137">Capptain e Mobile Engagement sono servizi diversi e la procedura seguente illustra solo come eseguire la migrazione dell'app client.</span><span class="sxs-lookup"><span data-stu-id="b88e6-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="b88e6-138">La migrazione dell'SDK nell'app NON comporta la migrazione dei dati dai server di Capptain ai server di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b88e6-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="b88e6-139">Se si esegue la migrazione da una versione precedente, consultare il sito web Capptain per eseguire prima la migrazione a 1.1.1, quindi applicare la procedura seguente</span><span class="sxs-lookup"><span data-stu-id="b88e6-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="b88e6-140">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="b88e6-140">Nuget package</span></span>
<span data-ttu-id="b88e6-141">Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="b88e6-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="b88e6-142">Applicazione di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b88e6-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="b88e6-143">L'SDK usa il termine `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="b88e6-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="b88e6-144">È necessario aggiornare il progetto per tenere conto di questa modifica.</span><span class="sxs-lookup"><span data-stu-id="b88e6-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="b88e6-145">È necessario disinstallare il pacchetto nuget corrente di Capptain.</span><span class="sxs-lookup"><span data-stu-id="b88e6-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="b88e6-146">Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain.</span><span class="sxs-lookup"><span data-stu-id="b88e6-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="b88e6-147">Se si desidera mantenere tali file, eseguirne una copia.</span><span class="sxs-lookup"><span data-stu-id="b88e6-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="b88e6-148">Successivamente, installare il nuovo pacchetto NuGet di Microsoft Azure Engagement nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b88e6-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="b88e6-149">È possibile trovarlo direttamente su [sito Web di NuGet]</span><span class="sxs-lookup"><span data-stu-id="b88e6-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="b88e6-150">o nell'indice qui.</span><span class="sxs-lookup"><span data-stu-id="b88e6-150">or here index.</span></span> <span data-ttu-id="b88e6-151">Questa operazione sostituisce tutti i file di risorse utilizzati da Engagement e aggiunge la nuova DLL di Engagement ai riferimenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="b88e6-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="b88e6-152">È necessario eliminare i riferimenti del progetto rimuovendo i riferimenti DLL di Capptain.</span><span class="sxs-lookup"><span data-stu-id="b88e6-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="b88e6-153">Se non si effettua questa operazione, la versione di Capptain creerà un conflitto e si verificheranno errori.</span><span class="sxs-lookup"><span data-stu-id="b88e6-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="b88e6-154">Se sono state personalizzate risorse Capptain, copiare il contenuto dei file precedenti e incollarlo in nuovi file di progetto.</span><span class="sxs-lookup"><span data-stu-id="b88e6-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="b88e6-155">Si noti che è necessario aggiornare sia i file xaml che i file cs.</span><span class="sxs-lookup"><span data-stu-id="b88e6-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="b88e6-156">Al termine di queste operazioni, è necessario sostituire i riferimenti di Capptain precedenti con i nuovi riferimenti di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b88e6-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="b88e6-157">Tutti gli spazi dei nomi Capptain devono essere aggiornati.</span><span class="sxs-lookup"><span data-stu-id="b88e6-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="b88e6-158">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="b88e6-159">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="b88e6-160">Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".</span><span class="sxs-lookup"><span data-stu-id="b88e6-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="b88e6-161">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="b88e6-162">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="b88e6-163">Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.</span><span class="sxs-lookup"><span data-stu-id="b88e6-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="b88e6-164">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="b88e6-165">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="b88e6-166">Modifiche alle pagine di sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="b88e6-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b88e6-167">Anche la sovrimpressione cambia.</span><span class="sxs-lookup"><span data-stu-id="b88e6-167">Overlay also changes.</span></span> <span data-ttu-id="b88e6-168">Il nuovo spazio dei nomi è `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="b88e6-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="b88e6-169">Deve essere usato sia nei file xaml sia nei file cs.</span><span class="sxs-lookup"><span data-stu-id="b88e6-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="b88e6-170">Inoltre, `CapptainGrid` deve essere denominato `EngagementGrid` e `capptain_notification_content` e `capptain_announcement_content` sono denominati `engagement_notification_content` e `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="b88e6-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="b88e6-171">Per la sovrimpressione:</span><span class="sxs-lookup"><span data-stu-id="b88e6-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="b88e6-172">Diventa:</span><span class="sxs-lookup"><span data-stu-id="b88e6-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="b88e6-173">Per altre risorse come le immagini di Capptain e i file HTML, tenere presente che sono state rinominate per l'utilizzo di "Engagement".</span><span class="sxs-lookup"><span data-stu-id="b88e6-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="b88e6-174">Dichiarazione di progetto</span><span class="sxs-lookup"><span data-stu-id="b88e6-174">Project declaration</span></span>
<span data-ttu-id="b88e6-175">In Package.appxmanifest `File Type Associations` è stato aggiornato da:</span><span class="sxs-lookup"><span data-stu-id="b88e6-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="b88e6-176">capptain\_reach\_content in engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="b88e6-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="b88e6-177">capptain\_log\_file in engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="b88e6-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="b88e6-178">ID applicazione / chiave SDK</span><span class="sxs-lookup"><span data-stu-id="b88e6-178">Application ID / SDK Key</span></span>
<span data-ttu-id="b88e6-179">Engagement utilizza una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="b88e6-179">Engagement uses a connection string.</span></span> <span data-ttu-id="b88e6-180">Non è necessario specificare un ID applicazione e una chiave SDK con Mobile Engagement, è sufficiente specificare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="b88e6-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="b88e6-181">È possibile configurarla nel file EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b88e6-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="b88e6-182">La configurazione di Engagement può essere impostata nel file `Resources\EngagementConfiguration.xml` del progetto.</span><span class="sxs-lookup"><span data-stu-id="b88e6-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b88e6-183">Modificare questo file per specificare:</span><span class="sxs-lookup"><span data-stu-id="b88e6-183">Edit this file to specify:</span></span>

* <span data-ttu-id="b88e6-184">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="b88e6-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="b88e6-185">Se si desidera specificarla in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="b88e6-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="b88e6-186">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b88e6-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="b88e6-187">Modifica del nome di elementi</span><span class="sxs-lookup"><span data-stu-id="b88e6-187">Items name change</span></span>
<span data-ttu-id="b88e6-188">Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*.</span><span class="sxs-lookup"><span data-stu-id="b88e6-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="b88e6-189">Lo stesso vale per *Capptain*, che è stato ridenominato in *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="b88e6-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="b88e6-190">Esempi di elementi di Capptain di uso comune:</span><span class="sxs-lookup"><span data-stu-id="b88e6-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="b88e6-191">CapptainConfiguration è diventato EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="b88e6-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="b88e6-192">CapptainAgent è diventato EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="b88e6-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="b88e6-193">CapptainReach è diventato EngagementReach</span><span class="sxs-lookup"><span data-stu-id="b88e6-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="b88e6-194">CapptainHttpConfig è diventato EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="b88e6-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="b88e6-195">GetCapptainPageName è diventato GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="b88e6-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="b88e6-196">Si noti la ridenominazione influisce anche sui metodi sottoposti a override.</span><span class="sxs-lookup"><span data-stu-id="b88e6-196">Note that rename also affects overridden methods.</span></span>

