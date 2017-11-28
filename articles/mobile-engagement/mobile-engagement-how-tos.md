---
title: Interfaccia utente di Azure Mobile Engagement - Procedure di Reach
description: Panoramica dell'interfaccia utente di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 33a0a9d0c399cb7f0a791c4c16dde2e2d62364ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="ec45e-103">Come iniziare a usare e gestire le notifiche push per raggiungere gli utenti finali</span><span class="sxs-lookup"><span data-stu-id="ec45e-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="ec45e-104">Dopo l'integrazione completa dell'SDK nell'app, è possibile iniziare a usare la sezione Reach dell'interfaccia utente per inviare notifiche push agli utenti dell'app.</span><span class="sxs-lookup"><span data-stu-id="ec45e-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="ec45e-105">Creare la prima campagna di notifica push</span><span class="sxs-lookup"><span data-stu-id="ec45e-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="ec45e-106">Verificare che Reach sia integrato nell'app con l'SDK.</span><span class="sxs-lookup"><span data-stu-id="ec45e-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="ec45e-107">Selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ec45e-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="ec45e-109">Andare alla sezione "Reach" e fare clic su "Nuovo annuncio".</span><span class="sxs-lookup"><span data-stu-id="ec45e-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="ec45e-111">Creare una nuova campagna e assegnarle un nome.</span><span class="sxs-lookup"><span data-stu-id="ec45e-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="ec45e-113">Selezionare la modalità di recapito della notifica, ad esempio Solo in-app.</span><span class="sxs-lookup"><span data-stu-id="ec45e-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="ec45e-115">Creare il messaggio di cui si desidera effettuare il push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="ec45e-117">È possibile scrivere un titolo nella notifica (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="ec45e-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="ec45e-118">Scrivere il contenuto del messaggio push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-118">Write push message content.</span></span>
* <span data-ttu-id="ec45e-119">È possibile caricare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="ec45e-119">You can upload an image.</span></span> <span data-ttu-id="ec45e-120">Tenere presente che le dimensioni del file non possono superare i 32.768 byte.</span><span class="sxs-lookup"><span data-stu-id="ec45e-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="ec45e-121">È anche possibile selezionare altre opzioni, ma, per l'obiettivo di questa esercitazione, se ne parlerà in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ec45e-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="ec45e-122">Selezionare il tipo di contenuto Solo notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="ec45e-124">Creare la campagna push che verrà visualizzata nell'elenco di campagne.</span><span class="sxs-lookup"><span data-stu-id="ec45e-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="ec45e-126">Testare la campagna di notifica push</span><span class="sxs-lookup"><span data-stu-id="ec45e-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="ec45e-128">Registrare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec45e-128">Register your device.</span></span>
* <span data-ttu-id="ec45e-129">Fare clic sulla casella di controllo del dispositivo di cui si vuole effettuare il push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="ec45e-130">Fare clic sul pulsante "Test" per inviare il push al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec45e-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="ec45e-132">Attivare la campagna.</span><span class="sxs-lookup"><span data-stu-id="ec45e-132">Activate the campaign</span></span>

![Test3][10]

* <span data-ttu-id="ec45e-134">Ora che la campagna è stata creata, è sufficiente attivarla per effettuare il push della notifica agli utenti.</span><span class="sxs-lookup"><span data-stu-id="ec45e-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="ec45e-135">Inviare push personalizzati</span><span class="sxs-lookup"><span data-stu-id="ec45e-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="ec45e-136">Questo esempio crea un push in cui viene immesso un codice di sconto personalizzato nella notifica push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="ec45e-138">La personalizzazione viene ottenuta sostituendo un marcatore da un tag app info, quindi sarà necessario assicurarsi che prima siano stati definiti i valori app-info appropriati per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ec45e-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="ec45e-139">In questo esempio, per gli utenti di destinazione verrà definito un tag app info denominato rebate_code.</span><span class="sxs-lookup"><span data-stu-id="ec45e-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="ec45e-140">Come si può vedere sopra, il contenuto della notifica push include il marker ${rebate_code} che indicherà che deve essere sostituito dal contenuto effettivo del tag app info.</span><span class="sxs-lookup"><span data-stu-id="ec45e-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="ec45e-141">se il tag app info non è definito per l'utente, l'utente non riceverà il push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="ec45e-142">Risultato</span><span class="sxs-lookup"><span data-stu-id="ec45e-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="ec45e-144">È possibile personalizzare ulteriormente il testo della notifica</span><span class="sxs-lookup"><span data-stu-id="ec45e-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="ec45e-146">Includendo il titolo della notifica</span><span class="sxs-lookup"><span data-stu-id="ec45e-146">Including the title of the notification,</span></span>
* <span data-ttu-id="ec45e-147">e il contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ec45e-147">And the content of the message.</span></span>
* <span data-ttu-id="ec45e-148">Scegliere il tipo di annuncio (visualizzazione testo o Web)</span><span class="sxs-lookup"><span data-stu-id="ec45e-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="ec45e-150">Il corpo di un annuncio può anche essere personalizzato con:</span><span class="sxs-lookup"><span data-stu-id="ec45e-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="ec45e-151">L'URL di azione, nel caso in cui si voglia personalizzare la pagina di destinazione</span><span class="sxs-lookup"><span data-stu-id="ec45e-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="ec45e-152">Il titolo</span><span class="sxs-lookup"><span data-stu-id="ec45e-152">The title,</span></span>
* <span data-ttu-id="ec45e-153">Il corpo del messaggio</span><span class="sxs-lookup"><span data-stu-id="ec45e-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="ec45e-154">Differenziare la notifica push (all'interno o all'esterno dell'app)</span><span class="sxs-lookup"><span data-stu-id="ec45e-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="ec45e-155">Scegliere il tipo di notifica di cui si effettuerà il push, selezionare l'applicazione, andare alla sezione "Reach", selezionare o creare una campagna push e andare alla sezione "Notifica".</span><span class="sxs-lookup"><span data-stu-id="ec45e-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="ec45e-156">Fare clic su "modalità di recapito" desiderata.</span><span class="sxs-lookup"><span data-stu-id="ec45e-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="ec45e-157">Fare clic sulla casella di controllo "Limita attività" per inviare la notifica solo quando vengono eseguite attività specifiche (schermate).</span><span class="sxs-lookup"><span data-stu-id="ec45e-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="ec45e-159">Modalità di recapito "Solo all'esterno dell'app"</span><span class="sxs-lookup"><span data-stu-id="ec45e-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="ec45e-161">La modalità di recapito "Solo all'esterno dell'app" fornisce la notifica push quando l'applicazione è chiusa.</span><span class="sxs-lookup"><span data-stu-id="ec45e-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="ec45e-162">Questa è la notifica push standard.</span><span class="sxs-lookup"><span data-stu-id="ec45e-162">This is the standard push notification.</span></span>
<span data-ttu-id="ec45e-163">Quando si seleziona "Solo all'esterno dell'app", è necessario aver già fornito i certificati dalla piattaforma su cui si basa l'applicazione (servizio APN o GCM).</span><span class="sxs-lookup"><span data-stu-id="ec45e-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="ec45e-164">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ec45e-164">See also</span></span>
* <span data-ttu-id="ec45e-165">[Apple Push Notification Service - Certificati](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging - Certificato](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="ec45e-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="ec45e-166">Modalità di recapito "Solo in-app"</span><span class="sxs-lookup"><span data-stu-id="ec45e-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="ec45e-168">La modalità di recapito "Solo in-app" fornisce la notifica push quando l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ec45e-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="ec45e-169">Per questa notifica, non è necessario passare attraverso il servizio APN e il sistema GCM.</span><span class="sxs-lookup"><span data-stu-id="ec45e-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="ec45e-170">È possibile usare il sistema di recapito in-app per raggiungere gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="ec45e-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="ec45e-171">È possibile personalizzare completamente la notifica e decidere in quale attività (schermata) visualizzare la notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="ec45e-172">Modalità di recapito "Sempre"</span><span class="sxs-lookup"><span data-stu-id="ec45e-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="ec45e-173">È possibile scegliere la modalità di recapito "Sempre", che consente di raggiungere l'utente finale indipendentemente dal fatto che l'applicazione sia in esecuzione o meno.</span><span class="sxs-lookup"><span data-stu-id="ec45e-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="ec45e-174">Quando si seleziona "Sempre", è necessario aver già fornito i certificati dalla piattaforma su cui si basa l'applicazione (servizio APN o GCM).</span><span class="sxs-lookup"><span data-stu-id="ec45e-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="ec45e-175">Pianificare una campagna push</span><span class="sxs-lookup"><span data-stu-id="ec45e-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="ec45e-176">Pianificare l'inizio di una campagna</span><span class="sxs-lookup"><span data-stu-id="ec45e-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="ec45e-178">È il 21 marzo e si vuole diffondere un annuncio alla mezzanotte del 22 marzo.</span><span class="sxs-lookup"><span data-stu-id="ec45e-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="ec45e-179">Non è necessario essere davanti all'interfaccia per effettuare un push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="ec45e-180">È possibile pianificare in anticipo il minuto esatto in cui le notifiche verranno inviate.</span><span class="sxs-lookup"><span data-stu-id="ec45e-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="ec45e-181">Deselezionare la casella di controllo "Nessuna" e selezionare un'ora di inizio</span><span class="sxs-lookup"><span data-stu-id="ec45e-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="ec45e-182">Scegliere la data e ora in cui avviare la campagna push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="ec45e-183">Pianificare la fine di una campagna</span><span class="sxs-lookup"><span data-stu-id="ec45e-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="ec45e-185">Si vuole interrompere la campagna il 25 marzo alle 15, ma si sa che non si sarà presenti per poterlo fare.</span><span class="sxs-lookup"><span data-stu-id="ec45e-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="ec45e-186">Non è necessario essere davanti all'interfaccia per effettuare un push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="ec45e-187">È possibile pianificare in anticipo il minuto esatto in cui la campagna verrà interrotta.</span><span class="sxs-lookup"><span data-stu-id="ec45e-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="ec45e-188">Fare clic sulla casella di controllo "Nessuna" e selezionare un'ora di fine</span><span class="sxs-lookup"><span data-stu-id="ec45e-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="ec45e-189">Scegliere la data e ora in cui terminare la campagna push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="ec45e-190">Terminare manualmente una campagna</span><span class="sxs-lookup"><span data-stu-id="ec45e-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="ec45e-192">Per impostazione predefinita, le caselle di controllo "Nessuna" sono selezionate.</span><span class="sxs-lookup"><span data-stu-id="ec45e-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="ec45e-193">La campagna inizierà al momento dell'attivazione nella sezione Reach e terminerà quando verrà interrotta in questa stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="ec45e-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="ec45e-194">Le campagne create senza una data di fine memorizzano la notifica push nel dispositivo e consentono di visualizzare al successivo avvio dell'app, anche se la campagna è stata interrotta manualmente.</span><span class="sxs-lookup"><span data-stu-id="ec45e-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="ec45e-195">Migliorare una notifica push con una visualizzazione testo</span><span class="sxs-lookup"><span data-stu-id="ec45e-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="ec45e-196">Cos'è una visualizzazione testo?</span><span class="sxs-lookup"><span data-stu-id="ec45e-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="ec45e-198">Una visualizzazione testo è un popup con contenuto testuale.</span><span class="sxs-lookup"><span data-stu-id="ec45e-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="ec45e-199">Questo popup viene visualizzato quando l'utente finale fa clic sulla notifica push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="ec45e-200">Una visualizzazione testo consente di presentare più contenuto all'utente finale.</span><span class="sxs-lookup"><span data-stu-id="ec45e-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="ec45e-201">È anche un'opportunità per presentare una chiamata a un'azione, ad esempio il passaggio a una pagina dell'app, il reindirizzamento a un archivio, l'apertura di una pagina Web, l'invio di un messaggio di posta elettronica, l'avvio di una ricerca basata sulla posizione geografica e così via.</span><span class="sxs-lookup"><span data-stu-id="ec45e-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="ec45e-202">Esempio: visualizzazione testo</span><span class="sxs-lookup"><span data-stu-id="ec45e-202">Example: Text View</span></span>
* <span data-ttu-id="ec45e-203">Creare la campagna di notifica push nella sezione "Reach" e assegnare un nome alla campagna.</span><span class="sxs-lookup"><span data-stu-id="ec45e-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="ec45e-205">Scrivere il messaggio che verrà visualizzato nella notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="ec45e-206">Selezionare "testo" come tipo di contenuto per l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="ec45e-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="ec45e-208">Quando si effettua il push di una visualizzazione testo, prima viene sempre visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="ec45e-209">Definire il testo. Dopo aver selezionato il contenuto dell'annuncio di testo, apparirà la sottosezione che consente di definire il testo da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="ec45e-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="ec45e-211">Scrivere il titolo che verrà visualizzato nella parte superiore del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ec45e-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="ec45e-212">Scrivere il contenuto principale della visualizzazione testo.</span><span class="sxs-lookup"><span data-stu-id="ec45e-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="ec45e-213">Scrivere il contenuto che verrà visualizzato sul pulsante di azione. Un pulsante di azione consente all'applicazione di eseguire un'azione specifica, ad esempio l'apertura di una pagina dell'applicazione, il reindirizzamento a un archivio di app o a qualsiasi tipo di origine sia possibile fornire.</span><span class="sxs-lookup"><span data-stu-id="ec45e-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="ec45e-214">Scrivere il contenuto che verrà visualizzato sul pulsante di uscita. Facendo clic sul pulsante di uscita, la visualizzazione testo scompare.</span><span class="sxs-lookup"><span data-stu-id="ec45e-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="ec45e-215">Creare la campagna di notifica push che verrà visualizzata nell'elenco di campagne.</span><span class="sxs-lookup"><span data-stu-id="ec45e-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="ec45e-217">Attivare la campagna di notifica push per inviare la visualizzazione testo agli utenti.</span><span class="sxs-lookup"><span data-stu-id="ec45e-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="ec45e-219">Risultato</span><span class="sxs-lookup"><span data-stu-id="ec45e-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="ec45e-221">L'utente riceve la notifica e fa clic su di essa.</span><span class="sxs-lookup"><span data-stu-id="ec45e-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="ec45e-222">La visualizzazione testo appare come un popup con cui l'utente può interagire.</span><span class="sxs-lookup"><span data-stu-id="ec45e-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="ec45e-223">Migliorare una notifica push con una visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="ec45e-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="ec45e-224">Cos'è una visualizzazione Web?</span><span class="sxs-lookup"><span data-stu-id="ec45e-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="ec45e-226">Una visualizzazione Web è un popup con contenuto Web.</span><span class="sxs-lookup"><span data-stu-id="ec45e-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="ec45e-227">Questo popup viene visualizzato quando l'utente finale fa clic sulla notifica push.</span><span class="sxs-lookup"><span data-stu-id="ec45e-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="ec45e-228">Una visualizzazione Web consente una maggiore interazione con l'utente finale.</span><span class="sxs-lookup"><span data-stu-id="ec45e-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="ec45e-229">È anche un'opportunità per presentare una chiamata a un'azione, ad esempio il reindirizzamento a un archivio di app, l'apertura di una pagina Web, l'invio di un messaggio di posta elettronica, l'avvio di una ricerca basata sulla posizione geografica e così via.</span><span class="sxs-lookup"><span data-stu-id="ec45e-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="ec45e-230">Esempio: visualizzazione Web</span><span class="sxs-lookup"><span data-stu-id="ec45e-230">Example: Web View</span></span>
* <span data-ttu-id="ec45e-231">Creare la campagna push nella sezione "Reach" e assegnare un nome alla campagna.</span><span class="sxs-lookup"><span data-stu-id="ec45e-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="ec45e-233">Scrivere il messaggio che verrà visualizzato nella notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="ec45e-234">Selezionare "Web" come tipo di contenuto per l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="ec45e-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="ec45e-236">Informazioni sui tipi di annuncio:</span><span class="sxs-lookup"><span data-stu-id="ec45e-236">About Announcement types:</span></span>
* <span data-ttu-id="ec45e-237">Solo notifica: una semplice notifica standard.</span><span class="sxs-lookup"><span data-stu-id="ec45e-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="ec45e-238">Vale a dire che se un utente fa clic, non apparirà alcuna ulteriore visualizzazione, ma si verificherà semplicemente l'azione associata.</span><span class="sxs-lookup"><span data-stu-id="ec45e-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="ec45e-239">Annuncio di testo: una notifica che invita l'utente a esaminare una visualizzazione testo.</span><span class="sxs-lookup"><span data-stu-id="ec45e-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="ec45e-240">Annuncio Web: una notifica che invita l'utente a esaminare una visualizzazione Web.</span><span class="sxs-lookup"><span data-stu-id="ec45e-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="ec45e-241">Selezionare il contenuto "Annuncio Web".</span><span class="sxs-lookup"><span data-stu-id="ec45e-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="ec45e-242">quando si effettua il push di una visualizzazione Web, prima viene sempre visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec45e-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="ec45e-243">Definire il contenuto Web. Dopo aver selezionato il contenuto dell'annuncio Web, apparirà la sottosezione che consente di definire il contenuto della visualizzazione Web da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="ec45e-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="ec45e-245">Scrivere il titolo che verrà visualizzato nella parte superiore del messaggio (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="ec45e-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="ec45e-246">Scrivere qui il codice HTML.</span><span class="sxs-lookup"><span data-stu-id="ec45e-246">Write your HTML code here.</span></span>
* <span data-ttu-id="ec45e-247">Fare clic sul pulsante della modalità di modifica dell'origine per passare da un'edizione all'altra e verificarne l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="ec45e-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="ec45e-248">Scrivere il contenuto che verrà visualizzato sul pulsante di azione. Un pulsante di azione consente all'applicazione di eseguire un'azione specifica, ad esempio l'apertura di una pagina dell'applicazione, il reindirizzamento a un archivio o a qualsiasi tipo di origine sia possibile fornire.</span><span class="sxs-lookup"><span data-stu-id="ec45e-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="ec45e-249">Scrivere il contenuto che verrà visualizzato sul pulsante di uscita. Facendo clic sul pulsante di uscita, la visualizzazione Web scompare.</span><span class="sxs-lookup"><span data-stu-id="ec45e-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="ec45e-250">Risultato</span><span class="sxs-lookup"><span data-stu-id="ec45e-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="ec45e-252">L'utente riceve la notifica e fa clic su di essa.</span><span class="sxs-lookup"><span data-stu-id="ec45e-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="ec45e-253">La visualizzazione testo appare come un popup con cui l'utente può interagire.</span><span class="sxs-lookup"><span data-stu-id="ec45e-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

