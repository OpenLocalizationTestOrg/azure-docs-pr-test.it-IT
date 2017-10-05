---
title: Guida alla risoluzione dei problemi di Azure Mobile Engagement - SDK
description: Risoluzione dei problemi relativi all'integrazione dell'SDK in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="7f02f-103">Guida alla risoluzione dei problemi relativi all'integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="7f02f-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="7f02f-104">Di seguito sono indicati possibili problemi relativi al modo in cui Azure Mobile Engagement si integra con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f02f-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="7f02f-105">Problemi dell'SDK rilevati da un errore in un'altra area dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7f02f-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="7f02f-106">Problema</span><span class="sxs-lookup"><span data-stu-id="7f02f-106">Issue</span></span>
* <span data-ttu-id="7f02f-107">Errore relativo alla raccolta dati dell'interfaccia utente (nelle sezioni di analisi, monitoraggio, segmentazione o dashboard).</span><span class="sxs-lookup"><span data-stu-id="7f02f-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="7f02f-108">Errori relativi alle notifiche push (le notifiche in-app, all'esterno dell'app o entrambe non funzionano).</span><span class="sxs-lookup"><span data-stu-id="7f02f-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="7f02f-109">Errori relativi alle funzionalità avanzate (le notifiche push di monitoraggio, georilevazione o specifiche della piattaforma non funzionano).</span><span class="sxs-lookup"><span data-stu-id="7f02f-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="7f02f-110">Errori dell'API (spesso l'errore non genera messaggi).</span><span class="sxs-lookup"><span data-stu-id="7f02f-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="7f02f-111">Errori di servizio (nessun servizio Azure Mobile Engagement funziona per l'applicazione).</span><span class="sxs-lookup"><span data-stu-id="7f02f-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="7f02f-112">Cause</span><span class="sxs-lookup"><span data-stu-id="7f02f-112">Causes</span></span>
* <span data-ttu-id="7f02f-113">La maggior parte dei problemi da risolvere con Azure Mobile Engagement SDK vengono rilevati da un errore dell'applicazione (ad esempio, da un errore durante la raccolta dati dell'interfaccia utente, da un errore delle notifiche push, delle funzionalità avanzate, dell'API, da un arresto anomalo dell'applicazione e da un'apparente interruzione del servizio).</span><span class="sxs-lookup"><span data-stu-id="7f02f-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="7f02f-114">Se una determinata funzionalità di Azure Mobile Engagement non ha mai funzionato nell'app, è necessario eseguire l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="7f02f-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="7f02f-115">Se una determinata funzionalità di Azure Mobile Engagement ha smesso di funzionare, può essere necessario aggiornare Azure Mobile Engagement SDK alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="7f02f-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="7f02f-116">Tenere presente che è disponibile una versione diversa di Azure Mobile Engagement SDK per ogni piattaforma supportata (Android, iOS, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="7f02f-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="7f02f-117">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="7f02f-117">SDK Integration</span></span>
* <span data-ttu-id="7f02f-118">Azure Mobile Engagement non integrato correttamente nell'SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="7f02f-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="7f02f-119">Reach non integrato correttamente nell'SDK (notifiche push in-app e all'esterno dell'app).</span><span class="sxs-lookup"><span data-stu-id="7f02f-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="7f02f-120">Certificato scaduto o versione di produzione o sviluppo non corretta (solo per iOS).</span><span class="sxs-lookup"><span data-stu-id="7f02f-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="7f02f-121">GCM o ADM non integrato correttamente nell'SDK (solo per Android - Notifiche push di un servizio specifico).</span><span class="sxs-lookup"><span data-stu-id="7f02f-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="7f02f-122">Verifica non integrata correttamente nell'SDK (installazione della verifica dello store).</span><span class="sxs-lookup"><span data-stu-id="7f02f-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="7f02f-123">Località lenta o località GPS non integrata correttamente nell'SDK (selezione destinazione in base alla georilevazione).</span><span class="sxs-lookup"><span data-stu-id="7f02f-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="7f02f-124">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="7f02f-124">**See also:**</span></span>

* <span data-ttu-id="7f02f-125">[Documentazione SDK - Guide all'integrazione][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7f02f-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="7f02f-126">[Guida alla risoluzione dei problemi - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="7f02f-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="7f02f-127">Aggiornamento dell'SDK</span><span class="sxs-lookup"><span data-stu-id="7f02f-127">SDK Upgrade</span></span>
* <span data-ttu-id="7f02f-128">È necessario aggiornare l'SDK per risolvere i problemi relativi alle versioni precedenti (spesso relativi a nuove versioni del sistema operativo del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="7f02f-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="7f02f-129">Disinstallare tutte le versioni precedenti dell'app dal dispositivo e installare la versione più recente, registrare nuovamente l'ID dispositivo dall'interfaccia utente di Azure Mobile Engagement per confermare che il dispositivo utilizza la versione più recente dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f02f-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="7f02f-130">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="7f02f-130">**See also:**</span></span>

* [<span data-ttu-id="7f02f-131">Documentazione SDK - Note di rilascio</span><span class="sxs-lookup"><span data-stu-id="7f02f-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="7f02f-132">Documentazione SDK - Guide all'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="7f02f-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="7f02f-133">Altri problemi dell'SDK</span><span class="sxs-lookup"><span data-stu-id="7f02f-133">SDK Other</span></span>
* <span data-ttu-id="7f02f-134">Gli errori nel file manifesto dell'applicazione "AndroidManifest.xml" possono impedire il funzionamento di Azure Mobile Engagement (solo per Android).</span><span class="sxs-lookup"><span data-stu-id="7f02f-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="7f02f-135">Un problema comune relativo all'integrazione dell'SDK e all'utilizzo dell'API si verifica quando vengono confuse le chiavi SDK e API.</span><span class="sxs-lookup"><span data-stu-id="7f02f-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="7f02f-136">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="7f02f-136">**See also:**</span></span>

* <span data-ttu-id="7f02f-137">[Concetti - Glossario][Link 6]</span><span class="sxs-lookup"><span data-stu-id="7f02f-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="7f02f-138">Problemi relativi alla codifica avanzata</span><span class="sxs-lookup"><span data-stu-id="7f02f-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="7f02f-139">Problema</span><span class="sxs-lookup"><span data-stu-id="7f02f-139">Issue</span></span>
* <span data-ttu-id="7f02f-140">Un codice specifico per una piattaforma, non collegato direttamente ad Azure Mobile Engagement, può causare problemi in iOS, Android e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="7f02f-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="7f02f-141">Cause</span><span class="sxs-lookup"><span data-stu-id="7f02f-141">Causes</span></span>
* <span data-ttu-id="7f02f-142">Molti problemi di codifica avanzata relativi ad Azure Mobile Engagement sono causati da codice di piattaforma scritto in modo errato e che non fa riferimento diretto ad Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7f02f-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="7f02f-143">Oltre alla documentazione su Azure Mobile Engagement, è necessario consultare la documentazione sulla piattaforma, durante le operazioni di sviluppo (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="7f02f-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="7f02f-144">Se non si configurano correttamente le "categorie", si impedisce il collegamento di una notifica a un'altra posizione interna o esterna all'app (soltanto su Android).</span><span class="sxs-lookup"><span data-stu-id="7f02f-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="7f02f-145">Se non si imposta "UIKit.framework" su "optional" nel codice iOS, viene visualizzato il messaggio di errore "Impossibile trovare simbolo" e i dispositivi iOS meno recenti si arrestano in modo anomalo (soltanto su iOS).</span><span class="sxs-lookup"><span data-stu-id="7f02f-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="7f02f-146">I certificati scaduti o quelli che non usano correttamente la versione di sviluppo o produzione causano problemi relativi alle notifiche push (solo per iOS).</span><span class="sxs-lookup"><span data-stu-id="7f02f-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="7f02f-147">Esistono alcune limitazioni inerenti a una piattaforma che Azure Mobile Engagement non è in grado di controllare (ad esempio, come funziona il system center per le notifiche push out-of-app in Android e iOS).</span><span class="sxs-lookup"><span data-stu-id="7f02f-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="7f02f-148">In Azure Mobile Engagement viene pubblicato un elenco completo di riferimento relativo ai pacchetti interni utilizzati da Azure Mobile Engagement in iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="7f02f-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="7f02f-149">Tenere presente che alcune funzionalità di Azure Mobile Engagement sono specifiche di piattaforma (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="7f02f-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="7f02f-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7f02f-150">See also</span></span>
* <span data-ttu-id="7f02f-151">[Guida alla risoluzione dei problemi - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="7f02f-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="7f02f-152">[Documentazione SDK - Note di rilascio][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7f02f-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="7f02f-153">[Documentazione SDK - Guide all'aggiornamento][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7f02f-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="7f02f-154">Arresti anomali dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="7f02f-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="7f02f-155">Problema</span><span class="sxs-lookup"><span data-stu-id="7f02f-155">Issue</span></span>
* <span data-ttu-id="7f02f-156">L'applicazione si arresta in modo anomalo nel dispositivo degli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="7f02f-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="7f02f-157">Cause</span><span class="sxs-lookup"><span data-stu-id="7f02f-157">Causes</span></span>
* <span data-ttu-id="7f02f-158">È possibile visualizzare le informazioni sull'arresto anomalo nell'*interfaccia utente di analisi* o nell'*API di analisi*.</span><span class="sxs-lookup"><span data-stu-id="7f02f-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="7f02f-159">È possibile trovare l'ID del dispositivo di test ed effettuare la stessa azione che ha causato l'arresto anomalo dell'applicazione. In questo modo, sarà possibile identificare la causa dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="7f02f-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="7f02f-160">I problemi noti relativi all'SDK di Azure Mobile Engagement che hanno causato l'arresto anomalo dell'applicazione vengono spesso risolti aggiornando l'SDK all'ultima versione disponibile.</span><span class="sxs-lookup"><span data-stu-id="7f02f-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="7f02f-161">Pertanto, consultare le note di rilascio della propria piattaforma, quando si analizza l'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="7f02f-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="7f02f-162">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7f02f-162">See also</span></span>
* <span data-ttu-id="7f02f-163">[Documentazione SDK - Note di rilascio][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7f02f-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="7f02f-164">[Documentazione SDK - Guide all'aggiornamento][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7f02f-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="7f02f-165">Errori di caricamento in App Store</span><span class="sxs-lookup"><span data-stu-id="7f02f-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="7f02f-166">Problema</span><span class="sxs-lookup"><span data-stu-id="7f02f-166">Issue</span></span>
* <span data-ttu-id="7f02f-167">Errori relativi al caricamento della versione più recente dell'app in Apple, Google o Windows App Store.</span><span class="sxs-lookup"><span data-stu-id="7f02f-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="7f02f-168">Cause</span><span class="sxs-lookup"><span data-stu-id="7f02f-168">Causes</span></span>
* <span data-ttu-id="7f02f-169">Talvolta, gli store di app bloccano quelle sulle quali sono attivate determinate funzioni. Ad esempio, in Apple Store non è possibile utilizzare IDFV nelle app, mentre in Google Play non è possibile condividere informazioni sulle applicazioni tra le app.</span><span class="sxs-lookup"><span data-stu-id="7f02f-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="7f02f-170">Consultare le note di rilascio sulla propria piattaforma e sulla versione corrente dell'SDK, in caso di problemi durante il caricamento di un'app nello store.</span><span class="sxs-lookup"><span data-stu-id="7f02f-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

