<span data-ttu-id="5099b-101">utilizzo di Service Bus toobegin le code in Azure, è innanzitutto necessario creare uno spazio dei nomi con un nome univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="5099b-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="5099b-102">Uno spazio dei nomi fornisce un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5099b-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="5099b-103">toocreate uno spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="5099b-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="5099b-104">Accesso toohello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5099b-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="5099b-105">Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **Enterprise Integration**, quindi fare clic su **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="5099b-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="5099b-106">In hello **Crea spazio dei nomi** finestra di dialogo immettere un nome di spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5099b-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="5099b-107">sistema di Hello controlla immediatamente toosee se nome hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="5099b-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="5099b-108">Dopo il nome di spazio dei nomi che hello è disponibile, scegliere hello tariffario (Basic, Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="5099b-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="5099b-109">In hello **sottoscrizione** campo, scegliere una sottoscrizione di Azure in cui lo spazio dei nomi di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5099b-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="5099b-110">In hello **gruppo di risorse** selezionare un gruppo di risorse esistente in cui hello dello spazio dei nomi in tempo reale oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="5099b-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="5099b-111">In **percorso**, scegliere hello paese in cui lo spazio dei nomi deve essere ospitato.</span><span class="sxs-lookup"><span data-stu-id="5099b-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Crea spazio dei nomi][create-namespace]
8. <span data-ttu-id="5099b-113">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5099b-113">Click **Create**.</span></span> <span data-ttu-id="5099b-114">sistema Hello ora crea uno spazio dei nomi e viene abilitato.</span><span class="sxs-lookup"><span data-stu-id="5099b-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="5099b-115">Potrebbe essere toowait alcuni minuti per le risorse di hello sistema esegue il provisioning per l'account.</span><span class="sxs-lookup"><span data-stu-id="5099b-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="5099b-116">Ottenere le credenziali di gestione di hello</span><span class="sxs-lookup"><span data-stu-id="5099b-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="5099b-117">Nell'elenco di hello degli spazi dei nomi, fare clic su hello appena creato il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5099b-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="5099b-118">Nel Pannello di hello dello spazio dei nomi, fare clic su **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="5099b-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="5099b-119">In hello **criteri di accesso condiviso** pannello, fare clic su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5099b-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="5099b-121">In hello **criteri: RootManageSharedAccessKey** pannello, fare clic su pulsante Copia hello Avanti troppo**chiave – primario di stringa di connessione**, negli Appunti toocopy hello connessione stringa tooyour per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="5099b-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="5099b-122">Incollare questo valore nel Blocco note o in un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="5099b-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="5099b-124">Passaggio precedente hello ripetizione, copiare e incollare il valore di hello di **chiave primaria** tooa percorso temporaneo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="5099b-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
