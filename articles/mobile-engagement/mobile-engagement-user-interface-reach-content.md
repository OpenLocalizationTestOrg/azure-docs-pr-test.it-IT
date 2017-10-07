---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere contenuto
description: Informazioni su come contenuto di univoco hello toomanage di tipi diversi di hello di notifica push campagne in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="c101d-103">Come toomanage hello contenuto univoco di tipi diversi di hello delle campagne di notifica push</span><span class="sxs-lookup"><span data-stu-id="c101d-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="c101d-104">È possibile utilizzare una sezione di contenuto di un nuovo contenuto hello toomodify di campagne reach di annunci, viene eseguito il polling, effettua il push dei dati e riquadri (solo Windows Phone) hello.</span><span class="sxs-lookup"><span data-stu-id="c101d-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="c101d-105">impostazione del contenuto delle campagne Push Hello è toohello specifico tipo di campagna.</span><span class="sxs-lookup"><span data-stu-id="c101d-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="c101d-106">Tipi di contenuti:</span><span class="sxs-lookup"><span data-stu-id="c101d-106">Content types:</span></span>
* <span data-ttu-id="c101d-107">Annunci</span><span class="sxs-lookup"><span data-stu-id="c101d-107">Announcements</span></span>
* <span data-ttu-id="c101d-108">Sondaggi</span><span class="sxs-lookup"><span data-stu-id="c101d-108">Polls</span></span>
* <span data-ttu-id="c101d-109">Push di dati</span><span class="sxs-lookup"><span data-stu-id="c101d-109">Data pushes</span></span>
* <span data-ttu-id="c101d-110">Riquadri (solo per Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="c101d-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="c101d-111">Contenuto degli annunci</span><span class="sxs-lookup"><span data-stu-id="c101d-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="c101d-113">Scegliere il tipo di hello dell'annuncio:</span><span class="sxs-lookup"><span data-stu-id="c101d-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="c101d-114">Solo notifica: una semplice notifica standard.</span><span class="sxs-lookup"><span data-stu-id="c101d-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="c101d-115">Vale a dire che se un utente fa clic su di esso, non verranno visualizzato visualizzazioni aggiuntive, ma solo l'azione di hello associata tooit si verificherà.</span><span class="sxs-lookup"><span data-stu-id="c101d-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="c101d-116">Annuncio di testo: si tratta di una notifica che coinvolge hello utente toohave un'occhiata a una visualizzazione di testo.</span><span class="sxs-lookup"><span data-stu-id="c101d-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="c101d-117">Annuncio Web: si tratta di una notifica che coinvolge hello utente toohave un'occhiata a una visualizzazione web.</span><span class="sxs-lookup"><span data-stu-id="c101d-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="c101d-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c101d-118">See also</span></span>
* <span data-ttu-id="c101d-119">[Reach - Procedure - Annunci][Link 3]</span><span class="sxs-lookup"><span data-stu-id="c101d-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="c101d-120">Informazioni sugli annunci di visualizzazione Web:</span><span class="sxs-lookup"><span data-stu-id="c101d-120">About Web View Announcements:</span></span>
<span data-ttu-id="c101d-121">Occorrenze del criterio di hello "{deviceid}" nel codice hello HTML o JavaScript fornito qui verranno sostituite automaticamente con l'identificatore hello del dispositivo hello visualizzazione annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="c101d-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="c101d-122">Si tratta di un modo semplice tooretrieve Azure Mobile Engagement gli identificatori dei dispositivi in esterno ospitato nel back-office servizio web.</span><span class="sxs-lookup"><span data-stu-id="c101d-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="c101d-123">Se si desidera toocreate una procedura completa di schermata di visualizzazione web (senza hello predefinito azione e uscita pulsanti forniti da Microsoft) è possibile utilizzare hello seguente di funzioni dal codice JavaScript dell'annuncio di visualizzazione web:</span><span class="sxs-lookup"><span data-stu-id="c101d-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="c101d-124">eseguire l'azione dell'annuncio hello: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="c101d-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="c101d-125">uscire dall'annuncio hello: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="c101d-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="c101d-126">Scegliere l'azione:</span><span class="sxs-lookup"><span data-stu-id="c101d-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="c101d-127">Informazioni sugli URL di azione:</span><span class="sxs-lookup"><span data-stu-id="c101d-127">About Action URLs:</span></span>
<span data-ttu-id="c101d-128">qualsiasi URL che può essere interpretato dal sistema operativo di un dispositivo di destinazione può essere usato come un URL di azione.</span><span class="sxs-lookup"><span data-stu-id="c101d-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="c101d-129">Qualsiasi URL che l'applicazione potrebbe dedicato supporto (ad esempio, gli utenti toomake passare tooa particolare schermata) può essere utilizzato anche come URL di azione.</span><span class="sxs-lookup"><span data-stu-id="c101d-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="c101d-130">Ogni occorrenza di pattern hello {deviceid} viene sostituita automaticamente dall'identificatore hello del dispositivo hello operazione hello.</span><span class="sxs-lookup"><span data-stu-id="c101d-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="c101d-131">Può essere utilizzato tooeasily recuperare Azure Mobile Engagement gli identificatori dei dispositivi tramite un servizio web esterno ospitato nel back-office.</span><span class="sxs-lookup"><span data-stu-id="c101d-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="c101d-132">**Azioni di Android e iOS**</span><span class="sxs-lookup"><span data-stu-id="c101d-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="c101d-133">Aprire una pagina Web</span><span class="sxs-lookup"><span data-stu-id="c101d-133">Open a web page</span></span>
  * <span data-ttu-id="c101d-134">http://\[dominio-sito-Web\]</span><span class="sxs-lookup"><span data-stu-id="c101d-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="c101d-135">Esempio: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="c101d-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="c101d-136">Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c101d-136">Send an e-mail</span></span>
  * <span data-ttu-id="c101d-137">mailto:\[destinatario-messaggio\]?subject=\[oggetto\]&body=\[messaggio\]</span><span class="sxs-lookup"><span data-stu-id="c101d-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="c101d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="c101d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="c101d-139">Inviare un SMS</span><span class="sxs-lookup"><span data-stu-id="c101d-139">Send a SMS</span></span>
  * <span data-ttu-id="c101d-140">sms:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="c101d-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="c101d-141">Esempio:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="c101d-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="c101d-142">Comporre un numero di telefono</span><span class="sxs-lookup"><span data-stu-id="c101d-142">Dial a phone number</span></span>
  * <span data-ttu-id="c101d-143">tel:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="c101d-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="c101d-144">Esempio:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="c101d-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="c101d-145">**Azioni solo di Android**</span><span class="sxs-lookup"><span data-stu-id="c101d-145">**Android only actions**</span></span>
  * <span data-ttu-id="c101d-146">Scarica un'applicazione in Play Store hello</span><span class="sxs-lookup"><span data-stu-id="c101d-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="c101d-147">market://details?id=\[pacchetto app\]</span><span class="sxs-lookup"><span data-stu-id="c101d-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="c101d-148">Esempio:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="c101d-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="c101d-149">Avviare una ricerca di localizzazione geografica</span><span class="sxs-lookup"><span data-stu-id="c101d-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="c101d-150">geo:0,0?q=\[query di ricerca\]</span><span class="sxs-lookup"><span data-stu-id="c101d-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="c101d-151">Esempio:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="c101d-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="c101d-152">**Azioni solo di iOS**</span><span class="sxs-lookup"><span data-stu-id="c101d-152">**iOS only actions**</span></span>
  * <span data-ttu-id="c101d-153">Scarica un'applicazione in App Store hello</span><span class="sxs-lookup"><span data-stu-id="c101d-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="c101d-154">http://itunes.apple.com/[paese]/app/[nome app]/id[ID app]?mt=8</span><span class="sxs-lookup"><span data-stu-id="c101d-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="c101d-155">Esempio: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="c101d-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="c101d-156">Azioni di Windows</span><span class="sxs-lookup"><span data-stu-id="c101d-156">Windows Actions</span></span>
  * <span data-ttu-id="c101d-157">Aprire una pagina Web</span><span class="sxs-lookup"><span data-stu-id="c101d-157">Open a web page</span></span>
  * <span data-ttu-id="c101d-158">http://\[dominio-sito-Web\]</span><span class="sxs-lookup"><span data-stu-id="c101d-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="c101d-159">Esempio: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="c101d-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="c101d-160">Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c101d-160">Send an e-mail</span></span>
  * <span data-ttu-id="c101d-161">mailto:\[destinatario-messaggio\]?subject=\[oggetto\]&body=\[messaggio\]</span><span class="sxs-lookup"><span data-stu-id="c101d-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="c101d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="c101d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="c101d-163">Inviare un SMS (è necessario Skype Store App)</span><span class="sxs-lookup"><span data-stu-id="c101d-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="c101d-164">sms:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="c101d-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="c101d-165">Esempio:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="c101d-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="c101d-166">Comporre un numero di telefono (è necessario Skype Store App)</span><span class="sxs-lookup"><span data-stu-id="c101d-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="c101d-167">tel:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="c101d-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="c101d-168">Esempio:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="c101d-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="c101d-169">Scarica un'applicazione in Play Store hello</span><span class="sxs-lookup"><span data-stu-id="c101d-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="c101d-170">ms-windows-store:PDP?PFN=\[ID pacchetto app\]</span><span class="sxs-lookup"><span data-stu-id="c101d-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="c101d-171">Esempio:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="c101d-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="c101d-172">Avviare una ricerca in Bing Mappe</span><span class="sxs-lookup"><span data-stu-id="c101d-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="c101d-173">bingmaps:?q=\[query ricerca\]</span><span class="sxs-lookup"><span data-stu-id="c101d-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="c101d-174">Esempio:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="c101d-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="c101d-175">Usare uno schema personalizzato</span><span class="sxs-lookup"><span data-stu-id="c101d-175">Use a custom scheme</span></span>
  * <span data-ttu-id="c101d-176">\[schema personalizzato\]://\[parametri schema personalizzato\]</span><span class="sxs-lookup"><span data-stu-id="c101d-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="c101d-177">Esempio:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="c101d-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="c101d-178">Usare dati di un pacchetto (è necessario App Store per la lettura dell'estensione)</span><span class="sxs-lookup"><span data-stu-id="c101d-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="c101d-179">\[cartella\]\[dati\].\[estensione\]</span><span class="sxs-lookup"><span data-stu-id="c101d-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="c101d-180">Esempio:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="c101d-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="c101d-181">Creare un URL di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="c101d-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="c101d-182">Vedere la sezione "Impostazioni" di hello hello <UI Documentation> per istruzioni sulla creazione di un URL di verifica consentirà toodownload agli utenti una delle altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c101d-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="c101d-183">Definire i testi hello dell'annuncio</span><span class="sxs-lookup"><span data-stu-id="c101d-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="c101d-184">Compilare hello titolo, contenuto e testi pulsante dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="c101d-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="c101d-185">È possibile assegnare un gruppo di destinatari di una campagna futura in base ai suggerimenti reach hello di come gli utenti hanno risposto toothis campagna.</span><span class="sxs-lookup"><span data-stu-id="c101d-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="c101d-186">Destinatari possono essere basata su commenti e suggerimenti hello di indica se la campagna è stata appena inserita, risposta, azioni o chiusi.</span><span class="sxs-lookup"><span data-stu-id="c101d-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="c101d-187">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c101d-187">See also</span></span>
* <span data-ttu-id="c101d-188">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="c101d-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="c101d-189">Contenuto dei sondaggi</span><span class="sxs-lookup"><span data-stu-id="c101d-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="c101d-191">Compilare hello titolo, descrizione e testi pulsante dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="c101d-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="c101d-192">Quindi, aggiungere domande e scelte per hello risposte tooyour domande.</span><span class="sxs-lookup"><span data-stu-id="c101d-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="c101d-193">È possibile assegnare un gruppo di destinatari di una campagna futura in base ai suggerimenti reach hello di come gli utenti hanno risposto toothis campagna.</span><span class="sxs-lookup"><span data-stu-id="c101d-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="c101d-194">È possibile definire i destinatari a seconda che la campagna sia stata solo oggetto di push, che gli utenti abbiano risposto, eseguito un'azione o si siano scollegati.</span><span class="sxs-lookup"><span data-stu-id="c101d-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="c101d-195">Destinatari possono anche essere basata su commenti e suggerimenti risposte di polling, in cui scelta di domande e risposte hello vengono utilizzate come criteri.</span><span class="sxs-lookup"><span data-stu-id="c101d-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="c101d-196">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c101d-196">See also</span></span>
* <span data-ttu-id="c101d-197">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="c101d-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="c101d-198">Contenuto dei push di dati</span><span class="sxs-lookup"><span data-stu-id="c101d-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="c101d-200">Scegliere il tipo di hello dei dati:</span><span class="sxs-lookup"><span data-stu-id="c101d-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="c101d-201">Text</span><span class="sxs-lookup"><span data-stu-id="c101d-201">Text</span></span>
* <span data-ttu-id="c101d-202">Dati binari</span><span class="sxs-lookup"><span data-stu-id="c101d-202">Binary data</span></span>
* <span data-ttu-id="c101d-203">Dati Base64</span><span class="sxs-lookup"><span data-stu-id="c101d-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="c101d-204">Definire il contenuto di hello dei dati</span><span class="sxs-lookup"><span data-stu-id="c101d-204">Define hello content of your data</span></span>
* <span data-ttu-id="c101d-205">Se si selezionano i dati di testo toopush, copiare e incollare testo hello nella casella "contenuto" hello.</span><span class="sxs-lookup"><span data-stu-id="c101d-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="c101d-206">Se si seleziona toopush dati binary o base64, utilizzare tooupload pulsante di "caricare il file" hello il file.</span><span class="sxs-lookup"><span data-stu-id="c101d-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="c101d-207">È possibile assegnare un gruppo di destinatari di una campagna futura in base ai suggerimenti reach hello di come gli utenti hanno risposto toothis campagna.</span><span class="sxs-lookup"><span data-stu-id="c101d-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="c101d-208">È possibile definire i destinatari a seconda che la campagna sia stata solo oggetto di push, che gli utenti abbiano risposto, eseguito un'azione o si siano scollegati.</span><span class="sxs-lookup"><span data-stu-id="c101d-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="c101d-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c101d-209">See also</span></span>
* <span data-ttu-id="c101d-210">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="c101d-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="c101d-211">Contenuto dei riquadri (solo per Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="c101d-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="c101d-213">Definire il contenuto di hello del riquadro</span><span class="sxs-lookup"><span data-stu-id="c101d-213">Define hello content of your tile</span></span>
<span data-ttu-id="c101d-214">il payload di riquadro Hello è toobe testo hello visualizzati nel riquadro di hello dell'app in dispositivi Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c101d-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="c101d-215">Un riquadro push è hello Microsoft Push Notification Service (MPNS) versione un push nativo per Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c101d-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="c101d-216">Hello riquadro push type è hello solo push tipo che non dispone di una risposta e pertanto non è possibile compilare destinatari hello di campagne future risultati hello di una campagna push di riquadro.</span><span class="sxs-lookup"><span data-stu-id="c101d-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="c101d-217">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c101d-217">See also</span></span>
* <span data-ttu-id="c101d-218">[Documentazione dell'API - API Reach - Push nativo][Link 4]</span><span class="sxs-lookup"><span data-stu-id="c101d-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

