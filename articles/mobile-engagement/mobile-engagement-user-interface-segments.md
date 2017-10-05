---
title: Interfaccia utente di Azure Mobile Engagement - Segmenti
description: Informazioni su come creare e gestire segmenti di utenti per identificare modelli di utilizzo mediante Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 087f4a1fef420abe9669f8dfe2b84c7a847ce263
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-segments-of-users-to-identify-usage-patterns"></a><span data-ttu-id="19266-103">Come creare e gestire segmenti di utenti per identificare modelli di utilizzo</span><span class="sxs-lookup"><span data-stu-id="19266-103">How to create and manage segments of users to identify usage patterns</span></span>
<span data-ttu-id="19266-104">In questo articolo viene descritta la scheda **SEGMENTI** del portale **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="19266-104">This article describes the **SEGMENTS** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="19266-105">Utilizzare il portale **Mobile Engagement** per monitorare e gestire le app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="19266-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span>

<span data-ttu-id="19266-106">La sezione Segmenti dell'interfaccia utente consente di dividere gli utenti in segmenti in base al comportamento e all'analisi che è possibile ottenere dall'applicazione ed è possibile accedervi anche tramite l'API Segmenti.</span><span class="sxs-lookup"><span data-stu-id="19266-106">The Segments section of the UI allows you to work on segmenting your users based on the different behavior and analytics that you can get from the application and can also access through the Segments API.</span></span> <span data-ttu-id="19266-107">I segmenti vengono calcolati per la prima volta 24 ore dopo che sono stati creati e quindi ricalcolati ogni 24 ore in base alle informazioni di analisi più recenti.</span><span class="sxs-lookup"><span data-stu-id="19266-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on the latest analytics information.</span></span> <span data-ttu-id="19266-108">Una volta calcolato un segmento, viene visualizzato un grafico di cronologia giorno per giorno ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="19266-108">Once a segment is calculated, it displays a "Day to day history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="19266-109">Molte sezioni dell'interfaccia utente del portale **Mobile Engagement** contengono il pulsante **MOSTRA LA GUIDA**.</span><span class="sxs-lookup"><span data-stu-id="19266-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="19266-110">Premere questo pulsante per ottenere ulteriori informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="19266-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="19266-111">Creare segmenti</span><span class="sxs-lookup"><span data-stu-id="19266-111">Create Segments</span></span>
<span data-ttu-id="19266-112">È possibile creare un segmento basato su criteri (fino a 10) in base a un periodo specifico di massimo 60 giorni precedenti dalla sezione di analisi.</span><span class="sxs-lookup"><span data-stu-id="19266-112">You can create a segment based on up to 10 criteria on a specific period up to 60 days in the past from the analytics section.</span></span> <span data-ttu-id="19266-113">Ad esempio, è possibile creare un segmento in base alle persone che hanno visualizzato alcune pagine o che hanno cercato contenuto specifico all'interno dell'app negli ultimi 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="19266-113">For example, you can create a segment based on the people who have viewed certain pages or searched for specific content within your app within the last 10 days.</span></span> <span data-ttu-id="19266-114">Queste informazioni sono disponibili nella sezione di analisi.</span><span class="sxs-lookup"><span data-stu-id="19266-114">This information is available in the analytics section.</span></span> <span data-ttu-id="19266-115">È possibile utilizzarle per creare un segmento e quindi configurare una notifica push da indirizzare a questo sottoinsieme di utenti per fare in modo che tornino all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19266-115">So, you can use it to create a segment, and then set up a push notification to target this subset of users to get them to come back to the application.</span></span> 

> [!NOTE]
> <span data-ttu-id="19266-116">una volta calcolato, un segmento non può essere modificato; può essere solo duplicato (copiato) o distrutto (eliminato).</span><span class="sxs-lookup"><span data-stu-id="19266-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="19266-117">Un segmento può essere duplicato all'interno della stessa applicazione (con lo stesso AppID) e anche in altre applicazioni (con un AppID diverso).</span><span class="sxs-lookup"><span data-stu-id="19266-117">A segment can be cloned within the same application (with the same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="19266-119">Esempi di segmento</span><span class="sxs-lookup"><span data-stu-id="19266-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="19266-121">I segmenti consentono di suddividere gli utenti finali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19266-121">Segments allow you to segment the end-users of your application.</span></span>
<span data-ttu-id="19266-122">La segmentazione degli utenti è un'importante strategia di marketing.</span><span class="sxs-lookup"><span data-stu-id="19266-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="19266-123">Azure Mobile Engagement consente di ottenere dati cronologici e creare segmenti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="19266-123">Azure Mobile Engagement allows you to get historic data and create custom segments.</span></span> <span data-ttu-id="19266-124">Questo potente strumento consente di acquisire informazioni sull'esperienza dei clienti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19266-124">This powerful tool enables you to learn about your customers’ experience in your application.</span></span> <span data-ttu-id="19266-125">È possibile analizzare facilmente i segmenti e utilizzarli come destinazioni di push.</span><span class="sxs-lookup"><span data-stu-id="19266-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="19266-126">Un caso di utilizzo comune si verifica quando si desidera eseguire il push di una notifica per incoraggiare gli utenti finali a valutare l'applicazione nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="19266-126">A common use-case is that you want to send a push a notification to encourage your end-users to rate your application in the store.</span></span> <span data-ttu-id="19266-127">Anziché inviare una notifica a tutti gli utenti finali, è possibile creare un segmento che specifichi solo gli utenti che hanno utilizzato l'applicazione ogni giorno nel corso dell'ultimo mese e sono stati soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="19266-127">Rather than sending a notification to all your end-users, you can create a segment that would specify only users that have used your application every day for the last month and have had a great user experience.</span></span> <span data-ttu-id="19266-128">Quando si invia un numero inferiore di notifiche push mirate, è possibile ottenere un ritorno sugli investimenti migliore.</span><span class="sxs-lookup"><span data-stu-id="19266-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-the-major-azure-mobile-engagement-elements"></a><span data-ttu-id="19266-130">Segmenti che è possibile creare in base agli elementi principali di Azure Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="19266-130">Segments you can create based on the major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="19266-131">Evento: creare un segmento destinato a un solo evento specifico dell'applicazione che si è verificato più di due volte alla settimana.</span><span class="sxs-lookup"><span data-stu-id="19266-131">Event: create a segment that targets one specific event of the application that happened more than twice a week.</span></span> 
* <span data-ttu-id="19266-132">Sessione: creare un segmento di utenti che hanno utilizzato l'applicazione più di 5 volte nell'ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="19266-132">Session: create a segment of users that have used the application more than 5 times last week.</span></span>
* <span data-ttu-id="19266-133">Attività: creare un segmento di utenti che hanno utilizzato una pagina o un contenuto più o meno di 10 volte nell'ultimo mese.</span><span class="sxs-lookup"><span data-stu-id="19266-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="19266-134">Processo: creare un segmento di utenti che hanno completato un processo più di due volte al giorno.</span><span class="sxs-lookup"><span data-stu-id="19266-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="19266-135">Arresto anomalo: creare un segmento di tutti gli utenti che hanno avuto un arresto anomalo più di 10 volte nel corso dell'ultima settimana</span><span class="sxs-lookup"><span data-stu-id="19266-135">Crash: create a segment of all the users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="19266-136">(il push per questo segmento dovrebbe includere un messaggio di scuse ed eventualmente un buono).</span><span class="sxs-lookup"><span data-stu-id="19266-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="19266-137">Errore: creare un segmento di tutti gli utenti che hanno incontrato un errore più di 100 volte negli ultimi 3 giorni.</span><span class="sxs-lookup"><span data-stu-id="19266-137">Error: create a segment of all the users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="19266-138">Info app: creare un segmento mirato a un'info app personalizzata che si è verificata negli ultimi 25 giorni.</span><span class="sxs-lookup"><span data-stu-id="19266-138">App Info: create a segment that targets a custom App Info that happened during the last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="19266-140">Per utilizzare il segmento in modo ottimale, è necessario aver effettuato un'integrazione personalizzata dell'SDK nell'applicazione con un piano di tag "Info app".</span><span class="sxs-lookup"><span data-stu-id="19266-140">To use Segment in an optimal way, you must have done a customized integration of the SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="19266-141">Quindi, passare alla home page dell'interfaccia, selezionare l'applicazione desiderata e scegliere la sezione "Segmenti".</span><span class="sxs-lookup"><span data-stu-id="19266-141">Then, go to the home page of the interface, select the application you want and click on the "Segments" section.</span></span>

1. <span data-ttu-id="19266-142">Selezionare la sezione "Segmenti".</span><span class="sxs-lookup"><span data-stu-id="19266-142">Select the "Segments" section.</span></span>
2. <span data-ttu-id="19266-143">Fare clic su "Nuovo segmento" per creare un nuovo segmento.</span><span class="sxs-lookup"><span data-stu-id="19266-143">Click on the "New segment" button to create a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="19266-144">Esempio di vita reale: creare un segmento semplice in base alle informazioni di "Sessione"</span><span class="sxs-lookup"><span data-stu-id="19266-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="19266-145">Creare un segmento di tutti gli utenti finali che hanno utilizzato l'app almeno 50 volte nell'ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="19266-145">Create a segment of all the end-users that have used your app at least 50 times in the last week.</span></span> <span data-ttu-id="19266-146">Da qui, individuare solo gli utenti finali che hanno trascorso almeno 30 secondi per sessione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19266-146">From there, find only the end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="19266-147">Verranno visualizzati tutti gli utenti finali che hanno avuto un'esperienza positiva nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19266-147">This will show all the end-users who have a positive experience in your app.</span></span> <span data-ttu-id="19266-148">Quindi, il segmento creato potrebbe essere utilizzato per effettuare il push di una notifica a tali utenti finali per chiedere loro di valutare l'app nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="19266-148">Then, the segment created could be used to push a notification to these end-users to ask them to rate your app in the store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="19266-150">Assegnare un nome al segmento per trovarlo rapidamente nell'elenco di "Segmenti".</span><span class="sxs-lookup"><span data-stu-id="19266-150">Give your segment a name in order to find it quickly in the "Segment" list.</span></span>
2. <span data-ttu-id="19266-151">Fare clic sul pulsante "Crea".</span><span class="sxs-lookup"><span data-stu-id="19266-151">Click on the "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="19266-153">Selezionare Sessione.</span><span class="sxs-lookup"><span data-stu-id="19266-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="19266-155">Selezionare il periodo "Ultima settimana".</span><span class="sxs-lookup"><span data-stu-id="19266-155">Select the period of "Last week".</span></span>
2. <span data-ttu-id="19266-156">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="19266-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="19266-158">Selezionare l'operatore rilevante nell'elenco: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="19266-158">Select the Operator that is relevant among the list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="19266-159">Immettere il numero desiderato.</span><span class="sxs-lookup"><span data-stu-id="19266-159">Enter the Count you want.</span></span>
5. <span data-ttu-id="19266-160">Selezionare l'occorrenza desiderata.</span><span class="sxs-lookup"><span data-stu-id="19266-160">Select the Occurrence you want.</span></span> 
6. <span data-ttu-id="19266-161">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="19266-161">Click next.</span></span>
   <span data-ttu-id="19266-162">In questo esempio nell'ultima settimana gli utenti corrispondenti sono quelli che hanno creato almeno 50 sessioni.</span><span class="sxs-lookup"><span data-stu-id="19266-162">This example is set so that over the last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="19266-164">Per la segmentazione in base alla sessione, è possibile scegliere come criterio la lunghezza per sessione.</span><span class="sxs-lookup"><span data-stu-id="19266-164">For the Session segmentation, you can choose the length per session as a criteria.</span></span>

1. <span data-ttu-id="19266-165">Selezionare l'operatore dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="19266-165">Select the Operator from the list.</span></span>
2. <span data-ttu-id="19266-166">Specificare la lunghezza per sessione.</span><span class="sxs-lookup"><span data-stu-id="19266-166">Provide the Length per session.</span></span>
3. <span data-ttu-id="19266-167">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="19266-167">Click Next.</span></span>
   <span data-ttu-id="19266-168">In questo esempio, in tutte le sessioni segmentate in base alla sezione dell'occorrenza, devono essere selezionati solo gli utenti che hanno trascorso più di 30 secondi per sessione.</span><span class="sxs-lookup"><span data-stu-id="19266-168">In this example, it says that over all the sessions that have been segmented on the occurrence section, select only the users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="19266-170">Assegnare il nome al criterio per recuperarlo nel relativo grafico completo e fare clic su Fine.</span><span class="sxs-lookup"><span data-stu-id="19266-170">Name your criterion in order to retrieve it in the complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="19266-172">Al termine dell'impostazione, il criterio viene visualizzato nel grafico del segmento.</span><span class="sxs-lookup"><span data-stu-id="19266-172">When you have finished setting up your criterion, it will appear in the segment funnel.</span></span>
<span data-ttu-id="19266-173">Poiché un segmento è basato su dati di analisi, i segmenti vengono calcolati una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="19266-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="19266-174">In questo esempio, il 47,7% degli utenti finali totali corrispondeva al criterio.</span><span class="sxs-lookup"><span data-stu-id="19266-174">In this example, 47,7% of the total end-users matched the criterion.</span></span> <span data-ttu-id="19266-175">Tali utenti sono quelli che hanno avuto un'esperienza ottima e che probabilmente esprimeranno una valutazione più alta se ricevono una notifica push che chiede loro di valutare l'applicazione nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="19266-175">They should be the users who have had a good experience and will be likely to provide a higher rating if you push them a notification asking them to rate the app in the store.</span></span>

## <a name="see-also"></a><span data-ttu-id="19266-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="19266-176">See also</span></span>
* <span data-ttu-id="19266-177">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="19266-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="19266-178">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="19266-178">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

