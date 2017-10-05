---
title: Integrazione di Android SDK per Azure Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="d1985-103">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="d1985-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="d1985-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="d1985-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="d1985-105">Correzione di un arresto anomalo del sistema che può verificarsi raramente quando si chiama `EngagementAgentUtils.isInDedicatedEngagementProcess`, che viene usato anche dalla classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="d1985-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="d1985-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="d1985-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="d1985-107">Supporto Android 8 (versioni precedenti dell'SDK non funzionano in Android 8).</span><span class="sxs-lookup"><span data-stu-id="d1985-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="d1985-108">Nessuna dipendenza nella raccolta di supporto.</span><span class="sxs-lookup"><span data-stu-id="d1985-108">No more dependency on support library.</span></span>
* <span data-ttu-id="d1985-109">Rimuovere la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="d1985-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="d1985-110">A causa di [limiti di esecuzione in Background](https://developer.android.com/preview/features/background.html) in Android 8, i log in background potrebbero subire un ritardo fino a quando l'utente non interagisce con il dispositivo; ciò avrà un impatto sulla campagna Push **Consegnata** e sulle statistiche **Notifica di sistema visualizzata** che subiscono un ritardo se il dispositivo era in sospensione (la notifica verrà ancora visualizzata, suonerà e vibrerà in tempo reale senza problemi).</span><span class="sxs-lookup"><span data-stu-id="d1985-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="d1985-111">A causa di [limiti del percorso di background](https://developer.android.com/preview/features/background-location-limits.html), il percorso in tempo reale in background non verrà aggiornato frequentemente in Android 8.</span><span class="sxs-lookup"><span data-stu-id="d1985-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="d1985-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="d1985-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="d1985-113">Correggere i colori del testo della notifica in-app in Android 7 in modo che corrispondano a quelli di versioni precedenti di Android.</span><span class="sxs-lookup"><span data-stu-id="d1985-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="d1985-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="d1985-115">Rimozione del blocco Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d1985-115">No more WIFI lock.</span></span>
* <span data-ttu-id="d1985-116">Correzione di un deadlock quando si chiama getDeviceId prima di init (bug introdotto nella versione 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="d1985-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="d1985-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="d1985-118">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="d1985-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="d1985-120">Sicurezza: disabilitare l'accesso al file locale di visualizzazione Web.</span><span class="sxs-lookup"><span data-stu-id="d1985-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="d1985-121">Sicurezza: rimozione della classe `EngagementPreferenceActivity` che estende la classe `PreferenceActivity` obsoleta e non sicura.</span><span class="sxs-lookup"><span data-stu-id="d1985-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="d1985-122">Sicurezza: le attività del servizio di copertura vengono ora documentate per l'uso di `exported="false"`. Questo flag può essere usato anche nelle versioni precedenti dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="d1985-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="d1985-123">4.2.0 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="d1985-124">L'SDK ora è concesso in licenza con MIT.</span><span class="sxs-lookup"><span data-stu-id="d1985-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="d1985-125">Consentire la specifica di un identificatore del dispositivo personalizzato in fase di inizializzazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="d1985-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="d1985-126">4.1.5 (01/02/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="d1985-127">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="d1985-128">4.1.4 (26/01/2016)</span><span class="sxs-lookup"><span data-stu-id="d1985-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="d1985-129">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="d1985-130">4.1.3 (9/12/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="d1985-131">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="d1985-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="d1985-133">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="d1985-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="d1985-135">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="d1985-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="d1985-137">Gestione di un nuovo modello di autorizzazione per Android M.</span><span class="sxs-lookup"><span data-stu-id="d1985-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="d1985-138">Ora è possibile configurare le funzionalità di posizione in fase di esecuzione anziché usare `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d1985-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="d1985-139">Correzione di un bug delle autorizzazioni: se si utilizza `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="d1985-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="d1985-140">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="d1985-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="d1985-141">4.0.0 (06/07/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="d1985-142">Modifiche al protocollo interno per rendere più affidabili le analisi e il push.</span><span class="sxs-lookup"><span data-stu-id="d1985-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="d1985-143">Il push nativo (GCM/ADM) viene ora usato anche per le notifiche in-app. È quindi necessario configurare le credenziali del push nativo per qualsiasi tipo di campagna push.</span><span class="sxs-lookup"><span data-stu-id="d1985-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="d1985-144">Correzione della notifica generale: elementi visualizzati solo 10 secondi dopo il push.</span><span class="sxs-lookup"><span data-stu-id="d1985-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="d1985-145">Correzione di un bug nella visualizzazione Web: facendo clic su un collegamento durante si eseguiva anche l'URL di azione predefinito.</span><span class="sxs-lookup"><span data-stu-id="d1985-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="d1985-146">Correzione di un arresto anomalo raro correlato alla gestione dell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="d1985-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="d1985-147">Correzione della gestione delle stringhe di configurazione dinamiche.</span><span class="sxs-lookup"><span data-stu-id="d1985-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="d1985-148">Aggiornamento del contratto di licenza.</span><span class="sxs-lookup"><span data-stu-id="d1985-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="d1985-149">3.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="d1985-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="d1985-150">Versione iniziale di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d1985-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="d1985-151">La configurazione di appId è stata sostituita con la configurazione della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="d1985-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="d1985-152">L'API non invia e non riceve più messaggi XMPP da entità XMPP arbitrarie.</span><span class="sxs-lookup"><span data-stu-id="d1985-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="d1985-153">L'API non riceve e non invia più messaggi tra i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d1985-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="d1985-154">Sono stati introdotti miglioramenti per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d1985-154">Security improvements.</span></span>
* <span data-ttu-id="d1985-155">È stata rimossa la verifica per Google Play e SmartAd.</span><span class="sxs-lookup"><span data-stu-id="d1985-155">Google Play and SmartAd tracking removed.</span></span>

