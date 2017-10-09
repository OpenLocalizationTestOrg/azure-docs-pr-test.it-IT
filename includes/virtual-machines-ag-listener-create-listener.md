<span data-ttu-id="d7eb5-101">In questo passaggio, creare manualmente listener del gruppo di disponibilità di hello in Gestione Cluster di Failover e SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="d7eb5-102">Aprire Gestione Cluster di Failover dal nodo hello che ospita la replica primaria hello.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="d7eb5-103">Seleziona hello **reti** nodo e nome di rete cluster hello nota.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="d7eb5-104">Questo nome viene utilizzato nella variabile hello $ClusterNetworkName hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="d7eb5-105">Espandere il nome del cluster hello e quindi fare clic su **ruoli**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="d7eb5-106">In hello **ruoli** riquadro, gruppo di disponibilità hello rapida nome, quindi fare clic **Aggiungi risorsa** > **punto di accesso Client**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Aggiungere il punto di accesso client per il gruppo di disponibilità](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="d7eb5-108">In hello **nome** creare un nome per questo nuovo listener, fare clic su **Avanti** due volte, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="d7eb5-109">Non portare il listener hello o in linea la risorsa a questo punto.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="d7eb5-110">Fare clic su hello **risorse** scheda e quindi espandere punto di accesso client hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="d7eb5-111">viene visualizzata la risorsa indirizzo IP Hello per ogni rete di cluster nel cluster.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="d7eb5-112">Se si tratta di una soluzione solo per Azure, viene visualizzata solo una risorsa indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="d7eb5-113">Effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d7eb5-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="d7eb5-114">una soluzione ibrida tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="d7eb5-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="d7eb5-115">a.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-115">a.</span></span> <span data-ttu-id="d7eb5-116">Risorsa di indirizzo IP hello corrispondente alla subnet locale tooyour e quindi scegliere **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="d7eb5-117">Si noti il nome di indirizzo IP hello e nome di rete.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="d7eb5-118">b.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-118">b.</span></span> <span data-ttu-id="d7eb5-119">Selezionare **Indirizzo IP statico**, assegnare un indirizzo IP non usato e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="d7eb5-120">tooconfigure una soluzione solo Azure:</span><span class="sxs-lookup"><span data-stu-id="d7eb5-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="d7eb5-121">a.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-121">a.</span></span> <span data-ttu-id="d7eb5-122">Risorsa di indirizzo IP hello corrispondente tooyour subnet di Azure e quindi scegliere **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="d7eb5-123">Se il listener hello non riesce toocome online a causa di un indirizzo IP in conflitto selezionato da DHCP, è possibile configurare un indirizzo IP statico valido in questa finestra delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="d7eb5-124">b.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-124">b.</span></span> <span data-ttu-id="d7eb5-125">In hello stesso **indirizzo IP** finestra Proprietà, modifica hello **nome indirizzo IP**.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="d7eb5-126">Questo nome viene utilizzato nella variabile hello $IPResourceName di hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="d7eb5-127">Se la soluzione si estende in più reti virtuali di Azure, ripetere questo passaggio per ogni risorsa IP.</span><span class="sxs-lookup"><span data-stu-id="d7eb5-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

