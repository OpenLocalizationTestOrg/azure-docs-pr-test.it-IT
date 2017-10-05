---
title: Segnalazione della posizione per Android SDK per Azure Mobile Engagement
description: Descrive come configurare la segnalazione della posizione per Android SDK per Azure Mobile Engagement
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
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="2f52a-103">Segnalazione della posizione per Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f52a-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f52a-104">Android</span><span class="sxs-lookup"><span data-stu-id="2f52a-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="2f52a-105">Questo argomento descrive come segnalare la posizione per l'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="2f52a-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f52a-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f52a-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="2f52a-107">Segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="2f52a-107">Location reporting</span></span>
<span data-ttu-id="2f52a-108">Per fare in modo che le posizioni vengano segnalate, è necessario aggiungere alcune righe di configurazione tra i tag `<application>` e `</application>`.</span><span class="sxs-lookup"><span data-stu-id="2f52a-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="2f52a-109">Segnalazione differita della posizione</span><span class="sxs-lookup"><span data-stu-id="2f52a-109">Lazy area location reporting</span></span>
<span data-ttu-id="2f52a-110">La segnalazione differita della posizione consente di segnalare il paese, l'area geografica e la località associati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2f52a-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="2f52a-111">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2f52a-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="2f52a-112">L'area del dispositivo viene segnalata al massimo una volta per sessione.</span><span class="sxs-lookup"><span data-stu-id="2f52a-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="2f52a-113">Il GPS non viene mai usato, per cui l'impatto di questo tipo di segnalazione della posizione sulla batteria è ridotto.</span><span class="sxs-lookup"><span data-stu-id="2f52a-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="2f52a-114">Le aree segnalate vengono usate per calcolare statistiche geografiche relative a utenti, sessioni, eventi ed errori.</span><span class="sxs-lookup"><span data-stu-id="2f52a-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="2f52a-115">Possono essere usate anche come criteri nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="2f52a-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="2f52a-116">Si abilita la segnalazione differita della posizione usando la configurazione descritta in precedenza in questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2f52a-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="2f52a-117">È inoltre necessario specificare un'autorizzazione di posizione.</span><span class="sxs-lookup"><span data-stu-id="2f52a-117">You also need to specify a location permission.</span></span> <span data-ttu-id="2f52a-118">Questo codice usa l'autorizzazione ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="2f52a-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="2f52a-119">Se l'app lo richiede, è possibile usare invece di ``ACCESS_FINE_LOCATION`` .</span><span class="sxs-lookup"><span data-stu-id="2f52a-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="2f52a-120">Segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="2f52a-120">Real-time location reporting</span></span>
<span data-ttu-id="2f52a-121">La segnalazione della posizione in tempo reale consente di segnalare la latitudine e la longitudine associate ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2f52a-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="2f52a-122">Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2f52a-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="2f52a-123">La segnalazione è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="2f52a-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="2f52a-124">Le posizioni in tempo reale *NON* sono usate per calcolare dati statistici.</span><span class="sxs-lookup"><span data-stu-id="2f52a-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="2f52a-125">Il loro unico scopo è consentire l'uso del criterio di definizione del recinto virtuale in tempo reale \<Reach-Audience-geofencing\> nelle campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="2f52a-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="2f52a-126">Per abilitare la segnalazione della posizione in tempo reale, aggiungere una riga di codice dove si è impostata la stringa di connessione di Engagement nell'attività dell'utilità di avvio.</span><span class="sxs-lookup"><span data-stu-id="2f52a-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="2f52a-127">Il risultato è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2f52a-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="2f52a-128">Segnalazione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="2f52a-128">GPS based reporting</span></span>
<span data-ttu-id="2f52a-129">Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="2f52a-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="2f52a-130">Per abilitare l'uso di posizioni basate su GPS, che sono molto più precise, usare l'oggetto di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2f52a-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="2f52a-131">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="2f52a-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="2f52a-132">Segnalazione in background</span><span class="sxs-lookup"><span data-stu-id="2f52a-132">Background reporting</span></span>
<span data-ttu-id="2f52a-133">Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo quando l'applicazione viene eseguita in primo piano, ad esempio durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="2f52a-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="2f52a-134">Per abilitare la segnalazione anche in background, usare questo oggetto di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2f52a-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="2f52a-135">Quando l'applicazione viene eseguita in background, vengono segnalate solo le posizioni basate sulla rete, anche se è abilitato il GPS.</span><span class="sxs-lookup"><span data-stu-id="2f52a-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="2f52a-136">Se l'utente riavvia il dispositivo, viene interrotta la segnalazione della posizione in background.</span><span class="sxs-lookup"><span data-stu-id="2f52a-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="2f52a-137">Per fare in modo che venga riavviata automaticamente al riavvio, aggiungere questo codice.</span><span class="sxs-lookup"><span data-stu-id="2f52a-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="2f52a-138">È necessario aggiungere anche le autorizzazioni seguenti, se mancanti:</span><span class="sxs-lookup"><span data-stu-id="2f52a-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="2f52a-139">Autorizzazioni Android M</span><span class="sxs-lookup"><span data-stu-id="2f52a-139">Android M permissions</span></span>
<span data-ttu-id="2f52a-140">A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2f52a-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="2f52a-141">Se la destinazione è il livello 23 dell'API Android, le autorizzazioni di runtime verranno disattivate per impostazione predefinita per le installazioni di nuove app.</span><span class="sxs-lookup"><span data-stu-id="2f52a-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="2f52a-142">In caso contrario vengono attivate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2f52a-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="2f52a-143">È possibile abilitare o disabilitare le autorizzazioni dal menu delle impostazioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f52a-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="2f52a-144">La disattivazione delle autorizzazioni dal menu di sistema elimina i processi in background dell'applicazione. Si tratta di un comportamento del sistema e non influisce sulla possibilità di ricevere push in background.</span><span class="sxs-lookup"><span data-stu-id="2f52a-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="2f52a-145">Nel contesto della segnalazione della posizione in Mobile Engagement, le autorizzazioni che richiedono l'approvazione in fase di esecuzione sono:</span><span class="sxs-lookup"><span data-stu-id="2f52a-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="2f52a-146">Richiedere le autorizzazioni all'utente con una finestra di dialogo di sistema standard.</span><span class="sxs-lookup"><span data-stu-id="2f52a-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="2f52a-147">Se l'utente approva, specificare ``EngagementAgent`` per applicare la modifica in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="2f52a-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="2f52a-148">In caso contrario la modifica verrà elaborata al successivo avvio dell'applicazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2f52a-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="2f52a-149">Ecco un esempio di codice da utilizzare in un'attività dell'applicazione per richiedere autorizzazioni e inoltrare il risultato, se positivo, a ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="2f52a-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
