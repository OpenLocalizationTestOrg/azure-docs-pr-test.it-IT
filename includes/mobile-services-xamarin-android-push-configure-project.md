
1. <span data-ttu-id="7ae02-101">In visualizzazione soluzione hello (o **Esplora** in Visual Studio), hello rapida **componenti** cartella, fare clic su **ottenere più componenti...** , cercare hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="7ae02-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="7ae02-102">Aprire il file di progetto ToDoActivity.cs hello e aggiungere il seguente hello utilizzando istruzione toohello classe:</span><span class="sxs-lookup"><span data-stu-id="7ae02-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="7ae02-103">In hello **ToDoActivity** classe, aggiungere hello nuovo codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7ae02-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
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
   
    <span data-ttu-id="7ae02-104">In questo modo istanza client per dispositivi mobili di hello tooaccess dal processo del servizio gestore hello push.</span><span class="sxs-lookup"><span data-stu-id="7ae02-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="7ae02-105">Aggiungere i seguenti toohello codice hello **OnCreate** (metodo), dopo aver hello **MobileServiceClient** viene creato:</span><span class="sxs-lookup"><span data-stu-id="7ae02-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="7ae02-106">La classe **ToDoActivity** è ora pronta per l'aggiunta di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="7ae02-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

