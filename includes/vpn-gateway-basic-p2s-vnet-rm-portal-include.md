una rete virtuale nel modello di distribuzione di gestione risorse di hello tramite il portale di Azure, hello toocreate procedura hello riportata di seguito. schermate di Hello sono fornite come esempi. Essere certi tooreplace hello i valori con valori personalizzati. Per ulteriori informazioni sull'utilizzo di reti virtuali, vedere hello [Panoramica di rete virtuale](../articles/virtual-network/virtual-networks-overview.md).

1. Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account di Azure.
2. Fare clic su **+** In hello **marketplace hello ricerca** , digitare "Rete virtuale". Individuare **rete virtuale** hello restituito elenco e fare clic su hello tooopen **rete virtuale** pagina.

  ![Pagina per individuare la risorsa Rete virtuale](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Pagina per individuare la risorsa Rete virtuale")
3. Nella parte inferiore di hello della pagina rete virtuale hello da hello **selezionare un modello di distribuzione** selezionare **Gestione risorse**, quindi fare clic su **crea**.

  ![Selezionare Resource Manager](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Selezionare Resource Manager")
4. In hello **crea rete virtuale** pagina, configurare le impostazioni di rete virtuale hello. Quando si compila i campi di hello, hello punto esclamativo rosso diventa un segno di spunta verde quando caratteri hello immessi nel campo hello sono validi. Alcuni valori possono essere compilati automaticamente. In caso affermativo, sostituire valori hello con valori personalizzati. Hello **crea rete virtuale** pagina ha un aspetto simile toohello esempio seguente:

  ![Convalida dei campi](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "Convalida dei campi")
5. **Nome**: immettere il nome di hello per la rete virtuale.
6. **Lo spazio degli indirizzi**: immettere lo spazio degli indirizzi di hello. Se si dispone di più tooadd di spazi di indirizzi, aggiungere lo spazio degli indirizzi prima. È possibile aggiungere altri spazi di indirizzi in un secondo momento, dopo la creazione di hello rete virtuale.
7. **Nome della subnet**: aggiungere hello nome e la subnet intervallo di indirizzi subnet. È possibile aggiungere altre subnet in un secondo momento, dopo la creazione di hello rete virtuale.
8. **Sottoscrizione**: verificare che hello sottoscrizione elencata è hello corretto. È possibile modificare le sottoscrizioni con elenco a discesa hello.
9. **Gruppo di risorse**: selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Se si sta creando un nuovo gruppo, nome gruppo di risorse di hello in base tooyour pianificato i valori di configurazione. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
10. **Percorso**: selezionare il percorso di hello per la rete virtuale. posizione di Hello determina in cui risiederà risorse hello distribuire toothis rete virtuale.
11. Selezionare **Pin toodashboard** se si desidera che la rete virtuale con facilità in dashboard hello toofind in grado di toobe e quindi fare clic su **crea**.

 ![PIN toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "toodashboard pin")
12. Dopo aver fatto clic **crea**, verrà visualizzato un riquadro nel dashboard che riflette lo stato di avanzamento hello di una rete virtuale. le modifiche apportate al riquadro Hello come hello rete virtuale viene creato.

  ![Riquadro Creazione della rete virtuale](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Riquadro Creazione della rete virtuale")