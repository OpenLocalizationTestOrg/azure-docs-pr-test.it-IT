### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="9b256-101">Configurare un'etichetta di DNS per l'indirizzo IP pubblico hello</span><span class="sxs-lookup"><span data-stu-id="9b256-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="9b256-102">tooconnect toohello, il motore di Database di SQL Server da hello Internet, è consigliabile creare un'etichetta di DNS per l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="9b256-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="9b256-103">È possibile connettersi utilizzando l'indirizzo IP ma hello etichetta DNS crea un Record che è più facile tooidentify e riassunti hello sottostante indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="9b256-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="9b256-104">Le etichette DNS non sono necessari se piano tooonly connettersi a SQL Server toohello istanza hello stessa rete virtuale o solo in locale.</span><span class="sxs-lookup"><span data-stu-id="9b256-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="9b256-105">toocreate un'etichetta di DNS, selezionare innanzitutto **macchine virtuali** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9b256-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="9b256-106">Selezionare la macchina virtuale SQL Server di toobring visualizzarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="9b256-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="9b256-107">Nella panoramica delle macchine virtuali hello, selezionare il **indirizzo IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="9b256-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![indirizzo ip pubblico](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="9b256-109">Nelle proprietà hello all'indirizzo IP pubblico, espandere **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="9b256-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="9b256-110">Immettere un nome per l'etichetta DNS.</span><span class="sxs-lookup"><span data-stu-id="9b256-110">Enter a DNS Label name.</span></span> <span data-ttu-id="9b256-111">Questo nome è un Record che possono essere utilizzati tooconnect tooyour macchina virtuale SQL Server in base al nome anziché in base all'indirizzo IP direttamente.</span><span class="sxs-lookup"><span data-stu-id="9b256-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="9b256-112">Fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9b256-112">Click hello **Save** button.</span></span>

    ![etichetta dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="9b256-114">Connettersi toohello motore di Database da un altro computer</span><span class="sxs-lookup"><span data-stu-id="9b256-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="9b256-115">In un computer connesso toohello internet, aprire SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="9b256-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9b256-116">Se SQL Server Management Studio non è installato, è possibile scaricarlo [qui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="9b256-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="9b256-117">In hello **connettersi tooServer** o **connettersi tooDatabase motore** della finestra di dialogo Modifica hello **nome Server** valore.</span><span class="sxs-lookup"><span data-stu-id="9b256-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="9b256-118">Immettere l'indirizzo IP hello o il nome DNS completo della macchina virtuale hello (determinata nell'attività precedente hello).</span><span class="sxs-lookup"><span data-stu-id="9b256-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="9b256-119">È anche possibile aggiungere una virgola e specificare la porta TCP di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b256-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="9b256-120">ad esempio `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="9b256-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="9b256-121">In hello **autenticazione** , quindi selezionare **autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="9b256-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="9b256-122">In hello **accesso** casella, il nome del tipo hello di un account di accesso SQL valido.</span><span class="sxs-lookup"><span data-stu-id="9b256-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="9b256-123">In hello **Password** casella, digitare la password dell'account di accesso hello hello.</span><span class="sxs-lookup"><span data-stu-id="9b256-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="9b256-124">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="9b256-124">Click **Connect**.</span></span>

    ![connessione a ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)