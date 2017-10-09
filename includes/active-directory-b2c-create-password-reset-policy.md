tooenable accurato la reimpostazione della password nell'applicazione, sarà necessario toocreate un criterio di reimpostazione della password. Si noti che la password a livello di tenant hello Reimposta l'opzione specificata [qui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Questo criterio viene esperienze hello consumer hello passa attraverso durante la reimpostazione della password e verrà visualizzato il contenuto di hello di token che hello applicazione al termine dell'esecuzione.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Nella sezione criteri hello delle impostazioni selezionare **criteri di reimpostazione della Password** e fare clic su **+ Aggiungi**.

![Selezionare i criteri di iscrizione o accesso e fare clic sul pulsante Aggiungi hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Immettere un criterio **nome** per tooreference l'applicazione. Ad esempio, immettere `SSPR`.

Selezionare **Provider di identità** e quindi selezionare **Reimposta la password usando l'indirizzo di posta elettronica**. Fare clic su **OK**.

![Selezionare la reimpostazione della password utilizzando l'indirizzo di posta elettronica come provider di identità e fare clic sul pulsante OK hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Selezionare **Attestazioni dell'applicazione**. Scegliere le attestazioni da includere nel token di autorizzazione hello inviati tooyour indietro applicazione dopo la reimpostazione della password riuscita esperienza. Selezionare ad esempio **ID oggetto dell'utente**.

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Fare clic su **crea** criteri hello tooadd. criteri di Hello sono elencato come **B2C_1_SSPR**. Hello **B2C_1_** prefisso viene aggiunto toohello nome.

Aprire criteri hello selezionando **B2C_1_SSPR**. Verificare le impostazioni di hello specificate nella tabella hello, quindi fare clic su **Esegui**.

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Impostazione      | Valore  |
| ------------ | ------ |
| **Applicazioni** | App Contoso B2C |
| **Selezionare l'URL di risposta** | `https://localhost:44316/` |

Verrà visualizzata una nuova scheda del browser e per verificare l'esperienza utente dell'applicazione di reimpostazione della password hello.

> [!NOTE]
> Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.
>
