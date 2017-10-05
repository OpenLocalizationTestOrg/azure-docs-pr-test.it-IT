---
title: Invio di notifiche push a iOS con Hub di notifica di Azure | Documentazione Microsoft
description: In questa esercitazione si apprende come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione iOS.
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
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="3a9c7-104">Invio di notifiche push a iOS con Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="3a9c7-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3a9c7-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3a9c7-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="3a9c7-106">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3a9c7-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3a9c7-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="3a9c7-109">Questa esercitazione illustra come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione per iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="3a9c7-110">Si creerà un'app iOS vuota che riceve notifiche push tramite [Apple Push Notification Service (servizio APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="3a9c7-111">Al termine, sarà possibile usare l’hub di notifica per trasmettere le notifiche push a tutti i dispositivi che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a9c7-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3a9c7-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="3a9c7-113">Il codice completo per questa esercitazione è disponibile in [GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3a9c7-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a9c7-114">Prerequisites</span></span>
<span data-ttu-id="3a9c7-115">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="3a9c7-116">[Mobile Services iOS SDK versione 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="3a9c7-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="3a9c7-117">Ultima versione di [Xcode]</span><span class="sxs-lookup"><span data-stu-id="3a9c7-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="3a9c7-118">Un dispositivo con iOS 8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="3a9c7-119">[Apple Developer Program](https://developer.apple.com/programs/) .</span><span class="sxs-lookup"><span data-stu-id="3a9c7-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3a9c7-120">Considerati i requisiti di configurazione delle notifiche push, è necessario distribuire e testare le notifiche push in un dispositivo fisico con iOS, iPhone o iPad, anziché in un simulatore iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="3a9c7-121">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="3a9c7-122">Configurare l'hub di notifica per l'invio di notifiche push di iOS</span><span class="sxs-lookup"><span data-stu-id="3a9c7-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="3a9c7-123">Questa sezione illustra come creare un nuovo hub di notifica e configurare l'autenticazione con il servizio APN usando il certificato push **.p12** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="3a9c7-124">Se si vuole usare un hub di notifica che è già stato creato, è possibile ignorare il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="3a9c7-125">Fare clic sul pulsante <b>Servizi di notifica</b> nel pannello <b>Impostazioni</b> e quindi selezionare <b>Apple (servizio APN)</b>.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="3a9c7-126">Fare clic su <b>Carica certificato</b> e selezionare il file con estensione <b>p12</b> esportato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="3a9c7-127">Assicurarsi di specificare anche la password corretta.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="3a9c7-128">Assicurarsi di selezionare la modalità <b>Sandbox</b>, destinata allo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="3a9c7-129">Usare la modalità <b>Produzione</b> solo se si vuole inviare notifiche push agli utenti che hanno acquistato l'app dallo Store.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="3a9c7-130">&emsp;&emsp;&emsp;&emsp;![Configurare APNS nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="3a9c7-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurare il certificato APN nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="3a9c7-132">L'hub di notifica è ora configurato per l'uso con il servizio APN e sono disponibili le stringhe di connessione per la registrazione dell'app e l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="3a9c7-133">Connettere l'app iOS all'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="3a9c7-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="3a9c7-134">In Xcode creare un nuovo progetto iOS e selezionare il modello **Single View Application** .</span><span class="sxs-lookup"><span data-stu-id="3a9c7-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - Single View Application][8]
    
2. <span data-ttu-id="3a9c7-136">Quando si configurano le opzioni per il nuovo progetto, assicurarsi di usare gli stessi valori per **Product Name** (Nome prodotto) e **Organization Identifier** (Identificatore organizzazione) specificati in precedenza durante l'impostazione dell'ID del bundle nel portale per sviluppatori Apple.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - Opzioni di progetto][11]
    
3. <span data-ttu-id="3a9c7-138">In **Targets** (Destinazioni) fare clic sul nome del progetto, quindi scegliere la scheda **Build Settings** (Impostazioni compilazione) ed espandere **Code Signing Identity** (Identità di firma del codice) e quindi in **Debug** impostare l'identità di firma del codice.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="3a9c7-139">Modificare l'impostazione di **Levels** (Livelli) da **Basic** (Base) a **All** (Tutto) e quindi impostare **Provisioning Profile** (Profili di provisioning) sul profilo di provisioning creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="3a9c7-140">Se il profilo di provisioning creato in Xcode non viene visualizzato, provare ad aggiornare i profili per l'identità di firma.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="3a9c7-141">Fare clic su **Xcode** nella barra dei menu, fare clic su **Preferences** (Preferenze), selezionare la scheda **Account**, fare clic sul pulsante **View Details** (Visualizza dettagli), selezionare la propria identità di firma e infine fare clic sul pulsante di aggiornamento nell'angolo in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - Profilo di provisioning][9]
4. <span data-ttu-id="3a9c7-143">Scaricare la[Mobile Services iOS SDK versione 1.2.4] e decomprimere il file.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="3a9c7-144">In Xcode fare clic con il pulsante destro del mouse sul progetto e scegliere l'opzione **Add Files to** (Aggiungi file a) per aggiungere la cartella **WindowsAzureMessaging.framework** al progetto Xcode.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="3a9c7-145">Selezionare **Copy items if needed** (Copia elementi se necessario) e fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3a9c7-146">Notification Hubs SDK non supporta attualmente bitcode Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="3a9c7-147">È necessario impostare **Enable Bitcode** (Abilita Bitcode) su **No** in **Build Options** (Opzioni di compilazione) per il progetto.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Decomprimere Azure SDK][10]
5. <span data-ttu-id="3a9c7-149">Aggiungere un nuovo file di intestazione al progetto denominato `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="3a9c7-150">Questo file includerà le costanti per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="3a9c7-151">Aggiungere le definizioni seguenti e sostituire i segnaposto dei valori letterali stringa con il *nome dell'hub* e il valore *DefaultListenSharedAccessSignature* annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="3a9c7-152">Aprire il file `AppDelegate.h` e aggiungere le direttive import seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="3a9c7-153">Nel file `AppDelegate.m file` aggiungere il codice seguente nel metodo `didFinishLaunchingWithOptions`, in base alla versione di iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="3a9c7-154">Questo codice registra l'handle di dispositivo nel servizio APNS:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="3a9c7-155">Per iOS 8:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="3a9c7-156">Per versioni di iOS precedenti alla 8:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="3a9c7-157">Nello stesso file aggiungere i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-157">In the same file, add the following methods.</span></span> <span data-ttu-id="3a9c7-158">Questo codice si connette all'hub di notifica usando le informazioni di connessione specificate in HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="3a9c7-159">Fornisce il token del dispositivo all'hub di notifica in modo che quest'ultimo possa inviare notifiche:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="3a9c7-160">Nello stesso file aggiungere il metodo seguente per visualizzare un avviso **UIAlert** se la notifica viene ricevuta mentre l'app è attiva:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="3a9c7-161">Compilare ed eseguire l'app sul dispositivo per assicurarsi che non si verifichino errori.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="3a9c7-162">Inviare notifiche push di prova</span><span class="sxs-lookup"><span data-stu-id="3a9c7-162">Send test push notifications</span></span>
<span data-ttu-id="3a9c7-163">È possibile testare la ricezione delle notifiche push nell'app inviandole tramite il [portale di Azure]. Cercare la sezione **Risoluzione dei problemi** nel pannello dell'hub e usare l'opzione *Invio di prova*.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Portale di Azure - Invio di prova][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="3a9c7-165">(Facoltativo) Inviare notifiche push dall'app</span><span class="sxs-lookup"><span data-stu-id="3a9c7-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a9c7-166">Questo esempio di invio di notifiche dall'app client è descritto solo a scopo didattico.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="3a9c7-167">Essendo necessario l'elemento `DefaultFullSharedAccessSignature` nell'app client, l'hub di notifica viene esposto al rischio che un utente acceda per inviare notifiche non autorizzate ai client.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="3a9c7-168">Questa sezione fornisce un esempio di invio di notifiche push dall'interno di un'app tramite l'interfaccia REST.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="3a9c7-169">In Xcode aprire `Main.storyboard` e aggiungere i componenti dell'interfaccia utente riportati di seguito dalla libreria di oggetti, per consentire all'utente di inviare notifiche push nell'app.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="3a9c7-170">Etichetta senza testo.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-170">A label with no label text.</span></span> <span data-ttu-id="3a9c7-171">Sarà usata per segnalare errori di invio di notifiche.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="3a9c7-172">La proprietà **Lines** deve essere impostata su **0**, in modo da limitare automaticamente le dimensioni ai margini destro e sinistro e alla parte superiore della visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="3a9c7-173">Campo di testo con testo **segnaposto** impostato su **Enter Notification Message** (Immetti messaggio di notifica).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="3a9c7-174">Vincolare il campo sotto l'etichetta, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="3a9c7-175">Impostare il controller di visualizzazione come delegato di uscita.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="3a9c7-176">Pulsante denominato **Send Notification** vincolato, appena sotto il campo di testo e al centro nell'area orizzontale.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="3a9c7-177">La visualizzazione dovrebbe apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-177">The view should look as follows:</span></span>
     
     ![Finestra di progettazione Xcode][32]
2. <span data-ttu-id="3a9c7-179">[Aggiungere punti di uscita](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) per l'etichetta e i campi di testo connessi alla visualizzazione e aggiornare la definizione di `interface` per supportare `UITextFieldDelegate` e `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="3a9c7-180">Aggiungere le tre dichiarazioni di proprietà riportate di seguito per supportare la chiamata dell'API REST e l'analisi della risposta.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="3a9c7-181">Il file ViewController.h dovrebbe apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="3a9c7-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="3a9c7-182">Aprire `HubInfo.h` e aggiungere le costanti seguenti che verranno usate per inviare notifiche all'hub.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="3a9c7-183">Sostituire il valore letterale stringa del segnaposto con la stringa di connessione *DefaultFullSharedAccessSignature* effettiva.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="3a9c7-184">Aggiungere le istruzioni `#import` seguenti al file `ViewController.h`.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="3a9c7-185">In `ViewController.m` aggiungere il codice seguente all'implementazione dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="3a9c7-186">Questo codice analizzerà la stringa di connessione *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="3a9c7-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="3a9c7-187">Come indicato nel [riferimento all'API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), queste informazioni analizzate verranno usate per generare un token di firma di accesso condiviso per l'intestazione della richiesta **Authorization** .</span><span class="sxs-lookup"><span data-stu-id="3a9c7-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="3a9c7-188">In `ViewController.m` aggiornare il metodo `viewDidLoad` per analizzare la stringa di connessione quando viene caricata la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="3a9c7-189">Aggiungere anche i metodi di utilità illustrati di seguito all'implementazione dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

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





1. <span data-ttu-id="3a9c7-190">In `ViewController.m`aggiungere il codice seguente all'implementazione dell'interfaccia per generare il token di autorizzazione della firma di accesso condiviso che verrà fornito nell'intestazione **Authorization** , come indicato nel [riferimento all'API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a9c7-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
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
2. <span data-ttu-id="3a9c7-191">Premere CTRL e trascinare dal pulsante **Send Notification** (Invia notifica) a `ViewController.m` per aggiungere un'azione denominata **SendNotificationMessage** per l'evento **Touch Down**.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="3a9c7-192">Aggiornare il metodo con il codice seguente per inviare la notifica con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-192">Update method with the following code to send the notification using the REST API.</span></span>
   
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
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
3. <span data-ttu-id="3a9c7-193">In `ViewController.m`aggiungere il metodo delegato seguente per supportare la chiusura della tastiera per il campo di testo.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="3a9c7-194">Premere CTRL e trascinare dal campo di testo all'icona del controller di visualizzazione nella finestra di progettazione di interfaccia per impostare il controller di visualizzazione del delegato di uscita.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="3a9c7-195">In `ViewController.m` aggiungere i metodi delegati seguenti per supportare l'analisi della risposta con `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
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
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="3a9c7-196">Compilare il progetto e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="3a9c7-197">Se si verifica un errore di compilazione in Xcode7 relativo al supporto per Bitcode, è necessario modificare **Build Settings** (Impostazioni compilazione) > **Enable Bitcode (ENABLE_BITCODE)** (Abilita Bitcode) impostandolo su **NO** in Xcode.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="3a9c7-198">Notification Hubs SDK non supporta attualmente bitcode.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="3a9c7-199">È possibile trovare tutti i payload di notifica disponibili nella [guida alla programmazione di notifiche push e locali]di Apple.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="3a9c7-200">Verifica della ricezione di notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="3a9c7-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="3a9c7-201">Per testare le notifiche push in iOS, è necessario distribuire l'app in un dispositivo fisico iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="3a9c7-202">Non è possibile inviare notifiche push Apple con il simulatore iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="3a9c7-203">Eseguire l'app e verificare che la registrazione riesca e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test di registrazione notifica push per app iOS][33]
2. <span data-ttu-id="3a9c7-205">È possibile inviare una notifica push di prova dal [portale di Azure], come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="3a9c7-206">Se è stato aggiunto codice per l'invio delle notifiche push nell'app, toccare nel campo di testo per immettere un messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="3a9c7-207">Usare il pulsante **Send** (Invia) sulla tastiera o il pulsante **Send Notification** (Invia notifica) nella visualizzazione per inviare il messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Test di invio notifica push per app iOS][34]
3. <span data-ttu-id="3a9c7-209">La notifica push viene inviata a tutti i dispositivi registrati per la ricezione di notifiche dall'hub di notifica specifico.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Test di ricezione notifica push per app iOS][35]

## <a name="next-steps"></a><span data-ttu-id="3a9c7-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a9c7-211">Next steps</span></span>
<span data-ttu-id="3a9c7-212">In questo semplice esempio le notifiche push sono state trasmesse a tutti i dispositivi iOS registrati.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="3a9c7-213">Come passaggio successivo nella formazione, vedere l'esercitazione [Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET] , che illustra la creazione di un back-end per l'invio di notifiche push tramite tag.</span><span class="sxs-lookup"><span data-stu-id="3a9c7-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="3a9c7-214">Per segmentare gli utenti per gruppi di interesse, è possibile vedere anche l'esercitazione [Usare Hub di notifica per inviare le ultime notizie] .</span><span class="sxs-lookup"><span data-stu-id="3a9c7-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="3a9c7-215">Per informazioni generali su Hub di notifica, vedere [Panoramica dell'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="3a9c7-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="3a9c7-216">[Mobile Services iOS SDK versione 1.2.4]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="3a9c7-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="3a9c7-217">[Panoramica dell'Hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="3a9c7-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="3a9c7-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="3a9c7-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="3a9c7-219">[Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="3a9c7-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="3a9c7-220">[Usare Hub di notifica per inviare le ultime notizie]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="3a9c7-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="3a9c7-221">[guida alla programmazione di notifiche push e locali]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="3a9c7-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="3a9c7-222">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="3a9c7-222">[Azure Portal]: https://portal.azure.com</span></span>
