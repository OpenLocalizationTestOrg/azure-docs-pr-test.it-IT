---
title: Interfaccia utente di Azure Mobile Engagement - Monitoraggio
description: Informazioni su come monitorare in tempo reale i dati dell'applicazione usando Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5f8a02e35db93585e0fe46d77b3ad18b94c99597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-monitor-real-time-data-about-your-application"></a><span data-ttu-id="19444-103">Come monitorare in tempo reale i dati relativi all'applicazione</span><span class="sxs-lookup"><span data-stu-id="19444-103">How to monitor real-time data about your application</span></span>
<span data-ttu-id="19444-104">In questo articolo viene descritta la scheda **MONITORAGGIO** del portale **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="19444-104">This article describes the **MONITOR** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="19444-105">Utilizzare il portale **Mobile Engagement** per monitorare e gestire le app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="19444-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="19444-106">Si noti che per iniziare a utilizzare il portale, è innanzitutto necessario creare un account **Azure Mobile Engagement** .</span><span class="sxs-lookup"><span data-stu-id="19444-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> 

<span data-ttu-id="19444-107">Nella sezione Monitoraggio dell'interfaccia utente vengono fornite informazioni di analisi in tempo reale ed è possibile impostare gli avvisi quando vengono raggiunte le soglie per la maggior parte delle informazioni cronologicamente disponibili anche nella sezione [ANALISI](mobile-engagement-user-interface-analytics.md) dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="19444-107">The Monitor section of the UI provides real-time analytics information and allows you to set alerts when thresholds are reached for most of the same information that is available historically in the [ANALYTICS](mobile-engagement-user-interface-analytics.md) section of the UI.</span></span> <span data-ttu-id="19444-108">Nella sezione **Glossario** nell'argomento [Concetti](http://go.microsoft.com/fwlink/?LinkId=525555) sono riportate le definizioni dei termini e delle abbreviazioni usati in Analisi e Monitoraggio, ad esempio: utente attivo, nuovo utente, utente assorbito, sessione, grafico percorso utenti, mapping utenti, URL di rilevamento, tendenze, attività, evento, processo, errore, informazioni supplementari, arresto anomalo e informazioni sull'app.</span><span class="sxs-lookup"><span data-stu-id="19444-108">See the **Glossary** section in the [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) topic for definitions of terms and abbreviations in Analytics and Monitoring (such as the following: Active User, New user, Retained User, Session, User Path Graph, Users Map, Tracking URLs, Trends, Activity, Event, Job, Error, Extra Info, Crash, and App-info).</span></span>

> [!NOTE]
> <span data-ttu-id="19444-109">Molte sezioni dell'interfaccia utente del portale **Mobile Engagement** contengono il pulsante **MOSTRA GUIDA**.</span><span class="sxs-lookup"><span data-stu-id="19444-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="19444-110">Premere questo pulsante per ottenere ulteriori informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="19444-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a><span data-ttu-id="19444-111">Monitoraggio: sessioni, processi, eventi, errori e arresti anomali</span><span class="sxs-lookup"><span data-stu-id="19444-111">Monitor - Sessions, Jobs, Events, Errors, and Crashes</span></span>
<span data-ttu-id="19444-112">È possibile verificare quanti utenti sono attualmente in sessione e su schermi specifici o stanno eseguendo particolari azioni.</span><span class="sxs-lookup"><span data-stu-id="19444-112">You can see how many users are currently in session and on specific screens or doing specific actions.</span></span> <span data-ttu-id="19444-113">È possibile visualizzare l'attività dell'utente per sessioni, processi, eventi, errori e arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="19444-113">You can view user activity divided by Sessions, Jobs, Events, Errors, and Crashes.</span></span> <span data-ttu-id="19444-114">È possibile visualizzare le informazioni correnti e mostrare le informazioni dall'ora, del giorno o della settimana più recente.</span><span class="sxs-lookup"><span data-stu-id="19444-114">You can see the current information and show the information from the last hour, day, or week.</span></span> <span data-ttu-id="19444-115">È possibile visualizzare tutte le informazioni in ogni categoria o ordinarle per sessione, processo, evento, errore e arresto anomalo specifico.</span><span class="sxs-lookup"><span data-stu-id="19444-115">You can see all of the information in each category or sort by the specific Session, Job, Event, Error, and Crash.</span></span>  <span data-ttu-id="19444-116">Il monitoraggio in tempo reale è utile durante eventi quali una campagna di push per verificare se esiste un aumento nell'azione subito dopo l'invio di una notifica push.</span><span class="sxs-lookup"><span data-stu-id="19444-116">Live monitoring is helpful to use during events such as a Push campaign to see if there is an uptick in action right after you send your Push notification.</span></span>

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a><span data-ttu-id="19444-118">Risoluzione dei problemi con Monitoraggio - Eventi - Dettagli</span><span class="sxs-lookup"><span data-stu-id="19444-118">Troubleshooting with Monitor - Events - Details</span></span>
<span data-ttu-id="19444-119">La generazione di un evento nell'applicazione dal dispositivo di test e la relativa ricerca in Monitoraggio - Eventi - Dettagli è uno dei modi più semplici per trovare l'ID del dispositivo di test e per confermare che l'integrazione Azure Mobile Engagement di Analisi, Monitoraggio e Segmenti funzioni dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19444-119">Generating an event in your application from your test device and finding it in Monitor - Events - Details is one of the easiest ways to find your Device ID for your test device and to confirm that Azure Mobile Engagement integration of Analytics, Monitoring, and Segments is working from your application.</span></span> <span data-ttu-id="19444-120">Dopo aver ottenuto l'ID del dispositivo di test, è possibile aggiungerlo ai dispositivi di test in "Account personale – Dispositivi".</span><span class="sxs-lookup"><span data-stu-id="19444-120">Once you have the Device ID of your test device, you can add it to your test devices in “My Account - Devices”.</span></span> <span data-ttu-id="19444-121">Se non è possibile generare un evento, assicurarsi che Azure Mobile Engagement sia correttamente integrato nell'app Android/iOS/Web/Windows/Windows Phone con l'SDK.</span><span class="sxs-lookup"><span data-stu-id="19444-121">If you can't generate an event, make sure that Azure Mobile Engagement is correctly integrated in your Android/iOS/Web/Windows/Windows Phone app with the SDK.</span></span>

<span data-ttu-id="19444-122">Per altre informazioni, vedere [Documentazione SDK][Link 5]</span><span class="sxs-lookup"><span data-stu-id="19444-122">For more information, see:  [SDK Documentation][Link 5]</span></span>

![Monitor2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a><span data-ttu-id="19444-124">Risoluzione dei problemi con Monitoraggio - Arresti anomali - Dettagli</span><span class="sxs-lookup"><span data-stu-id="19444-124">Troubleshooting with Monitor - Crashes - Details</span></span>
<span data-ttu-id="19444-125">È possibile esaminare le informazioni sull'arresto anomalo dell'app da Monitoraggio - Arresti anomali - Dettagli per determinare il motivo per cui l'app si blocca.</span><span class="sxs-lookup"><span data-stu-id="19444-125">You can review crash information about your app from Monitor - Crashes - Details to help determine why your app is crashing.</span></span> <span data-ttu-id="19444-126">È consigliabile, inoltre, cercare i problemi noti di ogni versione dell'SDK nelle note di rilascio che accompagnano ogni versione dell'SDK per Android/iOS/Web/Windows/Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="19444-126">You should also look up known issues with each version of the SDK in the release notes for each version of the SDK for Android/iOS/Web/Windows/Windows Phone.</span></span>

<span data-ttu-id="19444-127">Per altre informazioni, vedere [Documentazione SDK - Note di rilascio][Link 5]</span><span class="sxs-lookup"><span data-stu-id="19444-127">For more information, see:  [SDK Documentation - Release notes][Link 5]</span></span>

![Monitor3][16]

## <a name="monitor---alerts"></a><span data-ttu-id="19444-129">Monitoraggio - Avvisi</span><span class="sxs-lookup"><span data-stu-id="19444-129">Monitor - Alerts</span></span>
<span data-ttu-id="19444-130">È inoltre possibile specificare condizioni per gli avvisi da inviare automaticamente all'utente tramite posta elettronica o messaggistica istantanea</span><span class="sxs-lookup"><span data-stu-id="19444-130">You can also specify conditions for Alerts that will be automatically sent to you via e-mail or instant message.</span></span> <span data-ttu-id="19444-131">(sono supportati tutti i servizi compatibili con XMPP come GTalk di Google o iChat Apple). Gli avvisi sono basati su una soglia di rilevamento predefinita maggiore (>) o minore (<) di un numero specifico di sessioni, processi, eventi, errori o arresti anomali al secondo, minuto o ora.</span><span class="sxs-lookup"><span data-stu-id="19444-131">(Any XMPP-compliant services like Google's GTalk or Apple's iChat are supported.) Alerts are based on a pre-defined detection threshold greater than (>) or less than (<) a specific number of Sessions, Jobs, Events, Errors, or Crashes per second, minute, or hour.</span></span> <span data-ttu-id="19444-132">Tramite Avvisi è possibile monitorare tutte le attività di un determinato tipo o semplicemente l'attività di un particolare processo, evento o errore.</span><span class="sxs-lookup"><span data-stu-id="19444-132">Alerts can monitor all activities of a given type, or just monitor a specific Job, Event, or Error activity.</span></span> 

<span data-ttu-id="19444-133">È inoltre possibile specificare una velocità minima di rilevamento, ossia la quantità minima di minuti che separa due notifiche per lo stesso avviso, per assicurarsi che quando viene attivato l'avviso non si riceva mai più di una notifica per ogni intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="19444-133">You can also specify a Minimum Detection Rate, which is the minimum amount of minutes that will separate two notifications for the same alert to make sure that when your alert is triggered, you will never receive more than 1 notification per interval specified.</span></span>

![Monitor4][17]

## <a name="see-also"></a><span data-ttu-id="19444-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="19444-135">See also</span></span>
* <span data-ttu-id="19444-136">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="19444-136">[Concepts][Link 6]</span></span>
* <span data-ttu-id="19444-137">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="19444-137">[Troubleshooting Guide Service][Link 24]</span></span>

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
