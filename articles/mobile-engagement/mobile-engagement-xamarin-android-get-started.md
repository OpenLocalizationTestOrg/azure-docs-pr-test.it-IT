---
title: Introduzione ad Azure Mobile Engagement per Xamarin.Android
description: "Informazioni sull'uso di Azure Mobile Engagement con funzionalità di analisi e notifiche push per le app Xamarin.Android."
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
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="78a22-103">Introduzione ad Azure Mobile Engagement per app Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="78a22-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="78a22-104">Questo argomento descrive come usare Azure Mobile Engagement per ottenere informazioni sull'uso dell'app e sull'invio di notifiche push a utenti segmentati di un'applicazione Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="78a22-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="78a22-105">Questa esercitazione illustra uno scenario di trasmissione semplice tramite Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="78a22-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="78a22-106">Verrà creata un'app Xamarin.Android vuota che raccoglie dati di base e riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="78a22-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="78a22-107">Il servizio Azure Mobile Engagement verrà ritirato a marzo 2018 ed è attualmente disponibile solo per i clienti esistenti.</span><span class="sxs-lookup"><span data-stu-id="78a22-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="78a22-108">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="78a22-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="78a22-109">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="78a22-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="78a22-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="78a22-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="78a22-111">È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="78a22-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="78a22-112">Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="78a22-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="78a22-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="78a22-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="78a22-114">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="78a22-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="78a22-115">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="78a22-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="78a22-116">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="78a22-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="78a22-117"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android</span><span class="sxs-lookup"><span data-stu-id="78a22-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="78a22-118"><a id="connecting-app"></a>Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="78a22-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="78a22-119">Questa esercitazione presenta una "integrazione di base", che è la configurazione minima necessaria per raccogliere i dati e inviare una notifica push.</span><span class="sxs-lookup"><span data-stu-id="78a22-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="78a22-120">Verrà creata un'app di base con Xamarin Studio per illustrare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="78a22-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="78a22-121">Creare un nuovo progetto Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="78a22-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="78a22-122">Avviare **Xamarin Studio** e passare a **File** -> **New** ->  (Nuovo) **Solution** (Soluzione)</span><span class="sxs-lookup"><span data-stu-id="78a22-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="78a22-123">Selezionare **Android App** (App Android), assicurarsi che il linguaggio selezionato sia **C#** e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="78a22-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="78a22-124">Specificare le informazioni richieste nei campi **App Name** (Nome app) e **Organization Identifier** (Identificatore organizzazione).</span><span class="sxs-lookup"><span data-stu-id="78a22-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="78a22-125">Assicurarsi di selezionare **Google Play Services** con un segno di spunta e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="78a22-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="78a22-126">Aggiornare i campi **Project Name** (Nome progetto), **Solution Name** (Nome soluzione) e **Location** (Posizione), se necessario, e fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="78a22-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="78a22-127">Xamarin Studio creerà l'app in cui verrà integrato Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="78a22-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="78a22-128">Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="78a22-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="78a22-129">Fare clic con il pulsante destro del mouse sulla cartella **Packages** (Pacchetti) nelle finestre della soluzione, quindi scegliere **Add Packages...** (Aggiungi pacchetti)</span><span class="sxs-lookup"><span data-stu-id="78a22-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="78a22-130">Cercare **Microsoft Azure Mobile Engagement Xamarin SDK** e aggiungerlo alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="78a22-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="78a22-131">Aprire **MainActivity.cs** e aggiungere le istruzioni using seguenti:</span><span class="sxs-lookup"><span data-stu-id="78a22-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="78a22-132">Nel metodo `OnCreate` aggiungere quanto segue per inizializzare la connessione con il back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="78a22-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="78a22-133">Assicurarsi di aggiungere **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="78a22-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="78a22-134">Aggiungere le autorizzazioni e una dichiarazione del servizio</span><span class="sxs-lookup"><span data-stu-id="78a22-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="78a22-135">Aprire il file **Manifest.xml** nella cartella Properties.</span><span class="sxs-lookup"><span data-stu-id="78a22-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="78a22-136">Selezionare la scheda Source per aggiornare direttamente l'origine XML.</span><span class="sxs-lookup"><span data-stu-id="78a22-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="78a22-137">Aggiungere queste autorizzazioni al file Manifest.xml, nella cartella **Properties** del progetto, immediatamente prima o dopo il tag `<application>`:</span><span class="sxs-lookup"><span data-stu-id="78a22-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="78a22-138">Aggiungere quanto indicato sotto tra i tag `<application>` e `</application>` per dichiarare il servizio agente:</span><span class="sxs-lookup"><span data-stu-id="78a22-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="78a22-139">Nel codice appena incollato sostituire `"<Your application name>"` nell'etichetta.</span><span class="sxs-lookup"><span data-stu-id="78a22-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="78a22-140">Questo è il valore visualizzato nel menu **Impostazioni** , che mostra all'utente i servizi in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="78a22-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="78a22-141">È possibile aggiungere la parola "Service" all'etichetta, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="78a22-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="78a22-142">Inviare una schermata a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="78a22-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="78a22-143">Per iniziare a inviare dati e assicurarsi che gli utenti siano attivi, è necessario inviare almeno una schermata al back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="78a22-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="78a22-144">Per eseguire questa operazione, assicurarsi che `MainActivity` erediti da `EngagementActivity` anziché da `Activity`.</span><span class="sxs-lookup"><span data-stu-id="78a22-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="78a22-145">In alternativa, se non è possibile ereditare da `EngagementActivity` è necessario aggiungere i metodi `.StartActivity` e `.EndActivity` rispettivamente in `OnResume` e `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="78a22-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="78a22-146"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="78a22-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="78a22-147"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="78a22-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="78a22-148">Mobile Engagement consente di interagire con gli utenti e COINVOLGERLI tramite notifiche push e messaggistica in-app nel contesto di campagne.</span><span class="sxs-lookup"><span data-stu-id="78a22-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="78a22-149">Questo modulo è denominato REACH nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="78a22-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="78a22-150">Le sezioni seguenti consentono di configurare l'app per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="78a22-150">The following sections sets up your app to receive them.</span></span>

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
