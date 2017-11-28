---
title: aaaGet avviato con Azure Mobile Engagement per la distribuzione di Unity Android
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App Unity distribuzione tooiOS dispositivi.
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
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="9254d-103">Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in Android</span><span class="sxs-lookup"><span data-stu-id="9254d-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9254d-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e toosend push agli utenti di toosegmented notifiche di un'applicazione di Unity durante la distribuzione di dispositivo Android tooan.</span><span class="sxs-lookup"><span data-stu-id="9254d-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="9254d-105">Questa esercitazione viene utilizzato hello classico Unity rollback un'esercitazione palla come punto di partenza hello.</span><span class="sxs-lookup"><span data-stu-id="9254d-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="9254d-106">È opportuno seguire passaggi hello in questo [esercitazione](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement è illustrare nell'esercitazione hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="9254d-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="9254d-107">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9254d-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="9254d-108">Editor di Unity</span><span class="sxs-lookup"><span data-stu-id="9254d-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="9254d-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="9254d-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="9254d-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="9254d-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="9254d-111">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9254d-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9254d-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9254d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9254d-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="9254d-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="9254d-114"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android</span><span class="sxs-lookup"><span data-stu-id="9254d-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9254d-115"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="9254d-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="9254d-116">Importa pacchetto di Unity hello</span><span class="sxs-lookup"><span data-stu-id="9254d-116">Import hello Unity package</span></span>
1. <span data-ttu-id="9254d-117">Scaricare hello [pacchetto Unity Engagement Mobile](https://aka.ms/azmeunitysdk) e salvarlo tooyour di computer locale.</span><span class="sxs-lookup"><span data-stu-id="9254d-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="9254d-118">Andare troppo**risorse -> Importa pacchetto -> pacchetto personalizzato** e selezionare hello pacchetto scaricato in hello prima passo.</span><span class="sxs-lookup"><span data-stu-id="9254d-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="9254d-119">Assicurarsi che tutti i file siano selezionati e fare clic sul pulsante **Import** .</span><span class="sxs-lookup"><span data-stu-id="9254d-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="9254d-120">Dopo l'importazione ha esito positivo, verranno visualizzati i file SDK hello importato nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9254d-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="9254d-121">Aggiornare hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="9254d-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="9254d-122">Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **ANDROID\_connessione\_stringa** con stringa di connessione hello ottenuto in precedenza da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9254d-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="9254d-123">Salvare il file hello</span><span class="sxs-lookup"><span data-stu-id="9254d-123">Save hello file</span></span> 
3. <span data-ttu-id="9254d-124">Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android).</span><span class="sxs-lookup"><span data-stu-id="9254d-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="9254d-125">Si tratta di plug-in hello aggiunto da Mobile Engagement SDK hello e facendo clic su di essa verrà aggiornata automaticamente le impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="9254d-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="9254d-126">Imposta come tooexecute che ogni volta che si aggiorna hello **EngagementConfiguration** file in caso contrario non rifletteranno le modifiche nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="9254d-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="9254d-127">Configurare app hello per il rilevamento di base</span><span class="sxs-lookup"><span data-stu-id="9254d-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="9254d-128">Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica.</span><span class="sxs-lookup"><span data-stu-id="9254d-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="9254d-129">Aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="9254d-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="9254d-130">Aggiungere hello seguente toohello `Start()` (metodo)</span><span class="sxs-lookup"><span data-stu-id="9254d-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="9254d-131">Distribuire ed eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9254d-131">Deploy and run hello app</span></span>
<span data-ttu-id="9254d-132">Assicurarsi di disporre di Android SDK installati nel computer prima di tentare di toodeploy tooyour dispositivo app Unity.</span><span class="sxs-lookup"><span data-stu-id="9254d-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="9254d-133">Connettere una macchina tooyour dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="9254d-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="9254d-134">Aprire **File -> Build Settings** (File -> Impostazioni compilazione)</span><span class="sxs-lookup"><span data-stu-id="9254d-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="9254d-135">Selezionare **Android** e quindi fare clic su **Switch Platform** (Cambia piattaforma)</span><span class="sxs-lookup"><span data-stu-id="9254d-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="9254d-136">Fare clic su **Player Settings** e fornire un identificatore del bundle valido.</span><span class="sxs-lookup"><span data-stu-id="9254d-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="9254d-137">Infine, fare clic su **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="9254d-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="9254d-138">Potrebbe essere richiesto di un pacchetto Android cartella nome toostore hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="9254d-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="9254d-139">Se tutto va bene, pacchetto hello verrà distribuito tooyour connesso dispositivo e si dovrebbe essere visualizzato il gioco Unity sul telefono.</span><span class="sxs-lookup"><span data-stu-id="9254d-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="9254d-140"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9254d-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9254d-141"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="9254d-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="9254d-142">Aggiornare hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="9254d-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="9254d-143">Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **ANDROID\_GOOGLE\_numero** con hello **progetto Google Numero** è ottenuto in precedenza dal portale per sviluppatori di Google Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9254d-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="9254d-144">Si tratta di una stringa di valore per rendere tooenclose che è racchiuso tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="9254d-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="9254d-145">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="9254d-145">Save hello file.</span></span> 
3. <span data-ttu-id="9254d-146">Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android).</span><span class="sxs-lookup"><span data-stu-id="9254d-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="9254d-147">Si tratta di plug-in hello aggiunto da Mobile Engagement SDK hello e facendo clic su di essa verrà aggiornata automaticamente le impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="9254d-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="9254d-148">Configurare le notifiche di hello app tooreceive</span><span class="sxs-lookup"><span data-stu-id="9254d-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="9254d-149">Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica.</span><span class="sxs-lookup"><span data-stu-id="9254d-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="9254d-150">Aggiungere hello seguente toohello `Start()` (metodo)</span><span class="sxs-lookup"><span data-stu-id="9254d-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="9254d-151">Ora che hello app viene aggiornata, distribuire ed eseguire l'applicazione hello in un dispositivo per istruzioni hello riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="9254d-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

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
