---
title: aaaGet avviato con gli hub di notifica per le app xamarin | Documenti Microsoft
description: "In questa esercitazione, è illustrato toouse gli hub di notifica di Azure toosend push notifiche tooa applicazione Android di Xamarin."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="887a5-103">Introduzione ad Hub di notifica con Xamarin per Android</span><span class="sxs-lookup"><span data-stu-id="887a5-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="887a5-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="887a5-104">Overview</span></span>
<span data-ttu-id="887a5-105">Questa esercitazione illustra applicazione xamarin tooa di notifiche push toouse toosend di hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="887a5-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="887a5-106">Verrà creata un'app per Xamarin.Android vuota che riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="887a5-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="887a5-107">Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="887a5-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="887a5-108">Hello codice completato è disponibile in hello [app hub di notifica] [ GitHub] esempio.</span><span class="sxs-lookup"><span data-stu-id="887a5-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="887a5-109">In questa esercitazione illustra hello semplice scenario di trasmissione con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="887a5-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="887a5-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="887a5-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="887a5-111">codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="887a5-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="887a5-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="887a5-112">Prerequisites</span></span>
<span data-ttu-id="887a5-113">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="887a5-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="887a5-114">Visual Studio con Xamarin su Windows o Xamarin Studio su Mac OS X. Per istruzioni complete sull'installazione , vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="887a5-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="887a5-115">Un account Google attivo</span><span class="sxs-lookup"><span data-stu-id="887a5-115">Active Google account</span></span>
* <span data-ttu-id="887a5-116">[Componente di messaggistica di Azure]</span><span class="sxs-lookup"><span data-stu-id="887a5-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="887a5-117">[Componente client di Google Cloud Messaging]</span><span class="sxs-lookup"><span data-stu-id="887a5-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="887a5-118">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="887a5-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="887a5-119">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="887a5-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="887a5-120">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="887a5-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="887a5-121">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="887a5-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="887a5-122">Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="887a5-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="887a5-123">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="887a5-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="887a5-124">Fare clic su hello <b>configura</b> scheda nella parte superiore di hello, immettere hello <b>chiave API</b> valore ottenuto nella sezione precedente hello e quindi fare clic su <b>salvare</b>.</span><span class="sxs-lookup"><span data-stu-id="887a5-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="887a5-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="887a5-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="887a5-126">Hub di notifica è ora configurato toowork con GCM, e tooboth stringhe di connessione hello necessario registrare l'app tooreceive e alle notifiche toosend push.</span><span class="sxs-lookup"><span data-stu-id="887a5-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="887a5-127">Connettere l'hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="887a5-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="887a5-128">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="887a5-128">Create a new project</span></span>
1. <span data-ttu-id="887a5-129">In Xamarin Studio fare clic su **New Solution** (Nuova soluzione), **Android App** (App Android) e selezionare **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="887a5-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="887a5-130">Compilare i campi **App Name** (Nome app) e **Identifier** (Identificatore).</span><span class="sxs-lookup"><span data-stu-id="887a5-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="887a5-131">Fare clic su hello **le piattaforme di destinazione** toosupport desiderato e quindi fare clic su **Avanti** e **crea**.</span><span class="sxs-lookup"><span data-stu-id="887a5-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="887a5-132">In questo modo viene creato un nuovo progetto Android.</span><span class="sxs-lookup"><span data-stu-id="887a5-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="887a5-133">Aprire le proprietà del progetto hello facendo clic di nuovo progetto hello visualizzazione soluzioni e scegliendo **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="887a5-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="887a5-134">Seleziona hello **applicazione Android** elemento hello **compilare** sezione.</span><span class="sxs-lookup"><span data-stu-id="887a5-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="887a5-135">Verificare che la prima lettera di hello del **nome pacchetto** è in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="887a5-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="887a5-136">Hello prima lettera del nome del pacchetto hello deve essere minuscola.</span><span class="sxs-lookup"><span data-stu-id="887a5-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="887a5-137">In caso contrario, verranno visualizzati errori del manifesto dell'applicazione al momento della registrazione di **BroadcastReceiver** e **IntentFilter** per le notifiche push più avanti.</span><span class="sxs-lookup"><span data-stu-id="887a5-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="887a5-138">Facoltativamente, set hello **minimo Android versione** tooanother livello API.</span><span class="sxs-lookup"><span data-stu-id="887a5-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="887a5-139">Facoltativamente, set hello **versione di destinazione Android** toohello un'altra versione dell'API che si desidera tootarget (deve essere livello API 8 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="887a5-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="887a5-140">Fare clic su **OK** e finestra di dialogo Project Options hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="887a5-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="887a5-141">Aggiungi progetto tooyour componenti necessari di hello</span><span class="sxs-lookup"><span data-stu-id="887a5-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="887a5-142">Hello Google Cloud Messaging Client disponibile in hello archivio componenti Xamarin semplifica il processo di hello di supportare le notifiche push in xamarin.</span><span class="sxs-lookup"><span data-stu-id="887a5-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="887a5-143">Fare clic sulla cartella componenti hello in app xamarin e scegliere **ottenere più componenti**.</span><span class="sxs-lookup"><span data-stu-id="887a5-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="887a5-144">Ricerca di hello **messaggistica di Azure** componente e aggiungerlo toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="887a5-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="887a5-145">Ricerca di hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="887a5-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="887a5-146">Configurare Hub di notifica nel progetto</span><span class="sxs-lookup"><span data-stu-id="887a5-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="887a5-147">Raccogliere le seguenti informazioni per l'hub di notifica e di app Android hello:</span><span class="sxs-lookup"><span data-stu-id="887a5-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="887a5-148">**GoogleProjectNumber**: ottenere questo valore di numero progetto dal dashboard Panoramica hello dell'applicazione hello portale per sviluppatori Google.</span><span class="sxs-lookup"><span data-stu-id="887a5-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="887a5-149">Durante la creazione di app hello nel portale di hello apportate una nota di questo valore in precedenza.</span><span class="sxs-lookup"><span data-stu-id="887a5-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="887a5-150">**Stringa di connessione in attesa**: nel dashboard di hello in hello [portale di Azure classico], fare clic su **consente di visualizzare le stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="887a5-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="887a5-151">Hello copia *DefaultListenSharedAccessSignature* stringa di connessione per questo valore.</span><span class="sxs-lookup"><span data-stu-id="887a5-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="887a5-152">**Nome dell'hub**: questo è il nome di hello dell'hub da hello [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="887a5-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="887a5-153">Ad esempio, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="887a5-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="887a5-154">Creare un **Constants.cs** classe per il progetto Xamarin e definire i seguenti valori costanti in una classe hello hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="887a5-155">Sostituire i segnaposto hello con i valori.</span><span class="sxs-lookup"><span data-stu-id="887a5-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="887a5-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="887a5-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="887a5-157">}</span><span class="sxs-lookup"><span data-stu-id="887a5-157">}</span></span>
2. <span data-ttu-id="887a5-158">Aggiungere il seguente hello utilizzando istruzioni troppo**Mainactivity**:</span><span class="sxs-lookup"><span data-stu-id="887a5-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="887a5-159">Aggiungere un toohello variabile di istanza `MainActivity` classe che verrà utilizzato tooshow una finestra di dialogo di avviso quando l'applicazione hello è in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="887a5-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="887a5-160">Creare hello al metodo in hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="887a5-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="887a5-161">In hello `OnCreate` metodo **Mainactivity**, inizializzare hello `instance` variabile e aggiungere una chiamata troppo`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="887a5-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="887a5-162">Creare una nuova classe **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="887a5-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="887a5-163">Di seguito è illustrata in dettaglio la creazione da zero di una classe **BroadcastReceiver** .</span><span class="sxs-lookup"><span data-stu-id="887a5-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="887a5-164">Tuttavia, per la creazione di un rapido toomanually alternativo **MyBroadcastReceiver.cs** è toorefer toohello **GcmService.cs** file è stato trovato nel progetto di xamarin esempio hello incluso hello [Esempi degli hub di notifica][GitHub].</span><span class="sxs-lookup"><span data-stu-id="887a5-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="887a5-165">Duplicazione **GcmService.cs** e modifica dei nomi di classe può essere anche un toostart ideale.</span><span class="sxs-lookup"><span data-stu-id="887a5-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="887a5-166">Aggiungere il seguente hello utilizzando istruzioni troppo**MyBroadcastReceiver.cs** (che fa riferimento il componente toohello e assembly aggiunto in precedenza):</span><span class="sxs-lookup"><span data-stu-id="887a5-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="887a5-167">In **MyBroadcastReceiver.cs**, aggiungere hello seguendo le richieste di autorizzazione tra hello **utilizzando** istruzioni e hello **dello spazio dei nomi** dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="887a5-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="887a5-168">In **MyBroadcastReceiver.cs**, modificare hello **MyBroadcastReceiver** classe seguente hello toomatch:</span><span class="sxs-lookup"><span data-stu-id="887a5-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="887a5-169">Aggiungere un'altra classe in **MyBroadcastReceiver.cs** denominata **PushHandlerService** che deriva da **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="887a5-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="887a5-170">Verificare che hello tooapply **servizio** toohello classe di attributo:</span><span class="sxs-lookup"><span data-stu-id="887a5-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="887a5-171">**GcmServiceBase** implementa i metodi **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="887a5-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="887a5-172">Il nostro **PushHandlerService** classe di implementazione deve eseguire l'override di questi metodi, e questi metodi verranno attivati in risposta toointeracting con hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="887a5-173">Eseguire l'override di hello **OnRegistered()** metodo **PushHandlerService** utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="887a5-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="887a5-174">In hello **OnRegistered()** codice di sopra, è opportuno notare hello possibilità toospecify tag tooregister per i canali di messaggistica specifici.</span><span class="sxs-lookup"><span data-stu-id="887a5-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="887a5-175">Eseguire l'override di hello **OnMessage** metodo **PushHandlerService** utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="887a5-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="887a5-176">Aggiungere il seguente hello **createNotification** e **dialogNotify** metodi troppo**PushHandlerService** per informare gli utenti quando viene ricevuta una notifica.</span><span class="sxs-lookup"><span data-stu-id="887a5-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="887a5-177">La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="887a5-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="887a5-178">Se si verifica in Android 5.0 o versioni successive, l'applicazione hello sarà necessario toobe installato notification hello tooreceive.</span><span class="sxs-lookup"><span data-stu-id="887a5-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="887a5-179">Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="887a5-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="887a5-180">Eseguire l'override dei membri astratti **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** per consentire la compilazione del codice:</span><span class="sxs-lookup"><span data-stu-id="887a5-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="887a5-181">Eseguire l'app nell'emulatore hello</span><span class="sxs-lookup"><span data-stu-id="887a5-181">Run your app in hello emulator</span></span>
<span data-ttu-id="887a5-182">Se si esegue questa app nell'emulatore hello, assicurarsi di utilizzare un dispositivo virtuale Android (AVD) che supporta APIs Google.</span><span class="sxs-lookup"><span data-stu-id="887a5-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="887a5-183">Nelle notifiche di push tooreceive ordine, è necessario impostare un account Google nel dispositivo virtuale Android.</span><span class="sxs-lookup"><span data-stu-id="887a5-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="887a5-184">(Nell'emulatore hello passare troppo**impostazioni** e fare clic su **Aggiungi Account**.) Assicurarsi inoltre che tale emulatore hello è connesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="887a5-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="887a5-185">La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="887a5-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="887a5-186">Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="887a5-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="887a5-187">In **Tools** (Strumenti) fare clic su **Open Android Emulator Manager** (Apri Gestione emulatori Android), selezionare il dispositivo e quindi fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="887a5-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="887a5-188">Selezionare **Google APIs** (API Google) in **Target** (Destinazione) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="887a5-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="887a5-189">Nella barra degli strumenti superiore hello, fare clic su **eseguire**e quindi selezionare l'app.</span><span class="sxs-lookup"><span data-stu-id="887a5-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="887a5-190">Questo Avvia emulatore hello e si esegue l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="887a5-191">app Hello recupera hello *registrationId* da GCM e i registri con hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="887a5-192">Inviare notifiche dal back-end</span><span class="sxs-lookup"><span data-stu-id="887a5-192">Send notifications from your backend</span></span>
<span data-ttu-id="887a5-193">È possibile testare una ricezione di notifiche dell'App per l'invio di notifiche in hello [portale di Azure classico] tramite hello debug scheda hub di notifica hello, come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="887a5-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="887a5-194">Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile.</span><span class="sxs-lookup"><span data-stu-id="887a5-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="887a5-195">È inoltre possibile utilizzare hello API REST direttamente i messaggi di notifica toosend se una raccolta non è disponibile per il back-end.</span><span class="sxs-lookup"><span data-stu-id="887a5-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="887a5-196">Di seguito è riportato un elenco di alcune altre esercitazioni è consigliabile tooreview per l'invio di notifiche:</span><span class="sxs-lookup"><span data-stu-id="887a5-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="887a5-197">ASP.NET: Vedere [toousers le notifiche di utilizzare gli hub di notifica toopush].</span><span class="sxs-lookup"><span data-stu-id="887a5-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="887a5-198">Java di hub di notifica Azure SDK: vedere [come hub di notifica da Java toouse](notification-hubs-java-push-notification-tutorial.md) per l'invio di notifiche da Java.</span><span class="sxs-lookup"><span data-stu-id="887a5-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="887a5-199">È stato testato in Eclipse per lo sviluppo per Android.</span><span class="sxs-lookup"><span data-stu-id="887a5-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="887a5-200">PHP: Vedere [come hub di notifica da PHP toouse](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="887a5-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="887a5-201">Nelle sottosezioni riportate avanti di hello di esercitazione hello, inviare notifiche tramite un'applicazione console .NET e tramite un servizio mobile tramite uno script di nodo.</span><span class="sxs-lookup"><span data-stu-id="887a5-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="887a5-202">(Facoltativo) Inviare notifiche tramite un'app .NET</span><span class="sxs-lookup"><span data-stu-id="887a5-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="887a5-203">In questa sezione si invieranno notifiche con un'app console .NET.</span><span class="sxs-lookup"><span data-stu-id="887a5-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="887a5-204">Creare una nuova applicazione console in Visual C#:</span><span class="sxs-lookup"><span data-stu-id="887a5-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="887a5-205">In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="887a5-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="887a5-206">Consente di visualizzare la Console di gestione pacchetti hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="887a5-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="887a5-207">Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="887a5-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="887a5-208">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="887a5-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="887a5-209">Aprire il file Program.cs hello e aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="887a5-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="887a5-210">Nel `Program` classe, aggiungere al metodo hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="887a5-211">Aggiornamento del testo segnaposto hello con il *DefaultFullSharedAccessSignature* nome hub e di stringa di connessione da hello [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="887a5-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="887a5-212">Aggiungere hello righe in seguito il **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="887a5-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="887a5-213">Premere hello F5 toorun chiave hello app.</span><span class="sxs-lookup"><span data-stu-id="887a5-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="887a5-214">Si riceverà una notifica nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="887a5-215">(Facoltativo) Inviare notifiche tramite un servizio mobile</span><span class="sxs-lookup"><span data-stu-id="887a5-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="887a5-216">Guardare [Introduzione a Servizi mobili].</span><span class="sxs-lookup"><span data-stu-id="887a5-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="887a5-217">Accedi toohello [portale di Azure classico]e selezionare il servizio mobile.</span><span class="sxs-lookup"><span data-stu-id="887a5-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="887a5-218">Seleziona hello **dell'utilità di pianificazione** scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="887a5-219">Creare un nuovo processo pianificato, immettere un nome, quindi scegliere **On demand**.</span><span class="sxs-lookup"><span data-stu-id="887a5-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="887a5-220">Quando viene creato il processo di hello, selezionare il nome di processo hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="887a5-221">Quindi fare clic su hello **Script** scheda nella barra superiore hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="887a5-222">Inserire lo script all'interno di una funzione dell'utilità di pianificazione seguente hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="887a5-223">Segnaposto hello tooreplace che con la notifica hub hello nome e la stringa di connessione per rendere *DefaultFullSharedAccessSignature* ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="887a5-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="887a5-224">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="887a5-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="887a5-225">Fare clic su **Esegui una volta** nella barra inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="887a5-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="887a5-226">Si dovrebbe ricevere una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="887a5-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="887a5-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="887a5-227">Next steps</span></span>
<span data-ttu-id="887a5-228">In questo semplice esempio, si trasmessa tooall notifiche con i dispositivi Android.</span><span class="sxs-lookup"><span data-stu-id="887a5-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="887a5-229">In ordine tootarget utenti specifici, vedere l'esercitazione toohello [toousers le notifiche di utilizzare gli hub di notifica toopush].</span><span class="sxs-lookup"><span data-stu-id="887a5-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="887a5-230">Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="887a5-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="887a5-231">Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica] e hello [gli hub di notifica come toofor Android].</span><span class="sxs-lookup"><span data-stu-id="887a5-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introduzione a Servizi mobili]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[portale di Azure classico]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[gli hub di notifica come toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers le notifiche di utilizzare gli hub di notifica toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente client di Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/
[Componente di messaggistica di Azure]: http://components.xamarin.com/view/azure-messaging
