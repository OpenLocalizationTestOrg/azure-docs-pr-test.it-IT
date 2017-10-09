
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="b657e-101">File manifesto tooenable notifiche di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="b657e-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="b657e-102">Copiarne risorse di messaggistica in-app hello sotto il manifest tra hello `<application>` e `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="b657e-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="b657e-103">Specificare un'icona per le notifiche</span><span class="sxs-lookup"><span data-stu-id="b657e-103">Specify an icon for notifications</span></span>
<span data-ttu-id="b657e-104">Hello Incolla seguente frammento di codice XML del file manifest. XML tra hello `<application>` e `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="b657e-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="b657e-105">Definisce l'icona di hello visualizzata sia nel sistema e le notifiche in-app.</span><span class="sxs-lookup"><span data-stu-id="b657e-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="b657e-106">Essa è facoltativa per le notifiche in-app, ma obbligatoria per le notifiche di sistema.</span><span class="sxs-lookup"><span data-stu-id="b657e-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="b657e-107">Android rifiuterà le notifiche di sistema con icone non valide.</span><span class="sxs-lookup"><span data-stu-id="b657e-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="b657e-108">Assicurarsi che si utilizza un'icona che esiste in uno dei hello **drawable** cartelle (ad esempio ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="b657e-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="b657e-109">**mipmap** non è supportata.</span><span class="sxs-lookup"><span data-stu-id="b657e-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="b657e-110">Non è consigliabile utilizzare hello **avvio** icona.</span><span class="sxs-lookup"><span data-stu-id="b657e-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="b657e-111">Dispone di una risoluzione di diversi e viene in genere nelle cartelle di mipmap hello, che non è supportato.</span><span class="sxs-lookup"><span data-stu-id="b657e-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="b657e-112">Per le app reali, è possibile usare un'icona adatta alle notifiche in base alle [linee guida per la progettazione per Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="b657e-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="b657e-113">toobe che toouse corretto risoluzioni icona, è possibile esaminare [questi esempi](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="b657e-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="b657e-114">Scorrere verso il basso toohello **notifica** sezione e quindi fare clic su un'icona `PNGS` set drawable di toodownload hello icone.</span><span class="sxs-lookup"><span data-stu-id="b657e-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="b657e-115">È possibile visualizzare le cartelle drawable con cui toouse risoluzione per ogni versione dell'icona hello.</span><span class="sxs-lookup"><span data-stu-id="b657e-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="b657e-116">Abilitare le notifiche di push app tooreceive GCM</span><span class="sxs-lookup"><span data-stu-id="b657e-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="b657e-117">Incollare l'esempio hello nel manifest tra hello `<application>` e `</application>` tag dopo la sostituzione di hello **ID mittente** ottenuto dalla console Firebase progetto.</span><span class="sxs-lookup"><span data-stu-id="b657e-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="b657e-118">\n Hello è intenzionale quindi assicurarsi che si termina di progetto hello numero con esso.</span><span class="sxs-lookup"><span data-stu-id="b657e-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="b657e-119">Incollare codice hello sotto il manifest tra hello `<application>` e `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="b657e-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="b657e-120">Sostituire il nome di pacchetto hello <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="b657e-120">Replace hello package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="b657e-121">Aggiungere l'ultimo set di autorizzazioni che sono evidenziati prima hello di hello `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="b657e-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="b657e-122">Sostituire `<Your package name>` in base al nome di pacchetto effettivo hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b657e-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

