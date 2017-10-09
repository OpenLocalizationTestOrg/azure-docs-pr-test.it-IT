---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="ce438-103">Come tooIntegrate Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="ce438-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce438-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="ce438-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="ce438-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ce438-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ce438-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ce438-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ce438-107">Android</span><span class="sxs-lookup"><span data-stu-id="ce438-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="ce438-108">Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e funzioni in un'applicazione Android di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="ce438-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce438-109">L'API di Android SDK deve essere almeno di livello 10 o superiore (Android 2.3.3 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="ce438-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="ce438-110">Hello seguendo i passaggi è che sufficienti tooactivates hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals.</span><span class="sxs-lookup"><span data-stu-id="ce438-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="ce438-111">Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API in Android](mobile-engagement-android-use-engagement-api.md) poiché questi le statistiche sono dipende dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="ce438-112">Incorporare il progetto Android hello Engagement SDK e servizio</span><span class="sxs-lookup"><span data-stu-id="ce438-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="ce438-113">Download hello Android SDK da [qui](https://aka.ms/vq9mfn) ottenere `mobile-engagement-VERSION.jar` e inserirli in hello `libs` cartella del progetto Android (se non esiste ancora, creare cartelle di librerie hello).</span><span class="sxs-lookup"><span data-stu-id="ce438-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce438-114">Se si compila il pacchetto dell'applicazione con ProGuard, è necessario tookeep alcune classi.</span><span class="sxs-lookup"><span data-stu-id="ce438-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="ce438-115">È possibile utilizzare hello seguente frammento di configurazione:</span><span class="sxs-lookup"><span data-stu-id="ce438-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="ce438-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="ce438-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="ce438-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="ce438-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="ce438-118">Specificare la stringa di connessione Engagement, hello chiamata seguente metodo in attività di avvio hello:</span><span class="sxs-lookup"><span data-stu-id="ce438-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ce438-119">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce438-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="ce438-120">Se presente, aggiungere queste autorizzazioni Android hello (prima hello `<application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ce438-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="ce438-121">Aggiungere hello successiva sezione (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ce438-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="ce438-122">Modifica `<Your application name>` dal nome dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="ce438-123">Hello `android:label` attributo consente un nome hello toochoose di hello servizio Engagement come verrà visualizzato agli utenti finali toohello nella schermata di "Servizi in esecuzione" hello del telefono.</span><span class="sxs-lookup"><span data-stu-id="ce438-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="ce438-124">È consigliabile tooset questo attributo troppo`"<Your application name>Service"` (ad esempio `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="ce438-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="ce438-125">Se si specifica hello `android:process` attributo assicura che il servizio di Engagement hello verrà eseguito nel proprio processo (Engagement in esecuzione nella stessa procedura adottata applicazione renderà il thread principale o dell'interfaccia utente potenzialmente tempi hello).</span><span class="sxs-lookup"><span data-stu-id="ce438-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="ce438-126">Inserire nel codice `Application.onCreate()` e per tutti i processi dell'applicazione, incluso hello Engagement servizio verranno eseguiti altri i callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="ce438-127">Potrebbe avere effetti indesiderati (ad esempio, le allocazioni di memoria non necessari e i thread nel processo di Engagement hello, ricevitori broadcast duplicati o servizi).</span><span class="sxs-lookup"><span data-stu-id="ce438-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="ce438-128">Se esegue l'override `Application.onCreate()`, hello tooadd consigliato seguente all'inizio di hello del frammento di codice è il `Application.onCreate()` funzione:</span><span class="sxs-lookup"><span data-stu-id="ce438-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="ce438-129">È possibile eseguire hello stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="ce438-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="ce438-130">È anche possibile estendere `EngagementApplication` anziché estensione `Application`: hello callback `Application.onCreate()` hello controllo processo e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente hello è non hello uno hello Engagement servizio di hosting, hello stesse regole valide per Hello altre richiamate.</span><span class="sxs-lookup"><span data-stu-id="ce438-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="ce438-131">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="ce438-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="ce438-132">Metodo consigliato: eseguire l'overload delle classi `Activity`</span><span class="sxs-lookup"><span data-stu-id="ce438-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="ce438-133">Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, è sufficiente toomake tutti i `*Activity` sottoclassi ereditano hello corrispondente `Engagement*Activity` classi (ad esempio, se l'attività legacy estende `ListActivity`, assicurarsi che estende `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="ce438-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="ce438-134">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="ce438-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="ce438-135">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="ce438-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="ce438-136">Quando si utilizza `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate troppo`requestWindowFeature(...);` diventa troppo prima chiamata hello`super.onCreate(...);`, in caso contrario si verificherà un arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="ce438-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="ce438-137">È possibile trovare queste classi in hello `src` cartella e possono copiare nel progetto.</span><span class="sxs-lookup"><span data-stu-id="ce438-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="ce438-138">classi di Hello sono anche in hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="ce438-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="ce438-139">Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="ce438-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="ce438-140">Se non è possibile o non si desidera toooverload il `Activity` classi, è invece possibile iniziare e terminare le attività chiamando `EngagementAgent`del diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="ce438-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce438-141">Hello, Android SDK non chiama mai hello `endActivity()` (metodo), anche quando viene chiusa l'applicazione hello (in Android, chiudere le applicazioni sono in realtà non).</span><span class="sxs-lookup"><span data-stu-id="ce438-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="ce438-142">È pertanto *elevata* consigliato hello toocall `startActivity()` metodo hello `onResume` callback di *tutti* le attività e hello `endActivity()` metodo hello `onPause()` callback di *tutti* delle attività.</span><span class="sxs-lookup"><span data-stu-id="ce438-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="ce438-143">Si tratta di hello solo modo toobe assicurarsi che le sessioni non andrà perso.</span><span class="sxs-lookup"><span data-stu-id="ce438-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="ce438-144">Se una sessione viene perso, hello servizio Engagement mai disconnessa dal back-end Engagement hello (dal momento che il servizio di hello rimane connesso, purché una sessione è in sospeso).</span><span class="sxs-lookup"><span data-stu-id="ce438-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="ce438-145">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="ce438-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="ce438-146">Questo toohello molto simili di esempio `EngagementActivity` classe e le sue varianti, il cui codice sorgente viene fornito in hello `src` cartella.</span><span class="sxs-lookup"><span data-stu-id="ce438-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="ce438-147">Test</span><span class="sxs-lookup"><span data-stu-id="ce438-147">Test</span></span>
<span data-ttu-id="ce438-148">Esegue l'app per dispositivi mobili in un emulatore o un dispositivo e verificando che registra una sessione nella scheda Monitoraggio hello ora. verificare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="ce438-149">Nelle sezioni successive di Hello sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="ce438-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="ce438-150">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="ce438-150">Location reporting</span></span>
<span data-ttu-id="ce438-151">Se si desidera toobe percorsi segnalato, è necessario tooadd poche righe di configurazione (tra hello `<application>` e `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="ce438-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="ce438-152">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="ce438-152">Lazy area location reporting</span></span>
<span data-ttu-id="ce438-153">Segnalazione differita della posizione consente paese hello tooreport, area e località associata toodevices.</span><span class="sxs-lookup"><span data-stu-id="ce438-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="ce438-154">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="ce438-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="ce438-155">area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="ce438-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="ce438-156">Hello GPS non viene mai utilizzato e, pertanto questo tipo di report di percorso include solo poche (non toosay alcun) impatto sulla batteria hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="ce438-157">Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori.</span><span class="sxs-lookup"><span data-stu-id="ce438-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="ce438-158">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="ce438-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="ce438-159">percorso area lazy tooenable reporting, è possibile farlo tramite configurazione hello indicato in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ce438-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ce438-160">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="ce438-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="ce438-161">Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="ce438-162">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="ce438-162">Real time location reporting</span></span>
<span data-ttu-id="ce438-163">La segnalazione della posizione in tempo reale consente tooreport hello latitudine e la longitudine associata toodevices.</span><span class="sxs-lookup"><span data-stu-id="ce438-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="ce438-164">Per impostazione predefinita, questo tipo di segnalazione della posizione Usa solo i percorsi di rete (basati su ID di cella o Wi-Fi) e reporting hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="ce438-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="ce438-165">I percorsi in tempo reale sono *non* utilizzato toocompute statistiche.</span><span class="sxs-lookup"><span data-stu-id="ce438-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="ce438-166">Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.</span><span class="sxs-lookup"><span data-stu-id="ce438-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="ce438-167">posizione in tempo reale tooenable reporting, è possibile farlo tramite configurazione hello indicato in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ce438-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ce438-168">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="ce438-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="ce438-169">Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="ce438-170">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="ce438-170">GPS based reporting</span></span>
<span data-ttu-id="ce438-171">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="ce438-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="ce438-172">Utilizzare hello tooenable di GPS basato su percorsi, che sono molto più precise, usare l'oggetto configurazione hello:</span><span class="sxs-lookup"><span data-stu-id="ce438-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ce438-173">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="ce438-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="ce438-174">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="ce438-174">Background reporting</span></span>
<span data-ttu-id="ce438-175">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="ce438-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="ce438-176">reporting hello tooenable anche in background, usare hello configurazione oggetto:</span><span class="sxs-lookup"><span data-stu-id="ce438-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="ce438-177">Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete di base, anche se è abilitata hello GPS.</span><span class="sxs-lookup"><span data-stu-id="ce438-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="ce438-178">report sulla posizione background Hello verrà arrestata se utente hello viene riavviato il dispositivo, è possibile aggiungere questo toomake riavviato automaticamente in fase di avvio:</span><span class="sxs-lookup"><span data-stu-id="ce438-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="ce438-179">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="ce438-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="ce438-180">Autorizzazioni Android M</span><span class="sxs-lookup"><span data-stu-id="ce438-180">Android M permissions</span></span>
<span data-ttu-id="ce438-181">A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ce438-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="ce438-182">le autorizzazioni di runtime Hello verranno disattivate per impostazione predefinita per le nuove installazioni di app se la destinazione è il livello di API Android 23.</span><span class="sxs-lookup"><span data-stu-id="ce438-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="ce438-183">In caso contrario verranno attivate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ce438-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="ce438-184">utente Hello può abilitare o disabilitare le autorizzazioni dal menu di impostazioni dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="ce438-185">La disattivazione di autorizzazioni dal menu di sistema di processi in background di un'applicazione hello termina, questo è un comportamento del sistema e non influisce sulla possibilità tooreceive push in background.</span><span class="sxs-lookup"><span data-stu-id="ce438-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="ce438-186">Nel contesto di hello di Mobile Engagement, le autorizzazioni di hello che richiedono l'approvazione in fase di esecuzione sono:</span><span class="sxs-lookup"><span data-stu-id="ce438-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="ce438-187">`WRITE_EXTERNAL_STORAGE` (solo quando la destinazione è il livello 23 dell’API Android)</span><span class="sxs-lookup"><span data-stu-id="ce438-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="ce438-188">archiviazione esterna Hello viene utilizzato solo per funzionalità quadro generale di copertura.</span><span class="sxs-lookup"><span data-stu-id="ce438-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="ce438-189">Se si trova chiedere agli utenti di questo toobe autorizzazione arresto improvviso, è possibile rimuoverlo se è stato utilizzato solo per Engagement Mobile, ma al costo di hello di disabilitare la funzionalità quadro generale.</span><span class="sxs-lookup"><span data-stu-id="ce438-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="ce438-190">Per le funzionalità di percorso hello, è necessario richiedere autorizzazioni toouser utilizzando una finestra di dialogo di sistema standard.</span><span class="sxs-lookup"><span data-stu-id="ce438-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="ce438-191">Se l'utente hello Approva, è necessario tootell ``EngagementAgent`` tootake che modificano in considerazione in tempo reale (modifica hello in caso contrario verrà elaborato successivo ora hello utente avvia hello un'applicazione hello).</span><span class="sxs-lookup"><span data-stu-id="ce438-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="ce438-192">Ecco un toouse di esempio di codice in un'attività, delle autorizzazioni per l'applicazione toorequest e portare avanti hello se positivo troppo``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="ce438-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="ce438-193">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="ce438-193">Advanced reporting</span></span>
<span data-ttu-id="ce438-194">Facoltativamente, se si desidera tooreport eventi specifici di applicazione, gli errori e i processi, è necessario toouse hello API Engagement tramite i metodi di hello di hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="ce438-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="ce438-195">Un oggetto di questa classe può essere recuperati dal chiamante hello `EngagementAgent.getInstance()` metodo statico.</span><span class="sxs-lookup"><span data-stu-id="ce438-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="ce438-196">Consente tutte le funzionalità avanzate di Engagement toouse Hello Engagement API e dettagliato in hello come tooUse l'API di Engagement in Android (nonché in documentazione tecnica di hello di hello `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="ce438-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="ce438-197">Configurazione avanzata (in AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="ce438-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="ce438-198">Wakelocking</span><span class="sxs-lookup"><span data-stu-id="ce438-198">Wake locks</span></span>
<span data-ttu-id="ce438-199">Se si desidera assicurarsi che le statistiche vengono inviate in tempo reale quando si utilizza Wi-Fi o se viene disattivata il schermata Ciao toobe, aggiungere hello autorizzazione facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ce438-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="ce438-200">Segnalazione di arresto anomalo </span><span class="sxs-lookup"><span data-stu-id="ce438-200">Crash report</span></span>
<span data-ttu-id="ce438-201">Se si desidera toodisable segnalazioni di arresti anomali, aggiungere questo (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ce438-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="ce438-202">Soglia del burst</span><span class="sxs-lookup"><span data-stu-id="ce438-202">Burst threshold</span></span>
<span data-ttu-id="ce438-203">Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ce438-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="ce438-204">Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="ce438-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="ce438-205">In tal caso, aggiungere questo toodo (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ce438-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="ce438-206">Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile).</span><span class="sxs-lookup"><span data-stu-id="ce438-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="ce438-207">È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="ce438-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="ce438-208">Timeout della sessione</span><span class="sxs-lookup"><span data-stu-id="ce438-208">Session timeout</span></span>
<span data-ttu-id="ce438-209">Per impostazione predefinita, una sessione è terminata 10s dopo la fine di hello della propria attività ultima (che in genere si verifica da premendo hello Home o eseguire il backup di chiave, tramite telefono di hello impostazione inattivo o passare a un'altra applicazione).</span><span class="sxs-lookup"><span data-stu-id="ce438-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="ce438-210">Si tratta di tooavoid una divisione di sessione, ogni utente hello in fase di uscire e tornare rapidamente applicazione toohello (che può verificarsi quando ha prelevati da un'immagine, verificare una notifica e così via.).</span><span class="sxs-lookup"><span data-stu-id="ce438-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="ce438-211">È opportuno toomodify questo parametro.</span><span class="sxs-lookup"><span data-stu-id="ce438-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="ce438-212">In tal caso, aggiungere questo toodo (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ce438-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="ce438-213">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="ce438-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="ce438-214">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="ce438-214">Using a method call</span></span>
<span data-ttu-id="ce438-215">Se si desidera toostop Engagement l'invio di log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="ce438-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="ce438-216">Questa chiamata è persistente: usa un file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="ce438-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="ce438-217">Se Engagement è attivo quando si chiama questa funzione, può richiedere un minuto per hello servizio toostop.</span><span class="sxs-lookup"><span data-stu-id="ce438-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="ce438-218">Tuttavia, non verrà avviato servizio hello hello tutti successivo avvio di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="ce438-219">È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `true`.</span><span class="sxs-lookup"><span data-stu-id="ce438-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="ce438-220">Integrazione nella propria classe `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="ce438-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="ce438-221">Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.</span><span class="sxs-lookup"><span data-stu-id="ce438-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="ce438-222">È possibile configurare le preferenze di file (con modalità desiderata di hello) toouse di Engagement in hello `AndroidManifest.xml` file con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="ce438-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="ce438-223">Hello `engagement:agent:settings:name` chiave è utilizzata toodefine hello nome del file di preferenze condivise hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="ce438-224">Hello `engagement:agent:settings:mode` chiave è la modalità di hello toodefine utilizzate del file di preferenze condivise hello, è necessario utilizzare hello modalità stesso come il `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="ce438-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="ce438-225">modalità Hello deve essere passata come un numero: se si utilizza una combinazione di flag costante nel codice, controllare il valore totale di hello.</span><span class="sxs-lookup"><span data-stu-id="ce438-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="ce438-226">Engagement sempre utilizzare hello `engagement:key` booleano chiave all'interno di file di preferenze hello per la gestione di questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="ce438-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="ce438-227">Hello in seguito ad esempio `AndroidManifest.xml` Mostra hello valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ce438-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="ce438-228">È quindi possibile aggiungere un `CheckBoxPreference` nel layout delle preferenze come segue quello hello:</span><span class="sxs-lookup"><span data-stu-id="ce438-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
