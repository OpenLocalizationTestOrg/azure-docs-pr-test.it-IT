---
title: Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in Android
description: "Informazioni sull'uso di Azure Mobile Engagement con funzionalità di analisi e notifiche push per le app Unity distribuite in dispositivi iOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="b8b83-103">Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in Android</span><span class="sxs-lookup"><span data-stu-id="b8b83-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="b8b83-104">Questo argomento descrive come usare Azure Mobile Engagement per ottenere informazioni sull'uso dell'app e sull'invio di notifiche push a utenti segmentati di un'applicazione Unity durante lo sviluppo in un dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="b8b83-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="b8b83-105">Questa esercitazione fa uso della classica esercitazione Roll-a-ball di Unity come punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="b8b83-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="b8b83-106">Seguire i passaggi dell' [esercitazione Roll-a-ball](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement dimostrata nell'esercitazione seguente.</span><span class="sxs-lookup"><span data-stu-id="b8b83-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="b8b83-107">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="b8b83-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="b8b83-108">Editor di Unity</span><span class="sxs-lookup"><span data-stu-id="b8b83-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="b8b83-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="b8b83-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="b8b83-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="b8b83-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="b8b83-111">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b8b83-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b8b83-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b8b83-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b8b83-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="b8b83-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="b8b83-114"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android</span><span class="sxs-lookup"><span data-stu-id="b8b83-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="b8b83-115"><a id="connecting-app"></a>Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b8b83-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="b8b83-116">Importare il pacchetto Unity</span><span class="sxs-lookup"><span data-stu-id="b8b83-116">Import the Unity package</span></span>
1. <span data-ttu-id="b8b83-117">Scaricare il [pacchetto Unity per Mobile Engagement](https://aka.ms/azmeunitysdk) e salvarlo nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="b8b83-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="b8b83-118">Passare a **Assets -> Import Package -> Custom Package** (Asset -> Importa pacchetto -> Pacchetto personalizzato) e selezionare il pacchetto scaricato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b8b83-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="b8b83-119">Assicurarsi che tutti i file siano selezionati e fare clic sul pulsante **Import** .</span><span class="sxs-lookup"><span data-stu-id="b8b83-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="b8b83-120">Al termine dell'importazione verranno visualizzati i file dell'SDK importati nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b8b83-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="b8b83-121">Aggiornare EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="b8b83-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="b8b83-122">Aprire il file di script **EngagementConfiguration** dalla cartella dell'SDK e aggiornare **ANDROID\_CONNECTION\_STRING** con la stringa di connessione ottenuta in precedenza dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b83-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="b8b83-123">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="b8b83-123">Save the file</span></span> 
3. <span data-ttu-id="b8b83-124">Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android).</span><span class="sxs-lookup"><span data-stu-id="b8b83-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="b8b83-125">Si tratta del plug-in aggiunto da Mobile Engagement SDK. Facendo clic su di esso verranno aggiornate automaticamente le impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="b8b83-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="b8b83-126">Assicurarsi di eseguire questa operazione ogni volta che si aggiorna il file **EngagementConfiguration**. In caso contrario, le modifiche non saranno applicate all'app.</span><span class="sxs-lookup"><span data-stu-id="b8b83-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="b8b83-127">Configurare l'app per il rilevamento di base</span><span class="sxs-lookup"><span data-stu-id="b8b83-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="b8b83-128">Aprire lo script **PlayerController** collegato all'oggetto Player per la modifica.</span><span class="sxs-lookup"><span data-stu-id="b8b83-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="b8b83-129">Aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="b8b83-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="b8b83-130">Aggiungere quanto segue al metodo `Start()`:</span><span class="sxs-lookup"><span data-stu-id="b8b83-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="b8b83-131">Distribuire ed eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="b8b83-131">Deploy and run the app</span></span>
<span data-ttu-id="b8b83-132">Assicurarsi che Android SDK sia installato nel computer prima di provare a distribuire l'app Unity nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8b83-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="b8b83-133">Connettere un dispositivo Android al computer.</span><span class="sxs-lookup"><span data-stu-id="b8b83-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="b8b83-134">Aprire **File -> Build Settings** (File -> Impostazioni compilazione)</span><span class="sxs-lookup"><span data-stu-id="b8b83-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="b8b83-135">Selezionare **Android** e quindi fare clic su **Switch Platform** (Cambia piattaforma)</span><span class="sxs-lookup"><span data-stu-id="b8b83-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="b8b83-136">Fare clic su **Player Settings** e fornire un identificatore del bundle valido.</span><span class="sxs-lookup"><span data-stu-id="b8b83-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="b8b83-137">Infine, fare clic su **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="b8b83-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="b8b83-138">Potrebbe essere necessario specificare un nome della cartella in cui archiviare il pacchetto Android.</span><span class="sxs-lookup"><span data-stu-id="b8b83-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="b8b83-139">Se tutto va bene, il pacchetto verrà distribuito nel dispositivo connesso e il gioco Unity sarà disponibile nel telefono.</span><span class="sxs-lookup"><span data-stu-id="b8b83-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="b8b83-140"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b8b83-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="b8b83-141"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="b8b83-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="b8b83-142">Aggiornare EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="b8b83-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="b8b83-143">Aprire il file di script **EngagementConfiguration** dalla cartella dell'SDK e aggiornare **ANDROID\_GOOGLE\_NUMBER** con il **numero di progetto Google** ottenuto in precedenza dal portale per sviluppatori di Google Cloud.</span><span class="sxs-lookup"><span data-stu-id="b8b83-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="b8b83-144">Si tratta di un valore stringa, assicurarsi quindi che sia racchiuso tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="b8b83-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="b8b83-145">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="b8b83-145">Save the file.</span></span> 
3. <span data-ttu-id="b8b83-146">Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android).</span><span class="sxs-lookup"><span data-stu-id="b8b83-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="b8b83-147">Si tratta del plug-in aggiunto da Mobile Engagement SDK. Facendo clic su di esso verranno aggiornate automaticamente le impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="b8b83-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="b8b83-148">Configurare l'app per la ricezione di notifiche</span><span class="sxs-lookup"><span data-stu-id="b8b83-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="b8b83-149">Aprire lo script **PlayerController** collegato all'oggetto Player per la modifica.</span><span class="sxs-lookup"><span data-stu-id="b8b83-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="b8b83-150">Aggiungere quanto segue al metodo `Start()` :</span><span class="sxs-lookup"><span data-stu-id="b8b83-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="b8b83-151">Ora che l'app è aggiornata, distribuire ed eseguire l'app in un dispositivo in base alle istruzioni riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="b8b83-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
