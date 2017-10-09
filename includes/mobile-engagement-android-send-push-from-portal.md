### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Engagement Mobile concedere accesso tooyour chiave API GCM
tooallow Mobile Engagement toosend delle notifiche push per conto dell'utente, è necessario accedere a tooyour chiave API toogrant. Questa operazione viene eseguita la configurazione e inserendo la chiave nel portale Mobile Engagement hello.

1. Mediante il portale di Azure classico, verificare le app hello è in uso per questo progetto e quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Quindi fare clic su hello **impostazioni** -> **Push nativo** sezione tooenter la chiave GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Fare clic su hello **modifica** icona davanti **chiave API** in hello **impostazioni GCM** sezione come illustrato di seguito:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Nel menu a comparsa hello, incollare hello chiave Server GCM ottenuto prima e quindi fare clic su **Ok**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Invia un'app tooyour notifica
Verrà ora creata una campagna di notifica push semplice che invia un'app tooour di notifica push.

1. Passare toohello **raggiungere** scheda nel portale Mobile Engagement.
2. Fare clic su **nuovo annuncio** toocreate la campagna di notifica push.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Impostare i campi prima di hello della campagna tramite hello alla procedura seguente:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Assegnare un nome alla campagna.
   
    b. Seleziona hello **tipo di recapito** come *notifica di sistema -> semplice*: tipo di notifica push Android semplice hello che le funzionalità di un titolo e una riga di piccole dimensioni di testo.
   
    c. Selezionare **l'ora di recapito** come *qualsiasi momento* tooallow hello app tooreceive una notifica se l'applicazione hello è stato avviato o meno.
   
    d. In hello di tipo testo notifica hello **titolo** che sarà grassetto in push hello.
   
    e. Digitare quindi il **messaggio**
4. Scorrere verso il basso e in hello **contenuto** selezionare **sola notifica**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Possibili campagna più elementare di impostazione hello completato. Ora nuovamente a scorrere verso il basso e fare clic su hello **crea** pulsante toosave la campagna.
6. Ultimo passaggio: scegliere **attiva** tooactivate le notifiche di push toosend campagna.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

