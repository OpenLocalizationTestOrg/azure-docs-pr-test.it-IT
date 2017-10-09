---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="a0116-103">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a0116-103">Upgrade procedures</span></span>
<span data-ttu-id="a0116-104">Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a0116-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="a0116-105">È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a0116-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="a0116-106">Ad esempio se si esegue la migrazione da 1.4.0 too1.6.0 è toofirst seguire hello "da 1.4.0 too1.5.0" routine quindi hello "da 1.5.0 too1.6.0" stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a0116-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="a0116-107">L'aggiornamento da, indipendentemente dalla versione di hello è hello tooreplace `mobile-engagement-VERSION.jar` con hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="a0116-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="a0116-108">Da 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="a0116-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="a0116-109">Questo passaggio in realtà può essere eseguito in qualsiasi versione di hello SDK, è un miglioramento della sicurezza quando si integrano le attività di copertura.</span><span class="sxs-lookup"><span data-stu-id="a0116-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="a0116-110">È necessario ora aggiungere `exported="false"` tooall Reach attività.</span><span class="sxs-lookup"><span data-stu-id="a0116-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="a0116-111">Le attività del servizio di copertura su `AndroidManifest.xml`non devono comparire come segue:</span><span class="sxs-lookup"><span data-stu-id="a0116-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a><span data-ttu-id="a0116-112">Da 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="a0116-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="a0116-113">Hello SDK ora handle del nuovo modello di autorizzazione da Android M.</span><span class="sxs-lookup"><span data-stu-id="a0116-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="a0116-114">Se si utilizzano le funzionalità del percorso o le notifiche del quadro generale, leggere [questa sezione](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="a0116-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="a0116-115">Inoltre toohello nuovo modello di autorizzazione, è ora supportano la configurazione delle funzionalità di percorso in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0116-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="a0116-116">Ci sono ancora compatibili con parametri per il percorso del manifesto hello ma è obsoleta.</span><span class="sxs-lookup"><span data-stu-id="a0116-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="a0116-117">la configurazione di runtime toouse, Rimuovi hello nelle sezioni seguenti sono dal ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="a0116-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="a0116-118">e leggere [questo aggiornamento procedura](mobile-engagement-android-integrate-engagement.md#location-reporting) la configurazione di runtime toouse invece.</span><span class="sxs-lookup"><span data-stu-id="a0116-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="a0116-119">Da 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="a0116-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="a0116-120">Push nativo</span><span class="sxs-lookup"><span data-stu-id="a0116-120">Native push</span></span>
<span data-ttu-id="a0116-121">Push nativo (GCM/ADM) è ora anche utilizzato per notifiche in-app è necessario configurare le credenziali push nativo hello per qualsiasi tipo di campagna push.</span><span class="sxs-lookup"><span data-stu-id="a0116-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="a0116-122">Se non è già stata eseguita, completare [questa procedura](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="a0116-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="a0116-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a0116-123">AndroidManifest.xml</span></span>
<span data-ttu-id="a0116-124">L'integrazione con il servizio di copertura è stata modificata in ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="a0116-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="a0116-125">Sostituire:</span><span class="sxs-lookup"><span data-stu-id="a0116-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="a0116-126">Con</span><span class="sxs-lookup"><span data-stu-id="a0116-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="a0116-127">È ora possibile che venga visualizzata una schermata di caricamento quando si fa clic su un annuncio (con contenuto di tipo testo/Web) o un sondaggio.</span><span class="sxs-lookup"><span data-stu-id="a0116-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="a0116-128">La presenza di tooadd questo tali toowork campagne in 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="a0116-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="a0116-129">Risorse</span><span class="sxs-lookup"><span data-stu-id="a0116-129">Resources</span></span>
<span data-ttu-id="a0116-130">Incorporare hello nuovo `res/layout/engagement_loading.xml` file nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a0116-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="a0116-131">Da 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="a0116-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="a0116-132">Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a0116-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="a0116-133">Se si esegue la migrazione da una versione precedente, consultare hello Capptain sito web toomigrate too2.4.0 prima e quindi applicare hello seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="a0116-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0116-134">Capptain Engagement Mobile sono non hello stessi servizi e hello procedura indicata di seguito è la modalità toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="a0116-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="a0116-135">Migrazione hello SDK nell'applicazione hello non eseguirà la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a0116-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="a0116-136">File JAR</span><span class="sxs-lookup"><span data-stu-id="a0116-136">JAR file</span></span>
<span data-ttu-id="a0116-137">Sostituire `capptain.jar` con `mobile-engagement-VERSION.jar` nella cartella `libs`.</span><span class="sxs-lookup"><span data-stu-id="a0116-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="a0116-138">File di risorse</span><span class="sxs-lookup"><span data-stu-id="a0116-138">Resource files</span></span>
<span data-ttu-id="a0116-139">Ogni file di risorse che è stata fornita (preceduto dal prefisso `capptain_`) è toobe sostituito da hello nuovi (preceduti `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="a0116-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="a0116-140">Se tali file sono stati personalizzati, è necessario toore-applicare la personalizzazione nel file hello **tutti gli identificatori di hello nei file di risorse hello sono inoltre stati rinominati**.</span><span class="sxs-lookup"><span data-stu-id="a0116-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="a0116-141">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="a0116-141">Application ID</span></span>
<span data-ttu-id="a0116-142">Ora Engagement utilizza una connessione stringa tooconfigure hello SDK identificatori, ad esempio l'identificatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0116-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="a0116-143">Si dispone di toouse `EngagementAgent.init` metodo nell'attività di avvio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0116-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="a0116-144">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0116-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="a0116-145">Rimuovere qualsiasi chiamata troppo`CapptainAgent.configure` come `EngagementAgent.init` sostituisce tale metodo.</span><span class="sxs-lookup"><span data-stu-id="a0116-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="a0116-146">Hello `appId` non possono essere configurate tramite `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a0116-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="a0116-147">Rimuovere questa sezione da `AndroidManifest.xml`, se presente:</span><span class="sxs-lookup"><span data-stu-id="a0116-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="a0116-148">API Java</span><span class="sxs-lookup"><span data-stu-id="a0116-148">Java API</span></span>
<span data-ttu-id="a0116-149">Ogni tooany chiamata classe Java di Windows SDK è stato rinominato, toobe ad esempio, `CapptainAgent.getInstance(this)` deve essere rinominato `EngagementAgent.getInstance(this)`, `extends CapptainActivity` deve essere rinominata `extends EngagementActivity` e così via...</span><span class="sxs-lookup"><span data-stu-id="a0116-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="a0116-150">Se sono integrati con i file delle preferenze agente predefinito, il nome di file predefinito hello è ora `engagement.agent` e chiave hello è `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="a0116-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="a0116-151">Quando si creano gli annunci web, Javascript binder hello è ora `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="a0116-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="a0116-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a0116-152">AndroidManifest.xml</span></span>
<span data-ttu-id="a0116-153">Si è verificato numerose modifiche sono servizio hello non è più condivisa e numerosi destinatari non sono più esportabile.</span><span class="sxs-lookup"><span data-stu-id="a0116-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="a0116-154">dichiarazione di Hello del servizio è ora più semplice. Rimuovi filtro preventivo hello e tutti i metadati all'interno e Aggiungi `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="a0116-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="a0116-155">Oltre a tutto ciò che viene rinominato toouse engagement.</span><span class="sxs-lookup"><span data-stu-id="a0116-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="a0116-156">L'aspetto è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0116-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="a0116-157">Quando si desidera che i log dei test tooenable, hello metadati sono stato spostato toohello tag dell'applicazione e che è stato rinominato:</span><span class="sxs-lookup"><span data-stu-id="a0116-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="a0116-158">Tutti gli altri metadati dati appena sono stati rinominati, ecco l'elenco completo di hello (naturalmente Rinomina solo hello quelli utilizzare):</span><span class="sxs-lookup"><span data-stu-id="a0116-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="a0116-159">Rilevamento di Google Play e SmartAd è stato rimosso dal SDK è sufficiente tooremove questo senza sostituzione:</span><span class="sxs-lookup"><span data-stu-id="a0116-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="a0116-160">le attività di copertura Hello vengono ora dichiarate simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0116-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="a0116-161">Se si dispone di attività personalizzate di copertura, è necessario solo toochange hello azioni preventivo toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` o `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="a0116-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="a0116-162">Hello ricevitori broadcast sono stati rinominati, più è ora possibile aggiungere `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="a0116-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="a0116-163">Ecco l'elenco completo di hello di ricevitori hello con hello nuova specifica (naturalmente Rinomina solo hello quelli utilizzare):</span><span class="sxs-lookup"><span data-stu-id="a0116-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="a0116-164">Ricevitore di rilevamento è stato rimosso, in modo che sia tooremove in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="a0116-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="a0116-165">Si noti che la dichiarazione hello dell'implementazione di hello broadcast destinatario **EngagementMessageReceiver** è stata modificata in hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a0116-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="a0116-166">Questo avviene perché toosend hello API e rimuovere XMPP arbitrario messaggi da entità XMPP arbitraria e hello toosend API e ricevere messaggi tra i dispositivi sono stati rimossi.</span><span class="sxs-lookup"><span data-stu-id="a0116-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="a0116-167">Di conseguenza, è anche hello toodelete callback dal seguente il **EngagementMessageReceiver** implementazione:</span><span class="sxs-lookup"><span data-stu-id="a0116-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="a0116-168">e</span><span class="sxs-lookup"><span data-stu-id="a0116-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="a0116-169">quindi eliminare qualsiasi chiamata su **EngagementAgent** per:</span><span class="sxs-lookup"><span data-stu-id="a0116-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="a0116-170">e</span><span class="sxs-lookup"><span data-stu-id="a0116-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="a0116-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="a0116-171">Proguard</span></span>
<span data-ttu-id="a0116-172">Configurazione proguard può essere interessati da rebranding, hello regole sono ora simile:</span><span class="sxs-lookup"><span data-stu-id="a0116-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

