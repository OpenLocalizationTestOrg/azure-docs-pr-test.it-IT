## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Come toocreate una rete virtuale classica in hello portale di Azure
toocreate una rete virtuale classica, basata su scenario hello precedente, seguire i passaggi di hello seguenti.

1. Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.
2. Fare clic su **NEW** > **rete** > **rete virtuale**, si noti che hello **selezionare un modello di distribuzione** elenco già illustrato **classico**, quindi fare clic su **crea**, come illustrato nella figura che segue hello.
   
    ![Creare reti virtuali nel portale di Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. In hello **rete virtuale** blade, hello tipo **nome** di hello rete virtuale e quindi fare clic su **lo spazio degli indirizzi**. Configurare le impostazioni dello spazio di indirizzi per hello rete virtuale e la prima subnet, quindi fare clic su **OK**. Figura Hello seguente mostra le impostazioni di blocco CIDR hello per questo scenario.
   
    ![Riquadro spazio indirizzi](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Fare clic su **gruppo di risorse** e selezionare un tooadd gruppo di risorse hello tra oppure fare clic su **Crea nuovo gruppo di risorse** tooadd hello rete virtuale tooa nuovo gruppo di risorse. Hello nella figura seguente mostra hello di risorse di gruppo per un nuovo gruppo di risorse denominato **TestRG**. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Crea riquadro gruppo di risorse](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Se necessario, modificare hello **sottoscrizione** e **percorso** le impostazioni per la rete virtuale. 
6. Se non si desidera toosee hello rete virtuale come un riquadro in hello **schermata iniziale**, disabilitare **tooStartboard Pin**. 
7. Fare clic su **crea** e notifica hello riquadro denominato **rete virtuale creazione** come illustrato nella figura che segue hello.
   
    ![Creare reti virtuali nel portale](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Attendere che hello toobe di rete virtuale creata e quando viene visualizzato hello riquadro di sotto, farvi clic sopra tooadd altre subnet.
   
    ![Creare reti virtuali nel portale](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Dovrebbe essere hello **configurazione** per la rete virtuale, come illustrato di seguito. 
   
    ![Creare reti virtuali nel portale](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Fare clic su **Subnet** > **Aggiungi**, digitare un **nome** e specificare un **intervallo di indirizzi (blocco CIDR)** per la subnet e quindi fare clic su **OK**. Figura Hello seguente mostra le impostazioni di hello per questo scenario corrente.
    
    ![Creare reti virtuali nel portale di Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

