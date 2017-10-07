---
title: aaaAzure iOS Mobile Engagement SDK integrazione | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Come tooIntegrate Engagement in iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e funzioni nell'applicazione iOS di monitoraggio.

Hello Engagement SDK richiede + IOS 7 e 8 + Xcode: destinazione di distribuzione hello dell'applicazione deve essere almeno iOS 7.

> [!NOTE]
> Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). È presente un bug noto nel modulo Reach hello di questa versione di precedente durante l'esecuzione su dispositivi iOS, 10, vedere [hello integrazione modulo reach](mobile-engagement-ios-integrate-engagement-reach.md) per altri dettagli. Se si sceglie toouse hello SDK v3.2.4, ignorare hello `UserNotifications.framework` importare nel passaggio successivo hello.
>
>

Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals. Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API nell'app iOS](mobile-engagement-ios-use-engagement-api.md) poiché queste statistiche dipendono dall'applicazione.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Incorporare hello Engagement SDK nel progetto iOS
* Scaricare hello iOS SDK da [qui](http://aka.ms/qk2rnj).
* Progetto di componente hello Engagement SDK tooyour iOS: in Xcode, fare clic sul progetto e selezionare **"aggiungere file troppo..."** scegliere hello `EngagementSDK` cartella.
* Engagement richiede ulteriori Framework toowork: in project explorer di hello, aprire il riquadro di progetto e selezionare hello destinazione corretta. Aprire quindi hello **"Fasi di compilazione"** scheda in hello **"Binario con librerie di collegamento"** menu, aggiungere questi Framework:

  * `UserNotifications.framework`-Imposta hello collegamento come`Optional`
  * `AdSupport.framework`-Imposta hello collegamento come`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> framework AdSupport Hello può essere rimosso. Engagement deve hello di toocollect IDFA questo framework. Tuttavia, può essere disabilitata la raccolta IDFA \<ios-sdk-engagement-idfa\> toocomply con hello nuovo Apple politica di questo ID.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Inizializzare hello Engagement SDK
È necessario toomodify al delegato dell'applicazione:

* Nella parte superiore di hello del file di implementazione, importare agente Engagement hello:

      [...]
      #import "EngagementAgent.h"
* Inizializzare Engagement all'interno di metodo hello '**applicationDidFinishLaunching:**'o'**application: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Segnalazione di base
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Metodo consigliato: eseguire l'overload delle classi `UIViewController`
Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `UIViewController` sottoclassi ereditano hello `EngagementViewController` classi (stessa regola per `UITableViewController`  - \> `EngagementTableViewController`).

**Senza Engagement:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Con Engagement:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Metodo alternativo: chiamare `startActivity()` manualmente
Se non è possibile o non si desidera toooverload il `UIViewController` classi, invece, è possibile avviare le attività chiamando `EngagementAgent`del diretta dei metodi.

> [!IMPORTANT]
> Hello iOS SDK chiama automaticamente hello `endActivity()` metodo quando un'applicazione hello viene chiuso. È pertanto *elevata* consigliato hello toocall `startActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo*mai* chiamata hello `endActivity` (metodo), dopo la chiamata di questo metodo impone Hello toobe corrente della sessione è terminata.
>
>

## <a name="location-reporting"></a>Segnalazione della posizione
Condizioni Apple del servizio non consentono alle applicazioni toouse rilevamento solo a scopo di statistiche del percorso. Di conseguenza, è consigliabile tooenable percorso report solo se l'applicazione utilizza anche per altri motivi di rilevamento del percorso hello.

A partire da iOS 8, è necessario fornire una descrizione per la modalità l'app Usa i servizi di posizione impostando una stringa per la chiave hello [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription]nel file Info. plist dell'app. Se si desidera che il percorso di tooreport in background hello Engagement, aggiungere la chiave di hello NSLocationAlwaysUsageDescription. In tutti gli altri casi, aggiungere la chiave hello NSLocationWhenInUseUsageDescription. Si noti che è necessario NSLocationAlwaysAndWhenInUseUsageDescription sia NSLocationWhenInUseUsageDescription tooreport background percorso iOS 11.

### <a name="lazy-area-location-reporting"></a>Segnalazione differita della posizione
Segnalazione differita della posizione consente paese hello tooreport, area e località associata toodevices. Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi. area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione. Hello GPS non viene mai utilizzato e, pertanto questo tipo di report di percorso include solo poche (non toosay alcun) impatto sulla batteria hello.

Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori. Possono essere usate anche come criteri nelle campagne Reach. Hello noto ultima area segnalato per un dispositivo può essere recuperato grazie toohello [API dispositivo].

percorso di area lazy tooenable reporting, aggiungere hello successiva riga dopo l'inizializzazione hello Engagement agente:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Segnalazione della posizione in tempo reale
La segnalazione della posizione in tempo reale consente tooreport hello latitudine e la longitudine associata toodevices. Per impostazione predefinita, questo tipo di segnalazione della posizione Usa solo i percorsi di rete (basati su ID di cella o Wi-Fi) e reporting hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).

I percorsi in tempo reale sono *non* utilizzato toocompute statistiche. Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.

posizione in tempo reale tooenable reporting, aggiungere hello successiva riga dopo l'inizializzazione hello Engagement agente:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Segnalazione basata su GPS
Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete. utilizzo di hello tooenable di GPS basato su percorsi, che sono molto più precise, aggiungere:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Segnalazione in background
Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione). hello tooenable reporting anche in background, aggiungere:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete di base, anche se è abilitata hello GPS.
>
>

Implementazione di questa funzione chiamerà [startMonitoringSignificantLocationChanges] quando l'applicazione passa in background hello. Tenere presente che verrà automaticamente riavvia l'applicazione in background hello se arriva un nuovo evento.

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, se si desidera tooreport eventi specifici di applicazione, gli errori e i processi, è necessario toouse hello API Engagement tramite i metodi di hello di hello `EngagementAgent` classe. Un oggetto di questa classe può essere recuperato da chiamata hello `[EngagementAgent shared]` metodo statico.

Consente tutte le funzionalità avanzate di Engagement toouse Hello Engagement API e dettagliato in hello come tooUse l'API di Engagement in iOS (nonché in documentazione tecnica di hello di hello `EngagementAgent` classe).

## <a name="disable-idfa-collection"></a>Disabilitare la raccolta IDFA
Per impostazione predefinita, Engagement utilizzerà hello [IDFA] toouniquely identificare un utente. Tuttavia, se non si usa la pubblicità altrove nell'applicazione hello, potrebbe essere rifiutato da hello il processo di revisione di App Store. Può essere disabilitata la raccolta IDFA aggiungendo macro del preprocessore hello `ENGAGEMENT_DISABLE_IDFA` nel file pch (o in hello `Build Settings` dell'applicazione). In questo modo che non sia presente alcun riferimento troppo`ASIdentifierManager`, `advertisingIdentifier` o `isAdvertisingTrackingEnabled` nella compilazione dell'applicazione hello.

Integrazione di hello **prefix.pch** file:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

È possibile verificare che la raccolta IDFA hello correttamente è disabilitata nell'applicazione controllando i log dei test di Engagement hello. Vedere hello Test di integrazione\<ios-sdk-engagement-test-idfa\> documentazione per ulteriori informazioni.

## <a name="disable-log-reporting"></a>Disabilitare la segnalazione di log
### <a name="using-a-method-call"></a>Uso di una chiamata del metodo
Se si desidera toostop Engagement l'invio di log, è possibile chiamare:

    [[EngagementAgent shared] setEnabled:NO];

Questa chiamata è permanente: Usa `NSUserDefaults` informazioni hello toostore.

È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `YES`.

### <a name="integration-in-your-settings-bundle"></a>Integrazione nel bundle di impostazioni
Anziché chiamare questa funzione, è possibile integrare questa impostazione direttamente nel file `Settings.bundle` esistente. stringa Hello `engagement_agent_enabled` deve essere utilizzata come un identificatore di preferenza hello e deve essere associato tooa interruttore (`PSToggleSwitchSpecifier`).

Hello in seguito ad esempio `Settings.bundle` viene illustrato come tooimplement è:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[API dispositivo]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
