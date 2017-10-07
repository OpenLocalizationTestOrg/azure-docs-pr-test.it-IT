---
title: aaaLocation Reporting per Azure Mobile Engagement SDK Android
description: Viene descritto come percorso tooconfigure reporting per Azure Mobile Engagement SDK Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="58e50-103">Segnalazione della posizione per Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="58e50-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58e50-104">Android</span><span class="sxs-lookup"><span data-stu-id="58e50-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="58e50-105">Questo argomento viene descritto come percorso toodo reporting per l'applicazione di Android.</span><span class="sxs-lookup"><span data-stu-id="58e50-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58e50-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="58e50-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="58e50-107">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="58e50-107">Location reporting</span></span>
<span data-ttu-id="58e50-108">Se si desidera toobe percorsi segnalato, è necessario tooadd poche righe di configurazione (tra hello `<application>` e `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="58e50-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="58e50-109">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="58e50-109">Lazy area location reporting</span></span>
<span data-ttu-id="58e50-110">Segnalazione differita della posizione consente reporting hello paese, area e località associate ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="58e50-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="58e50-111">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="58e50-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="58e50-112">area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="58e50-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="58e50-113">Hello GPS non viene mai utilizzato e, pertanto questo tipo di percorso report ha impatto significativo a batteria hello.</span><span class="sxs-lookup"><span data-stu-id="58e50-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="58e50-114">Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori.</span><span class="sxs-lookup"><span data-stu-id="58e50-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="58e50-115">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="58e50-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="58e50-116">Si attiva il percorso di area lazy reporting con la configurazione di hello indicato in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="58e50-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="58e50-117">È inoltre necessario toospecify un'autorizzazione di percorso.</span><span class="sxs-lookup"><span data-stu-id="58e50-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="58e50-118">Questo codice usa l'autorizzazione ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="58e50-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="58e50-119">Se l'app lo richiede, è possibile usare invece di ``ACCESS_FINE_LOCATION`` .</span><span class="sxs-lookup"><span data-stu-id="58e50-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="58e50-120">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="58e50-120">Real-time location reporting</span></span>
<span data-ttu-id="58e50-121">La segnalazione della posizione in tempo reale consente reporting hello latitudine e la longitudine associate ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="58e50-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="58e50-122">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="58e50-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="58e50-123">reporting Hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio, durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="58e50-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="58e50-124">I percorsi in tempo reale sono *non* utilizzato toocompute statistiche.</span><span class="sxs-lookup"><span data-stu-id="58e50-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="58e50-125">Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.</span><span class="sxs-lookup"><span data-stu-id="58e50-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="58e50-126">creazione di report, la posizione in tempo reale tooenable aggiungere una riga di codice toowhere impostare stringa di connessione Engagement hello in attività di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="58e50-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="58e50-127">ottenere un risultato Hello hello seguente:</span><span class="sxs-lookup"><span data-stu-id="58e50-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="58e50-128">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="58e50-128">GPS based reporting</span></span>
<span data-ttu-id="58e50-129">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="58e50-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="58e50-130">tooenable hello GPS basato su percorsi, che sono molto più precisa, utilizzare oggetti di configurazione hello:</span><span class="sxs-lookup"><span data-stu-id="58e50-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="58e50-131">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="58e50-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="58e50-132">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="58e50-132">Background reporting</span></span>
<span data-ttu-id="58e50-133">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio, durante una sessione).</span><span class="sxs-lookup"><span data-stu-id="58e50-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="58e50-134">hello tooenable reporting anche in background, utilizzare l'oggetto di configurazione:</span><span class="sxs-lookup"><span data-stu-id="58e50-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="58e50-135">Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete, anche se è abilitata hello GPS.</span><span class="sxs-lookup"><span data-stu-id="58e50-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="58e50-136">Se l'utente hello riavvio del dispositivo, report di posizione background hello viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="58e50-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="58e50-137">toomake riavviato automaticamente in fase di avvio, aggiungere questo codice.</span><span class="sxs-lookup"><span data-stu-id="58e50-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="58e50-138">È inoltre necessario hello tooadd seguente autorizzazione se mancante:</span><span class="sxs-lookup"><span data-stu-id="58e50-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="58e50-139">Autorizzazioni Android M</span><span class="sxs-lookup"><span data-stu-id="58e50-139">Android M permissions</span></span>
<span data-ttu-id="58e50-140">A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="58e50-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="58e50-141">Se la destinazione è il livello di API Android 23, le autorizzazioni di runtime hello sono disattivate per impostazione predefinita per le nuove installazioni di app.</span><span class="sxs-lookup"><span data-stu-id="58e50-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="58e50-142">In caso contrario vengono attivate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="58e50-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="58e50-143">È possibile abilitare o disabilitare le autorizzazioni dal menu di impostazioni dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="58e50-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="58e50-144">La disattivazione di autorizzazioni dal menu di sistema hello termina i processi in background hello dell'applicazione hello, che è un comportamento del sistema e non influisce sulla possibilità tooreceive push in background.</span><span class="sxs-lookup"><span data-stu-id="58e50-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="58e50-145">Nel contesto di hello della posizione di Mobile Engagement reporting, le autorizzazioni di hello che richiedono l'approvazione in fase di esecuzione sono:</span><span class="sxs-lookup"><span data-stu-id="58e50-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="58e50-146">Richiedere autorizzazioni all'utente di hello utilizzando una finestra di dialogo di sistema standard.</span><span class="sxs-lookup"><span data-stu-id="58e50-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="58e50-147">Indicare se l'utente hello Approva, ``EngagementAgent`` tootake che cambiano in considerazione in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="58e50-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="58e50-148">In caso contrario modifica hello è elaborato successivo ora hello utente avvia hello un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="58e50-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="58e50-149">Ecco un toouse di esempio di codice in un'attività, delle autorizzazioni per l'applicazione toorequest e portare avanti hello se positivo troppo``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="58e50-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
