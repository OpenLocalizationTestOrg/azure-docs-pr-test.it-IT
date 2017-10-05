---
title: Esercitazione sull'invio di ultime notizie mediante Hub di notifica - iOS
description: Informazioni su come usare Hub di notifica del bus di servizio di Azure per inviare notifiche relative alle ultime notizie a dispositivi iOS.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="578b6-103">Uso di Hub di notifica per inviare le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="578b6-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="578b6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="578b6-104">Overview</span></span>
<span data-ttu-id="578b6-105">In questo argomento viene illustrato come utilizzare Hub di notifica di Azure per trasmettere le notifiche relative alle ultime notizie a un'app per iOS.</span><span class="sxs-lookup"><span data-stu-id="578b6-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="578b6-106">Al termine dell'esercitazione, si sarà appreso a effettuare la registrazione alle categorie di ultime notizie desiderate e ricevere le notifiche push solo da tali categorie.</span><span class="sxs-lookup"><span data-stu-id="578b6-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="578b6-107">Questo scenario è un modello comune per molte app nelle quali le notifiche devono essere inviate a gruppi di utenti che hanno dichiarato un interesse, ad esempio lettori di feed RSS, app per fan di musica e così via.</span><span class="sxs-lookup"><span data-stu-id="578b6-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="578b6-108">È possibile abilitare gli scenari di trasmissione includendo uno o più *tag* durante la creazione di una registrazione nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="578b6-109">Quando le notifiche vengono inviate a un tag, tutti i dispositivi che hanno effettuato la registrazione al tag riceveranno la notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="578b6-110">Poiché i tag sono costituiti da stringhe, non è necessario eseguire il provisioning anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="578b6-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="578b6-111">Per ulteriori informazioni sui tag, vedere [Espressioni di routing e tag  per hub di notifica](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="578b6-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="578b6-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="578b6-112">Prerequisites</span></span>
<span data-ttu-id="578b6-113">Questo argomento si basa sull'app creata nell'esercitazione [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="578b6-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="578b6-114">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="578b6-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="578b6-115">Aggiungere la selezione delle categorie all'app</span><span class="sxs-lookup"><span data-stu-id="578b6-115">Add category selection to the app</span></span>
<span data-ttu-id="578b6-116">Il primo passaggio prevede l'aggiunta degli elementi dell'interfaccia utente allo storyboard esistente per consentire all'utente di selezionare le categorie per le quali registrarsi.</span><span class="sxs-lookup"><span data-stu-id="578b6-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="578b6-117">Le categorie selezionate da un utente sono archiviate nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="578b6-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="578b6-118">All'avvio dell'app, viene creata una registrazione del dispositivo nell'hub di notifica con le categorie selezionate come tag.</span><span class="sxs-lookup"><span data-stu-id="578b6-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="578b6-119">Nel file MainStoryboard_iPhone.storyboard aggiungere i componenti seguenti dalla libreria di oggetti:</span><span class="sxs-lookup"><span data-stu-id="578b6-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="578b6-120">Un'etichetta con il testo "Breaking News".</span><span class="sxs-lookup"><span data-stu-id="578b6-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="578b6-121">Etichette con il testo relativo alle categorie "World", "Politics", "Business", "Technology", "Science", "Sports".</span><span class="sxs-lookup"><span data-stu-id="578b6-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="578b6-122">Sei opzioni, una per ogni categoria, impostare lo **stato** di ogni opzione su **Off** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="578b6-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="578b6-123">Un pulsante con l'etichetta "Subscribe".</span><span class="sxs-lookup"><span data-stu-id="578b6-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="578b6-124">L'aspetto dello storyboard dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="578b6-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="578b6-125">Nell'assistente dell'editor creare outlet per tutte le opzioni e denominarli "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch".</span><span class="sxs-lookup"><span data-stu-id="578b6-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="578b6-126">Creare un'azione per il pulsante denominata "subscribe".</span><span class="sxs-lookup"><span data-stu-id="578b6-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="578b6-127">BreakingNewsViewController.h deve contenere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="578b6-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="578b6-128">Creare una nuova **classe Cocoa Touch** chiamata `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="578b6-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="578b6-129">Copiare il seguente codice nella sezione dell'interfaccia del file Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="578b6-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="578b6-130">Aggiungere la seguente direttiva import a Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="578b6-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="578b6-131">Copiare il codice seguente nella sezione di implementazione del file Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="578b6-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="578b6-132">Questa classe usa l'archiviazione locale per archiviare le categorie di notizie che il dispositivo deve ricevere.</span><span class="sxs-lookup"><span data-stu-id="578b6-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="578b6-133">Contiene inoltre un metodo per effettuare la registrazione per queste categorie tramite una registrazione [Modello](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="578b6-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="578b6-134">Nel file Appdelegate.h, aggiungere un'istruzione import per Notifications.h e aggiungere una proprietà per un'istanza della classe delle notifiche:</span><span class="sxs-lookup"><span data-stu-id="578b6-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="578b6-135">Nel metodo **didFinishLaunchingWithOptions** in AppDelegate.m aggiungere il codice per inizializzare l'istanza di notifiche all'inizio del metodo.</span><span class="sxs-lookup"><span data-stu-id="578b6-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="578b6-136">`HUBNAME` e `HUBLISTENACCESS` (definiti in hubinfo.h) dovrebbero già avere i segnaposto `<hub name>` e `<connection string with listen access>` sostituiti con il nome dell'hub di notifica e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="578b6-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="578b6-137">Poiché le credenziali che sono distribuite con un'app client in genere non sono sicure, distribuire solo la chiave per l'accesso Listen con l'app client.</span><span class="sxs-lookup"><span data-stu-id="578b6-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="578b6-138">L'accesso Listen consente all'app di registrarsi per le notifiche ma le registrazioni esistenti non possono essere modificate e le notifiche non possono essere inviate.</span><span class="sxs-lookup"><span data-stu-id="578b6-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="578b6-139">La chiave di accesso completa viene usata in un servizio back-end sicuro per l'invio delle notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="578b6-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="578b6-140">Nel metodo **didRegisterForRemoteNotificationsWithDeviceToken** in AppDelegate.m sostituire il codice nel metodo con il codice seguente per passare il token del dispositivo alla classe delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="578b6-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="578b6-141">La classe delle notifiche eseguirà la registrazione per le notifiche con le categorie.</span><span class="sxs-lookup"><span data-stu-id="578b6-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="578b6-142">Se l'utente modifica le selezioni delle categorie, chiamare il metodo `subscribeWithCategories` in risposta al pulsante **sottoscrizione** per aggiornarle.</span><span class="sxs-lookup"><span data-stu-id="578b6-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="578b6-143">Poiché il token di dispositivo assegnato dal servizio di notifica Push di Apple può cambiare in qualsiasi momento, è necessario ripetere la registrazione per le notifiche di frequente per evitare errori di notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="578b6-144">In questo esempio viene effettuata la registrazione per le notifiche a ogni avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="578b6-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="578b6-145">Per le app che vengono eseguite con una frequenza maggiore di una volta al giorno, è possibile ignorare la registrazione per conservare la larghezza di banda qualora sia trascorso meno di un giorno dalla registrazione precedente.</span><span class="sxs-lookup"><span data-stu-id="578b6-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="578b6-146">Si noti che a questo punto nel metodo **didRegisterForRemoteNotificationsWithDeviceToken** non dovrebbe essere presente altro codice.</span><span class="sxs-lookup"><span data-stu-id="578b6-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="578b6-147">I metodi seguenti devono essere già presenti in appdelegate. M dal completamento di [iniziare con gli hub di notifica] [ get-started] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="578b6-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="578b6-148">In caso contrario, aggiungerli.</span><span class="sxs-lookup"><span data-stu-id="578b6-148">If not, add them.</span></span>
   
    <span data-ttu-id="578b6-149">-(void) MessageBox:(NSString *) titolo messaggio:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="578b6-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="578b6-150">}</span><span class="sxs-lookup"><span data-stu-id="578b6-150">}</span></span>
   
   * <span data-ttu-id="578b6-151">applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification: (NSDictionary *) userInfo {NSLog (@"% @", userInfo);   [self MessageBox:@"Notification" messaggio: [valueForKey:@"alert [userInfo objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="578b6-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="578b6-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="578b6-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="578b6-153">In ViewController.m, aggiungere un'istruzione import per AppDelegate.h e copiare il codice seguente nel metodo **subscribe** generato da XCode.</span><span class="sxs-lookup"><span data-stu-id="578b6-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="578b6-154">Questo codice aggiornerà la registrazione della notifica per utilizzare i nuovi tag di categoria selezionati dall'utente nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="578b6-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="578b6-155">Questo metodo crea un elenco **NSMutableArray** di categorie e usa la classe **Notifications** per archiviare l'elenco nell'archiviazione locale e registrare i tag corrispondenti nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="578b6-156">Se le categorie vengono modificate, la registrazione viene ricreata con le nuove categorie.</span><span class="sxs-lookup"><span data-stu-id="578b6-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="578b6-157">In ViewController.m, aggiungere il codice seguente nel metodo **viewDidLoad** per impostare l'interfaccia utente in base alle categorie salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="578b6-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="578b6-158">Ora l'app può archiviare un insieme di categorie nella risorsa di archiviazione locale del dispositivo utilizzata per la registrazione con l'hub di notifica ogni volta che l'app viene avviata.</span><span class="sxs-lookup"><span data-stu-id="578b6-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="578b6-159">L'utente può modificare la selezione di categorie al runtime e scegliere il metodo **subscribe** per aggiornare la registrazione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="578b6-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="578b6-160">Successivamente, si aggiornerà l'app per inviare le notifiche relative alle ultime notizie direttamente nell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="578b6-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="578b6-161">(facoltativo) Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="578b6-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="578b6-162">Se non si ha accesso a Visual Studio, è possibile passare alla sezione successiva e inviare notifiche dall’app stessa.</span><span class="sxs-lookup"><span data-stu-id="578b6-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="578b6-163">È anche possibile inviare la notifica modello appropriata dal [portale di Azure classico] usando la scheda debug per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="578b6-164">(facoltativo) Inviare notifiche dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="578b6-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="578b6-165">In genere le notifiche vengono inviate da un servizio di back-end ma per questa esercitazione è possibile inviare notifiche relative alle ultime notizie direttamente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="578b6-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="578b6-166">A tale scopo si aggiornerà il `SendNotificationRESTAPI` metodo che è stato definito nel [iniziare con gli hub di notifica] [ get-started] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="578b6-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="578b6-167">In ViewController.m aggiornare il metodo `SendNotificationRESTAPI` come segue in modo che accetti un parametro per il tag di categoria e invii la notifica [modello](notification-hubs-templates-cross-platform-push-messages.md) appropriata.</span><span class="sxs-lookup"><span data-stu-id="578b6-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. <span data-ttu-id="578b6-168">In ViewController.m aggiornare l’azione **Send Notification** nel modo illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="578b6-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="578b6-169">In tal modo si inviano notifiche a più piattaforme utilizzando singolarmente ogni tag.</span><span class="sxs-lookup"><span data-stu-id="578b6-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="578b6-170">Ricompilare il progetto e assicurarsi che non siano presenti errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="578b6-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="578b6-171">Esecuzione dell'app e generazione di notifiche</span><span class="sxs-lookup"><span data-stu-id="578b6-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="578b6-172">Premere il pulsante Esegui per compilare il progetto e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="578b6-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="578b6-173">Selezionare alcune opzioni di notizie per cui eseguire la sottoscrizione e premere il pulsante **Subscribe** .</span><span class="sxs-lookup"><span data-stu-id="578b6-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="578b6-174">Verrà visualizzata una finestra di dialogo che indica che è staa effettuata la sottoscrizione alle notifiche.</span><span class="sxs-lookup"><span data-stu-id="578b6-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="578b6-175">Quando si fa clic su **Subscribe**, l'app converte le categorie selezionate in tag e richiede una nuova registrazione del dispositivo per i tag selezionati dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="578b6-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="578b6-176">Immettere un messaggio da inviare come ultime notizie, quindi premere il pulsante **Send Notification** (Invia notifica).</span><span class="sxs-lookup"><span data-stu-id="578b6-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="578b6-177">In alternativa, eseguire l'app console .NET per generare le notifiche.</span><span class="sxs-lookup"><span data-stu-id="578b6-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="578b6-178">Ogni dispositivo iscritto alle notizie riceverà le notifiche relative alle ultime notizie appena inviate.</span><span class="sxs-lookup"><span data-stu-id="578b6-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="578b6-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="578b6-179">Next steps</span></span>
<span data-ttu-id="578b6-180">In questa esercitazione si è appreso a trasmettere le ultime novità per categoria.</span><span class="sxs-lookup"><span data-stu-id="578b6-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="578b6-181">Per informazioni su altri scenari avanzati di Hub di notifica, provare a completare le seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="578b6-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="578b6-182">**[Usare Hub di notifica per la trasmissione di notizie localizzate]**</span><span class="sxs-lookup"><span data-stu-id="578b6-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="578b6-183">Informazioni su come espandere l'app relativa alle ultime novità per abilitare l'invio di notifiche localizzate.</span><span class="sxs-lookup"><span data-stu-id="578b6-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="578b6-184">[Usare Hub di notifica per la trasmissione di notizie localizzate]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="578b6-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="578b6-185">[portale di Azure classico]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="578b6-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
