---
title: aaaGet avviato con Azure Mobile Engagement per iOS in Objective C | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app iOS.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Introduzione a Azure Mobile Engagement per app per iOS in Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push applicazione notifiche di toosegmented utenti tooan iOS.
In questa esercitazione si creerà un'app per iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).

Questa esercitazione richiede il seguente hello:

* XCode 8, che è possibile installare da MAC App Store
* Hello [iOS Mobile Engagement SDK]

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Mobile Engagement relative ad app per iOS.

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push. la documentazione completa integrazione Hello è reperibile in hello [integrazione SDK iOS di Mobile Engagement](mobile-engagement-ios-sdk-overview.md)

Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate XCode.

### <a name="create-a-new-ios-project"></a>Creare un nuovo progetto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>La connessione back-end Mobile Engagement toohello app
1. Scaricare hello [iOS Mobile Engagement SDK].
2. Estrarre hello. cartella di tooa GZ file nel computer.
3. Fare clic sul progetto hello e quindi selezionare **aggiungere file al**.

    ![][1]
4. Passare toohello cartella in cui è stato estratto hello SDK, selezionare hello `EngagementSDK` cartella, fare clic su **opzioni** hello angolo inferiore sinistro e assicurarsi che tale casella di controllo di hello **copiare gli elementi, se necessario** e hello casella di controllo per la destinazione siano selezionate, quindi premere **OK**.

    ![][2]
5. Aprire hello **Build Phases** scheda hello in **binario con librerie di collegamento** menu, aggiungere il framework di hello, come illustrato di seguito:

    ![][3]
6. Tornare indietro toohello portale di Azure dell'app **le informazioni di connessione** pagina e copia la stringa di connessione hello.

    ![][4]
7. Hello successiva riga di codice aggiungere il **appdelegate. M** file.

        #import "EngagementAgent.h"
8. A questo punto incollare la stringa di connessione hello in hello `didFinishLaunchingWithOptions` delegato.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`è un'istruzione facoltativa che consente di abilitare i registri SDK a tooidentify problemi.

## <a id="monitor"></a>Abilitare il monitoraggio in tempo reale
In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).

1. Aprire hello **ViewController.h** file e importare **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Questo punto, sostituire superclassi hello di hello **ViewController** interfaccia da `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti impostarle backup tooreceive l'app.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Abilitare il tooreceive app invisibile all'utente le notifiche Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Aggiungi progetto di hello Reach libreria tooyour
1. Fare clic con il pulsante destro sul progetto.
2. Selezionare **Aggiungi file**.
3. Passare toohello cartella in cui è stato estratto hello SDK.
4. Seleziona hello `EngagementReach` cartella.
5. Fare clic su **Aggiungi**.

### <a name="modify-your-application-delegate"></a>Modificare il delegato dell'applicazione
1. In **AppDeletegate.m** file, importare il modulo di copertura di Engagement hello.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Inside hello `application:didFinishLaunchingWithOptions` (metodo), creare un modulo di Reach e passarlo tooyour linea Engagement inizializzazione:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Abilitare il tooreceive app le notifiche Push APNS
1. Aggiungere i seguenti toohello riga hello `application:didFinishLaunchingWithOptions` metodo:

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
2. Aggiungere hello `application:didRegisterForRemoteNotificationsWithDeviceToken` metodo come indicato di seguito:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Aggiungere hello `didFailToRegisterForRemoteNotificationsWithError` metodo come indicato di seguito:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Aggiungere hello `didReceiveRemoteNotification:fetchCompletionHandler` metodo come indicato di seguito:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
