---
title: Integrazione di Android SDK per Azure Mobile Engagement
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
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="eaf38-103">Come integrare il servizio di copertura di Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="eaf38-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eaf38-104">Prima di usare questa guida, è necessario eseguire la procedura di integrazione descritta nel documento relativo all'integrazione di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="eaf38-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="eaf38-105">Integrazione standard</span><span class="sxs-lookup"><span data-stu-id="eaf38-105">Standard integration</span></span>

<span data-ttu-id="eaf38-106">Copiare i file di risorse del servizio di copertura dall'SDK al progetto:</span><span class="sxs-lookup"><span data-stu-id="eaf38-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="eaf38-107">Copiare i file dalla cartella `res/layout` disponibile nell'SDK alla cartella `res/layout` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="eaf38-108">Copiare i file dalla cartella `res/drawable` disponibile nell'SDK alla cartella `res/drawable` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="eaf38-109">Modificare il file `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="eaf38-110">Aggiungere la sezione seguente tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="eaf38-111">Questa autorizzazione è necessaria per rispondere alle notifiche di sistema non selezionate all'avvio. In caso contrario, verranno mantenute su disco ma non verranno più visualizzate. È quindi necessario includere questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="eaf38-112">Specificare un'icona usata per le notifiche (in-app e di sistema) copiando e modificando la sezione seguente tra i tag `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="eaf38-113">Questa sezione è **obbligatoria** se si prevede di usare le notifiche di sistema durante la creazione di campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="eaf38-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="eaf38-114">Android impedisce la visualizzazione di notifiche di sistema senza icone.</span><span class="sxs-lookup"><span data-stu-id="eaf38-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="eaf38-115">Se si omette questa sezione, gli utenti finali non saranno quindi in grado di riceverle.</span><span class="sxs-lookup"><span data-stu-id="eaf38-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="eaf38-116">Se si crea una campagna con notifiche di sistema usando un'immagine di grandi dimensioni, è necessario aggiungere le autorizzazioni seguenti, se mancanti, dopo il tag `</application>` :</span><span class="sxs-lookup"><span data-stu-id="eaf38-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="eaf38-117">Per Android M e se l'applicazione è destinata al livello dell’API Android 23 o superiore, l’autorizzazione ``WRITE_EXTERNAL_STORAGE`` richiede l'approvazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="eaf38-118">Leggere [questa sezione](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="eaf38-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="eaf38-119">Nella campagna di copertura è anche possibile specificare se il dispositivo deve emettere un segnale e/o una vibrazione in caso di notifiche di sistema.</span><span class="sxs-lookup"><span data-stu-id="eaf38-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="eaf38-120">A questo scopo, è necessario assicurarsi di avere dichiarato l'autorizzazione seguente dopo il tag `</application>` :</span><span class="sxs-lookup"><span data-stu-id="eaf38-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="eaf38-121">Senza questa autorizzazione, Android impedisce la visualizzazione delle notifiche di sistema se è stata selezionata l'opzione relativa al segnale o alla vibrazione nel responsabile della campagna di copertura.</span><span class="sxs-lookup"><span data-stu-id="eaf38-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="eaf38-122">Push nativo</span><span class="sxs-lookup"><span data-stu-id="eaf38-122">Native Push</span></span>
<span data-ttu-id="eaf38-123">Dopo la configurazione del modulo di copertura, sarà necessario configurare il push nativo in modo da permettere la ricezione delle campagne sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="eaf38-124">Sono supportati due servizi su Android:</span><span class="sxs-lookup"><span data-stu-id="eaf38-124">We support two services on Android:</span></span>

* <span data-ttu-id="eaf38-125">Dispositivi Google Play: usare [Google Cloud Messaging] seguendo le istruzioni dell'articolo [Come integrare GCM con Engagement](mobile-engagement-android-gcm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="eaf38-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="eaf38-126">Dispositivi Amazon: usare [Amazon Device Messaging] seguendo le istruzioni dell'articolo [Come integrare ADM con Engagement](mobile-engagement-android-adm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="eaf38-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="eaf38-127">Per fare riferimento sia ai dispositivi Amazon che ai dispositivi Google Play, è possibile includere tutti gli elementi in un file AndroidManifest.xml/APK per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="eaf38-128">È tuttavia possibile che l'applicazione venga rifiutata da Amazon, se viene rilevato il codice GCM.</span><span class="sxs-lookup"><span data-stu-id="eaf38-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="eaf38-129">In tale caso, usare più file APK.</span><span class="sxs-lookup"><span data-stu-id="eaf38-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="eaf38-130">**L'applicazione è ora pronta per ricevere e visualizzare campagne Reach.**</span><span class="sxs-lookup"><span data-stu-id="eaf38-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="eaf38-131">Come gestire il push di dati</span><span class="sxs-lookup"><span data-stu-id="eaf38-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="eaf38-132">Integrazione</span><span class="sxs-lookup"><span data-stu-id="eaf38-132">Integration</span></span>
<span data-ttu-id="eaf38-133">Se si vuole che l'applicazione sia in grado di ricevere push di dati del servizio Reach, è necessario creare una classe secondaria di `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e includere un riferimento a tale classe nel file `AndroidManifest.xml`, tra i tag `<application>` e/o `</application>`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="eaf38-134">Sarà quindi possibile eseguire l'override dei callback `onDataPushStringReceived` e `onDataPushBase64Received`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="eaf38-135">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf38-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="eaf38-136">Categoria</span><span class="sxs-lookup"><span data-stu-id="eaf38-136">Category</span></span>
<span data-ttu-id="eaf38-137">Il parametro category è facoltativo quando si crea una campagna per il push dei dati e consente di filtrare i push dei dati.</span><span class="sxs-lookup"><span data-stu-id="eaf38-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="eaf38-138">Questo parametro è utile se sono presenti diversi ricevitori di trasmissioni che gestiscono tipi diversi di push di dati o quando si vuole eseguire il push di vari tipi di dati `Base64` al fine di identificare il tipo prima dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="eaf38-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="eaf38-139">Parametro restituito dai callback</span><span class="sxs-lookup"><span data-stu-id="eaf38-139">Callbacks' return parameter</span></span>
<span data-ttu-id="eaf38-140">Le linee guida seguenti permettono di gestire correttamente il parametro restituito da `onDataPushStringReceived` e `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="eaf38-141">Se non sa come gestire un push di dati, un ricevitore di trasmissioni deve restituire `null` nel callback.</span><span class="sxs-lookup"><span data-stu-id="eaf38-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="eaf38-142">È consigliabile usare la categoria per determinare se il ricevitore di trasmissioni deve o non deve gestire il push di dati.</span><span class="sxs-lookup"><span data-stu-id="eaf38-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="eaf38-143">Se accetta il push di dati, uno dei ricevitori di trasmissioni deve restituire `true` nel callback.</span><span class="sxs-lookup"><span data-stu-id="eaf38-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="eaf38-144">Se riconosce il push di dati ma lo rimuove per qualsiasi motivo, uno dei ricevitori di trasmissioni deve restituire `false` nel callback.</span><span class="sxs-lookup"><span data-stu-id="eaf38-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="eaf38-145">Se i dati ricevuti non sono validi, ad esempio, verrà restituito `false` .</span><span class="sxs-lookup"><span data-stu-id="eaf38-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="eaf38-146">Se un ricevitore di trasmissioni restituisce `true` mentre un altro restituisce `false` per lo stesso push di dati, il comportamento non è definito. È necessario evitare questa situazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="eaf38-147">Il tipo restituito viene usato solo per le statistiche del servizio di copertura:</span><span class="sxs-lookup"><span data-stu-id="eaf38-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="eaf38-148">`Replied` viene incrementato di uno se i ricevitori di trasmissioni hanno restituito `true` o `false`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="eaf38-149">`Actioned` viene incrementato solo se uno dei ricevitori di trasmissioni ha restituito `true`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="eaf38-150">Come personalizzare le campagne</span><span class="sxs-lookup"><span data-stu-id="eaf38-150">How to customize campaigns</span></span>
<span data-ttu-id="eaf38-151">Per personalizzare le campagne, è possibile modificare i layout disponibili in Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="eaf38-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="eaf38-152">È consigliabile mantenere tutti gli identificatori usati nei layout e i tipi di visualizzazioni che usano un identificatore, in particolare per le visualizzazioni di testo e le visualizzazioni di immagini.</span><span class="sxs-lookup"><span data-stu-id="eaf38-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="eaf38-153">Alcune visualizzazioni vengono semplicemente usate per nascondere o mostrare alcune aree, in modo da consentirne la modifica del tipo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="eaf38-154">Se si vuole modificare il tipo di una visualizzazione nei layout forniti, verificare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="eaf38-155">Notifiche</span><span class="sxs-lookup"><span data-stu-id="eaf38-155">Notifications</span></span>
<span data-ttu-id="eaf38-156">Sono disponibili due tipi di notifiche, ovvero le notifiche di sistema e le notifiche in-app, che usano file di layout diversi.</span><span class="sxs-lookup"><span data-stu-id="eaf38-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="eaf38-157">Notifiche di sistema</span><span class="sxs-lookup"><span data-stu-id="eaf38-157">System notifications</span></span>
<span data-ttu-id="eaf38-158">Per personalizzare le notifiche di sistema, è necessario usare le **categorie**.</span><span class="sxs-lookup"><span data-stu-id="eaf38-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="eaf38-159">Passare alla sezione [Categorie](#categories).</span><span class="sxs-lookup"><span data-stu-id="eaf38-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="eaf38-160">Notifiche in-app</span><span class="sxs-lookup"><span data-stu-id="eaf38-160">In-app notifications</span></span>
<span data-ttu-id="eaf38-161">Per impostazione predefinita, una notifica in-app è una visualizzazione che viene aggiunta dinamicamente all'interfaccia utente dell'attività corrente con il metodo `addContentView()`di Android.</span><span class="sxs-lookup"><span data-stu-id="eaf38-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="eaf38-162">Si tratta di una sovrimpressione di notifica.</span><span class="sxs-lookup"><span data-stu-id="eaf38-162">This is called a notification overlay.</span></span> <span data-ttu-id="eaf38-163">Le sovrimpressioni delle notifiche sono ideali per un'integrazione rapida poiché non richiedono alcuna modifica di layout nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="eaf38-164">Per modificare l'aspetto delle sovrimpressioni delle notifiche, è sufficiente modificare il file `engagement_notification_area.xml` in base alle esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="eaf38-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf38-165">Il file `engagement_notification_overlay.xml` è quello usato per creare una sovrimpressione di notifica e include il file `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="eaf38-166">È anche possibile personalizzarlo in base alle esigenze, ad esempio per posizionare l'area di notifica all'interno della sovrimpressione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="eaf38-167">Includere il layout per le notifiche come parte del layout di un'attività</span><span class="sxs-lookup"><span data-stu-id="eaf38-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="eaf38-168">Le sovrimpressioni sono ideali per un'integrazione rapida, ma possono risultare fastidiose o possono avere effetti collaterali in alcuni casi speciali.</span><span class="sxs-lookup"><span data-stu-id="eaf38-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="eaf38-169">Il sistema di sovrimpressione può essere personalizzato a livello di attività, permettendo di evitare con facilità effetti collaterali per attività speciali.</span><span class="sxs-lookup"><span data-stu-id="eaf38-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="eaf38-170">È possibile decidere di includere il layout per le notifiche Microsoft nel proprio layout esistente mediante l'istruzione **include** di Android.</span><span class="sxs-lookup"><span data-stu-id="eaf38-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="eaf38-171">L'esempio seguente mostra un layout `ListActivity` modificato che contiene solo un elemento `ListView`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="eaf38-172">**Prima dell'integrazione con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="eaf38-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="eaf38-173">**Dopo l'integrazione con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="eaf38-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="eaf38-174">In questo esempio è stato aggiunto un contenitore padre, poiché il layout originale usa una visualizzazione elenco come elemento di primo livello.</span><span class="sxs-lookup"><span data-stu-id="eaf38-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="eaf38-175">È stato incluso anche un elemento `android:layout_weight="1"` per permettere l'aggiunta di una visualizzazione sotto una visualizzazione elenco configurata con `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="eaf38-176">Engagement Reach SDK rileva automaticamente che il layout per le notifiche è incluso nell'attività e non aggiunge alcuna sovrimpressione per questa attività.</span><span class="sxs-lookup"><span data-stu-id="eaf38-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="eaf38-177">Se si usa un elemento ListActivity nell'applicazione, una sovrimpressione visibile relativa al servizio di copertura impedirà di reagire agli elementi selezionati nella visualizzazione elenco.</span><span class="sxs-lookup"><span data-stu-id="eaf38-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="eaf38-178">Questo è un problema noto.</span><span class="sxs-lookup"><span data-stu-id="eaf38-178">This is a known issue.</span></span> <span data-ttu-id="eaf38-179">Per risolvere questo problema, è consigliabile incorporare il layout per le notifiche nel layout personalizzato dell'attività List, come indicato nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="eaf38-180">Disabilitazione delle notifiche dell'applicazione per le singole attività</span><span class="sxs-lookup"><span data-stu-id="eaf38-180">Disabling application notification per activity</span></span>
<span data-ttu-id="eaf38-181">Se non si vuole che la sovrimpressione venga aggiunta all'attività e se non si include il layout per le notifiche nel layout personalizzato, è possibile disabilitare la sovrimpressione per questa attività nel file `AndroidManifest.xml` aggiungendo una sezione `meta-data`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="eaf38-182"><a name="categories"></a> Categorie</span><span class="sxs-lookup"><span data-stu-id="eaf38-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="eaf38-183">Quando si modificano i layout forniti, si modifica l'aspetto di tutte le notifiche.</span><span class="sxs-lookup"><span data-stu-id="eaf38-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="eaf38-184">Le categorie consentono di definire diversi aspetti assegnati (comportamenti) delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="eaf38-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="eaf38-185">Quando si crea una campagna Reach, è possibile specificare una categoria.</span><span class="sxs-lookup"><span data-stu-id="eaf38-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="eaf38-186">Tenere presente che le categorie consentono di personalizzare annunci e sondaggi, come descritto successivamente nel documento.</span><span class="sxs-lookup"><span data-stu-id="eaf38-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="eaf38-187">Per registrare un gestore di categorie per le notifiche, è necessario aggiungere una chiamata durante l'inizializzazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eaf38-188">Prima di continuare, leggere le informazioni relative all'attributo android:process \<android-sdk-engagement-process\> nell'argomento Come integrare Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="eaf38-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="eaf38-189">L'esempio seguente presuppone che l'avviso precedente sia stato rispettato e che sia stata usata una classe secondaria di `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="eaf38-190">L'oggetto `MyNotifier` è l'implementazione del gestore delle categorie di notifica.</span><span class="sxs-lookup"><span data-stu-id="eaf38-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="eaf38-191">Corrisponde a un'implementazione dell'interfaccia `EngagementNotifier` o a una classe secondaria dell'implementazione predefinita: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="eaf38-192">Si noti che lo stesso componente di notifica può gestire diverse categorie e che è possibile registrarle come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="eaf38-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="eaf38-193">Per sostituire l'implementazione predefinita della categoria, è possibile registrare l'implementazione come indicato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

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

<span data-ttu-id="eaf38-194">La categoria corrente usata in un gestore viene passata come parametro nella maggior parte dei metodi di cui è possibile eseguire l'override in `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="eaf38-195">Viene passata come parametro `String` o indirettamente in un oggetto `EngagementReachContent` che ha un metodo `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="eaf38-196">È possibile cambiare gran parte del processo di creazione delle notifiche ridefinendo i metodi in `EngagementDefaultNotifier`. Per una personalizzazione più avanzata, vedere la documentazione tecnica e il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="eaf38-197">Notifiche in-app</span><span class="sxs-lookup"><span data-stu-id="eaf38-197">In-app notifications</span></span>
<span data-ttu-id="eaf38-198">Per usare semplicemente layout alternativi per una categoria specifica, è possibile implementare quanto indicato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

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

<span data-ttu-id="eaf38-199">**Esempio di `my_notification_overlay.xml`:**</span><span class="sxs-lookup"><span data-stu-id="eaf38-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="eaf38-200">Come si può notare, l'identificatore visualizzazione di sovrimpressione è diverso da quello standard.</span><span class="sxs-lookup"><span data-stu-id="eaf38-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="eaf38-201">È importante che ogni layout usi un identificatore univoco per le sovrimpressioni.</span><span class="sxs-lookup"><span data-stu-id="eaf38-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="eaf38-202">**Esempio di `my_notification_area.xml`:**</span><span class="sxs-lookup"><span data-stu-id="eaf38-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="eaf38-203">Come si può notare, l'identificatore visualizzazione di area di notifica è diverso da quello standard.</span><span class="sxs-lookup"><span data-stu-id="eaf38-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="eaf38-204">È importante che ogni layout usi un identificatore univoco per le aree di notifica.</span><span class="sxs-lookup"><span data-stu-id="eaf38-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="eaf38-205">Questo semplice esempio di categoria permette di visualizzare le notifiche relative alle applicazioni (anche di tipo in-app) nella parte superiore dello schermo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="eaf38-206">Non sono state apportate modifiche agli identificatori standard usati nell'area di notifica stessa.</span><span class="sxs-lookup"><span data-stu-id="eaf38-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="eaf38-207">Per apportare modifiche, è necessario ridefinire il metodo `EngagementDefaultNotifier.prepareInAppArea` .</span><span class="sxs-lookup"><span data-stu-id="eaf38-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="eaf38-208">Se si vuole applicare questo livello di personalizzazione avanzata, è consigliabile esaminare la documentazione tecnica e il codice sorgente di `EngagementNotifier` e `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="eaf38-209">Notifiche di sistema</span><span class="sxs-lookup"><span data-stu-id="eaf38-209">System notifications</span></span>
<span data-ttu-id="eaf38-210">L'estensione di `EngagementDefaultNotifier` permette di eseguire l'override di `onNotificationPrepared` per modificare la notifica preparata dall'implementazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eaf38-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="eaf38-211">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf38-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="eaf38-212">Questo esempio permette di visualizzare una notifica di sistema per un contenuto come evento in corso quando viene usata la categoria "ongoing".</span><span class="sxs-lookup"><span data-stu-id="eaf38-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="eaf38-213">Se si vuole creare l'oggetto `Notification` da zero, è possibile restituire `false` al metodo e chiamare `notify` su `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="eaf38-214">In questo caso è importante mantenere gli elementi `contentIntent` e `deleteIntent`, oltre all'identificatore di notifica usato da `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="eaf38-215">L'esempio seguente illustra un'implementazione corretta di questo tipo:</span><span class="sxs-lookup"><span data-stu-id="eaf38-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="eaf38-216">Annunci di sola notifica</span><span class="sxs-lookup"><span data-stu-id="eaf38-216">Notification only announcements</span></span>
<span data-ttu-id="eaf38-217">È possibile personalizzare la gestione della selezione di un annuncio di sola notifica eseguendo l'override di `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` per modificare il valore `Intent` preparato.</span><span class="sxs-lookup"><span data-stu-id="eaf38-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="eaf38-218">L'uso di questo metodo permette di ottimizzare con facilità i flag.</span><span class="sxs-lookup"><span data-stu-id="eaf38-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="eaf38-219">Ad esempio, per aggiungere il flag `SINGLE_TOP`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="eaf38-220">Per utenti del servizio Engagement legacy, si noti che le notifiche di sistema senza URL di azione ora avviano l'applicazione se era in esecuzione in background. È quindi possibile chiamare questo metodo con un annuncio senza URL di azione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="eaf38-221">Occorre tenere presente questo aspetto quando si personalizza l'elemento Intent.</span><span class="sxs-lookup"><span data-stu-id="eaf38-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="eaf38-222">È anche possibile implementare `EngagementNotifier.executeNotifAnnouncementAction` da zero.</span><span class="sxs-lookup"><span data-stu-id="eaf38-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="eaf38-223">Ciclo di vita delle notifiche</span><span class="sxs-lookup"><span data-stu-id="eaf38-223">Notification life cycle</span></span>
<span data-ttu-id="eaf38-224">Quando si usa la categoria predefinita, alcuni metodi del ciclo di vita vengono chiamati sull'oggetto `EngagementReachInteractiveContent` per segnalare le statistiche e aggiornare lo stato della campagna:</span><span class="sxs-lookup"><span data-stu-id="eaf38-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="eaf38-225">Quando la notifica viene visualizzata in un'applicazione o viene inserita nella barra di stato, il metodo `displayNotification` (per la segnalazione delle statistiche) viene chiamato da `EngagementReachAgent` se `handleNotification` restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="eaf38-226">Se la notifica viene ignorata, viene chiamato il metodo `exitNotification`, vengono segnalate le statistiche e le campagne successive possono essere elaborate.</span><span class="sxs-lookup"><span data-stu-id="eaf38-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="eaf38-227">Se la notifica viene selezionata, viene chiamato `actionNotification` , vengono segnalate le statistiche e viene avviato l'elemento Intent associato.</span><span class="sxs-lookup"><span data-stu-id="eaf38-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="eaf38-228">Se l'implementazione di `EngagementNotifier` ignora il comportamento predefinito, è necessario chiamare i metodi del ciclo di vita autonomamente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="eaf38-229">Negli esempi seguenti vengono descritte alcune situazioni nelle quali viene ignorato il comportamento predefinito:</span><span class="sxs-lookup"><span data-stu-id="eaf38-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="eaf38-230">Il metodo `EngagementDefaultNotifier` non è stato esteso, ad esempio la gestione delle categorie è stata implementata da zero.</span><span class="sxs-lookup"><span data-stu-id="eaf38-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="eaf38-231">Per le notifiche di sistema, è stato eseguito l'override di `onNotificationPrepared` e sono state apportate modifiche a `contentIntent` o `deleteIntent` nell'oggetto `Notification`.</span><span class="sxs-lookup"><span data-stu-id="eaf38-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="eaf38-232">Per le notifiche in-app, è stato eseguito l'override di `prepareInAppArea`. Assicurarsi di mappare almeno `actionNotification` a uno dei controlli dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="eaf38-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf38-233">Se `handleNotification` genera un'eccezione, il contenuto viene eliminato e `dropContent` viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="eaf38-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="eaf38-234">Ciò viene segnalato nelle statistiche e sarà possibile elaborare le campagne successive.</span><span class="sxs-lookup"><span data-stu-id="eaf38-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="eaf38-235">Annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="eaf38-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="eaf38-236">Layout</span><span class="sxs-lookup"><span data-stu-id="eaf38-236">Layouts</span></span>
<span data-ttu-id="eaf38-237">È possibile modificare i file `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` per personalizzare annunci di testo, annunci Web e sondaggi.</span><span class="sxs-lookup"><span data-stu-id="eaf38-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="eaf38-238">Questi file condividono due layout comuni per l'area del titolo e quella dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="eaf38-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="eaf38-239">Il layout per il titolo è `engagement_content_title.xml` e usa il file tracciabile eponimo per lo sfondo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="eaf38-240">Il layout per i pulsanti di azione e di uscita è `engagement_button_bar.xml` e usa il file tracciabile eponimo per lo sfondo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="eaf38-241">In un sondaggio, il layout per le domande e le rispettive opzioni viene ampliato in modo dinamico usando più volte il file di layout `engagement_question.xml` per le domande e il file `engagement_choice.xml` per le opzioni.</span><span class="sxs-lookup"><span data-stu-id="eaf38-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="eaf38-242">Categorie</span><span class="sxs-lookup"><span data-stu-id="eaf38-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="eaf38-243">Layout alternativi</span><span class="sxs-lookup"><span data-stu-id="eaf38-243">Alternate layouts</span></span>
<span data-ttu-id="eaf38-244">In modo analogo alle notifiche, è possibile impostare la categoria di una campagna in modo che disponga di layout alternativi per gli annunci e i sondaggi.</span><span class="sxs-lookup"><span data-stu-id="eaf38-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="eaf38-245">Ad esempio, per creare una categoria per un annuncio di testo, è possibile estendere `EngagementTextAnnouncementActivity` e farvi riferimento nel file `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="eaf38-246">Si noti che la categoria nel filtro Intent viene usata per la differenziazione rispetto all'attività predefinita dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="eaf38-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="eaf38-247">Reach SDK usa il sistema basato su Intent per risolvere l'attività corretta per una categoria specifica ed esegue il fallback alla categoria predefinita in caso di risoluzione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="eaf38-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="eaf38-248">In tal caso è necessario implementare `MyCustomTextAnnouncementActivity`. Se si vuole solo modificare il layout, mantenendo gli stessi identificatori visualizzazione, è sufficiente definire la classe come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="eaf38-249">Per sostituire la categoria predefinita degli annunci di testo, è sufficiente sostituire `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` con l'implementazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="eaf38-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="eaf38-250">Gli annunci Web e i sondaggi possono essere personalizzati in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="eaf38-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="eaf38-251">Per gli annunci Web è possibile estendere `EngagementWebAnnouncementActivity` e dichiarare l'attività nel file `AndroidManifest.xml`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="eaf38-252">Per i sondaggi è possibile estendere `EngagementPollActivity` e dichiarare l'attività nel file `AndroidManifest.xml`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf38-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="eaf38-253">Implementazione da zero</span><span class="sxs-lookup"><span data-stu-id="eaf38-253">Implementation from scratch</span></span>
<span data-ttu-id="eaf38-254">È possibile implementare le categorie per le attività di annuncio e sondaggio senza estendere una delle classi `Engagement*Activity` fornite dall'SDK di Reach.</span><span class="sxs-lookup"><span data-stu-id="eaf38-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="eaf38-255">Ciò risulta utile ad esempio se si vuole definire un layout che non usa la stessa visualizzazione dei layout standard.</span><span class="sxs-lookup"><span data-stu-id="eaf38-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="eaf38-256">Come per la personalizzazione avanzata delle notifiche, si consiglia di esaminare il codice sorgente dell'implementazione standard.</span><span class="sxs-lookup"><span data-stu-id="eaf38-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="eaf38-257">Occorre tenere presente che il servizio di copertura avvia l'attività con uno scopo specifico, corrispondente al filtro Intent, oltre a un parametro aggiuntivo che corrisponde all'identificatore del contenuto.</span><span class="sxs-lookup"><span data-stu-id="eaf38-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="eaf38-258">Per recuperare il contenuto che include i campi specificati durante la creazione della campagna nel sito Web, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaf38-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

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

<span data-ttu-id="eaf38-259">Per le statistiche è necessario inserire nei report il contenuto visualizzato nell'evento `onResume`:</span><span class="sxs-lookup"><span data-stu-id="eaf38-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="eaf38-260">Ricordare quindi di chiamare `actionContent(this)` o `exitContent(this)` sull'oggetto Content prima del passaggio in background dell'attività.</span><span class="sxs-lookup"><span data-stu-id="eaf38-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="eaf38-261">Se non si chiama `actionContent` o `exitContent`, le statistiche non verranno inviate (ovvero non saranno disponibili statistiche sulla campagna) e soprattutto non verranno visualizzate notifiche per le campagne successive fino al riavvio del processo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf38-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="eaf38-262">Se si modifica l'orientamento o altri aspetti della configurazione, è possibile che il codice non riesca a determinare con facilità se l'attività deve passare o meno in background. L'implementazione standard assicura che il contenuto venga segnalato come chiuso se l'utente esce dall'attività (premendo `HOME` o `BACK`), ma non in caso di modifica dell'orientamento.</span><span class="sxs-lookup"><span data-stu-id="eaf38-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="eaf38-263">Questa è la parte interessante dell'implementazione:</span><span class="sxs-lookup"><span data-stu-id="eaf38-263">Here is the interesting part of the implementation:</span></span>

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
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="eaf38-264">Come si può notare, se è stato chiamato `actionContent(this)` e l'attività è stata completata, è possibile chiamare `exitContent(this)` in modo sicuro senza che ciò abbia alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="eaf38-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="eaf38-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="eaf38-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="eaf38-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="eaf38-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
