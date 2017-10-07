---
title: aaaiOS le notifiche Push con hub di notifica per App Xamarin | Documenti Microsoft
description: In questa esercitazione viene illustrato applicazione iOS Xamarin tooa di notifiche push toouse toosend di hub di notifica di Azure.
services: notification-hubs
keywords: notifiche push di ios,messaggi push,notifiche push,messaggio push
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="633e5-104">Notifiche push di iOS con Hub di notifica per app Xamarin</span><span class="sxs-lookup"><span data-stu-id="633e5-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="633e5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="633e5-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="633e5-106">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="633e5-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="633e5-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="633e5-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="633e5-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="633e5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="633e5-109">Questa esercitazione illustra applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="633e5-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="633e5-110">Creerai un'app xamarin vuota che riceve le notifiche push tramite hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="633e5-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="633e5-111">Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="633e5-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="633e5-112">Hello codice completato è disponibile in hello [app hub di notifica] [ GitHub] esempio.</span><span class="sxs-lookup"><span data-stu-id="633e5-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="633e5-113">Questa esercitazione illustra hello scenario broadcast messaggio push semplice con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="633e5-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="633e5-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="633e5-114">Prerequisites</span></span>
<span data-ttu-id="633e5-115">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="633e5-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="633e5-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="633e5-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="633e5-117">Dispositivo compatibile con iOS 7.0 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="633e5-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="633e5-118">Iscrizione a iOS Developer Program</span><span class="sxs-lookup"><span data-stu-id="633e5-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="633e5-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="633e5-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="633e5-120">A causa dei requisiti di configurazione per le notifiche push iOS, è necessario distribuire e testare l'applicazione di esempio hello in un dispositivo fisico iOS (iPhone o iPad) anziché nel simulatore hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="633e5-121">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="633e5-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="633e5-122">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="633e5-122">Configure your notification hub</span></span>
<span data-ttu-id="633e5-123">In questa sezione viene illustrata la creazione di un nuovo hub di notifica e la configurazione dell'autenticazione con il servizio APN utilizzando hello **. p12** certificato push creato.</span><span class="sxs-lookup"><span data-stu-id="633e5-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="633e5-124">Se si desidera toouse un hub di notifica che è già stato creato, è possibile ignorare toostep 5.</span><span class="sxs-lookup"><span data-stu-id="633e5-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="633e5-125">Dal momento che una connessione del servizio APN hello tooconfigure, nel portale di Azure, hello aprire le impostazioni di Hub di notifica, fare clic su ande su <b>Notification Services</b>, quindi fare clic su hello <b>Apple (APNS)</b> elemento nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="633e5-126">Al termine, fare clic su <b>carica certificato</b> e seleziona hello <b>. p12</b> certificato esportato in precedenza, nonché password hello hello certificato.</span><span class="sxs-lookup"><span data-stu-id="633e5-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="633e5-127">Verificare che tooselect <b>Sandbox</b> modalità poiché si inviano push di messaggi in un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="633e5-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="633e5-128">Utilizzare solo hello <b>produzione</b> se si desidera che toousers di notifiche push toosend che hanno già acquistato l'app dall'archivio hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="633e5-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="633e5-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="633e5-130">Hub di notifica è ora configurato toowork con il servizio APN e aver tooregister stringhe di connessione hello app e inviare notifiche push.</span><span class="sxs-lookup"><span data-stu-id="633e5-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="633e5-131">Connettere l'hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="633e5-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="633e5-132">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="633e5-132">Create a new project</span></span>
1. <span data-ttu-id="633e5-133">In Xamarin Studio, creare un nuovo progetto di iOS e selezionare hello **Unified API** > **singola visualizzazione applicazione** modello.</span><span class="sxs-lookup"><span data-stu-id="633e5-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio: selezionare il tipo di applicazione][31]
2. <span data-ttu-id="633e5-135">Aggiungere un componente di messaggistica di Azure toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="633e5-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="633e5-136">In visualizzazione soluzione hello, fare clic sul hello **componenti** cartella per il progetto e scegliere **ottenere più componenti**.</span><span class="sxs-lookup"><span data-stu-id="633e5-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="633e5-137">Ricerca di hello **messaggistica di Azure** componente e aggiungere hello componente tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="633e5-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="633e5-138">In **appdelegate. cs**, aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="633e5-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="633e5-139">Dichiarare un'istanza di **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="633e5-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="633e5-140">Creare un **Constants.cs** classe con hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="633e5-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="633e5-141">In **appdelegate. cs**, aggiornare **FinishedLaunching()** seguente hello toomatch:</span><span class="sxs-lookup"><span data-stu-id="633e5-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="633e5-142">Eseguire l'override di hello **RegisteredForRemoteNotifications()** metodo **appdelegate. cs**:</span><span class="sxs-lookup"><span data-stu-id="633e5-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="633e5-143">Eseguire l'override di hello **ReceivedRemoteNotification()** metodo **appdelegate. cs**:</span><span class="sxs-lookup"><span data-stu-id="633e5-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="633e5-144">Creare i seguenti hello **ProcessNotification()** metodo **appdelegate. cs**:</span><span class="sxs-lookup"><span data-stu-id="633e5-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="633e5-145">È possibile scegliere toooverride **FailedToRegisterForRemoteNotifications()** toohandle situazioni, ad esempio alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="633e5-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="633e5-146">Ciò è particolarmente importante in utente hello potrebbe avviare l'applicazione in modalità offline (ad esempio aereo) e si desidera push toohandle app tooyour specifici scenari di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="633e5-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="633e5-147">Eseguire l'applicazione hello sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="633e5-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="633e5-148">Invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="633e5-148">Sending Push Notifications</span></span>
<span data-ttu-id="633e5-149">È possibile eseguire test di ricevere le notifiche push nell'app per l'invio di notifiche in hello [portale Azure] tramite hello **invio di Test** funzionalità hello **risoluzione dei problemi** set di strumenti, a destra nella hello hub pagina di notifica, come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="633e5-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="633e5-150">Le notifiche push vengono in genere inviate attraverso un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile.</span><span class="sxs-lookup"><span data-stu-id="633e5-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="633e5-151">Inoltre, è possibile utilizzare hello API REST direttamente push toosend messaggi in caso di una libreria non è disponibile nel proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="633e5-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="633e5-152">In questa esercitazione verrà semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="633e5-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="633e5-153">Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="633e5-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="633e5-154">Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:</span><span class="sxs-lookup"><span data-stu-id="633e5-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="633e5-155">**Interfaccia REST**: È possibile supportare la notifica push su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="633e5-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="633e5-156">**Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="633e5-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="633e5-157">**Node.js** : [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="633e5-158">**App per dispositivi mobili**: per un esempio di come toosend notifiche da un back-end dell'App Mobile di servizio App di Azure che è integrato con hub di notifica, vedere [app mobile tooyour le notifiche push Aggiungi](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="633e5-159">**Java o PHP**: per un esempio di come le notifiche push toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="633e5-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="633e5-160">(Facoltativo) Inviare notifiche push da un'app console .NET.</span><span class="sxs-lookup"><span data-stu-id="633e5-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="633e5-161">In questa sezione si invieranno notifiche push con una semplice app console .NET.</span><span class="sxs-lookup"><span data-stu-id="633e5-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="633e5-162">Ai fini di hello di questo esempio, si passerà tooa ambiente di sviluppo di Windows che è già installato Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="633e5-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="633e5-163">In Visual Studio creare una nuova applicazione console in Visual C#:</span><span class="sxs-lookup"><span data-stu-id="633e5-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="633e5-164">In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="633e5-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="633e5-165">console di gestione pacchetti Hello dovrebbe essere visualizzato toohello ancorato inferiore dell'area di lavoro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="633e5-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="633e5-166">Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="633e5-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="633e5-167">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="633e5-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="633e5-168">Aprire hello `Program.cs` file e aggiungere il seguente hello `using` istruzione, garantendo che è possibile utilizzare le classi di Azure e le funzioni all'interno della classe principale:</span><span class="sxs-lookup"><span data-stu-id="633e5-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="633e5-169">Nel `Program` classe, aggiungere al metodo hello (non dimenticare hello tooreplace **stringa di connessione** e **nome hub**):</span><span class="sxs-lookup"><span data-stu-id="633e5-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="633e5-170">Aggiungere hello righe in seguito il `Main` metodo:</span><span class="sxs-lookup"><span data-stu-id="633e5-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="633e5-171">Premere hello F5 toorun chiave hello app.</span><span class="sxs-lookup"><span data-stu-id="633e5-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="633e5-172">Entro pochi secondi dovrebbe essere visualizzata una notifica push nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="633e5-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="633e5-173">Se si utilizza Wi-Fi o una rete cellulare dati, assicurarsi di disporre di una connessione internet sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="633e5-174">È possibile trovare tutti i payload possibili hello in hello Apple [locali e Guida per programmatori notifica Push].</span><span class="sxs-lookup"><span data-stu-id="633e5-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="633e5-175">(Facoltativo) Inviare notifiche da un servizio mobile</span><span class="sxs-lookup"><span data-stu-id="633e5-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="633e5-176">In questa sezione si invieranno notifiche push usando un servizio mobile con uno script node.</span><span class="sxs-lookup"><span data-stu-id="633e5-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="633e5-177">seguire una notifica tramite un servizio mobile, toosend [Introduzione a servizi mobili]e quindi:</span><span class="sxs-lookup"><span data-stu-id="633e5-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="633e5-178">Accedi toohello [portale di Azure classico]e selezionare il servizio mobile.</span><span class="sxs-lookup"><span data-stu-id="633e5-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="633e5-179">Seleziona hello **dell'utilità di pianificazione** scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="633e5-180">Creare un nuovo processo pianificato, immettere un nome, quindi scegliere **On demand**.</span><span class="sxs-lookup"><span data-stu-id="633e5-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="633e5-181">Quando viene creato il processo di hello, selezionare il nome di processo hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="633e5-182">Quindi fare clic su hello **Script** scheda nella barra superiore hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="633e5-183">Inserire lo script all'interno di una funzione dell'utilità di pianificazione seguente hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="633e5-184">Segnaposto hello tooreplace che con la notifica hub hello nome e la stringa di connessione per rendere *DefaultFullSharedAccessSignature* ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="633e5-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="633e5-185">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="633e5-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="633e5-186">Fare clic su **Esegui una volta** nella barra inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="633e5-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="633e5-187">Si dovrebbe ricevere un avviso sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="633e5-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="633e5-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="633e5-188">Next steps</span></span>
<span data-ttu-id="633e5-189">In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="633e5-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="633e5-190">In ordine tootarget utenti specifici, vedere l'esercitazione toohello [toousers le notifiche di utilizzare gli hub di notifica toopush].</span><span class="sxs-lookup"><span data-stu-id="633e5-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="633e5-191">Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="633e5-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="633e5-192">Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica] e hello [toofor con gli hub di notifica come iOS].</span><span class="sxs-lookup"><span data-stu-id="633e5-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Introduzione a servizi mobili]: /develop/mobile/tutorials/get-started-xamarin-ios
[portale di Azure classico]: https://manage.windowsazure.com/
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[toofor con gli hub di notifica come iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers le notifiche di utilizzare gli hub di notifica toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet

[locali e Guida per programmatori notifica Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[portale Azure]: https://portal.azure.com
