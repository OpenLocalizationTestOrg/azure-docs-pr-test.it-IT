### <a name="prerequisites"></a>Prerequisiti
* Un account Twilio
* Un numero di telefono Twilio verificato in grado di ricevere SMS
* Un numero di telefono Twilio verificato in grado di inviare SMS

> [!NOTE]
> Se si utilizza un account di valutazione di Twilio, è possibile solo inviare SMS troppo**verificato** i numeri di telefono.  
> 
> 

Prima di poter utilizzare l'account di Twilio in un'app di logica, è necessario autorizzare l'account di Twilio tooyour hello logica app tooconnect. Fortunatamente, è possibile farlo facilmente all'interno dell'app logica su hello portale di Azure. 

Di seguito è hello passaggi tooauthorize il tooyour tooconnect di logica app account Twilio:

1. toocreate tooTwilio una connessione, nella finestra di progettazione di hello logica app, selezionare **Mostra Microsoft API gestite** in hello nell'elenco a discesa, quindi immettere *Twilio* nella casella di ricerca hello. Selezionare trigger hello o azione che ti toouse:  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Se è ancora stato creato alcun tooTwilio connessioni prima, si otterrà tooprovide richieste le credenziali di Twilio. Queste credenziali verranno utilizzato tooauthorize tooconnect di app la logica per e accedere ai dati dell'account di Twilio:  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. È necessario hello **id dell'account Twilio** e **il token di accesso di Twilio** dal dashboard di hello in Twilio, quindi accedi tooyour Twilio account ora toograb questi due tipi di informazioni:  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. App Twilio e logica di utilizzare nomi diversi tooidentify questi due tipi di informazioni. Ecco come è necessario eseguirne il mapping finestra di dialogo toohello logica App:![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Seleziona hello **creare connessione** pulsante:  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. Si noti hello connessione è stata creata e si è ora disponibile tooproceed con altri hello i passaggi nell'app logica:  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

