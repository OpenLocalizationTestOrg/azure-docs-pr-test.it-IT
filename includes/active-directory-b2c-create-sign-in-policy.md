Accedi tooenable sull'applicazione, sarà necessario toocreate sign-in criteri. Questo criterio descrive esperienze hello consumer passa attraverso durante l'accesso e verrà visualizzato il contenuto di hello di token che l'applicazione hello accessi ha esito positivo.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)] Fare clic su **Criteri di accesso**.

Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.

Hello **nome** determina il nome di accesso criteri hello utilizzato dall'applicazione. Immettere ad esempio **SiIn**.

Fare clic su **Provider di identità** e selezionare **Accesso all'account locale**. Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati. Fare clic su **OK**.

Fare clic su **Attestazioni applicazione**. Consente di scegliere le attestazioni che si desidera vengano restituite nei token hello inviati applicazione back-tooyour dopo un'esperienza di accesso ha esito positivo. Selezionare ad esempio **Nome visualizzato**, **Provider di identità**, **Codice postale** e **ID oggetto dell'utente**. Fare clic su **OK**.

Fare clic su **Crea**. Si noti che il criterio di hello appena creato viene visualizzato come **B2C_1_SiIn** (hello **B2C\_1\_**  frammento viene aggiunta automaticamente) in hello **criteri di accesso**blade.

Aprire criteri hello facendo **B2C_1_SiIn**.

Selezionare **Contoso B2C app** in hello **applicazioni** elenco a discesa e `https://localhost:44321/` in hello **URL di risposta / URI di reindirizzamento** elenco a discesa.

Fare clic su **Esegui adesso**. Apre una nuova scheda del browser e sarà possibile eseguire mediante l'esperienza utente hello di firma nell'applicazione.

> [!NOTE]
> Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.
>