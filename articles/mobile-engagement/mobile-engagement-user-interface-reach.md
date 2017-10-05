---
title: Interfaccia utente di Azure Mobile Engagement - Reach
description: Informazioni su come raggiungere gli utenti dell'applicazione con le notifiche push usando Azure Mobile Engagement
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
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="e797a-103">Come raggiungere gli utenti dell'applicazione con le notifiche push</span><span class="sxs-lookup"><span data-stu-id="e797a-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="e797a-104">In questo articolo viene descritta la scheda **REACH** del portale **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="e797a-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="e797a-105">Utilizzare il portale **Mobile Engagement** per monitorare e gestire le app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e797a-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="e797a-106">Si noti che per iniziare a utilizzare il portale, è innanzitutto necessario creare un account **Azure Mobile Engagement** .</span><span class="sxs-lookup"><span data-stu-id="e797a-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="e797a-107">Per ulteriori informazioni, vedere [Creare un account Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="e797a-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="e797a-108">La sezione Reach dell'interfaccia utente è lo strumento di gestione delle campagne push dove è possibile creare, modificare, attivare, terminare, monitorare e ottenere statistiche per le campagne di notifica push nonché funzionalità a cui è possibile accedere anche tramite l'API Reach e alcuni elementi dell'API Push di basso livello.</span><span class="sxs-lookup"><span data-stu-id="e797a-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="e797a-109">Tenere presente che, indipendentemente dall'uso delle API o dell'interfaccia utente, è necessario integrare Azure Mobile Engagement e Reach nell'applicazione per ogni piattaforma con l'SDK prima di poter usare le campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="e797a-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="e797a-110">Molte sezioni dell'interfaccia utente del portale **Mobile Engagement** contengono il pulsante **MOSTRA GUIDA**.</span><span class="sxs-lookup"><span data-stu-id="e797a-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="e797a-111">Premere questo pulsante per ottenere ulteriori informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="e797a-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="e797a-112">Quattro tipi di notifiche push</span><span class="sxs-lookup"><span data-stu-id="e797a-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="e797a-113">Annunci: consentono di inviare messaggi pubblicitari agli utenti che li reindirizzano a un'altra posizione all'interno dell'app o di inviarli a una pagina Web o a un archivio esterno all'app.</span><span class="sxs-lookup"><span data-stu-id="e797a-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="e797a-114">Sondaggi: consentono di raccogliere informazioni dagli utenti finali ponendo loro domande.</span><span class="sxs-lookup"><span data-stu-id="e797a-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="e797a-115">Push di dati: consentono di inviare un file di dati binario o base64.</span><span class="sxs-lookup"><span data-stu-id="e797a-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="e797a-116">Le informazioni contenute in un push di dati vengono inviate all'applicazione per modificare l'esperienza corrente degli utenti nell'app.</span><span class="sxs-lookup"><span data-stu-id="e797a-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="e797a-117">L'applicazione deve essere in grado di elaborare i dati di un push di dati.</span><span class="sxs-lookup"><span data-stu-id="e797a-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="e797a-118">Dettagli della campagna</span><span class="sxs-lookup"><span data-stu-id="e797a-118">Campaign Details</span></span>
<span data-ttu-id="e797a-119">È possibile modificare, duplicare, eliminare o attivare campagne che non sono state ancora attivate passando il puntatore sopra i relativi nomi oppure fare clic per aprirle.</span><span class="sxs-lookup"><span data-stu-id="e797a-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="e797a-120">È possibile duplicare campagne che sono già state attivate passando il puntatore sopra i nomi o fare clic per aprirle.</span><span class="sxs-lookup"><span data-stu-id="e797a-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="e797a-121">Tuttavia, non è possibile modificare una campagna dopo che è stata attivata.</span><span class="sxs-lookup"><span data-stu-id="e797a-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="e797a-123">Feedback di Reach</span><span class="sxs-lookup"><span data-stu-id="e797a-123">Reach Feedback</span></span>
<span data-ttu-id="e797a-124">Per visualizzare i dettagli di una campagna di copertura, fare clic su **Statistiche** .</span><span class="sxs-lookup"><span data-stu-id="e797a-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="e797a-125">La visualizzazione **Semplice** offre una rappresentazione visiva in forma di istogramma a barre di ciò che accade dopo l'attivazione di una campagna.</span><span class="sxs-lookup"><span data-stu-id="e797a-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="e797a-126">La visualizzazione **Avanzata** offre informazioni più granulari sulla campagna push.</span><span class="sxs-lookup"><span data-stu-id="e797a-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="e797a-127">Tali informazioni non saranno disponibili se si invia una campagna di prova, ad esempio una campagna push, a un dispositivo di test.</span><span class="sxs-lookup"><span data-stu-id="e797a-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="e797a-128">Le informazioni devono essere interpretate nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="e797a-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="e797a-129">**Con push** : specifica il numero di messaggi inviati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e797a-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="e797a-130">Questo numero dipenderà dai destinatari specificati durante la creazione della campagna push.</span><span class="sxs-lookup"><span data-stu-id="e797a-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="e797a-131">Se non si specificano destinatari, i messaggi verranno inviati a tutti i dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="e797a-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="e797a-132">Come per tutti gli altri servizi push, le notifiche push non vengono inviate direttamente ai dispositivi, ma ai rispettivi servizi di notifica push (Push Notification Service, PNS - APN/GCM/WNS) specifici della piattaforma in modo che recapitino le notifiche ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e797a-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="e797a-133">**Recapitati** : specifica il numero di messaggi recapitati correttamente dal servizio PNS al dispositivo e confermati come ricevuti da Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="e797a-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="e797a-134">*Motivi per cui il numero dei messaggi Recapitati può essere inferiore al numero dei massaggi Inviati:*</span><span class="sxs-lookup"><span data-stu-id="e797a-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="e797a-135">Se l'utente ha disinstallato l'app dal dispositivo, ma il PNS non ne è a conoscenza al momento dell'invio del push, il messaggio verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="e797a-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="e797a-136">Se nel dispositivo è installata l'app, ma i dispositivi sono stati offline per lunghi periodi di tempo, il PNS non riuscirà a recapitare il messaggio al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e797a-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="e797a-137">Se il messaggio viene recapitato al dispositivo ma Mobile Engagement SDK nell'app non riconosce il contenuto del messaggio, il messaggio viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="e797a-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="e797a-138">Questo problema può verificarsi se la personalizzazione della notifica nell'app genera un'eccezione che viene rilevata nell'SDK e il messaggio viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="e797a-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="e797a-139">Ciò può verificarsi anche se l'app nel dispositivo usa una versione di Mobile Engagement SDK che non è in grado di comprendere la versione più recente del messaggio push inviato dalla piattaforma, ma solo quando l'app è stata aggiornata dopo l'invio della notifica dalla piattaforma del servizio.</span><span class="sxs-lookup"><span data-stu-id="e797a-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="e797a-140">La scheda **Avanzate** indicherà il numero di messaggi eliminati.</span><span class="sxs-lookup"><span data-stu-id="e797a-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="e797a-141">Nei dispositivi iOS, i messaggi a volte non vengono recapitati se la batteria del dispositivo è scarica o se l'app utilizza una quantità significativa di alimentazione durante l'elaborazione delle notifiche remote.</span><span class="sxs-lookup"><span data-stu-id="e797a-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="e797a-142">Si tratta di una limitazione dei dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="e797a-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="e797a-143">**Visualizzati** : specifica il numero di messaggi visualizzati correttamente dall'utente dell'app sul dispositivo sotto forma di una notifica di sistema push o out-of-app nel centro notifiche o di una notifica in-app all'interno dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e797a-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="e797a-144">La scheda **Avanzate** indicherà il numero di notifiche di sistema e il numero di notifiche in-app.</span><span class="sxs-lookup"><span data-stu-id="e797a-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="e797a-145">*Motivi per cui il numero dei messaggi Visualizzati può essere inferiore al numero dei massaggi Recapitati (in attesa di visualizzazione)*</span><span class="sxs-lookup"><span data-stu-id="e797a-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="e797a-146">Se la campagna di notifica ha una data di fine, è possibile che la notifica sia stata recapitata, ma che la campagna fosse già scaduta nel momento in cui la notifica doveva essere aperta e visualizzata all'utente dell'app e che quindi non sia mai stata visualizzata.</span><span class="sxs-lookup"><span data-stu-id="e797a-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="e797a-147">Se la notifica è una notifica in-app, viene visualizzata solo quando l'utente dell'app apre l'app.</span><span class="sxs-lookup"><span data-stu-id="e797a-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="e797a-148">Nei casi in cui l'app non è stata aperta dall'utente, l'SDK segnalerà che la notifica è stata recapitata ma non ancora visualizzata, fino all'apertura dell'app.</span><span class="sxs-lookup"><span data-stu-id="e797a-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="e797a-149">Se la notifica è una notifica in-app ed è configurata per la visualizzazione in un'attività/schermata specifica, anche in questo caso la notifica verrà segnalata come recapitata ma non ancora visualizzata fino all'apertura di una schermata specifica dell'app da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e797a-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="e797a-150">**Interazioni dell'utente** : specifica il numero di messaggi con cui l'utente dell'app ha interagito e includerà i messaggi attivati o chiusi.</span><span class="sxs-lookup"><span data-stu-id="e797a-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="e797a-151">*L'utente dell'app può attivare una notifica in uno dei modi seguenti:*</span><span class="sxs-lookup"><span data-stu-id="e797a-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="e797a-152">Se la notifica è una notifica di sistema o out-of-app o una notifica in-app inviata come sola notifica, l'utente dell'app deve fare clic sulla notifica.</span><span class="sxs-lookup"><span data-stu-id="e797a-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="e797a-153">Se la notifica è una notifica in-app con un testo, una visualizzazione Web o sondaggi, l'utente dell'app deve fare clic sul pulsante di attivazione nella notifica.</span><span class="sxs-lookup"><span data-stu-id="e797a-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="e797a-154">Se la notifica è una notifica in-app con una visualizzazione Web, l'utente dell'app deve fare clic su un URL nella visualizzazione Web [solo per Android]</span><span class="sxs-lookup"><span data-stu-id="e797a-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="e797a-155">*L'utente dell'app può chiudere una notifica in uno dei modi seguenti:*</span><span class="sxs-lookup"><span data-stu-id="e797a-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="e797a-156">Facendo clic sul pulsante di chiusura direttamente nella notifica.</span><span class="sxs-lookup"><span data-stu-id="e797a-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="e797a-157">Facendo scorrere rapidamente con un dito o eliminando la notifica.</span><span class="sxs-lookup"><span data-stu-id="e797a-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="e797a-158">Le notifiche in-app con testo o contenuto Web e sondaggi vengono in genere visualizzate dall'utente dell'app con un processo in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="e797a-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="e797a-159">Viene prima visualizzata una notifica e, facendo clic su di essa, viene visualizzato il testo, il contenuto Web o i sondaggi.</span><span class="sxs-lookup"><span data-stu-id="e797a-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="e797a-160">L'utente dell'app può chiudere una notifica con uno di questi passaggi e i dettagli vengono acquisiti nella visualizzazione Avanzata.</span><span class="sxs-lookup"><span data-stu-id="e797a-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="e797a-161">**Attivati** : specifica il numero di messaggi esplicitamente attivati dall'utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="e797a-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="e797a-162">Si tratta del dato più interessante, in quanto indica il numero di utenti dell'app interessati al messaggio inviato nella notifica.</span><span class="sxs-lookup"><span data-stu-id="e797a-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="e797a-163">Nelle piattaforme iOS e Windows, se l'utente ha l'app aperta e la campagna era di tipo "AnyTime", è possibile che le notifiche out-of-app e in-app vengano visualizzate nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="e797a-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="e797a-164">Il numero di messaggi Visualizzati può pertanto essere superiore al numero dei messaggi Recapitati.</span><span class="sxs-lookup"><span data-stu-id="e797a-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="e797a-165">Se l'utente interagisce con la notifica o la attiva, anche il numero di Interazioni utente o di messaggi Attivati può essere superiore al numero dei messaggi Recapitati.</span><span class="sxs-lookup"><span data-stu-id="e797a-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="e797a-167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e797a-167">See also</span></span>
* <span data-ttu-id="e797a-168">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e797a-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="e797a-169">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="e797a-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

