listener del gruppo di disponibilità di Hello è un indirizzo IP e rete nome che hello in ascolto il gruppo di disponibilità di SQL Server. listener del gruppo di disponibilità hello toocreate, hello seguenti:

1. <a name="getnet"></a>Ottenere il nome della risorsa di rete cluster hello hello.

    a. Utilizzare il protocollo RDP tooconnect toohello macchina virtuale di Azure che ospita la replica primaria hello. 

    b. Aprire Gestione cluster di failover.

    c. Seleziona hello **reti** nodo e nome di rete cluster hello nota. Usare questo nome in hello `$ClusterNetworkName` variabile hello script di PowerShell. In hello dopo il nome di rete cluster hello immagine è **rete Cluster 1**:

   ![Nome rete di cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Aggiungere il punto di accesso client hello.  
    punto di accesso client hello è il nome di rete hello utilizzati dalle applicazioni tooconnect toohello database in un gruppo di disponibilità. Creare il punto di accesso client hello in Gestione Cluster di Failover.

    a. Espandere il nome del cluster hello e quindi fare clic su **ruoli**.

    b. In hello **ruoli** riquadro, gruppo di disponibilità hello rapida nome, quindi fare clic **Aggiungi risorsa** > **punto di accesso Client**.

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. In hello **nome** casella, creare un nome per questo nuovo listener. 
   nome Hello nuovo listener hello è il nome di rete hello utilizzati dalle applicazioni tooconnect toodatabases nel gruppo di disponibilità di SQL Server hello.
   
    d. toofinish la creazione del listener di hello, fare clic su **Avanti** due volte, quindi fare clic su **fine**. Non portare il listener hello o in linea la risorsa a questo punto.

3. <a name="congroup"></a>Configurare la risorsa IP hello per il gruppo di disponibilità hello.

    a. Fare clic su hello **risorse** scheda e quindi espandere punto di accesso client hello creato.  
    punto di accesso client hello è offline.

   ![Punto di accesso client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Fare clic sulla risorsa IP hello e quindi fare clic su proprietà. Si noti il nome di hello dell'indirizzo IP hello e utilizzarlo in hello `$IPResourceName` variabile hello script di PowerShell.

    c. In **Indirizzo IP** fare clic su **Indirizzo IP statico**. Impostare l'indirizzo IP hello hello stesso indirizzi utilizzato quando si imposta l'indirizzo di bilanciamento del carico hello in hello portale di Azure.

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Rendere dipendente nel punto di accesso client hello risorsa hello del gruppo di disponibilità SQL Server.

    a. In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità.

    b. In hello **risorse** scheda **altre risorse**, gruppo di risorse disponibilità hello destro e quindi fare clic su **proprietà**. 

    c. Nella scheda dipendenze hello, aggiungere il nome di hello della risorsa (listener hello) punto di accesso client di hello.

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Fare clic su **OK**.

5. <a name="listname"></a>Rendere l'accesso ai client di hello punto risorsa dipendente dalla risorsa indirizzo IP hello.

    a. In Gestione cluster di failover fare clic su **Ruoli** e quindi sul gruppo di disponibilità. 

    b. In hello **risorse** scheda destro del mouse su risorse di punto di accesso client hello in **nome Server**, quindi fare clic su **proprietà**. 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Fare clic su hello **dipendenze** scheda. Verificare che l'indirizzo IP hello è una dipendenza. In caso contrario, è possibile impostare una dipendenza sull'indirizzo IP hello. Se sono presenti più risorse elencate, verificare che gli indirizzi IP hello OR, not e le dipendenze. Fare clic su **OK**. 

   ![Risorsa IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Il nome del listener hello destro e quindi fare clic su **in linea**. 

    >[!TIP]
    >È possibile convalidare tale hello dipendenze sono configurate correttamente. In Gestione Cluster di Failover, passare tooRoles destro del mouse hello gruppo di disponibilità, fare clic su **altre azioni**, quindi fare clic su **Visualizza rapporto dipendenze**. Quando le dipendenze di hello siano configurate correttamente, il gruppo di disponibilità hello è dipendente dal nome di rete hello e il nome di rete hello è dipendente dalla risorsa indirizzo IP di hello. 


6. <a name="setparam"></a>Impostare i parametri del cluster di hello in PowerShell.
    
    a. Copiare hello seguente tooone script PowerShell di istanze di SQL Server. Aggiornare le variabili di hello per l'ambiente.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Impostare i parametri del cluster di hello eseguendo uno script di PowerShell hello in uno dei nodi del cluster hello.  

    > [!NOTE]
    > Se le istanze di SQL Server sono in aree separate, è necessario uno script di PowerShell hello toorun due volte. Hello prima volta, utilizzare hello `$ILBIP` e `$ProbePort` dall'area prima hello. Hello una seconda volta, utilizzare hello `$ILBIP` e `$ProbePort` dalla seconda area hello. nome di rete cluster Hello e nome della risorsa IP cluster hello sono hello stesso. 
