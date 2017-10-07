---
title: aaaAzure iOS Mobile Engagement SDK aggiornare Procedure | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedure di aggiornamento
Se è già stata integrata una versione precedente di Engagement all'interno dell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

Per ogni nuova versione di hello SDK è necessario sostituire (rimuovere e importare di nuovo in xcode) hello cartelle EngagementSDK ed EngagementReach.

## <a name="from-300-too400"></a>Da 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 è obbligatoria a partire dalla versione 4.0.0 di hello SDK.

> [!NOTE]
> Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). È presente un bug noto nel modulo reach hello di questa versione di precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono prese in considerazione. toofix questo sarà necessario tooimplement hello obsoleto API `application:didReceiveRemoteNotification:` nell'app, delegato come indicato di seguito:
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata. È necessario passare tooXCode 8 appena possibile.
> 
> 

### <a name="usernotifications-framework"></a>Framework di UserNotifications
È necessario tooadd hello `UserNotifications` framework le fasi di compilazione.

in project explorer di hello, aprire il riquadro di progetto e selezionare la destinazione corretta hello. Aprire quindi hello **"Fasi di compilazione"** scheda in hello **"Binario con librerie di collegamento"** menu, aggiungere framework `UserNotifications.framework` -collegamento hello set come`Optional`

### <a name="application-push-capability"></a>Funzionalità di push dell'applicazione
XCode 8 può reimpostare l'app push capacità,. ricontrollarlo in hello `capability` scheda la destinazione selezionata.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Aggiungere hello nuovo iOS 10 registrazione Cod
Hello precedente codice frammento tooregister app hello toonotifications funziona comunque ma usa le API deprecate durante l'esecuzione in iOS 10.

Hello importazione `User Notification` framework:

        #import <UserNotifications/UserNotifications.h> 

Nel metodo `application:didFinishLaunchingWithOptions` del delegato dell'applicazione sostituire:

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

con:

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

## <a name="from-200-too300"></a>Da 2.0.0 too3.0.0
Eliminazione del supporto per iOS 4.X. A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 6.

Se si utilizza portata dell'applicazione, è necessario aggiungere `remote-notification` toohello valore `UIBackgroundModes` matrice nel file Info. plist nelle notifiche di ordine tooreceive remoto.

metodo Hello `application:didReceiveRemoteNotification:` deve toobe sostituito `application:didReceiveRemoteNotification:fetchCompletionHandler:` nel delegato dell'applicazione.

"AEPushDelegate.h" è deprecata e interfaccia necessario tooremove tutti i riferimenti. Ciò include la rimozione `[[EngagementAgent shared] setPushDelegate:self]` e delegare i metodi dal delegato dell'applicazione hello:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>Da 1.16.0 too2.0.0
Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement.
Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.16 quindi applicare hello seguente procedura.

> [!IMPORTANT]
> Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client. Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement
> 
> 

### <a name="agent"></a>Agente
metodo Hello `registerApp:` è stato sostituito dal nuovo metodo hello `init:`. È necessario aggiornare il delegato dell'applicazione di conseguenza e usare la stringa di connessione:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Rilevamento SmartAd è stato rimosso dal SDK, è sufficiente tooremove tutte le istanze di `AETrackModule` classe

### <a name="class-name-changes"></a>Modifiche del nome della classe
Come parte di hello rebranding, esistono alcuni nomi di classe o il file che devono toobe modificato.

A tutte le classi con prefisso "CP" viene assegnato quello "AE".

Esempio:

* `CPModule.h`è stato rinominato troppo`AEModule.h`.

Tutte le classi con prefisso "Capptain" vengono rinominate con il prefisso "Engagement".

Esempi:

* classe Hello `CapptainAgent` viene rinominato troppo`EngagementAgent`.
* classe Hello `CapptainTableViewController` viene rinominato troppo`EngagementTableViewController`.
* classe Hello `CapptainUtils` viene rinominato troppo`EngagementUtils`.
* classe Hello `CapptainViewController` viene rinominato troppo`EngagementViewController`.

