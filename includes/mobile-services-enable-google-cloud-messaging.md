
1. Passare toohello [Google Cloud Console](https://console.developers.google.com/project), accedere con le credenziali dell'account Google. 
2. Fare clic su **Crea progetto**, digitare un nome di progetto e quindi fare clic su **Crea**. Se richiesto, eseguire la verifica tramite SMS hello e fare clic su **crea** nuovamente.
   
    ![Creare un nuovo progetto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Digitare il nuovo **nome del progetto** e fare clic su **Crea progetto**.
3. Fare clic su hello **utilità e altro ancora** pulsante e quindi fare clic su **informazioni sul progetto**. Prendere nota di hello **numero progetto**. Sarà necessario tooset questo valore come hello `SenderId` variabili nell'app client hello.
   
    ![Utilità e altro ancora](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. In hello progetto dashboard, in **API Mobile**, fare clic su **Google Cloud Messaging**, quindi fare clic nella pagina successiva hello **Abilita API** e accettare le condizioni di hello del servizio. 
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Nel dashboard del progetto hello, fare clic su **credenziali** > **Create Credential** > **chiave API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. In **Crea una nuova chiave** fare clic su **Chiave server**, digitare un nome per la chiave e quindi fare clic su **Crea**.
7. Prendere nota di hello **chiave API** valore.
   
    Si utilizza questo tooenable valore della chiave API tooauthenticate Azure con GCM e inviare notifiche push per conto dell'applicazione.

