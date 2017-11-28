---
title: tooiOS di notifiche push aaaSending con gli hub di notifica di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure.
services: notification-hubs
documentationcenter: ios
keywords: notifica push,notifiche push,notifiche push ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="975a5-104">TooiOS l'invio di notifiche push con hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="975a5-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="975a5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="975a5-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="975a5-106">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="975a5-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="975a5-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="975a5-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="975a5-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="975a5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="975a5-109">Questa esercitazione illustra applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="975a5-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="975a5-110">Creerai un'app iOS vuota che riceve le notifiche push tramite hello [servizio Apple Push Notification (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="975a5-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="975a5-111">Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="975a5-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="975a5-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="975a5-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="975a5-113">codice Hello completata per questa esercitazione è disponibile [su GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="975a5-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="975a5-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="975a5-114">Prerequisites</span></span>
<span data-ttu-id="975a5-115">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="975a5-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="975a5-116">[iOS Mobile Services SDK versione 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="975a5-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="975a5-117">Ultima versione di [Xcode]</span><span class="sxs-lookup"><span data-stu-id="975a5-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="975a5-118">Un dispositivo con iOS 8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="975a5-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="975a5-119">[Apple Developer Program](https://developer.apple.com/programs/) .</span><span class="sxs-lookup"><span data-stu-id="975a5-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="975a5-120">A causa dei requisiti di configurazione per le notifiche push, è necessario distribuire e testare le notifiche push in un dispositivo fisico iOS (iPhone o iPad) anziché simulatore iOS hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="975a5-121">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per iOS.</span><span class="sxs-lookup"><span data-stu-id="975a5-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="975a5-122">Configurare l'hub di notifica per l'invio di notifiche push di iOS</span><span class="sxs-lookup"><span data-stu-id="975a5-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="975a5-123">In questa sezione viene illustrata la creazione di un nuovo hub di notifica e la configurazione dell'autenticazione con il servizio APN utilizzando hello **. p12** certificato push creato.</span><span class="sxs-lookup"><span data-stu-id="975a5-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="975a5-124">Se si desidera toouse un hub di notifica che è già stato creato, è possibile ignorare toostep 5.</span><span class="sxs-lookup"><span data-stu-id="975a5-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="975a5-125">Fare clic su hello <b>Notification Services</b> pulsante hello <b>impostazioni</b> pannello, quindi selezionare <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="975a5-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="975a5-126">Fare clic su <b>carica certificato</b> e seleziona hello <b>. p12</b> file esportato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="975a5-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="975a5-127">Assicurarsi di specificare anche la password corretta hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="975a5-128">Verificare che tooselect <b>Sandbox</b> modalità poiché si tratta per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="975a5-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="975a5-129">Utilizzare solo hello <b>produzione</b> se si desidera toousers di notifiche push toosend che hanno acquistato l'app dall'archivio hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="975a5-130">&emsp;&emsp;&emsp;&emsp;![Configurare APNS nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="975a5-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurare il certificato APN nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="975a5-132">Hub di notifica è ora configurato toowork con il servizio APN e aver tooregister stringhe di connessione hello app e inviare notifiche push.</span><span class="sxs-lookup"><span data-stu-id="975a5-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="975a5-133">Connettere il tooNotification app iOS hub</span><span class="sxs-lookup"><span data-stu-id="975a5-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="975a5-134">In Xcode, creare un nuovo progetto di iOS e selezionare hello **singola visualizzazione applicazione** modello.</span><span class="sxs-lookup"><span data-stu-id="975a5-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - Single View Application][8]
    
2. <span data-ttu-id="975a5-136">Quando si impostano opzioni hello per il nuovo progetto, verificare che toouse hello stesso **Product Name** e **identificatore organizzazione** utilizzato quando si imposta in precedenza ID bundle hello in hello Apple Developer portale.</span><span class="sxs-lookup"><span data-stu-id="975a5-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - Opzioni di progetto][11]
    
3. <span data-ttu-id="975a5-138">In **destinazioni**, fare clic sul nome del progetto, fare clic su hello **Build Settings** scheda ed espandere **identità di firma codice**, quindi in **Debug**, impostare l'identità di firma codice.</span><span class="sxs-lookup"><span data-stu-id="975a5-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="975a5-139">Attiva/disattiva **livelli** da **base** troppo**tutti**e impostare **profilo di Provisioning** toohello profilo creato in precedenza di provisioning .</span><span class="sxs-lookup"><span data-stu-id="975a5-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="975a5-140">Se non viene visualizzato hello provisioning nuovo profilo creato in Xcode, provare ad aggiornare i profili di hello per le identità di firma.</span><span class="sxs-lookup"><span data-stu-id="975a5-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="975a5-141">Fare clic su **Xcode** sulla barra dei menu hello, fare clic su **preferenze**, fare clic su hello **Account** scheda, fare clic su hello **Visualizza dettagli** fare clic sui identità di firma e quindi scegliere il pulsante di aggiornamento hello nell'angolo inferiore destro hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - Profilo di provisioning][9]
4. <span data-ttu-id="975a5-143">Scaricare hello [iOS Mobile Services SDK versione 1.2.4] e decomprimere file hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="975a5-144">In Xcode, mouse sul progetto e fare clic su hello **aggiungere file alla** hello tooadd opzione **WindowsAzureMessaging.framework** progetto Xcode tooyour di cartella.</span><span class="sxs-lookup"><span data-stu-id="975a5-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="975a5-145">Selezionare **Copy items if needed** (Copia elementi se necessario) e fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="975a5-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="975a5-146">hub di notifica Hello SDK non supporta attualmente bitcode in Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="975a5-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="975a5-147">È necessario impostare **abilitare Bitcode** troppo**n** in hello **le opzioni di compilazione** per il progetto.</span><span class="sxs-lookup"><span data-stu-id="975a5-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Decomprimere Azure SDK][10]
5. <span data-ttu-id="975a5-149">Aggiungere un nuovo progetto tooyour file di intestazione denominato `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="975a5-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="975a5-150">Questo file contiene costanti hello per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="975a5-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="975a5-151">Aggiungere hello seguenti definizioni e sostituire i segnaposto di valore letterale stringa hello con il *nome hub* hello e *DefaultListenSharedAccessSignature* annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="975a5-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="975a5-152">Aprire il `AppDelegate.h` file aggiungere hello seguenti direttive di importazione:</span><span class="sxs-lookup"><span data-stu-id="975a5-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="975a5-153">Nel `AppDelegate.m file`, aggiungere hello seguente di codice hello `didFinishLaunchingWithOptions` metodo in base alla versione di iOS.</span><span class="sxs-lookup"><span data-stu-id="975a5-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="975a5-154">Questo codice registra l'handle di dispositivo nel servizio APNS:</span><span class="sxs-lookup"><span data-stu-id="975a5-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="975a5-155">Per iOS 8:</span><span class="sxs-lookup"><span data-stu-id="975a5-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="975a5-156">Per too8 precedenti versioni di iOS:</span><span class="sxs-lookup"><span data-stu-id="975a5-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="975a5-157">In hello stesso file, aggiungere hello dei seguenti metodi.</span><span class="sxs-lookup"><span data-stu-id="975a5-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="975a5-158">Questo codice si connette l'hub di notifica toohello utilizzando hello informazioni di connessione specificato nel HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="975a5-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="975a5-159">Fornisce quindi hub di notifica toohello token dispositivo hello in modo che hello hub di notifica è possibile inviare notifiche:</span><span class="sxs-lookup"><span data-stu-id="975a5-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="975a5-160">In hello stesso file, aggiungere hello seguente metodo toodisplay un **UIAlert** se viene ricevuta notifica di hello mentre è attiva app hello:</span><span class="sxs-lookup"><span data-stu-id="975a5-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="975a5-161">Compilare ed eseguire l'applicazione hello in tooverify il dispositivo che non si verificano errori.</span><span class="sxs-lookup"><span data-stu-id="975a5-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="975a5-162">Inviare notifiche push di prova</span><span class="sxs-lookup"><span data-stu-id="975a5-162">Send test push notifications</span></span>
<span data-ttu-id="975a5-163">È possibile verificare la ricezione di notifiche nell'app mediante l'invio di notifiche push in hello [portale Azure] tramite hello **Troubleshooting** sezione nel Pannello di hub hello (utilizzare hello *inviodiTest* opzione).</span><span class="sxs-lookup"><span data-stu-id="975a5-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portale di Azure - Invio di prova][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="975a5-165">(Facoltativo) Inviare notifiche push da app hello</span><span class="sxs-lookup"><span data-stu-id="975a5-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="975a5-166">Questo esempio l'invio di notifiche da app client hello viene fornito solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="975a5-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="975a5-167">Poiché questo richiederà hello `DefaultFullSharedAccessSignature` toobe presente sull'app client hello, che espone il rischio di toohello hub di notifica che un utente può ottenere le notifiche di accesso non autorizzato toosend tooyour client.</span><span class="sxs-lookup"><span data-stu-id="975a5-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="975a5-168">Se si desidera toosend le notifiche push all'interno di un'app, in questa sezione viene fornito un esempio di come toodo questo utilizzando hello interfaccia REST.</span><span class="sxs-lookup"><span data-stu-id="975a5-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="975a5-169">In Xcode aprire `Main.storyboard` e aggiungere i seguenti componenti dell'interfaccia utente dagli hello oggetto libreria tooallow hello utente toosend notifiche push in app hello hello:</span><span class="sxs-lookup"><span data-stu-id="975a5-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="975a5-170">Etichetta senza testo.</span><span class="sxs-lookup"><span data-stu-id="975a5-170">A label with no label text.</span></span> <span data-ttu-id="975a5-171">Sarà errori tooreport utilizzato per l'invio di notifiche.</span><span class="sxs-lookup"><span data-stu-id="975a5-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="975a5-172">Hello **righe** proprietà deve essere impostata troppo**0** in modo che verrà ridimensionato automaticamente toohello vincolata destra e i margini sinistro e parte superiore di hello della visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="975a5-173">Un campo di testo con **segnaposto** testo impostato troppo**messaggio di notifica immettere**.</span><span class="sxs-lookup"><span data-stu-id="975a5-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="975a5-174">Vincolare campo hello immediatamente sotto l'etichetta di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="975a5-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="975a5-175">Visualizzazione Controller hello come delegato presa hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="975a5-176">Un pulsante denominato **invia una notifica** vincolata sotto il campo di testo hello e in centro orizzontale hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="975a5-177">visualizzazione di Hello dovrebbe apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="975a5-177">hello view should look as follows:</span></span>
     
     ![Finestra di progettazione Xcode][32]
2. <span data-ttu-id="975a5-179">[Aggiungere le prese](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) per il campo di testo ed etichetta hello connessi, la visualizzazione e aggiornare il `interface` definizione toosupport `UITextFieldDelegate` e `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="975a5-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="975a5-180">Aggiungere hello tre dichiarazioni di proprietà indicate di seguito toohelp supporto chiamando hello API REST e l'analisi di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="975a5-181">Il file ViewController.h dovrebbe apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="975a5-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="975a5-182">Aprire `HubInfo.h` e aggiungere i seguenti costanti che verranno utilizzate per l'invio di hub di notifiche tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="975a5-183">Sostituire l'effettivo valore letterale stringa segnaposto hello *DefaultFullSharedAccessSignature* stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="975a5-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="975a5-184">Aggiungere il seguente hello `#import` tooyour istruzioni `ViewController.h` file.</span><span class="sxs-lookup"><span data-stu-id="975a5-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="975a5-185">In `ViewController.m` aggiungere hello implementazione dell'interfaccia toohello di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="975a5-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="975a5-186">Questo codice analizzerà la stringa di connessione *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="975a5-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="975a5-187">Come accennato in hello [riferimento all'API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), queste informazioni analizzate saranno toogenerate usato un token di firma di accesso condiviso per hello **autorizzazione** intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="975a5-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="975a5-188">In `ViewController.m`, hello aggiornamento `viewDidLoad` metodo tooparse hello stringa di connessione quando viene caricato vista hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="975a5-189">Aggiungere anche i metodi di utilità hello, illustrati di seguito, l'implementazione dell'interfaccia toohello.</span><span class="sxs-lookup"><span data-stu-id="975a5-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="975a5-190">In `ViewController.m`, aggiungere hello seguente codice toohello interfaccia implementazione toogenerate hello SaS token di autenticazione che verrà fornito in hello **autorizzazione** intestazione, come indicato in hello [API REST Riferimento](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="975a5-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="975a5-191">CTRL + trascinare da hello **invia una notifica di** pulsante troppo`ViewController.m` tooadd un'azione denominata **SendNotificationMessage** per hello **tocco premuto** evento.</span><span class="sxs-lookup"><span data-stu-id="975a5-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="975a5-192">Metodo di aggiornamento con hello dopo la notifica di hello codice toosend mediante hello API REST.</span><span class="sxs-lookup"><span data-stu-id="975a5-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="975a5-193">In `ViewController.m`, aggiungere hello seguente toosupport metodo delegato tastiera hello per il campo di testo hello di chiusura.</span><span class="sxs-lookup"><span data-stu-id="975a5-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="975a5-194">CTRL + trascinare dalla hello testo campo toohello View Controller icona hello tooset della finestra di progettazione dell'interfaccia di hello Visualizza controller come delegato presa hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="975a5-195">In `ViewController.m`, aggiungere seguente hello delegare la risposta metodi toosupport analisi hello tramite `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="975a5-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="975a5-196">Compilare il progetto hello e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="975a5-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="975a5-197">Se si verifica un errore di compilazione in Xcode7 sul supporto di bitcode, è necessario modificare hello **Build Settings** > **abilitare Bitcode (ENABLE_BITCODE)** troppo**n** in Xcode.</span><span class="sxs-lookup"><span data-stu-id="975a5-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="975a5-198">Hello SDK hub di notifica non supporta attualmente bitcode.</span><span class="sxs-lookup"><span data-stu-id="975a5-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="975a5-199">È possibile trovare tutti i payload di notifica possibili hello in hello Apple [locali e Guida per programmatori notifica Push].</span><span class="sxs-lookup"><span data-stu-id="975a5-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="975a5-200">Verifica della ricezione di notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="975a5-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="975a5-201">le notifiche push tootest in iOS, è necessario distribuire dispositivi dei / o fisici tooa app hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="975a5-202">È possibile inviare notifiche push di Apple usando simulatore iOS hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="975a5-203">Eseguire app hello e verificare che la registrazione ha esito positivo e quindi premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="975a5-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test di registrazione notifica push per app iOS][33]
2. <span data-ttu-id="975a5-205">È possibile inviare una notifica push di test da hello [portale Azure], come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="975a5-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="975a5-206">Se è stato aggiunto il codice per l'invio di notifiche push in hello app, toccare tooenter campo di testo hello all'interno di un messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="975a5-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="975a5-207">Premere quindi hello **inviare** pulsante sulla tastiera di hello o hello **invia una notifica di** pulsante nel messaggio di notifica di hello vista toosend hello.</span><span class="sxs-lookup"><span data-stu-id="975a5-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Test di invio notifica push per app iOS][34]
3. <span data-ttu-id="975a5-209">Hello push notifica viene inviata tooall i dispositivi registrati tooreceive notifiche hello da hello determinato Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="975a5-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Test di ricezione notifica push per app iOS][35]

## <a name="next-steps"></a><span data-ttu-id="975a5-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="975a5-211">Next steps</span></span>
<span data-ttu-id="975a5-212">In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi iOS registrati.</span><span class="sxs-lookup"><span data-stu-id="975a5-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="975a5-213">Si consiglia di un passaggio successivo del learning procedere toohello [notifica hub di notifica gli utenti di Azure per iOS con back-end .NET] esercitazione che assiste nella creazione di un push toosend back-end le notifiche tramite tag.</span><span class="sxs-lookup"><span data-stu-id="975a5-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="975a5-214">Se si desidera che gli utenti dai gruppi di interesse toosegment, è inoltre possibile spostare in toohello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="975a5-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="975a5-215">Per informazioni generali su Hub di notifica, vedere [Panoramica dell'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="975a5-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[iOS Mobile Services SDK versione 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Panoramica dell'Hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[notifica hub di notifica gli utenti di Azure per iOS con back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[locali e Guida per programmatori notifica Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[portale Azure]: https://portal.azure.com
