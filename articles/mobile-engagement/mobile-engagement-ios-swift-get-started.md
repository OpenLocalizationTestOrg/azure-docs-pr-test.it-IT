---
title: aaaGet avviato con Azure Mobile Engagement per iOS in Swift | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App iOS.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Introduzione a Azure Mobile Engagement per app per iOS in Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push applicazione notifiche di toosegmented utenti tooan iOS.
In questa esercitazione si creerà un'app per iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).

Questa esercitazione richiede il seguente hello:

* XCode 8, che è possibile installare da MAC App Store
* Hello [iOS Mobile Engagement SDK]
* Certificato per notifiche push (.p12) che è possibile ottenere nell'Apple Dev Center.

> [!NOTE]
> Questa esercitazione usa Swift versione 3.0. 
> 
> 

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Mobile Engagement relative ad app per iOS.

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push. la documentazione completa integrazione Hello è reperibile in hello [integrazione SDK iOS di Mobile Engagement](mobile-engagement-ios-sdk-overview.md)

Verrà creata un'applicazione di base con l'integrazione di XCode toodemonstrate hello:

### <a name="create-a-new-ios-project"></a>Creare un nuovo progetto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Scaricare hello [iOS Mobile Engagement SDK]
2. Estrarre hello. gz file tooa cartella computer
3. Fare clic con il pulsante destro progetto hello e selezionare "Aggiungi file troppo..."
   
    ![][1]
4. Esplorazione delle cartelle toohello in cui è stato estratto hello SDK e seleziona hello `EngagementSDK` cartella, quindi premere OK.
   
    ![][2]
5. Aprire hello `Build Phases` scheda in hello `Link Binary With Libraries` menu aggiungere il framework di hello, come illustrato di seguito:
   
    ![][3]
6. Creare un Bridging intestazione toobe toouse in grado di hello dell'obiettivo C API SDK, scegliere File > Nuovo > File > iOS > origine > File di intestazione.
   
    ![][4]
7. Modifica hello bridging intestazione file tooexpose Mobile Engagement Objective-C tooyour Swift codice, aggiungere hello importazioni seguenti:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. In impostazioni di compilazione, assicurarsi che hello Objective-C Bridging intestazione impostazione nel compilatore Swift - la generazione del codice di compilazione include un'intestazione di toothis percorso. Di seguito è riportato un esempio di percorso: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (a seconda del percorso hello)**
   
   ![][6]
9. Tornare indietro toohello portale di Azure dell'app *le informazioni di connessione* pagina e copia hello stringa di connessione
   
   ![][5]
10. A questo punto incollare la stringa di connessione hello in hello `didFinishLaunchingWithOptions` delegato
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Abilitazione del monitoraggio in tempo reale
In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).

1. Aprire hello **ViewController.swift** file e sostituire la classe base hello di **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitazione delle notifiche push e della messaggistica in-app
Engagement mobile permette di toointeract e con gli utenti con le notifiche Push e la messaggistica In-app nel contesto di hello delle campagne. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti installerà il tooreceive app li.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Abilitare il tooreceive app invisibile all'utente le notifiche Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Aggiungi progetto di hello Reach libreria tooyour
1. Fare clic con il pulsante destro del mouse sul progetto.
2. Selezionare `Add file too...`.
3. Esplorazione delle cartelle toohello in cui è stato estratto hello SDK
4. Seleziona hello `EngagementReach` cartella
5. Fare clic su Aggiungi.
6. Modificare hello bridging intestazioni di copertura di Mobile Engagement Objective-C intestazione file tooexpose e aggiungere hello importazioni seguenti:
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>Modificare il delegato dell'applicazione
1. Inside hello `didFinishLaunchingWithOptions` : creare un modulo di copertura e passarlo tooyour linea Engagement inizializzazione:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Abilitare il tooreceive app le notifiche Push APNS
1. Aggiungere i seguenti toohello riga hello `didFinishLaunchingWithOptions` metodo:
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Aggiungere hello `didRegisterForRemoteNotificationsWithDeviceToken` metodo come indicato di seguito:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Aggiungere hello `didReceiveRemoteNotification:fetchCompletionHandler:` metodo come indicato di seguito:
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
