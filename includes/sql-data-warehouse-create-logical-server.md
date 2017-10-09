### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="bd2f8-101">Creare un nuovo server SQL logico in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bd2f8-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="bd2f8-102">Fare clic su **Nuovo**, cercare **server logico** e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![Cercare il server logico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="bd2f8-104">Selezionare **SQL Server (server logico)**.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-104">Select **SQL server (logical server)**</span></span> 

    ![Selezionare il server logico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="bd2f8-106">Fare clic su **crea** tooopen hello nuovo SQL Server (server logico) pannello.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="bd2f8-107"><kbd>![aprire Pannello server logico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![blade server logico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="bd2f8-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="bd2f8-108">Nella casella di testo Nome server del Pannello di SQL Server (server logico) hello, specificare un nome valido per nuovo server logico hello.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="bd2f8-109">Un segno di spunta verde indica che è stato specificato un nome valido.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nuovo nome server](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="bd2f8-111">Hello nome completo per il nuovo server sarà < nome_server >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="bd2f8-112">Nella casella di testo account di accesso amministratore Server hello, specificare un nome utente per l'accesso con autenticazione SQL hello per questo server.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="bd2f8-113">Questo account di accesso è noto come account di accesso dell'entità server hello.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="bd2f8-114">Un segno di spunta verde indica che è stato specificato un nome valido.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![account di accesso amministratore di sql](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="bd2f8-116">In hello **Password** e **Conferma password** caselle di testo, specificare una password per l'account di accesso dell'entità server hello.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="bd2f8-117">Un segno di spunta verde indica che è stata specificata una password valida.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![password amministratore di sql](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="bd2f8-119">Selezionare una sottoscrizione in cui si dispone di autorizzazione toocreate oggetti.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![sottoscrizione](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="bd2f8-121">Nella casella di testo hello risorsa gruppo, selezionare **Crea nuovo** e quindi, nella casella di testo gruppo di risorse hello, fornire un nome valido per hello nuovo gruppo di risorse (è possibile anche utilizzare un gruppo di risorse esistente se è già stato creato uno).</span><span class="sxs-lookup"><span data-stu-id="bd2f8-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="bd2f8-122">Un segno di spunta verde indica che è stato specificato un nome valido.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nuovo gruppo di risorse](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="bd2f8-124">In hello **percorso** casella di testo, selezionare un data center posizione tooyour appropriata, ad esempio "Australia orientale".</span><span class="sxs-lookup"><span data-stu-id="bd2f8-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![località del server](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="bd2f8-126">casella di controllo per Hello **server tooaccess di servizi di azure Consenti** non può essere modificato in questo pannello.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="bd2f8-127">È possibile modificare questa impostazione nel Pannello di hello server firewall.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="bd2f8-128">Per altre informazioni, vedere [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md) (Introduzione alla sicurezza).</span><span class="sxs-lookup"><span data-stu-id="bd2f8-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="bd2f8-129">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="bd2f8-129">Click **Create**.</span></span>

    ![Pulsante Crea](./media/sql-data-warehouse-create-logical-server/create.png)

