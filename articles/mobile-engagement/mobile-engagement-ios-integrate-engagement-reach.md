---
title: aaaAzure iOS Mobile Engagement SDK raggiungere integrazione | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>La modalità di copertura di Engagement tooIntegrate in iOS
Attenersi alla procedura di integrazione hello descritta in hello [come tooIntegrate Engagement documento iOS](mobile-engagement-ios-integrate-engagement.md) prima di seguire questa Guida.

Questa documentazione richiede XCode 8. Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Esiste un bug noto nella versione precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono attivate. toofix questo sarà necessario tooimplement hello obsoleto API `application:didReceiveRemoteNotification:` nell'app, delegato come indicato di seguito:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata. È necessario passare tooXCode 8 appena possibile.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Abilitare il tooreceive app invisibile all'utente le notifiche Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Procedura di integrazione
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Incorporare hello Engagement Reach SDK nel progetto iOS
* Aggiungere hello Reach sdk nel progetto Xcode. In Xcode, passare troppo**progetto \> aggiungere tooproject** scegliere hello `EngagementReach` cartella.

### <a name="modify-your-application-delegate"></a>Modificare il delegato dell'applicazione
* Nella parte superiore di hello del file di implementazione, importare il modulo di copertura di Engagement hello:

      [...]
      #import "AEReachModule.h"
* Metodo `applicationDidFinishLaunching:` o `application:didFinishLaunchingWithOptions:`, creare un modulo di reach e passarlo tooyour linea Engagement inizializzazione:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Modificare **'icon.png'** stringa con il nome di immagine hello desiderato come l'icona di notifica.
* Se si desidera che l'opzione hello toouse *valore badge aggiornamento* in campagne di copertura o eseguire il push nativo toouse \<formato/nativo di copertura di SaaS/API/campagna Push\> campagne, è necessario gestire modulo Reach hello Hello badge icona stesso (verrà cancellato automaticamente badge applicazione hello e reimposta anche il valore di hello archiviato da Engagement ogni volta che un'applicazione hello è avviato o foregrounded). Questa operazione viene eseguita aggiungendo hello successiva riga dopo l'inizializzazione del modulo Reach:

      [reach setAutoBadgeEnabled:YES];
* Se si desidera toohandle Reach push di dati, è necessario consentire il delegato applicazione conforme toohello `AEReachDataPushDelegate` protocollo. Aggiungere hello successiva riga dopo l'inizializzazione del modulo Reach:

      [reach setDataPushDelegate:self];
* È possibile implementare i metodi di hello `onDataPushStringReceived:` e `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` nel delegato dell'applicazione:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Categoria
il parametro di categoria Hello è facoltativo quando si crea una campagna Push di dati e consente che inserisce dati toofilter. Ciò è utile se si desidera toopush diversi tipi di `Base64` tooidentify dati e si desidera tipo prima dell'analisi li.

**L'applicazione è ora visualizzato e pronto tooreceive raggiunga il contenuto.**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Come tooreceive sondaggi in qualsiasi momento e gli annunci
Engagement possibile inviare notifiche di raggiungere gli utenti finali tooyour in qualsiasi momento utilizzando hello Apple Push Notification Service.

tooenable questa funzionalità, verranno tooprepare l'applicazione per le notifiche push di Apple e modificare il delegato dell'applicazione.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Preparare l'applicazione per le notifiche push Apple
Seguire la Guida hello: [come tooPrepare l'applicazione per le notifiche Push di Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Aggiungere il codice client necessario hello
*A questo punto l'applicazione deve disporre di un certificato Apple push registrato nel server front-end di Engagement hello.*

Se non si è già fatto, è necessario tooregister le notifiche push tooreceive di applicazione.

* Hello importazione `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Aggiungere hello seguente riga all'avvio dell'applicazione (in genere in `application:didFinishLaunchingWithOptions:`):

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

Quindi, è necessario tooprovide token del dispositivo hello tooEngagement restituiti dai server Apple. Questa operazione viene eseguita nel metodo hello denominato `application:didRegisterForRemoteNotificationsWithDeviceToken:` nel delegato dell'applicazione:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Infine, è necessario tooinform hello Engagement SDK quando l'applicazione riceve una notifica remota. toodo che, chiamare hello metodo `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` nel delegato dell'applicazione:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Per impostazione predefinita, copertura di Engagement controlla completionHandler hello. Se si desidera toomanually rispondono toohello `handler` blocco nel codice, è possibile passare null per hello `handler` argomento e il controllo completamento hello bloccare manualmente. Vedere hello `UIBackgroundFetchResult` tipo per un elenco di valori possibili.
>
>

### <a name="full-example"></a>Esempio completo
Di seguito, è riportato un esempio completo sull'integrazione:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Risolvere i conflitti del delegato UNUserNotificationCenter

*Se né l'applicazione né una delle librerie di terze parti implementa il valore `UNUserNotificationCenterDelegate`, è possibile ignorare questa parte.*

Oggetto `UNUserNotificationCenter` delegato viene utilizzato da hello SDK toomonitor hello del ciclo di vita di notifiche di Engagement nei dispositivi che eseguono in iOS, 10 o versione successiva. Hello SDK è un'implementazione personalizzata di hello `UNUserNotificationCenterDelegate` protocollo ma può essere presente solo una `UNUserNotificationCenter` delegato per ogni applicazione. Aggiunta di un altro delegato toohello `UNUserNotificationCenter` oggetto è in conflitto con hello Engagement uno. Se hello SDK rileva delegato l'o eventuali altre terze parti non viene utilizzata la propria implementazione toogive è una possibilità tooresolve hello è in conflitto. Sarà necessario tooadd hello Engagement logica tooyour proprietari di conflitti di hello tooresolve delegato in ordine.

Esistono due modi tooachieve questo.

Proposta di 1, semplicemente inoltrando il delegato chiama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Proposta 2, ereditando dalla hello o `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> È possibile determinare se una notifica proviene da Engagement o meno, il passaggio relativo `userInfo` toohello dizionario agente `isEngagementPushPayload:` metodo della classe.

Verificare che tale hello `UNUserNotificationCenter` delegato dell'oggetto è impostato il delegato tooyour all'interno di uno hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` metodo del delegato di applicazione.
Ad esempio, se è implementato hello sopra proposta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Come le campagne toocustomize
### <a name="notifications"></a>Notifiche
Esistono due tipi di notifiche: quelle di sistema e quelle in-app.

Le notifiche di sistema vengono gestite da iOS e non possono essere personalizzate.

Le notifiche in-app sono costituite da una vista che viene aggiunto in modo dinamico toohello finestra dell'applicazione corrente. Si tratta di una sovrimpressione di notifica. Sovrapposizioni di notifica sono ideali per un'integrazione veloce perché non richiedono si toomodify qualsiasi visualizzazione nell'applicazione.

#### <a name="layout"></a>Layout
aspetto di hello toomodify delle notifiche nell'applicazione, è sufficiente modificare file hello `AENotificationView.xib` tooyour deve, purché si mantenere i valori di tag hello e tipi di sottoviste esistente hello.

Per impostazione predefinita, nell'applicazione vengono visualizzate in basso hello hello. Se si preferisce toodisplay li nella parte superiore di hello della schermata, hello modifica fornita `AENotificationView.xib` e modificare hello `AutoSizing` proprietà di visualizzazione principale di hello in modo possono essere mantenuto nella parte superiore di hello della relativa superview.

#### <a name="categories"></a>Categorie
Quando si modifica hello fornito layout, modificare aspetto hello di tutte le notifiche. Le categorie consentono toodefine che vari destinazione Cerca (possibilmente comportamenti) per le notifiche. Quando si crea una campagna Reach, è possibile specificare una categoria. Tenere presente che le categorie consentono di personalizzare annunci e sondaggi, come descritto successivamente nel documento.

tooregister un gestore di categoria per le notifiche, è necessario tooadd viene inizializzata una chiamata una volta hello raggiungere modulo.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`deve essere un'istanza di un oggetto conforme al protocollo toohello `AENotifier`.

È possibile implementare i metodi di protocollo hello personalmente o è possibile scegliere una classe esistente di hello tooreimplement `AEDefaultNotifier` che già esegue la maggior parte del lavoro hello.

Ad esempio, se si desidera visualizzazione di notifiche hello tooredefine per una categoria specifica, è possibile seguire questo esempio:

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

In questo semplice esempio di categoria si presuppone che nel pacchetto dell'applicazione sia presente un file denominato `MyNotificationView.xib` . Se il metodo hello non è in grado di toofind corrispondente `.xib`, non verrà visualizzata la notifica hello ed Engagement creerà un messaggio nella console di hello.

Hello fornito nib file deve rispettare hello seguenti regole:

* Deve includere soltanto una visualizzazione.
* Sottoviste devono essere di hello stesso tipi hello quelle all'interno di hello fornito nib file denominato`AENotificationView.xib`
* Sottoviste devono avere stesso tag come quelle all'interno di hello fornito nib file denominato hello hello`AENotificationView.xib`

> [!TIP]
> È sufficiente copiare i file nib hello fornito, denominato `AENotificationView.xib`e iniziare a utilizzarla da qui. Ma fare attenzione, hello visualizzazione all'interno di questo file nib è associata la classe toohello `AENotificationView`. Questa classe ridefinito metodo hello `layoutSubViews` toomove e ridimensionare i sottoviste in base toocontext. È possibile tooreplace con un `UIView` o una classe di visualizzazione personalizzata.
>
>

Se è necessario personalizzare più approfondita delle notifiche (se si desidera ad esempio tooload nella visualizzazione direttamente dal codice hello), è consigliabile tootake un'occhiata hello fornita documentazione di classe e codice sorgente di `Protocol ReferencesDefaultNotifier` e `AENotifier`.

Si noti che è possibile utilizzare hello stesso notifica per più categorie.

È possibile notifica predefinito anche ridefinito hello simile al seguente:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Gestione delle notifiche
Quando si utilizza categoria predefinita hello, alcuni metodi del ciclo di vita vengono chiamati in hello `AEReachContent` tooreport stato campagna hello statistiche e l'aggiornamento dell'oggetto:

* Verrà visualizzata la notifica hello nell'applicazione, hello `displayNotification` metodo viene chiamato (che indica le statistiche) da `AEReachModule` se `handleNotification:` restituisce `YES`.
* Se la notifica hello viene ignorata, hello `exitNotification` metodo viene chiamato, viene segnalata statistica e campagne successiva ora possono essere elaborate.
* Se si fa clic notifica hello, `actionNotification` viene chiamato, viene restituita statistica e viene eseguita l'azione di hello associata.

Se l'implementazione di `AENotifier` bypass hello comportamento predefinito, è necessario toocall questi metodi del ciclo di vita da soli. Hello seguono esempi vengono illustrati alcuni casi in cui viene ignorato il comportamento predefinito di hello:

* Il metodo `AEDefaultNotifier` non è stato esteso, ad esempio la gestione delle categorie è stata implementata da zero.
* Overrode `prepareNotificationView:forContent:`, toomap che almeno `onNotificationActioned` o `onNotificationExited` tooone dei controlli U.I.

> [!WARNING]
> Se `handleNotification:` genera un'eccezione, hello contenuto viene eliminato e `drop` viene chiamato, tale condizione viene segnalata nelle statistiche e campagne successiva ora possono essere elaborate.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Includere la notifica come parte di una visualizzazione esistente
Le sovrimpressioni rappresentano un metodo ottimale per eseguire integrazioni rapide; talvolta, però, non sono convenienti e possono produrre effetti collaterali indesiderati.

Se non si è soddisfatti del sistema di sovrapposizione hello in alcune visualizzazioni, è possibile personalizzarlo per queste viste.

È possibile decidere il layout di notifica tooinclude nelle visualizzazioni esistenti. toodo in tal caso, è due stili di implementazione:

1. Aggiungi visualizzazione notifiche hello utilizzando Generatore di interfaccia

   * Aprire lo *strumento di creazione delle interfacce*
   * Inserire un 320 x 60 (o 768 x 60 se si utilizza iPad) `UIView` in cui si desidera hello notifica tooappear
   * Impostare il valore di Tag hello per questa vista troppo: **36822491**
2. Aggiungi visualizzazione notifiche hello a livello di codice. È sufficiente aggiungere codice dopo la visualizzazione è stata inizializzata hello:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

La macro `NOTIFICATION_AREA_VIEW_TAG` è disponibile in `AEDefaultNotifier.h`.

> [!NOTE]
> notifica predefinito Hello rileva automaticamente che notifica il layout hello è incluso in questa vista e non verrà aggiunto un overlay relativo.
>
>

### <a name="announcements-and-polls"></a>Annunci e sondaggi
#### <a name="layouts"></a>Layout
È possibile modificare il file hello `AEDefaultAnnouncementView.xib` e `AEDefaultPollView.xib` come mantenere i valori di tag hello e tipi di sottoviste esistente hello.

#### <a name="categories"></a>Categorie
##### <a name="alternate-layouts"></a>Layout alternativi
Come le notifiche, la categoria della campagna hello può essere utilizzato toohave layout alternativi per gli annunci e viene eseguito il polling.

toocreate una categoria per un annuncio, è necessario estendere **AEAnnouncementViewController** ed effettuare la registrazione una volta inizializzata modulo reach hello:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Ogni volta che un utente farà clic su una notifica per un annuncio con la categoria di hello "my\_categoria", il controller di visualizzazione registrati (in questo caso `MyCustomAnnouncementViewController`) verrà inizializzato chiamando il metodo hello `initWithAnnouncement:` e Visualizza hello è aggiunta toohello finestra dell'applicazione corrente.
>
>

Nell'implementazione di hello `AEAnnouncementViewController` classe si disporrà di proprietà hello tooread `announcement` tooinitialize i sottoviste. Prendere in considerazione hello esempio riportato di seguito, in cui due etichette vengono inizializzate utilizzando `title` e `body` le proprietà di hello `AEReachAnnouncement` classe:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Se non si desidera tooload visualizzazioni da soli ma si desidera layout visualizzazione annuncio di tooreuse hello predefinito, puoi semplicemente far il controller di visualizzazione personalizzato estende la classe hello fornito `AEDefaultAnnouncementViewController`. In tal caso, duplicato file nib hello `AEDefaultAnnouncementView.xib` e rinominarlo in modo può essere caricato da controller di visualizzazione personalizzata (per un controller denominato `CustomAnnouncementViewController`, è necessario chiamare il file nib `CustomAnnouncementView.xib`).

categoria di tooreplace hello predefinita di annunci, semplicemente registrare il controller di visualizzazione personalizzata per categoria hello definita in `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Esegue il polling può essere personalizzata hello allo stesso modo:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Questa volta, hello fornito `MyCustomPollViewController` deve estendere `AEPollViewController`. Oppure è possibile scegliere tooextend dal controller predefinito hello: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Non dimenticare di toocall `action` (`submitAnswers:` per i controller di visualizzazione personalizzata di polling) o `exit` metodo prima di controller di hello visualizzazione viene ignorata. In caso contrario, le statistiche non verranno inviate (vale a dire non analitica nella campagna hello) e altre campagne importante successiva non verranno notificate fino a quando non viene riavviato il processo di applicazione hello.
>
>

##### <a name="implementation-example"></a>Esempio di implementazione
In questa implementazione visualizzazione personalizzata di annuncio hello viene caricato da un file esterno XI.

Ad esempio per la personalizzazione avanzata notifica, è consigliabile toolook al codice sorgente hello dell'implementazione standard di hello.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
