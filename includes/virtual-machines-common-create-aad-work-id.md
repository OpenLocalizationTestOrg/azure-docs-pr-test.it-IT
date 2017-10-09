
<br>

> [!NOTE]
> <span data-ttu-id="600f3-101">Se si sono ricevuti un nome utente e una password da un amministratore, è probabile che si abbia già un ID aziendale o dell’istituto d’istruzione (a volte detto anche *ID dell’organizzazione*).</span><span class="sxs-lookup"><span data-stu-id="600f3-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="600f3-102">In questo caso, è possibile iniziare immediatamente toouse il tooaccess account Azure, le risorse di Azure che richiedono uno.</span><span class="sxs-lookup"><span data-stu-id="600f3-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="600f3-103">Se si ritiene che non è possibile utilizzare tali risorse, potrebbe essere tooreturn toothis articolo per la Guida.</span><span class="sxs-lookup"><span data-stu-id="600f3-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="600f3-104">Per ulteriori informazioni, vedere [gli account che è possibile utilizzare per l'accesso](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [sottoscrizione di Azure è tooAzure correlati AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="600f3-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="600f3-105">passaggi di Hello sono semplici.</span><span class="sxs-lookup"><span data-stu-id="600f3-105">hello steps are simple.</span></span> <span data-ttu-id="600f3-106">È necessario toolocate accesso sull'identità nel portale di Azure classico hello, individuare il dominio di Azure Active Directory predefinito e aggiungere un nuovo tooit utente come co-amministratore Azure.</span><span class="sxs-lookup"><span data-stu-id="600f3-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="600f3-107">Individuare la directory predefinita nel portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="600f3-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="600f3-108">Avviare accedendo toohello [portale di Azure classico](https://manage.windowsazure.com) con l'identità dell'account Microsoft personale.</span><span class="sxs-lookup"><span data-stu-id="600f3-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="600f3-109">Dopo che sono connessi, scorrere verso il basso il pannello di hello blu sul lato sinistro hello e fare clic su **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="600f3-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="600f3-111">Occorre innanzitutto trovare alcuni informazioni sulla propria identità in Azure.</span><span class="sxs-lookup"><span data-stu-id="600f3-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="600f3-112">Dovrebbe essere simile al seguente hello seguente nel riquadro principale hello, che mostra la presenza di una directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="600f3-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="600f3-113">È possibile cercare altre informazioni sulla directory</span><span class="sxs-lookup"><span data-stu-id="600f3-113">Let's find out some more information about it.</span></span> <span data-ttu-id="600f3-114">Fare clic sulla riga directory predefinita hello, che consente di nelle proprietà di directory predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="600f3-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="600f3-115">nome di dominio predefinito hello tooview, fare clic su **domini**.</span><span class="sxs-lookup"><span data-stu-id="600f3-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="600f3-116">In questo caso dovrebbe essere in grado di toosee quando è stato creato hello account Azure, Azure Active Directory creato un dominio personale predefinito che è un valore hash (un numero generato da una stringa di testo) dell'ID personale utilizzato come un sottodominio di c o m. Ovvero hello dominio toowhich questo punto si aggiungerà un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="600f3-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="600f3-117">Creazione di un nuovo utente nel dominio predefinito hello</span><span class="sxs-lookup"><span data-stu-id="600f3-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="600f3-118">Fare clic su **UTENTI** e cercare il proprio account personale.</span><span class="sxs-lookup"><span data-stu-id="600f3-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="600f3-119">Dovrebbe essere in hello **originato da** colonna che si tratta di un **account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="600f3-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="600f3-120">Vogliamo toocreate un utente nel predefinito. c o m dominio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="600f3-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="600f3-121">Stiamo toofollow [queste istruzioni](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello passaggi successivi, ma utilizzare un esempio specifico.</span><span class="sxs-lookup"><span data-stu-id="600f3-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="600f3-122">Nella parte inferiore di hello della pagina hello, fare clic su **+ Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="600f3-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="600f3-123">Nella pagina hello che viene visualizzato, digitare nome utente hello e apportare hello **tipo di utente** un **nuovo utente nell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="600f3-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="600f3-124">In questo esempio, nuovo nome utente di hello è `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="600f3-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="600f3-125">Selezionare dominio predefinito hello che è stato individuato in precedenza come dominio hello indirizzo dell'ahmet di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="600f3-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="600f3-126">Fare clic sulla freccia avanti di hello al termine.</span><span class="sxs-lookup"><span data-stu-id="600f3-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="600f3-127">Aggiungere ulteriori dettagli per Ahmet, ma assicurarsi che tooselect hello appropriato **ruolo** valore.</span><span class="sxs-lookup"><span data-stu-id="600f3-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="600f3-128">È facile toouse **amministratore globale** toomake che tutto funzioni, ma se è possibile utilizzare un ruolo inferiore, che è una buona idea.</span><span class="sxs-lookup"><span data-stu-id="600f3-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="600f3-129">Questo esempio viene utilizzato hello **utente** ruolo.</span><span class="sxs-lookup"><span data-stu-id="600f3-129">This example uses hello **User** role.</span></span> <span data-ttu-id="600f3-130">Per altre informazioni, vedere le [autorizzazioni degli amministratori in base al ruolo](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1). Non abilitare l'autenticazione a più fattori a meno che non si desidera toouse autenticazione a più fattori per ogni log nell'operazione.</span><span class="sxs-lookup"><span data-stu-id="600f3-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="600f3-131">Al termine, fare clic sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="600f3-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="600f3-132">Fare clic su hello **creare** pulsante toogenerate e visualizzare una password temporanea per Ahmet.</span><span class="sxs-lookup"><span data-stu-id="600f3-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="600f3-133">Copiare l'indirizzo di posta elettronica di nome utente hello o utilizzare **invia PASSWORD IN messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="600f3-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="600f3-134">Sarà necessario toolog informazioni hello in a breve.</span><span class="sxs-lookup"><span data-stu-id="600f3-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="600f3-135">Ora verrà visualizzato un nuovo utente hello, **Ahmet hello Developer**, origine da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="600f3-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="600f3-136">Si è creato un nuovo lavoro hello o identità dell'istituto di istruzione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="600f3-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="600f3-137">Tuttavia, questa identità non dispone ancora di autorizzazioni toouse Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="600f3-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="600f3-138">Se si utilizza **invia PASSWORD IN messaggio di posta elettronica**, hello seguente tipo di messaggio di posta elettronica viene inviato.</span><span class="sxs-lookup"><span data-stu-id="600f3-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="600f3-139">Aggiunta di diritti di co-amministratore di Azure per le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="600f3-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="600f3-140">A questo punto è necessario tooadd hello nuovo utente come coamministratore della sottoscrizione in modo hello nuovo utente possa accedere toohello portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="600f3-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="600f3-141">Questa operazione, nel Pannello di hello in basso a sinistra fare clic su toodo **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="600f3-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="600f3-142">Nell'area Impostazioni principali hello, fare clic su **amministratori** in hello superiore e si dovrebbe essere solo della tua identità di account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="600f3-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="600f3-143">Nella parte inferiore di hello della pagina hello, fare clic su **+ Aggiungi** toospecify un coamministratore.</span><span class="sxs-lookup"><span data-stu-id="600f3-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="600f3-144">In questo caso, immettere indirizzo di posta elettronica hello del nuovo utente hello che è stato creato, inclusi il dominio predefinito.</span><span class="sxs-lookup"><span data-stu-id="600f3-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="600f3-145">Come illustrato nella schermata successiva di hello, un segno di spunta verde viene visualizzata utente toohello successivo per la directory predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="600f3-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="600f3-146">Ricordare tooselect tutte le sottoscrizioni di hello che si desidera tooadminister in grado di toobe questo utente.</span><span class="sxs-lookup"><span data-stu-id="600f3-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="600f3-147">Al termine dovrebbero essere visibili due utenti, tra cui la nuova identità di co-amministratore.</span><span class="sxs-lookup"><span data-stu-id="600f3-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="600f3-148">Disconnettersi da portale hello.</span><span class="sxs-lookup"><span data-stu-id="600f3-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="600f3-149">Accesso e modifica password hello del nuovo utente</span><span class="sxs-lookup"><span data-stu-id="600f3-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="600f3-150">Accedere come nuovo utente creato hello.</span><span class="sxs-lookup"><span data-stu-id="600f3-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="600f3-151">Sarà immediatamente toocreate richiesta una nuova password.</span><span class="sxs-lookup"><span data-stu-id="600f3-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="600f3-152">Deve essere ricompensati con esito positivo simile hello seguente.</span><span class="sxs-lookup"><span data-stu-id="600f3-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="600f3-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="600f3-153">Next steps</span></span>
<span data-ttu-id="600f3-154">È ora possibile usare il nuovo toouse identità Azure Active Directory [modelli gruppo di risorse di Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="600f3-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
