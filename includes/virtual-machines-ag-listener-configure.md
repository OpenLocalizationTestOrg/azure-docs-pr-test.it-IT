<span data-ttu-id="be2bf-101">listener del gruppo di disponibilità di Hello è un indirizzo IP e rete nome che hello in ascolto il gruppo di disponibilità di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="be2bf-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="be2bf-102">listener del gruppo di disponibilità hello toocreate, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="be2bf-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="be2bf-103"><a name="getnet"></a>Ottenere il nome della risorsa di rete cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="be2bf-104">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-104">a.</span></span> <span data-ttu-id="be2bf-105">Utilizzare il protocollo RDP tooconnect toohello macchina virtuale di Azure che ospita la replica primaria hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="be2bf-106">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-106">b.</span></span> <span data-ttu-id="be2bf-107">Aprire Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="be2bf-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="be2bf-108">c.</span><span class="sxs-lookup"><span data-stu-id="be2bf-108">c.</span></span> <span data-ttu-id="be2bf-109">Seleziona hello **reti** nodo e nome di rete cluster hello nota.</span><span class="sxs-lookup"><span data-stu-id="be2bf-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="be2bf-110">Usare questo nome in hello `$ClusterNetworkName` variabile hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2bf-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="be2bf-111">In hello dopo il nome di rete cluster hello immagine è **rete Cluster 1**:</span><span class="sxs-lookup"><span data-stu-id="be2bf-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nome rete di cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="be2bf-113"><a name="addcap"></a>Aggiungere il punto di accesso client hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="be2bf-114">punto di accesso client hello è il nome di rete hello utilizzati dalle applicazioni tooconnect toohello database in un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="be2bf-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="be2bf-115">Creare il punto di accesso client hello in Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="be2bf-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="be2bf-116">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-116">a.</span></span> <span data-ttu-id="be2bf-117">Espandere il nome del cluster hello e quindi fare clic su **ruoli**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="be2bf-118">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-118">b.</span></span> <span data-ttu-id="be2bf-119">In hello **ruoli** riquadro, gruppo di disponibilità hello rapida nome, quindi fare clic **Aggiungi risorsa** > **punto di accesso Client**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="be2bf-121">c.</span><span class="sxs-lookup"><span data-stu-id="be2bf-121">c.</span></span> <span data-ttu-id="be2bf-122">In hello **nome** casella, creare un nome per questo nuovo listener.</span><span class="sxs-lookup"><span data-stu-id="be2bf-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="be2bf-123">nome Hello nuovo listener hello è il nome di rete hello utilizzati dalle applicazioni tooconnect toodatabases nel gruppo di disponibilità di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="be2bf-124">d.</span><span class="sxs-lookup"><span data-stu-id="be2bf-124">d.</span></span> <span data-ttu-id="be2bf-125">toofinish la creazione del listener di hello, fare clic su **Avanti** due volte, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="be2bf-126">Non portare il listener hello o in linea la risorsa a questo punto.</span><span class="sxs-lookup"><span data-stu-id="be2bf-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="be2bf-127"><a name="congroup"></a>Configurare la risorsa IP hello per il gruppo di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="be2bf-128">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-128">a.</span></span> <span data-ttu-id="be2bf-129">Fare clic su hello **risorse** scheda e quindi espandere punto di accesso client hello creato.</span><span class="sxs-lookup"><span data-stu-id="be2bf-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="be2bf-130">punto di accesso client hello è offline.</span><span class="sxs-lookup"><span data-stu-id="be2bf-130">hello client access point is offline.</span></span>

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="be2bf-132">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-132">b.</span></span> <span data-ttu-id="be2bf-133">Fare clic sulla risorsa IP hello e quindi fare clic su proprietà.</span><span class="sxs-lookup"><span data-stu-id="be2bf-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="be2bf-134">Si noti il nome di hello dell'indirizzo IP hello e utilizzarlo in hello `$IPResourceName` variabile hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2bf-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="be2bf-135">c.</span><span class="sxs-lookup"><span data-stu-id="be2bf-135">c.</span></span> <span data-ttu-id="be2bf-136">In **Indirizzo IP** fare clic su **Indirizzo IP statico**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="be2bf-137">Impostare l'indirizzo IP hello hello stesso indirizzi utilizzato quando si imposta l'indirizzo di bilanciamento del carico hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be2bf-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="be2bf-139"><a name = "dependencyGroup"></a>Rendere dipendente nel punto di accesso client hello risorsa hello del gruppo di disponibilità SQL Server.</span><span class="sxs-lookup"><span data-stu-id="be2bf-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="be2bf-140">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-140">a.</span></span> <span data-ttu-id="be2bf-141">In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="be2bf-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="be2bf-142">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-142">b.</span></span> <span data-ttu-id="be2bf-143">In hello **risorse** scheda **altre risorse**, gruppo di risorse disponibilità hello destro e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="be2bf-144">c.</span><span class="sxs-lookup"><span data-stu-id="be2bf-144">c.</span></span> <span data-ttu-id="be2bf-145">Nella scheda dipendenze hello, aggiungere il nome di hello della risorsa (listener hello) punto di accesso client di hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="be2bf-147">d.</span><span class="sxs-lookup"><span data-stu-id="be2bf-147">d.</span></span> <span data-ttu-id="be2bf-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-148">Click **OK**.</span></span>

5. <span data-ttu-id="be2bf-149"><a name="listname"></a>Rendere l'accesso ai client di hello punto risorsa dipendente dalla risorsa indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="be2bf-150">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-150">a.</span></span> <span data-ttu-id="be2bf-151">In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="be2bf-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="be2bf-152">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-152">b.</span></span> <span data-ttu-id="be2bf-153">In hello **risorse** scheda destro del mouse su risorse di punto di accesso client hello in **nome Server**, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="be2bf-155">c.</span><span class="sxs-lookup"><span data-stu-id="be2bf-155">c.</span></span> <span data-ttu-id="be2bf-156">Fare clic su hello **dipendenze** scheda. Verificare che l'indirizzo IP hello è una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="be2bf-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="be2bf-157">In caso contrario, è possibile impostare una dipendenza sull'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="be2bf-158">Se sono presenti più risorse elencate, verificare che gli indirizzi IP hello OR, not e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="be2bf-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="be2bf-159">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-159">Click **OK**.</span></span> 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="be2bf-161">d.</span><span class="sxs-lookup"><span data-stu-id="be2bf-161">d.</span></span> <span data-ttu-id="be2bf-162">Il nome del listener hello destro e quindi fare clic su **in linea**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="be2bf-163">È possibile convalidare tale hello dipendenze sono configurate correttamente.</span><span class="sxs-lookup"><span data-stu-id="be2bf-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="be2bf-164">In Gestione Cluster di Failover, passare tooRoles destro del mouse hello gruppo di disponibilità, fare clic su **altre azioni**, quindi fare clic su **Visualizza rapporto dipendenze**.</span><span class="sxs-lookup"><span data-stu-id="be2bf-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="be2bf-165">Quando le dipendenze di hello siano configurate correttamente, il gruppo di disponibilità hello è dipendente dal nome di rete hello e il nome di rete hello è dipendente dalla risorsa indirizzo IP di hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="be2bf-166"><a name="setparam"></a>Impostare i parametri del cluster di hello in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2bf-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="be2bf-167">a.</span><span class="sxs-lookup"><span data-stu-id="be2bf-167">a.</span></span> <span data-ttu-id="be2bf-168">Copiare hello seguente tooone script PowerShell di istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="be2bf-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="be2bf-169">Aggiornare le variabili di hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="be2bf-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="be2bf-170">b.</span><span class="sxs-lookup"><span data-stu-id="be2bf-170">b.</span></span> <span data-ttu-id="be2bf-171">Impostare i parametri del cluster di hello eseguendo uno script di PowerShell hello in uno dei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="be2bf-172">Se le istanze di SQL Server sono in aree separate, è necessario uno script di PowerShell hello toorun due volte.</span><span class="sxs-lookup"><span data-stu-id="be2bf-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="be2bf-173">Hello prima volta, utilizzare hello `$ILBIP` e `$ProbePort` dall'area prima hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="be2bf-174">Hello una seconda volta, utilizzare hello `$ILBIP` e `$ProbePort` dalla seconda area hello.</span><span class="sxs-lookup"><span data-stu-id="be2bf-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="be2bf-175">nome di rete cluster Hello e nome della risorsa IP cluster hello sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="be2bf-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
