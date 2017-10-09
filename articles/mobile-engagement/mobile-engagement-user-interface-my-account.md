---
title: aaaAzure interfaccia utente di Mobile Engagement - Account personale
description: Informazioni su come toomanage i dispositivi di test e profilo di account con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1d85f0e87c43605f59f6536ae42a7fb6a99ee36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-your-account-profile-and-test-devices"></a><span data-ttu-id="22397-103">Come toomanage i dispositivi di test e profilo di account</span><span class="sxs-lookup"><span data-stu-id="22397-103">How toomanage your account profile and test devices</span></span>
<span data-ttu-id="22397-104">Questo articolo descrive hello **Home** pagina di hello **Mobile Engagement** portale.</span><span class="sxs-lookup"><span data-stu-id="22397-104">This article describes hello **Home** page of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="22397-105">Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="22397-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> 

<span data-ttu-id="22397-106">tooget toohello **il mio account** pagina, fare clic sull'account in primo piano hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="22397-106">tooget toohello **my account** page, click on your account on hello top of hello page.</span></span>

<span data-ttu-id="22397-107">Hello conto nella sezione dell'interfaccia utente è in cui è possibile visualizzare e modificare le impostazioni di hello associate al proprio account, tra cui impostazioni del profilo e verificare l'ID dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="22397-107">hello My Account section of hello UI is where you can view and change hello settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="22397-108">Queste impostazioni contengono elementi che è possibile accedere tramite l'API dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="22397-108">These settings contain items that can also be accessed via hello Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="22397-110">Profilo:</span><span class="sxs-lookup"><span data-stu-id="22397-110">Profile:</span></span>
<span data-ttu-id="22397-111">È possibile visualizzare o modificare le impostazioni del proprio account mostrate di seguito:</span><span class="sxs-lookup"><span data-stu-id="22397-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="22397-112">È inoltre possibile assegnare un altro utente dell'autorizzazione toouse l'applicazione in base agli indirizzi di posta elettronica da hello [Home](mobile-engagement-user-interface-home.md).</span><span class="sxs-lookup"><span data-stu-id="22397-112">You can also give another user permission toouse your application based on their e-mail address from hello [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="22397-114">Dispositivi:</span><span class="sxs-lookup"><span data-stu-id="22397-114">Devices:</span></span>
<span data-ttu-id="22397-115">È possibile visualizzare, aggiungere o rimuovere test ID dispositivo di dispositivi di test hello che è possibile utilizzare tootest il **raggiungere** o **push** campagne.</span><span class="sxs-lookup"><span data-stu-id="22397-115">You can view, add, or remove test Device ID's of hello test devices that you can use tootest your **reach** or **push** campaigns.</span></span> <span data-ttu-id="22397-116">Le istruzioni contestuali per la modalità toofind hello ID dispositivo dei dispositivi per ogni piattaforma (iOS, Android, Windows Phone, e così via) vengono visualizzati quando si fa clic su "Nuovo dispositivo".</span><span class="sxs-lookup"><span data-stu-id="22397-116">Contextual instructions for how toofind hello Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="22397-118">toouse Push API o l'API dispositivo è necessario tooknow identificatore univoco del dispositivo degli utenti (parametro deviceid hello).</span><span class="sxs-lookup"><span data-stu-id="22397-118">toouse Push API or Device API you need tooknow your users' unique device identifier (hello deviceid parameter).</span></span> <span data-ttu-id="22397-119">Esistono diversi modi tooretrieve è:</span><span class="sxs-lookup"><span data-stu-id="22397-119">There are several ways tooretrieve it:</span></span>

1. <span data-ttu-id="22397-120">Dal back-end, è possibile utilizzare funzionalità di "Get" hello di hello API dispositivo tooget hello elenco completo degli identificatori di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22397-120">From your backend, you can use hello "Get" feature of hello Device API tooget hello full list of device identifiers.</span></span>
2. <span data-ttu-id="22397-121">Dall'app, è possibile utilizzare tooget SDK hello è.</span><span class="sxs-lookup"><span data-stu-id="22397-121">From your app, you can use hello SDK tooget it.</span></span> <span data-ttu-id="22397-122">(In Android, chiamare hello getDeviceID() funzione hello Agent (classe), e in iOS, leggere proprietà deviceid hello hello classe agente)</span><span class="sxs-lookup"><span data-stu-id="22397-122">(On Android, call hello getDeviceID() function of hello Agent class, and on iOS, read hello deviceid property of hello Agent class.)</span></span>
3. <span data-ttu-id="22397-123">Da un annuncio Reach, se associata a annuncio hello all'URL di azione hello contiene il modello di hello {deviceid}, si verrà automaticamente sostituito con identificatore hello del dispositivo hello hello azione di trigger.</span><span class="sxs-lookup"><span data-stu-id="22397-123">From a Reach announcement, if hello action URL associated with hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device triggering hello action.</span></span>
   <span data-ttu-id="22397-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata verrà sostituito con: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span><span class="sxs-lookup"><span data-stu-id="22397-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="22397-125">Da un annuncio web Reach, se il codice HTML di annuncio hello hello contiene il modello di hello {deviceid}, si verrà automaticamente sostituito con identificatore hello del dispositivo che hello Visualizza l'annuncio di hello web.</span><span class="sxs-lookup"><span data-stu-id="22397-125">From a Reach web announcement, if hello HTML code of hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device displaying hello web announcement.</span></span>
   <span data-ttu-id="22397-126">Ecco l'identificatore del dispositivo: {deviceid} verrà sostituito da: Ecco l'identificatore del dispositivo: XXXXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="22397-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="22397-127">Aprire l'applicazione sul dispositivo ed eseguire un evento nell'app contrassegnata.</span><span class="sxs-lookup"><span data-stu-id="22397-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="22397-128">Da parte dell'interfaccia utente, gli eventi di app - Monitor - - "Dettagli", trovare hello evento effettuata nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="22397-128">From "UI - your app - Monitor - Events - Details", find hello Event you performed in hello list.</span></span>
   <span data-ttu-id="22397-129">Fare clic toothis evento hello Monitor.</span><span class="sxs-lookup"><span data-stu-id="22397-129">Click toothis event in hello Monitor.</span></span>
   <span data-ttu-id="22397-130">È necessario trovare l'ID dispositivo nell'elenco di hello dei dispositivi hello che hanno eseguito questo evento.</span><span class="sxs-lookup"><span data-stu-id="22397-130">You should find your Device ID in hello list of hello devices that have performed this event.</span></span>
   <span data-ttu-id="22397-131">Quindi, è possibile copiare l'ID dispositivo e registrarlo in hello "Dispositivi - Account - UI - nuovo dispositivo, selezionare la piattaforma del dispositivo".</span><span class="sxs-lookup"><span data-stu-id="22397-131">Then, you can copy this Device ID and register it in hello "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="22397-132">(Tenere presente che quando IDFA è disabilitato per iOS, hello ID dispositivo può modificare il tempo di hello se si disinstalla e reinstalla l'applicazione.)</span><span class="sxs-lookup"><span data-stu-id="22397-132">(Be aware that when IDFA is disabled for iOS, hello Device ID may change over hello time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="22397-133">Guida per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="22397-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="22397-134">[Guida per la risoluzione dei problemi - Assistenza][Link 24]</span><span class="sxs-lookup"><span data-stu-id="22397-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="22397-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="22397-135">See also</span></span>
* <span data-ttu-id="22397-136">[Documentazione dell'interfaccia utente - Home page][Link 13]</span><span class="sxs-lookup"><span data-stu-id="22397-136">[UI Documentation - Home][Link 13]</span></span>

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




