1. <span data-ttu-id="cb05e-101">Accesso toohello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="cb05e-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="cb05e-102">Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **Enterprise Integration**, quindi fare clic su **inoltro**.</span><span class="sxs-lookup"><span data-stu-id="cb05e-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="cb05e-103">In hello **Crea spazio dei nomi** finestra di dialogo immettere un nome di spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="cb05e-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="cb05e-104">sistema di Hello controlla immediatamente toosee se nome hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="cb05e-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="cb05e-105">In hello **sottoscrizione** campo, scegliere una sottoscrizione di Azure in cui lo spazio dei nomi di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="cb05e-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="cb05e-106">In hello  **[gruppo di risorse](../articles/azure-resource-manager/resource-group-portal.md)**  selezionare un gruppo di risorse esistente in cui hello dello spazio dei nomi in tempo reale oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="cb05e-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="cb05e-107">In **percorso**, scegliere hello paese in cui lo spazio dei nomi deve essere ospitato.</span><span class="sxs-lookup"><span data-stu-id="cb05e-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Crea spazio dei nomi][create-namespace]
7. <span data-ttu-id="cb05e-109">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cb05e-109">Click **Create**.</span></span> <span data-ttu-id="cb05e-110">sistema Hello ora crea uno spazio dei nomi e viene abilitato.</span><span class="sxs-lookup"><span data-stu-id="cb05e-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="cb05e-111">Dopo alcuni minuti, hello risorse di sistema esegue il provisioning per l'account.</span><span class="sxs-lookup"><span data-stu-id="cb05e-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="cb05e-112">Ottenere le credenziali di gestione di hello</span><span class="sxs-lookup"><span data-stu-id="cb05e-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="cb05e-113">Nell'elenco di hello degli spazi dei nomi, fare clic su hello appena creato il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="cb05e-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="cb05e-114">Nel Pannello di hello dello spazio dei nomi, fare clic su **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="cb05e-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="cb05e-115">In hello **criteri di accesso condiviso** pannello, fare clic su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="cb05e-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="cb05e-117">In hello **criteri: RootManageSharedAccessKey** pannello, fare clic su pulsante Copia hello Avanti troppo**chiave – primario di stringa di connessione**, negli Appunti toocopy hello connessione stringa tooyour per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="cb05e-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="cb05e-118">Incollare questo valore nel Blocco note o in un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="cb05e-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="cb05e-120">Passaggio precedente hello ripetizione, copiare e incollare il valore di hello di **chiave primaria** tooa percorso temporaneo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="cb05e-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
