### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Creare un nuovo server SQL logico in hello portale di Azure

1. Fare clic su **Nuovo**, cercare **server logico** e quindi premere **INVIO**.

    ![Cercare il server logico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Selezionare **SQL Server (server logico)**. 

    ![Selezionare il server logico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Fare clic su **crea** tooopen hello nuovo SQL Server (server logico) pannello.

   <kbd>![aprire Pannello server logico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![blade server logico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Nella casella di testo Nome server del Pannello di SQL Server (server logico) hello, specificare un nome valido per nuovo server logico hello. Un segno di spunta verde indica che è stato specificato un nome valido.
    
    ![nuovo nome server](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Hello nome completo per il nuovo server sarà < nome_server >. database.windows.net.
    >
    
4. Nella casella di testo account di accesso amministratore Server hello, specificare un nome utente per l'accesso con autenticazione SQL hello per questo server. Questo account di accesso è noto come account di accesso dell'entità server hello. Un segno di spunta verde indica che è stato specificato un nome valido.
    
    ![account di accesso amministratore di sql](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. In hello **Password** e **Conferma password** caselle di testo, specificare una password per l'account di accesso dell'entità server hello. Un segno di spunta verde indica che è stata specificata una password valida.
    
    ![password amministratore di sql](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Selezionare una sottoscrizione in cui si dispone di autorizzazione toocreate oggetti.

    ![sottoscrizione](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Nella casella di testo hello risorsa gruppo, selezionare **Crea nuovo** e quindi, nella casella di testo gruppo di risorse hello, fornire un nome valido per hello nuovo gruppo di risorse (è possibile anche utilizzare un gruppo di risorse esistente se è già stato creato uno). Un segno di spunta verde indica che è stato specificato un nome valido.

    ![nuovo gruppo di risorse](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. In hello **percorso** casella di testo, selezionare un data center posizione tooyour appropriata, ad esempio "Australia orientale".
    
    ![località del server](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > casella di controllo per Hello **server tooaccess di servizi di azure Consenti** non può essere modificato in questo pannello. È possibile modificare questa impostazione nel Pannello di hello server firewall. Per altre informazioni, vedere [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md) (Introduzione alla sicurezza).
    >
    
9. Fare clic su **Create**.

    ![Pulsante Crea](./media/sql-data-warehouse-create-logical-server/create.png)

