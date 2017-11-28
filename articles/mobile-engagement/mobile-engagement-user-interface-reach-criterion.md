---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere criterio
description: Informazioni su come toouse destinazione criteri toosend push campagne tooa selezionare sottoinsieme di utenti con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="80821-103">In che modo toouse destinazione criteri toosend push campagne tooa seleziona sottoinsieme di utenti</span><span class="sxs-lookup"><span data-stu-id="80821-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="80821-104">I destinatari di destinazione in base a criteri specifici con pulsante "Nuovo criterio" hello è uno dei hello più potenti concetti in Azure Mobile Engagement che consente di che inviare rilevanti push delle notifiche che i clienti hello risponderà tooinstead di questi comportamenti tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="80821-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="80821-105">È possibile limitare i destinatari in base ai criteri standard e simulare push toodetermine quante persone hanno riceverà una notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="80821-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="80821-106">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="80821-106">**See also:**</span></span>

* <span data-ttu-id="80821-107">[Documentazione dell'interfaccia utente - Reach - Nuova campagna di push][Link 27]</span><span class="sxs-lookup"><span data-stu-id="80821-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="80821-108">I criteri dei destinatari possono includere:</span><span class="sxs-lookup"><span data-stu-id="80821-108">Audience criteria can include:</span></span>
* <span data-ttu-id="80821-109">* * Technicals: * * è possibile destinare hello in base alle stesse informazioni tecniche è possibile visualizzare hello Analitica e sezioni di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="80821-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="80821-110">**Vedere anche:**[Documentazione dell'interfaccia utente - Analytics][Link 15], [Documentazione dell'interfaccia utente - Monitor][Link 16]</span><span class="sxs-lookup"><span data-stu-id="80821-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="80821-111">**Percorso:** posizione geografica utilizzabili dalle applicazioni che utilizzano "segnalazione della posizione in tempo reale" Geo-Fencing come un tootarget criteri un gruppo di destinatari da hello posizione GPS.</span><span class="sxs-lookup"><span data-stu-id="80821-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="80821-112">Chiamata di "Lazy Area percorso report" inoltre essere tootarget usato un gruppo di destinatari dal percorso di un telefono cellulare hello ("segnalazione della posizione in tempo reale" e "Lazy segnalazione della posizione" deve essere attivato da hello SDK).</span><span class="sxs-lookup"><span data-stu-id="80821-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="80821-113">**Vedere anche:** [Documentazione SDK - iOS - Integrazione][Link 5], [Documentazione SDK - Android - Integrazione][Link 5]</span><span class="sxs-lookup"><span data-stu-id="80821-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="80821-114">**Feedback di copertura:** è possibile definire i destinatari sulla base del loro feedback sulle precedenti notifiche di copertura usando il feedback di copertura derivante da annunci, sondaggi e push di dati.</span><span class="sxs-lookup"><span data-stu-id="80821-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="80821-115">In questo modo destinazione toobetter i destinatari quando due o tre raggiunto campagne rispetto a quelle Impossibile hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="80821-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="80821-116">E può essere utilizzato anche toofilter gli utenti che hanno già ricevuto una notifica con contenuto simile, impostando un tooNOT campagna inviato toousers che hanno già ricevuto una campagna specifica precedente.</span><span class="sxs-lookup"><span data-stu-id="80821-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="80821-117">È anche possibile escludere gli utenti inclusi in una campagna specifica ancora attiva in modo che non ricevano nuove notifiche push.</span><span class="sxs-lookup"><span data-stu-id="80821-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="80821-118">**Vedere anche:** [Documentazione dell'interfaccia utente - Reach - Push del contenuto][Link 29]</span><span class="sxs-lookup"><span data-stu-id="80821-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="80821-119">**Rilevamento installazione:** è possibile rilevare le informazioni in base alla posizione in cui gli utenti hanno installato l'app.</span><span class="sxs-lookup"><span data-stu-id="80821-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="80821-120">**Vedere anche:** [Documentazione dell'interfaccia utente - Impostazioni][Link 20]</span><span class="sxs-lookup"><span data-stu-id="80821-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="80821-121">**Profilo utente:** possibile destinazione in base alle informazioni utente standard e non si può destinazione in base alle informazioni di hello app personalizzata che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="80821-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="80821-122">Ciò include gli utenti attualmente connessi e gli utenti che hanno risposto a domande specifiche, richiesta in app hello stessa anziché semplicemente come hanno risposto campagne tooprevious tooset.</span><span class="sxs-lookup"><span data-stu-id="80821-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="80821-123">Tutte le informazioni sull'app definite per l'app stessa vengono visualizzate nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="80821-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="80821-124">Segmenti: è possibile definire i destinatari sulla base dei segmenti creati a seconda del comportamento utente definito da più criteri.</span><span class="sxs-lookup"><span data-stu-id="80821-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="80821-125">Tutti i segmenti definiti per l'app vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="80821-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="80821-126">**Vedere anche:**[Documentazione dell'interfaccia utente - Segmenti][Link 18]</span><span class="sxs-lookup"><span data-stu-id="80821-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="80821-127">**App Info:** personalizzato App Info tag possono essere creati da un comportamento utente tootrack "Impostazioni".</span><span class="sxs-lookup"><span data-stu-id="80821-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="80821-128">**Vedere anche:** [Documentazione dell'interfaccia utente - Impostazioni][Link 20]</span><span class="sxs-lookup"><span data-stu-id="80821-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="80821-129">Esempio:</span><span class="sxs-lookup"><span data-stu-id="80821-129">Example:</span></span>
<span data-ttu-id="80821-130">Se si desidera toopush un annuncio toohello solo sottoinsieme di utenti che hanno eseguito una in-app acquistare azione.</span><span class="sxs-lookup"><span data-stu-id="80821-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="80821-131">Vai a pagina di impostazioni applicazione tooyour, selezionare il menu di "info App" hello e selezionare "Nuova app info"</span><span class="sxs-lookup"><span data-stu-id="80821-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="80821-132">Registrare nuove informazioni booleane sull'app definite "inAppPurchase"</span><span class="sxs-lookup"><span data-stu-id="80821-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="80821-133">Rendere l'applicazione impostare informazioni sull'app troppo "true" quando l'utente di hello esegue correttamente un acquisto in-app (tramite hello sendAppInfo ("inAppPurchase",...) funzione)</span><span class="sxs-lookup"><span data-stu-id="80821-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="80821-134">Se non si desidera toodo questo dall'applicazione, è possibile farlo dal back-end utilizzando l'API dispositivo hello)</span><span class="sxs-lookup"><span data-stu-id="80821-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="80821-135">Quindi, è sufficiente toocreate annuncio, con un criterio di limitazione toousers il gruppo di destinatari con "inAppPurchase" set troppo "true")</span><span class="sxs-lookup"><span data-stu-id="80821-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="80821-136">Destinazione in base ai criteri diversi da tag info app richiede informazioni toogather Azure Mobile Engagement dai dispositivi degli utenti prima di push hello viene inviato e pertanto può provocare un ritardo.</span><span class="sxs-lookup"><span data-stu-id="80821-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="80821-137">Anche le opzioni di configurazione push complesse (ad esempio l'aggiornamento dei badge) possono determinare ritardi dei push.</span><span class="sxs-lookup"><span data-stu-id="80821-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="80821-138">Utilizzo di una campagna "un unico passaggio" da hello API Push è hello assoluto metodo più veloce push in Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="80821-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="80821-139">Utilizzare solo il tag di info app come criteri di push per una campagna di copertura (sia dall'API Reach hello o hello dell'interfaccia utente) è metodo più veloce Avanti hello poiché tag info app vengono archiviate sul lato server hello.</span><span class="sxs-lookup"><span data-stu-id="80821-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="80821-140">Utilizzando altri criteri di destinazione per una campagna push è hello più flessibile, ma più lente push (metodo), poiché Azure Mobile Engagement ha dispositivi hello tooquery campagna hello toosend di ordine.</span><span class="sxs-lookup"><span data-stu-id="80821-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="80821-142">Le opzioni dei criteri si applicano a:</span><span class="sxs-lookup"><span data-stu-id="80821-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="80821-143">**Informazioni tecniche**</span><span class="sxs-lookup"><span data-stu-id="80821-143">**Technicals**</span></span>     
* <span data-ttu-id="80821-144">Nome firmware: nome del firmware</span><span class="sxs-lookup"><span data-stu-id="80821-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="80821-145">Versione firmware: versione del firmware</span><span class="sxs-lookup"><span data-stu-id="80821-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="80821-146">Modello dispositivo: modello del dispositivo</span><span class="sxs-lookup"><span data-stu-id="80821-146">Device model:    Device model</span></span>
* <span data-ttu-id="80821-147">Produttore dispositivo: produttore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="80821-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="80821-148">Versione applicazione: versione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="80821-148">Application version:    Application version</span></span>
* <span data-ttu-id="80821-149">Nome operatore: nome dell'operatore, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="80821-150">Paese operatore: paese dell'operatore, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="80821-151">Tipo di rete: tipo di rete</span><span class="sxs-lookup"><span data-stu-id="80821-151">Network type:    Network type</span></span>
* <span data-ttu-id="80821-152">Impostazioni locali: impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="80821-152">Locale:    Locale</span></span>
* <span data-ttu-id="80821-153">Dimensioni schermo: dimensioni dello schermo</span><span class="sxs-lookup"><span data-stu-id="80821-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="80821-154">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="80821-154">**Location**</span></span>      
* <span data-ttu-id="80821-155">Ultima area nota: paese, regione, località</span><span class="sxs-lookup"><span data-stu-id="80821-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="80821-156">Geo-fencing in tempo reale: elenco di punti di interesse (nome, azioni), POI circolare (nome, latitudine, longitudine, raggio in metri)</span><span class="sxs-lookup"><span data-stu-id="80821-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="80821-157">**Feedback di copertura**</span><span class="sxs-lookup"><span data-stu-id="80821-157">**Reach feedback**</span></span>     
* <span data-ttu-id="80821-158">Feedback annuncio: annuncio, feedback</span><span class="sxs-lookup"><span data-stu-id="80821-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="80821-159">Feedback sondaggio: sondaggio, feedback</span><span class="sxs-lookup"><span data-stu-id="80821-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="80821-160">Feedback risposta al sondaggio: feedback di risposta al sondaggio, domanda, opzione</span><span class="sxs-lookup"><span data-stu-id="80821-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="80821-161">Feedback push di dati: push di dati, feedback</span><span class="sxs-lookup"><span data-stu-id="80821-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="80821-162">**Rilevamento installazione**</span><span class="sxs-lookup"><span data-stu-id="80821-162">**Install Tracking**</span></span>     
* <span data-ttu-id="80821-163">Archivio: archivio, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="80821-164">Origine: origine, non definita</span><span class="sxs-lookup"><span data-stu-id="80821-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="80821-165">**Profilo utente**</span><span class="sxs-lookup"><span data-stu-id="80821-165">**User profile**</span></span>     
* <span data-ttu-id="80821-166">Sesso: maschio o femmina, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="80821-167">Data di nascita: operatore, data, non definita</span><span class="sxs-lookup"><span data-stu-id="80821-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="80821-168">Consenso: true o false, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="80821-169">**Informazioni sulle app**</span><span class="sxs-lookup"><span data-stu-id="80821-169">**App Info**</span></span>      
* <span data-ttu-id="80821-170">Stringa: stringa, non definita</span><span class="sxs-lookup"><span data-stu-id="80821-170">String:    String, undefined</span></span>
* <span data-ttu-id="80821-171">Data: operatore, data, non definita</span><span class="sxs-lookup"><span data-stu-id="80821-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="80821-172">Numero intero: operatore, numero, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="80821-173">Booleano: true o false, non definito</span><span class="sxs-lookup"><span data-stu-id="80821-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="80821-174">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="80821-174">**Segment**</span></span>    
* <span data-ttu-id="80821-175">Nome di segmenti (dall'elenco a discesa), esclusione (utenti di destinazione che non fanno parte del segmento).</span><span class="sxs-lookup"><span data-stu-id="80821-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
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

