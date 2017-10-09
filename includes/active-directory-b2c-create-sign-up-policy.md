tooenable iscrizione sull'applicazione, è necessario toocreate un criterio di iscrizione. Questo criterio descrive esperienze hello consumer scorrere durante l'iscrizione e riceve il contenuto di hello di token che l'applicazione hello iscrizioni ha esito positivo.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Fare clic su **Criteri di iscrizione**.

Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.

Hello **nome** determina il nome di criterio iscrizione hello utilizzato dall'applicazione. Immettere ad esempio **SiUp**.

Fare clic su **Provider di identità** e selezionare **Iscrizione posta elettronica**. Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati. Fare clic su **OK**.

Fare clic su **Attributi iscrizione**. Consente di scegliere gli attributi che si desidera toocollect consumer hello durante l'iscrizione. Selezionare ad esempio **Paese/Area**, **Nome visualizzato** e **Codice postale**. Fare clic su **OK**.

Fare clic su **Attestazioni applicazione**. Consente di scegliere le attestazioni che si desidera vengano restituite nei token hello inviati applicazione back-tooyour dopo un'esperienza di iscrizione ha esito positivo. Selezionare ad esempio **Nome visualizzato**, **Provider di identità**, **Codice postale**, **L'utente è nuovo** e l'**ID oggetto dell'utente**.

Fare clic su **Crea**. criterio Hello creato viene visualizzato come **B2C_1_SiUp** (hello **B2C\_1\_**  frammento viene aggiunta automaticamente) in hello **criteri iscrizione** blade.

Aprire criteri hello facendo **B2C_1_SiUp**.

Selezionare **Contoso B2C app** in hello **applicazioni** elenco a discesa e `https://localhost:44321/` in hello **URL di risposta / URI di reindirizzamento** elenco a discesa.

Fare clic su **Esegui adesso**. Verrà visualizzata una nuova scheda del browser e sarà possibile eseguire mediante l'esperienza utente hello di effettuare l'iscrizione per l'applicazione.

> [!NOTE]
> Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.
>