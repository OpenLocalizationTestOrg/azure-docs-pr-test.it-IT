---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere campagna
description: Laern come toocreate e gestire le campagne di notifica push tramite Azure Mobile Engagement
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="dad2a-103">Come toocreate e gestire le campagne di notifica push</span><span class="sxs-lookup"><span data-stu-id="dad2a-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="dad2a-104">È possibile utilizzare hello Reach sezione dell'interfaccia utente di hello toocreate una nuova campagna Push con una formula complessa, fornendo tutte le informazioni di hello è necessario toosend una notifica push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="dad2a-105">Hello opzioni di una campagna Push variano leggermente a seconda dei tipi di hello quattro campagna: annunci, viene eseguito il polling, inserisce dati e riquadri (solo Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="dad2a-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="dad2a-106">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-106">Option Applies to:</span></span>
* <span data-ttu-id="dad2a-107">Lingue: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-108">Campagna: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-109">Notifica: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="dad2a-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="dad2a-110">Contenuto: univoco per ogni tipo di campagna</span><span class="sxs-lookup"><span data-stu-id="dad2a-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="dad2a-111">Destinatari: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-112">Intervallo di tempo: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="dad2a-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="dad2a-113">Test: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="dad2a-115">Lingue</span><span class="sxs-lookup"><span data-stu-id="dad2a-115">Languages</span></span>
<span data-ttu-id="dad2a-116">È possibile utilizzare l'elenco a discesa lingue hello menu toosend una versione diversa del toodevices Push impostate toouse diverse lingue.</span><span class="sxs-lookup"><span data-stu-id="dad2a-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="dad2a-117">Per impostazione predefinita, tutti i dispositivi riceveranno hello stesso Push indipendentemente dal linguaggio in cui sono impostati toouse.</span><span class="sxs-lookup"><span data-stu-id="dad2a-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="dad2a-118">Gli utenti con dispositivi set tooa diversa lingua hello lingua predefinita della riceveranno hello Push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="dad2a-119">Molte delle opzioni di campagna push hello consentono di contenuto alternativo toospecify per ognuna delle altre lingue hello selezionate.</span><span class="sxs-lookup"><span data-stu-id="dad2a-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="dad2a-121">Le differenze di lingua si applicano a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-121">Language differences apply to:</span></span>
* <span data-ttu-id="dad2a-122">Lingue: Linguaggi univoci possono essere selezionati nella lingua predefinita di addizione toohello</span><span class="sxs-lookup"><span data-stu-id="dad2a-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="dad2a-123">Campagna: uguale per tutte le lingue</span><span class="sxs-lookup"><span data-stu-id="dad2a-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="dad2a-124">Notifica: Univoco per ogni lingua inoltre toohello lingua predefinita</span><span class="sxs-lookup"><span data-stu-id="dad2a-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="dad2a-125">Il contenuto: Univoco per ogni lingua inoltre toohello lingua predefinita</span><span class="sxs-lookup"><span data-stu-id="dad2a-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="dad2a-126">Destinatari: possono essere filtrati in base a un criterio di lingua distinto</span><span class="sxs-lookup"><span data-stu-id="dad2a-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="dad2a-127">Intervallo di tempo: uguale per tutte le lingue</span><span class="sxs-lookup"><span data-stu-id="dad2a-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="dad2a-128">Test: Può essere inviato tooeach lingua alla volta</span><span class="sxs-lookup"><span data-stu-id="dad2a-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="dad2a-129">Lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="dad2a-129">Supported Languages:</span></span>
* <span data-ttu-id="dad2a-130">Arabo (ar)</span><span class="sxs-lookup"><span data-stu-id="dad2a-130">Arabic (ar)</span></span> 
* <span data-ttu-id="dad2a-131">Bulgaro (bg)</span><span class="sxs-lookup"><span data-stu-id="dad2a-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="dad2a-132">Catalano (ca)</span><span class="sxs-lookup"><span data-stu-id="dad2a-132">Catalan (ca)</span></span> 
* <span data-ttu-id="dad2a-133">Cinese (zh)</span><span class="sxs-lookup"><span data-stu-id="dad2a-133">Chinese (zh)</span></span> 
* <span data-ttu-id="dad2a-134">Croato (h)</span><span class="sxs-lookup"><span data-stu-id="dad2a-134">Croatian (hr)</span></span> 
* <span data-ttu-id="dad2a-135">Ceco (cs)</span><span class="sxs-lookup"><span data-stu-id="dad2a-135">Czech (cs)</span></span> 
* <span data-ttu-id="dad2a-136">Danese (da)</span><span class="sxs-lookup"><span data-stu-id="dad2a-136">Danish (da)</span></span> 
* <span data-ttu-id="dad2a-137">Olandese (nl)</span><span class="sxs-lookup"><span data-stu-id="dad2a-137">Dutch (nl)</span></span> 
* <span data-ttu-id="dad2a-138">Inglese (en)</span><span class="sxs-lookup"><span data-stu-id="dad2a-138">English (en)</span></span> 
* <span data-ttu-id="dad2a-139">Finlandese (fi)</span><span class="sxs-lookup"><span data-stu-id="dad2a-139">Finnish (fi)</span></span> 
* <span data-ttu-id="dad2a-140">Francese (fr)</span><span class="sxs-lookup"><span data-stu-id="dad2a-140">French (fr)</span></span> 
* <span data-ttu-id="dad2a-141">Tedesco (de)</span><span class="sxs-lookup"><span data-stu-id="dad2a-141">German (de)</span></span> 
* <span data-ttu-id="dad2a-142">Greco (el)</span><span class="sxs-lookup"><span data-stu-id="dad2a-142">Greek (el)</span></span> 
* <span data-ttu-id="dad2a-143">Ebraico (he)</span><span class="sxs-lookup"><span data-stu-id="dad2a-143">Hebrew (he)</span></span> 
* <span data-ttu-id="dad2a-144">Hindi (hi)</span><span class="sxs-lookup"><span data-stu-id="dad2a-144">Hindi (hi)</span></span> 
* <span data-ttu-id="dad2a-145">Ungherese (hu)</span><span class="sxs-lookup"><span data-stu-id="dad2a-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="dad2a-146">Indonesiano (id)</span><span class="sxs-lookup"><span data-stu-id="dad2a-146">Indonesian (id)</span></span> 
* <span data-ttu-id="dad2a-147">Italiano (it)</span><span class="sxs-lookup"><span data-stu-id="dad2a-147">Italian (it)</span></span> 
* <span data-ttu-id="dad2a-148">Giapponese (ja)</span><span class="sxs-lookup"><span data-stu-id="dad2a-148">Japanese (ja)</span></span> 
* <span data-ttu-id="dad2a-149">Coreano (ko)</span><span class="sxs-lookup"><span data-stu-id="dad2a-149">Korean (ko)</span></span> 
* <span data-ttu-id="dad2a-150">Lettone (lv)</span><span class="sxs-lookup"><span data-stu-id="dad2a-150">Latvian (lv)</span></span> 
* <span data-ttu-id="dad2a-151">Lituano (lt)</span><span class="sxs-lookup"><span data-stu-id="dad2a-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="dad2a-152">Malese (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="dad2a-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="dad2a-153">Norvegese Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="dad2a-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="dad2a-154">Polacco (pl)</span><span class="sxs-lookup"><span data-stu-id="dad2a-154">Polish (pl)</span></span> 
* <span data-ttu-id="dad2a-155">Portoghese (pt)</span><span class="sxs-lookup"><span data-stu-id="dad2a-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="dad2a-156">Romeno (ro)</span><span class="sxs-lookup"><span data-stu-id="dad2a-156">Romanian (ro)</span></span> 
* <span data-ttu-id="dad2a-157">Russo (ru)</span><span class="sxs-lookup"><span data-stu-id="dad2a-157">Russian (ru)</span></span> 
* <span data-ttu-id="dad2a-158">Serbo (sr)</span><span class="sxs-lookup"><span data-stu-id="dad2a-158">Serbian (sr)</span></span> 
* <span data-ttu-id="dad2a-159">Slovacco (sk)</span><span class="sxs-lookup"><span data-stu-id="dad2a-159">Slovak (sk)</span></span> 
* <span data-ttu-id="dad2a-160">Sloveno (sl)</span><span class="sxs-lookup"><span data-stu-id="dad2a-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="dad2a-161">Spagnolo (es)</span><span class="sxs-lookup"><span data-stu-id="dad2a-161">Spanish (es)</span></span> 
* <span data-ttu-id="dad2a-162">Svedese (sv)</span><span class="sxs-lookup"><span data-stu-id="dad2a-162">Swedish (sv)</span></span> 
* <span data-ttu-id="dad2a-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="dad2a-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="dad2a-164">Tailandese (th)</span><span class="sxs-lookup"><span data-stu-id="dad2a-164">Thai (th)</span></span> 
* <span data-ttu-id="dad2a-165">Turco (tr)</span><span class="sxs-lookup"><span data-stu-id="dad2a-165">Turkish (tr)</span></span> 
* <span data-ttu-id="dad2a-166">Ucraino (Regno Unito)</span><span class="sxs-lookup"><span data-stu-id="dad2a-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="dad2a-167">Vietnamita (vi)</span><span class="sxs-lookup"><span data-stu-id="dad2a-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="dad2a-168">Campagna</span><span class="sxs-lookup"><span data-stu-id="dad2a-168">Campaign</span></span>
<span data-ttu-id="dad2a-169">È possibile utilizzare hello campagna sezione tooset hello nome e la categoria della campagna anche come se si prevede di sezione di destinatari hello tooignore di una campagna Push e invece di inviare questa campagna tramite l'API Reach hello (e alcuni elementi con livello basso hello API Push).</span><span class="sxs-lookup"><span data-stu-id="dad2a-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="dad2a-170">Le categorie possono essere usate con notifiche. nell'applicazione toocontrol un modello di notifica personalizzata in base alle impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="dad2a-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="dad2a-171">È possibile ottenere un elenco di "Categorie" esistente tramite l'API Reach hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="dad2a-172">Se l'opzione hello "Ignora destinatari push verrà inviato toousers tramite API hello" nella sezione "Campagna" hello di una campagna di copertura, campagna hello non invierà automaticamente, sarà necessario toosend manualmente tramite l'API Reach hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="dad2a-174">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-174">Option Applies to:</span></span>
* <span data-ttu-id="dad2a-175">Nome: tutti</span><span class="sxs-lookup"><span data-stu-id="dad2a-175">Name:    All</span></span>
* <span data-ttu-id="dad2a-176">Categoria: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="dad2a-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="dad2a-177">Ignora i destinatari push verrà inviato toousers tramite API hello: tutti</span><span class="sxs-lookup"><span data-stu-id="dad2a-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="dad2a-178">Notifica</span><span class="sxs-lookup"><span data-stu-id="dad2a-178">Notification</span></span>
<span data-ttu-id="dad2a-179">È possibile utilizzare le impostazioni di base hello notifica sezione tooset per il push, tra cui: hello titolo di hello Push, il messaggio hello, un'immagine all'interno dell'applicazione, o se è non rilevanti.</span><span class="sxs-lookup"><span data-stu-id="dad2a-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="dad2a-180">Molte impostazioni di notifica sono toohello specifico della piattaforma del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dad2a-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="dad2a-181">È possibile scegliere se il push verrà inviato "in-app", "all'esterno dell'app" o in entrambi i modi.</span><span class="sxs-lookup"><span data-stu-id="dad2a-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="dad2a-182">(Tenere presente che gli utenti possono "opt-in" o "rifiutare esplicitamente" "fuori app" inserisce nel sistema operativo hello livello nei propri dispositivi e Azure Mobile Engagement non essere in grado di toooverride questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="dad2a-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="dad2a-183">Ricordare anche che gestisce l'API Reach hello "nell'app" e "out-of-app" effettua il push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="dad2a-184">Hello API Push può essere utilizzati toohandle "out dell'app" inserisce troppo). Push possono essere personalizzati con immagini o contenuto HTML, inclusi i collegamenti diretti per il collegamento all'esterno del percorso App o tooanother nell'App (SDK Android 2.1.0 o successive categorie preventivo richieste).</span><span class="sxs-lookup"><span data-stu-id="dad2a-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="dad2a-185">È possibile modificare il badge di iOS o di un'icona hello e inviare il contenuto di testo o web (un popup con html, URL collegamento tooanother percorso del contenuto all'interno o all'esterno di hello app).</span><span class="sxs-lookup"><span data-stu-id="dad2a-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="dad2a-186">È anche possibile fai squillare i dispositivi Android o vibrare con hello Push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="dad2a-187">(Tenere presente che sarà necessario hello corrette autorizzazioni SDK in Android tooring file manifesto o vibrare un dispositivo). Non esiste alcuno standard del settore per le dimensioni dell'immagine grande di Android perché le dimensioni dello schermo variano con ogni dispositivo. Tuttavia, le immagini da 400x100 sono adatte a quasi a tutte le dimensioni degli schermi.</span><span class="sxs-lookup"><span data-stu-id="dad2a-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="dad2a-188">Tipi di recapito:</span><span class="sxs-lookup"><span data-stu-id="dad2a-188">Delivery Types:</span></span>
* <span data-ttu-id="dad2a-189">All'esterno dell'app solo: notifica hello verrà recapitata quando l'utente hello non utilizza un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="dad2a-190">Hello fuori notifica solo app richiede un certificato di Apple o Google (certificato APNS o GCM).</span><span class="sxs-lookup"><span data-stu-id="dad2a-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="dad2a-191">Nell'applicazione solo: notifica hello viene visualizzata solo quando un'applicazione hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dad2a-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="dad2a-192">notifica di Hello utilizza hello Capptain recapito sistema tooreach hello utente.</span><span class="sxs-lookup"><span data-stu-id="dad2a-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="dad2a-193">È possibile personalizzare completamente hello layout/visualizzazione il push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="dad2a-194">In qualsiasi momento: Questa opzione assicura che si invia una notifica che o meno, è in esecuzione l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="dad2a-196">L'opzione si applica a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-196">Option Applies to:</span></span>
* <span data-ttu-id="dad2a-197">Notifica: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="dad2a-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="dad2a-198">Content</span><span class="sxs-lookup"><span data-stu-id="dad2a-198">Content</span></span>
<span data-ttu-id="dad2a-199">È possibile utilizzare contenuto hello di hello sezione contenuto toomodify di annunci, viene eseguito il polling, effettua il push dei dati e riquadri (solo Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="dad2a-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="dad2a-200">impostazione del contenuto delle campagne Push Hello è toohello specifico tipo di campagna.</span><span class="sxs-lookup"><span data-stu-id="dad2a-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="dad2a-201">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dad2a-201">See also</span></span>
* <span data-ttu-id="dad2a-202">[Documentazione dell'interfaccia utente - Reach - Push del contenuto][Link 29]</span><span class="sxs-lookup"><span data-stu-id="dad2a-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="dad2a-204">Audience</span><span class="sxs-lookup"><span data-stu-id="dad2a-204">Audience</span></span>
<span data-ttu-id="dad2a-205">La campagna o i limiti di una campagna in base ai criteri personalizzati, è possibile utilizzare hello destinatari sezione toodefine un elenco di elementi toolimit standard.</span><span class="sxs-lookup"><span data-stu-id="dad2a-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="dad2a-206">set di opzioni tooLimit standard Hello i destinatari consentono agli utenti di nuovo o quello precedente tooeither toopush o solo gli utenti di push nativo.</span><span class="sxs-lookup"><span data-stu-id="dad2a-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="dad2a-207">È inoltre possibile impostare un numero di hello toolimit di quota di utenti che ricevono push hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="dad2a-208">È possibile modificare manualmente l'espressione hello per la modalità la campagna tooinclude filtrati uno o più utenti tootarget criterio.</span><span class="sxs-lookup"><span data-stu-id="dad2a-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="dad2a-209">È possibile digitare manualmente un'espressione di destinatari.</span><span class="sxs-lookup"><span data-stu-id="dad2a-209">You can manually type an audience expression.</span></span> <span data-ttu-id="dad2a-210">Un'espressione di questo tipo deve definire esplicitamente relazione hello tra criteri.</span><span class="sxs-lookup"><span data-stu-id="dad2a-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="dad2a-211">Un criterio viene descritto da un identificatore che deve iniziare con una lettera maiuscola e non può contenere spazi.</span><span class="sxs-lookup"><span data-stu-id="dad2a-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="dad2a-212">relazione Hello tra criteri hello può essere descritte con 'and', 'or', 'not' gli operatori, nonché '(',')'.</span><span class="sxs-lookup"><span data-stu-id="dad2a-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="dad2a-213">Esempio: "Criterion1 or (Criterion1 and not Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="dad2a-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="dad2a-214">Con numerosi utenti inclusi in campagne, sul lato server hello come destinazione di analisi può richiedere molto tempo, soprattutto se si tenta di toostart più campagne in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="dad2a-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="dad2a-215">Se possibile, iniziare una sola campagna alla volta.</span><span class="sxs-lookup"><span data-stu-id="dad2a-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="dad2a-216">In hello massimo inizio solo quattro campagne alla volta.</span><span class="sxs-lookup"><span data-stu-id="dad2a-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="dad2a-217">Push solo tooyour utenti attivi (casella di controllo "coinvolgere solo gli utenti che possono essere raggiunto tramite Push nativo" e "Coinvolgere solo gli utenti attivi") in modo che solo gli utenti che è ancora installata App hello e utilizzano saranno necessario toobe analizzati.</span><span class="sxs-lookup"><span data-stu-id="dad2a-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="dad2a-218">Dopo aver definito i destinatari, è possibile utilizzare hello simulare pulsante toofind il numero di utenti che riceveranno questo Push.</span><span class="sxs-lookup"><span data-stu-id="dad2a-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="dad2a-219">Questo calcola hello numero di utenti noti potenzialmente destinato al gruppo di destinatari (si tratta di una stima basata su un campione casuale di utenti).</span><span class="sxs-lookup"><span data-stu-id="dad2a-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="dad2a-220">Tenere presente che gli utenti che hanno disinstallato l'applicazione hello fanno parte del gruppo di destinatari, ma non possono essere raggiunto.</span><span class="sxs-lookup"><span data-stu-id="dad2a-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="dad2a-221">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dad2a-221">See also</span></span>
* <span data-ttu-id="dad2a-222">[Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="dad2a-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="dad2a-224">Modifica espressione</span><span class="sxs-lookup"><span data-stu-id="dad2a-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="dad2a-226">L'opzione Limitare i destinatari si applica a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="dad2a-227">Effettua push solo di un sottoinsieme di utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-228">Effettua push solo dei vecchi utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-229">Effettua push solo dei nuovi utenti: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-230">Effettua push solo degli utenti inattivi: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="dad2a-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="dad2a-231">Effettua push solo degli utenti attivi: tutti (annunci, sondaggi, push di dati e riquadri)</span><span class="sxs-lookup"><span data-stu-id="dad2a-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="dad2a-232">Effettua push solo degli utenti raggiungibili con Push nativo: annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="dad2a-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="dad2a-233">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="dad2a-233">Time Frame</span></span>
<span data-ttu-id="dad2a-234">È possibile utilizzare hello tempo sezione tooset quando hello push verrà inviato o è possibile lasciare immediatamente campagna hello toostart vuoto di hello intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="dad2a-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="dad2a-235">Tenere presente che con fuso orario hello degli utenti finali può iniziare campagna hello un giorno prima di quanto si prevede che per gli utenti finali in Asia e invia batch di piccole dimensioni di push contemporaneamente fino a quando tutti i fusi orari hello world corrispondenza hello intervallo di tempo impostato per la campagna.</span><span class="sxs-lookup"><span data-stu-id="dad2a-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="dad2a-236">Con fuso orario hello degli utenti finali possono inoltre causare ritardi nelle campagne poiché dispone ora di hello toorequest da un telefono hello prima di iniziare il push di hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="dad2a-237">quando le campagne non hanno data di fine, i push possono essere memorizzati nella cache locale ed essere ancora visualizzati dopo aver completato manualmente la campagna.</span><span class="sxs-lookup"><span data-stu-id="dad2a-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="dad2a-238">tooavoid questo comportamento, specifica un'ora di fine per le campagne.</span><span class="sxs-lookup"><span data-stu-id="dad2a-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="dad2a-239">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dad2a-239">See also</span></span>
* <span data-ttu-id="dad2a-240">[Reach - Procedure - Pianificazione][Link 3]</span><span class="sxs-lookup"><span data-stu-id="dad2a-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="dad2a-242">Le impostazioni di applicano a:</span><span class="sxs-lookup"><span data-stu-id="dad2a-242">Settings Apply to:</span></span>
* <span data-ttu-id="dad2a-243">Intervallo di tempo: annunci, sondaggi e riquadri</span><span class="sxs-lookup"><span data-stu-id="dad2a-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="dad2a-244">Test</span><span class="sxs-lookup"><span data-stu-id="dad2a-244">Test</span></span>
<span data-ttu-id="dad2a-245">È possibile utilizzare il dispositivo di un test di push tooyour hello Test sezione toosend prima del salvataggio della campagna hello.</span><span class="sxs-lookup"><span data-stu-id="dad2a-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="dad2a-246">Se è stato configurato tutte le lingue per la campagna personalizzate, è possibile testare push hello in ciascuna lingua.</span><span class="sxs-lookup"><span data-stu-id="dad2a-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="dad2a-247">È possibile configurare un dispositivo di test da "Account personale".</span><span class="sxs-lookup"><span data-stu-id="dad2a-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="dad2a-248">Inserisce alcun lato server vengono registrati i dati quando si utilizza il pulsante hello troppo "non test", i dati vengono registrati solo per le campagne push reale.</span><span class="sxs-lookup"><span data-stu-id="dad2a-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="dad2a-249">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dad2a-249">See also</span></span>
* <span data-ttu-id="dad2a-250">[Documentazione dell'interfaccia utente - Account personale][Link 14]</span><span class="sxs-lookup"><span data-stu-id="dad2a-250">[UI Documentation - My Account][Link 14]</span></span>

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

