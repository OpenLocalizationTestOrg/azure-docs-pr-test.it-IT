---
title: Introduzione a Hub di notifica per le app per Xamarin.Android | Documentazione Microsoft
description: Questa esercitazione contiene informazioni su come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione per Xamarin Android.
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
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="e2ed4-103">Introduzione ad Hub di notifica con Xamarin per Android</span><span class="sxs-lookup"><span data-stu-id="e2ed4-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="e2ed4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e2ed4-104">Overview</span></span>
<span data-ttu-id="e2ed4-105">In questa esercitazione viene illustrato come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione di Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="e2ed4-106">Verrà creata un'app per Xamarin.Android vuota che riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="e2ed4-107">Al termine, sarà possibile usare l’hub di notifica per trasmettere le notifiche push a tutti i dispositivi che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="e2ed4-108">Il codice compilato è disponibile nell'esempio di [app NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="e2ed4-109">Questa esercitazione illustra uno scenario di trasmissione semplice tramite hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e2ed4-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e2ed4-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="e2ed4-111">Il codice completo per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2ed4-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e2ed4-112">Prerequisites</span></span>
<span data-ttu-id="e2ed4-113">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="e2ed4-114">Visual Studio con Xamarin su Windows o Xamarin Studio su Mac OS X. Per istruzioni complete sull'installazione , vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="e2ed4-115">Un account Google attivo</span><span class="sxs-lookup"><span data-stu-id="e2ed4-115">Active Google account</span></span>
* <span data-ttu-id="e2ed4-116">[Componente di messaggistica di Azure]</span><span class="sxs-lookup"><span data-stu-id="e2ed4-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="e2ed4-117">[Componente client di Google Cloud Messaging]</span><span class="sxs-lookup"><span data-stu-id="e2ed4-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="e2ed4-118">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2ed4-119">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e2ed4-120">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e2ed4-121">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="e2ed4-122">Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e2ed4-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="e2ed4-123">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="e2ed4-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="e2ed4-124">Fare clic sulla scheda <b>Configure</b> (Configura) nella parte superiore, immettere il valore di <b>API Key</b> (Chiave API) ottenuto nella sezione precedente e quindi fare clic su <b>Save</b> (Salva).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="e2ed4-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="e2ed4-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="e2ed4-126">L'hub di notifica è ora configurato per l'uso con GCM e si dispone delle stringhe di connessione per registrare l'app in modo da ricevere e inviare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="e2ed4-127">Connettere l'app all'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="e2ed4-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="e2ed4-128">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="e2ed4-128">Create a new project</span></span>
1. <span data-ttu-id="e2ed4-129">In Xamarin Studio fare clic su **New Solution** (Nuova soluzione), **Android App** (App Android) e selezionare **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="e2ed4-130">Compilare i campi **App Name** (Nome app) e **Identifier** (Identificatore).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="e2ed4-131">In **Target Plaforms** (Piattaforme di destinazione) selezionare la piattaforma che si vuole supportare e quindi fare clic su **Next** (Avanti) e su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="e2ed4-132">In questo modo viene creato un nuovo progetto Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="e2ed4-133">Aprire le proprietà del progetto facendo clic con il pulsante destro del mouse sul nuovo progetto nella visualizzazione Solution e scegliendo **Options**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="e2ed4-134">Selezionare la voce **Android Application** (Applicazione Android) nella sezione **Build** (Crea).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="e2ed4-135">Verificare che la prima lettera di **Package name** sia minuscola.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e2ed4-136">La prima lettera del nome del pacchetto deve essere minuscola.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="e2ed4-137">In caso contrario, verranno visualizzati errori del manifesto dell'applicazione al momento della registrazione di **BroadcastReceiver** e **IntentFilter** per le notifiche push più avanti.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="e2ed4-138">Impostare facoltativamente **Minimum Android version** su un altro livello API.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="e2ed4-139">Facoltativamente, impostare **Target Android version** sulla versione dell'API di destinazione (deve essere almeno API livello 8 o superiore).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="e2ed4-140">Fare clic su **OK** e chiudere la finestra di dialogo Project Options.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="e2ed4-141">Aggiungere i componenti necessari al progetto</span><span class="sxs-lookup"><span data-stu-id="e2ed4-141">Add the required components to your project</span></span>
<span data-ttu-id="e2ed4-142">Il client Google Cloud Messaging disponibile in Xamarin Component Store semplifica il processo di supporto delle notifiche push in Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="e2ed4-143">Fare clic con il pulsante destro del mouse sulla cartella Components nell'app Xamarin.Android e scegliere **Get More Components**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="e2ed4-144">Cercare il componente **Messaggistica di Azure** e aggiungerlo al progetto.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="e2ed4-145">Cercare il componente **Client Google Cloud Messaging** e aggiungerlo al progetto.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="e2ed4-146">Configurare Hub di notifica nel progetto</span><span class="sxs-lookup"><span data-stu-id="e2ed4-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="e2ed4-147">Raccogliere le informazioni seguenti per l'app Android e l'hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="e2ed4-148">**GoogleProjectNumber**: ottenere il valore Project Number (Numero progetto) dalla panoramica dell'app nel portale di sviluppo di Google.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="e2ed4-149">Prendere nota di questo valore in precedenza, durante la creazione dell'app nel portale.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="e2ed4-150">**Stringa di connessione Listen**: nel dashboard del [portale di Azure classico] fare clic su **Visualizza stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="e2ed4-151">Copiare la stringa di connessione *DefaultListenSharedAccessSignature* per questo valore.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="e2ed4-152">**Hub name**: si tratta del nome dell'hub del [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="e2ed4-153">Ad esempio, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="e2ed4-154">Creare una classe **Constants.cs** per il progetto Xamarin e definire i valori costanti seguenti nella classe.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="e2ed4-155">Sostituire i segnaposto con i valori.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="e2ed4-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="e2ed4-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="e2ed4-157">}</span><span class="sxs-lookup"><span data-stu-id="e2ed4-157">}</span></span>
2. <span data-ttu-id="e2ed4-158">Aggiungere le istruzioni using seguenti a **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="e2ed4-159">Aggiungere una variabile di istanza alla classe `MainActivity` che verrà usata per visualizzare una finestra di dialogo di avviso quando l'app è in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="e2ed4-160">Creare il metodo seguente nella classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="e2ed4-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="e2ed4-161">Nel metodo `OnCreate` di **MainActivity.cs** inizializzare la variabile `instance` e aggiungere una chiamata a `RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="e2ed4-162">Creare una nuova classe **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e2ed4-163">Di seguito è illustrata in dettaglio la creazione da zero di una classe **BroadcastReceiver** .</span><span class="sxs-lookup"><span data-stu-id="e2ed4-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="e2ed4-164">Esiste tuttavia un'alternativa più rapida alla creazione manuale di **MyBroadcastReceiver.cs**, che consiste nel fare riferimento al file **GcmService.cs** disponibile nel progetto Xamarin.Android di esempio incluso con gli [esempi di NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="e2ed4-165">Anche duplicare il file **GcmService.cs** e modificare i nomi delle classi può essere un ottimo punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="e2ed4-166">Aggiungere le istruzioni using seguenti a **MyBroadcastReceiver.cs** , facendo riferimento al componente e all'assembly aggiunti in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="e2ed4-167">In **MyBroadcastReceiver.cs** aggiungere le richieste di autorizzazione seguenti tra le istruzioni **using** e la dichiarazione **namespace**:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="e2ed4-168">In **MyBroadcastReceiver.cs** modificare la classe **MyBroadcastReceiver** in modo che corrisponda all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
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
10. <span data-ttu-id="e2ed4-169">Aggiungere un'altra classe in **MyBroadcastReceiver.cs** denominata **PushHandlerService** che deriva da **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="e2ed4-170">Assicurarsi di applicare l'attributo **Service** alla classe:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="e2ed4-171">**GcmServiceBase** implementa i metodi **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="e2ed4-172">La classe di implementazione **PushHandlerService** deve eseguire l'override di questi metodi, che si attiveranno in risposta all'interazione con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="e2ed4-173">Eseguire l'override del metodo **OnRegistered()** in **PushHandlerService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
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
    > <span data-ttu-id="e2ed4-174">Nel codice **OnRegistered()** precedente notare la capacità di specificare tag per la registrazione a canali di messaggistica specifici.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="e2ed4-175">Eseguire l'override del metodo **OnMessage** in **PushHandlerService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
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
14. <span data-ttu-id="e2ed4-176">Aggiungere i metodi **createNotification** e **dialogNotify** seguenti a **PushHandlerService** per informare gli utenti quando viene ricevuta una notifica.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e2ed4-177">La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="e2ed4-178">Se si testa in Android 5.0 o versioni successive, l'app deve essere in esecuzione per poter ricevere la notifica.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="e2ed4-179">Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
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
15. <span data-ttu-id="e2ed4-180">Eseguire l'override dei membri astratti **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** per consentire la compilazione del codice:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
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

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="e2ed4-181">Eseguire l'app nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="e2ed4-181">Run your app in the emulator</span></span>
<span data-ttu-id="e2ed4-182">Se si esegue l'app nell'emulatore, assicurarsi di usare un emulatore Android Virtual Device (AVD) con il supporto per Google APIs.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2ed4-183">Per ricevere notifiche push, è necessario impostare un account Google in Android Virtual Device.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="e2ed4-184">Nell'emulatore passare a **Settings** (Impostazioni) e fare clic su **Add Account** (Aggiungi account). Assicurarsi inoltre che l'emulatore sia connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="e2ed4-185">La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="e2ed4-186">Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="e2ed4-187">In **Tools** (Strumenti) fare clic su **Open Android Emulator Manager** (Apri Gestione emulatori Android), selezionare il dispositivo e quindi fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="e2ed4-188">Selezionare **Google APIs** (API Google) in **Target** (Destinazione) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="e2ed4-189">Fare clic su **Run**sulla barra degli strumenti nella parte superiore della schermata e selezionare l'app.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="e2ed4-190">In questo modo l'emulatore viene avviato e l'app eseguita.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="e2ed4-191">L'app recupera la proprietà *registrationId* da GCM ed esegue la registrazione con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="e2ed4-192">Inviare notifiche dal back-end</span><span class="sxs-lookup"><span data-stu-id="e2ed4-192">Send notifications from your backend</span></span>
<span data-ttu-id="e2ed4-193">È possibile testare la ricezione delle notifiche nell'app inviando notifiche nel [portale di Azure classico] tramite la scheda Debug nell'hub di notifica, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="e2ed4-194">Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="e2ed4-195">È anche possibile utilizzare l'API REST direttamente per inviare messaggi di notifica se una libreria non è disponibile per il back-end.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="e2ed4-196">Di seguito è riportato un elenco di altre esercitazioni, che è possibile esaminare per l'invio di notifiche:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="e2ed4-197">ASP.NET: vedere [Usare Hub di notifica per inviare notifiche push agli utenti].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="e2ed4-198">Azure Notification Hubs Java SDK: vedere [Come usare Hub di notifica da Java](notification-hubs-java-push-notification-tutorial.md) per l'invio di notifiche da Java.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="e2ed4-199">È stato testato in Eclipse per lo sviluppo per Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="e2ed4-200">PHP: vedere [Come usare Hub di notifica da PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="e2ed4-201">Nelle sezioni secondarie successive di questa esercitazione vengono inviate notifiche con un'app console .NET e con un servizio mobile tramite uno script node.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="e2ed4-202">(Facoltativo) Inviare notifiche tramite un'app .NET</span><span class="sxs-lookup"><span data-stu-id="e2ed4-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="e2ed4-203">In questa sezione si invieranno notifiche con un'app console .NET.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="e2ed4-204">Creare una nuova applicazione console in Visual C#:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="e2ed4-205">In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="e2ed4-206">In questo modo viene visualizzata la console di Gestione pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="e2ed4-207">Nella finestra Console di Gestione pacchetti impostare **Progetto predefinito** sul nuovo progetto di applicazione console, quindi eseguire il comando seguente nella finestra della console:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="e2ed4-208">Verrà aggiunto un riferimento all’SDK dell’Hub di notifica di Azure mediante il <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet Microsoft.Azure.NotificationHubs</a>.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="e2ed4-209">Aprire il file Program.cs e aggiungere l'istruzione `using` seguente:</span><span class="sxs-lookup"><span data-stu-id="e2ed4-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="e2ed4-210">Nella classe `Program` aggiungere il metodo seguente.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="e2ed4-211">Aggiornare il testo segnaposto con la stringa di connessione *DefaultFullSharedAccessSignature* e il nome dell'hub dal [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="e2ed4-212">Aggiungere le righe seguenti nel metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="e2ed4-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="e2ed4-213">Premere F5 per eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="e2ed4-214">Si dovrebbe ricevere una notifica nell’app.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="e2ed4-215">(Facoltativo) Inviare notifiche tramite un servizio mobile</span><span class="sxs-lookup"><span data-stu-id="e2ed4-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="e2ed4-216">Guardare [Introduzione a Servizi mobili].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="e2ed4-217">Accedere al [portale di Azure classico]e selezionare il servizio mobile.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="e2ed4-218">Selezionare la scheda **Utilità di pianificazione** in alto.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="e2ed4-219">Creare un nuovo processo pianificato, immettere un nome, quindi scegliere **On demand**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="e2ed4-220">Una volta creato il processo, fare clic sul relativo nome.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-220">When the job is created, click the job name.</span></span> <span data-ttu-id="e2ed4-221">Fare quindi clic sulla scheda **Script** nella barra superiore.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="e2ed4-222">Inserire lo script seguente all'interno della funzione dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="e2ed4-223">Assicurarsi di sostituire i segnaposto con il nome dell'hub di notifica e la stringa di connessione associata a *DefaultFullSharedAccessSignature* ottenuti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="e2ed4-224">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="e2ed4-225">Fare clic su **Run Once** sulla barra inferiore.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="e2ed4-226">Si dovrebbe ricevere una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2ed4-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2ed4-227">Next steps</span></span>
<span data-ttu-id="e2ed4-228">In questo semplice esempio le notifiche sono state trasmesse a tutti i dispositivi Android.</span><span class="sxs-lookup"><span data-stu-id="e2ed4-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="e2ed4-229">Per rivolgersi a utenti specifici, fare riferimento all'esercitazione [Usare Hub di notifica per inviare notifiche push agli utenti].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="e2ed4-230">Se si desidera segmentare gli utenti per gruppi di interesse, consultare [Uso di Hub di notifica per inviare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="e2ed4-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="e2ed4-231">Per altre informazioni sull'uso di Hub di notifica, vedere [Panoramica dell'Hub di notifica] e [Notification Hubs How-To for Android.] (Procedura di Hub di notifica per Android).</span><span class="sxs-lookup"><span data-stu-id="e2ed4-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
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
<span data-ttu-id="e2ed4-232">[Introduzione a Servizi mobili]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="e2ed4-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="e2ed4-233">[portale di Azure classico]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="e2ed4-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="e2ed4-234">[Panoramica dell'Hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="e2ed4-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="e2ed4-235">[Notification Hubs How-To for Android.]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="e2ed4-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="e2ed4-236">[Usare Hub di notifica per inviare notifiche push agli utenti]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="e2ed4-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="e2ed4-237">[Uso di Hub di notifica per inviare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="e2ed4-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="e2ed4-238">[Componente client di Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="e2ed4-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="e2ed4-239">[Componente di messaggistica di Azure]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="e2ed4-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>
