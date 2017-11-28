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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="0dbcf-103">Come tooIntegrate Engagement in iOS</span><span class="sxs-lookup"><span data-stu-id="0dbcf-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dbcf-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="0dbcf-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="0dbcf-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0dbcf-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="0dbcf-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0dbcf-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="0dbcf-107">Android</span><span class="sxs-lookup"><span data-stu-id="0dbcf-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="0dbcf-108">Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e funzioni nell'applicazione iOS di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="0dbcf-109">Hello Engagement SDK richiede + IOS 7 e 8 + Xcode: destinazione di distribuzione hello dell'applicazione deve essere almeno iOS 7.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="0dbcf-110">Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="0dbcf-111">È presente un bug noto nel modulo Reach hello di questa versione di precedente durante l'esecuzione su dispositivi iOS, 10, vedere [hello integrazione modulo reach](mobile-engagement-ios-integrate-engagement-reach.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="0dbcf-112">Se si sceglie toouse hello SDK v3.2.4, ignorare hello `UserNotifications.framework` importare nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="0dbcf-113">Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="0dbcf-114">Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API nell'app iOS](mobile-engagement-ios-use-engagement-api.md) poiché queste statistiche dipendono dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="0dbcf-115">Incorporare hello Engagement SDK nel progetto iOS</span><span class="sxs-lookup"><span data-stu-id="0dbcf-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="0dbcf-116">Scaricare hello iOS SDK da [qui](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="0dbcf-117">Progetto di componente hello Engagement SDK tooyour iOS: in Xcode, fare clic sul progetto e selezionare **"aggiungere file troppo..."** scegliere hello `EngagementSDK` cartella.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="0dbcf-118">Engagement richiede ulteriori Framework toowork: in project explorer di hello, aprire il riquadro di progetto e selezionare hello destinazione corretta.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="0dbcf-119">Aprire quindi hello **"Fasi di compilazione"** scheda in hello **"Binario con librerie di collegamento"** menu, aggiungere questi Framework:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="0dbcf-120">`UserNotifications.framework`-Imposta hello collegamento come`Optional`</span><span class="sxs-lookup"><span data-stu-id="0dbcf-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="0dbcf-121">`AdSupport.framework`-Imposta hello collegamento come`Optional`</span><span class="sxs-lookup"><span data-stu-id="0dbcf-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="0dbcf-122">framework AdSupport Hello può essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="0dbcf-123">Engagement deve hello di toocollect IDFA questo framework.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="0dbcf-124">Tuttavia, può essere disabilitata la raccolta IDFA \<ios-sdk-engagement-idfa\> toocomply con hello nuovo Apple politica di questo ID.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="0dbcf-125">Inizializzare hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="0dbcf-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="0dbcf-126">È necessario toomodify al delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="0dbcf-127">Nella parte superiore di hello del file di implementazione, importare agente Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="0dbcf-128">Inizializzare Engagement all'interno di metodo hello '**applicationDidFinishLaunching:**'o'**application: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="0dbcf-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="0dbcf-129">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="0dbcf-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="0dbcf-130">Metodo consigliato: eseguire l'overload delle classi `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="0dbcf-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="0dbcf-131">Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `UIViewController` sottoclassi ereditano hello `EngagementViewController` classi (stessa regola per `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="0dbcf-132">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0dbcf-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="0dbcf-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0dbcf-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="0dbcf-134">Metodo alternativo: chiamare `startActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="0dbcf-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="0dbcf-135">Se non è possibile o non si desidera toooverload il `UIViewController` classi, invece, è possibile avviare le attività chiamando `EngagementAgent`del diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dbcf-136">Hello iOS SDK chiama automaticamente hello `endActivity()` metodo quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="0dbcf-137">È pertanto *elevata* consigliato hello toocall `startActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo*mai* chiamata hello `endActivity` (metodo), dopo la chiamata di questo metodo impone Hello toobe corrente della sessione è terminata.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="0dbcf-138">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="0dbcf-138">Location reporting</span></span>
<span data-ttu-id="0dbcf-139">Condizioni Apple del servizio non consentono alle applicazioni toouse rilevamento solo a scopo di statistiche del percorso.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="0dbcf-140">Di conseguenza, è consigliabile tooenable percorso report solo se l'applicazione utilizza anche per altri motivi di rilevamento del percorso hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="0dbcf-141">A partire da iOS 8, è necessario fornire una descrizione per la modalità l'app Usa i servizi di posizione impostando una stringa per la chiave hello [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription]nel file Info. plist dell'app.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="0dbcf-142">Se si desidera che il percorso di tooreport in background hello Engagement, aggiungere la chiave di hello NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="0dbcf-143">In tutti gli altri casi, aggiungere la chiave hello NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="0dbcf-144">Si noti che è necessario NSLocationAlwaysAndWhenInUseUsageDescription sia NSLocationWhenInUseUsageDescription tooreport background percorso iOS 11.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="0dbcf-145">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="0dbcf-145">Lazy area location reporting</span></span>
<span data-ttu-id="0dbcf-146">Segnalazione differita della posizione consente paese hello tooreport, area e località associata toodevices.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="0dbcf-147">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="0dbcf-148">area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="0dbcf-149">Hello GPS non viene mai utilizzato e, pertanto questo tipo di report di percorso include solo poche (non toosay alcun) impatto sulla batteria hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="0dbcf-150">Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="0dbcf-151">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="0dbcf-152">Hello noto ultima area segnalato per un dispositivo può essere recuperato grazie toohello [API dispositivo].</span><span class="sxs-lookup"><span data-stu-id="0dbcf-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="0dbcf-153">percorso di area lazy tooenable reporting, aggiungere hello successiva riga dopo l'inizializzazione hello Engagement agente:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="0dbcf-154">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="0dbcf-154">Real time location reporting</span></span>
<span data-ttu-id="0dbcf-155">La segnalazione della posizione in tempo reale consente tooreport hello latitudine e la longitudine associata toodevices.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="0dbcf-156">Per impostazione predefinita, questo tipo di segnalazione della posizione Usa solo i percorsi di rete (basati su ID di cella o Wi-Fi) e reporting hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="0dbcf-157">I percorsi in tempo reale sono *non* utilizzato toocompute statistiche.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="0dbcf-158">Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="0dbcf-159">posizione in tempo reale tooenable reporting, aggiungere hello successiva riga dopo l'inizializzazione hello Engagement agente:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="0dbcf-160">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="0dbcf-160">GPS based reporting</span></span>
<span data-ttu-id="0dbcf-161">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="0dbcf-162">utilizzo di hello tooenable di GPS basato su percorsi, che sono molto più precise, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="0dbcf-163">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="0dbcf-163">Background reporting</span></span>
<span data-ttu-id="0dbcf-164">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="0dbcf-165">hello tooenable reporting anche in background, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="0dbcf-166">Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete di base, anche se è abilitata hello GPS.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="0dbcf-167">Implementazione di questa funzione chiamerà [startMonitoringSignificantLocationChanges] quando l'applicazione passa in background hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="0dbcf-168">Tenere presente che verrà automaticamente riavvia l'applicazione in background hello se arriva un nuovo evento.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="0dbcf-169">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="0dbcf-169">Advanced reporting</span></span>
<span data-ttu-id="0dbcf-170">Facoltativamente, se si desidera tooreport eventi specifici di applicazione, gli errori e i processi, è necessario toouse hello API Engagement tramite i metodi di hello di hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="0dbcf-171">Un oggetto di questa classe può essere recuperato da chiamata hello `[EngagementAgent shared]` metodo statico.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="0dbcf-172">Consente tutte le funzionalità avanzate di Engagement toouse Hello Engagement API e dettagliato in hello come tooUse l'API di Engagement in iOS (nonché in documentazione tecnica di hello di hello `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="0dbcf-173">Disabilitare la raccolta IDFA</span><span class="sxs-lookup"><span data-stu-id="0dbcf-173">Disable IDFA collection</span></span>
<span data-ttu-id="0dbcf-174">Per impostazione predefinita, Engagement utilizzerà hello [IDFA] toouniquely identificare un utente.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="0dbcf-175">Tuttavia, se non si usa la pubblicità altrove nell'applicazione hello, potrebbe essere rifiutato da hello il processo di revisione di App Store.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="0dbcf-176">Può essere disabilitata la raccolta IDFA aggiungendo macro del preprocessore hello `ENGAGEMENT_DISABLE_IDFA` nel file pch (o in hello `Build Settings` dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="0dbcf-177">In questo modo che non sia presente alcun riferimento troppo`ASIdentifierManager`, `advertisingIdentifier` o `isAdvertisingTrackingEnabled` nella compilazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="0dbcf-178">Integrazione di hello **prefix.pch** file:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="0dbcf-179">È possibile verificare che la raccolta IDFA hello correttamente è disabilitata nell'applicazione controllando i log dei test di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="0dbcf-180">Vedere hello Test di integrazione\<ios-sdk-engagement-test-idfa\> documentazione per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="0dbcf-181">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="0dbcf-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="0dbcf-182">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="0dbcf-182">Using a method call</span></span>
<span data-ttu-id="0dbcf-183">Se si desidera toostop Engagement l'invio di log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="0dbcf-184">Questa chiamata è permanente: Usa `NSUserDefaults` informazioni hello toostore.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="0dbcf-185">È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `YES`.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="0dbcf-186">Integrazione nel bundle di impostazioni</span><span class="sxs-lookup"><span data-stu-id="0dbcf-186">Integration in your settings bundle</span></span>
<span data-ttu-id="0dbcf-187">Anziché chiamare questa funzione, è possibile integrare questa impostazione direttamente nel file `Settings.bundle` esistente.</span><span class="sxs-lookup"><span data-stu-id="0dbcf-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="0dbcf-188">stringa Hello `engagement_agent_enabled` deve essere utilizzata come un identificatore di preferenza hello e deve essere associato tooa interruttore (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="0dbcf-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="0dbcf-189">Hello in seguito ad esempio `Settings.bundle` viene illustrato come tooimplement è:</span><span class="sxs-lookup"><span data-stu-id="0dbcf-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
