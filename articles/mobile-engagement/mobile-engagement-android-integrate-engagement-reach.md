---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="d52ba-103">La modalità di copertura di Engagement tooIntegrate in Android</span><span class="sxs-lookup"><span data-stu-id="d52ba-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d52ba-104">È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="d52ba-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="d52ba-105">Integrazione standard</span><span class="sxs-lookup"><span data-stu-id="d52ba-105">Standard integration</span></span>

<span data-ttu-id="d52ba-106">Copiare il file di risorse di copertura hello SDK nel progetto:</span><span class="sxs-lookup"><span data-stu-id="d52ba-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="d52ba-107">Copiare i file hello da hello `res/layout` cartella recapitati con hello SDK in hello `res/layout` cartella dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="d52ba-108">Copiare i file hello da hello `res/drawable` cartella recapitati con hello SDK in hello `res/drawable` cartella dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="d52ba-109">Modificare il file `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="d52ba-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="d52ba-110">Aggiungere hello successiva sezione (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="d52ba-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* <span data-ttu-id="d52ba-111">È necessario questa autorizzazione tooreplay le notifiche di sistema che non sono stati scelto all'avvio (in caso contrario verranno mantenuti su disco, ma non potranno essere visualizzati più, è importante tooinclude questo).</span><span class="sxs-lookup"><span data-stu-id="d52ba-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="d52ba-112">Specificare un'icona utilizzata per le notifiche (entrambi in app e quelli di sistema) copiando e la modifica seguente sezione hello (tra hello `<application>` e `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="d52ba-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="d52ba-113">Questa sezione è **obbligatoria** se si prevede di usare le notifiche di sistema durante la creazione di campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="d52ba-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="d52ba-114">Android impedisce la visualizzazione di notifiche di sistema senza icone.</span><span class="sxs-lookup"><span data-stu-id="d52ba-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="d52ba-115">Pertanto se si omette questa sezione, gli utenti finali non saranno in grado di tooreceive li.</span><span class="sxs-lookup"><span data-stu-id="d52ba-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="d52ba-116">Se si creano le campagne con le notifiche di sistema utilizzando quadro generale, è necessario hello tooadd queste autorizzazioni (dopo hello `</application>` tag) mancanti:</span><span class="sxs-lookup"><span data-stu-id="d52ba-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="d52ba-117">Per Android M e se l'applicazione è destinata al livello dell’API Android 23 o superiore, l’autorizzazione ``WRITE_EXTERNAL_STORAGE`` richiede l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d52ba-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="d52ba-118">Leggere [questa sezione](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="d52ba-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="d52ba-119">Per le notifiche di sistema, che è inoltre possibile specificare in hello raggiungere campagna se il dispositivo hello deve dell'anello e/o vibrare.</span><span class="sxs-lookup"><span data-stu-id="d52ba-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="d52ba-120">Per tale toowork, aver toomake che è stata dichiarata hello seguente autorizzazione (dopo hello `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="d52ba-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="d52ba-121">Senza questa autorizzazione, Android impedisce che vengano visualizzate notifiche di sistema se è stata selezionata l'anello hello o hello vibrare opzione responsabile della campagna raggiungere hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="d52ba-122">Push nativo</span><span class="sxs-lookup"><span data-stu-id="d52ba-122">Native Push</span></span>
<span data-ttu-id="d52ba-123">Ora che è stato configurato modulo Reach, è necessario campagne tooconfigure push nativo toobe tooreceive in grado di hello sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="d52ba-124">Sono supportati due servizi su Android:</span><span class="sxs-lookup"><span data-stu-id="d52ba-124">We support two services on Android:</span></span>

* <span data-ttu-id="d52ba-125">I dispositivi Google Play: utilizzare [Google Cloud Messaging] dal seguente hello [come tooIntegrate GCM con Engagement Guida](mobile-engagement-android-gcm-integrate.md) Guida.</span><span class="sxs-lookup"><span data-stu-id="d52ba-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="d52ba-126">Dispositivi Amazon: utilizzare [Amazon Device Messaging] dal seguente hello [come tooIntegrate ADM con Engagement Guida](mobile-engagement-android-adm-integrate.md) Guida.</span><span class="sxs-lookup"><span data-stu-id="d52ba-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="d52ba-127">Se si desidera tootarget dispositivi Amazon sia Google Play, il relativo toohave possibili tutto il contenuto 1 AndroidManifest.xml/APK per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d52ba-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="d52ba-128">Ma quando si inviano tooAmazon, essi possono rifiutare l'applicazione se è disponibile codice GCM.</span><span class="sxs-lookup"><span data-stu-id="d52ba-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="d52ba-129">In tale caso, usare più file APK.</span><span class="sxs-lookup"><span data-stu-id="d52ba-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="d52ba-130">**L'applicazione è ora visualizzato e pronto tooreceive raggiungere campagne!**</span><span class="sxs-lookup"><span data-stu-id="d52ba-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="d52ba-131">Come eseguire il push dei dati toohandle</span><span class="sxs-lookup"><span data-stu-id="d52ba-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="d52ba-132">Integrazione</span><span class="sxs-lookup"><span data-stu-id="d52ba-132">Integration</span></span>
<span data-ttu-id="d52ba-133">Se si desidera toobe l'applicazione è in grado di inserisce tooreceive dati Reach, avere toocreate una sottoclasse di `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e farvi riferimento in hello `AndroidManifest.xml` file (tra hello `<application>` e/o `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="d52ba-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="d52ba-134">È possibile eseguire l'override di hello `onDataPushStringReceived` e `onDataPushBase64Received` callback.</span><span class="sxs-lookup"><span data-stu-id="d52ba-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="d52ba-135">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d52ba-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="d52ba-136">Categoria</span><span class="sxs-lookup"><span data-stu-id="d52ba-136">Category</span></span>
<span data-ttu-id="d52ba-137">il parametro di categoria Hello è facoltativo quando si crea una campagna Push di dati e consente che inserisce dati toofilter.</span><span class="sxs-lookup"><span data-stu-id="d52ba-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="d52ba-138">Ciò è utile se si dispone di più ricevitori broadcast la gestione di tipi diversi di push di dati, o se si desidera toopush diversi tipi di `Base64` tooidentify dati e si desidera tipo prima dell'analisi li.</span><span class="sxs-lookup"><span data-stu-id="d52ba-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="d52ba-139">Parametro restituito dai callback</span><span class="sxs-lookup"><span data-stu-id="d52ba-139">Callbacks' return parameter</span></span>
<span data-ttu-id="d52ba-140">Ecco alcune linee guida tooproperly handle hello parametro restituito di `onDataPushStringReceived` e `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="d52ba-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="d52ba-141">Deve restituire un ricevitore broadcast `null` nel callback hello se non conosce push toohandle un tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="d52ba-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="d52ba-142">È consigliabile utilizzare hello categoria toodetermine se il ricevitore broadcast deve gestire il push di dati hello o non.</span><span class="sxs-lookup"><span data-stu-id="d52ba-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="d52ba-143">Uno dei hello broadcast destinatario deve restituire `true` nel callback hello se accetta il push di dati di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="d52ba-144">Uno dei hello broadcast destinatario deve restituire `false` nel callback hello se riconosce il push di dati di hello, ma ignora per qualsiasi motivo.</span><span class="sxs-lookup"><span data-stu-id="d52ba-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="d52ba-145">Ad esempio, restituire `false` quando hello ha ricevuto dati non sono validi.</span><span class="sxs-lookup"><span data-stu-id="d52ba-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="d52ba-146">Se uno broadcast destinatario restituisce `true` mentre un altro restituisce `false` per hello stesso push di dati, il comportamento di hello è definito, è consigliabile non farlo.</span><span class="sxs-lookup"><span data-stu-id="d52ba-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="d52ba-147">tipo restituito di Hello viene usato solo per le statistiche di copertura hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="d52ba-148">`Replied`viene incrementato se uno di ricevitori broadcast hello ha restituito uno `true` o `false`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="d52ba-149">`Actioned`viene incrementato solo se uno di hello broadcast ricevitori restituiti `true`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="d52ba-150">Come le campagne toocustomize</span><span class="sxs-lookup"><span data-stu-id="d52ba-150">How toocustomize campaigns</span></span>
<span data-ttu-id="d52ba-151">toocustomize campagne, è possibile modificare il layout di hello forniti in hello Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="d52ba-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="d52ba-152">È consigliabile mantenere tutti gli identificatori di hello utilizzati nei layout hello e mantenere hello tipi di viste di hello che utilizzano un identificatore, soprattutto per visualizzazioni di testo e immagine.</span><span class="sxs-lookup"><span data-stu-id="d52ba-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="d52ba-153">Alcune visualizzazioni sono toohide solo utilizzato o mostrano aree in modo relativo tipo può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="d52ba-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="d52ba-154">Controllare il codice sorgente hello se si prevede di tipo hello toochange di una visualizzazione in layout hello fornito.</span><span class="sxs-lookup"><span data-stu-id="d52ba-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="d52ba-155">Notifiche</span><span class="sxs-lookup"><span data-stu-id="d52ba-155">Notifications</span></span>
<span data-ttu-id="d52ba-156">Sono disponibili due tipi di notifiche, ovvero le notifiche di sistema e le notifiche in-app, che usano file di layout diversi.</span><span class="sxs-lookup"><span data-stu-id="d52ba-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="d52ba-157">Notifiche di sistema</span><span class="sxs-lookup"><span data-stu-id="d52ba-157">System notifications</span></span>
<span data-ttu-id="d52ba-158">le notifiche di sistema toocustomize occorre hello toouse **categorie**.</span><span class="sxs-lookup"><span data-stu-id="d52ba-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="d52ba-159">È possibile passare troppo[categorie](#categories).</span><span class="sxs-lookup"><span data-stu-id="d52ba-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="d52ba-160">Notifiche in-app</span><span class="sxs-lookup"><span data-stu-id="d52ba-160">In-app notifications</span></span>
<span data-ttu-id="d52ba-161">Per impostazione predefinita, una notifica in-app è una vista che toohello aggiunti in modo dinamico corrente attività utente grazie toohello Android metodo di interfaccia `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="d52ba-162">Si tratta di una sovrimpressione di notifica.</span><span class="sxs-lookup"><span data-stu-id="d52ba-162">This is called a notification overlay.</span></span> <span data-ttu-id="d52ba-163">Sovrapposizioni di notifica sono ideali per un'integrazione veloce perché non richiedono che si toomodify qualsiasi layout nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="d52ba-164">toomodify aspetto hello le sovrapposizioni di notifica, è sufficiente modificare il file hello `engagement_notification_area.xml` tooyour necessario.</span><span class="sxs-lookup"><span data-stu-id="d52ba-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="d52ba-165">file Hello `engagement_notification_overlay.xml` è hello che viene utilizzato toocreate una sovrapposizione di notifica, include file hello `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="d52ba-166">È inoltre possibile personalizzare il toosuit le proprie esigenze (quali per l'area di notifica hello all'interno di sovrapposizione hello di posizionamento).</span><span class="sxs-lookup"><span data-stu-id="d52ba-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="d52ba-167">Includere il layout per le notifiche come parte del layout di un'attività</span><span class="sxs-lookup"><span data-stu-id="d52ba-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="d52ba-168">Le sovrimpressioni sono ideali per un'integrazione rapida, ma possono risultare fastidiose o possono avere effetti collaterali in alcuni casi speciali.</span><span class="sxs-lookup"><span data-stu-id="d52ba-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="d52ba-169">sistema di sovrapposizione Hello può essere personalizzata a livello di attività, rendendo gli effetti collaterali tooprevent semplice per le attività speciale.</span><span class="sxs-lookup"><span data-stu-id="d52ba-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="d52ba-170">È possibile decidere il layout di notifica tooinclude nel toohello di grazie layout Android esistente **includono** istruzione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="d52ba-171">Hello seguito è riportato un esempio di un oggetto modificato `ListActivity` layout che contengono solo un `ListView`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="d52ba-172">**Prima dell'integrazione con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d52ba-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="d52ba-173">**Dopo l'integrazione con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d52ba-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="d52ba-174">In questo esempio è stato aggiunto un contenitore padre, perché il layout originale di hello utilizzata una visualizzazione elenco come elemento di primo livello hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="d52ba-175">Abbiamo anche aggiunto `android:layout_weight="1"` tooadd in grado di toobe una vista di sotto di una visualizzazione elenco è configurato con `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="d52ba-176">Hello Engagement Reach SDK rileva automaticamente che notifica il layout hello è incluso in questa attività e non verrà aggiunto un overlay per questa attività.</span><span class="sxs-lookup"><span data-stu-id="d52ba-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="d52ba-177">Se si utilizza un ListActivity nell'applicazione, una sovrapposizione di copertura visibile sarà possibile reazione tooclicked gli elementi in visualizzazione elenco hello più.</span><span class="sxs-lookup"><span data-stu-id="d52ba-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="d52ba-178">Questo è un problema noto.</span><span class="sxs-lookup"><span data-stu-id="d52ba-178">This is a known issue.</span></span> <span data-ttu-id="d52ba-179">toowork questo problema si consiglia di layout di notifica tooembed hello nel proprio elenco attività layout come nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="d52ba-180">Disabilitazione delle notifiche dell'applicazione per le singole attività</span><span class="sxs-lookup"><span data-stu-id="d52ba-180">Disabling application notification per activity</span></span>
<span data-ttu-id="d52ba-181">Se non si desidera hello sovrapposizione toobe aggiunti tooyour attività e se non si include il layout di notifica hello in un layout personalizzato, è possibile disabilitare sovrapposizione hello per questa attività di hello `AndroidManifest.xml` aggiungendo un `meta-data` sezione come nell'esempio hello esempio:</span><span class="sxs-lookup"><span data-stu-id="d52ba-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="d52ba-182"><a name="categories"></a> Categorie</span><span class="sxs-lookup"><span data-stu-id="d52ba-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="d52ba-183">Quando si modifica hello fornito layout, modificare aspetto hello di tutte le notifiche.</span><span class="sxs-lookup"><span data-stu-id="d52ba-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="d52ba-184">Le categorie consentono toodefine che vari destinazione Cerca (possibilmente comportamenti) per le notifiche.</span><span class="sxs-lookup"><span data-stu-id="d52ba-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="d52ba-185">Quando si crea una campagna Reach, è possibile specificare una categoria.</span><span class="sxs-lookup"><span data-stu-id="d52ba-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="d52ba-186">Tenere presente che le categorie consentono di personalizzare annunci e sondaggi, come descritto successivamente nel documento.</span><span class="sxs-lookup"><span data-stu-id="d52ba-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="d52ba-187">tooregister un gestore di categoria per le notifiche, è necessario tooadd una chiamata quando viene inizializzata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d52ba-188">Leggere l'avviso hello sull'attributo android: processo hello \<android-sdk-engagement-process\> in hello come tooIntegrate Engagement su Android argomento prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="d52ba-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="d52ba-189">Hello seguente si presuppone è riconosciuto avviso precedente hello e usare una sottoclasse di `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="d52ba-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="d52ba-190">Hello `MyNotifier` oggetto è l'implementazione di hello del gestore di categoria di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="d52ba-191">È l'implementazione di hello `EngagementNotifier` interfaccia o una sottoclasse dell'implementazione predefinita di hello: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="d52ba-192">Si noti che hello notifica stesso grado di gestire diverse categorie, è possibile registrarli simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d52ba-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="d52ba-193">implementazione di categoria tooreplace hello predefinita, è possibile registrare l'implementazione come nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="d52ba-194">categoria di Hello corrente utilizzata in un gestore viene passata come un parametro nella maggior parte dei metodi in cui è possibile eseguire l'override `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="d52ba-195">Viene passata come parametro `String` o indirettamente in un oggetto `EngagementReachContent` che ha un metodo `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="d52ba-196">È possibile modificare la maggior parte del processo di creazione notifica hello mediante la ridefinizione di metodi su `EngagementDefaultNotifier`per personalizzazione più avanzata è disponibile tootake un aspetto della documentazione tecnica di hello e codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="d52ba-197">Notifiche in-app</span><span class="sxs-lookup"><span data-stu-id="d52ba-197">In-app notifications</span></span>
<span data-ttu-id="d52ba-198">Se si desidera layout alternativi toouse per una categoria specifica, è possibile implementare come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d52ba-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="d52ba-199">**Esempio di `my_notification_overlay.xml`:**</span><span class="sxs-lookup"><span data-stu-id="d52ba-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="d52ba-200">Come si può notare, l'identificatore della vista sovrapposizione hello è diverso da standard hello uno.</span><span class="sxs-lookup"><span data-stu-id="d52ba-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="d52ba-201">È importante che ogni layout usi un identificatore univoco per le sovrimpressioni.</span><span class="sxs-lookup"><span data-stu-id="d52ba-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="d52ba-202">**Esempio di `my_notification_area.xml`:**</span><span class="sxs-lookup"><span data-stu-id="d52ba-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="d52ba-203">Come si può notare, identificatore visualizzazione area di notifica hello è diverso da quello standard hello uno.</span><span class="sxs-lookup"><span data-stu-id="d52ba-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="d52ba-204">È importante che ogni layout usi un identificatore univoco per le aree di notifica.</span><span class="sxs-lookup"><span data-stu-id="d52ba-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="d52ba-205">Questo semplice esempio di categoria rende le notifiche di applicazione (o in-app) visualizzate in alto hello hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="d52ba-206">Non è stato hello standard identificatori nell'area di notifica hello stesso.</span><span class="sxs-lookup"><span data-stu-id="d52ba-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="d52ba-207">Se si desidera, la presenza di hello tooredefine toochange `EngagementDefaultNotifier.prepareInAppArea` metodo.</span><span class="sxs-lookup"><span data-stu-id="d52ba-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="d52ba-208">È consigliabile toolook della documentazione tecnica di hello e codice sorgente hello di `EngagementNotifier` e `EngagementDefaultNotifier` se si desidera questo livello di personalizzazione avanzata.</span><span class="sxs-lookup"><span data-stu-id="d52ba-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="d52ba-209">Notifiche di sistema</span><span class="sxs-lookup"><span data-stu-id="d52ba-209">System notifications</span></span>
<span data-ttu-id="d52ba-210">Estendendo `EngagementDefaultNotifier`, è possibile eseguire l'override `onNotificationPrepared` notifica hello tooalter preparato dall'implementazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="d52ba-211">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d52ba-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="d52ba-212">In questo esempio crea una notifica di sistema per un contenuto verrà visualizzato come un evento in corso quando hello "in corso" categoria viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="d52ba-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="d52ba-213">Se si desidera hello toobuild `Notification` dell'oggetto da zero, è possibile restituire `false` toohello metodo e chiamare `notify` in hello `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="d52ba-214">In questo caso è importante mantenere un `contentIntent`, `deleteIntent` e hello identificatore di notifica utilizzato da `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="d52ba-215">L'esempio seguente illustra un'implementazione corretta di questo tipo:</span><span class="sxs-lookup"><span data-stu-id="d52ba-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="d52ba-216">Annunci di sola notifica</span><span class="sxs-lookup"><span data-stu-id="d52ba-216">Notification only announcements</span></span>
<span data-ttu-id="d52ba-217">Hello gestione di hello fare clic su una solo annuncio può essere personalizzato eseguendo l'override di notifica `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello preparato `Intent`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="d52ba-218">Questo metodo consente il flag di hello tootune facilmente.</span><span class="sxs-lookup"><span data-stu-id="d52ba-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="d52ba-219">Ad esempio tooadd hello `SINGLE_TOP` flag:</span><span class="sxs-lookup"><span data-stu-id="d52ba-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="d52ba-220">Per gli utenti di Engagement legacy, tenere presente che le notifiche di sistema senza azione URL ora viene avviata un'applicazione hello se è stato in background, pertanto è possibile chiamare questo metodo con un annuncio senza URL di azione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="d52ba-221">È necessario considerare che quando si personalizza l'intento di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="d52ba-222">È anche possibile implementare `EngagementNotifier.executeNotifAnnouncementAction` da zero.</span><span class="sxs-lookup"><span data-stu-id="d52ba-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="d52ba-223">Ciclo di vita delle notifiche</span><span class="sxs-lookup"><span data-stu-id="d52ba-223">Notification life cycle</span></span>
<span data-ttu-id="d52ba-224">Quando si utilizza categoria predefinita hello, alcuni metodi del ciclo di vita vengono chiamati in hello `EngagementReachInteractiveContent` tooreport stato campagna hello statistiche e l'aggiornamento dell'oggetto:</span><span class="sxs-lookup"><span data-stu-id="d52ba-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="d52ba-225">Quando la notifica hello viene visualizzata nell'applicazione o inserire nella barra di stato hello, hello `displayNotification` metodo viene chiamato (che indica le statistiche) da `EngagementReachAgent` se `handleNotification` restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="d52ba-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="d52ba-226">Se la notifica hello viene ignorata, hello `exitNotification` metodo viene chiamato, viene segnalata statistica e campagne successiva ora possono essere elaborate.</span><span class="sxs-lookup"><span data-stu-id="d52ba-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="d52ba-227">Se si fa clic notifica hello, `actionNotification` viene chiamato, viene segnalata statistica e viene avviato con finalità di hello associata.</span><span class="sxs-lookup"><span data-stu-id="d52ba-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="d52ba-228">Se l'implementazione di `EngagementNotifier` bypass hello comportamento predefinito, è necessario toocall questi metodi del ciclo di vita da soli.</span><span class="sxs-lookup"><span data-stu-id="d52ba-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="d52ba-229">Hello seguono esempi vengono illustrati alcuni casi in cui viene ignorato il comportamento predefinito di hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="d52ba-230">Il metodo `EngagementDefaultNotifier` non è stato esteso, ad esempio la gestione delle categorie è stata implementata da zero.</span><span class="sxs-lookup"><span data-stu-id="d52ba-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="d52ba-231">Per le notifiche di sistema, si overrode hello `onNotificationPrepared` e sono stati modificati `contentIntent` o `deleteIntent` in hello `Notification` oggetto.</span><span class="sxs-lookup"><span data-stu-id="d52ba-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="d52ba-232">Per le notifiche nell'applicazione, overrode `prepareInAppArea`, toomap che almeno `actionNotification` tooone dei controlli U.I.</span><span class="sxs-lookup"><span data-stu-id="d52ba-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="d52ba-233">Se `handleNotification` genera un'eccezione, hello contenuto viene eliminato e `dropContent` viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="d52ba-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="d52ba-234">Ciò viene segnalato nelle statistiche e sarà possibile elaborare le campagne successive.</span><span class="sxs-lookup"><span data-stu-id="d52ba-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="d52ba-235">Annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="d52ba-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="d52ba-236">Layout</span><span class="sxs-lookup"><span data-stu-id="d52ba-236">Layouts</span></span>
<span data-ttu-id="d52ba-237">È possibile modificare hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` file toocustomize annunci di testo, sondaggi e gli annunci di web.</span><span class="sxs-lookup"><span data-stu-id="d52ba-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="d52ba-238">Questi file condividono due layout comuni per l'area del titolo hello e l'area del pulsante hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="d52ba-239">layout di Hello per titolo hello è `engagement_content_title.xml` e utilizza hello eponymous drawable file per lo sfondo di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="d52ba-240">Hello layout per i pulsanti di azione e uscita hello è `engagement_button_bar.xml` e utilizza hello eponymous drawable file per lo sfondo di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="d52ba-241">In un sondaggio, hello layout domanda e le scelte sono ingrandite in modo dinamico utilizzando più volte hello `engagement_question.xml` file layout per domande hello e hello `engagement_choice.xml` file per le scelte di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="d52ba-242">Categorie</span><span class="sxs-lookup"><span data-stu-id="d52ba-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="d52ba-243">Layout alternativi</span><span class="sxs-lookup"><span data-stu-id="d52ba-243">Alternate layouts</span></span>
<span data-ttu-id="d52ba-244">Come le notifiche, la categoria della campagna hello può essere utilizzato toohave layout alternativi per gli annunci e viene eseguito il polling.</span><span class="sxs-lookup"><span data-stu-id="d52ba-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="d52ba-245">Ad esempio, toocreate una categoria per un annuncio di testo, è possibile estendere `EngagementTextAnnouncementActivity` e farvi riferimento hello `AndroidManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="d52ba-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="d52ba-246">Si noti che categoria hello finalità hello filtro viene utilizzato differenza hello toomake con attività di annuncio hello predefinita.</span><span class="sxs-lookup"><span data-stu-id="d52ba-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="d52ba-247">Hello Reach SDK Usa hello preventivo tooresolve hello destra l'attività del sistema per una categoria specifica e viene utilizzata la cartella nella categoria predefinita hello se hello risoluzione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="d52ba-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="d52ba-248">È necessario tooimplement `MyCustomTextAnnouncementActivity`, solo il layout di hello toochange (senza mantenere hello stessi identificatori di visualizzazione), è sufficiente classe hello toodefine come nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="d52ba-249">categoria di tooreplace hello predefinita di annunci di testo, sostituire semplicemente `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="d52ba-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="d52ba-250">Gli annunci Web e i sondaggi possono essere personalizzati in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="d52ba-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="d52ba-251">Per gli annunci web è possibile estendere `EngagementWebAnnouncementActivity` e dichiarare l'attività di hello `AndroidManifest.xml` come nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="d52ba-252">Per i sondaggi è possibile estendere `EngagementPollActivity` e dichiarare il hello in `AndroidManifest.xml` come nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="d52ba-253">Implementazione da zero</span><span class="sxs-lookup"><span data-stu-id="d52ba-253">Implementation from scratch</span></span>
<span data-ttu-id="d52ba-254">È possibile implementare le categorie per le attività di annuncio (e polling) senza l'estensione di uno di hello `Engagement*Activity` le classi fornite da hello Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="d52ba-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="d52ba-255">Ciò è utile, ad esempio se si desidera toodefine un layout che non utilizza hello stesso viste come layout standard hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="d52ba-256">Ad esempio per la personalizzazione avanzata notifica, è consigliabile toolook al codice sorgente hello dell'implementazione standard di hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="d52ba-257">Ecco alcuni aspetti tookeep presente: Reach verrà avviata l'attività hello un preventivo specifico (corrispondente toohello preventivo filtro) più un parametro aggiuntivo che è l'identificatore di contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="d52ba-258">tooretrieve hello oggetto contenuto che contengono campi hello specificati quando la creazione di hello campagna sul sito web hello è possibile farlo:</span><span class="sxs-lookup"><span data-stu-id="d52ba-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="d52ba-259">Per le statistiche, sarà necessario segnalare hello contenuto viene visualizzato in hello `onResume` evento:</span><span class="sxs-lookup"><span data-stu-id="d52ba-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="d52ba-260">Quindi, non dimenticare toocall sia `actionContent(this)` o `exitContent(this)` sull'oggetto di contenuto hello prima attività hello in background.</span><span class="sxs-lookup"><span data-stu-id="d52ba-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="d52ba-261">Se non si chiama uno `actionContent` o `exitContent`, le statistiche non verranno inviate (vale a dire non analitica nella campagna hello) e più importante, hello campagne successive non verranno notificate fino a quando non viene riavviato il processo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="d52ba-262">Orientamento o altre modifiche alla configurazione possono hello codice difficile toodetermine se l'attività hello viene posto in background o non di hello rende implementazione standard contenuto hello che viene segnalato come è stato chiuso se l'utente di hello lascia attività hello (tramite premendo `HOME` o `BACK`) ma non se cambia l'orientamento hello.</span><span class="sxs-lookup"><span data-stu-id="d52ba-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="d52ba-263">Di seguito è interessante hello dell'implementazione di hello:</span><span class="sxs-lookup"><span data-stu-id="d52ba-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="d52ba-264">Come si può notare, se è stato chiamato `actionContent(this)` quindi terminata attività hello, `exitContent(this)` può essere chiamato in modo sicuro senza causare alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="d52ba-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
