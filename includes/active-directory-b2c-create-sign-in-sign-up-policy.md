Accedi tooenable sull'applicazione, sarà necessario toocreate sign-in criteri. Questo criterio descrive esperienze hello consumer passa attraverso durante l'accesso e verrà visualizzato il contenuto di hello di token che l'applicazione hello accessi ha esito positivo.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Nella sezione criteri hello delle impostazioni selezionare **iscrizione o accesso criteri** e fare clic su **+ Aggiungi**.

![Selezionare i criteri di iscrizione o di accesso e fare clic sul pulsante Aggiungi](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Immettere un criterio **nome** per tooreference l'applicazione. Ad esempio, immettere `SiUpIn`.

Selezionare **Provider di identità** e quindi selezionare **Iscrizione posta elettronica**. Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati. Fare clic su **OK**.

![Selezionare l'iscrizione di posta elettronica come provider di identità e fare clic sul pulsante OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Selezionare **Attributi di iscrizione**. Scegliere gli attributi desiderati toocollect consumer hello durante l'iscrizione. Selezionare ad esempio **Paese/area geografica**, **Nome visualizzato** e **Codice postale**. Fare clic su **OK**.

![Selezionare alcuni attributi e fare clic sul pulsante OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Selezionare **Attestazioni dell'applicazione**. Scegliere le attestazioni da includere nel token di autorizzazione hello inviati applicazione back-tooyour dopo un'esperienza di iscrizione o accesso ha esito positivo. Selezionare ad esempio **Nome visualizzato**, **Provider di identità**, **Codice postale**, **Nuovo utente** e **ID oggetto dell'utente**.

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Fare clic su **crea** criteri hello tooadd. criteri di Hello sono elencato come **B2C_1_SiUpIn**. Hello **B2C_1_** prefisso viene aggiunto toohello nome.

Aprire criteri hello selezionando **B2C_1_SiUpIn**. Verificare le impostazioni di hello specificate nella tabella hello, quindi fare clic su **Esegui**.

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Impostazione      | Valore  |
| ------------ | ------ |
| **Applicazioni** | App Contoso B2C |
| **Selezionare l'URL di risposta** | `https://localhost:44316/` |

Verrà visualizzata una nuova scheda del browser, ed è possibile verificare l'esperienza di iscrizione o accesso consumer hello come configurato.

> [!NOTE]
> Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.
>