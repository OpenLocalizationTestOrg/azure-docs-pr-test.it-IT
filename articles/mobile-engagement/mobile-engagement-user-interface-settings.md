---
title: aaaAzure interfaccia utente di Mobile Engagement - impostazioni
description: Informazioni su come toomanage hello impostazioni globali dell'applicazione con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a><span data-ttu-id="662d8-103">Come toomanage hello impostazioni globali dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="662d8-103">How toomanage hello global settings of your application</span></span>
<span data-ttu-id="662d8-104">Hello **impostazioni** opzioni disponibili per una variabile di applicazione, a seconda della piattaforma hello di un'applicazione hello e autorizzazioni di hello è stato concesso per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="662d8-104">hello **Settings** menu options available for an application vary, depending on hello platform of hello application and hello permissions you have been granted for hello application.</span></span> <span data-ttu-id="662d8-105">Le impostazioni includono i seguenti hello: dettagli, progetti, Push nativo, la velocità di Push, il Tag (app info) e della pressione commerciale.</span><span class="sxs-lookup"><span data-stu-id="662d8-105">Settings include hello following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="662d8-106">opzione di menu (info app) di Tag della sezione Impostazioni hello Hello può essere gestito dall'applicazione (tramite hello SDK) o dal back-end (tramite hello API dispositivo).</span><span class="sxs-lookup"><span data-stu-id="662d8-106">hello Tag (app info) menu option of hello Settings section can be managed by your application (using hello SDK) or by your backend (using hello Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="662d8-107">Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante.</span><span class="sxs-lookup"><span data-stu-id="662d8-107">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="662d8-108">Premere tooget questo pulsante più informazioni contestuali su una sezione.</span><span class="sxs-lookup"><span data-stu-id="662d8-108">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="662d8-109">Dettagli</span><span class="sxs-lookup"><span data-stu-id="662d8-109">Details</span></span>
<span data-ttu-id="662d8-110">Consente di toochange hello nome e una descrizione del proprietario della vista hello dell'applicazione e le autorizzazioni del ruolo applicazione.</span><span class="sxs-lookup"><span data-stu-id="662d8-110">Allows you toochange hello name and description of your application, view hello owner of your application and your role permissions.</span></span> 

<span data-ttu-id="662d8-111">Configurazione Analitica consente hello e tooview o modifica giorno hello settimane avviare nel periodo di conservazione in giorni.</span><span class="sxs-lookup"><span data-stu-id="662d8-111">Analytics configuration enables  you tooview or change hello day weeks start on and hello retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="662d8-113">Progetti</span><span class="sxs-lookup"><span data-stu-id="662d8-113">Projects</span></span>
<span data-ttu-id="662d8-114">Consente di tooselect tutti i progetti da tooappear l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="662d8-114">Allows you tooselect all projects you want your application tooappear in.</span></span> 

<span data-ttu-id="662d8-115">È inoltre possibile cercare un progetto e visualizza il nome hello, descrizione, proprietario e le autorizzazioni di un progetto dell'applicazione fa parte di.</span><span class="sxs-lookup"><span data-stu-id="662d8-115">You can also search for a project and view hello name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="662d8-116">Per altre informazioni, vedere: [Documentazione UI - Home][Link 13]</span><span class="sxs-lookup"><span data-stu-id="662d8-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="662d8-118">Push nativo</span><span class="sxs-lookup"><span data-stu-id="662d8-118">Native Push</span></span>
<span data-ttu-id="662d8-119">Consente di tooregister un nuovo certificato o l'eliminazione e certificato esistente per utilizzare con push nativo.</span><span class="sxs-lookup"><span data-stu-id="662d8-119">Allows you tooregister a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="662d8-120">Push nativo consente Azure Mobile Engagement toopush tooyour in qualsiasi momento, anche quando non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="662d8-120">Native Push enables Azure Mobile Engagement toopush tooyour application at any time, even when it is not running.</span></span> 

<span data-ttu-id="662d8-121">Dopo aver fornito le credenziali o i certificati per almeno un servizio Push nativo, è possibile selezionare "In qualsiasi momento" durante la creazione di campagne Reach, nonché utilizzare hello "notifica" parametro in hello API PUSH.</span><span class="sxs-lookup"><span data-stu-id="662d8-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use hello "notifier" parameter in hello PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="662d8-122">Apple Push Notification Service (APNS)</span><span class="sxs-lookup"><span data-stu-id="662d8-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="662d8-123">tooenable Push nativo con Apple Push Notification Service hello sarà necessario tooregister il certificato.</span><span class="sxs-lookup"><span data-stu-id="662d8-123">tooenable Native Push using hello Apple Push Notification Service you will need tooregister your certificate.</span></span> <span data-ttu-id="662d8-124">Sarà necessario tipo hello toospecify del certificato come sviluppo (DEV) o produzione (produzione).</span><span class="sxs-lookup"><span data-stu-id="662d8-124">You will need toospecify hello type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="662d8-125">Sarà quindi necessario caricare la password del certificato e hello.</span><span class="sxs-lookup"><span data-stu-id="662d8-125">Then you will need upload your certificate and hello password.</span></span>

<span data-ttu-id="662d8-126">Per ulteriori informazioni, vedere: [documentazione SDK - iOS - come tooPrepare l'applicazione per le notifiche Push di Apple][Link 5]</span><span class="sxs-lookup"><span data-stu-id="662d8-126">For more information, see: [SDK Documentation - iOS - How tooPrepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="662d8-128">Servizio notifica Push Windows (WPNS)</span><span class="sxs-lookup"><span data-stu-id="662d8-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="662d8-129">tooenable Push nativo con il servizio di notifica Windows, è necessario fornire le credenziali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="662d8-129">tooenable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="662d8-130">Sono necessari l'identificatore di sicurezza del pacchetto (SID) e la chiave segreta.</span><span class="sxs-lookup"><span data-stu-id="662d8-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="662d8-132">Google Cloud Messaging per Android (GCM)</span><span class="sxs-lookup"><span data-stu-id="662d8-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="662d8-133">tooenable Push nativo con GCM, è necessario istruzioni hello toofollow da Google.</span><span class="sxs-lookup"><span data-stu-id="662d8-133">tooenable Native Push using GCM, you need toofollow hello instructions from Google.</span></span> <span data-ttu-id="662d8-134">È necessario, quindi, incollare una chiave API semplice del server, configurata senza restrizioni IP.</span><span class="sxs-lookup"><span data-stu-id="662d8-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="662d8-135">Richiede l'integrazione con hello SDK per Android 1.12.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="662d8-135">Requires integration with hello SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="662d8-136">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="662d8-136">For more information, see:</span></span> 

* <span data-ttu-id="662d8-137">[SDK documentazione Android come tooIntegrate GCM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="662d8-137">[SDK Documentation Android How tooIntegrate GCM][Link 5]</span></span>
* [<span data-ttu-id="662d8-138">Guida GCM di Google per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="662d8-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="662d8-139">Amazon Device Messaging for Android (ADM)</span><span class="sxs-lookup"><span data-stu-id="662d8-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="662d8-140">tooenable nativo Push con ADM, è necessario fornire Amazon <OAuth credentials> costituito da un ID Client e il segreto Client (richiede l'integrazione con il SDK per Android 2.1.0 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="662d8-140">tooenable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="662d8-141">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="662d8-141">For more information, see:</span></span> 

* <span data-ttu-id="662d8-142">[SDK documentazione Android come tooIntegrate ADM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="662d8-142">[SDK Documentation Android How tooIntegrate ADM][Link 5]</span></span>
* [<span data-ttu-id="662d8-143">Documentazione ADM di Amazon per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="662d8-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="662d8-145">Velocità di push</span><span class="sxs-lookup"><span data-stu-id="662d8-145">Push Speed</span></span>
<span data-ttu-id="662d8-146">Mostra velocità di push dell'applicazione corrente hello e consente una velocità di push hello toodefine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="662d8-146">Shows hello current push speed of your application and allows you toodefine hello push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="662d8-148">Tag (info app)</span><span class="sxs-lookup"><span data-stu-id="662d8-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="662d8-150">Pressione commerciale</span><span class="sxs-lookup"><span data-stu-id="662d8-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="662d8-152">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="662d8-152">See also</span></span>
* <span data-ttu-id="662d8-153">[Concetti][Link 6]</span><span class="sxs-lookup"><span data-stu-id="662d8-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="662d8-154">[Guida alla risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="662d8-154">[Troubleshooting Guide Service][Link 24]</span></span>

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

