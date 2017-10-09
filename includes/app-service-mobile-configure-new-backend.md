
1. Fare clic su hello **servizi App** pulsante, selezionare l'App per dispositivi mobili di back-end, **delle Guide rapide**, quindi selezionare la piattaforma (iOS, Android, Xamarin, Cordova) dei client.

    ![Portale di Azure con Avvio rapido per le app per dispositivi mobili evidenziato][quickstart]

2. Se non è configurata una connessione al database, crearne una eseguendo hello seguenti:

    ![Portale di Azure con App Mobile Connect toodatabase][connect]

    a. Creare un nuovo server e un nuovo database SQL.

    ![Portale di Azure con creazione di un nuovo database e un nuovo server per le app per dispositivi mobili][server]

    b. Attendere finché non viene creato correttamente connessione dati hello.

    ![Notifica del completamento della creazione della connessione dati nel portale di Azure][notification]

    c. La connessione dati deve avere esito positivo.

    ![Notifica "Esiste già una connessione dati" nel portale di Azure][already-connection]

3. In **2. Creare un'API di tabella** selezionare Node.js per **Linguaggio back-end**. 
 
4. Accettare il riconoscimento di hello e quindi selezionare **tabella TodoItem creare**.  
    Con questa azione viene creata una nuova tabella di attività nel database. 

    >[!IMPORTANT]
    > Cambio di un tooNode.js back-end esistente verrà sovrascritto tutto il contenuto. un back-end .NET, vedere toocreate [funziona con server hello back-end .NET SDK per App per dispositivi mobili][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
