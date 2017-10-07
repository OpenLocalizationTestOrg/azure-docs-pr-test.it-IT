---
title: Interfaccia utente di Engagement Mobile - Reach aaaAzure
description: Informazioni su come tooreach toohello utenti dell'applicazione con Azure Mobile Engagement le notifiche push
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="8e3db-103">Come tooreach toohello utenti dell'applicazione con le notifiche push</span><span class="sxs-lookup"><span data-stu-id="8e3db-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="8e3db-104">Questo articolo descrive hello **raggiungere** scheda di hello **Mobile Engagement** portale.</span><span class="sxs-lookup"><span data-stu-id="8e3db-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="8e3db-105">Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e3db-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="8e3db-106">Si noti che toostart tramite il portale di hello è innanzitutto necessario toocreate un **Azure Mobile Engagement** account.</span><span class="sxs-lookup"><span data-stu-id="8e3db-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="8e3db-107">Per ulteriori informazioni, vedere [Creare un account Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="8e3db-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="8e3db-108">Hello raggiungere sezione dell'interfaccia utente è hello lo strumento Gestione campagna Push hello in cui è possibile creare/modificare/attiva/fine/monitoraggio e ottenere le statistiche sulle campagne di notifica Push e sulle funzionalità che è possibile accedere tramite l'API Reach hello (e alcuni elementi di hello bassa livello API Push).</span><span class="sxs-lookup"><span data-stu-id="8e3db-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="8e3db-109">Tenere presente che se si utilizza hello API o hello dell'interfaccia utente, sarà necessario toointegrate Azure Mobile Engagement sia portata nell'applicazione per ogni piattaforma con hello SDK prima di poter usare raggiungere campagne.</span><span class="sxs-lookup"><span data-stu-id="8e3db-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="8e3db-110">Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8e3db-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="8e3db-111">Premere tooget questo pulsante più informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="8e3db-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="8e3db-112">Quattro tipi di notifiche push</span><span class="sxs-lookup"><span data-stu-id="8e3db-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="8e3db-113">Annunci - Consenti toosend pubblicità messaggi toousers che reindirizza tooanother posizione all'interno di applicazione o toosend le pagine Web tooa o archiviare all'esterno dell'app.</span><span class="sxs-lookup"><span data-stu-id="8e3db-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="8e3db-114">Esegue il polling - consentono ponendo domande toogather informazioni dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="8e3db-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="8e3db-115">Push di dati - consentono toosend un file di dati binary o base64.</span><span class="sxs-lookup"><span data-stu-id="8e3db-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="8e3db-116">informazioni di Hello contenute in un push di dati inviati tooyour applicazione toomodify esperienza corrente degli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e3db-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="8e3db-117">L'applicazione deve toobe tooprocess in grado di hello dati di un push di dati.</span><span class="sxs-lookup"><span data-stu-id="8e3db-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="8e3db-118">Dettagli della campagna</span><span class="sxs-lookup"><span data-stu-id="8e3db-118">Campaign Details</span></span>
<span data-ttu-id="8e3db-119">È possibile eliminare, modificare o clonare o attivare campagne che non sono stati ancora attivate passando sopra i nomi o è possibile fare clic su tooopen li.</span><span class="sxs-lookup"><span data-stu-id="8e3db-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="8e3db-120">È possibile duplicare le campagne che sono già state attivate passando sopra i nomi o è possibile fare clic su tooopen li.</span><span class="sxs-lookup"><span data-stu-id="8e3db-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="8e3db-121">Tuttavia, non è possibile modificare una campagna dopo che è stata attivata.</span><span class="sxs-lookup"><span data-stu-id="8e3db-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="8e3db-123">Feedback di Reach</span><span class="sxs-lookup"><span data-stu-id="8e3db-123">Reach Feedback</span></span>
<span data-ttu-id="8e3db-124">Fare clic su **statistiche** dettagli hello toosee di una campagna di copertura.</span><span class="sxs-lookup"><span data-stu-id="8e3db-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="8e3db-125">Hello **semplice** Vista fornisce una rappresentazione visiva sotto forma di hello di un grafico a barre su cosa è successo dopo che è stata attivata una campagna di colonna.</span><span class="sxs-lookup"><span data-stu-id="8e3db-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="8e3db-126">Hello **avanzate** visualizzazione fornisce dettagli più granulari sulla campagna push hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="8e3db-127">Questi dettagli non sarà disponibili se si invia una campagna di test, ovvero un dispositivo di test inviato tooa push.</span><span class="sxs-lookup"><span data-stu-id="8e3db-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="8e3db-128">Le informazioni devono essere interpretate nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="8e3db-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="8e3db-129">**Inserito** -specifica il numero di hello di messaggi con push toohello dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8e3db-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="8e3db-130">Questo numero dipenderà dai destinatari hello specificato durante la creazione della campagna push hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="8e3db-131">Se non si specifica un gruppo di destinatari, i dispositivi registrato hello tooall verrà inviato il push.</span><span class="sxs-lookup"><span data-stu-id="8e3db-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="8e3db-132">Come tutti gli altri servizi, push è non notifiche di push hello direttamente i dispositivi toohello ma invece inviarli toohello rispettivi piattaforma servizi di notifica Push specifici (PNS - APNS/GCM/WNS) in modo che è possibile recapitare le notifiche di hello toohello dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8e3db-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="8e3db-133">**Recapitati** -specifica il numero di hello di messaggi che vengono recapitati dal dispositivo di toohello PNS hello e riconosciuto come ricevuto da Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="8e3db-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="8e3db-134">*Motivi per cui il numero dei messaggi Recapitati può essere inferiore al numero dei massaggi Inviati:*</span><span class="sxs-lookup"><span data-stu-id="8e3db-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="8e3db-135">Se l'utente hello è disinstallato l'applicazione hello dal dispositivo hello ma hello PNS non riconosce in fase di hello che inviamo hello push toohello PNS messaggio hello verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="8e3db-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="8e3db-136">Se il dispositivo di hello è applicazione hello ma dispositivi hello stessi sono stati offline per lunghi periodi di tempo, quindi hello PNS avrà esito negativo dispositivo toohello messaggio hello di toodeliver.</span><span class="sxs-lookup"><span data-stu-id="8e3db-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="8e3db-137">Se il messaggio hello ottenere recapitato toohello dispositivo ma Ciao hello app Mobile Engagement SDK non riconosce il contenuto di hello del messaggio hello, Elimina il messaggio.</span><span class="sxs-lookup"><span data-stu-id="8e3db-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="8e3db-138">Questo problema può verificarsi se personalizzazione hello della notifica hello in app hello genera un'eccezione che viene rilevato nel messaggio di hello hello SDK e drop.</span><span class="sxs-lookup"><span data-stu-id="8e3db-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="8e3db-139">Ciò può verificarsi anche se app hello dispositivo hello è utilizzando una versione di hello Mobile Engagement SDK che non è in grado di toounderstand hello versione messaggio hello del push inviate da piattaforma hello ma si tratta solo quando l'applicazione hello è stato aggiornato dopo la notifica hello è stata inviata da piattaforma hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="8e3db-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="8e3db-140">Hello **avanzate** scheda indicherà il numero di messaggi sono stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="8e3db-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="8e3db-141">Nei dispositivi iOS, i messaggi a volte non venga recapitati se dei dispositivi hello nella batteria in esaurimento o se l'app hello utilizza notevole quantità di energia durante l'elaborazione remote notifiche.</span><span class="sxs-lookup"><span data-stu-id="8e3db-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="8e3db-142">Si tratta di un limite di dispositivi iOS hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="8e3db-143">**Visualizzato** -specifica il numero di hello di messaggi che vengono correttamente visualizzati toohello utente di app nel dispositivo hello sotto forma di hello di una notifica push/out-di-app di sistema nel centro notifiche hello o una notifica in-app all'interno di hello mobili app.</span><span class="sxs-lookup"><span data-stu-id="8e3db-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="8e3db-144">Hello **avanzate** scheda indicherà quante sono le notifiche di sistema e quanti notifiche nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e3db-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="8e3db-145">*Conteggio dei motivi per visualizzare sia minore di count consegnati (in attesa toobe visualizzato)*</span><span class="sxs-lookup"><span data-stu-id="8e3db-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="8e3db-146">Se ha una data di fine su di esso, è possibile che notifica hello è stata recapitata, ma quando il tempo di hello proviene tooopen campagna notifica hello e la Visualizza utente app toohello, è stato già scaduto in modo che non è stato visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8e3db-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="8e3db-147">Se una notifica in-app è la notifica di hello notifica hello è visualizzata solo se l'utente app hello apre l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="8e3db-148">Nei casi in cui utente app hello non è stato aperto l'applicazione hello, hello SDK segnalerà che notifica hello è stata recapitata, ma non ancora visualizzata finché non viene aperto l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="8e3db-149">Se notifica hello è una notifica in-app e configurato toobe visualizzato in una determinata attività o la stessa schermata anche notifica hello verrà segnalata come recapitati ma non ancora consegnate fino a quando l'utente di hello apre app hello in una schermata specifica.</span><span class="sxs-lookup"><span data-stu-id="8e3db-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="8e3db-150">**Le interazioni utente** -specifica il numero di hello di messaggi di cui l'utente app hello ha interagito con e includerà i messaggi hello che sono azioni o chiusi.</span><span class="sxs-lookup"><span data-stu-id="8e3db-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="8e3db-151">*Hello app è possibile eseguire azioni una notifica in uno dei seguenti modi hello:*</span><span class="sxs-lookup"><span data-stu-id="8e3db-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="8e3db-152">Se hello notifica è una notifica di sistema/out-di-app o inviata una notifica in-app come sola notifica l'utente di app hello fa clic sulla notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="8e3db-153">Se notifica hello è una notifica in-app con un testo o di una visualizzazione web o viene eseguito il polling hello quindi utente app fa clic su hello pulsante di azione di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="8e3db-154">Se la notifica hello è quindi una notifica in-app con una visualizzazione web hello app utente fa clic su un URL hello web solo nella visualizzazione [Android]</span><span class="sxs-lookup"><span data-stu-id="8e3db-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="8e3db-155">*utente applicazione Hello può chiudere una notifica in uno dei seguenti modi hello:*</span><span class="sxs-lookup"><span data-stu-id="8e3db-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="8e3db-156">Fare clic sul pulsante Chiudi hello notifica hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="8e3db-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="8e3db-157">Passaggio di stoccaggio o l'eliminazione di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="8e3db-158">Le notifiche in-app con il contenuto di testo/web e viene eseguito il polling sono utente app toohello in genere visualizzati in un processo in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="8e3db-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="8e3db-159">Viene visualizzato prima una notifica e quando si fa clic su di essa, viene visualizzato il contenuto di testo/web/polling successivi hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="8e3db-160">utente applicazione Hello può chiudere una notifica in uno di questi passaggi e i dettagli di hello nella vista avanzata hello acquisisce questo.</span><span class="sxs-lookup"><span data-stu-id="8e3db-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="8e3db-161">**Azioni** -specifica il numero di hello di messaggi che sono stati azioni in modo esplicito dall'utente di app hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="8e3db-162">Si tratta di numero più interessante hello in questo modo viene indicato il numero di utenti app sono stato interessato dal messaggio hello inserite nella notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8e3db-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="8e3db-163">IOS & piattaforme Windows, se hello utente dispone di app hello aperta e campagna hello è stata una campagna "In qualsiasi momento" è possibile che le notifiche di app e in app visualizzarle nella hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="8e3db-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="8e3db-164">Ciò potrebbe causare un conteggio visualizzate superiore hello consegnati.</span><span class="sxs-lookup"><span data-stu-id="8e3db-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="8e3db-165">Se l'utente hello interagisce o notifica hello azioni, quindi anche hello interazioni utente/Actioned conteggio potrebbe essere maggiore di recapito.</span><span class="sxs-lookup"><span data-stu-id="8e3db-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="8e3db-167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8e3db-167">See also</span></span>
* <span data-ttu-id="8e3db-168">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="8e3db-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="8e3db-169">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="8e3db-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

