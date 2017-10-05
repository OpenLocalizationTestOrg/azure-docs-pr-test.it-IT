---
title: Interfaccia utente di Azure Mobile Engagement - Contenuti di Reach
description: Informazioni su come gestire il contenuto univoco dei diversi tipi di campagne di notifica push in Azure Mobile Engagement
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
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="11431-103">Come gestire il contenuto univoco dei diversi tipi di campagne di notifica push</span><span class="sxs-lookup"><span data-stu-id="11431-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="11431-104">È possibile usare la sezione Contenuto di una nuova campagna di copertura per modificare il contenuto di annunci, sondaggi, push di dati e riquadri (solo per Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="11431-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="11431-105">L'impostazione del contenuto delle campagne di push è specifico per il tipo di campagna.</span><span class="sxs-lookup"><span data-stu-id="11431-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="11431-106">Tipi di contenuti:</span><span class="sxs-lookup"><span data-stu-id="11431-106">Content types:</span></span>
* <span data-ttu-id="11431-107">Annunci</span><span class="sxs-lookup"><span data-stu-id="11431-107">Announcements</span></span>
* <span data-ttu-id="11431-108">Sondaggi</span><span class="sxs-lookup"><span data-stu-id="11431-108">Polls</span></span>
* <span data-ttu-id="11431-109">Push di dati</span><span class="sxs-lookup"><span data-stu-id="11431-109">Data pushes</span></span>
* <span data-ttu-id="11431-110">Riquadri (solo per Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="11431-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="11431-111">Contenuto degli annunci</span><span class="sxs-lookup"><span data-stu-id="11431-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="11431-113">Scegliere il tipo di annuncio:</span><span class="sxs-lookup"><span data-stu-id="11431-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="11431-114">Solo notifica: una semplice notifica standard.</span><span class="sxs-lookup"><span data-stu-id="11431-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="11431-115">Vale a dire che se un utente fa clic, non apparirà alcuna ulteriore visualizzazione, ma si verificherà semplicemente l'azione associata.</span><span class="sxs-lookup"><span data-stu-id="11431-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="11431-116">Annuncio di testo: una notifica che invita l'utente a esaminare una visualizzazione testo.</span><span class="sxs-lookup"><span data-stu-id="11431-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="11431-117">Annuncio Web: una notifica che incoraggia l'utente a esaminare una visualizzazione Web.</span><span class="sxs-lookup"><span data-stu-id="11431-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="11431-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11431-118">See also</span></span>
* <span data-ttu-id="11431-119">[Reach - Procedure - Annunci][Link 3]</span><span class="sxs-lookup"><span data-stu-id="11431-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="11431-120">Informazioni sugli annunci di visualizzazione Web:</span><span class="sxs-lookup"><span data-stu-id="11431-120">About Web View Announcements:</span></span>
<span data-ttu-id="11431-121">Le ricorrenze del modello "{deviceid}" nel codice HTML o nel codice JavaScript fornito in questa sezione verranno automaticamente sostituite dall'identificatore del dispositivo che visualizza l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="11431-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="11431-122">Si tratta di un metodo semplice per recuperare gli identificatori dei dispositivi di Azure Mobile Engagement in un servizio Web esterno ospitato sul back-office.</span><span class="sxs-lookup"><span data-stu-id="11431-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="11431-123">Se si desidera creare una visualizzazione Web a schermo intero (senza i pulsanti di azione e uscita predefiniti forniti), è possibile usare le funzioni seguenti dal codice JavaScript dell'annuncio di visualizzazione Web:</span><span class="sxs-lookup"><span data-stu-id="11431-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="11431-124">Per eseguire l'azione di annuncio: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="11431-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="11431-125">Per uscire dall'annuncio: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="11431-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="11431-126">Scegliere l'azione:</span><span class="sxs-lookup"><span data-stu-id="11431-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="11431-127">Informazioni sugli URL di azione:</span><span class="sxs-lookup"><span data-stu-id="11431-127">About Action URLs:</span></span>
<span data-ttu-id="11431-128">qualsiasi URL che può essere interpretato dal sistema operativo di un dispositivo di destinazione può essere usato come un URL di azione.</span><span class="sxs-lookup"><span data-stu-id="11431-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="11431-129">Qualsiasi URL dedicato che potrebbe essere supportato dall'applicazione (ad esempio per far sì che gli utenti passino a una schermata specifica) può essere usato anche come URL di azione.</span><span class="sxs-lookup"><span data-stu-id="11431-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="11431-130">Ogni ricorrenza del modello {deviceid} verrà automaticamente sostituita dall'identificatore del dispositivo che esegue l'azione.</span><span class="sxs-lookup"><span data-stu-id="11431-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="11431-131">Questo metodo consente di recuperare facilmente gli identificatori dei dispositivi di Azure Mobile Engagement tramite un servizio Web esterno ospitato sul back-office.</span><span class="sxs-lookup"><span data-stu-id="11431-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="11431-132">**Azioni di Android e iOS**</span><span class="sxs-lookup"><span data-stu-id="11431-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="11431-133">Aprire una pagina Web</span><span class="sxs-lookup"><span data-stu-id="11431-133">Open a web page</span></span>
  * <span data-ttu-id="11431-134">http://\[dominio-sito-Web\]</span><span class="sxs-lookup"><span data-stu-id="11431-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="11431-135">Esempio: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="11431-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="11431-136">Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="11431-136">Send an e-mail</span></span>
  * <span data-ttu-id="11431-137">mailto:\[destinatario-messaggio\]?subject=\[oggetto\]&body=\[messaggio\]</span><span class="sxs-lookup"><span data-stu-id="11431-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="11431-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="11431-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="11431-139">Inviare un SMS</span><span class="sxs-lookup"><span data-stu-id="11431-139">Send a SMS</span></span>
  * <span data-ttu-id="11431-140">sms:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="11431-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="11431-141">Esempio:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="11431-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="11431-142">Comporre un numero di telefono</span><span class="sxs-lookup"><span data-stu-id="11431-142">Dial a phone number</span></span>
  * <span data-ttu-id="11431-143">tel:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="11431-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="11431-144">Esempio:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="11431-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="11431-145">**Azioni solo di Android**</span><span class="sxs-lookup"><span data-stu-id="11431-145">**Android only actions**</span></span>
  * <span data-ttu-id="11431-146">Scaricare un'applicazione in Play Store</span><span class="sxs-lookup"><span data-stu-id="11431-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="11431-147">market://details?id=\[pacchetto app\]</span><span class="sxs-lookup"><span data-stu-id="11431-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="11431-148">Esempio:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="11431-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="11431-149">Avviare una ricerca di localizzazione geografica</span><span class="sxs-lookup"><span data-stu-id="11431-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="11431-150">geo:0,0?q=\[query di ricerca\]</span><span class="sxs-lookup"><span data-stu-id="11431-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="11431-151">Esempio:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="11431-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="11431-152">**Azioni solo di iOS**</span><span class="sxs-lookup"><span data-stu-id="11431-152">**iOS only actions**</span></span>
  * <span data-ttu-id="11431-153">Scaricare un'applicazione in App Store</span><span class="sxs-lookup"><span data-stu-id="11431-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="11431-154">http://itunes.apple.com/[paese]/app/[nome app]/id[ID app]?mt=8</span><span class="sxs-lookup"><span data-stu-id="11431-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="11431-155">Esempio: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="11431-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="11431-156">Azioni di Windows</span><span class="sxs-lookup"><span data-stu-id="11431-156">Windows Actions</span></span>
  * <span data-ttu-id="11431-157">Aprire una pagina Web</span><span class="sxs-lookup"><span data-stu-id="11431-157">Open a web page</span></span>
  * <span data-ttu-id="11431-158">http://\[dominio-sito-Web\]</span><span class="sxs-lookup"><span data-stu-id="11431-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="11431-159">Esempio: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="11431-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="11431-160">Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="11431-160">Send an e-mail</span></span>
  * <span data-ttu-id="11431-161">mailto:\[destinatario-messaggio\]?subject=\[oggetto\]&body=\[messaggio\]</span><span class="sxs-lookup"><span data-stu-id="11431-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="11431-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="11431-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="11431-163">Inviare un SMS (è necessario Skype Store App)</span><span class="sxs-lookup"><span data-stu-id="11431-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="11431-164">sms:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="11431-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="11431-165">Esempio:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="11431-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="11431-166">Comporre un numero di telefono (è necessario Skype Store App)</span><span class="sxs-lookup"><span data-stu-id="11431-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="11431-167">tel:\[numero-telefonico\]</span><span class="sxs-lookup"><span data-stu-id="11431-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="11431-168">Esempio:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="11431-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="11431-169">Scaricare un'applicazione in Play Store</span><span class="sxs-lookup"><span data-stu-id="11431-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="11431-170">ms-windows-store:PDP?PFN=\[ID pacchetto app\]</span><span class="sxs-lookup"><span data-stu-id="11431-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="11431-171">Esempio:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="11431-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="11431-172">Avviare una ricerca in Bing Mappe</span><span class="sxs-lookup"><span data-stu-id="11431-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="11431-173">bingmaps:?q=\[query ricerca\]</span><span class="sxs-lookup"><span data-stu-id="11431-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="11431-174">Esempio:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="11431-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="11431-175">Usare uno schema personalizzato</span><span class="sxs-lookup"><span data-stu-id="11431-175">Use a custom scheme</span></span>
  * <span data-ttu-id="11431-176">\[schema personalizzato\]://\[parametri schema personalizzato\]</span><span class="sxs-lookup"><span data-stu-id="11431-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="11431-177">Esempio:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="11431-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="11431-178">Usare dati di un pacchetto (è necessario App Store per la lettura dell'estensione)</span><span class="sxs-lookup"><span data-stu-id="11431-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="11431-179">\[cartella\]\[dati\].\[estensione\]</span><span class="sxs-lookup"><span data-stu-id="11431-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="11431-180">Esempio:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="11431-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="11431-181">Creare un URL di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="11431-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="11431-182">Per istruzioni sulla creazione di un URL di rilevamento che consente agli utenti di scaricare una delle altre applicazioni, vedere la sezione "Impostazioni" della <UI Documentation>.</span><span class="sxs-lookup"><span data-stu-id="11431-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="11431-183">Definire il testo dell'annuncio</span><span class="sxs-lookup"><span data-stu-id="11431-183">Define the texts of your announcement</span></span>
<span data-ttu-id="11431-184">Compilare il titolo, il contenuto e il testo dei pulsanti dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="11431-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="11431-185">È possibile definire i destinatari di una campagna futura in base al feedback di copertura sulla risposta degli utenti alla campagna corrente.</span><span class="sxs-lookup"><span data-stu-id="11431-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="11431-186">È possibile definire i destinatari a seconda che la campagna sia stata solo oggetto di push, che gli utenti abbiano risposto, abbiano eseguito un'azione o si siano scollegati.</span><span class="sxs-lookup"><span data-stu-id="11431-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="11431-187">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11431-187">See also</span></span>
* <span data-ttu-id="11431-188">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="11431-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="11431-189">Contenuto dei sondaggi</span><span class="sxs-lookup"><span data-stu-id="11431-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="11431-191">Compilare il titolo, la descrizione e il testo dei pulsanti dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="11431-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="11431-192">Aggiungere quindi domande e opzioni per le risposte alle domande.</span><span class="sxs-lookup"><span data-stu-id="11431-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="11431-193">È possibile definire i destinatari di una campagna futura in base al feedback di copertura sulla risposta degli utenti alla campagna corrente.</span><span class="sxs-lookup"><span data-stu-id="11431-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="11431-194">È possibile definire i destinatari a seconda che la campagna sia stata solo oggetto di push, che gli utenti abbiano risposto, eseguito un'azione o si siano scollegati.</span><span class="sxs-lookup"><span data-stu-id="11431-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="11431-195">La definizione dei destinatari può essere basata anche sul feedback di risposta ai sondaggi, dove domande e opzioni di risposta vengono usate come criteri.</span><span class="sxs-lookup"><span data-stu-id="11431-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="11431-196">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11431-196">See also</span></span>
* <span data-ttu-id="11431-197">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="11431-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="11431-198">Contenuto dei push di dati</span><span class="sxs-lookup"><span data-stu-id="11431-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="11431-200">Scegliere il tipo di testo dei dati:</span><span class="sxs-lookup"><span data-stu-id="11431-200">Choose the type of your data:</span></span>
* <span data-ttu-id="11431-201">Text</span><span class="sxs-lookup"><span data-stu-id="11431-201">Text</span></span>
* <span data-ttu-id="11431-202">Dati binari</span><span class="sxs-lookup"><span data-stu-id="11431-202">Binary data</span></span>
* <span data-ttu-id="11431-203">Dati Base64</span><span class="sxs-lookup"><span data-stu-id="11431-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="11431-204">Definire il contenuto dei dati</span><span class="sxs-lookup"><span data-stu-id="11431-204">Define the content of your data</span></span>
* <span data-ttu-id="11431-205">Se si seleziona il push dei dati di testo, copiare e incollare il testo nella casella "contenuto".</span><span class="sxs-lookup"><span data-stu-id="11431-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="11431-206">Se si seleziona il push dei dati binari o base64, usare il pulsante "carica il file" per caricare il file.</span><span class="sxs-lookup"><span data-stu-id="11431-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="11431-207">È possibile definire i destinatari di una campagna futura in base al feedback di copertura sulla risposta degli utenti alla campagna corrente.</span><span class="sxs-lookup"><span data-stu-id="11431-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="11431-208">È possibile definire i destinatari a seconda che la campagna sia stata solo oggetto di push, che gli utenti abbiano risposto, eseguito un'azione o si siano scollegati.</span><span class="sxs-lookup"><span data-stu-id="11431-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="11431-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11431-209">See also</span></span>
* <span data-ttu-id="11431-210">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="11431-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="11431-211">Contenuto dei riquadri (solo per Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="11431-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="11431-213">Definire il contenuto del riquadro</span><span class="sxs-lookup"><span data-stu-id="11431-213">Define the content of your tile</span></span>
<span data-ttu-id="11431-214">Il payload dei riquadri è il testo da visualizzare nel riquadro dell'app sui dispositivi Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="11431-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="11431-215">Un push di riquadri è la versione Servizio di notifica Push di Microsoft (MPNS) di un push nativo per Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="11431-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="11431-216">Il tipo di push di riquadri è l'unico tipo di push che non ha risposta e pertanto non è possibile creare i destinatari delle campagne future in base ai risultati di una campagna di push di riquadri.</span><span class="sxs-lookup"><span data-stu-id="11431-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="11431-217">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11431-217">See also</span></span>
* <span data-ttu-id="11431-218">[Documentazione dell'API - API Reach - Push nativo][Link 4]</span><span class="sxs-lookup"><span data-stu-id="11431-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

