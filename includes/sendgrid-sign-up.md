I clienti di Azure possono sbloccare 25.000 messaggi di posta elettronica gratuiti ogni mese. Questi messaggi mensili gratuiti 25.000 offrirà accesso tooadvanced reporting e analitica e [tutte le API] [ all APIs] (Web, SMTP, evento, l'analisi e informazioni). Per informazioni sui servizi aggiuntivi forniti da SendGrid, visitare hello [SendGrid soluzioni] [ SendGrid Solutions] pagina.

### <a name="toosign-up-for-a-sendgrid-account"></a>toosign a un account di SendGrid
1. Accedi toohello [il portale di gestione di Azure][Azure Management Portal].
2. Dal menu hello hello sinistra, fare clic su **New**.

    ![command-bar-new][command-bar-new]
3. Fare clic su **Componenti aggiuntivi** e quindi **SendGrid Email Delivery** (Recapito email di SendGrid).

    ![sendgrid-store][sendgrid-store]
4. Completare il modulo di iscrizione hello e selezionare **crea**.

    ![creazione di SendGrid][sendgrid-create]
5. Immettere un **nome** tooidentify il SendGrid servizio nelle impostazioni di Azure. I nomi devono essere composti da un numero di caratteri compreso tra 1 e 100 e possono includere solo caratteri alfanumerici, trattini, punti e caratteri di sottolineatura. nome Hello deve essere univoco nell'elenco di elementi di archivio Azure sottoscritti.
6. Immettere e confermare la **password**.
7. Scegliere la propria **sottoscrizione**.
8. Creare un nuovo **gruppo di risorse** o selezionarne uno esistente.
9. In hello **tariffario** sezione selezionare il piano di SendGrid hello da toosign per.

    ![prezzi di SendGrid][sendgrid-pricing]
10. Se disponibile, immettere un **codice di promozione**.
11. Inserire le **informazioni di contatto**.
12. Leggere e accettare hello **legali**.
13. Dopo aver confermato l'acquisto verrà visualizzato un **distribuzione ha avuto esito positivo** popup e si verrà visualizzato l'account elencato nella hello **tutte le risorse** sezione.

    ![all-resources][all-resources]

    Dopo aver completato l'acquisto e fa clic su hello **Gestisci** processo di verifica tramite posta elettronica hello tooinitiate pulsante, si riceverà un messaggio di posta elettronica da cui si chiede tooverify SendGrid l'account. Se non si riceve questa email o se si hanno problemi nella verifica dell'account, consultare le domande frequenti.

    ![manage][manage]

    **È possibile solo inviare i messaggi di posta elettronica too100/giorno fino a quando non significa che l'account.**

    toomodify il piano della sottoscrizione o vedere hello impostazioni contatto di SendGrid, fare clic sul nome hello di hello di tooopen il servizio SendGrid dashboard di SendGrid Marketplace.

    ![Impostazioni][settings]

    toosend un messaggio di posta elettronica usando SendGrid, è necessario fornire la chiave API.

### <a name="toofind-your-sendgrid-api-key"></a>toofind la chiave API SendGrid
1. Fare clic su **Manage**.

    ![manage][manage]
2. Nel dashboard di SendGrid, selezionare **impostazioni** e quindi **chiavi API** menu hello in hello sinistra.

    ![chiavi API][api-keys]

3. Fare clic su hello **creare la chiave API** elenco a discesa e selezionare **chiave API generale**.

    ![chiave API generale][general-api-key]
4. Come minimo, fornire hello **nome di questa chiave** e fornire l'accesso completo troppo**inviare posta elettronica** e selezionare **salvare**.

    ![access][access]
5. L'API verrà visualizzata una sola volta a questo punto. Essere toostore che, in modo sicuro.

### <a name="toofind-your-sendgrid-credentials"></a>toofind le credenziali SendGrid
1. Fare clic su hello icona chiave toofind il **Username**.

    ![key][key]
2. password Hello è hello scelta effettuata al momento dell'installazione. È possibile selezionare **Cambia password** o **reimpostazione password** toomake tutte le modifiche.

toomanage le impostazioni di distribuzione di posta elettronica, fare clic su hello **pulsante Gestione**. Si verrà reindirizzati tooyour dashboard di SendGrid.

    ![manage][manage]

    For more information on sending email through SendGrid, visit hello [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure Management Portal]: https://manage.windowsazure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
