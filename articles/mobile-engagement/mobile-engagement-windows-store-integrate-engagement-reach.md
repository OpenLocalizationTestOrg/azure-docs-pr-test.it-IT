---
title: Integrazione di Reach SDK per app universali di Windows
description: Come integrare il servizio di copertura di Azure Mobile Engagement con le app universali di Windows
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="174b1-103">Integrazione di Reach SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="174b1-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="174b1-104">Prima di usare questa guida, è necessario eseguire la procedura di integrazione descritta nel documento [Integrazione di Mobile Engagement SDK per app di Windows universali](mobile-engagement-windows-store-integrate-engagement.md) .</span><span class="sxs-lookup"><span data-stu-id="174b1-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="174b1-105">Incorporare Engagement Reach SDK nel progetto di app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="174b1-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="174b1-106">Nessun elemento da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="174b1-106">You do not have anything to add.</span></span> <span data-ttu-id="174b1-107">`EngagementReach` sono già presenti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="174b1-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="174b1-108">È possibile personalizzare le immagini incluse nella cartella `Resources` del progetto, soprattutto l'icona del marchio, che per impostazione predefinita è l'icona di Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="174b1-109">Nelle app universali è inoltre possibile spostare la cartella `Resources` del progetto condiviso per condividere il contenuto tra app, ma è necessario mantenere il file `Resources\EngagementConfiguration.xml` nel percorso predefinito poiché è dipendente dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="174b1-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="174b1-110">Abilitare Servizi notifica Push Windows</span><span class="sxs-lookup"><span data-stu-id="174b1-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="174b1-111">Solo Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="174b1-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="174b1-112">Per usare **Servizi notifica Push Windows** (indicati come WNS) nel file `Package.appxmanifest` su `Application UI` fare clic su `All Image Assets` nella casella a sinistra.</span><span class="sxs-lookup"><span data-stu-id="174b1-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="174b1-113">A destra della casella in `Notifications`, modificare il valore di `toast capable` da `(not set)` a `(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="174b1-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="174b1-114">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="174b1-114">All platforms</span></span>
<span data-ttu-id="174b1-115">È necessario sincronizzare l'app con il proprio account Microsoft e con la piattaforma di Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="174b1-116">A questo scopo, è necessario creare un account o accedere al [Windows Dev Center](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="174b1-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="174b1-117">Creare quindi una nuova applicazione e individuare il SID e la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="174b1-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="174b1-118">Nel front-end di Engagement passare all'impostazione dell'app in `native push` e incollare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="174b1-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="174b1-119">Dopo questa operazione, fare clic sul progetto, selezionare `store` e `Associate App with the Store...`.</span><span class="sxs-lookup"><span data-stu-id="174b1-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="174b1-120">Per sincronizzare l'applicazione creata in precedenza, è sufficiente selezionarla.</span><span class="sxs-lookup"><span data-stu-id="174b1-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="174b1-121">Inizializzare Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="174b1-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="174b1-122">Modificare il file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="174b1-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="174b1-123">Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` nel metodo `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="174b1-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="174b1-124">`EngagementReach.Instance.Init` viene eseguito in un thread dedicato.</span><span class="sxs-lookup"><span data-stu-id="174b1-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="174b1-125">Non è necessario eseguirlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="174b1-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="174b1-126">Se si usano notifiche push in altre sezioni dell'applicazione, è necessario [condividere il canale di push](#push-channel-sharing) con Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="174b1-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="174b1-127">Integrazione</span><span class="sxs-lookup"><span data-stu-id="174b1-127">Integration</span></span>
<span data-ttu-id="174b1-128">Engagement offre due modi per aggiungere i banner in-app, le visualizzazioni intermedie di annunci e i sondaggi Reach all'applicazione: l'integrazione di una sovrimpressione e l'integrazione manuale di visualizzazioni Web.</span><span class="sxs-lookup"><span data-stu-id="174b1-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="174b1-129">È consigliabile non combinare entrambe le soluzioni nella stessa pagina.</span><span class="sxs-lookup"><span data-stu-id="174b1-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="174b1-130">La scelta tra uno dei due tipi d'integrazione può essere riassunta nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="174b1-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="174b1-131">Se le pagine ereditano già dall'agente `EngagementPage`, è consigliabile scegliere l'integrazione di una sovrimpressione. È sufficiente sostituire `EngagementPage` con `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` con `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nelle pagine.</span><span class="sxs-lookup"><span data-stu-id="174b1-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="174b1-132">È possibile scegliere l'integrazione manuale di visualizzazioni Web se si vuole inserire l'interfaccia utente di Reach in un punto preciso nelle pagine oppure se non si vuole aggiungere un altro livello di ereditarietà alle pagine.</span><span class="sxs-lookup"><span data-stu-id="174b1-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="174b1-133">Integrazione di una sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="174b1-133">Overlay integration</span></span>
<span data-ttu-id="174b1-134">La sovrimpressione di Engagement aggiunge in modo dinamico gli elementi dell'interfaccia utente utilizzati per visualizzare le campagne Reach nella pagina.</span><span class="sxs-lookup"><span data-stu-id="174b1-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="174b1-135">Se la sovrimpressione non è adatta al layout, considerare invece l'integrazione manuale delle visualizzazioni Web.</span><span class="sxs-lookup"><span data-stu-id="174b1-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="174b1-136">Nel file con estensione xaml modificare il riferimento `EngagementPage` in `EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="174b1-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="174b1-137">Aggiungere le dichiarazioni di spazi dei nomi:</span><span class="sxs-lookup"><span data-stu-id="174b1-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="174b1-138">Sostituire `engagement:EngagementPage` con `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="174b1-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="174b1-139">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="174b1-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="174b1-140">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="174b1-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="174b1-141">Quindi, nel file con estensione cs contrassegnare la pagina in `EngagementPageOverlay` anziché `EngagementPage` e importare `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="174b1-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="174b1-142">Sostituire `EngagementPage` con `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="174b1-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="174b1-143">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="174b1-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="174b1-144">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="174b1-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="174b1-145">La sovrimpressione di Engagement aggiunge un elemento `Grid` in alto alla pagina che è costituita dal layout e dai due elementi `WebView`, uno per il banner e l'altro per la visualizzazione intermedia.</span><span class="sxs-lookup"><span data-stu-id="174b1-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="174b1-146">È possibile personalizzare gli elementi della sovrimpressione direttamente nel file `EngagementPageOverlay.cs`.</span><span class="sxs-lookup"><span data-stu-id="174b1-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="174b1-147">Integrazione manuale delle visualizzazioni Web</span><span class="sxs-lookup"><span data-stu-id="174b1-147">Web views manual integration</span></span>
<span data-ttu-id="174b1-148">Reach cerca nelle pagine i due elementi `WebView` che determinano la visualizzazione del banner e della visualizzazione intermedia.</span><span class="sxs-lookup"><span data-stu-id="174b1-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="174b1-149">L'unica cosa necessaria da fare è aggiungere quei due elementi `WebView` in un punto qualsiasi delle pagine. Ecco un esempio:</span><span class="sxs-lookup"><span data-stu-id="174b1-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="174b1-150">In questo esempio gli elementi `WebView` vengono allungati per adattarsi al contenitore che automaticamente li ridimensiona nel caso in cui lo schermo viene ruotato o la dimensione della pagina cambia.</span><span class="sxs-lookup"><span data-stu-id="174b1-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="174b1-151">È importante che gli elementi `WebView` mantengano la stessa denominazione `engagement_notification_content` e `engagement_announcement_content`, poiché</span><span class="sxs-lookup"><span data-stu-id="174b1-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="174b1-152">Reach li identifica dal nome.</span><span class="sxs-lookup"><span data-stu-id="174b1-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="174b1-153">Gestire il push di dati (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="174b1-153">Handle datapush (optional)</span></span>
<span data-ttu-id="174b1-154">Se si desidera che l'applicazione sia in grado di ricevere push di dati Reach, è necessario implementare due eventi della classe EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="174b1-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="174b1-155">In App.xaml.cs nel costruttore App () aggiungere:</span><span class="sxs-lookup"><span data-stu-id="174b1-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="174b1-156">È possibile notare che il callback di ogni metodo restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="174b1-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="174b1-157">Engagement invia un feedback per il back-end dopo l'invio del push di dati.</span><span class="sxs-lookup"><span data-stu-id="174b1-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="174b1-158">Se il callback restituisce false, verrà inviato il feedback `exit` .</span><span class="sxs-lookup"><span data-stu-id="174b1-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="174b1-159">In caso contrario, il feedback sarà `action`.</span><span class="sxs-lookup"><span data-stu-id="174b1-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="174b1-160">Se non è impostato alcun callback per gli eventi, il feedback `drop` verrà restituito a Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="174b1-161">Engagement non è in grado di ricevere più feedback per un push di dati.</span><span class="sxs-lookup"><span data-stu-id="174b1-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="174b1-162">Se si prevede di impostare diversi gestori su un evento, tenere presente che il feedback corrisponderà all'ultimo inviato.</span><span class="sxs-lookup"><span data-stu-id="174b1-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="174b1-163">In questo caso, è consigliabile restituire sempre lo stesso valore per evitare confusione di feedback sul front-end.</span><span class="sxs-lookup"><span data-stu-id="174b1-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="174b1-164">Personalizzare l'interfaccia utente (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="174b1-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="174b1-165">Primo passaggio</span><span class="sxs-lookup"><span data-stu-id="174b1-165">First step</span></span>
<span data-ttu-id="174b1-166">È possibile personalizzare l'interfaccia utente di Reach.</span><span class="sxs-lookup"><span data-stu-id="174b1-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="174b1-167">A tale scopo, è necessario creare una sottoclasse della classe `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="174b1-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="174b1-168">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="174b1-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="174b1-169">Impostare quindi il contenuto del campo `EngagementReach.Instance.Handler` con l'oggetto personalizzato nella classe `App.xaml.cs` all'interno del metodo `App()`.</span><span class="sxs-lookup"><span data-stu-id="174b1-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="174b1-170">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="174b1-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="174b1-171">Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="174b1-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="174b1-172">Non è necessario crearne di proprie e, se ne viene creata una, non è necessario eseguire l'override di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="174b1-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="174b1-173">Il comportamento predefinito consiste nel selezionare l'oggetto di base di Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="174b1-174">Visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="174b1-174">Web View</span></span>
<span data-ttu-id="174b1-175">Per impostazione predefinita, Reach userà le risorse incorporate della DLL per visualizzare le pagine e le notifiche.</span><span class="sxs-lookup"><span data-stu-id="174b1-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="174b1-176">Per fornire possibilità di personalizzazione completa è utilizzata solo la visualizzazione Web.</span><span class="sxs-lookup"><span data-stu-id="174b1-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="174b1-177">Se si vuole personalizzare i layout, eseguire direttamente l'override dei file di risorse `EngagementAnnouncement.html` e `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="174b1-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="174b1-178">Engagement richiede tutto il codice in `<body></body>` per un'esecuzione corretta,</span><span class="sxs-lookup"><span data-stu-id="174b1-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="174b1-179">ma è possibile aggiungere tag esterni a `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="174b1-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="174b1-180">È tuttavia possibile usare le proprie risorse.</span><span class="sxs-lookup"><span data-stu-id="174b1-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="174b1-181">È possibile eseguire l'override dei metodi `EngagementReachHandler` in una sottoclasse per indicare a Engagement di usare i layout, ma fare attenzione al meccanismo di Engagement incorporato:</span><span class="sxs-lookup"><span data-stu-id="174b1-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="174b1-182">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="174b1-182">**Sample Code :**</span></span>

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


<span data-ttu-id="174b1-183">Per impostazione predefinita, AnnouncementHTML è `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="174b1-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="174b1-184">Rappresenta il file html per il progetto del contenuto di un messaggio push (annuncio di testo, annuncio Web e annuncio di sondaggio).</span><span class="sxs-lookup"><span data-stu-id="174b1-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="174b1-185">AnnouncementName è `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="174b1-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="174b1-186">È il nome del progetto webview nella pagina xaml.</span><span class="sxs-lookup"><span data-stu-id="174b1-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="174b1-187">NotificationHTML è `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="174b1-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="174b1-188">Rappresenta il file html per il progetto la notifica di un messaggio di push.</span><span class="sxs-lookup"><span data-stu-id="174b1-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="174b1-189">NotificationName è `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="174b1-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="174b1-190">È il nome del progetto webview nella pagina xaml.</span><span class="sxs-lookup"><span data-stu-id="174b1-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="174b1-191">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="174b1-191">Customization</span></span>
<span data-ttu-id="174b1-192">È possibile personalizzare la visualizzazione Web di notifiche e annunci nel modo desiderato se si mantiene l'oggetto Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="174b1-193">Tenere presente che l'oggetto webview è descritto tre volte. La prima volta in xaml, la seconda nel file cs nel metodo "setwebview()" e la terza nel file html.</span><span class="sxs-lookup"><span data-stu-id="174b1-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="174b1-194">Nel file xaml si descrive il componente di webview del layout grafico corrente.</span><span class="sxs-lookup"><span data-stu-id="174b1-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="174b1-195">Nel file cs è possibile definire "setwebview()" in cui è possibile impostare la dimensione delle due webview (notifica, annuncio).</span><span class="sxs-lookup"><span data-stu-id="174b1-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="174b1-196">Questa operazione è molto efficace per il ridimensionamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="174b1-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="174b1-197">Nel file html di Engagement viene descritto il contenuto della visualizzazione Web, il progetto e le posizioni degli elementi.</span><span class="sxs-lookup"><span data-stu-id="174b1-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="174b1-198">Messaggio di avvio</span><span class="sxs-lookup"><span data-stu-id="174b1-198">Launch message</span></span>
<span data-ttu-id="174b1-199">Quando un utente fa clic su una notifica del sistema (avviso popup), Engagement avvia l'applicazione, carica il contenuto dei messaggi di push e visualizza la pagina per la campagna corrispondente.</span><span class="sxs-lookup"><span data-stu-id="174b1-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="174b1-200">Tra l'avvio dell'applicazione e la visualizzazione della pagina si verifica un ritardo (a seconda della velocità della rete).</span><span class="sxs-lookup"><span data-stu-id="174b1-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="174b1-201">Per indicare all'utente che è in corso un caricamento, è necessario fornire un'indicazione visiva, ad esempio una barra o un indicatore di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="174b1-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="174b1-202">Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.</span><span class="sxs-lookup"><span data-stu-id="174b1-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="174b1-203">Per implementare il callback, in App.xaml.cs in "Public App(){}" aggiungere:</span><span class="sxs-lookup"><span data-stu-id="174b1-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="174b1-204">È possibile impostare il callback nel metodo "Public App(){}" del file `App.xaml.cs`, preferibilmente prima della chiamata `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="174b1-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="174b1-205">Ogni gestore viene chiamato dal thread dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="174b1-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="174b1-206">Non è necessario preoccuparsi quando si utilizza MessageBox o un elemento correlato all'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="174b1-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="174b1-207"><a id="push-channel-sharing"></a> Condivisione del canale push</span><span class="sxs-lookup"><span data-stu-id="174b1-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="174b1-208">Se si usano notifiche push per altri scopi all'interno dell'applicazione, è necessario usare la funzione di condivisone del canale push di Engagement SDK,</span><span class="sxs-lookup"><span data-stu-id="174b1-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="174b1-209">in modo da evitare la perdita di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="174b1-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="174b1-210">È possibile specificare il canale push desiderato durante la procedura di inizializzazione di Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="174b1-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="174b1-211">In questo modo, l'SDK userà il canale specificato anziché richiederne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="174b1-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="174b1-212">Aggiornare l'inizializzazione di Engagement Reach con il canale push nel metodo `InitEngagement` ottenuto dal file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="174b1-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="174b1-213">In alternativa, se si decide di usare il canale push dopo l'inizializzazione di Reach, è possibile impostare un callback su Engagement Reach per ottenere il canale push creato dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="174b1-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="174b1-214">Impostare il callback in un momento qualsiasi **dopo** l'inizializzazione di Reach:</span><span class="sxs-lookup"><span data-stu-id="174b1-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="174b1-215">Suggerimento per lo schema</span><span class="sxs-lookup"><span data-stu-id="174b1-215">Custom scheme tip</span></span>
<span data-ttu-id="174b1-216">È possibile utilizzare uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="174b1-216">We provide custom scheme use.</span></span> <span data-ttu-id="174b1-217">È possibile inviare un tipo diverso di URI dal front-end di Engagement da utilizzare nell'applicazione Engagement.</span><span class="sxs-lookup"><span data-stu-id="174b1-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="174b1-218">Lo schema predefinito come `http, ftp, ...` è gestito da Windows. Una finestra chiederà se nel dispositivo sono installate applicazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="174b1-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="174b1-219">È possibile anche creare uno schema personalizzato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="174b1-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="174b1-220">Il metodo semplice per impostare uno schema personalizzato nell'applicazione consiste nell'aprire `Package.appxmanifest` e andare nel pannello `Declarations`.</span><span class="sxs-lookup"><span data-stu-id="174b1-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="174b1-221">Selezionare `Protocol` nella casella di scorrimento Dichiarazioni disponibili e aggiungerlo.</span><span class="sxs-lookup"><span data-stu-id="174b1-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="174b1-222">Modificare il campo `Name` con il nuovo nome desiderato per il protocollo.</span><span class="sxs-lookup"><span data-stu-id="174b1-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="174b1-223">Per usare questo protocollo modificare `App.xaml.cs` con il metodo `OnActivated` e non dimenticare di inizializzare Engagement anche qui:</span><span class="sxs-lookup"><span data-stu-id="174b1-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

