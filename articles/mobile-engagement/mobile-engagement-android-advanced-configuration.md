---
title: Configurazione avanzata di Android SDK per Azure Mobile Engagement
description: Descrive le opzioni di configurazione avanzate tra cui il manifesto Android con Android SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="989b2-103">Configurazione avanzata di Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="989b2-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="989b2-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="989b2-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="989b2-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="989b2-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="989b2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="989b2-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="989b2-107">Android</span><span class="sxs-lookup"><span data-stu-id="989b2-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="989b2-108">Questa procedura descrive come configurare le diverse opzioni di configurazione per le app Android di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="989b2-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="989b2-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="989b2-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="989b2-110">Requisiti di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="989b2-110">Permission Requirements</span></span>
<span data-ttu-id="989b2-111">Alcune opzioni richiedono autorizzazioni specifiche, ognuna delle quali viene elencata di seguito a titolo di riferimento e inline nella funzionalità specifica.</span><span class="sxs-lookup"><span data-stu-id="989b2-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="989b2-112">Aggiungere queste autorizzazioni al file AndroidManifest.xml del progetto immediatamente prima o dopo il tag `<application>`.</span><span class="sxs-lookup"><span data-stu-id="989b2-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="989b2-113">Il codice di autorizzazione deve essere simile al seguente. L'autorizzazione appropriata viene compilata in base alla tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="989b2-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="989b2-114">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="989b2-114">Permission</span></span> | <span data-ttu-id="989b2-115">Quando si usa</span><span class="sxs-lookup"><span data-stu-id="989b2-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="989b2-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="989b2-116">INTERNET</span></span> |<span data-ttu-id="989b2-117">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="989b2-117">Required.</span></span> <span data-ttu-id="989b2-118">Per report di base</span><span class="sxs-lookup"><span data-stu-id="989b2-118">For basic reporting</span></span> |
| <span data-ttu-id="989b2-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="989b2-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="989b2-120">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="989b2-120">Required.</span></span> <span data-ttu-id="989b2-121">Per report di base</span><span class="sxs-lookup"><span data-stu-id="989b2-121">For basic reporting</span></span> |
| <span data-ttu-id="989b2-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="989b2-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="989b2-123">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="989b2-123">Required.</span></span> <span data-ttu-id="989b2-124">Per visualizzare il centro notifiche dopo il riavvio del dispositivo</span><span class="sxs-lookup"><span data-stu-id="989b2-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="989b2-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="989b2-125">WAKE_LOCK</span></span> |<span data-ttu-id="989b2-126">Consigliato.</span><span class="sxs-lookup"><span data-stu-id="989b2-126">Recommended.</span></span> <span data-ttu-id="989b2-127">Abilita la raccolta dei dati quando si usa il WiFi o quando lo schermo è spento</span><span class="sxs-lookup"><span data-stu-id="989b2-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="989b2-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="989b2-128">VIBRATE</span></span> |<span data-ttu-id="989b2-129">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="989b2-129">Optional.</span></span> <span data-ttu-id="989b2-130">Abilita la vibrazione alla ricezione delle notifiche</span><span class="sxs-lookup"><span data-stu-id="989b2-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="989b2-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="989b2-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="989b2-132">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="989b2-132">Optional.</span></span> <span data-ttu-id="989b2-133">Abilita la notifica generale di Android</span><span class="sxs-lookup"><span data-stu-id="989b2-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="989b2-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="989b2-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="989b2-135">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="989b2-135">Optional.</span></span> <span data-ttu-id="989b2-136">Abilita la notifica generale di Android</span><span class="sxs-lookup"><span data-stu-id="989b2-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="989b2-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="989b2-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="989b2-138">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="989b2-138">Optional.</span></span> <span data-ttu-id="989b2-139">Abilita la segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="989b2-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="989b2-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="989b2-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="989b2-141">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="989b2-141">Optional.</span></span> <span data-ttu-id="989b2-142">Abilita la segnalazione della posizione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="989b2-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="989b2-143">A partire da Android M, [alcune autorizzazioni vengono gestite in fase di esecuzione](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="989b2-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="989b2-144">Se si usa già ``ACCESS_FINE_LOCATION`` non è necessario usare anche ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="989b2-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="989b2-145">Opzioni di configurazione del file manifesto Android</span><span class="sxs-lookup"><span data-stu-id="989b2-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="989b2-146">Segnalazione di arresto anomalo </span><span class="sxs-lookup"><span data-stu-id="989b2-146">Crash report</span></span>
<span data-ttu-id="989b2-147">Per disabilitare la segnalazione di arresti anomali del sistema, aggiungere questo codice tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="989b2-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="989b2-148">Soglia del burst</span><span class="sxs-lookup"><span data-stu-id="989b2-148">Burst threshold</span></span>
<span data-ttu-id="989b2-149">Per impostazione predefinita, il servizio Engagement segnala i log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="989b2-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="989b2-150">Se l'applicazione segnala i log molto spesso, è preferibile memorizzare i log nel buffer e segnalarli tutti insieme con cadenza regolare, la cosiddetta "modalità burst".</span><span class="sxs-lookup"><span data-stu-id="989b2-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="989b2-151">A tale scopo, aggiungere questo codice tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="989b2-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="989b2-152">La modalità burst aumenta lievemente la durata della batteria ma ha un impatto su Monitor di Engagement: la durata di tutte le sessioni e di tutti i processi viene arrotondata alla soglia di burst e, di conseguenza, le sessioni e i processi inferiori alla soglia di burst potrebbero non essere visibili.</span><span class="sxs-lookup"><span data-stu-id="989b2-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="989b2-153">La soglia di burst non dovrebbe essere maggiore di 30000 (30 secondi).</span><span class="sxs-lookup"><span data-stu-id="989b2-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="989b2-154">Timeout della sessione</span><span class="sxs-lookup"><span data-stu-id="989b2-154">Session timeout</span></span>
 <span data-ttu-id="989b2-155">È possibile terminare un'attività premendo **Home** o **Indietro**, impostando l'inattività del telefono o passando a un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="989b2-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="989b2-156">Per impostazione predefinita, una sessione viene terminata 10 secondi dopo la fine dell'ultima attività.</span><span class="sxs-lookup"><span data-stu-id="989b2-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="989b2-157">Ciò avviene per evitare una divisione di sessione ogni volta che l'utente esce e rientra nell'applicazione rapidamente, come può accadere quando preleva un'immagine, controlla una notifica e così via. Questo parametro può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="989b2-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="989b2-158">A tale scopo, aggiungere questo codice tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="989b2-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="989b2-159">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="989b2-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="989b2-160">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="989b2-160">Using a method call</span></span>
<span data-ttu-id="989b2-161">Se si vuole che Engagement non invii più log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="989b2-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="989b2-162">Questa chiamata è persistente: usa un file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="989b2-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="989b2-163">Se Engagement è attivo quando si chiama questa funzione, l'arresto del servizio può richiedere 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="989b2-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="989b2-164">Al successivo avvio dell'applicazione, tuttavia, il servizio non verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="989b2-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="989b2-165">È possibile abilitare di nuovo la segnalazione di log chiamando la stessa funzione con `true`.</span><span class="sxs-lookup"><span data-stu-id="989b2-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="989b2-166">Integrazione nella propria classe `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="989b2-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="989b2-167">Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.</span><span class="sxs-lookup"><span data-stu-id="989b2-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="989b2-168">È possibile configurare Engagement in modo da usare il file di preferenze (con la modalità desiderata) nel file `AndroidManifest.xml` con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="989b2-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="989b2-169">La chiave `engagement:agent:settings:name` viene usata per definire il nome del file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="989b2-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="989b2-170">La chiave `engagement:agent:settings:mode` viene usata per definire la modalità del file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="989b2-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="989b2-171">Usare la stessa modalità usata per `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="989b2-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="989b2-172">La modalità deve essere passata come numero: se si usa una combinazione di flag di costanti nel codice, controllare il valore totale.</span><span class="sxs-lookup"><span data-stu-id="989b2-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="989b2-173">Engagement usa sempre la chiave booleana `engagement:key` all'interno del file di preferenze per la gestione di questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="989b2-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="989b2-174">L'esempio seguente di `AndroidManifest.xml` mostra i valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="989b2-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="989b2-175">Sarà quindi possibile aggiungere un elemento `CheckBoxPreference` nel layout delle preferenze simile a quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="989b2-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
