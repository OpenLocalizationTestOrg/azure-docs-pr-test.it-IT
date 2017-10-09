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
# <a name="upgrade-procedures"></a>Procedure di aggiornamento
Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK. Ad esempio se si esegue la migrazione da 1.4.0 too1.6.0 è toofirst seguire hello "da 1.4.0 too1.5.0" routine quindi hello "da 1.5.0 too1.6.0" stored procedure.

L'aggiornamento da, indipendentemente dalla versione di hello è hello tooreplace `mobile-engagement-VERSION.jar` con hello uno nuovo.

## <a name="from-420-too421"></a>Da 4.2.0 too4.2.1
Questo passaggio in realtà può essere eseguito in qualsiasi versione di hello SDK, è un miglioramento della sicurezza quando si integrano le attività di copertura.

È necessario ora aggiungere `exported="false"` tooall Reach attività.

Le attività del servizio di copertura su `AndroidManifest.xml`non devono comparire come segue:

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

## <a name="from-400-too410"></a>Da 4.0.0 too4.1.0
Hello SDK ora handle del nuovo modello di autorizzazione da Android M.

Se si utilizzano le funzionalità del percorso o le notifiche del quadro generale, leggere [questa sezione](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Inoltre toohello nuovo modello di autorizzazione, è ora supportano la configurazione delle funzionalità di percorso in fase di esecuzione.
Ci sono ancora compatibili con parametri per il percorso del manifesto hello ma è obsoleta. la configurazione di runtime toouse, Rimuovi hello nelle sezioni seguenti sono dal ``AndroidManifest.xml``:

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

e leggere [questo aggiornamento procedura](mobile-engagement-android-integrate-engagement.md#location-reporting) la configurazione di runtime toouse invece.

## <a name="from-300-too400"></a>Da 3.0.0 too4.0.0
### <a name="native-push"></a>Push nativo
Push nativo (GCM/ADM) è ora anche utilizzato per notifiche in-app è necessario configurare le credenziali push nativo hello per qualsiasi tipo di campagna push.

Se non è già stata eseguita, completare [questa procedura](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
L'integrazione con il servizio di copertura è stata modificata in ``AndroidManifest.xml``.

Sostituire:

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

Con

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

È ora possibile che venga visualizzata una schermata di caricamento quando si fa clic su un annuncio (con contenuto di tipo testo/Web) o un sondaggio.
La presenza di tooadd questo tali toowork campagne in 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Risorse
Incorporare hello nuovo `res/layout/engagement_loading.xml` file nel progetto.

## <a name="from-240-too300"></a>Da 2.4.0 too3.0.0
Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement. Se si esegue la migrazione da una versione precedente, consultare hello Capptain sito web toomigrate too2.4.0 prima e quindi applicare hello seguente procedura.

> [!IMPORTANT]
> Capptain Engagement Mobile sono non hello stessi servizi e hello procedura indicata di seguito è la modalità toomigrate hello app client. Migrazione hello SDK nell'applicazione hello non eseguirà la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement.
> 
> 

### <a name="jar-file"></a>File JAR
Sostituire `capptain.jar` con `mobile-engagement-VERSION.jar` nella cartella `libs`.

### <a name="resource-files"></a>File di risorse
Ogni file di risorse che è stata fornita (preceduto dal prefisso `capptain_`) è toobe sostituito da hello nuovi (preceduti `engagement_`).

Se tali file sono stati personalizzati, è necessario toore-applicare la personalizzazione nel file hello **tutti gli identificatori di hello nei file di risorse hello sono inoltre stati rinominati**.

### <a name="application-id"></a>ID applicazione
Ora Engagement utilizza una connessione stringa tooconfigure hello SDK identificatori, ad esempio l'identificatore dell'applicazione hello.

Si dispone di toouse `EngagementAgent.init` metodo nell'attività di avvio simile al seguente:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure.

Rimuovere qualsiasi chiamata troppo`CapptainAgent.configure` come `EngagementAgent.init` sostituisce tale metodo.

Hello `appId` non possono essere configurate tramite `AndroidManifest.xml`.

Rimuovere questa sezione da `AndroidManifest.xml`, se presente:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>API Java
Ogni tooany chiamata classe Java di Windows SDK è stato rinominato, toobe ad esempio, `CapptainAgent.getInstance(this)` deve essere rinominato `EngagementAgent.getInstance(this)`, `extends CapptainActivity` deve essere rinominata `extends EngagementActivity` e così via...

Se sono integrati con i file delle preferenze agente predefinito, il nome di file predefinito hello è ora `engagement.agent` e chiave hello è `engagement:agent`.

Quando si creano gli annunci web, Javascript binder hello è ora `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Si è verificato numerose modifiche sono servizio hello non è più condivisa e numerosi destinatari non sono più esportabile.

dichiarazione di Hello del servizio è ora più semplice. Rimuovi filtro preventivo hello e tutti i metadati all'interno e Aggiungi `exportable=false`.

Oltre a tutto ciò che viene rinominato toouse engagement.

L'aspetto è analogo al seguente:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Quando si desidera che i log dei test tooenable, hello metadati sono stato spostato toohello tag dell'applicazione e che è stato rinominato:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Tutti gli altri metadati dati appena sono stati rinominati, ecco l'elenco completo di hello (naturalmente Rinomina solo hello quelli utilizzare):

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

Rilevamento di Google Play e SmartAd è stato rimosso dal SDK è sufficiente tooremove questo senza sostituzione:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

le attività di copertura Hello vengono ora dichiarate simile al seguente:

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

Se si dispone di attività personalizzate di copertura, è necessario solo toochange hello azioni preventivo toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` o `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hello ricevitori broadcast sono stati rinominati, più è ora possibile aggiungere `exported=false`. Ecco l'elenco completo di hello di ricevitori hello con hello nuova specifica (naturalmente Rinomina solo hello quelli utilizzare):

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

Ricevitore di rilevamento è stato rimosso, in modo che sia tooremove in questa sezione:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Si noti che la dichiarazione hello dell'implementazione di hello broadcast destinatario **EngagementMessageReceiver** è stata modificata in hello `AndroidManifest.xml`. Questo avviene perché toosend hello API e rimuovere XMPP arbitrario messaggi da entità XMPP arbitraria e hello toosend API e ricevere messaggi tra i dispositivi sono stati rimossi. Di conseguenza, è anche hello toodelete callback dal seguente il **EngagementMessageReceiver** implementazione:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

e

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

quindi eliminare qualsiasi chiamata su **EngagementAgent** per:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

e

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Configurazione proguard può essere interessati da rebranding, hello regole sono ora simile:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

