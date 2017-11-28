### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="7c652-101">Configurare un'etichetta DNS per l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="7c652-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="7c652-102">Per connettersi al motore di database di SQL Server da Internet, prendere in considerazione la possibilità di configurare un'etichetta DNS per l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="7c652-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="7c652-103">È possibile connettersi tramite l'indirizzo IP, ma l'etichetta DNS crea un record A che è più facile da identificare ed estrae l'indirizzo IP pubblico sottostante.</span><span class="sxs-lookup"><span data-stu-id="7c652-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="7c652-104">Le etichette DNS non sono necessarie se si intende connettersi solo all'istanza di SQL Server presente nella stessa rete virtuale o solo in locale.</span><span class="sxs-lookup"><span data-stu-id="7c652-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="7c652-105">Per creare un'etichetta DNS, selezionare prima di tutto **Macchine virtuali** nel portale.</span><span class="sxs-lookup"><span data-stu-id="7c652-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="7c652-106">Selezionare la propria macchina virtuale di SQL Server per visualizzarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="7c652-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="7c652-107">Nella panoramica della macchina virtuale selezionare l'**indirizzo IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="7c652-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![indirizzo ip pubblico](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="7c652-109">Nelle proprietà dell'indirizzo IP pubblico espandere **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="7c652-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="7c652-110">Immettere un nome per l'etichetta DNS.</span><span class="sxs-lookup"><span data-stu-id="7c652-110">Enter a DNS Label name.</span></span> <span data-ttu-id="7c652-111">Il nome è un record A che consente di connettersi alla macchina virtuale di SQL Server usando il nome, anziché tramite l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="7c652-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="7c652-112">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7c652-112">Click the **Save** button.</span></span>

    ![etichetta dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="7c652-114">Eseguire la connessione al motore di database da un altro computer</span><span class="sxs-lookup"><span data-stu-id="7c652-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="7c652-115">In un computer connesso a Internet aprire SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="7c652-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="7c652-116">Se SQL Server Management Studio non è installato, è possibile scaricarlo [qui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="7c652-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="7c652-117">Nella finestra di dialogo **Connetti al server** o **Connetti al motore di database** modificare il valore di **Nome server**.</span><span class="sxs-lookup"><span data-stu-id="7c652-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="7c652-118">Immettere l'indirizzo IP o il nome DNS completo della macchina virtuale, determinato nell'attività precedente.</span><span class="sxs-lookup"><span data-stu-id="7c652-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="7c652-119">È anche possibile aggiungere una virgola e specificare la porta TCP di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7c652-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="7c652-120">ad esempio `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="7c652-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="7c652-121">Nella casella **Autenticazione** selezionare **Autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7c652-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="7c652-122">Nella casella **Accesso** digitare il nome di un account di accesso SQL valido.</span><span class="sxs-lookup"><span data-stu-id="7c652-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="7c652-123">Nella casella **Password** digitare la password dell'account di accesso.</span><span class="sxs-lookup"><span data-stu-id="7c652-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="7c652-124">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="7c652-124">Click **Connect**.</span></span>

    ![connessione a ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)