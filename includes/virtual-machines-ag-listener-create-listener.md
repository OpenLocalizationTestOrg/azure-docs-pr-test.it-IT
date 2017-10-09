In questo passaggio, creare manualmente listener del gruppo di disponibilità di hello in Gestione Cluster di Failover e SQL Server Management Studio.

1. Aprire Gestione Cluster di Failover dal nodo hello che ospita la replica primaria hello.

2. Seleziona hello **reti** nodo e nome di rete cluster hello nota. Questo nome viene utilizzato nella variabile hello $ClusterNetworkName hello script di PowerShell.

3. Espandere il nome del cluster hello e quindi fare clic su **ruoli**.

4. In hello **ruoli** riquadro, gruppo di disponibilità hello rapida nome, quindi fare clic **Aggiungi risorsa** > **punto di accesso Client**.
   
    ![Aggiungere il punto di accesso client per il gruppo di disponibilità](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. In hello **nome** creare un nome per questo nuovo listener, fare clic su **Avanti** due volte, quindi fare clic su **fine**.  
    Non portare il listener hello o in linea la risorsa a questo punto.

6. Fare clic su hello **risorse** scheda e quindi espandere punto di accesso client hello appena creato. 
    viene visualizzata la risorsa indirizzo IP Hello per ogni rete di cluster nel cluster. Se si tratta di una soluzione solo per Azure, viene visualizzata solo una risorsa indirizzo IP.

7. Effettuare una delle seguenti hello:
   
   * una soluzione ibrida tooconfigure:
     
        a. Risorsa di indirizzo IP hello corrispondente alla subnet locale tooyour e quindi scegliere **proprietà**. Si noti il nome di indirizzo IP hello e nome di rete.
   
        b. Selezionare **Indirizzo IP statico**, assegnare un indirizzo IP non usato e quindi fare clic su **OK**.
 
   * tooconfigure una soluzione solo Azure:

        a. Risorsa di indirizzo IP hello corrispondente tooyour subnet di Azure e quindi scegliere **proprietà**.
       
       > [!NOTE]
       > Se il listener hello non riesce toocome online a causa di un indirizzo IP in conflitto selezionato da DHCP, è possibile configurare un indirizzo IP statico valido in questa finestra delle proprietà.
       > 
       > 

       b. In hello stesso **indirizzo IP** finestra Proprietà, modifica hello **nome indirizzo IP**.  
        Questo nome viene utilizzato nella variabile hello $IPResourceName di hello script di PowerShell. Se la soluzione si estende in più reti virtuali di Azure, ripetere questo passaggio per ogni risorsa IP.

