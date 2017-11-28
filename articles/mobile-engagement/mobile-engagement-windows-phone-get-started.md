---
title: iniziare con le app di Azure Mobile Engagement per Windows Phone Silverlight aaaGet
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app di Windows Phone Silverlight.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="efd9a-103">Introduzione ad Azure Mobile Engagement per app per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="efd9a-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="efd9a-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche di un'applicazione Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="efd9a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="efd9a-105">Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="efd9a-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="efd9a-106">Si creerà un'app per Windows Phone Silverlight vuota che raccoglie dati di base e riceve notifiche push tramite il Servizio notifica push Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="efd9a-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="efd9a-107">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="efd9a-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="efd9a-108">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="efd9a-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="efd9a-109">I progetti Windows Phone 8.1 e versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="efd9a-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="efd9a-110">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="efd9a-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="efd9a-111">Se la destinazione è Windows Phone 8.1 (non Silverlight), fare riferimento toohello [esercitazione universali di Windows](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="efd9a-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="efd9a-112">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="efd9a-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="efd9a-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="efd9a-113">Visual Studio 2013</span></span>
* <span data-ttu-id="efd9a-114">[MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="efd9a-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="efd9a-115">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="efd9a-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="efd9a-116">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="efd9a-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="efd9a-117">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="efd9a-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="efd9a-118"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app per Windows Phone</span><span class="sxs-lookup"><span data-stu-id="efd9a-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="efd9a-119"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="efd9a-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="efd9a-120">Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="efd9a-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="efd9a-121">la documentazione completa integrazione Hello è reperibile in hello [integrazione Mobile Engagement SDK di Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="efd9a-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="efd9a-122">Verrà creata un'applicazione di base con l'integrazione di Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="efd9a-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="efd9a-123">Creare un nuovo progetto Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="efd9a-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="efd9a-124">Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efd9a-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="efd9a-125">Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="efd9a-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="efd9a-126">Nel menu a comparsa hello, selezionare **Windows 8** -> **Windows Phone** -> **applicazione vuota (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="efd9a-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="efd9a-127">Compilare app hello **nome** e **Nome soluzione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efd9a-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="efd9a-128">È possibile scegliere di tootarget **Windows Phone 8.0** o **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="efd9a-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="efd9a-129">Ora è stata creata una nuova app di Windows Phone Silverlight in cui integrare hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="efd9a-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="efd9a-130">La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="efd9a-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="efd9a-131">Installare hello [MicrosoftAzure.MobileEngagement] pacchetto nuget nel progetto.</span><span class="sxs-lookup"><span data-stu-id="efd9a-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="efd9a-132">Aprire `WMAppManifest.xml` , nella cartella proprietà di hello e accertarsi che siano dichiarate seguente hello (aggiungerli se non sono) in hello `<Capabilities />` tag:</span><span class="sxs-lookup"><span data-stu-id="efd9a-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="efd9a-133">Incollare una stringa di connessione hello copiato in precedenza per l'applicazione di Mobile Engagement ora e incollarlo in hello `Resources\EngagementConfiguration.xml` file tra hello `<connectionString>` e `</connectionString>` tag:</span><span class="sxs-lookup"><span data-stu-id="efd9a-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="efd9a-134">In hello `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="efd9a-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="efd9a-135">a.</span><span class="sxs-lookup"><span data-stu-id="efd9a-135">a.</span></span> <span data-ttu-id="efd9a-136">Aggiungere hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="efd9a-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="efd9a-137">b.</span><span class="sxs-lookup"><span data-stu-id="efd9a-137">b.</span></span> <span data-ttu-id="efd9a-138">Inizializzare Ciao SDK hello `Application_Launching` metodo:</span><span class="sxs-lookup"><span data-stu-id="efd9a-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="efd9a-139">c.</span><span class="sxs-lookup"><span data-stu-id="efd9a-139">c.</span></span> <span data-ttu-id="efd9a-140">Inserire il seguente hello in hello `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="efd9a-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="efd9a-141"><a id="monitor"></a>Abilitare il monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="efd9a-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="efd9a-142">In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).</span><span class="sxs-lookup"><span data-stu-id="efd9a-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="efd9a-143">In hello MainPage.xaml.cs, aggiungere hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="efd9a-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="efd9a-144">Sostituire la classe base hello di **MainPage**, che si trova prima **PhoneApplicationPage**, con **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="efd9a-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="efd9a-145">Nel file `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="efd9a-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="efd9a-146">a.</span><span class="sxs-lookup"><span data-stu-id="efd9a-146">a.</span></span> <span data-ttu-id="efd9a-147">Aggiungere le dichiarazioni di spazi dei nomi tooyour:</span><span class="sxs-lookup"><span data-stu-id="efd9a-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="efd9a-148">b.</span><span class="sxs-lookup"><span data-stu-id="efd9a-148">b.</span></span> <span data-ttu-id="efd9a-149">Sostituire `phone:PhoneApplicationPage` nei nomi di tag XML hello con `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="efd9a-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="efd9a-150"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="efd9a-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="efd9a-151"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="efd9a-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="efd9a-152">Engagement mobile permette toointeract e raggiungere gli utenti con le notifiche Push e la messaggistica in-app nel contesto di hello delle campagne.</span><span class="sxs-lookup"><span data-stu-id="efd9a-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="efd9a-153">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="efd9a-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="efd9a-154">Hello nelle sezioni seguenti impostarle backup tooreceive l'app.</span><span class="sxs-lookup"><span data-stu-id="efd9a-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="efd9a-155">Abilitare il tooreceive app le notifiche Push MPNS</span><span class="sxs-lookup"><span data-stu-id="efd9a-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="efd9a-156">Aggiungere nuove funzionalità tooyour `WMAppManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="efd9a-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="efd9a-157">Inizializzare hello REACH SDK</span><span class="sxs-lookup"><span data-stu-id="efd9a-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="efd9a-158">In `App.xaml.cs`, chiamare `EngagementReach.Instance.Init();` in hello **Application_Launching** funzione, subito dopo l'inizializzazione dell'agente di hello:</span><span class="sxs-lookup"><span data-stu-id="efd9a-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="efd9a-159">In `App.xaml.cs`, chiamare `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** funzione, subito dopo l'inizializzazione dell'agente di hello:</span><span class="sxs-lookup"><span data-stu-id="efd9a-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="efd9a-160">Le impostazioni sono state completate.</span><span class="sxs-lookup"><span data-stu-id="efd9a-160">You're all set.</span></span> <span data-ttu-id="efd9a-161">Ora è necessario verificare di avere eseguito correttamente l'integrazione di base.</span><span class="sxs-lookup"><span data-stu-id="efd9a-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="efd9a-162"><a id="send"></a>Invia un'app tooyour notifica</span><span class="sxs-lookup"><span data-stu-id="efd9a-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="efd9a-163">Dovrebbe essere una notifica sul dispositivo che verrà visualizzati come una notifica in-app se app hello è aperto in caso contrario come notifica di tipo avviso popup hello seguente:</span><span class="sxs-lookup"><span data-stu-id="efd9a-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
