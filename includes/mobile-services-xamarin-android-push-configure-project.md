
1. In visualizzazione soluzione hello (o **Esplora** in Visual Studio), hello rapida **componenti** cartella, fare clic su **ottenere più componenti...** , cercare hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto.
2. Aprire il file di progetto ToDoActivity.cs hello e aggiungere il seguente hello utilizzando istruzione toohello classe:
   
        using Gcm.Client;
3. In hello **ToDoActivity** classe, aggiungere hello nuovo codice seguente: 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    In questo modo istanza client per dispositivi mobili di hello tooaccess dal processo del servizio gestore hello push.
4. Aggiungere i seguenti toohello codice hello **OnCreate** (metodo), dopo aver hello **MobileServiceClient** viene creato:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

La classe **ToDoActivity** è ora pronta per l'aggiunta di notifiche push.

