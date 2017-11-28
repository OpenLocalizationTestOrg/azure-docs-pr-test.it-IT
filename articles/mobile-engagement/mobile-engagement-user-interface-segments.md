---
title: aaaAzure interfaccia utente di Engagement Mobile - segmenti
description: Informazioni su come toocreate e gestiscono segmenti di modelli di utilizzo tooidentify gli utenti con Azure Mobile Engagement
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
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="decf8-103">Come toocreate e gestiscono segmenti di modelli di utilizzo tooidentify utenti</span><span class="sxs-lookup"><span data-stu-id="decf8-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="decf8-104">Questo articolo descrive hello **segmenti** scheda di hello **Mobile Engagement** portale.</span><span class="sxs-lookup"><span data-stu-id="decf8-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="decf8-105">Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="decf8-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="decf8-106">sezione di segmenti Hello di hello dell'interfaccia utente consente toowork nella segmentazione agli utenti in base a un comportamento diverso hello e analitica che è possibile ottenere da un'applicazione hello e possono accedere anche tramite API di segmenti hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="decf8-107">Segmenti vengono innanzitutto calcolati 24 ore dopo che sono stati creati e vengono ricalcolate ogni 24 ore in base alle informazioni analitica più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="decf8-108">Una volta che viene calcolato un segmento, viene visualizzato un grafico "Cronologia tooday giorno" ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="decf8-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="decf8-109">Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante.</span><span class="sxs-lookup"><span data-stu-id="decf8-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="decf8-110">Premere tooget questo pulsante più informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="decf8-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="decf8-111">Creare segmenti</span><span class="sxs-lookup"><span data-stu-id="decf8-111">Create Segments</span></span>
<span data-ttu-id="decf8-112">È possibile creare un segmento di base dei criteri too10 di un periodo specifico di giorni too60 hello passato dalla sezione analitica hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="decf8-113">Ad esempio, è possibile creare un segmento in base alle persone hello che dispongono di visualizzare alcune pagine o cercare contenuto specifico all'interno dell'app all'interno di hello ultimi 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="decf8-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="decf8-114">Queste informazioni sono disponibili nella sezione analitica hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="decf8-115">In tal caso, è possibile usarlo toocreate un segmento e quindi impostare un tootarget di notifica push questo subset di utenti tooget li toocome toohello indietro applicazione.</span><span class="sxs-lookup"><span data-stu-id="decf8-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="decf8-116">una volta calcolato, un segmento non può essere modificato; può essere solo duplicato (copiato) o distrutto (eliminato).</span><span class="sxs-lookup"><span data-stu-id="decf8-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="decf8-117">È possibile duplicare un segmento all'interno di hello stessa applicazione (con hello AppID stesso), e possono anche essere clonato in altre applicazioni (con un ID applicazione diverso).</span><span class="sxs-lookup"><span data-stu-id="decf8-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="decf8-119">Esempi di segmento</span><span class="sxs-lookup"><span data-stu-id="decf8-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="decf8-121">Segmenti consentono agli utenti finali hello toosegment dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="decf8-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="decf8-122">La segmentazione degli utenti è un'importante strategia di marketing.</span><span class="sxs-lookup"><span data-stu-id="decf8-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="decf8-123">Azure Mobile Engagement consente dati cronologici tooget e creare segmenti di personalizzati.</span><span class="sxs-lookup"><span data-stu-id="decf8-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="decf8-124">Questo potente strumento consente toolearn sull'esperienza dei clienti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="decf8-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="decf8-125">È possibile analizzare facilmente i segmenti e utilizzarli come destinazioni di push.</span><span class="sxs-lookup"><span data-stu-id="decf8-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="decf8-126">Un caso di utilizzo comune è che si desidera toosend tooencourage una notifica push il toorate gli utenti finali dell'applicazione nell'archivio di hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="decf8-127">Anziché inviare una notifica tooall agli utenti finali, è possibile creare un segmento che è necessario specificare solo gli utenti che hanno utilizzato l'applicazione ogni giorno per ultimo mese hello e hanno avuto esperienza di un utente.</span><span class="sxs-lookup"><span data-stu-id="decf8-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="decf8-128">Quando si invia un numero inferiore di notifiche push mirate, è possibile ottenere un ritorno sugli investimenti migliore.</span><span class="sxs-lookup"><span data-stu-id="decf8-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="decf8-130">Segmenti che è possibile creare in base agli elementi di Azure Mobile Engagement principali hello:</span><span class="sxs-lookup"><span data-stu-id="decf8-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="decf8-131">Evento: creare un segmento di tale evento specifico di destinazioni con uno di un'applicazione hello che si sono verificati più di due volte a settimana.</span><span class="sxs-lookup"><span data-stu-id="decf8-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="decf8-132">Sessione: creazione di un segmento di utenti che hanno utilizzato più di 5 volte la settimana scorsa un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="decf8-133">Attività: creare un segmento di utenti che hanno utilizzato una pagina o un contenuto più o meno di 10 volte nell'ultimo mese.</span><span class="sxs-lookup"><span data-stu-id="decf8-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="decf8-134">Processo: creare un segmento di utenti che hanno completato un processo più di due volte al giorno.</span><span class="sxs-lookup"><span data-stu-id="decf8-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="decf8-135">Arresto anomalo: creazione di un segmento di tutti gli utenti di hello che hanno subito un arresto anomalo di più di 10 volte la settimana scorsa.</span><span class="sxs-lookup"><span data-stu-id="decf8-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="decf8-136">(il push per questo segmento dovrebbe includere un messaggio di scuse ed eventualmente un buono).</span><span class="sxs-lookup"><span data-stu-id="decf8-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="decf8-137">Errore: creare un segmento di tutti gli utenti di hello che hanno un errore più di 100 volte ultimi 3 giorni.</span><span class="sxs-lookup"><span data-stu-id="decf8-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="decf8-138">App Info: creazione di un segmento che ha come destinazione un App Info personalizzato che si sono verificati durante hello ultimi 25 giorni.</span><span class="sxs-lookup"><span data-stu-id="decf8-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="decf8-140">toouse segmento in modo ottimale, è necessario aver eseguito un'integrazione personalizzata di hello SDK nell'applicazione con un piano di assegnazione di tag di tag "App Info".</span><span class="sxs-lookup"><span data-stu-id="decf8-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="decf8-141">Quindi, passare toohello home page di interfaccia di hello, selezionare un'applicazione hello desiderato e fare clic sulla sezione "Segmenti" hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="decf8-142">Selezionare una sezione "Segmenti" hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="decf8-143">Fare clic su "Nuovo segmento" hello pulsante toocreate un nuovo segmento.</span><span class="sxs-lookup"><span data-stu-id="decf8-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="decf8-144">Esempio di vita reale: creare un segmento semplice in base alle informazioni di "Sessione"</span><span class="sxs-lookup"><span data-stu-id="decf8-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="decf8-145">Creare un segmento di tutti gli utenti finali hello che hanno utilizzato almeno 50 volte l'app in hello ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="decf8-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="decf8-146">Da qui, trovare solo gli utenti finali hello impiegato almeno 30 secondi nell'app per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="decf8-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="decf8-147">Verranno visualizzati tutti hello agli utenti finali un'esperienza positiva nell'app.</span><span class="sxs-lookup"><span data-stu-id="decf8-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="decf8-148">Quindi, segmento hello creato potrebbe essere utilizzato toopush un tooask gli utenti finali di notifica toothese li toorate l'app in hello archiviare.</span><span class="sxs-lookup"><span data-stu-id="decf8-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="decf8-150">Assegnare un nome di segmento in ordine toofind rapidamente nell'elenco di "Segmento" hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="decf8-151">Fare clic sul hello pulsante "Crea".</span><span class="sxs-lookup"><span data-stu-id="decf8-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="decf8-153">Selezionare Sessione.</span><span class="sxs-lookup"><span data-stu-id="decf8-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="decf8-155">Selezionare il periodo di hello di "Ultima settimana".</span><span class="sxs-lookup"><span data-stu-id="decf8-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="decf8-156">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="decf8-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="decf8-158">Seleziona hello operatore rilevanti tra elenco hello: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="decf8-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="decf8-159">Immettere hello numero desiderato.</span><span class="sxs-lookup"><span data-stu-id="decf8-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="decf8-160">Selezionare hello occorrenza desiderato.</span><span class="sxs-lookup"><span data-stu-id="decf8-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="decf8-161">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="decf8-161">Click next.</span></span>
   <span data-ttu-id="decf8-162">In questo esempio viene impostato in modo che over hello ultima settimana, corrispondenza utenti che hanno almeno 50 sessioni.</span><span class="sxs-lookup"><span data-stu-id="decf8-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="decf8-164">Per hello segmentazione della sessione, è possibile scegliere di lunghezza hello per ogni sessione come criterio.</span><span class="sxs-lookup"><span data-stu-id="decf8-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="decf8-165">Selezionare hello operatore dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="decf8-166">Fornire hello lunghezza per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="decf8-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="decf8-167">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="decf8-167">Click Next.</span></span>
   <span data-ttu-id="decf8-168">In questo esempio, afferma che su tutti hello sessioni che sono state segmentate nella sezione di occorrenza hello, selezionare solo gli utenti di hello impiegato più di 30 secondi per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="decf8-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="decf8-170">Nome del criterio di ordine tooretrieve in hello completare a imbuto e fare clic su Fine.</span><span class="sxs-lookup"><span data-stu-id="decf8-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="decf8-172">Al termine dell'impostazione del criterio, esso apparirà nel grafico a imbuto segmento hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="decf8-173">Poiché un segmento è basato su dati di analisi, i segmenti vengono calcolati una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="decf8-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="decf8-174">In questo esempio, 47,7% degli utenti finali totale hello corrispondente criterio hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="decf8-175">Dovrebbero essere utenti hello hanno un'esperienza ottimale e sarà possibile tooprovide probabilmente una classificazione superiore, se si esegue il push in una notifica chiedere loro toorate hello app nell'archivio di hello.</span><span class="sxs-lookup"><span data-stu-id="decf8-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="decf8-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="decf8-176">See also</span></span>
* <span data-ttu-id="decf8-177">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="decf8-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="decf8-178">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="decf8-178">[Troubleshooting Guide Service][Link 24]</span></span>

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

