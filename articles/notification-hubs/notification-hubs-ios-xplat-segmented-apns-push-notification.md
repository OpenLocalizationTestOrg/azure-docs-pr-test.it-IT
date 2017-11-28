---
title: aaaNotification hub ultime notizie esercitazione - iOS
description: Informazioni su come toouse hub di notifica di Azure Service Bus toosend dispositivi tooiOS le notifiche di notizie di rilievo.
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
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="f6512-103">Utilizzare gli hub di notifica toosend le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="f6512-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="f6512-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f6512-104">Overview</span></span>
<span data-ttu-id="f6512-105">In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooan app iOS.</span><span class="sxs-lookup"><span data-stu-id="f6512-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="f6512-106">Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie.</span><span class="sxs-lookup"><span data-stu-id="f6512-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="f6512-107">Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per ventole musica e così via.</span><span class="sxs-lookup"><span data-stu-id="f6512-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="f6512-108">Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="f6512-109">Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="f6512-110">Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f6512-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="f6512-111">Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="f6512-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6512-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6512-112">Prerequisites</span></span>
<span data-ttu-id="f6512-113">In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="f6512-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="f6512-114">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="f6512-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="f6512-115">Aggiungi categoria selezione toohello app</span><span class="sxs-lookup"><span data-stu-id="f6512-115">Add category selection toohello app</span></span>
<span data-ttu-id="f6512-116">primo passaggio Hello è tooadd hello UI elementi tooyour storyboard esistente che consentono di hello utente tooselect categorie tooregister.</span><span class="sxs-lookup"><span data-stu-id="f6512-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="f6512-117">categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="f6512-118">Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.</span><span class="sxs-lookup"><span data-stu-id="f6512-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="f6512-119">Nel MainStoryboard_iPhone.storyboard aggiungere hello seguendo i componenti dalla libreria di oggetti hello:</span><span class="sxs-lookup"><span data-stu-id="f6512-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="f6512-120">Un'etichetta con il testo "Breaking News".</span><span class="sxs-lookup"><span data-stu-id="f6512-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="f6512-121">Etichette con il testo relativo alle categorie "World", "Politics", "Business", "Technology", "Science", "Sports".</span><span class="sxs-lookup"><span data-stu-id="f6512-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="f6512-122">Sei switch, uno per ogni categoria, impostare ogni switch **stato** toobe **Off** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f6512-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="f6512-123">Un pulsante con l'etichetta "Subscribe".</span><span class="sxs-lookup"><span data-stu-id="f6512-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="f6512-124">L'aspetto dello storyboard dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f6512-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="f6512-125">Nell'editor di Assistente hello, creare prese per tutte le opzioni di hello e chiamarli "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="f6512-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="f6512-126">Creare un'azione per il pulsante denominata "subscribe".</span><span class="sxs-lookup"><span data-stu-id="f6512-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="f6512-127">Il ViewController.h deve contenere i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="f6512-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="f6512-128">Creare una nuova **classe Cocoa Touch** chiamata `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="f6512-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="f6512-129">Copiare hello seguente codice nella sezione dell'interfaccia hello del file hello Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="f6512-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="f6512-130">Aggiungere hello tooNotifications.m direttiva import seguente:</span><span class="sxs-lookup"><span data-stu-id="f6512-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="f6512-131">Copiare hello seguente codice nella sezione di implementazione hello del file hello Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="f6512-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
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



    <span data-ttu-id="f6512-132">Questa classe utilizza toostore di archiviazione locale e recuperare le categorie di hello delle news che riceverà questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6512-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="f6512-133">Contiene inoltre un metodo tooregister per queste categorie utilizzando un [modello](notification-hubs-templates-cross-platform-push-messages.md) registrazione.</span><span class="sxs-lookup"><span data-stu-id="f6512-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="f6512-134">Nel file appdelegate. H hello, aggiungere un'istruzione di importazione per Notifications.h e aggiungere una proprietà di un'istanza della classe notifiche hello:</span><span class="sxs-lookup"><span data-stu-id="f6512-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="f6512-135">In hello **didFinishLaunchingWithOptions** metodo appdelegate. M, aggiungere l'istanza di notifiche hello di tooinitialize di hello codice all'inizio di hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="f6512-136">`HUBNAME`e `HUBLISTENACCESS` (definito in hubinfo.h) dovrebbe già disporre hello `<hub name>` e `<connection string with listen access>` segnaposto sostituiti con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature*ottenuti in precedenza</span><span class="sxs-lookup"><span data-stu-id="f6512-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="f6512-137">Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="f6512-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="f6512-138">Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="f6512-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="f6512-139">chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="f6512-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="f6512-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** metodo appdelegate. M, sostituire il codice di hello nel metodo hello con hello seguenti classi di codice toopass hello dispositivo toohello token notifiche.</span><span class="sxs-lookup"><span data-stu-id="f6512-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="f6512-141">classe notifiche Hello eseguirà hello registrazione per le notifiche con categorie hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="f6512-142">Se l'utente di hello cambia le selezioni delle categorie, definiamo hello `subscribeWithCategories` metodo nella risposta toohello **sottoscrizione** tooupdate pulsante li.</span><span class="sxs-lookup"><span data-stu-id="f6512-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f6512-143">Perché il token di dispositivo hello assegnato da hello Apple Push Notification Service (APNS) è possibile modificare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid.</span><span class="sxs-lookup"><span data-stu-id="f6512-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="f6512-144">Questo esempio viene registrato per notifica ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="f6512-145">Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="f6512-146">Si noti che a questo punto non dovrebbe esistere alcun altro codice in hello **didRegisterForRemoteNotificationsWithDeviceToken** metodo.</span><span class="sxs-lookup"><span data-stu-id="f6512-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="f6512-147">Hello metodi seguenti devono essere già presenti in appdelegate. M completamento hello [iniziare con gli hub di notifica] [ get-started] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f6512-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="f6512-148">In caso contrario, aggiungerli.</span><span class="sxs-lookup"><span data-stu-id="f6512-148">If not, add them.</span></span>
   
    <span data-ttu-id="f6512-149">-(void) MessageBox:(NSString *) titolo messaggio:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="f6512-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="f6512-150">}</span><span class="sxs-lookup"><span data-stu-id="f6512-150">}</span></span>
   
   * <span data-ttu-id="f6512-151">applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification: (NSDictionary *) userInfo {NSLog (@"% @", userInfo);   [self MessageBox:@"Notification" messaggio: [valueForKey:@"alert [userInfo objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="f6512-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="f6512-152">Questo metodo gestisce le notifiche ricevute durante l'esecuzione mediante la visualizzazione di una semplice applicazione hello **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="f6512-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="f6512-153">In ViewController.m, aggiungere un'istruzione di importazione per appdelegate. H e copia hello seguente di codice in hello generato XCode **sottoscrizione** metodo.</span><span class="sxs-lookup"><span data-stu-id="f6512-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="f6512-154">Questo codice aggiornerà hello notifica registrazione toouse hello nuova categoria tag hello utente ha scelto nell'interfaccia utente di hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
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
   
   <span data-ttu-id="f6512-155">Questo metodo crea un **NSMutableArray** di categorie e utilizza hello **notifiche** toostore hello elenco classe hello locale archiviazione registri hello corrispondente tag e con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="f6512-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="f6512-156">Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="f6512-157">In ViewController.m, aggiungere hello seguente di codice hello **viewDidLoad** interfaccia utente di metodo tooset hello in base alle categorie di hello salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f6512-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="f6512-158">app Hello ora possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="f6512-159">utente di Hello può modificare hello selezione di categorie in fase di esecuzione e fare clic su hello **sottoscrizione** metodo tooupdate hello registrazione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="f6512-160">Aggiornare quindi hello toosend di app hello rilievo notifiche notizie direttamente in hello app stessa.</span><span class="sxs-lookup"><span data-stu-id="f6512-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="f6512-161">(facoltativo) Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="f6512-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="f6512-162">Se non si dispone di accesso tooVisual Studio, è possibile ignorare la sezione successiva toohello e inviare notifiche da hello app stessa.</span><span class="sxs-lookup"><span data-stu-id="f6512-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="f6512-163">È anche possibile inviare notifica di hello modello corretto da hello [portale di Azure classico] utilizzo scheda debug hello per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="f6512-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="f6512-164">(facoltativo) Inviare notifiche dal dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="f6512-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="f6512-165">In genere le notifiche potrebbero essere inviate da un servizio back-end, tuttavia, è possibile inviare notifiche sulle ultime notizie direttamente dall'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="f6512-166">toodo questo verrà aggiornato hello `SendNotificationRESTAPI` metodo che è stato definito in hello [iniziare con gli hub di notifica] [ get-started] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f6512-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="f6512-167">In hello aggiornamento ViewController.m `SendNotificationRESTAPI` metodo come segue in modo che accetta un parametro per il tag di categoria hello e le invia hello corretto [modello](notification-hubs-templates-cross-platform-push-messages.md) notifica.</span><span class="sxs-lookup"><span data-stu-id="f6512-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
2. <span data-ttu-id="f6512-168">In hello aggiornamento ViewController.m **invia una notifica** azione, come illustrato nel codice hello che segue.</span><span class="sxs-lookup"><span data-stu-id="f6512-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="f6512-169">In modo che verranno inviate notifiche hello con ogni tag singolarmente e inviare toomultiple piattaforme.</span><span class="sxs-lookup"><span data-stu-id="f6512-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="f6512-170">Ricompilare il progetto e assicurarsi che non siano presenti errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f6512-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="f6512-171">Eseguire app hello e generare le notifiche</span><span class="sxs-lookup"><span data-stu-id="f6512-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="f6512-172">Hello premere eseguire pulsante toobuild hello progetto e avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="f6512-173">Selezionare alcune toosubscribe tooand di rilievo notizie opzioni e quindi premere hello **Sottoscrivi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f6512-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="f6512-174">Verrà visualizzata una finestra di dialogo che indica le notifiche sono stati sottoscritti hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="f6512-175">Quando si sceglie **Sottoscrivi**, hello app converte hello selezionata categorie nei tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato da hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f6512-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="f6512-176">Immettere un toobe messaggio inviato come notizie premere hello **invia una notifica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f6512-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="f6512-177">In alternativa, eseguire le notifiche tramite toogenerate app hello .NET console.</span><span class="sxs-lookup"><span data-stu-id="f6512-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="f6512-178">Ogni notizie toobreaking dispositivo sottoscritto riceverà notifiche sulle ultime hello notizie che appena stata inviata.</span><span class="sxs-lookup"><span data-stu-id="f6512-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6512-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6512-179">Next steps</span></span>
<span data-ttu-id="f6512-180">In questa esercitazione è stato appreso come toobroadcast le ultime notizie per categoria.</span><span class="sxs-lookup"><span data-stu-id="f6512-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="f6512-181">Provare a eseguire una delle seguenti esercitazioni che evidenziano altri scenari avanzati di hub di notifica hello:</span><span class="sxs-lookup"><span data-stu-id="f6512-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="f6512-182">**[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]**</span><span class="sxs-lookup"><span data-stu-id="f6512-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="f6512-183">Informazioni su come hello tooexpand interrompere l'invio di notizie app tooenable localizzata notifiche.</span><span class="sxs-lookup"><span data-stu-id="f6512-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[portale di Azure classico]: https://manage.windowsazure.com
