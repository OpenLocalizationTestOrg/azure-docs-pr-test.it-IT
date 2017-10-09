

## <a name="generate-hello-certificate-signing-request-file"></a>Generare file di richiesta di firma certificato hello
Hello Apple Push Notification Service (APNS) utilizza certificati tooauthenticate le notifiche push. Seguire questi toosend certificato push necessarie di istruzioni toocreate hello e ricevere le notifiche. Per ulteriori informazioni su questi concetti, vedere ufficiale hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentazione.

Creare file di firma richiesta certificato (CSR) hello, che viene utilizzato da toogenerate Apple un certificato firmato push.

1. Nel Mac, eseguire lo strumento di accesso portachiavi hello. Può essere aperta da hello **utilità** cartella o hello **altri** cartella nel punto di partenza hello.
2. Fare clic su **Keychain Access** (Accesso Portachiavi), espandere **Certificate Assistant** (Assistente Certificato), quindi fare clic su **Request a Certificate from a Certificate Authority...** (Richiedi un certificato da una Autorità di Certificazione...).
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Selezionare il **indirizzo di posta elettronica utente** e **nome comune** , assicurarsi che **salvato toodisk** sia selezionata e quindi fare clic su **continua**. Lasciare hello **indirizzo di posta elettronica CA** campo vuoto perché non è obbligatorio.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Digitare un nome per il file di firma richiesta certificato (CSR) hello in **Salva con nome**, selezionare il percorso di hello in **in**, quindi fare clic su **salvare**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Questo file CSR di hello Salva nel percorso di hello selezionato. percorso predefinito di Hello è hello Desktop. Tenere presente che il percorso di hello scelto per il file.

Successivamente, si verrà registrare l'app di Apple, abilitare le notifiche push e caricare questo toocreate CSR esportato un certificato per il push.

## <a name="register-your-app-for-push-notifications"></a>Registrare l'app per le notifiche push
toobe toosend in grado di push notifiche tooan app iOS, è necessario registrare l'applicazione con Apple e registrate per le notifiche push.  

1. Se non è già stato registrato l'app, passare toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di Provisioning iOS</a> in hello Centro per sviluppatori di Apple, eseguire l'accesso con il proprio ID Apple, fare clic su **identificatori**, quindi fare clic su **ID App** e infine fare clic su hello  **+**  tooregister una nuova app di accedere.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Aggiornare i seguenti tre campi per la nuova app hello e quindi fare clic su **continua**:
   
   * **Nome**: digitare un nome descrittivo per l'app in hello **nome** campo hello **descrizione dell'ID App** sezione.
   * **Identificatore di aggregazione**: in hello **ID App esplicito** sezione, immettere un **identificatore Bundle** nel modulo hello `<Organization Identifier>.<Product Name>` come indicato in hello [distribuzione di App Guida](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Hello *identificatore organizzazione* e *nome prodotto* uso deve corrispondere identificatore organizzazione hello e il nome di prodotto che verrà utilizzato quando si crea il progetto XCode. In seguito screeshot di hello *degli hub di notifica* viene utilizzato come l'identificatore di un'organizzazione e *GetStarted* viene utilizzato come nome del prodotto hello. Assicurandosi che corrisponde valori hello che verranno utilizzati nel progetto XCode consentirà è toouse hello corretto profilo di pubblicazione con XCode. 
   * **Le notifiche push**: hello controllo **le notifiche Push** opzione hello **servizi App** sezione.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Questo genera l'ID di App e si richiede informazioni hello tooconfirm. Fare clic su **registrare** tooconfirm hello nuovo ID di App.
     
      Quando si fa clic su **registrare**, verrà visualizzato hello **registrazione completare** schermata, come illustrato di seguito. Fare clic su **Done**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Nel centro per sviluppatori, con l'ID dell'App, hello individuare hello app ID appena creato, quindi fare clic sulla riga corrispondente.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Facendo clic sull'ID di app hello verranno visualizzati i dettagli dell'app hello. Fare clic su hello **modifica** pulsante nella parte inferiore di hello.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Scorrere toohello parte inferiore della schermata di hello e fare clic su hello **Create Certificate...**  pulsante nella sezione hello **certificato SSL di Push di sviluppo**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Consente di visualizzare Assistente "Aggiungi certificato iOS" hello.
   
   > [!NOTE]
   > Questa esercitazione usa un certificato di sviluppo. Hello stesso processo viene utilizzato durante la registrazione di un certificato di produzione. Assicurarsi di utilizzare hello stesso quando si inviano notifiche di tipo di certificato.
   > 
   > 
3. Fare clic su **Scegli File**, toohello percorso di salvataggio file CSR hello creato nella prima attività hello Sfoglia, quindi fare clic su **genera**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Dopo aver creato il certificato di hello dal portale di hello, fare clic su hello **scaricare** pulsante e fare clic su **eseguita**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Questo download certificato hello e lo salva tooyour computer nella cartella di download.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Per impostazione predefinita, hello scaricati file un certificato di sviluppo è denominato **aps_development.cer**.
   > 
   > 
5. Fare doppio clic sul certificato scaricato push hello **aps_development.cer**.
   
      Questo modo vengono installati nuovo certificato hello hello Keychain, come illustrato di seguito:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > nome Hello nel certificato potrebbe essere diverso, ma verrà preceduto **sviluppo Apple iOS servizi Push:**.
   > 
   > 
6. In accesso portachiavi, fare clic sul certificato push nuova hello creati in hello **certificati** categoria. Fare clic su **esportare**, assegnare un nome file hello, selezionare hello **. p12** formattare e quindi fare clic su **salvare**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Prendere nota del nome file hello e percorso del certificato esportato. p12 hello. Sarà tooenable utilizzata l'autenticazione con il servizio APN.
   
   > [!NOTE]
   > In questa esercitazione viene creato un file QuickStart.p12. Il nome e il percorso del file potrebbero essere diversi.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Creare un profilo di provisioning per l'applicazione hello
1. In hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di Provisioning iOS</a>selezionare **i profili di Provisioning**selezionare **tutti**e quindi fare clic su hello  **+**  pulsante toocreate un nuovo profilo. Verrà avviata hello **aggiungere Provisiong profilo iOS** guidata
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Selezionare **lo sviluppo di App iOS** in **sviluppo** come tipo di profilo provisiong hello, fare clic su **continua**. 
3. Selezionare quindi l'ID app hello appena creata dal hello **ID App** elenco a discesa e fare clic su **continua**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. In hello **selezionare certificati** schermata, selezionare il certificato di sviluppo consuete utilizzato per la firma del codice e fare clic su **continua**. Non si tratta del certificato per push hello che appena creato.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Selezionare quindi hello **dispositivi** toouse per i test e fare clic su **continua**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Infine, scegliere un nome per il profilo di hello in **nome profilo**, fare clic su **genera**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Quando viene creato nuovo profilo di provisioning hello fare clic su toodownload e installazione sul computer di sviluppo Xcode. Fare quindi clic su **Done**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
