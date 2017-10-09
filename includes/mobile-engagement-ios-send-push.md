### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Concedere accesso tooyour certificato Push tooMobile Engagement
Engagement Mobile tooallow toosend le notifiche Push per conto dell'utente, è necessario accedere a certificato tooyour toogrant. Questa operazione viene eseguita la configurazione e immettendo il certificato al portale Mobile Engagement hello. Assicurarsi di avere ottenuto il certificato con estensione p12 come descritto nella [documentazione di Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Passare portale Mobile Engagement tooyour. Verificare la corretta hello sono quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Fare clic su hello **impostazioni** pagina del portale del progetto. Da scegliere è hello **Push nativo** sezione tooupload il certificato p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Selezionare il certificato p12, caricarlo e digitare la password:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Invia un'app tooyour notifica
Verrà ora creata una semplice campagna di notifica Push che invierà un'app tooour push:

1. Passare toohello **raggiungere** scheda nel portale Mobile Engagement.
2. Fare clic su **nuovo annuncio** toocreate la campagna push
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. I campi prima di hello della campagna del programma di installazione:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Fornire un **Nome** per la campagna 
   * Seleziona hello **l'ora di recapito** come **all'esterno dell'app solo**: si tratta di hello Apple push notification tipo semplice che le funzionalità del testo.
   * Nel testo della notifica hello, digitare hello prima **titolo** che sarà hello nella prima riga push hello.
   * Digitare quindi il **messaggio** che sarà della seconda riga hello
4. Scorrere verso il basso e in hello sezione di contenuto selezionare **sola notifica**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Campagna più elementare di hello impostazione completata. A questo punto, scorrere verso il basso e fare clic su **crea** pulsante toosave la campagna di notifica push. 
6. Infine, fare clic su **attiva** notifica push toosend. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Sarà possibile ricevere una notifica di hello sul dispositivo iOS nell'area di notifica hello hello seguente:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Se si dispone di un Apple Watch associati a questo dispositivo iOS si vedrà notifica hello nel Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

