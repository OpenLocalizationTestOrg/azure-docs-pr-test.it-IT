
### <a name="update-manifest-file-tooenable-notifications"></a>File manifesto tooenable notifiche di aggiornamento
Copiarne risorse di messaggistica in-app hello sotto il manifest tra hello `<application>` e `</application>` tag.

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

### <a name="specify-an-icon-for-notifications"></a>Specificare un'icona per le notifiche
Hello Incolla seguente frammento di codice XML del file manifest. XML tra hello `<application>` e `</application>` tag.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Definisce l'icona di hello visualizzata sia nel sistema e le notifiche in-app. Essa è facoltativa per le notifiche in-app, ma obbligatoria per le notifiche di sistema. Android rifiuterà le notifiche di sistema con icone non valide.

Assicurarsi che si utilizza un'icona che esiste in uno dei hello **drawable** cartelle (ad esempio ``engagement_close.png``). **mipmap** non è supportata.

> [!NOTE]
> Non è consigliabile utilizzare hello **avvio** icona. Dispone di una risoluzione di diversi e viene in genere nelle cartelle di mipmap hello, che non è supportato.
> 
> 

Per le app reali, è possibile usare un'icona adatta alle notifiche in base alle [linee guida per la progettazione per Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toobe che toouse corretto risoluzioni icona, è possibile esaminare [questi esempi](https://www.google.com/design/icons).
> Scorrere verso il basso toohello **notifica** sezione e quindi fare clic su un'icona `PNGS` set drawable di toodownload hello icone. È possibile visualizzare le cartelle drawable con cui toouse risoluzione per ogni versione dell'icona hello.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Abilitare le notifiche di push app tooreceive GCM
1. Incollare l'esempio hello nel manifest tra hello `<application>` e `</application>` tag dopo la sostituzione di hello **ID mittente** ottenuto dalla console Firebase progetto. \n Hello è intenzionale quindi assicurarsi che si termina di progetto hello numero con esso.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Incollare codice hello sotto il manifest tra hello `<application>` e `</application>` tag. Sostituire il nome di pacchetto hello <Your package name>.
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. Aggiungere l'ultimo set di autorizzazioni che sono evidenziati prima hello di hello `<application>` tag. Sostituire `<Your package name>` in base al nome di pacchetto effettivo hello dell'applicazione.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

