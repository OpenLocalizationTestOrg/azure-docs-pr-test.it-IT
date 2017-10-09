1. Nel **app** progetto, il file aperto hello `AndroidManifest.xml`. Nel codice hello in hello due passaggi successivi, sostituire  *`**my_app_package**`*  con nome hello del pacchetto dell'applicazione hello per il progetto. Questo è il valore di hello di hello `package` attributo di hello `manifest` tag.
2. Aggiungere queste autorizzazioni di nuovo dopo hello esistente hello `uses-permission` elemento:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Aggiungere hello seguente codice dopo hello `application` tag di apertura:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. File aperti hello *ToDoActivity.java*e aggiungere hello successiva istruzione di importazione:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Aggiungere hello seguente classe toohello variabile privata. Sostituire  *`<PROJECT_NUMBER>`*  con numero di progetto hello assegnato da Google tooyour app nella precedente procedura hello.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Modificare la definizione di hello di *MobileServiceClient* da **privata** troppo**statici pubblici**, pertanto ora simile al seguente:

        public static MobileServiceClient mClient;
7. Aggiungere un nuovo notifiche toohandle classe. In Esplora progetti, aprire hello **src** > **principale** > **java** nodi e nodo nome pacchetto hello del pulsante destro del mouse. Fare clic su **Nuovo** e quindi su **Java Class** (Classe Java).
8. In **Nome** digitare `MyHandler`, quindi fare clic su **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. Nel file MyHandler hello, sostituire la dichiarazione di classe hello con:

        public class MyHandler extends NotificationsHandler {
10. Aggiungere hello seguendo le istruzioni di importazione per hello `MyHandler` classe:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Aggiungere questo toohello membro `MyHandler` classe:

        public static final int NOTIFICATION_ID = 1;
12. In hello `MyHandler` classe, aggiungere i seguenti hello toooverride codice hello **onRegistered** (metodo), che registra il dispositivo con hub di notifica di hello servizio mobile.

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
       }
13. In hello `MyHandler` classe, aggiungere i seguenti hello toooverride codice hello **onReceive** metodo che causa hello notifica toodisplay quando viene ricevuto.

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
       }
14. Nel file TodoActivity.java hello, aggiornare hello **onCreate** metodo hello *ToDoActivity* classe classe del gestore tooregister hello notifica. Eseguire questo codice che tooadd hello *MobileServiceClient* viene creata un'istanza.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    L'app è notifiche push toosupport aggiornato.
