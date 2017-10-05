---
title: Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in iOS
description: "Informazioni sull'uso di Azure Mobile Engagement con funzionalità di analisi e notifiche push per le app Unity distribuite in dispositivi iOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="2ccf3-103">Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in iOS</span><span class="sxs-lookup"><span data-stu-id="2ccf3-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2ccf3-104">Questo argomento descrive come usare Azure Mobile Engagement per ottenere informazioni sull'uso dell'app e sull'invio di notifiche push a utenti segmentati di un'applicazione Unity durante lo sviluppo in un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="2ccf3-105">Questa esercitazione fa uso della classica esercitazione Roll-a-ball di Unity come punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="2ccf3-106">Seguire i passaggi dell' [esercitazione Roll-a-ball](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement dimostrata nell'esercitazione seguente.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="2ccf3-107">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="2ccf3-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="2ccf3-108">Editor di Unity</span><span class="sxs-lookup"><span data-stu-id="2ccf3-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="2ccf3-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="2ccf3-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="2ccf3-110">Editor di Xcode</span><span class="sxs-lookup"><span data-stu-id="2ccf3-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="2ccf3-111">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2ccf3-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ccf3-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="2ccf3-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="2ccf3-114"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="2ccf3-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="2ccf3-115"><a id="connecting-app"></a>Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2ccf3-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="2ccf3-116">Importare il pacchetto Unity</span><span class="sxs-lookup"><span data-stu-id="2ccf3-116">Import the Unity package</span></span>
1. <span data-ttu-id="2ccf3-117">Scaricare il [pacchetto Unity per Mobile Engagement](https://aka.ms/azmeunitysdk) e salvarlo nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="2ccf3-118">Passare a **Assets -> Import Package -> Custom Package** (Asset -> Importa pacchetto -> Pacchetto personalizzato) e selezionare il pacchetto scaricato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="2ccf3-119">Assicurarsi che tutti i file siano selezionati e fare clic sul pulsante **Import** .</span><span class="sxs-lookup"><span data-stu-id="2ccf3-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="2ccf3-120">Al termine dell'importazione verranno visualizzati i file dell'SDK importati nel progetto.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="2ccf3-121">Aggiornare EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="2ccf3-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="2ccf3-122">Aprire il file di script **EngagementConfiguration** dalla cartella dell'SDK e aggiornare **IOS\_CONNECTION\_STRING** con la stringa di connessione ottenuta in precedenza dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="2ccf3-123">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="2ccf3-124">Configurare l'app per il rilevamento di base</span><span class="sxs-lookup"><span data-stu-id="2ccf3-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="2ccf3-125">Aprire lo script **PlayerController** collegato all'oggetto Player per la modifica.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="2ccf3-126">Aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="2ccf3-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="2ccf3-127">Aggiungere quanto segue al metodo `Start()`:</span><span class="sxs-lookup"><span data-stu-id="2ccf3-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="2ccf3-128">Distribuire ed eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="2ccf3-128">Deploy and run the app</span></span>
1. <span data-ttu-id="2ccf3-129">Connettere un dispositivo iOS al computer.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="2ccf3-130">Aprire **File -> Build Settings** (File -> Impostazioni compilazione)</span><span class="sxs-lookup"><span data-stu-id="2ccf3-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="2ccf3-131">Selezionare **iOS** e quindi fare clic su **Switch Platform** (Cambia piattaforma)</span><span class="sxs-lookup"><span data-stu-id="2ccf3-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="2ccf3-132">Fare clic su **Player Settings** e fornire un identificatore del bundle valido.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="2ccf3-133">Infine, fare clic su **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="2ccf3-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="2ccf3-134">Potrebbe essere necessario specificare un nome della cartella in cui archiviare il pacchetto iOS.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="2ccf3-135">Se tutto va bene, il progetto verrà compilato e sarà possibile aprirlo nell'applicazione Xcode.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="2ccf3-136">Assicurarsi che l' **identificatore del bundle** sia corretto nel progetto.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="2ccf3-137">A questo punto, eseguire l'app in Xcode in modo che il pacchetto venga distribuito nel dispositivo connesso. Il gioco Unity dovrebbe essere disponibile nel telefono.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="2ccf3-138"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="2ccf3-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="2ccf3-139"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="2ccf3-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="2ccf3-140">Mobile Engagement consente di interagire con gli utenti e coinvolgerli tramite notifiche push e messaggistica in-app nel contesto delle campagne.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="2ccf3-141">Questo modulo è denominato REACH nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2ccf3-142">Non è necessario eseguire altre operazioni di configurazione nell'app per ricevere notifiche, perché è già configurata.</span><span class="sxs-lookup"><span data-stu-id="2ccf3-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
