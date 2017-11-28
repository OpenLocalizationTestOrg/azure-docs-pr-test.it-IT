---
title: configurazione aaaAdvanced per Azure Mobile Engagement SDK Android
description: Vengono descritte le opzioni di configurazione inclusi manifesto Android con Azure Mobile Engagement SDK Android hello avanzate hello
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
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="1e18d-103">Configurazione avanzata di Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1e18d-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e18d-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="1e18d-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="1e18d-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1e18d-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="1e18d-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1e18d-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="1e18d-107">Android</span><span class="sxs-lookup"><span data-stu-id="1e18d-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="1e18d-108">Questa procedura viene descritto come tooconfigure varie opzioni di configurazione per le app Android di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1e18d-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e18d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1e18d-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="1e18d-110">Requisiti di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="1e18d-110">Permission Requirements</span></span>
<span data-ttu-id="1e18d-111">Alcune opzioni richiedono autorizzazioni specifiche, ognuno dei quali sono elencati di seguito per riferimento e in linea nella funzionalità specifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="1e18d-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="1e18d-112">Aggiungere questi toohello autorizzazioni AndroidManifest.xml del progetto, immediatamente prima o dopo hello `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="1e18d-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="1e18d-113">codice di autorizzazione Hello deve toolook hello seguente, in cui si compila le autorizzazioni appropriate hello dalla tabella hello che segue.</span><span class="sxs-lookup"><span data-stu-id="1e18d-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="1e18d-114">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="1e18d-114">Permission</span></span> | <span data-ttu-id="1e18d-115">Quando si usa</span><span class="sxs-lookup"><span data-stu-id="1e18d-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="1e18d-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="1e18d-116">INTERNET</span></span> |<span data-ttu-id="1e18d-117">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1e18d-117">Required.</span></span> <span data-ttu-id="1e18d-118">Per report di base</span><span class="sxs-lookup"><span data-stu-id="1e18d-118">For basic reporting</span></span> |
| <span data-ttu-id="1e18d-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="1e18d-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="1e18d-120">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1e18d-120">Required.</span></span> <span data-ttu-id="1e18d-121">Per report di base</span><span class="sxs-lookup"><span data-stu-id="1e18d-121">For basic reporting</span></span> |
| <span data-ttu-id="1e18d-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="1e18d-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="1e18d-123">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1e18d-123">Required.</span></span> <span data-ttu-id="1e18d-124">tooshow Center notifiche hello dopo il riavvio del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1e18d-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="1e18d-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="1e18d-125">WAKE_LOCK</span></span> |<span data-ttu-id="1e18d-126">Consigliato.</span><span class="sxs-lookup"><span data-stu-id="1e18d-126">Recommended.</span></span> <span data-ttu-id="1e18d-127">Abilita la raccolta dei dati quando si usa il WiFi o quando lo schermo è spento</span><span class="sxs-lookup"><span data-stu-id="1e18d-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="1e18d-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="1e18d-128">VIBRATE</span></span> |<span data-ttu-id="1e18d-129">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e18d-129">Optional.</span></span> <span data-ttu-id="1e18d-130">Abilita la vibrazione alla ricezione delle notifiche</span><span class="sxs-lookup"><span data-stu-id="1e18d-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="1e18d-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="1e18d-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="1e18d-132">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e18d-132">Optional.</span></span> <span data-ttu-id="1e18d-133">Abilita la notifica generale di Android</span><span class="sxs-lookup"><span data-stu-id="1e18d-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="1e18d-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="1e18d-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="1e18d-135">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e18d-135">Optional.</span></span> <span data-ttu-id="1e18d-136">Abilita la notifica generale di Android</span><span class="sxs-lookup"><span data-stu-id="1e18d-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="1e18d-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="1e18d-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="1e18d-138">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e18d-138">Optional.</span></span> <span data-ttu-id="1e18d-139">Abilita la segnalazione della posizione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="1e18d-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="1e18d-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="1e18d-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="1e18d-141">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e18d-141">Optional.</span></span> <span data-ttu-id="1e18d-142">Abilita la segnalazione della posizione basata su GPS</span><span class="sxs-lookup"><span data-stu-id="1e18d-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="1e18d-143">A partire da Android M, [alcune autorizzazioni vengono gestite in fase di esecuzione](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="1e18d-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="1e18d-144">Se si sta già utilizzando ``ACCESS_FINE_LOCATION``, è necessario tooalso utilizzare ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="1e18d-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="1e18d-145">Opzioni di configurazione del file manifesto Android</span><span class="sxs-lookup"><span data-stu-id="1e18d-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="1e18d-146">Segnalazione di arresto anomalo </span><span class="sxs-lookup"><span data-stu-id="1e18d-146">Crash report</span></span>
<span data-ttu-id="1e18d-147">segnalazioni di arresti anomali toodisable, aggiungere il codice tra hello `<application>` e `</application>` tag:</span><span class="sxs-lookup"><span data-stu-id="1e18d-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="1e18d-148">Soglia del burst</span><span class="sxs-lookup"><span data-stu-id="1e18d-148">Burst threshold</span></span>
<span data-ttu-id="1e18d-149">Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="1e18d-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="1e18d-150">Se la relazione dei log applicazioni variano frequentemente, è meglio toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (denominata "potenziamento in modalità").</span><span class="sxs-lookup"><span data-stu-id="1e18d-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="1e18d-151">toodo in tal caso, aggiungere il codice tra hello `<application>` e `</application>` tag:</span><span class="sxs-lookup"><span data-stu-id="1e18d-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="1e18d-152">Modalità burst leggermente aumenta la durata della batteria hello ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi vengono arrotondati toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile).</span><span class="sxs-lookup"><span data-stu-id="1e18d-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="1e18d-153">La soglia di burst non dovrebbe essere maggiore di 30000 (30 secondi).</span><span class="sxs-lookup"><span data-stu-id="1e18d-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="1e18d-154">Timeout della sessione</span><span class="sxs-lookup"><span data-stu-id="1e18d-154">Session timeout</span></span>
 <span data-ttu-id="1e18d-155">È possibile terminare un'attività premendo hello **Home** o **nuovamente** chiave telefonicamente impostazione hello inattivo o per passare a un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e18d-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="1e18d-156">Per impostazione predefinita, una sessione viene terminata dieci secondi dopo la fine di hello del relativo ultima attività.</span><span class="sxs-lookup"><span data-stu-id="1e18d-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="1e18d-157">Ciò consente di evitare una divisione di sessione, ogni utente hello in fase di chiusura e restituisce toohello applicazione rapidamente, che possono verificarsi quando l'utente hello preleva un'immagine, verifica una notifica e così via. È opportuno toomodify questo parametro.</span><span class="sxs-lookup"><span data-stu-id="1e18d-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="1e18d-158">toodo in tal caso, aggiungere il codice tra hello `<application>` e `</application>` tag:</span><span class="sxs-lookup"><span data-stu-id="1e18d-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="1e18d-159">Disabilitare la segnalazione di log</span><span class="sxs-lookup"><span data-stu-id="1e18d-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="1e18d-160">Uso di una chiamata del metodo</span><span class="sxs-lookup"><span data-stu-id="1e18d-160">Using a method call</span></span>
<span data-ttu-id="1e18d-161">Se si desidera toostop Engagement l'invio di log, è possibile chiamare:</span><span class="sxs-lookup"><span data-stu-id="1e18d-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="1e18d-162">Questa chiamata è persistente: usa un file di preferenze condivise.</span><span class="sxs-lookup"><span data-stu-id="1e18d-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="1e18d-163">Se Engagement è attivo quando si chiama questa funzione, potrebbe richiedere un minuto per hello servizio toostop.</span><span class="sxs-lookup"><span data-stu-id="1e18d-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="1e18d-164">Tuttavia, non verrà avviato servizio hello hello tutti successivo avvio di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e18d-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="1e18d-165">È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `true`.</span><span class="sxs-lookup"><span data-stu-id="1e18d-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="1e18d-166">Integrazione nella propria classe `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="1e18d-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="1e18d-167">Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.</span><span class="sxs-lookup"><span data-stu-id="1e18d-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="1e18d-168">È possibile configurare le preferenze di file (con modalità desiderata di hello) toouse di Engagement in hello `AndroidManifest.xml` file con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="1e18d-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="1e18d-169">Hello `engagement:agent:settings:name` chiave è utilizzata toodefine hello nome del file di preferenze condivise hello.</span><span class="sxs-lookup"><span data-stu-id="1e18d-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="1e18d-170">Hello `engagement:agent:settings:mode` chiave è la modalità di hello toodefine utilizzate del file di preferenze condivise hello.</span><span class="sxs-lookup"><span data-stu-id="1e18d-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="1e18d-171">Utilizzare hello stessa modalità come il `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="1e18d-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="1e18d-172">modalità Hello deve essere passata come un numero: se si utilizza una combinazione di flag costante nel codice, controllare il valore totale di hello.</span><span class="sxs-lookup"><span data-stu-id="1e18d-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="1e18d-173">Engagement sempre utilizza hello `engagement:key` booleano chiave all'interno di file di preferenze hello per la gestione di questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="1e18d-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="1e18d-174">Hello in seguito ad esempio `AndroidManifest.xml` Mostra hello valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1e18d-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="1e18d-175">È quindi possibile aggiungere un `CheckBoxPreference` nel layout delle preferenze come segue quello hello:</span><span class="sxs-lookup"><span data-stu-id="1e18d-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
