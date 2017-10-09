---
title: aaaGet avviato con Android le app di Azure Mobile Engagement
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app Android.
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="fed9f-103">Introduzione a Azure Mobile Engagement per app Android</span><span class="sxs-lookup"><span data-stu-id="fed9f-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="fed9f-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e come toosend push agli utenti di toosegmented notifiche di un'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="fed9f-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="fed9f-105">Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fed9f-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="fed9f-106">Si creerà un'app per Android vuota che raccoglie dati di base e riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="fed9f-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fed9f-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fed9f-107">Prerequisites</span></span>
<span data-ttu-id="fed9f-108">Completato questa esercitazione richiede hello [Android Developer Tools](https://developer.android.com/sdk/index.html), che include l'ambiente di sviluppo integrato di Android Studio hello e la piattaforma Android più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="fed9f-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="fed9f-109">È inoltre necessario hello [Mobile Engagement SDK Android](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="fed9f-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed9f-110">toocomplete questa esercitazione, è necessario un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="fed9f-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="fed9f-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="fed9f-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fed9f-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="fed9f-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="fed9f-113">Configurare Mobile Engagement per l'app Android</span><span class="sxs-lookup"><span data-stu-id="fed9f-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="fed9f-114">La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="fed9f-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="fed9f-115">Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="fed9f-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="fed9f-116">Creare un'app di base con l'integrazione di Android Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="fed9f-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="fed9f-117">la documentazione completa integrazione Hello è reperibile in hello [integrazione Mobile Engagement SDK Android](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fed9f-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="fed9f-118">Creare un progetto Android</span><span class="sxs-lookup"><span data-stu-id="fed9f-118">Create an Android project</span></span>
1. <span data-ttu-id="fed9f-119">Avviare **Android Studio**e nel menu a comparsa hello, selezionare **avviare un nuovo progetto Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="fed9f-120">Specificare il nome dell'app e il dominio aziendale.</span><span class="sxs-lookup"><span data-stu-id="fed9f-120">Provide an app name and company domain.</span></span> <span data-ttu-id="fed9f-121">Prendere nota delle informazioni specificate perché saranno necessarie successivamente.</span><span class="sxs-lookup"><span data-stu-id="fed9f-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="fed9f-122">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="fed9f-123">Selezione del livello di API e del fattore di forma hello destinazione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fed9f-124">Mobile Engagement richiede almeno un livello API 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="fed9f-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="fed9f-125">Selezionare **attività vuota** qui, viene visualizzata la schermata solo hello per questa app e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="fed9f-126">Infine, lasciare le impostazioni predefinite hello e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="fed9f-127">Android Studio verranno create app demo hello in cui integrare Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fed9f-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="fed9f-128">Includere la libreria di SDK hello nel progetto</span><span class="sxs-lookup"><span data-stu-id="fed9f-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="fed9f-129">Scaricare hello [Mobile Engagement SDK Android](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="fed9f-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="fed9f-130">Estrarre la cartella di tooa hello archivio file nel computer.</span><span class="sxs-lookup"><span data-stu-id="fed9f-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="fed9f-131">Identificare libreria JAR hello per la versione corrente di questo SDK hello e copiarlo negli Appunti toohello.</span><span class="sxs-lookup"><span data-stu-id="fed9f-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="fed9f-132">Passare toohello **progetto** sezione (1) e incollare JAR hello nella cartella di librerie hello (2).</span><span class="sxs-lookup"><span data-stu-id="fed9f-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="fed9f-133">libreria di hello tooload, progetto hello di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="fed9f-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="fed9f-134">La connessione back-end Engagement tooMobile app con hello stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fed9f-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="fed9f-135">Copiare hello seguenti righe di codice nella creazione di attività hello (deve essere eseguita solo in un'unica posizione dell'applicazione, in genere attività principale di hello).</span><span class="sxs-lookup"><span data-stu-id="fed9f-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="fed9f-136">Per questa app di esempio, aprire hello MainActivity in src -> main -> cartella java e aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="fed9f-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="fed9f-137">Risolvere i riferimenti di hello premendo Alt + Invio oppure aggiunta hello seguendo le istruzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="fed9f-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="fed9f-138">Tornare indietro toohello portale classico di Azure dell'app **le informazioni di connessione** hello pagina e copia **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="fed9f-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="fed9f-139">Incollarlo hello `setConnectionString` parametro, sostituendo l'intera stringa hello mostrato nel seguente codice hello:</span><span class="sxs-lookup"><span data-stu-id="fed9f-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="fed9f-140">Aggiungere le autorizzazioni e una dichiarazione del servizio</span><span class="sxs-lookup"><span data-stu-id="fed9f-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="fed9f-141">Aggiungere questi toohello autorizzazioni manifest del progetto, immediatamente prima o dopo hello `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="fed9f-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="fed9f-142">toodeclare hello servizio agente, aggiungere il codice tra hello `<application>` e `</application>` tag:</span><span class="sxs-lookup"><span data-stu-id="fed9f-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="fed9f-143">Nel codice hello incollata, sostituire `"<Your application name>"` etichetta hello, che viene visualizzato nella hello **impostazioni** menu in cui è possibile visualizzare i servizi in esecuzione sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="fed9f-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="fed9f-144">È possibile aggiungere, ad esempio la parola hello "Servizio" in tale etichetta.</span><span class="sxs-lookup"><span data-stu-id="fed9f-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="fed9f-145">Inviare un tooMobile schermata Engagement</span><span class="sxs-lookup"><span data-stu-id="fed9f-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="fed9f-146">toostart l'invio dei dati e assicurarsi che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).</span><span class="sxs-lookup"><span data-stu-id="fed9f-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="fed9f-147">Andare troppo**Mainactivity** e aggiungere hello seguente classe di base hello tooreplace di **MainActivity** troppo**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="fed9f-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="fed9f-148">Se non è la classe base *attività*, consultare [avanzate Reporting Android](mobile-engagement-android-advanced-reporting.md) come tooinherit da classi diverse.</span><span class="sxs-lookup"><span data-stu-id="fed9f-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="fed9f-149">Commento hello linea per questo scenario di esempio semplice di seguito:</span><span class="sxs-lookup"><span data-stu-id="fed9f-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="fed9f-150">Se si desidera hello tookeep `ActionBar` nell'app, vedere [avanzate Reporting Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="fed9f-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="fed9f-151">Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="fed9f-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="fed9f-152">Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="fed9f-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="fed9f-153">Durante una campagna, Mobile Engagement consente di interagire con gli utenti e coinvolgerli tramite notifiche push e messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="fed9f-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="fed9f-154">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="fed9f-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="fed9f-155">Hello successiva sezione Imposta backup tooreceive l'app.</span><span class="sxs-lookup"><span data-stu-id="fed9f-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="fed9f-156">Copiare le risorse dell'SDK nel progetto</span><span class="sxs-lookup"><span data-stu-id="fed9f-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="fed9f-157">Spostarsi indietro tooyour SDK download del contenuto e copiare hello **res** cartella.</span><span class="sxs-lookup"><span data-stu-id="fed9f-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="fed9f-158">Tornare indietro tooAndroid Studio, seleziona hello **principale** directory dei file del progetto, quindi incollarlo tooadd hello di risorse tooyour project.</span><span class="sxs-lookup"><span data-stu-id="fed9f-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="fed9f-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fed9f-159">Next steps</span></span>
<span data-ttu-id="fed9f-160">Andare troppo[Android SDK](mobile-engagement-android-sdk-overview.md) tooget dettagliate conoscenza hello integrazione SDK.</span><span class="sxs-lookup"><span data-stu-id="fed9f-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
