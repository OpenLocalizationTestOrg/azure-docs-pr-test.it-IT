
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="f9cfd-101">Aggiornare il file manifesto per abilitare le notifiche</span><span class="sxs-lookup"><span data-stu-id="f9cfd-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="f9cfd-102">Copiare le risorse di messaggistica in-app seguenti nel file Manifest.xml tra i tag `<application>` e `</application>`.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="f9cfd-103">Specificare un'icona per le notifiche</span><span class="sxs-lookup"><span data-stu-id="f9cfd-103">Specify an icon for notifications</span></span>
<span data-ttu-id="f9cfd-104">Incollare il frammento di codice XML seguente nel file Manifest.xml tra i tag `<application>` e `</application>`.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="f9cfd-105">In questo modo si definisce l'icona che viene visualizzata sia nelle notifiche di sistema sia nelle notifiche in-app.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="f9cfd-106">Essa è facoltativa per le notifiche in-app, ma obbligatoria per le notifiche di sistema.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="f9cfd-107">Android rifiuterà le notifiche di sistema con icone non valide.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="f9cfd-108">Assicurarsi di usare un'icona esistente in una delle cartelle **drawable** (ad esempio ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="f9cfd-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="f9cfd-109">**mipmap** non è supportata.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="f9cfd-110">È consigliabile non usare l'icona di **avvio**.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="f9cfd-111">poiché ha una risoluzione diversa e si trova in genere nelle cartelle mipmap, che non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="f9cfd-112">Per le app reali, è possibile usare un'icona adatta alle notifiche in base alle [linee guida per la progettazione per Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="f9cfd-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="f9cfd-113">Per assicurarsi di usare la risoluzione corretta per l'icona, vedere [questi esempi](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="f9cfd-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="f9cfd-114">Scorrere verso il basso fino alla sezione **Notification**, fare clic su un'icona e quindi su `PNGS` per scaricare il set di icone di tipo drawable.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="f9cfd-115">È possibile scegliere le cartelle drawable da usare con una risoluzione specifica per ogni versione dell'icona.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="f9cfd-116">Abilitare l'app per la ricezione delle notifiche push GCM</span><span class="sxs-lookup"><span data-stu-id="f9cfd-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="f9cfd-117">Incollare quanto segue nel file Manifest.xml tra i tag `<application>` e `</application>` dopo aver sostituito il **Sender ID** ottenuto dalla console del progetto Firebase.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="f9cfd-118">L'uso di \n è intenzionale. Assicurarsi di inserirlo alla fine del numero di progetto.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="f9cfd-119">Incollare il codice seguente nel file Manifest.xml tra i tag `<application>` e `</application>`.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="f9cfd-120">Sostituire il nome del pacchetto <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-120">Replace the package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="f9cfd-121">Aggiungere l'ultimo set di autorizzazioni evidenziate prima del tag `<application>` .</span><span class="sxs-lookup"><span data-stu-id="f9cfd-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="f9cfd-122">Sostituire `<Your package name>` con il nome effettivo del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f9cfd-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

