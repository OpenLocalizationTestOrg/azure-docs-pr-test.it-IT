<span data-ttu-id="6e5c3-101">Il listener del gruppo di disponibilità è un nome di rete e indirizzo IP sul quale è in ascolto il gruppo di disponibilità di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-101">The availability group listener is an IP address and network name that the SQL Server availability group listens on.</span></span> <span data-ttu-id="6e5c3-102">Per creare il listener del gruppo di disponibilità, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6e5c3-102">To create the availability group listener, do the following:</span></span>

1. <span data-ttu-id="6e5c3-103"><a name="getnet"></a>Ottenere il nome della risorsa della rete del cluster.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-103"><a name="getnet"></a>Get the name of the cluster network resource.</span></span>

    <span data-ttu-id="6e5c3-104">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-104">a.</span></span> <span data-ttu-id="6e5c3-105">Usare RDP per connettersi alla macchina virtuale di Azure che ospita la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-105">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

    <span data-ttu-id="6e5c3-106">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-106">b.</span></span> <span data-ttu-id="6e5c3-107">Aprire Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="6e5c3-108">c.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-108">c.</span></span> <span data-ttu-id="6e5c3-109">Selezionare il nodo **Reti** e annotare il nome di rete del cluster.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-109">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="6e5c3-110">Usare questo nome nella variabile `$ClusterNetworkName` nello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-110">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span> <span data-ttu-id="6e5c3-111">Nell'immagine seguente il nome della rete di cluster è **Cluster Network 1**:</span><span class="sxs-lookup"><span data-stu-id="6e5c3-111">In the following image the cluster network name is **Cluster Network 1**:</span></span>

   ![Nome rete di cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="6e5c3-113"><a name="addcap"></a>Aggiungere il punto di accesso client.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-113"><a name="addcap"></a>Add the client access point.</span></span>  
    <span data-ttu-id="6e5c3-114">Il punto di accesso client è il nome della rete che le applicazioni useranno per connettersi ai database nel gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-114">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="6e5c3-115">Creare il punto di accesso client in Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-115">Create the client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="6e5c3-116">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-116">a.</span></span> <span data-ttu-id="6e5c3-117">Espandere il nome di cluster, quindi fare clic su **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-117">Expand the cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="6e5c3-118">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-118">b.</span></span> <span data-ttu-id="6e5c3-119">Nel pannello **Ruoli** fare clic con il pulsante destro del mouse sul nome del gruppo di disponibilità e quindi scegliere **Aggiungi risorsa** > **Punto di accesso client**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-119">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="6e5c3-121">c.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-121">c.</span></span> <span data-ttu-id="6e5c3-122">Nella casella **Nome** creare un nome per il nuovo listener.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-122">In the **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="6e5c3-123">Il nome del nuovo listener è il nome della rete che le applicazioni useranno per connettersi ai database nel gruppo di disponibilità di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-123">The name for the new listener is the network name that applications use to connect to databases in the SQL Server availability group.</span></span>
   
    <span data-ttu-id="6e5c3-124">d.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-124">d.</span></span> <span data-ttu-id="6e5c3-125">Per completare la creazione del listener, fare clic su **Avanti** due volte e quindi su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="6e5c3-126">Non portare il listener o la risorsa in linea a questo punto.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-126">Do not bring the listener or resource online at this point.</span></span>

3. <span data-ttu-id="6e5c3-127"><a name="congroup"></a>Configurare la risorsa IP per il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-127"><a name="congroup"></a>Configure the IP resource for the availability group.</span></span>

    <span data-ttu-id="6e5c3-128">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-128">a.</span></span> <span data-ttu-id="6e5c3-129">Scegliere la scheda **Risorse** e quindi espandere il punto di accesso client creato.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-129">Click the **Resources** tab, and then expand the client access point you created.</span></span>  
    <span data-ttu-id="6e5c3-130">Il punto di accesso client è offline.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-130">The client access point is offline.</span></span>

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="6e5c3-132">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-132">b.</span></span> <span data-ttu-id="6e5c3-133">Fare clic con il pulsante destro del mouse sulla risorsa IP e quindi scegliere Proprietà.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-133">Right-click the IP resource, and then click properties.</span></span> <span data-ttu-id="6e5c3-134">Annotare il nome dell'indirizzo IP e usarlo nella variabile `$IPResourceName` nello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-134">Note the name of the IP address, and use it in the `$IPResourceName` variable in the PowerShell script.</span></span>

    <span data-ttu-id="6e5c3-135">c.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-135">c.</span></span> <span data-ttu-id="6e5c3-136">In **Indirizzo IP** fare clic su **Indirizzo IP statico**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="6e5c3-137">Impostare l'indirizzo IP sullo stesso indirizzo usato quando è stato impostato l'indirizzo del servizio di bilanciamento del carico nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-137">Set the IP address as the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="6e5c3-139"><a name = "dependencyGroup"></a>Rendere la risorsa del gruppo di disponibilità di SQL Server dipendente dal punto di accesso client.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-139"><a name = "dependencyGroup"></a>Make the SQL Server availability group resource dependent on the client access point.</span></span>

    <span data-ttu-id="6e5c3-140">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-140">a.</span></span> <span data-ttu-id="6e5c3-141">In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="6e5c3-142">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-142">b.</span></span> <span data-ttu-id="6e5c3-143">Nella scheda **Risorse** fare clic con il pulsante destro del mouse sul gruppo di disponibilità in **Altre risorse** e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-143">On the **Resources** tab, under **Other Resources**, right-click the availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="6e5c3-144">c.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-144">c.</span></span> <span data-ttu-id="6e5c3-145">Nella scheda relativa alle dipendenze aggiungere il nome della risorsa del punto di accesso client (listener).</span><span class="sxs-lookup"><span data-stu-id="6e5c3-145">On the dependencies tab, add the name of the client access point (the listener) resource.</span></span>

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="6e5c3-147">d.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-147">d.</span></span> <span data-ttu-id="6e5c3-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-148">Click **OK**.</span></span>

5. <span data-ttu-id="6e5c3-149"><a name="listname"></a>Rendere la risorsa del punto di accesso client dipendente dall'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-149"><a name="listname"></a>Make the client access point resource dependent on the IP address.</span></span>

    <span data-ttu-id="6e5c3-150">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-150">a.</span></span> <span data-ttu-id="6e5c3-151">In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="6e5c3-152">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-152">b.</span></span> <span data-ttu-id="6e5c3-153">Nella scheda **Risorse** fare clic con il pulsante destro del mouse sulla risorsa del punto di accesso client in **Nome server** e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-153">On the **Resources** tab, right-click the client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="6e5c3-155">c.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-155">c.</span></span> <span data-ttu-id="6e5c3-156">Selezionare la scheda **Dipendenze** .</span><span class="sxs-lookup"><span data-stu-id="6e5c3-156">Click the **Dependencies** tab.</span></span> <span data-ttu-id="6e5c3-157">Verificare che l'indirizzo IP sia una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-157">Verify that the IP address is a dependency.</span></span> <span data-ttu-id="6e5c3-158">In caso contrario, impostare una dipendenza sull'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-158">If it is not, set a dependency on the IP address.</span></span> <span data-ttu-id="6e5c3-159">Se sono presenti più risorse elencate, verificare che gli indirizzi abbiano le dipendenze OR, e non quelle AND.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-159">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="6e5c3-160">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-160">Click **OK**.</span></span> 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="6e5c3-162">d.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-162">d.</span></span> <span data-ttu-id="6e5c3-163">Fare clic con il pulsante destro del mouse sul nome del listener e quindi scegliere **Porta online**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-163">Right-click the listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="6e5c3-164">È possibile confermare che le dipendenze sono state configurate correttamente.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-164">You can validate that the dependencies are correctly configured.</span></span> <span data-ttu-id="6e5c3-165">In Gestione cluster di failover passare a Ruoli, fare clic con il pulsante destro del mouse sul gruppo di disponibilità, scegliere **Altre azioni** e infine fare clic su **Visualizza rapporto dipendenze**.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-165">In Failover Cluster Manager, go to Roles, right-click the availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="6e5c3-166">Quando le dipendenze sono configurate correttamente, il gruppo di disponibilità dipende dal nome della rete e il nome della rete dipende dall'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-166">When the dependencies are correctly configured, the availability group is dependent on the network name, and the network name is dependent on the IP address.</span></span> 


6. <span data-ttu-id="6e5c3-167"><a name="setparam"></a>Impostare i parametri del cluster in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-167"><a name="setparam"></a>Set the cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="6e5c3-168">a.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-168">a.</span></span> <span data-ttu-id="6e5c3-169">Copiare lo script di PowerShell seguente in una delle istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-169">Copy the following PowerShell script to one of your SQL Server instances.</span></span> <span data-ttu-id="6e5c3-170">Aggiornare le variabili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-170">Update the variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
    $IPResourceName = "<IPResourceName>" # the IP Address resource name
    $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="6e5c3-171">b.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-171">b.</span></span> <span data-ttu-id="6e5c3-172">Impostare i parametri del cluster eseguendo lo script di PowerShell in uno dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-172">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="6e5c3-173">Se le istanze di SQL Server sono in aree separate, è necessario eseguire lo script di PowerShell due volte.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-173">If your SQL Server instances are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="6e5c3-174">La prima volta usare i parametri `$ILBIP` e `$ProbePort` della prima area.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-174">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="6e5c3-175">La seconda volta usare i parametri `$ILBIP` e `$ProbePort` della seconda area.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-175">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="6e5c3-176">Il nome della rete del cluster e il nome della risorsa IP del cluster coincidono.</span><span class="sxs-lookup"><span data-stu-id="6e5c3-176">The cluster network name and the cluster IP resource name are the same.</span></span> 
