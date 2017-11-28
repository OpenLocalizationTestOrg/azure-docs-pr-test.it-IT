---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
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
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="e4d1f-103">Guida alla risoluzione dei problemi relativi all'integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="e4d1f-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="e4d1f-104">di seguito Hello sono possibili problemi che possono verificarsi con l'integrazione di Azure Mobile Engagement nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="e4d1f-105">Problemi dell'SDK rilevati da un errore in un'altra area dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e4d1f-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="e4d1f-106">Problema</span><span class="sxs-lookup"><span data-stu-id="e4d1f-106">Issue</span></span>
* <span data-ttu-id="e4d1f-107">Errore relativo alla raccolta dati dell'interfaccia utente (nelle sezioni di analisi, monitoraggio, segmentazione o dashboard).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="e4d1f-108">Errori relativi alle notifiche push (le notifiche in-app, all'esterno dell'app o entrambe non funzionano).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="e4d1f-109">Errori relativi alle funzionalità avanzate (le notifiche push di monitoraggio, georilevazione o specifiche della piattaforma non funzionano).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="e4d1f-110">Errori dell'API (spesso l'errore non genera messaggi).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="e4d1f-111">Errori di servizio (nessun servizio Azure Mobile Engagement funziona per l'applicazione).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="e4d1f-112">Cause</span><span class="sxs-lookup"><span data-stu-id="e4d1f-112">Causes</span></span>
* <span data-ttu-id="e4d1f-113">La maggior parte dei problemi necessarie toobe risolto con hello Azure Mobile Engagement SDK verranno individuati da un errore nell'applicazione (ad esempio un errore di raccolta dati dell'interfaccia utente, errore push, errore di funzionalità avanzata, errore API, arresti anomali delle applicazioni o servizio apparente interruzione).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="e4d1f-114">Se una particolare funzionalità di Azure Mobile Engagement non è mai lavorato nell'applicazione prima di, è necessario integrazione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="e4d1f-115">Se una particolare funzionalità di Azure Mobile Engagement funzionava e interrotto, potrebbe essere tooupgrade toohello ultima versione con hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="e4d1f-116">Tenere presente che esiste una versione diversa di hello Azure Mobile Engagement SDK per ogni piattaforma supportata da Azure Mobile Engagement (Android, iOS, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="e4d1f-117">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="e4d1f-117">SDK Integration</span></span>
* <span data-ttu-id="e4d1f-118">Azure Mobile Engagement non integrato correttamente nell'SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="e4d1f-119">Reach non integrato correttamente nell'SDK (notifiche push in-app e all'esterno dell'app).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="e4d1f-120">Certificato scaduto o versione di produzione o sviluppo non corretta (solo per iOS).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="e4d1f-121">GCM o ADM non integrato correttamente nell'SDK (solo per Android - Notifiche push di un servizio specifico).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="e4d1f-122">Verifica non integrata correttamente nell'SDK (installazione della verifica dello store).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="e4d1f-123">Località lenta o località GPS non integrata correttamente nell'SDK (selezione destinazione in base alla georilevazione).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="e4d1f-124">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="e4d1f-124">**See also:**</span></span>

* <span data-ttu-id="e4d1f-125">[Documentazione SDK - Guide all'integrazione][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="e4d1f-126">[Guida alla risoluzione dei problemi - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="e4d1f-127">Aggiornamento dell'SDK</span><span class="sxs-lookup"><span data-stu-id="e4d1f-127">SDK Upgrade</span></span>
* <span data-ttu-id="e4d1f-128">Problemi di tooresolve tooupgrade SDK con le versioni precedenti di hello SDK (spesso correlate toonewer versioni del sistema operativo del dispositivo hello) è necessario.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="e4d1f-129">Disinstallare tutte le versioni precedenti dell'app dal dispositivo e reinstallare la versione più recente di hello dell'app, hello registrare nuovamente l'ID dispositivo da hello dell'interfaccia utente di Azure Mobile Engagement tooconfirm che il dispositivo utilizza hello la versione più recente dell'app.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="e4d1f-130">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="e4d1f-130">**See also:**</span></span>

* [<span data-ttu-id="e4d1f-131">Documentazione SDK - Note di rilascio</span><span class="sxs-lookup"><span data-stu-id="e4d1f-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="e4d1f-132">Documentazione SDK - Guide all'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="e4d1f-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="e4d1f-133">Altri problemi dell'SDK</span><span class="sxs-lookup"><span data-stu-id="e4d1f-133">SDK Other</span></span>
* <span data-ttu-id="e4d1f-134">Gli errori nel manifesto dell'applicazione "AndroidManifest.xml" possono causare Azure Mobile Engagement non toowork (solo Android).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="e4d1f-135">Un problema comune con l'integrazione SDK e utilizzo delle API è hello tooconfuse chiave SDK e hello chiave API.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="e4d1f-136">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="e4d1f-136">**See also:**</span></span>

* <span data-ttu-id="e4d1f-137">[Concetti - Glossario][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="e4d1f-138">Problemi relativi alla codifica avanzata</span><span class="sxs-lookup"><span data-stu-id="e4d1f-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="e4d1f-139">Problema</span><span class="sxs-lookup"><span data-stu-id="e4d1f-139">Issue</span></span>
* <span data-ttu-id="e4d1f-140">Codice specifico della piattaforma non direttamente correlate tooAzure che Engagement Mobile può causare problemi in iOS, Android e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="e4d1f-141">Cause</span><span class="sxs-lookup"><span data-stu-id="e4d1f-141">Causes</span></span>
* <span data-ttu-id="e4d1f-142">Molte avanzate di codifica con Azure Mobile Engagement sono causate dalla piattaforma in modo non corretto scritta codice specifico non direttamente correlate tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="e4d1f-143">Sarà necessario piattaforma toohello specifico di documentazione tooconsult che si sviluppa per inoltre la documentazione di Mobile Engagement tooAzure (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="e4d1f-144">Configurazione non corretta "categorie", impedisce il collegamento da un percorso tooanother notifica all'interno o all'esterno di hello app (solo Android).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="e4d1f-145">Se non viene impostata "UIKit.framework" troppo "facoltativo" nel codice iOS, visualizza un "Simbolo di errore non trovato" e/o l'arresto anomalo in dispositivi iOS meno recenti (solo iOS).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="e4d1f-146">I certificati scaduti o non correttamente utilizzando hello DEV o una versione di produzione del certificato hello, push causa problemi (solo iOS).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="e4d1f-147">Esistono alcuni piattaforma tooa inerente limitazioni che non è possibile controllare Azure Mobile Engagement (ad esempio, funzionamento per center sistema hello all'esterno dell'app inserimenti in Android e iOS).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="e4d1f-148">Azure Mobile Engagement pubblica un elenco completo dei pacchetti di hello interno utilizzato da Azure Mobile Engagement per iOS e Android per riferimento.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="e4d1f-149">Tenere presente che alcune funzionalità di Azure Mobile Engagement sono toohello specifico della piattaforma (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="e4d1f-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e4d1f-150">See also</span></span>
* <span data-ttu-id="e4d1f-151">[Guida alla risoluzione dei problemi - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="e4d1f-152">[Documentazione SDK - Note di rilascio][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="e4d1f-153">[Documentazione SDK - Guide all'aggiornamento][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="e4d1f-154">Arresti anomali dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="e4d1f-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="e4d1f-155">Problema</span><span class="sxs-lookup"><span data-stu-id="e4d1f-155">Issue</span></span>
* <span data-ttu-id="e4d1f-156">L'applicazione si blocca nel dispositivo hello degli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="e4d1f-157">Cause</span><span class="sxs-lookup"><span data-stu-id="e4d1f-157">Causes</span></span>
* <span data-ttu-id="e4d1f-158">Informazioni sull'arresto anomalo possono essere visualizzati in hello *dell'interfaccia utente Analitica* o hello *API Analitica*</span><span class="sxs-lookup"><span data-stu-id="e4d1f-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="e4d1f-159">È possibile trovare hello ID dispositivo del dispositivo di test e richiedere hello stessa azione che ha causato il toocrash di applicazione per un utente finale di toohelp identificare causa hello dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="e4d1f-160">Problemi noti con hello Azure Mobile Engagement SDK che causano toocrash applicazioni talvolta risolti dall'aggiornamento toohello la versione più recente di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="e4d1f-161">Verificare che toocheck hello note sulla piattaforma durante l'esame di arresti anomali del sistema.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="e4d1f-162">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e4d1f-162">See also</span></span>
* <span data-ttu-id="e4d1f-163">[Documentazione SDK - Note di rilascio][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="e4d1f-164">[Documentazione SDK - Guide all'aggiornamento][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e4d1f-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="e4d1f-165">Errori di caricamento in App Store</span><span class="sxs-lookup"><span data-stu-id="e4d1f-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="e4d1f-166">Problema</span><span class="sxs-lookup"><span data-stu-id="e4d1f-166">Issue</span></span>
* <span data-ttu-id="e4d1f-167">Errori correlati toouploading hello più recente di app tooApple, Google o archivio di App di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="e4d1f-168">Cause</span><span class="sxs-lookup"><span data-stu-id="e4d1f-168">Causes</span></span>
* <span data-ttu-id="e4d1f-169">App archivia talvolta blocco app con determinate funzionalità abilitate (ad esempio hello Apple Store impedisce hello ricorso IDFV nelle app di store hello e archivio GooglePlay hello hello condivisione delle informazioni di applicazione tra App).</span><span class="sxs-lookup"><span data-stu-id="e4d1f-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="e4d1f-170">Assicurarsi di controllare le note sulla versione di hello sulla piattaforma e la versione corrente di hello SDK nel caso di difficoltà di caricamento di un archivio di app toohello.</span><span class="sxs-lookup"><span data-stu-id="e4d1f-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

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

