---
title: aaaGet avviato con Windows Universal App Azure Mobile Engagement
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per App universali di Windows.
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
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="336c7-103">Introduzione a Azure Mobile Engagement per app di Windows universali</span><span class="sxs-lookup"><span data-stu-id="336c7-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="336c7-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche di un'applicazione Windows universale.</span><span class="sxs-lookup"><span data-stu-id="336c7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="336c7-105">Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="336c7-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="336c7-106">Si crea un'app universale di Windows vuota che raccoglie dati di base relativi all'utilizzo dell'app e riceve notifiche push tramite Servizi notifica Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="336c7-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="336c7-107">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="336c7-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="336c7-108">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="336c7-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="336c7-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="336c7-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="336c7-110">Configurare Mobile Engagement per l'app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="336c7-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="336c7-111"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="336c7-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="336c7-112">Questa esercitazione viene illustrato una "integrazione di base," hello minimo imposta dati toocollect necessarie e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="336c7-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="336c7-113">la documentazione completa integrazione Hello è reperibile in hello [integrazione Windows Mobile Engagement SDK universale](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="336c7-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="336c7-114">Creare un'app di base con l'integrazione di Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="336c7-115">Creare un progetto di app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="336c7-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="336c7-116">Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="336c7-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="336c7-117">Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="336c7-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="336c7-118">Nel menu a comparsa hello, selezionare **Windows** -> **Universal** -> **App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="336c7-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="336c7-119">Compilare app hello **nome** e **Nome soluzione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="336c7-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="336c7-120">Ora è stata creata un progetto di App universali di Windows in cui è stato quindi integrare hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="336c7-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="336c7-121">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="336c7-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="336c7-122">Installare hello [MicrosoftAzure.MobileEngagement] pacchetto Nuget nel progetto.</span><span class="sxs-lookup"><span data-stu-id="336c7-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="336c7-123">Se la destinazione piattaforme Windows e Windows Phone, è necessario toodo questo per entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="336c7-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="336c7-124">Per Windows 8. x e Windows Phone 8.1, hello stesso Nuget pacchetto posizioni hello corretto specifico della piattaforma i file binari in ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="336c7-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="336c7-125">Aprire **package. appxmanifest** e verificare che tale hello funzionalità seguente viene aggiunto sono:</span><span class="sxs-lookup"><span data-stu-id="336c7-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="336c7-126">Ora di copiare una stringa di connessione hello copiato in precedenza per l'applicazione di Mobile Engagement e incollarlo in hello `Resources\EngagementConfiguration.xml` file tra hello `<connectionString>` e `</connectionString>` tag:</span><span class="sxs-lookup"><span data-stu-id="336c7-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="336c7-127">Se l'app è destinata a entrambe le piattaforme Windows e Windows Phone, è comunque preferibile creare due applicazioni Mobile Engagement, una per ogni piattaforma supportata.</span><span class="sxs-lookup"><span data-stu-id="336c7-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="336c7-128">La presenza di due App assicura che è possibile creare corretta segmentazione dei destinatari hello e che si possono inviare le notifiche di destinazione in modo appropriato per ogni piattaforma.</span><span class="sxs-lookup"><span data-stu-id="336c7-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="336c7-129">NuGet non copia automaticamente le risorse SDK hello nell'applicazione UWP Windows 10.</span><span class="sxs-lookup"><span data-stu-id="336c7-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="336c7-130">È stata toodo manualmente seguendo i passaggi di hello cui visualizzati quando viene installato il pacchetto Nuget di hello (Readme. txt).</span><span class="sxs-lookup"><span data-stu-id="336c7-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="336c7-131">In hello `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="336c7-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="336c7-132">a.</span><span class="sxs-lookup"><span data-stu-id="336c7-132">a.</span></span> <span data-ttu-id="336c7-133">Aggiungere hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="336c7-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="336c7-134">b.</span><span class="sxs-lookup"><span data-stu-id="336c7-134">b.</span></span> <span data-ttu-id="336c7-135">Aggiungere un metodo che inizializza hello Engagement:</span><span class="sxs-lookup"><span data-stu-id="336c7-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="336c7-136">c.</span><span class="sxs-lookup"><span data-stu-id="336c7-136">c.</span></span> <span data-ttu-id="336c7-137">Inizializzare Ciao SDK hello **OnLaunched** metodo:</span><span class="sxs-lookup"><span data-stu-id="336c7-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="336c7-138">c.</span><span class="sxs-lookup"><span data-stu-id="336c7-138">c.</span></span> <span data-ttu-id="336c7-139">Inserire il seguente hello in hello **OnActivated** (metodo) e, se non è già presente, aggiungere il metodo hello:</span><span class="sxs-lookup"><span data-stu-id="336c7-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="336c7-140"><a id="monitor"></a>Abilitare il monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="336c7-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="336c7-141">toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).</span><span class="sxs-lookup"><span data-stu-id="336c7-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="336c7-142">In hello **MainPage.xaml.cs**, aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="336c7-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="336c7-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="336c7-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="336c7-144">Classe di base hello di **MainPage** da **pagina** troppo**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="336c7-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="336c7-145">In hello `MainPage.xaml` file:</span><span class="sxs-lookup"><span data-stu-id="336c7-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="336c7-146">a.</span><span class="sxs-lookup"><span data-stu-id="336c7-146">a.</span></span> <span data-ttu-id="336c7-147">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="336c7-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="336c7-148">b.</span><span class="sxs-lookup"><span data-stu-id="336c7-148">b.</span></span> <span data-ttu-id="336c7-149">Sostituire hello **pagina** nei nomi di tag XML hello con **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="336c7-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="336c7-150">Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="336c7-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="336c7-151">In caso contrario, non viene riportata l'attività di hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="336c7-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="336c7-152">Ciò è particolarmente importante in un progetto Windows Phone in cui il modello predefinito di hello ha un `OnNavigatedTo` metodo.</span><span class="sxs-lookup"><span data-stu-id="336c7-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="336c7-153">Per **App universali di Windows 10**, utilizzare il metodo hello consigliato in hello "metodo consigliato: eseguire l'overload di classi di pagina" sezione di [avanzate Reporting con hello Windows Universal App Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md) , invece di hello uno indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="336c7-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="336c7-154"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="336c7-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="336c7-155"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="336c7-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="336c7-156">Engagement mobile permette toointeract e raggiungere gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="336c7-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="336c7-157">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="336c7-158">Hello nelle sezioni seguenti impostarle backup tooreceive l'app.</span><span class="sxs-lookup"><span data-stu-id="336c7-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="336c7-159">Abilitare il tooreceive app le notifiche Push WNS</span><span class="sxs-lookup"><span data-stu-id="336c7-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="336c7-160">In hello `Package.appxmanifest` file hello **applicazione** scheda **notifiche**, impostare **popup:** troppo**Sì**</span><span class="sxs-lookup"><span data-stu-id="336c7-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="336c7-161">Inizializzare hello REACH SDK</span><span class="sxs-lookup"><span data-stu-id="336c7-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="336c7-162">In `App.xaml.cs`, chiamare **EngagementReach.Instance.Init(e);** in hello **InitEngagement** funzione subito dopo l'inizializzazione dell'agente di hello:</span><span class="sxs-lookup"><span data-stu-id="336c7-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="336c7-163">Si è pronti toosend un avviso popup.</span><span class="sxs-lookup"><span data-stu-id="336c7-163">You're ready toosend a toast.</span></span> <span data-ttu-id="336c7-164">Viene quindi verificato che l'integrazione di base sia stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="336c7-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="336c7-165">Concedere accesso tooMobile Engagement toosend notifiche</span><span class="sxs-lookup"><span data-stu-id="336c7-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="336c7-166">Aprire [Dev Center per Windows Store] nel Web browser, accedere e creare un account, se necessario.</span><span class="sxs-lookup"><span data-stu-id="336c7-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="336c7-167">Fare clic su **Dashboard** angolo hello in alto a destra e quindi fare clic su **crea una nuova app** dal menu Pannello sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="336c7-168">Creare l'app riservandone il nome.</span><span class="sxs-lookup"><span data-stu-id="336c7-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="336c7-169">Dopo aver creato l'applicazione hello, passare troppo**servizi -> notifiche Push** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="336c7-170">In hello Push sezione notifiche, fare clic su hello **sito Services Live** collegamento.</span><span class="sxs-lookup"><span data-stu-id="336c7-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="336c7-171">Passare toohello relativa alle credenziali Push.</span><span class="sxs-lookup"><span data-stu-id="336c7-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="336c7-172">Verificare di disporre in hello **impostazioni App** sezione e quindi copiare il **SID pacchetto** e **segreto Client**</span><span class="sxs-lookup"><span data-stu-id="336c7-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="336c7-173">Passare toohello **impostazioni** del portale Mobile Engagement e fare clic su hello **Push nativo** sezione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="336c7-174">Quindi, fare clic su hello **modifica** tooenter pulsante il **ID di pacchetto sicurezza (SID)** e **chiave privata** come illustrato:</span><span class="sxs-lookup"><span data-stu-id="336c7-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="336c7-175">Verificare infine che è stato associato l'app di Visual Studio con questa app creata nell'archivio di App hello.</span><span class="sxs-lookup"><span data-stu-id="336c7-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="336c7-176">Fare clic su **Associa applicazione a Store** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="336c7-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="336c7-177"><a id="send"></a>Invia un'app tooyour notifica</span><span class="sxs-lookup"><span data-stu-id="336c7-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="336c7-178">Se l'applicazione hello è in esecuzione, si noterà una notifica in-app.</span><span class="sxs-lookup"><span data-stu-id="336c7-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="336c7-179">in caso contrario, se l'applicazione hello è chiuso, viene visualizzata una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="336c7-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="336c7-180">Se è visualizzata una notifica in-app, ma non una notifica di tipo avviso popup e si esegue l'applicazione hello in modalità di debug in Visual Studio, quindi provare a **gli eventi del ciclo di vita -> Sospendi** in hello barra degli strumenti tooensure app hello è sospeso.</span><span class="sxs-lookup"><span data-stu-id="336c7-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="336c7-181">Se si fa clic sul pulsante Home hello durante il debug di un'applicazione hello in Visual Studio, quindi non sempre sospesi e durante la notifica hello viene visualizzato come in-app, non viene visualizzata come una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="336c7-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Dev Center per Windows Store]: https://dev.windows.com
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
