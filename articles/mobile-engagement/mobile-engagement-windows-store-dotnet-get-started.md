---
title: Introduzione ad Azure Mobile Engagement per app universali di Windows
description: "Informazioni sull'uso di Azure Mobile Engagement con funzionalità di analisi e notifiche push per le app di Windows universali."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="0011e-103">Introduzione a Azure Mobile Engagement per app di Windows universali</span><span class="sxs-lookup"><span data-stu-id="0011e-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="0011e-104">Questo argomento descrive come usare Azure Mobile Engagement per ottenere informazioni sull'utilizzo dell'app e inviare notifiche push a utenti segmentati di un'applicazione universale di Windows.</span><span class="sxs-lookup"><span data-stu-id="0011e-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="0011e-105">Questa esercitazione illustra uno scenario di trasmissione semplice tramite Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0011e-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="0011e-106">Si crea un'app universale di Windows vuota che raccoglie dati di base relativi all'utilizzo dell'app e riceve notifiche push tramite Servizi notifica Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="0011e-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="0011e-107">Il servizio Azure Mobile Engagement verrà ritirato a marzo 2018 ed è attualmente disponibile solo per i clienti esistenti.</span><span class="sxs-lookup"><span data-stu-id="0011e-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="0011e-108">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="0011e-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0011e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0011e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="0011e-110">Configurare Mobile Engagement per l'app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="0011e-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="0011e-111"><a id="connecting-app"></a>Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0011e-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="0011e-112">Questa esercitazione presenta una "integrazione di base", che è la configurazione minima necessaria per raccogliere i dati e inviare una notifica push.</span><span class="sxs-lookup"><span data-stu-id="0011e-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="0011e-113">La documentazione sull'integrazione completa è reperibile nella [integrazione di Mobile Engagement SDK per app di Windows universali](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0011e-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="0011e-114">Si crea un'app di base con Visual Studio per illustrare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="0011e-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="0011e-115">Creare un progetto di app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="0011e-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="0011e-116">I passaggi seguenti presuppongono l'utilizzo di Visual Studio 2015 anche se i passaggi sono simili nelle versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0011e-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="0011e-117">Avviare Visual Studio e selezionare **Nuovo progetto** nella schermata **Home**.</span><span class="sxs-lookup"><span data-stu-id="0011e-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="0011e-118">Nel popup selezionare **Windows** -> **Universal** -> **App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="0011e-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="0011e-119">Inserire **Nome** e **Nome soluzione** dell'app, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0011e-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="0011e-120">A questo punto è stata creata un'app universale di Windows in cui si integra quindi Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="0011e-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="0011e-121">Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0011e-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="0011e-122">Installare il pacchetto NuGet [MicrosoftAzure.MobileEngagement] nel progetto.</span><span class="sxs-lookup"><span data-stu-id="0011e-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="0011e-123">Se l'app è destinata a entrambe le piattaforme Windows e Windows Phone, è necessario eseguire questa operazione per entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="0011e-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="0011e-124">Per Windows 8.x e Windows Phone 8.1, lo stesso pacchetto NuGet inserisce i file binari corretti specifici della piattaforma in ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="0011e-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="0011e-125">Aprire **Package.appxmanifest** e assicurarsi che venga aggiunta la funzionalità seguente:</span><span class="sxs-lookup"><span data-stu-id="0011e-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="0011e-126">Copiare la stringa di connessione copiata in precedenza per l'app Mobile Engagement e incollarla nel file `Resources\EngagementConfiguration.xml`, tra i tag `<connectionString>` e `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="0011e-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="0011e-127">Se l'app è destinata a entrambe le piattaforme Windows e Windows Phone, è comunque preferibile creare due applicazioni Mobile Engagement, una per ogni piattaforma supportata.</span><span class="sxs-lookup"><span data-stu-id="0011e-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="0011e-128">Avere due app garantisce di poter definire la segmentazione corretta dei destinatari e di poter inviare notifiche opportunamente mirate per ogni piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0011e-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0011e-129">NuGet non copia automaticamente le risorse SDK nell'applicazione UWP di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0011e-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="0011e-130">È necessario copiare le risorse manualmente seguendo i passaggi (Leggimi.txt) visualizzati durante l'installazione del pacchetto Nuget.</span><span class="sxs-lookup"><span data-stu-id="0011e-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="0011e-131">Nel file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="0011e-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="0011e-132">a.</span><span class="sxs-lookup"><span data-stu-id="0011e-132">a.</span></span> <span data-ttu-id="0011e-133">Aggiungere l'istruzione `using`:</span><span class="sxs-lookup"><span data-stu-id="0011e-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="0011e-134">b.</span><span class="sxs-lookup"><span data-stu-id="0011e-134">b.</span></span> <span data-ttu-id="0011e-135">Aggiungere un metodo che inizializza la soluzione di engagement:</span><span class="sxs-lookup"><span data-stu-id="0011e-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="0011e-136">c.</span><span class="sxs-lookup"><span data-stu-id="0011e-136">c.</span></span> <span data-ttu-id="0011e-137">Inizializzare l'SDK nel metodo **OnLaunched** :</span><span class="sxs-lookup"><span data-stu-id="0011e-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="0011e-138">c.</span><span class="sxs-lookup"><span data-stu-id="0011e-138">c.</span></span> <span data-ttu-id="0011e-139">Inserire il codice seguente nel metodo **OnActivated** e aggiungere il metodo, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="0011e-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="0011e-140"><a id="monitor"></a>Abilitare il monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="0011e-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="0011e-141">Per iniziare a inviare dati e assicurarsi che gli utenti siano attivi, è necessario inviare almeno una schermata (Activity) al back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0011e-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="0011e-142">Nel file **MainPage.xaml.cs** aggiungere l'istruzione `using` seguente:</span><span class="sxs-lookup"><span data-stu-id="0011e-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="0011e-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="0011e-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="0011e-144">Modificare la classe base di **MainPage** da **Page** a **EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="0011e-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="0011e-145">Nel file `MainPage.xaml`:</span><span class="sxs-lookup"><span data-stu-id="0011e-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="0011e-146">a.</span><span class="sxs-lookup"><span data-stu-id="0011e-146">a.</span></span> <span data-ttu-id="0011e-147">Aggiungere le dichiarazioni di spazi dei nomi:</span><span class="sxs-lookup"><span data-stu-id="0011e-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="0011e-148">b.</span><span class="sxs-lookup"><span data-stu-id="0011e-148">b.</span></span> <span data-ttu-id="0011e-149">Sostituire **Page** nel nome del tag XML con **engagement:EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="0011e-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0011e-150">Se la pagina esegue l'override del metodo `OnNavigatedTo`, accertarsi di chiamare `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="0011e-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="0011e-151">In caso contrario, l'attività non viene segnalata. `EngagementPage` chiama `StartActivity` nel metodo `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="0011e-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="0011e-152">Questo aspetto è particolarmente importante in un progetto Windows Phone in cui il modello predefinito ha un metodo `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="0011e-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="0011e-153">Per le **app universali di Windows 10**, usare il metodo consigliato nella sezione "Metodo consigliato: eseguire l'overload delle classi Pages" dell'articolo [Segnalazione avanzata con Engagement SDK per le app di Windows universali](mobile-engagement-windows-store-advanced-reporting.md) anziché quello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0011e-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="0011e-154"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="0011e-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="0011e-155"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="0011e-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="0011e-156">Mobile Engagement consente di interagire con gli utenti e coinvolgerli tramite notifiche push e messaggistica in-app nel contesto di campagne.</span><span class="sxs-lookup"><span data-stu-id="0011e-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="0011e-157">Questo modulo è denominato REACH nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0011e-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="0011e-158">Le sezioni seguenti consentono di configurare l'app per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="0011e-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="0011e-159">Abilitare l'app alla ricezione di notifiche push WNS</span><span class="sxs-lookup"><span data-stu-id="0011e-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="0011e-160">Nel file `Package.appxmanifest` scegliere la scheda **Applicazione** e impostare **Popup supportati** su **Sì** in **Notifiche**</span><span class="sxs-lookup"><span data-stu-id="0011e-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="0011e-161">Inizializzare REACH SDK</span><span class="sxs-lookup"><span data-stu-id="0011e-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="0011e-162">In `App.xaml.cs` chiamare **EngagementReach.Instance.Init(e);** nella funzione **InitEngagement** subito dopo l'inizializzazione dell'agente:</span><span class="sxs-lookup"><span data-stu-id="0011e-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="0011e-163">Ora è possibile inviare un avviso popup.</span><span class="sxs-lookup"><span data-stu-id="0011e-163">You're ready to send a toast.</span></span> <span data-ttu-id="0011e-164">Viene quindi verificato che l'integrazione di base sia stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="0011e-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="0011e-165">Concedere l'accesso a Mobile Engagement per inviare notifiche</span><span class="sxs-lookup"><span data-stu-id="0011e-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="0011e-166">Aprire [Dev Center per Windows Store] nel Web browser, accedere e creare un account, se necessario.</span><span class="sxs-lookup"><span data-stu-id="0011e-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="0011e-167">Fare clic su **Dashboard** nell'angolo superiore destro, quindi scegliere **Crea una nuova app** dal menu nel pannello sinistro.</span><span class="sxs-lookup"><span data-stu-id="0011e-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="0011e-168">Creare l'app riservandone il nome.</span><span class="sxs-lookup"><span data-stu-id="0011e-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="0011e-169">Dopo la creazione dell'app, passare a **Servizi -> Notifiche push** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0011e-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="0011e-170">Nella sezione Notifiche push fare clic sul collegamento del **sito dei servizi Live** .</span><span class="sxs-lookup"><span data-stu-id="0011e-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="0011e-171">Viene visualizzata la sezione relativa alle credenziali push.</span><span class="sxs-lookup"><span data-stu-id="0011e-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="0011e-172">Assicurarsi di trovarsi nella sezione **Impostazioni app** e quindi copiare i valori di **SID pacchetto** e **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="0011e-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="0011e-173">Passare a **Impostazioni** del portale Mobile Engagement e fare clic sulla sezione **Push nativo** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0011e-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="0011e-174">Fare quindi clic sul pulsante **Modifica** per immettere l'**ID di sicurezza (SID) del pacchetto** e la **Chiave privata**, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="0011e-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="0011e-175">Assicurarsi infine di avere associato l'app di Visual Studio all'app creata nell'App Store.</span><span class="sxs-lookup"><span data-stu-id="0011e-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="0011e-176">Fare clic su **Associa applicazione a Store** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0011e-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="0011e-177"><a id="send"></a>Inviare una notifica all'app</span><span class="sxs-lookup"><span data-stu-id="0011e-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="0011e-178">Se l'app è in esecuzione, viene visualizzata una notifica in-app.</span><span class="sxs-lookup"><span data-stu-id="0011e-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="0011e-179">In caso contrario, se l'app è chiusa, viene visualizzata una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="0011e-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="0011e-180">Se viene visualizzata una notifica in-app, ma non una notifica di tipo avviso popup e si esegue l'app in modalità debug in Visual Studio, provare a selezionare **Eventi ciclo di vita -> Sospendi** sulla barra degli strumenti per assicurarsi che l'app venga sospesa.</span><span class="sxs-lookup"><span data-stu-id="0011e-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="0011e-181">Se è stato fatto clic sul pulsante Home durante il debug dell'applicazione in Visual Studio, non sempre viene sospesa e, anche se la notifica viene visualizzata come in-app, non compare come notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="0011e-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="0011e-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="0011e-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="0011e-183">[Dev Center per Windows Store]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="0011e-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
