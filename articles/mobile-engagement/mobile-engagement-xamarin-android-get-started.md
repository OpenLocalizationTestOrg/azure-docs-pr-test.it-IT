---
title: aaaGet avviato con Azure Mobile Engagement per xamarin
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app xamarin.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="90fe7-103">Introduzione ad Azure Mobile Engagement per app Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="90fe7-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="90fe7-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e come toosend push agli utenti di toosegmented notifiche di un'applicazione di xamarin.</span><span class="sxs-lookup"><span data-stu-id="90fe7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="90fe7-105">Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="90fe7-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="90fe7-106">Verrà creata un'app Xamarin.Android vuota che raccoglie dati di base e riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="90fe7-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="90fe7-107">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="90fe7-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="90fe7-108">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="90fe7-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="90fe7-109">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="90fe7-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="90fe7-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="90fe7-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="90fe7-111">È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="90fe7-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="90fe7-112">Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="90fe7-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="90fe7-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="90fe7-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="90fe7-114">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="90fe7-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="90fe7-115">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="90fe7-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="90fe7-116">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="90fe7-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="90fe7-117"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android</span><span class="sxs-lookup"><span data-stu-id="90fe7-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="90fe7-118"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="90fe7-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="90fe7-119">Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="90fe7-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="90fe7-120">Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="90fe7-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="90fe7-121">Creare un nuovo progetto Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="90fe7-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="90fe7-122">Avviare **Xamarin Studio** andare troppo**File** -> **New** -> **soluzione**</span><span class="sxs-lookup"><span data-stu-id="90fe7-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="90fe7-123">Selezionare **App Android** assicurarsi lingua hello selezionata è **c#** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="90fe7-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="90fe7-124">Compilare hello **nome App** hello e **identificatore organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="90fe7-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="90fe7-125">Verificare che toocheckmark **Google Play Services** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="90fe7-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="90fe7-126">Hello aggiornamento **nome progetto**, **Nome soluzione** e **percorso** se necessario, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="90fe7-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="90fe7-127">Xamarin Studio consente di creare app di hello in cui integrare Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="90fe7-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="90fe7-128">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="90fe7-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="90fe7-129">Fare clic con il pulsante destro hello **pacchetti** cartella windows soluzione hello e selezionare **Aggiungi pacchetti...**</span><span class="sxs-lookup"><span data-stu-id="90fe7-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="90fe7-130">Ricerca di hello **Xamarin SDK di Microsoft Azure Mobile Engagement** e aggiungerlo tooyour soluzione.</span><span class="sxs-lookup"><span data-stu-id="90fe7-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="90fe7-131">Aprire **Mainactivity** e aggiungere hello seguenti istruzioni using:</span><span class="sxs-lookup"><span data-stu-id="90fe7-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="90fe7-132">In hello `OnCreate` metodo, aggiungere hello seguente connessione di hello tooinitialize con back-end Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="90fe7-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="90fe7-133">Verificare che tooadd il **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="90fe7-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="90fe7-134">Aggiungere le autorizzazioni e una dichiarazione del servizio</span><span class="sxs-lookup"><span data-stu-id="90fe7-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="90fe7-135">Aprire la console di hello **Manifest.xml** file nella cartella proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="90fe7-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="90fe7-136">Selezionare la scheda origine in modo da aggiornare direttamente l'origine XML hello.</span><span class="sxs-lookup"><span data-stu-id="90fe7-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="90fe7-137">Aggiungere questi toohello autorizzazioni manifest (che è possibile trovare in hello **proprietà** cartella) del progetto, immediatamente prima o dopo hello `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="90fe7-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="90fe7-138">Aggiungere il seguente hello tra hello `<application>` e `</application>` tag servizio agente di hello toodeclare:</span><span class="sxs-lookup"><span data-stu-id="90fe7-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="90fe7-139">Nel codice hello appena incollati, sostituire `"<Your application name>"` nell'etichetta hello.</span><span class="sxs-lookup"><span data-stu-id="90fe7-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="90fe7-140">Viene visualizzato in hello **impostazioni** menu in cui gli utenti possono visualizzare i servizi in esecuzione sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="90fe7-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="90fe7-141">È possibile aggiungere, ad esempio la parola hello "Servizio" in tale etichetta.</span><span class="sxs-lookup"><span data-stu-id="90fe7-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="90fe7-142">Inviare un tooMobile schermata Engagement</span><span class="sxs-lookup"><span data-stu-id="90fe7-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="90fe7-143">In ordine toostart l'invio dei dati e garantire agli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello dello schermo.</span><span class="sxs-lookup"><span data-stu-id="90fe7-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="90fe7-144">Per eseguire questa operazione-verificare che hello `MainActivity` eredita da `EngagementActivity` anziché `Activity`.</span><span class="sxs-lookup"><span data-stu-id="90fe7-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="90fe7-145">In alternativa, se non è possibile ereditare da `EngagementActivity` è necessario aggiungere i metodi `.StartActivity` e `.EndActivity` rispettivamente in `OnResume` e `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="90fe7-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="90fe7-146"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="90fe7-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="90fe7-147"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="90fe7-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="90fe7-148">Engagement mobile permette toointeract con e raggiungere gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="90fe7-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="90fe7-149">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="90fe7-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="90fe7-150">Hello le sezioni seguenti viene impostato il tooreceive app li.</span><span class="sxs-lookup"><span data-stu-id="90fe7-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
