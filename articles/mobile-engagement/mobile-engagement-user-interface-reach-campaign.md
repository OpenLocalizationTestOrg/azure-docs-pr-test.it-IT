---
title: Interfaccia utente di Azure Mobile Engagement - Campagna Reach
description: Informazioni sulla creazione e sulla gestione di campagne di notifica push usando Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="7c99d-103">Come creare e gestire le campagne di notifica push</span><span class="sxs-lookup"><span data-stu-id="7c99d-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="7c99d-104">È possibile usare la sezione Reach dell'interfaccia utente per creare una nuova campagna di push con una formula complessa fornendo tutte le informazioni necessarie per inviare una notifica push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="7c99d-105">Le opzioni di una campagna di push variano leggermente in base ai quattro tipi di campagna: annunci, sondaggi, push di dati e riquadri (solo per Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="7c99d-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="7c99d-106">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-106">Option Applies to:</span></span>
* <span data-ttu-id="7c99d-107">Lingue: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-108">Campagna: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-109">Notifica: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="7c99d-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="7c99d-110">Contenuto: univoco per ogni tipo di campagna</span><span class="sxs-lookup"><span data-stu-id="7c99d-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="7c99d-111">Destinatari: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-112">Intervallo di tempo: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="7c99d-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="7c99d-113">Test: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="7c99d-115">Lingue</span><span class="sxs-lookup"><span data-stu-id="7c99d-115">Languages</span></span>
<span data-ttu-id="7c99d-116">È possibile usare il menu a discesa Lingue per inviare una versione diversa del push ai dispositivi configurati per l'uso di lingue diverse.</span><span class="sxs-lookup"><span data-stu-id="7c99d-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="7c99d-117">Per impostazione predefinita, tutti i dispositivi riceveranno lo stesso push indipendentemente dalla lingua usata.</span><span class="sxs-lookup"><span data-stu-id="7c99d-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="7c99d-118">Gli utenti con il dispositivo impostato su una lingua diversa riceveranno la versione del push nella lingua predefinita.</span><span class="sxs-lookup"><span data-stu-id="7c99d-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="7c99d-119">Molte opzioni della campagna di push consentono di specificare contenuto alternativo per ognuna delle lingue aggiuntive selezionate.</span><span class="sxs-lookup"><span data-stu-id="7c99d-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="7c99d-121">Le differenze di lingua si applicano a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-121">Language differences apply to:</span></span>
* <span data-ttu-id="7c99d-122">Lingue: è possibile selezionare lingue univoche oltre a quella predefinita</span><span class="sxs-lookup"><span data-stu-id="7c99d-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="7c99d-123">Campagna: uguale per tutte le lingue</span><span class="sxs-lookup"><span data-stu-id="7c99d-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="7c99d-124">Notifica: univoca per ogni lingua oltre a quella predefinita</span><span class="sxs-lookup"><span data-stu-id="7c99d-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="7c99d-125">Contenuto: univoco per ogni lingua oltre a quella predefinita</span><span class="sxs-lookup"><span data-stu-id="7c99d-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="7c99d-126">Destinatari: possono essere filtrati in base a un criterio di lingua distinto</span><span class="sxs-lookup"><span data-stu-id="7c99d-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="7c99d-127">Intervallo di tempo: uguale per tutte le lingue</span><span class="sxs-lookup"><span data-stu-id="7c99d-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="7c99d-128">Test: può essere inviato a tutte le lingue contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="7c99d-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="7c99d-129">Lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="7c99d-129">Supported Languages:</span></span>
* <span data-ttu-id="7c99d-130">Arabo (ar)</span><span class="sxs-lookup"><span data-stu-id="7c99d-130">Arabic (ar)</span></span> 
* <span data-ttu-id="7c99d-131">Bulgaro (bg)</span><span class="sxs-lookup"><span data-stu-id="7c99d-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="7c99d-132">Catalano (ca)</span><span class="sxs-lookup"><span data-stu-id="7c99d-132">Catalan (ca)</span></span> 
* <span data-ttu-id="7c99d-133">Cinese (zh)</span><span class="sxs-lookup"><span data-stu-id="7c99d-133">Chinese (zh)</span></span> 
* <span data-ttu-id="7c99d-134">Croato (h)</span><span class="sxs-lookup"><span data-stu-id="7c99d-134">Croatian (hr)</span></span> 
* <span data-ttu-id="7c99d-135">Ceco (cs)</span><span class="sxs-lookup"><span data-stu-id="7c99d-135">Czech (cs)</span></span> 
* <span data-ttu-id="7c99d-136">Danese (da)</span><span class="sxs-lookup"><span data-stu-id="7c99d-136">Danish (da)</span></span> 
* <span data-ttu-id="7c99d-137">Olandese (nl)</span><span class="sxs-lookup"><span data-stu-id="7c99d-137">Dutch (nl)</span></span> 
* <span data-ttu-id="7c99d-138">Inglese (en)</span><span class="sxs-lookup"><span data-stu-id="7c99d-138">English (en)</span></span> 
* <span data-ttu-id="7c99d-139">Finlandese (fi)</span><span class="sxs-lookup"><span data-stu-id="7c99d-139">Finnish (fi)</span></span> 
* <span data-ttu-id="7c99d-140">Francese (fr)</span><span class="sxs-lookup"><span data-stu-id="7c99d-140">French (fr)</span></span> 
* <span data-ttu-id="7c99d-141">Tedesco (de)</span><span class="sxs-lookup"><span data-stu-id="7c99d-141">German (de)</span></span> 
* <span data-ttu-id="7c99d-142">Greco (el)</span><span class="sxs-lookup"><span data-stu-id="7c99d-142">Greek (el)</span></span> 
* <span data-ttu-id="7c99d-143">Ebraico (he)</span><span class="sxs-lookup"><span data-stu-id="7c99d-143">Hebrew (he)</span></span> 
* <span data-ttu-id="7c99d-144">Hindi (hi)</span><span class="sxs-lookup"><span data-stu-id="7c99d-144">Hindi (hi)</span></span> 
* <span data-ttu-id="7c99d-145">Ungherese (hu)</span><span class="sxs-lookup"><span data-stu-id="7c99d-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="7c99d-146">Indonesiano (id)</span><span class="sxs-lookup"><span data-stu-id="7c99d-146">Indonesian (id)</span></span> 
* <span data-ttu-id="7c99d-147">Italiano (it)</span><span class="sxs-lookup"><span data-stu-id="7c99d-147">Italian (it)</span></span> 
* <span data-ttu-id="7c99d-148">Giapponese (ja)</span><span class="sxs-lookup"><span data-stu-id="7c99d-148">Japanese (ja)</span></span> 
* <span data-ttu-id="7c99d-149">Coreano (ko)</span><span class="sxs-lookup"><span data-stu-id="7c99d-149">Korean (ko)</span></span> 
* <span data-ttu-id="7c99d-150">Lettone (lv)</span><span class="sxs-lookup"><span data-stu-id="7c99d-150">Latvian (lv)</span></span> 
* <span data-ttu-id="7c99d-151">Lituano (lt)</span><span class="sxs-lookup"><span data-stu-id="7c99d-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="7c99d-152">Malese (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="7c99d-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="7c99d-153">Norvegese Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="7c99d-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="7c99d-154">Polacco (pl)</span><span class="sxs-lookup"><span data-stu-id="7c99d-154">Polish (pl)</span></span> 
* <span data-ttu-id="7c99d-155">Portoghese (pt)</span><span class="sxs-lookup"><span data-stu-id="7c99d-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="7c99d-156">Romeno (ro)</span><span class="sxs-lookup"><span data-stu-id="7c99d-156">Romanian (ro)</span></span> 
* <span data-ttu-id="7c99d-157">Russo (ru)</span><span class="sxs-lookup"><span data-stu-id="7c99d-157">Russian (ru)</span></span> 
* <span data-ttu-id="7c99d-158">Serbo (sr)</span><span class="sxs-lookup"><span data-stu-id="7c99d-158">Serbian (sr)</span></span> 
* <span data-ttu-id="7c99d-159">Slovacco (sk)</span><span class="sxs-lookup"><span data-stu-id="7c99d-159">Slovak (sk)</span></span> 
* <span data-ttu-id="7c99d-160">Sloveno (sl)</span><span class="sxs-lookup"><span data-stu-id="7c99d-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="7c99d-161">Spagnolo (es)</span><span class="sxs-lookup"><span data-stu-id="7c99d-161">Spanish (es)</span></span> 
* <span data-ttu-id="7c99d-162">Svedese (sv)</span><span class="sxs-lookup"><span data-stu-id="7c99d-162">Swedish (sv)</span></span> 
* <span data-ttu-id="7c99d-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="7c99d-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="7c99d-164">Tailandese (th)</span><span class="sxs-lookup"><span data-stu-id="7c99d-164">Thai (th)</span></span> 
* <span data-ttu-id="7c99d-165">Turco (tr)</span><span class="sxs-lookup"><span data-stu-id="7c99d-165">Turkish (tr)</span></span> 
* <span data-ttu-id="7c99d-166">Ucraino (Regno Unito)</span><span class="sxs-lookup"><span data-stu-id="7c99d-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="7c99d-167">Vietnamita (vi)</span><span class="sxs-lookup"><span data-stu-id="7c99d-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="7c99d-168">Campagna</span><span class="sxs-lookup"><span data-stu-id="7c99d-168">Campaign</span></span>
<span data-ttu-id="7c99d-169">È possibile usare la sezione Campagna per impostare il nome e la categoria della campagna nonché, se si intende ignorare la sezione dei destinatari di una campagna di push, inviare invece la campagna tramite l'API Reach (e alcuni elementi con l'API Push di basso livello).</span><span class="sxs-lookup"><span data-stu-id="7c99d-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="7c99d-170">Le categorie possono essere usate con un modello di notifica personalizzato per controllare le notifiche in-app in base alle impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="7c99d-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="7c99d-171">È possibile ottenere un elenco di "Categorie" esistenti tramite l'API Reach.</span><span class="sxs-lookup"><span data-stu-id="7c99d-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="7c99d-172">Se si usa l'opzione "Ignora destinatari, il push verrà inviato agli utenti tramite l'API" nella sezione "Campagna" di una campagna di copertura, la campagna NON sarà inviata automaticamente, ma sarà necessario inviarla manualmente tramite l'API Copertura.</span><span class="sxs-lookup"><span data-stu-id="7c99d-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="7c99d-174">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-174">Option Applies to:</span></span>
* <span data-ttu-id="7c99d-175">Nome: tutti</span><span class="sxs-lookup"><span data-stu-id="7c99d-175">Name:    All</span></span>
* <span data-ttu-id="7c99d-176">Categoria: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="7c99d-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="7c99d-177">Ignora i destinatari. Il push verrà inviato agli utenti tramite l'API: tutti</span><span class="sxs-lookup"><span data-stu-id="7c99d-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="7c99d-178">Notifica</span><span class="sxs-lookup"><span data-stu-id="7c99d-178">Notification</span></span>
<span data-ttu-id="7c99d-179">È possibile usare la sezione Notifica per definire le impostazioni di base per il push, tra cui: il titolo del push, il messaggio, un'immagine in-app oppure se può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="7c99d-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="7c99d-180">Molte impostazioni di notifica sono specifiche della piattaforma del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c99d-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="7c99d-181">È possibile scegliere se il push verrà inviato "in-app", "all'esterno dell'app" o in entrambi i modi.</span><span class="sxs-lookup"><span data-stu-id="7c99d-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="7c99d-182">Tenere presente che gli utenti possono accettare o rifiutare esplicitamente i push "all'esterno dell'app" a livello di sistema operativo sui propri dispositivi e Azure Mobile Engagement non potrà eseguire l'override di questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="7c99d-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="7c99d-183">Tenere presente, inoltre, che l'API Reach gestisce i push "in-app" e "all'esterno dell'app".</span><span class="sxs-lookup"><span data-stu-id="7c99d-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="7c99d-184">L'API Push può essere usata anche per gestire push "all'esterno dell'app". I push possono essere personalizzati con immagini o contenuto HTML, inclusi collegamenti diretti per il collegamento all'esterno dell'applicazione o a un'altra posizione nell'applicazione (è necessario l'SDK Android 2.1.0 o categorie successive).</span><span class="sxs-lookup"><span data-stu-id="7c99d-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="7c99d-185">È possibile modificare l'icona o il badge iOS e inviare testo o contenuto Web (una finestra popup con contenuto HTML, un collegamento URL a un'altra posizione all'interno o all'esterno dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="7c99d-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="7c99d-186">È inoltre possibile impostare lo squillo o la vibrazione dei dispositivi Android con il push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="7c99d-187">Tenere presente che perché un dispositivo squilli o vibri il file manifesto Android deve contenere le autorizzazioni dell'SDK corretto. Non esiste alcuno standard del settore per le dimensioni dell'immagine grande di Android perché le dimensioni dello schermo variano con ogni dispositivo. Tuttavia, le immagini da 400x100 sono adatte a quasi a tutte le dimensioni degli schermi.</span><span class="sxs-lookup"><span data-stu-id="7c99d-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="7c99d-188">Tipi di recapito:</span><span class="sxs-lookup"><span data-stu-id="7c99d-188">Delivery Types:</span></span>
* <span data-ttu-id="7c99d-189">Solo all'esterno dell'app: la notifica sarà recapitata quando l'utente non usa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c99d-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="7c99d-190">La notifica solo all'esterno dell'app richiede un certificato di Apple o Google (certificato APNS o GCM).</span><span class="sxs-lookup"><span data-stu-id="7c99d-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="7c99d-191">Solo in-app: la notifica viene visualizzata solo quando l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7c99d-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="7c99d-192">La notifica usa il sistema di recapito Capptain per raggiungere l'utente.</span><span class="sxs-lookup"><span data-stu-id="7c99d-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="7c99d-193">È possibile personalizzare completamente il layout o la visualizzazione del push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="7c99d-194">In qualsiasi momento: questa opzione assicura che una notifica venga inviata indipendentemente dal fatto che l'applicazione sia in esecuzione o meno.</span><span class="sxs-lookup"><span data-stu-id="7c99d-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="7c99d-196">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-196">Option Applies to:</span></span>
* <span data-ttu-id="7c99d-197">Notifica: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="7c99d-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="7c99d-198">Content</span><span class="sxs-lookup"><span data-stu-id="7c99d-198">Content</span></span>
<span data-ttu-id="7c99d-199">È possibile usare la sezione Contenuto per modificare il contenuto di annunci, sondaggi, push di dati e riquadri (solo per Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="7c99d-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="7c99d-200">L'impostazione del contenuto delle campagne di push è specifico per il tipo di campagna.</span><span class="sxs-lookup"><span data-stu-id="7c99d-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="7c99d-201">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7c99d-201">See also</span></span>
* <span data-ttu-id="7c99d-202">[Documentazione dell'interfaccia utente - Reach - Push del contenuto][Link 29]</span><span class="sxs-lookup"><span data-stu-id="7c99d-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="7c99d-204">Destinatari</span><span class="sxs-lookup"><span data-stu-id="7c99d-204">Audience</span></span>
<span data-ttu-id="7c99d-205">È possibile usare la sezione Destinatari per definire un elenco standard di elementi per limitare la campagna in base a criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7c99d-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="7c99d-206">L'insieme standard di opzioni per limitare i destinatari consente di effettuare il push solo per utenti nuovi, esistenti o nativi.</span><span class="sxs-lookup"><span data-stu-id="7c99d-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="7c99d-207">È inoltre possibile impostare una quota per limitare il numero di utenti che ricevono il push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="7c99d-208">È possibile modificare manualmente l'espressione per la modalità di filtro della campagna in modo da includere uno o più criteri per gli utenti di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7c99d-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="7c99d-209">È possibile digitare manualmente un'espressione di destinatari.</span><span class="sxs-lookup"><span data-stu-id="7c99d-209">You can manually type an audience expression.</span></span> <span data-ttu-id="7c99d-210">Tale espressione deve definire in modo esplicito la relazione tra i criteri.</span><span class="sxs-lookup"><span data-stu-id="7c99d-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="7c99d-211">Un criterio viene descritto da un identificatore che deve iniziare con una lettera maiuscola e non può contenere spazi.</span><span class="sxs-lookup"><span data-stu-id="7c99d-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="7c99d-212">La relazione tra i criteri può essere descritta usando gli operatori 'and', 'or', 'not' e '(',')'.</span><span class="sxs-lookup"><span data-stu-id="7c99d-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="7c99d-213">Esempio: "Criterion1 or (Criterion1 and not Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="7c99d-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="7c99d-214">con numerosi destinatari inclusi nelle campagne, la ricerca dei destinatari sul lato server può risultare lenta, soprattutto se si tenta di avviare più campagne contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7c99d-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="7c99d-215">Se possibile, iniziare una sola campagna alla volta.</span><span class="sxs-lookup"><span data-stu-id="7c99d-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="7c99d-216">Al massimo, avviare quattro campagne alla volta.</span><span class="sxs-lookup"><span data-stu-id="7c99d-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="7c99d-217">Eseguire il push solo per gli utenti attivi (casella di controllo "Effettua push solo degli utenti raggiungibili con Push nativo" e "Effettua push solo degli utenti attivi") in modo da individuare solo gli utenti che hanno l'app installata e che la usano ancora.</span><span class="sxs-lookup"><span data-stu-id="7c99d-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="7c99d-218">Una volta definiti i destinatari, è possibile usare il pulsante di simulazione per scoprire quanti utenti riceveranno il push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="7c99d-219">Verrà calcolato il numero di utenti noti potenzialmente appartenenti al gruppo di destinatari (si tratta di una stima basata su un campione casuale di utenti).</span><span class="sxs-lookup"><span data-stu-id="7c99d-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="7c99d-220">Tenere presente che anche gli utenti che hanno disinstallato l'applicazione fanno parte di questi destinatari, ma non possono essere raggiunti.</span><span class="sxs-lookup"><span data-stu-id="7c99d-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="7c99d-221">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7c99d-221">See also</span></span>
* <span data-ttu-id="7c99d-222">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="7c99d-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="7c99d-224">Modifica espressione</span><span class="sxs-lookup"><span data-stu-id="7c99d-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="7c99d-226">L'opzione Limitare i destinatari si applica a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="7c99d-227">Effettua push solo di un sottoinsieme di utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-228">Effettua push solo dei vecchi utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-229">Effettua push solo dei nuovi utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-230">Effettua push solo degli utenti inattivi: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="7c99d-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="7c99d-231">Effettua push solo degli utenti attivi: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="7c99d-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="7c99d-232">Effettua push solo degli utenti raggiungibili con Push nativo: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="7c99d-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="7c99d-233">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="7c99d-233">Time Frame</span></span>
<span data-ttu-id="7c99d-234">È possibile usare la sezione Intervallo di tempo per stabilire quando verrà inviato il push oppure omettere l'intervallo di tempo per avviare immediatamente la campagna.</span><span class="sxs-lookup"><span data-stu-id="7c99d-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="7c99d-235">Si tenga presente che se si utilizza il fuso orario degli utenti finali, la campagna potrebbe iniziare un giorno prima del previsto per gli utenti finali in Asia, per cui è consigliabile inviare piccoli gruppi di push alla volta finché tutti i fusi orari del mondo corrispondono all'intervallo di tempo impostato per la campagna.</span><span class="sxs-lookup"><span data-stu-id="7c99d-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="7c99d-236">L'utilizzo del fuso orario degli utenti finali, inoltre, può causare ritardi nelle campagne poiché è necessario chiedere l'ora al telefono prima di iniziare il push.</span><span class="sxs-lookup"><span data-stu-id="7c99d-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="7c99d-237">quando le campagne non hanno data di fine, i push possono essere memorizzati nella cache locale ed essere ancora visualizzati dopo aver completato manualmente la campagna.</span><span class="sxs-lookup"><span data-stu-id="7c99d-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="7c99d-238">Per evitare questo comportamento, specificare un'ora di fine per le campagne.</span><span class="sxs-lookup"><span data-stu-id="7c99d-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="7c99d-239">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7c99d-239">See also</span></span>
* <span data-ttu-id="7c99d-240">[Reach - Procedure - Pianificazione][Link 3]</span><span class="sxs-lookup"><span data-stu-id="7c99d-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="7c99d-242">Le impostazioni di applicano a:</span><span class="sxs-lookup"><span data-stu-id="7c99d-242">Settings Apply to:</span></span>
* <span data-ttu-id="7c99d-243">Intervallo di tempo: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="7c99d-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="7c99d-244">Test</span><span class="sxs-lookup"><span data-stu-id="7c99d-244">Test</span></span>
<span data-ttu-id="7c99d-245">È possibile usare la sezione Test per inviare il push al dispositivo di test prima di salvare la campagna.</span><span class="sxs-lookup"><span data-stu-id="7c99d-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="7c99d-246">Se sono state configurate lingue personalizzate per la campagna, è possibile testare il push in ciascuna lingua.</span><span class="sxs-lookup"><span data-stu-id="7c99d-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="7c99d-247">È possibile configurare un dispositivo di test da "Account personale".</span><span class="sxs-lookup"><span data-stu-id="7c99d-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="7c99d-248">Non vengono registrati dati sul lato server quando si usa il pulsante per "testare" i push, vengono registrati solo i dati per le campagne di push reali.</span><span class="sxs-lookup"><span data-stu-id="7c99d-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="7c99d-249">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7c99d-249">See also</span></span>
* <span data-ttu-id="7c99d-250">[Documentazione dell'interfaccia utente - Account personale][Link 14]</span><span class="sxs-lookup"><span data-stu-id="7c99d-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

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

