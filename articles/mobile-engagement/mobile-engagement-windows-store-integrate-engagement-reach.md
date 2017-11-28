---
title: Integrazione di SDK a raggiungere Universal App aaaWindows
description: Come tooIntegrate Azure Mobile Engagement raggiunge con App universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="615f9-103">Integrazione di Reach SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="615f9-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="615f9-104">Attenersi alla procedura di integrazione hello descritta in hello [integrazione di Windows universale Engagement SDK](mobile-engagement-windows-store-integrate-engagement.md) prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="615f9-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="615f9-105">Incorporare hello Engagement Reach SDK nel progetto Windows universale</span><span class="sxs-lookup"><span data-stu-id="615f9-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="615f9-106">Non è un valore tooadd.</span><span class="sxs-lookup"><span data-stu-id="615f9-106">You do not have anything tooadd.</span></span> <span data-ttu-id="615f9-107">`EngagementReach` sono già presenti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="615f9-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="615f9-108">È possibile personalizzare le immagini si trova in hello `Resources` cartella del progetto, in particolare hello marchio icona (tale impostazione predefinita toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="615f9-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="615f9-109">Per le app universali è inoltre possibile spostare hello `Resources` cartella tooshare del progetto condiviso il contenuto tra le app, ma si disporrà di hello tookeep `Resources\EngagementConfiguration.xml` di file nel percorso predefinito è dipendente dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="615f9-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="615f9-110">Abilitare il servizio di notifica di Windows hello</span><span class="sxs-lookup"><span data-stu-id="615f9-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="615f9-111">Solo Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="615f9-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="615f9-112">In hello toouse ordine **servizio di notifica Windows** (definito WNS) nei `Package.appxmanifest` file nel `Application UI` fare clic su `All Image Assets` nella casella a sinistra bot hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="615f9-113">In hello destra della casella hello `Notifications`, modificare `toast capable` da `(not set)` troppo`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="615f9-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="615f9-114">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="615f9-114">All platforms</span></span>
<span data-ttu-id="615f9-115">È necessario toosynchronize dell'app tooyour Microsoft account e toohello engagement della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="615f9-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="615f9-116">Per questo è necessario un account toocreate o accedere [Centro sviluppatori windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="615f9-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="615f9-117">Dopo la creazione di una nuova applicazione e trovare hello SID e una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="615f9-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="615f9-118">Nel server front-end engagement hello, passare l'impostazione di app in `native push` e incollare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="615f9-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="615f9-119">Dopo questa operazione, fare clic sul progetto, selezionare `store` e `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="615f9-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="615f9-120">È sufficiente un'applicazione hello tooselect hanno creata prima toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="615f9-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="615f9-121">Inizializzare hello Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="615f9-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="615f9-122">Modificare hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="615f9-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="615f9-123">Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` nel metodo `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="615f9-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="615f9-124">Hello `EngagementReach.Instance.Init` viene eseguito in un thread dedicato.</span><span class="sxs-lookup"><span data-stu-id="615f9-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="615f9-125">Non è toodo è manualmente.</span><span class="sxs-lookup"><span data-stu-id="615f9-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="615f9-126">Se si usano le notifiche push in un' posizione nell'applicazione, è troppo[condividono il canale di push](#push-channel-sharing) con copertura di Engagement.</span><span class="sxs-lookup"><span data-stu-id="615f9-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="615f9-127">Integrazione</span><span class="sxs-lookup"><span data-stu-id="615f9-127">Integration</span></span>
<span data-ttu-id="615f9-128">Engagement fornisce il banner in-app copertura di due modi tooadd hello e visualizzazioni intermedi per sondaggi nell'applicazione e gli annunci: hello sovrapporre di integrazione e l'integrazione di hello web viste manuale.</span><span class="sxs-lookup"><span data-stu-id="615f9-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="615f9-129">È consigliabile non combinare entrambe approccio hello stessa pagina.</span><span class="sxs-lookup"><span data-stu-id="615f9-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="615f9-130">scelta di Hello tra integrazione due hello può essere riepilogata in questo modo:</span><span class="sxs-lookup"><span data-stu-id="615f9-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="615f9-131">È possibile scegliere di integrazione di sovrapposizione hello se le pagine eredita già da hello agente `EngagementPage`, è sufficiente sostituire `EngagementPage` da `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` da `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nelle pagine.</span><span class="sxs-lookup"><span data-stu-id="615f9-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="615f9-132">È possibile scegliere integrazione manuale di hello web viste se si desidera tooprecisely sul posto hello raggiungere dell'interfaccia utente all'interno di pagine o se non si desidera tooadd pagine di livello tooyour ereditarietà un'altra.</span><span class="sxs-lookup"><span data-stu-id="615f9-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="615f9-133">Integrazione di una sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="615f9-133">Overlay integration</span></span>
<span data-ttu-id="615f9-134">sovrapposizione di Engagement Hello aggiunge in modo dinamico gli elementi dell'interfaccia utente di hello utilizzati campagne Reach toodisplay nella pagina.</span><span class="sxs-lookup"><span data-stu-id="615f9-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="615f9-135">Se hello sovrapposizione non soddisfa il layout è consigliabile visualizzazioni web hello integrazione manuale invece.</span><span class="sxs-lookup"><span data-stu-id="615f9-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="615f9-136">Modifica file con estensione XAML `EngagementPage` riferimento troppo`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="615f9-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="615f9-137">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="615f9-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="615f9-138">Sostituire `engagement:EngagementPage` con `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="615f9-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="615f9-139">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="615f9-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="615f9-140">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="615f9-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="615f9-141">Quindi, nel file con estensione cs contrassegnare la pagina in `EngagementPageOverlay` anziché `EngagementPage` e importare `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="615f9-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="615f9-142">Sostituire `EngagementPage` con `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="615f9-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="615f9-143">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="615f9-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="615f9-144">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="615f9-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="615f9-145">Aggiunge Hello sovrapposizione Engagement un `Grid` elemento nella parte superiore della pagina è composto di layout e hello due `WebView` elementi uno per hello banner e hello altra visualizzazione hello intermedi.</span><span class="sxs-lookup"><span data-stu-id="615f9-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="615f9-146">È possibile personalizzare elementi di sovrapposizione hello direttamente in hello `EngagementPageOverlay.cs` file.</span><span class="sxs-lookup"><span data-stu-id="615f9-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="615f9-147">Integrazione manuale delle visualizzazioni Web</span><span class="sxs-lookup"><span data-stu-id="615f9-147">Web views manual integration</span></span>
<span data-ttu-id="615f9-148">Copertura verrà eseguita la ricerca delle pagine per hello due `WebView` elementi responsabili della visualizzazione messaggio hello e visualizzazione intermedi hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="615f9-149">Hello solo cosa toodo è tooadd questi due `WebView` elementi in un punto qualsiasi delle pagine, di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="615f9-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="615f9-150">In questo hello esempio `WebView` elementi sono toofit estesa relativo contenitore che automaticamente ridimensionato nuovamente tali in caso di modifica delle dimensioni dello schermo rotazione o la finestra.</span><span class="sxs-lookup"><span data-stu-id="615f9-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="615f9-151">È importante tookeep hello stessa denominazione `engagement_notification_content` e `engagement_announcement_content` per hello `WebView` elementi.</span><span class="sxs-lookup"><span data-stu-id="615f9-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="615f9-152">Reach li identifica dal nome.</span><span class="sxs-lookup"><span data-stu-id="615f9-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="615f9-153">Gestire il push di dati (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="615f9-153">Handle datapush (optional)</span></span>
<span data-ttu-id="615f9-154">Se si desidera il push di dati applicazione toobe tooreceive in grado di raggiungere, è necessario tooimplement due eventi di classe EngagementReach hello:</span><span class="sxs-lookup"><span data-stu-id="615f9-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="615f9-155">In App.xaml.cs nel costruttore App() hello aggiungere:</span><span class="sxs-lookup"><span data-stu-id="615f9-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="615f9-156">È possibile visualizzare il callback di hello di ogni metodo restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="615f9-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="615f9-157">Engagement invia un feedback tooits back-end dopo l'invio di push di dati hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="615f9-158">Se il callback di hello restituisce false, hello `exit` feedback verrà inviato.</span><span class="sxs-lookup"><span data-stu-id="615f9-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="615f9-159">In caso contrario, il feedback sarà `action`.</span><span class="sxs-lookup"><span data-stu-id="615f9-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="615f9-160">Se il callback non è impostato per gli eventi di hello, hello `drop` commenti e suggerimenti verranno restituiti tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="615f9-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="615f9-161">Engagement non è in grado di tooreceive feedback multipli per il push di dati.</span><span class="sxs-lookup"><span data-stu-id="615f9-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="615f9-162">Se si intende tooset diversi gestori di un evento, tenere presente che il feedback hello corrisponderà toohello ultimo quello inviato.</span><span class="sxs-lookup"><span data-stu-id="615f9-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="615f9-163">In questo caso, è consigliabile tooalways restituisce hello stesso tooavoid valore determinato confusione commenti e suggerimenti su hello front-end.</span><span class="sxs-lookup"><span data-stu-id="615f9-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="615f9-164">Personalizzare l'interfaccia utente (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="615f9-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="615f9-165">Primo passaggio</span><span class="sxs-lookup"><span data-stu-id="615f9-165">First step</span></span>
<span data-ttu-id="615f9-166">Abbiamo consentono di raggiungere hello toocustomize dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="615f9-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="615f9-167">toodo, è necessario toocreate una sottoclasse di hello `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="615f9-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="615f9-168">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="615f9-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="615f9-169">Quindi, impostare il contenuto di hello di hello `EngagementReach.Instance.Handler` campo con l'oggetto personalizzato nel `App.xaml.cs` classe all'interno di hello `App()` metodo.</span><span class="sxs-lookup"><span data-stu-id="615f9-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="615f9-170">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="615f9-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="615f9-171">Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="615f9-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="615f9-172">Non è toocreate personalizzata, e se in tal caso, non è necessario toooverride ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="615f9-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="615f9-173">comportamento predefinito di Hello è oggetto di base di tooselect hello Engagement.</span><span class="sxs-lookup"><span data-stu-id="615f9-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="615f9-174">Visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="615f9-174">Web View</span></span>
<span data-ttu-id="615f9-175">Per impostazione predefinita, Reach utilizzerà hello incorporato di risorse di notifiche di hello DLL toodisplay hello e pagine.</span><span class="sxs-lookup"><span data-stu-id="615f9-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="615f9-176">una procedura completa di tooprovide il possibilità di personalizzazione si utilizza solo la visualizzazione web.</span><span class="sxs-lookup"><span data-stu-id="615f9-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="615f9-177">Se si desidera toocustomize layout, eseguire l'override direttamente i file di risorse hello `EngagementAnnouncement.html` e `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="615f9-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="615f9-178">Engagement deve tutto il codice in `<body></body>` toorun correttamente.</span><span class="sxs-lookup"><span data-stu-id="615f9-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="615f9-179">ma è possibile aggiungere tag esterni a `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="615f9-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="615f9-180">Tuttavia, è possibile decidere toouse le risorse.</span><span class="sxs-lookup"><span data-stu-id="615f9-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="615f9-181">È possibile eseguire l'override `EngagementReachHandler` i metodi toouse di Engagement tootell la sottoclasse i layout, ma utilizzare meccanismo engagement di attenzione tooembedded hello:</span><span class="sxs-lookup"><span data-stu-id="615f9-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="615f9-182">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="615f9-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="615f9-183">Per impostazione predefinita, AnnouncementHTML è `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="615f9-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="615f9-184">Rappresenta i file html hello che progettazione hello contenuto di un messaggio push (annuncio di testo, anoucement Web e di annuncio di polling).</span><span class="sxs-lookup"><span data-stu-id="615f9-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="615f9-185">AnnouncementName è `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="615f9-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="615f9-186">È il nome di hello della progettazione di webview hello nella pagina xaml.</span><span class="sxs-lookup"><span data-stu-id="615f9-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="615f9-187">NotificationHTML è `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="615f9-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="615f9-188">Rappresenta i file html hello che progettare hello notifica di un messaggio di push.</span><span class="sxs-lookup"><span data-stu-id="615f9-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="615f9-189">NotificationName è `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="615f9-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="615f9-190">È il nome di hello della progettazione di webview hello nella pagina xaml.</span><span class="sxs-lookup"><span data-stu-id="615f9-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="615f9-191">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="615f9-191">Customization</span></span>
<span data-ttu-id="615f9-192">È possibile personalizzare la visualizzazione Web di notifiche e annunci nel modo desiderato se si mantiene l'oggetto Engagement.</span><span class="sxs-lookup"><span data-stu-id="615f9-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="615f9-193">Fare attenzione che oggetto webview descritto tre volte - hello prima volta in xaml, secondo periodo di tempo in file con estensione cs nel metodo "setwebview()" hello e infine ora nel file html hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="615f9-194">In xaml è descrivere il componente corrente layout grafico webview hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="615f9-195">Nel file con estensione cs è possibile definire "setwebview()" in cui si imposta la dimensione hello di hello webview due (notifica, annuncio).</span><span class="sxs-lookup"><span data-stu-id="615f9-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="615f9-196">È molto utile durante il ridimensionamento di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="615f9-197">Nel file html di Engagement hello è descrivere hello webview contenuto, progettazione e hello posizioni di elementi tra loro.</span><span class="sxs-lookup"><span data-stu-id="615f9-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="615f9-198">Messaggio di avvio</span><span class="sxs-lookup"><span data-stu-id="615f9-198">Launch message</span></span>
<span data-ttu-id="615f9-199">Quando un utente fa clic su una notifica di sistema (un tipo di avviso popup), Engagement avvia un'applicazione hello, carico hello contenuto di hello il push dei messaggi e visualizzare la pagina hello campagna corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="615f9-200">Si verifica un ritardo tra l'avvio di hello del display di applicazione e hello hello della pagina hello (a seconda della velocità di hello della rete).</span><span class="sxs-lookup"><span data-stu-id="615f9-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="615f9-201">utente di toohello tooindicate che si sta caricando, è necessario fornire un informazioni visive, ad esempio una barra di stato o un indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="615f9-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="615f9-202">Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.</span><span class="sxs-lookup"><span data-stu-id="615f9-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="615f9-203">aggiungere i callback di hello tooimplement, in App.xaml.cs "Pubblica App() {}":</span><span class="sxs-lookup"><span data-stu-id="615f9-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="615f9-204">È possibile impostare il callback di hello nel metodo "Public App() {}" con il `App.xaml.cs` file, preferibilmente prima hello `EngagementReach.Instance.Init()` chiamare.</span><span class="sxs-lookup"><span data-stu-id="615f9-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="615f9-205">Ogni gestore viene chiamato dal Thread UI hello.</span><span class="sxs-lookup"><span data-stu-id="615f9-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="615f9-206">Non si dispone tooworry quando si utilizza un MessageBox o qualcosa correlate all'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="615f9-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="615f9-207"><a id="push-channel-sharing"></a> Condivisione del canale push</span><span class="sxs-lookup"><span data-stu-id="615f9-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="615f9-208">Se si utilizza le notifiche push per uno scopo diverso nell'applicazione è necessario canale di push hello toouse funzionalità di hello Engagement SDK per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="615f9-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="615f9-209">Si tratta di push tooavoid mancante.</span><span class="sxs-lookup"><span data-stu-id="615f9-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="615f9-210">È possibile fornire la propria inizializzazione di copertura di Engagement toohello push del canale.</span><span class="sxs-lookup"><span data-stu-id="615f9-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="615f9-211">Hello SDK utilizzeranno anziché richiedere uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="615f9-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="615f9-212">Aggiornare l'inizializzazione di copertura di Engagement hello con il canale di push in hello `InitEngagement` metodo hello `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="615f9-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="615f9-213">In alternativa, se si desidera tooconsume hello push canale dopo l'inizializzazione di copertura hello è possibile impostare un callback sul canale di copertura di Engagement tooget hello push dopo averla creata da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="615f9-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="615f9-214">Impostare il callback nel punto in cui **dopo** hello Reach inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="615f9-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="615f9-215">Suggerimento per lo schema</span><span class="sxs-lookup"><span data-stu-id="615f9-215">Custom scheme tip</span></span>
<span data-ttu-id="615f9-216">È possibile utilizzare uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="615f9-216">We provide custom scheme use.</span></span> <span data-ttu-id="615f9-217">È possibile inviare un tipo diverso di URI da engagement front-end toobe utilizzato nell'applicazione engagement.</span><span class="sxs-lookup"><span data-stu-id="615f9-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="615f9-218">Lo schema predefinito come `http, ftp, ...` è gestito da Windows. Una finestra chiederà se nel dispositivo sono installate applicazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="615f9-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="615f9-219">È possibile anche creare uno schema personalizzato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="615f9-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="615f9-220">Hello semplice tooset uno schema personalizzato nell'applicazione è tooopen il `Package.appxmanifest` andare in `Declarations` pannello.</span><span class="sxs-lookup"><span data-stu-id="615f9-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="615f9-221">Selezionare `Protocol` in hello dichiarazioni disponibili scorrere casella e aggiungerlo.</span><span class="sxs-lookup"><span data-stu-id="615f9-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="615f9-222">Modifica hello `Name` campo con il protocollo di nuovo il nome desiderato.</span><span class="sxs-lookup"><span data-stu-id="615f9-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="615f9-223">Ora toouse questo protocollo, modificare il `App.xaml.cs` con hello `OnActivated` (metodo) e non dimenticare di engagement tooinitialize qui anche:</span><span class="sxs-lookup"><span data-stu-id="615f9-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

