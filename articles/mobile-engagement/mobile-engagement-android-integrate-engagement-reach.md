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
# <a name="how-toointegrate-engagement-reach-on-android"></a>La modalità di copertura di Engagement tooIntegrate in Android
> [!IMPORTANT]
> È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.
> 
> 

## <a name="standard-integration"></a>Integrazione standard

Copiare il file di risorse di copertura hello SDK nel progetto:

* Copiare i file hello da hello `res/layout` cartella recapitati con hello SDK in hello `res/layout` cartella dell'applicazione.
* Copiare i file hello da hello `res/drawable` cartella recapitati con hello SDK in hello `res/drawable` cartella dell'applicazione.

Modificare il file `AndroidManifest.xml`:

* Aggiungere hello successiva sezione (tra hello `<application>` e `</application>` tag):
  
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
* È necessario questa autorizzazione tooreplay le notifiche di sistema che non sono stati scelto all'avvio (in caso contrario verranno mantenuti su disco, ma non potranno essere visualizzati più, è importante tooinclude questo).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Specificare un'icona utilizzata per le notifiche (entrambi in app e quelli di sistema) copiando e la modifica seguente sezione hello (tra hello `<application>` e `</application>` tag):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Questa sezione è **obbligatoria** se si prevede di usare le notifiche di sistema durante la creazione di campagne Reach. Android impedisce la visualizzazione di notifiche di sistema senza icone. Pertanto se si omette questa sezione, gli utenti finali non saranno in grado di tooreceive li.
> 
> 

* Se si creano le campagne con le notifiche di sistema utilizzando quadro generale, è necessario hello tooadd queste autorizzazioni (dopo hello `</application>` tag) mancanti:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Per Android M e se l'applicazione è destinata al livello dell’API Android 23 o superiore, l’autorizzazione ``WRITE_EXTERNAL_STORAGE`` richiede l'approvazione dell'utente. Leggere [questa sezione](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Per le notifiche di sistema, che è inoltre possibile specificare in hello raggiungere campagna se il dispositivo hello deve dell'anello e/o vibrare. Per tale toowork, aver toomake che è stata dichiarata hello seguente autorizzazione (dopo hello `</application>` tag):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Senza questa autorizzazione, Android impedisce che vengano visualizzate notifiche di sistema se è stata selezionata l'anello hello o hello vibrare opzione responsabile della campagna raggiungere hello.

## <a name="native-push"></a>Push nativo
Ora che è stato configurato modulo Reach, è necessario campagne tooconfigure push nativo toobe tooreceive in grado di hello sul dispositivo hello.

Sono supportati due servizi su Android:

* I dispositivi Google Play: utilizzare [Google Cloud Messaging] dal seguente hello [come tooIntegrate GCM con Engagement Guida](mobile-engagement-android-gcm-integrate.md) Guida.
* Dispositivi Amazon: utilizzare [Amazon Device Messaging] dal seguente hello [come tooIntegrate ADM con Engagement Guida](mobile-engagement-android-adm-integrate.md) Guida.

Se si desidera tootarget dispositivi Amazon sia Google Play, il relativo toohave possibili tutto il contenuto 1 AndroidManifest.xml/APK per lo sviluppo. Ma quando si inviano tooAmazon, essi possono rifiutare l'applicazione se è disponibile codice GCM.

In tale caso, usare più file APK.

**L'applicazione è ora visualizzato e pronto tooreceive raggiungere campagne!**

## <a name="how-toohandle-data-push"></a>Come eseguire il push dei dati toohandle
### <a name="integration"></a>Integrazione
Se si desidera toobe l'applicazione è in grado di inserisce tooreceive dati Reach, avere toocreate una sottoclasse di `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e farvi riferimento in hello `AndroidManifest.xml` file (tra hello `<application>` e/o `</application>` tag):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

È possibile eseguire l'override di hello `onDataPushStringReceived` e `onDataPushBase64Received` callback. Di seguito è fornito un esempio:

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

### <a name="category"></a>Categoria
il parametro di categoria Hello è facoltativo quando si crea una campagna Push di dati e consente che inserisce dati toofilter. Ciò è utile se si dispone di più ricevitori broadcast la gestione di tipi diversi di push di dati, o se si desidera toopush diversi tipi di `Base64` tooidentify dati e si desidera tipo prima dell'analisi li.

### <a name="callbacks-return-parameter"></a>Parametro restituito dai callback
Ecco alcune linee guida tooproperly handle hello parametro restituito di `onDataPushStringReceived` e `onDataPushBase64Received`:

* Deve restituire un ricevitore broadcast `null` nel callback hello se non conosce push toohandle un tipo di dati. È consigliabile utilizzare hello categoria toodetermine se il ricevitore broadcast deve gestire il push di dati hello o non.
* Uno dei hello broadcast destinatario deve restituire `true` nel callback hello se accetta il push di dati di hello.
* Uno dei hello broadcast destinatario deve restituire `false` nel callback hello se riconosce il push di dati di hello, ma ignora per qualsiasi motivo. Ad esempio, restituire `false` quando hello ha ricevuto dati non sono validi.
* Se uno broadcast destinatario restituisce `true` mentre un altro restituisce `false` per hello stesso push di dati, il comportamento di hello è definito, è consigliabile non farlo.

tipo restituito di Hello viene usato solo per le statistiche di copertura hello:

* `Replied`viene incrementato se uno di ricevitori broadcast hello ha restituito uno `true` o `false`.
* `Actioned`viene incrementato solo se uno di hello broadcast ricevitori restituiti `true`.

## <a name="how-toocustomize-campaigns"></a>Come le campagne toocustomize
toocustomize campagne, è possibile modificare il layout di hello forniti in hello Reach SDK.

È consigliabile mantenere tutti gli identificatori di hello utilizzati nei layout hello e mantenere hello tipi di viste di hello che utilizzano un identificatore, soprattutto per visualizzazioni di testo e immagine. Alcune visualizzazioni sono toohide solo utilizzato o mostrano aree in modo relativo tipo può essere modificato. Controllare il codice sorgente hello se si prevede di tipo hello toochange di una visualizzazione in layout hello fornito.

### <a name="notifications"></a>Notifiche
Sono disponibili due tipi di notifiche, ovvero le notifiche di sistema e le notifiche in-app, che usano file di layout diversi.

#### <a name="system-notifications"></a>Notifiche di sistema
le notifiche di sistema toocustomize occorre hello toouse **categorie**. È possibile passare troppo[categorie](#categories).

#### <a name="in-app-notifications"></a>Notifiche in-app
Per impostazione predefinita, una notifica in-app è una vista che toohello aggiunti in modo dinamico corrente attività utente grazie toohello Android metodo di interfaccia `addContentView()`. Si tratta di una sovrimpressione di notifica. Sovrapposizioni di notifica sono ideali per un'integrazione veloce perché non richiedono che si toomodify qualsiasi layout nell'applicazione.

toomodify aspetto hello le sovrapposizioni di notifica, è sufficiente modificare il file hello `engagement_notification_area.xml` tooyour necessario.

> [!NOTE]
> file Hello `engagement_notification_overlay.xml` è hello che viene utilizzato toocreate una sovrapposizione di notifica, include file hello `engagement_notification_area.xml`. È inoltre possibile personalizzare il toosuit le proprie esigenze (quali per l'area di notifica hello all'interno di sovrapposizione hello di posizionamento).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Includere il layout per le notifiche come parte del layout di un'attività
Le sovrimpressioni sono ideali per un'integrazione rapida, ma possono risultare fastidiose o possono avere effetti collaterali in alcuni casi speciali. sistema di sovrapposizione Hello può essere personalizzata a livello di attività, rendendo gli effetti collaterali tooprevent semplice per le attività speciale.

È possibile decidere il layout di notifica tooinclude nel toohello di grazie layout Android esistente **includono** istruzione. Hello seguito è riportato un esempio di un oggetto modificato `ListActivity` layout che contengono solo un `ListView`.

**Prima dell'integrazione con Engagement:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Dopo l'integrazione con Engagement:**

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

In questo esempio è stato aggiunto un contenitore padre, perché il layout originale di hello utilizzata una visualizzazione elenco come elemento di primo livello hello. Abbiamo anche aggiunto `android:layout_weight="1"` tooadd in grado di toobe una vista di sotto di una visualizzazione elenco è configurato con `android:layout_height="fill_parent"`.

Hello Engagement Reach SDK rileva automaticamente che notifica il layout hello è incluso in questa attività e non verrà aggiunto un overlay per questa attività.

> [!TIP]
> Se si utilizza un ListActivity nell'applicazione, una sovrapposizione di copertura visibile sarà possibile reazione tooclicked gli elementi in visualizzazione elenco hello più. Questo è un problema noto. toowork questo problema si consiglia di layout di notifica tooembed hello nel proprio elenco attività layout come nell'esempio precedente hello.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Disabilitazione delle notifiche dell'applicazione per le singole attività
Se non si desidera hello sovrapposizione toobe aggiunti tooyour attività e se non si include il layout di notifica hello in un layout personalizzato, è possibile disabilitare sovrapposizione hello per questa attività di hello `AndroidManifest.xml` aggiungendo un `meta-data` sezione come nell'esempio hello esempio:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> Categorie
Quando si modifica hello fornito layout, modificare aspetto hello di tutte le notifiche. Le categorie consentono toodefine che vari destinazione Cerca (possibilmente comportamenti) per le notifiche. Quando si crea una campagna Reach, è possibile specificare una categoria. Tenere presente che le categorie consentono di personalizzare annunci e sondaggi, come descritto successivamente nel documento.

tooregister un gestore di categoria per le notifiche, è necessario tooadd una chiamata quando viene inizializzata l'applicazione hello.

> [!IMPORTANT]
> Leggere l'avviso hello sull'attributo android: processo hello \<android-sdk-engagement-process\> in hello come tooIntegrate Engagement su Android argomento prima di procedere.
> 
> 

Hello seguente si presuppone è riconosciuto avviso precedente hello e usare una sottoclasse di `EngagementApplication`:

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

Hello `MyNotifier` oggetto è l'implementazione di hello del gestore di categoria di notifica hello. È l'implementazione di hello `EngagementNotifier` interfaccia o una sottoclasse dell'implementazione predefinita di hello: `EngagementDefaultNotifier`.

Si noti che hello notifica stesso grado di gestire diverse categorie, è possibile registrarli simile al seguente:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

implementazione di categoria tooreplace hello predefinita, è possibile registrare l'implementazione come nel seguente esempio hello:

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

categoria di Hello corrente utilizzata in un gestore viene passata come un parametro nella maggior parte dei metodi in cui è possibile eseguire l'override `EngagementDefaultNotifier`.

Viene passata come parametro `String` o indirettamente in un oggetto `EngagementReachContent` che ha un metodo `getCategory()`.

È possibile modificare la maggior parte del processo di creazione notifica hello mediante la ridefinizione di metodi su `EngagementDefaultNotifier`per personalizzazione più avanzata è disponibile tootake un aspetto della documentazione tecnica di hello e codice sorgente hello.

##### <a name="in-app-notifications"></a>Notifiche in-app
Se si desidera layout alternativi toouse per una categoria specifica, è possibile implementare come hello di esempio seguente:

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

**Esempio di `my_notification_overlay.xml`:**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Come si può notare, l'identificatore della vista sovrapposizione hello è diverso da standard hello uno. È importante che ogni layout usi un identificatore univoco per le sovrimpressioni.

**Esempio di `my_notification_area.xml`:**

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

Come si può notare, identificatore visualizzazione area di notifica hello è diverso da quello standard hello uno. È importante che ogni layout usi un identificatore univoco per le aree di notifica.

Questo semplice esempio di categoria rende le notifiche di applicazione (o in-app) visualizzate in alto hello hello. Non è stato hello standard identificatori nell'area di notifica hello stesso.

Se si desidera, la presenza di hello tooredefine toochange `EngagementDefaultNotifier.prepareInAppArea` metodo. È consigliabile toolook della documentazione tecnica di hello e codice sorgente hello di `EngagementNotifier` e `EngagementDefaultNotifier` se si desidera questo livello di personalizzazione avanzata.

##### <a name="system-notifications"></a>Notifiche di sistema
Estendendo `EngagementDefaultNotifier`, è possibile eseguire l'override `onNotificationPrepared` notifica hello tooalter preparato dall'implementazione predefinita di hello.

ad esempio:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

In questo esempio crea una notifica di sistema per un contenuto verrà visualizzato come un evento in corso quando hello "in corso" categoria viene utilizzata.

Se si desidera hello toobuild `Notification` dell'oggetto da zero, è possibile restituire `false` toohello metodo e chiamare `notify` in hello `NotificationManager`. In questo caso è importante mantenere un `contentIntent`, `deleteIntent` e hello identificatore di notifica utilizzato da `EngagementReachReceiver`.

L'esempio seguente illustra un'implementazione corretta di questo tipo:

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

##### <a name="notification-only-announcements"></a>Annunci di sola notifica
Hello gestione di hello fare clic su una solo annuncio può essere personalizzato eseguendo l'override di notifica `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello preparato `Intent`. Questo metodo consente il flag di hello tootune facilmente.

Ad esempio tooadd hello `SINGLE_TOP` flag:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Per gli utenti di Engagement legacy, tenere presente che le notifiche di sistema senza azione URL ora viene avviata un'applicazione hello se è stato in background, pertanto è possibile chiamare questo metodo con un annuncio senza URL di azione. È necessario considerare che quando si personalizza l'intento di hello.

È anche possibile implementare `EngagementNotifier.executeNotifAnnouncementAction` da zero.

##### <a name="notification-life-cycle"></a>Ciclo di vita delle notifiche
Quando si utilizza categoria predefinita hello, alcuni metodi del ciclo di vita vengono chiamati in hello `EngagementReachInteractiveContent` tooreport stato campagna hello statistiche e l'aggiornamento dell'oggetto:

* Quando la notifica hello viene visualizzata nell'applicazione o inserire nella barra di stato hello, hello `displayNotification` metodo viene chiamato (che indica le statistiche) da `EngagementReachAgent` se `handleNotification` restituisce `true`.
* Se la notifica hello viene ignorata, hello `exitNotification` metodo viene chiamato, viene segnalata statistica e campagne successiva ora possono essere elaborate.
* Se si fa clic notifica hello, `actionNotification` viene chiamato, viene segnalata statistica e viene avviato con finalità di hello associata.

Se l'implementazione di `EngagementNotifier` bypass hello comportamento predefinito, è necessario toocall questi metodi del ciclo di vita da soli. Hello seguono esempi vengono illustrati alcuni casi in cui viene ignorato il comportamento predefinito di hello:

* Il metodo `EngagementDefaultNotifier` non è stato esteso, ad esempio la gestione delle categorie è stata implementata da zero.
* Per le notifiche di sistema, si overrode hello `onNotificationPrepared` e sono stati modificati `contentIntent` o `deleteIntent` in hello `Notification` oggetto.
* Per le notifiche nell'applicazione, overrode `prepareInAppArea`, toomap che almeno `actionNotification` tooone dei controlli U.I.

> [!NOTE]
> Se `handleNotification` genera un'eccezione, hello contenuto viene eliminato e `dropContent` viene chiamato. Ciò viene segnalato nelle statistiche e sarà possibile elaborare le campagne successive.
> 
> 

### <a name="announcements-and-polls"></a>Annunci e sondaggi
#### <a name="layouts"></a>Layout
È possibile modificare hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` file toocustomize annunci di testo, sondaggi e gli annunci di web.

Questi file condividono due layout comuni per l'area del titolo hello e l'area del pulsante hello. layout di Hello per titolo hello è `engagement_content_title.xml` e utilizza hello eponymous drawable file per lo sfondo di hello. Hello layout per i pulsanti di azione e uscita hello è `engagement_button_bar.xml` e utilizza hello eponymous drawable file per lo sfondo di hello.

In un sondaggio, hello layout domanda e le scelte sono ingrandite in modo dinamico utilizzando più volte hello `engagement_question.xml` file layout per domande hello e hello `engagement_choice.xml` file per le scelte di hello.

#### <a name="categories"></a>Categorie
##### <a name="alternate-layouts"></a>Layout alternativi
Come le notifiche, la categoria della campagna hello può essere utilizzato toohave layout alternativi per gli annunci e viene eseguito il polling.

Ad esempio, toocreate una categoria per un annuncio di testo, è possibile estendere `EngagementTextAnnouncementActivity` e farvi riferimento hello `AndroidManifest.xml` file:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Si noti che categoria hello finalità hello filtro viene utilizzato differenza hello toomake con attività di annuncio hello predefinita.

Hello Reach SDK Usa hello preventivo tooresolve hello destra l'attività del sistema per una categoria specifica e viene utilizzata la cartella nella categoria predefinita hello se hello risoluzione non riuscita.

È necessario tooimplement `MyCustomTextAnnouncementActivity`, solo il layout di hello toochange (senza mantenere hello stessi identificatori di visualizzazione), è sufficiente classe hello toodefine come nel seguente esempio hello:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

categoria di tooreplace hello predefinita di annunci di testo, sostituire semplicemente `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` dall'implementazione.

Gli annunci Web e i sondaggi possono essere personalizzati in modo analogo.

Per gli annunci web è possibile estendere `EngagementWebAnnouncementActivity` e dichiarare l'attività di hello `AndroidManifest.xml` come nell'esempio seguente hello:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Per i sondaggi è possibile estendere `EngagementPollActivity` e dichiarare il hello in `AndroidManifest.xml` come nell'esempio seguente hello:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implementazione da zero
È possibile implementare le categorie per le attività di annuncio (e polling) senza l'estensione di uno di hello `Engagement*Activity` le classi fornite da hello Reach SDK. Ciò è utile, ad esempio se si desidera toodefine un layout che non utilizza hello stesso viste come layout standard hello.

Ad esempio per la personalizzazione avanzata notifica, è consigliabile toolook al codice sorgente hello dell'implementazione standard di hello.

Ecco alcuni aspetti tookeep presente: Reach verrà avviata l'attività hello un preventivo specifico (corrispondente toohello preventivo filtro) più un parametro aggiuntivo che è l'identificatore di contenuto hello.

tooretrieve hello oggetto contenuto che contengono campi hello specificati quando la creazione di hello campagna sul sito web hello è possibile farlo:

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

Per le statistiche, sarà necessario segnalare hello contenuto viene visualizzato in hello `onResume` evento:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Quindi, non dimenticare toocall sia `actionContent(this)` o `exitContent(this)` sull'oggetto di contenuto hello prima attività hello in background.

Se non si chiama uno `actionContent` o `exitContent`, le statistiche non verranno inviate (vale a dire non analitica nella campagna hello) e più importante, hello campagne successive non verranno notificate fino a quando non viene riavviato il processo di applicazione hello.

Orientamento o altre modifiche alla configurazione possono hello codice difficile toodetermine se l'attività hello viene posto in background o non di hello rende implementazione standard contenuto hello che viene segnalato come è stato chiuso se l'utente di hello lascia attività hello (tramite premendo `HOME` o `BACK`) ma non se cambia l'orientamento hello.

Di seguito è interessante hello dell'implementazione di hello:

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

Come si può notare, se è stato chiamato `actionContent(this)` quindi terminata attività hello, `exitContent(this)` può essere chiamato in modo sicuro senza causare alcun effetto.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
