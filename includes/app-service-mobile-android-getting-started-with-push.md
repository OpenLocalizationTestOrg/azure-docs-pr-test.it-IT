1. <span data-ttu-id="fea68-101">Nel **app** progetto, il file aperto hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="fea68-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="fea68-102">Nel codice hello in hello due passaggi successivi, sostituire  *`**my_app_package**`*  con nome hello del pacchetto dell'applicazione hello per il progetto.</span><span class="sxs-lookup"><span data-stu-id="fea68-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="fea68-103">Questo è il valore di hello di hello `package` attributo di hello `manifest` tag.</span><span class="sxs-lookup"><span data-stu-id="fea68-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="fea68-104">Aggiungere queste autorizzazioni di nuovo dopo hello esistente hello `uses-permission` elemento:</span><span class="sxs-lookup"><span data-stu-id="fea68-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="fea68-105">Aggiungere hello seguente codice dopo hello `application` tag di apertura:</span><span class="sxs-lookup"><span data-stu-id="fea68-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="fea68-106">File aperti hello *ToDoActivity.java*e aggiungere hello successiva istruzione di importazione:</span><span class="sxs-lookup"><span data-stu-id="fea68-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="fea68-107">Aggiungere hello seguente classe toohello variabile privata.</span><span class="sxs-lookup"><span data-stu-id="fea68-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="fea68-108">Sostituire  *`<PROJECT_NUMBER>`*  con numero di progetto hello assegnato da Google tooyour app nella precedente procedura hello.</span><span class="sxs-lookup"><span data-stu-id="fea68-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="fea68-109">Modificare la definizione di hello di *MobileServiceClient* da **privata** troppo**statici pubblici**, pertanto ora simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fea68-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="fea68-110">Aggiungere un nuovo notifiche toohandle classe.</span><span class="sxs-lookup"><span data-stu-id="fea68-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="fea68-111">In Esplora progetti, aprire hello **src** > **principale** > **java** nodi e nodo nome pacchetto hello del pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="fea68-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="fea68-112">Fare clic su **Nuovo** e quindi su **Java Class** (Classe Java).</span><span class="sxs-lookup"><span data-stu-id="fea68-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="fea68-113">In **Nome** digitare `MyHandler`, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fea68-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="fea68-114">Nel file MyHandler hello, sostituire la dichiarazione di classe hello con:</span><span class="sxs-lookup"><span data-stu-id="fea68-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="fea68-115">Aggiungere hello seguendo le istruzioni di importazione per hello `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="fea68-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="fea68-116">Aggiungere questo toohello membro `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="fea68-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="fea68-117">In hello `MyHandler` classe, aggiungere i seguenti hello toooverride codice hello **onRegistered** (metodo), che registra il dispositivo con hub di notifica di hello servizio mobile.</span><span class="sxs-lookup"><span data-stu-id="fea68-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="fea68-118">}</span><span class="sxs-lookup"><span data-stu-id="fea68-118">}</span></span>
13. <span data-ttu-id="fea68-119">In hello `MyHandler` classe, aggiungere i seguenti hello toooverride codice hello **onReceive** metodo che causa hello notifica toodisplay quando viene ricevuto.</span><span class="sxs-lookup"><span data-stu-id="fea68-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="fea68-120">}</span><span class="sxs-lookup"><span data-stu-id="fea68-120">}</span></span>
14. <span data-ttu-id="fea68-121">Nel file TodoActivity.java hello, aggiornare hello **onCreate** metodo hello *ToDoActivity* classe classe del gestore tooregister hello notifica.</span><span class="sxs-lookup"><span data-stu-id="fea68-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="fea68-122">Eseguire questo codice che tooadd hello *MobileServiceClient* viene creata un'istanza.</span><span class="sxs-lookup"><span data-stu-id="fea68-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="fea68-123">L'app è notifiche push toosupport aggiornato.</span><span class="sxs-lookup"><span data-stu-id="fea68-123">Your app is now updated toosupport push notifications.</span></span>
