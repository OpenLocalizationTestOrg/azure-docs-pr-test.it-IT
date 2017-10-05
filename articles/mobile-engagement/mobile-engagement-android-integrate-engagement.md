---
title: Integrazione di Android SDK per Azure Mobile Engagement
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="9ca04-103">Come integrare Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="9ca04-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ca04-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="9ca04-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="9ca04-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="9ca04-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="9ca04-106">iOS</span><span class="sxs-lookup"><span data-stu-id="9ca04-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="9ca04-107">Android</span><span class="sxs-lookup"><span data-stu-id="9ca04-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="9ca04-108">Questa procedura descrive il modo più semplice per attivare le funzioni di analisi e monitoraggio di Engagement in un'applicazione per Android.</span><span class="sxs-lookup"><span data-stu-id="9ca04-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ca04-109">L'API di Android SDK deve essere almeno di livello 10 o superiore (Android 2.3.3 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="9ca04-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="9ca04-110">I passaggi seguenti sono sufficienti per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici.</span><span class="sxs-lookup"><span data-stu-id="9ca04-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="9ca04-111">La segnalazione dei log necessari per calcolare altre statistiche quali eventi, errori e processi deve essere eseguita manualmente mediante l'API di Engagement (vedere [Come usare l'API di Engagement in Android](mobile-engagement-android-use-engagement-api.md) ) poiché queste statistiche dipendono dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="9ca04-112">Incorporare il servizio ed Engagement SDK nel progetto Android</span><span class="sxs-lookup"><span data-stu-id="9ca04-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="9ca04-113">Android SDK è disponibile [qui`libs` per il download. Ottenere il file ](https://aka.ms/vq9mfn) e inserirlo nella cartella `mobile-engagement-VERSION.jar` del progetto Android. Creare la cartella libs, se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="9ca04-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ca04-114">Se si compila il pacchetto dell'applicazione con ProGuard, è necessario mantenere alcune classi.</span><span class="sxs-lookup"><span data-stu-id="9ca04-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="9ca04-115">È possibile usare il frammento di codice di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca04-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="9ca04-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="9ca04-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="9ca04-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="9ca04-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="9ca04-118">Specificare la stringa di connessione a Engagement chiamando il metodo seguente nell'attività dell'utilità di avvio:</span><span class="sxs-lookup"><span data-stu-id="9ca04-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="9ca04-119">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca04-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="9ca04-120">Aggiungere le autorizzazioni Android seguenti, se mancanti, prima del tag `<application>`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="9ca04-121">Aggiungere la sezione seguente tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="9ca04-122">Al posto di `<Your application name>` specificare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="9ca04-123">La chiave `android:label` consente di scegliere il nome del servizio Engagement così come verrà presentato agli utenti finali nella schermata dei servizi in esecuzione sul telefono.</span><span class="sxs-lookup"><span data-stu-id="9ca04-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="9ca04-124">È consigliabile impostare questo attributo su `"<Your application name>Service"`, ad esempio `"AcmeFunGameService"`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="9ca04-125">Se si specifica l'attributo `android:process` , il servizio Engagement verrà eseguito nel relativo processo (l'esecuzione di Engagement nello stesso processo dell'applicazione può ridurre la reattività del thread principale o dell'interfaccia utente).</span><span class="sxs-lookup"><span data-stu-id="9ca04-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="9ca04-126">Il codice inserito in `Application.onCreate()` e altri callback dell'applicazione verrà eseguito per tutti i processi dell'applicazione, incluso il servizio Engagement.</span><span class="sxs-lookup"><span data-stu-id="9ca04-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="9ca04-127">È possibile che si verifichino effetti collaterali indesiderati, ad esempio allocazioni di memoria e thread superflui nel processo di Engagement oppure ricevitori o servizi di trasmissione duplicati.</span><span class="sxs-lookup"><span data-stu-id="9ca04-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="9ca04-128">Se si esegue l'override di `Application.onCreate()`, è consigliabile aggiungere il frammento di codice seguente all'inizio della funzione `Application.onCreate()`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="9ca04-129">È possibile eseguire la stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="9ca04-130">È anche possibile estendere `EngagementApplication` anziché `Application`: il callback esegue il controllo del processo `Application.onCreate()` e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente non è quello che ospita il servizio Engagement. Per gli altri callback vengono applicate le stesse regole.</span><span class="sxs-lookup"><span data-stu-id="9ca04-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="9ca04-131">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="9ca04-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="9ca04-132">Metodo consigliato: eseguire l'overload delle classi `Activity`</span><span class="sxs-lookup"><span data-stu-id="9ca04-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="9ca04-133">Per attivare la segnalazione di tutti i log richiesti da Engagement per il calcolo delle statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici, è sufficiente fare in modo che tutte le sottoclassi `*Activity` ereditino dalle classi `Engagement*Activity` corrispondenti. Ad esempio, se l'attività legacy estende `ListActivity`, fare in modo che estenda `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="9ca04-134">**Senza Engagement:**</span><span class="sxs-lookup"><span data-stu-id="9ca04-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="9ca04-135">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="9ca04-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="9ca04-136">Quando si usa `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate a `requestWindowFeature(...);` vengano eseguite prima della chiamata a `super.onCreate(...);`. In caso contrario, si verificherà un arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9ca04-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="9ca04-137">Queste classi sono incluse nella cartella `src` e possono essere copiate nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9ca04-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="9ca04-138">Sono reperibili anche in **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="9ca04-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="9ca04-139">Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="9ca04-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="9ca04-140">Se non si può o non si vuole eseguire l'overload delle classi `Activity`, è possibile avviare e terminare le attività chiamando direttamente i metodi di `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ca04-141">Android SDK non chiama mai il metodo `endActivity()`, neanche alla chiusura dell'applicazione (in Android le applicazioni in realtà non vengono mai chiuse).</span><span class="sxs-lookup"><span data-stu-id="9ca04-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="9ca04-142">Per questo motivo, è *ALTAMENTE* consigliabile chiamare il metodo `startActivity()` nel callback `onResume` di *TUTTE* le attività e il metodo `endActivity()` nel callback `onPause()` di *TUTTE* le attività.</span><span class="sxs-lookup"><span data-stu-id="9ca04-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="9ca04-143">È l'unico modo per evitare la perdita di sessioni.</span><span class="sxs-lookup"><span data-stu-id="9ca04-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="9ca04-144">In caso di perdita di una sessione, il servizio Engagement non si disconnetterà mai dal back-end di Engagement, dato che il servizio rimane connesso fintanto che una sessione è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="9ca04-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="9ca04-145">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="9ca04-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="9ca04-146">Questo esempio è molto simile alla classe `EngagementActivity` e alle relative varianti, il cui codice di origine è disponibile nella cartella `src`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="9ca04-147">Test</span><span class="sxs-lookup"><span data-stu-id="9ca04-147">Test</span></span>
<span data-ttu-id="9ca04-148">Verificare ora l'integrazione, eseguendo l'app per dispositivi mobili in un emulatore o in un dispositivo e verificando che registri una sessione nella scheda Monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="9ca04-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="9ca04-149">Le sezioni successive sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="9ca04-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="9ca04-150">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="9ca04-150">Location reporting</span></span>
<span data-ttu-id="9ca04-151">Per fare in modo che le posizioni vengano segnalate, è necessario aggiungere alcune righe di configurazione tra i tag `<application>` e `</application>`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="9ca04-152">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="9ca04-152">Lazy area location reporting</span></span>
<span data-ttu-id="9ca04-153">La segnalazione differita della posizione consente di segnalare il paese, l'area geografica e la località associati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9ca04-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="9ca04-154">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="9ca04-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="9ca04-155">L'area del dispositivo viene segnalata al massimo una volta per sessione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="9ca04-156">Il GPS non viene mai usato, per cui l'impatto di questo tipo di segnalazione della posizione sulla batteria è minimo, se non addirittura nullo.</span><span class="sxs-lookup"><span data-stu-id="9ca04-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="9ca04-157">Le aree segnalate vengono usate per calcolare statistiche geografiche relative a utenti, sessioni, eventi ed errori.</span><span class="sxs-lookup"><span data-stu-id="9ca04-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="9ca04-158">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="9ca04-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="9ca04-159">Per abilitare la segnalazione differita della posizione, è possibile utilizzare la configurazione descritta in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9ca04-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="9ca04-160">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="9ca04-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="9ca04-161">Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="9ca04-162">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9ca04-162">Real time location reporting</span></span>
<span data-ttu-id="9ca04-163">La segnalazione della posizione in tempo reale consente di segnalare la latitudine e la longitudine associate ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9ca04-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="9ca04-164">Per impostazione predefinita, la segnalazione differita della posizione usa solo posizioni di rete (in base all'ID di cella o alla connessione Wi-Fi) ed è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="9ca04-165">Le posizioni in tempo reale *NON* sono usate per calcolare dati statistici.</span><span class="sxs-lookup"><span data-stu-id="9ca04-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="9ca04-166">L'unico scopo è consentire l'uso del criterio di definizione del recinto virtuale in tempo reale \<Reach-Audience-geofencing\> nelle campagne di copertura.</span><span class="sxs-lookup"><span data-stu-id="9ca04-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="9ca04-167">Per abilitare la segnalazione della posizione in tempo reale, è possibile utilizzare la configurazione descritta in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9ca04-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="9ca04-168">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="9ca04-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="9ca04-169">Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="9ca04-170">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="9ca04-170">GPS based reporting</span></span>
<span data-ttu-id="9ca04-171">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="9ca04-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="9ca04-172">Per abilitare l'uso di posizioni basate su GPS (che sono molto più precise), utilizzare l’oggetto di configurazione:</span><span class="sxs-lookup"><span data-stu-id="9ca04-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="9ca04-173">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="9ca04-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="9ca04-174">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="9ca04-174">Background reporting</span></span>
<span data-ttu-id="9ca04-175">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="9ca04-176">Per abilitare la segnalazione anche in background, utilizzare l’oggetto di configurazione:</span><span class="sxs-lookup"><span data-stu-id="9ca04-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="9ca04-177">Quando l'applicazione viene eseguita in background, vengono segnalate solo le posizioni basate sulla rete, anche se è abilitato il GPS.</span><span class="sxs-lookup"><span data-stu-id="9ca04-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="9ca04-178">La segnalazione della posizione in background verrà arrestata se l'utente riavvia il dispositivo. Per fare in modo che venga riavviata automaticamente al riavvio, aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="9ca04-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="9ca04-179">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="9ca04-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="9ca04-180">Autorizzazioni Android M</span><span class="sxs-lookup"><span data-stu-id="9ca04-180">Android M permissions</span></span>
<span data-ttu-id="9ca04-181">A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9ca04-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="9ca04-182">Le autorizzazioni di runtime verranno disattivate per impostazione predefinita per le installazioni di nuove app se la destinazione è il livello 23 dell’API Android.</span><span class="sxs-lookup"><span data-stu-id="9ca04-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="9ca04-183">In caso contrario verranno attivate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9ca04-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="9ca04-184">L'utente può abilitare o disabilitare le autorizzazioni dal menu delle impostazioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9ca04-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="9ca04-185">La disattivazione delle autorizzazioni dal menu di sistema elimina i processi in background dell'applicazione; si tratta di un comportamento del sistema e non influisce sulla possibilità di ricevere push in background.</span><span class="sxs-lookup"><span data-stu-id="9ca04-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="9ca04-186">Nel contesto di Mobile Engagement, le autorizzazioni che richiedono l'approvazione al runtime sono:</span><span class="sxs-lookup"><span data-stu-id="9ca04-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="9ca04-187">`WRITE_EXTERNAL_STORAGE` (solo quando la destinazione è il livello 23 dell’API Android)</span><span class="sxs-lookup"><span data-stu-id="9ca04-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="9ca04-188">L’archiviazione esterna viene utilizzata solo per la funzionalità della panoramica generale Reach.</span><span class="sxs-lookup"><span data-stu-id="9ca04-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="9ca04-189">Se si ritiene che richiedere agli utenti questa autorizzazione sia problematico, è possibile rimuoverla se è stata utilizzata solo per Mobile Engagement, ma comporta la disattivazione delle funzionalità della panoramica generale.</span><span class="sxs-lookup"><span data-stu-id="9ca04-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="9ca04-190">Per le funzionalità del percorso, è necessario richiedere le autorizzazioni all'utente tramite una finestra di dialogo di sistema standard.</span><span class="sxs-lookup"><span data-stu-id="9ca04-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="9ca04-191">Se l'utente approva, è necessario specificare ``EngagementAgent`` per tenere in considerazione la modifica in tempo reale (in caso contrario la modifica verrà elaborata la volta successiva che l'utente avvia l'applicazione).</span><span class="sxs-lookup"><span data-stu-id="9ca04-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="9ca04-192">Ecco un esempio di codice da utilizzare in un'attività dell'applicazione per richiedere autorizzazioni e inoltrare il risultato, se positivo, a ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="9ca04-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="9ca04-193">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="9ca04-193">Advanced reporting</span></span>
<span data-ttu-id="9ca04-194">Facoltativamente, per segnalare eventi, errori e processi specifici dell'applicazione, è necessario usare l'API di Engagement mediante i metodi della classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="9ca04-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="9ca04-195">Un oggetto di questa classe può essere recuperato chiamando il metodo statico `EngagementAgent.getInstance()` .</span><span class="sxs-lookup"><span data-stu-id="9ca04-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="9ca04-196">L'API di Engagement consente di usare tutte le funzionalità avanzate di Engagement ed è descritta in dettaglio nell'argomento dedicato all'uso dell'API in Android, oltre che nella documentazione tecnica relativa alla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="9ca04-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="9ca04-197">Configurazione avanzata (in AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="9ca04-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="9ca04-198">Wakelocking</span><span class="sxs-lookup"><span data-stu-id="9ca04-198">Wake locks</span></span>
<span data-ttu-id="9ca04-199">Per assicurarsi che le statistiche vengano inviate in tempo reale quando si usa una connessione Wi-Fi o quando lo schermo è spento, aggiungere la seguente autorizzazione facoltativa:</span><span class="sxs-lookup"><span data-stu-id="9ca04-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="9ca04-200">Segnalazione di arresto anomalo </span><span class="sxs-lookup"><span data-stu-id="9ca04-200">Crash report</span></span>
<span data-ttu-id="9ca04-201">Per disabilitare la segnalazione di arresti anomali del sistema, aggiungere quanto segue tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="9ca04-202">Soglia del burst</span><span class="sxs-lookup"><span data-stu-id="9ca04-202">Burst threshold</span></span>
<span data-ttu-id="9ca04-203">Per impostazione predefinita, il servizio Engagement segnala i log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="9ca04-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="9ca04-204">Se l'applicazione segnala i log molto spesso, è preferibile memorizzare i log nel buffer e segnalarli tutti insieme con cadenza regolare (la cosiddetta "modalità burst").</span><span class="sxs-lookup"><span data-stu-id="9ca04-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="9ca04-205">A tale scopo, aggiungere quanto segue tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="9ca04-206">La modalità burst aumenta lievemente la durata della batteria ma ha un impatto su Monitor di Engagement: la durata di tutte le sessioni e di tutti i processi verrà arrotondata alla soglia di burst (di conseguenza, le sessioni e i processi inferiori alla soglia di burst potrebbero non essere visibili).</span><span class="sxs-lookup"><span data-stu-id="9ca04-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="9ca04-207">Si consiglia di usare una soglia di burst non maggiore di 30000 (30 secondi).</span><span class="sxs-lookup"><span data-stu-id="9ca04-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="9ca04-208">Timeout della sessione</span><span class="sxs-lookup"><span data-stu-id="9ca04-208">Session timeout</span></span>
<span data-ttu-id="9ca04-209">Per impostazione predefinita, una sessione viene terminata 10 secondi dopo la fine dell'ultima attività, che in genere si verifica premendo Home o Indietro, impostando l'inattività del telefono o passando a un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="9ca04-210">Questo avviene per evitare una divisione di sessione ogni volta che l'utente esce e rientra nell'applicazione molto rapidamente, come può accadere quando preleva un'immagine, controlla una notifica e così via.</span><span class="sxs-lookup"><span data-stu-id="9ca04-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="9ca04-211">Questo parametro può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="9ca04-211">You may want to modify this parameter.</span></span> <span data-ttu-id="9ca04-212">A tale scopo, aggiungere quanto segue tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="9ca04-213">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="9ca04-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="9ca04-214">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="9ca04-214">Using a method call</span></span>
<span data-ttu-id="9ca04-215">Se si vuole che Engagement non invii più log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="9ca04-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="9ca04-216">Questa chiamata è persistente: usa un file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="9ca04-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="9ca04-217">Se Engagement è attivo quando si chiama questa funzione, l'arresto del servizio può richiedere 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="9ca04-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="9ca04-218">Al successivo avvio dell'applicazione, tuttavia, il servizio non verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="9ca04-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="9ca04-219">È possibile abilitare di nuovo la segnalazione di log chiamando la stessa funzione con `true`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="9ca04-220">Integrazione nella propria classe `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="9ca04-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="9ca04-221">Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.</span><span class="sxs-lookup"><span data-stu-id="9ca04-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="9ca04-222">È possibile configurare Engagement in modo da usare il file di preferenze (con la modalità desiderata) nel file `AndroidManifest.xml` con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="9ca04-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="9ca04-223">La chiave `engagement:agent:settings:name` viene usata per definire il nome del file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="9ca04-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="9ca04-224">La chiave `engagement:agent:settings:mode` viene usata per definire la modalità del file di preferenze condivise. È consigliabile adottare la stessa modalità usata per `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="9ca04-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="9ca04-225">La modalità deve essere passata come numero: se si usa una combinazione di flag di costanti nel codice, controllare il valore totale.</span><span class="sxs-lookup"><span data-stu-id="9ca04-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="9ca04-226">Engagement usa sempre la chiave booleana `engagement:key` all'interno del file di preferenze per la gestione di questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="9ca04-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="9ca04-227">L'esempio seguente di `AndroidManifest.xml` mostra i valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9ca04-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="9ca04-228">Sarà quindi possibile aggiungere un elemento `CheckBoxPreference` nel layout delle preferenze simile a quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9ca04-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
