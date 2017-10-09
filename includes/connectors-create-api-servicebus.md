### <a name="prerequisites"></a>Prerequisiti
È necessario avere un account del [bus di servizio](https://azure.microsoft.com/services/service-bus/).  

Prima di poter utilizzare l'account di Azure Service Bus in un'app di logica, è necessario autorizzare l'account di hello logica app tooconnect tooyour service bus. Fortunatamente, è possibile farlo facilmente all'interno dell'app logica su hello portale di Azure.  

Di seguito è hello passaggi tooauthorize il tooyour tooconnect di logica app account Bus di servizio:  

1. Selezionare un tooService connessione Bus, nella finestra di progettazione di hello logica app, toocreate **Mostra Microsoft API gestite** nell'elenco a discesa hello. Immettere quindi **bus di servizio** nella casella di ricerca hello. Selezionare trigger hello o azione che si desidera toouse.  
    ![Immagine di connessione al bus di servizio 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Se non sono state create tooService eventuali connessioni Bus prima, si sarà tooprovide richieste le credenziali del Bus di servizio. Queste credenziali vengono utilizzate tooauthorize tooand di tooconnect app la logica di accesso ai dati dell'account del Bus di servizio. connettore di Service Bus Hello deve stringa di connessione hello per spazio dei nomi Service Bus hello. Richiede anche le autorizzazioni **Gestisci**. Tooknow una buona soluzione se la stringa di connessione dello spazio dei nomi hello o un'entità specifica non contiene se hello `EntityPath` parametro. In caso affermativo, non è di stringa di connessione corretta hello per un'app di logica.  
    ![Stringa di connessione del bus di servizio](./media/connectors-create-api-servicebus/connectionstring.png)
3. Dopo aver ricevuto la stringa di connessione hello per spazio dei nomi hello, è possibile utilizzare per la connessione API in App per la logica di hello.  
    ![Immagine di connessione al bus di servizio 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Si noti hello connessione è stata creata e si è ora disponibile tooproceed con altri hello i passaggi nell'app logica.  
    ![Immagine di connessione al bus di servizio 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

