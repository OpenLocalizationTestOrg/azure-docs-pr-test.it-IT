---
title: Integrazione di Azure Mobile Engagement SDK per iOS | Documentazione Microsoft
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
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="c9aa2-103">Come integrare Engagement in iOS</span><span class="sxs-lookup"><span data-stu-id="c9aa2-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9aa2-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c9aa2-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="c9aa2-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c9aa2-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="c9aa2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c9aa2-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="c9aa2-107">Android</span><span class="sxs-lookup"><span data-stu-id="c9aa2-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="c9aa2-108">Questa procedura descrive il modo più semplice per attivare le funzioni di analisi e monitoraggio di Engagement in un'applicazione per iOS.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="c9aa2-109">L'Engagement SDK richiede iOS7 o versione successiva e XCode 8: la destinazione della distribuzione dell'applicazione deve essere almeno iOS 7.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="c9aa2-110">Se si dipende davvero da XCode 7, è possibile usare [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="c9aa2-111">Esiste un bug noto nel modulo di copertura di questa precedente versione che si verifica durante l'esecuzione sui dispositivi iOS 10. Per altri dettagli, vedere [l'integrazione del modulo di copertura](mobile-engagement-ios-integrate-engagement-reach.md).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="c9aa2-112">Se si sceglie di utilizzare l'SDK v3.2.4, ignorare l'importazione di `UserNotifications.framework` nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="c9aa2-113">I passaggi seguenti sono sufficienti per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="c9aa2-114">La segnalazione dei log necessari per calcolare altre statistiche quali eventi, errori e processi deve essere eseguita manualmente mediante l'API di Engagement. Vedere [Come usare l'API di Engagement in iOS](mobile-engagement-ios-use-engagement-api.md) poiché queste statistiche dipendono dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="c9aa2-115">Incorporare l'SDK di Engagement nel progetto iOS</span><span class="sxs-lookup"><span data-stu-id="c9aa2-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="c9aa2-116">Scaricare l’SDK per iOS da [qui](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="c9aa2-117">Aggiungere Engagement SDK nel progetto iOS: in Xcode fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **"Add files to ..."** (Aggiungi file a) e infine selezionare la cartella `EngagementSDK`.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="c9aa2-118">Per il funzionamento di Engagement sono necessari framework aggiuntivi: nell'area di esplorazione dei progetti aprire il riquadro del progetto, quindi selezionare la destinazione corretta.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="c9aa2-119">Aprire la scheda **Build Phases** (Crea fasi) e nel menu **Link Binary With Libraries** (Collega binario con librerie) aggiungere i framework come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="c9aa2-120">`UserNotifications.framework`: impostare il collegamento come `Optional`</span><span class="sxs-lookup"><span data-stu-id="c9aa2-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="c9aa2-121">`AdSupport.framework`: impostare il collegamento come `Optional`</span><span class="sxs-lookup"><span data-stu-id="c9aa2-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="c9aa2-122">È possibile rimuovere il framework AdSupport.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="c9aa2-123">Engagement necessita di questo framework per raccogliere l'identificatore IDFA (Identifier for Advertising).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="c9aa2-124">È tuttavia possibile disabilitare la raccolta di identificatori IDFA \<ios-sdk-engagement-idfa\> per conformarsi ai nuovi criteri Apple relativi a questo ID.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="c9aa2-125">Inizializzare Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="c9aa2-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="c9aa2-126">È necessario modificare il delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="c9aa2-127">Nella parte superiore del file di implementazione importare l'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="c9aa2-128">Inizializzare Engagement all'interno del metodo '**applicationDidFinishLaunching:**' o '**application:didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="c9aa2-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="c9aa2-129">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="c9aa2-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="c9aa2-130">Metodo consigliato: eseguire l'overload delle classi `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="c9aa2-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="c9aa2-131">Per attivare la segnalazione di tutti i log richiesti da Engagement per il calcolo delle statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici, è sufficiente fare in modo che tutte le sottoclassi `UIViewController` ereditino dalle classi `EngagementViewController` (stessa regola per `UITableViewController` -\> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="c9aa2-132">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c9aa2-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="c9aa2-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c9aa2-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="c9aa2-134">Metodo alternativo: chiamare `startActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="c9aa2-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="c9aa2-135">Se non si può o non si vuole eseguire l'overload delle classi `UIViewController`, è possibile avviare le attività chiamando direttamente i metodi di `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9aa2-136">iOS SDK chiama automaticamente il metodo `endActivity()` quando viene chiusa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="c9aa2-137">Di conseguenza, è *CONSIGLIABILE* chiamare il metodo `startActivity` ogni volta che l'attività dell'utente cambia e non chiamare *MAI* il metodo `endActivity` poiché questo metodo forza la chiusura della sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="c9aa2-138">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="c9aa2-138">Location reporting</span></span>
<span data-ttu-id="c9aa2-139">Le condizioni del servizio Apple non permettono alle applicazioni di usare la verifica della posizione per scopi puramente statistici.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="c9aa2-140">È quindi consigliabile abilitare la segnalazione della posizione solo se l'applicazione usa la verifica della posizione anche per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="c9aa2-141">A partire da iOS 8, è necessario fornire una descrizione dell'uso dei servizi di posizione da parte dell'app, impostando una stringa per la chiave [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription] nel file Info.plist dell'app.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="c9aa2-142">Se si vuole segnalare la posizione in background con Engagement, aggiungere la chiave NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="c9aa2-143">In tutti gli altri casi, aggiungere la chiave NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="c9aa2-144">Si noti che sono necessari sia NSLocationAlwaysAndWhenInUseUsageDescription sia NSLocationWhenInUseUsageDescription per indicare il percorso in background in iOS 11.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="c9aa2-145">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="c9aa2-145">Lazy area location reporting</span></span>
<span data-ttu-id="c9aa2-146">La segnalazione differita della posizione consente di segnalare il paese, l'area geografica e la località associati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="c9aa2-147">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="c9aa2-148">L'area del dispositivo viene segnalata al massimo una volta per sessione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="c9aa2-149">Il GPS non viene mai usato, per cui l'impatto di questo tipo di segnalazione della posizione sulla batteria è minimo, se non addirittura nullo.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="c9aa2-150">Le aree segnalate vengono usate per calcolare statistiche geografiche relative a utenti, sessioni, eventi ed errori.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="c9aa2-151">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="c9aa2-152">L'ultima area conosciuta segnalata per un dispositivo può essere recuperata grazie all' [API del dispositivo].</span><span class="sxs-lookup"><span data-stu-id="c9aa2-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="c9aa2-153">Per abilitare la segnalazione differita della posizione, aggiungere la riga seguente dopo l'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="c9aa2-154">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="c9aa2-154">Real time location reporting</span></span>
<span data-ttu-id="c9aa2-155">La segnalazione della posizione in tempo reale consente di segnalare la latitudine e la longitudine associate ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="c9aa2-156">Per impostazione predefinita, la segnalazione differita della posizione usa solo posizioni di rete (in base all'ID di cella o alla connessione Wi-Fi) ed è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="c9aa2-157">Le posizioni in tempo reale *NON* sono usate per calcolare dati statistici.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="c9aa2-158">L'unico scopo è consentire l'uso del criterio di definizione del recinto virtuale in tempo reale \<Reach-Audience-geofencing\> nelle campagne di copertura.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="c9aa2-159">Per abilitare la segnalazione della posizione in tempo reale, aggiungere la riga seguente dopo l'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="c9aa2-160">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="c9aa2-160">GPS based reporting</span></span>
<span data-ttu-id="c9aa2-161">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="c9aa2-162">Per abilitare l'uso di posizioni basate su GPS (che sono molto più precise), aggiungere:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="c9aa2-163">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="c9aa2-163">Background reporting</span></span>
<span data-ttu-id="c9aa2-164">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="c9aa2-165">Per abilitare la segnalazione anche in background, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="c9aa2-166">Quando l'applicazione viene eseguita in background, vengono segnalate solo le posizioni basate sulla rete, anche se è abilitato il GPS.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="c9aa2-167">Se si implementa questa funzione, viene chiamato [startMonitoringSignificantLocationChanges] quando l'applicazione passa in background.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="c9aa2-168">Si noti che l'applicazione verrà riavviata automaticamente in background in caso di arrivo di un nuovo evento relativo alla posizione.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="c9aa2-169">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="c9aa2-169">Advanced reporting</span></span>
<span data-ttu-id="c9aa2-170">Facoltativamente, per segnalare eventi, errori e processi specifici dell'applicazione, è necessario usare l'API di Engagement mediante i metodi della classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="c9aa2-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="c9aa2-171">Un oggetto di questa classe può essere recuperato chiamando il metodo statico `[EngagementAgent shared]` .</span><span class="sxs-lookup"><span data-stu-id="c9aa2-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="c9aa2-172">L'API di Engagement consente di usare tutte le funzionalità avanzate di Engagement ed è descritta in dettaglio nell'argomento dedicato all'uso dell'API in iOS, oltre che nella documentazione tecnica relativa alla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="c9aa2-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="c9aa2-173">Disabilitare la raccolta IDFA</span><span class="sxs-lookup"><span data-stu-id="c9aa2-173">Disable IDFA collection</span></span>
<span data-ttu-id="c9aa2-174">Per impostazione predefinita, Engagement usa l'identificatore [IDFA] per identificare un utente in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="c9aa2-175">Se però si usano annunci pubblicitari altrove nell'app, è possibile che l'app venga respinta dal processo di verifica di App Store.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="c9aa2-176">La raccolta IDFA può essere disabilitata mediante l'aggiunta della macro del preprocessore `ENGAGEMENT_DISABLE_IDFA` nel file con estensione pch (o nella sezione `Build Settings` dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="c9aa2-177">In questo modo è possibile assicurarsi che la build dell'applicazione non includa riferimenti a `ASIdentifierManager`, `advertisingIdentifier` o `isAdvertisingTrackingEnabled`.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="c9aa2-178">Integrazione nel file **prefix.pch** :</span><span class="sxs-lookup"><span data-stu-id="c9aa2-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="c9aa2-179">È possibile verificare la corretta disabilitazione della raccolta IDFA nell'applicazione controllando i log di test di Engagement.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="c9aa2-180">Per altre informazioni, vedere la documentazione sul test di integrazione \<ios-sdk-engagement-test-idfa\>.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="c9aa2-181">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="c9aa2-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="c9aa2-182">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="c9aa2-182">Using a method call</span></span>
<span data-ttu-id="c9aa2-183">Se si vuole che Engagement non invii più log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="c9aa2-184">Questa chiamata è persistente: usa `NSUserDefaults` per archiviare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="c9aa2-185">È possibile abilitare di nuovo la segnalazione di log chiamando la stessa funzione con `YES`.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="c9aa2-186">Integrazione nel bundle di impostazioni</span><span class="sxs-lookup"><span data-stu-id="c9aa2-186">Integration in your settings bundle</span></span>
<span data-ttu-id="c9aa2-187">Anziché chiamare questa funzione, è possibile integrare questa impostazione direttamente nel file `Settings.bundle` esistente.</span><span class="sxs-lookup"><span data-stu-id="c9aa2-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="c9aa2-188">La stringa `engagement_agent_enabled` deve essere usata come identificatore di preferenze e deve essere associata a un'opzione di attivazione/disattivazione (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="c9aa2-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="c9aa2-189">L'esempio seguente di `Settings.bundle` mostra come implementarla:</span><span class="sxs-lookup"><span data-stu-id="c9aa2-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

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
<span data-ttu-id="c9aa2-190">[API del dispositivo]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="c9aa2-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="c9aa2-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="c9aa2-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="c9aa2-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="c9aa2-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="c9aa2-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="c9aa2-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="c9aa2-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="c9aa2-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
