profilo tooenable modifica sull'applicazione, sarà necessario toocreate un modifica dei criteri del profilo. Questo criterio viene esperienze hello consumer passerà tramite durante il contenuto di modifica e hello profilo di token che un'applicazione hello riceverà il corretto completamento.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Nella sezione criteri hello delle impostazioni selezionare **modifica i criteri del profilo** e fare clic su **+ Aggiungi**.

![Selezionare i criteri di modifica del profilo e fare clic sul pulsante Aggiungi hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Immettere un criterio **nome** per tooreference l'applicazione. Ad esempio, immettere `SiPe`.

Selezionare **Provider di identità** e quindi selezionare**Accesso all'account locale**. Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati. Fare clic su **OK**.

![Selezionare Signin Account locale come provider di identità e fare clic sul pulsante OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Selezionare **Attributi del profilo**. Scegliere di visualizzare e modificare nel loro profilo consumer hello attributi. Selezionare ad esempio **Paese/area geografica**, **Nome visualizzato** e **Codice postale**. Fare clic su **OK**.

![Selezionare alcuni attributi e fare clic sul pulsante OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Selezionare **Attestazioni dell'applicazione**. Scegliere le attestazioni da includere nel token di autorizzazione hello inviati applicazione back-tooyour dopo un profilo di esito positivo di un'esperienza di modifica. Selezionare ad esempio **Nome visualizzato** e **Codice postale**.

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Fare clic su **crea** criteri hello tooadd. criteri di Hello sono elencato come **B2C_1_SiPe**. Hello **B2C_1_** prefisso viene aggiunto toohello nome.

Aprire criteri hello selezionando **B2C_1_SiPe**. Verificare le impostazioni di hello specificate nella tabella hello, quindi fare clic su **Esegui**.

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Impostazione      | Valore  |
| ------------ | ------ |
| **Applicazioni** | App Contoso B2C |
| **Selezionare l'URL di risposta** | `https://localhost:44316/` |

Verrà visualizzata una nuova scheda del browser e si può verificare il profilo di hello consumer esperienza di modifica, come configurato.

> [!NOTE]
> Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.
>