---
title: aaaGet avviato con Azure Mobile Engagement per la distribuzione di Unity iOS
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App Unity distribuzione tooiOS dispositivi.
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
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="c702a-103">Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in iOS</span><span class="sxs-lookup"><span data-stu-id="c702a-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="c702a-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e toosend push agli utenti di toosegmented notifiche di un'applicazione di Unity quando si distribuisce il dispositivo iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="c702a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="c702a-105">Questa esercitazione viene utilizzato hello classico Unity rollback un'esercitazione palla come punto di partenza hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="c702a-106">È opportuno seguire passaggi hello in questo [esercitazione](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement è illustrare nell'esercitazione hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="c702a-107">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c702a-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="c702a-108">Editor di Unity</span><span class="sxs-lookup"><span data-stu-id="c702a-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="c702a-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="c702a-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="c702a-110">Editor di Xcode</span><span class="sxs-lookup"><span data-stu-id="c702a-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="c702a-111">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="c702a-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c702a-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="c702a-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c702a-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="c702a-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="c702a-114"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="c702a-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="c702a-115"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="c702a-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="c702a-116">Importa pacchetto di Unity hello</span><span class="sxs-lookup"><span data-stu-id="c702a-116">Import hello Unity package</span></span>
1. <span data-ttu-id="c702a-117">Scaricare hello [pacchetto Unity Engagement Mobile](https://aka.ms/azmeunitysdk) e salvarlo tooyour di computer locale.</span><span class="sxs-lookup"><span data-stu-id="c702a-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="c702a-118">Andare troppo**risorse -> Importa pacchetto -> pacchetto personalizzato** e selezionare hello pacchetto scaricato in hello prima passo.</span><span class="sxs-lookup"><span data-stu-id="c702a-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="c702a-119">Assicurarsi che tutti i file siano selezionati e fare clic sul pulsante **Import** .</span><span class="sxs-lookup"><span data-stu-id="c702a-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="c702a-120">Dopo l'importazione ha esito positivo, verranno visualizzati i file SDK hello importato nel progetto.</span><span class="sxs-lookup"><span data-stu-id="c702a-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="c702a-121">Aggiornare hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="c702a-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="c702a-122">Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **IOS\_connessione\_stringa** con stringa di connessione hello ottenuti in precedenza dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="c702a-123">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="c702a-124">Configurare app hello per il rilevamento di base</span><span class="sxs-lookup"><span data-stu-id="c702a-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="c702a-125">Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica.</span><span class="sxs-lookup"><span data-stu-id="c702a-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="c702a-126">Aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="c702a-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="c702a-127">Aggiungere hello seguente toohello `Start()` (metodo)</span><span class="sxs-lookup"><span data-stu-id="c702a-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="c702a-128">Distribuire ed eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c702a-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="c702a-129">Connettere una macchina di tooyour dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="c702a-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="c702a-130">Aprire **File -> Build Settings** (File -> Impostazioni compilazione)</span><span class="sxs-lookup"><span data-stu-id="c702a-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="c702a-131">Selezionare **iOS** e quindi fare clic su **Switch Platform** (Cambia piattaforma)</span><span class="sxs-lookup"><span data-stu-id="c702a-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="c702a-132">Fare clic su **Player Settings** e fornire un identificatore del bundle valido.</span><span class="sxs-lookup"><span data-stu-id="c702a-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="c702a-133">Infine, fare clic su **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="c702a-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="c702a-134">Potrebbe essere richiesto tooprovide un pacchetto di cartella nome toostore hello iOS.</span><span class="sxs-lookup"><span data-stu-id="c702a-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="c702a-135">Se tutto va correttamente, verrà compilato il progetto hello e deve aprire sull'applicazione di XCode.</span><span class="sxs-lookup"><span data-stu-id="c702a-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="c702a-136">Verificare che tale hello **identificatore Bundle** sia corretto nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="c702a-137">Eseguire app hello in XCode in modo tale che il pacchetto di hello dispositivo connesso tooyour distribuito nel telefono, si dovrebbe vedere del gioco Unity!</span><span class="sxs-lookup"><span data-stu-id="c702a-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="c702a-138"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="c702a-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="c702a-139"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="c702a-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="c702a-140">Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="c702a-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="c702a-141">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="c702a-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="c702a-142">Non si dispone toodo ulteriori attività di configurazione nelle notifiche di tooreceive app ed è già il programma di installazione per tale.</span><span class="sxs-lookup"><span data-stu-id="c702a-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

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
