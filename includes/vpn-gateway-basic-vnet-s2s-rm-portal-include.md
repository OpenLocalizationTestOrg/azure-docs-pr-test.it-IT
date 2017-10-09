una rete virtuale nel modello di distribuzione di gestione risorse di hello tramite il portale di Azure, hello toocreate procedura hello riportata di seguito. Hello utilizzare [valori di esempio](#values) se si utilizza questa procedura come un'esercitazione. Se non si siano eseguendo questi passaggi come un'esercitazione, è possibile che tooreplace hello i valori con il proprio. Per ulteriori informazioni sull'utilizzo di reti virtuali, vedere hello [Panoramica di rete virtuale](../articles/virtual-network/virtual-networks-overview.md).

1. Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e accedere con l'account di Azure.
2. Fare clic su **New**. In hello **marketplace hello ricerca** , digitare 'Rete virtuale'. Individuare **rete virtuale** hello restituito elenco e fare clic su hello tooopen **rete virtuale** blade.
3. Parte inferiore di hello del Pannello di rete virtuale hello, da hello **selezionare un modello di distribuzione** selezionare **Gestione risorse**, quindi fare clic su **crea**. Verrà aperto il pannello di 'Crea rete virtuale' hello.

    ![Pannello Crea rete virtuale](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Pannello Crea rete virtuale")
4. In hello **crea rete virtuale** pannello, configurare le impostazioni di rete virtuale hello. Quando si compila i campi di hello, hello punto esclamativo rosso diventa un segno di spunta verde quando caratteri hello immessi nel campo hello sono validi.

  - **Nome**: immettere il nome di hello per la rete virtuale. In questo esempio si usa il nome TestVNet1.
  - **Lo spazio degli indirizzi**: immettere lo spazio degli indirizzi di hello. Se si dispone di più tooadd di spazi di indirizzi, aggiungere lo spazio degli indirizzi prima. È possibile aggiungere altri spazi di indirizzi in un secondo momento, dopo la creazione di hello rete virtuale. Assicurarsi che lo spazio indirizzo hello non sovrapporsi allo spazio di indirizzi hello per il percorso locale specificato.
  - **Nome della subnet**: aggiungere hello primo nome e la subnet intervallo di indirizzi subnet. È possibile aggiungere altre subnet e subnet del gateway hello in un secondo momento, dopo la creazione di questa rete virtuale. 
  - **Sottoscrizione**: verificare che sottoscrizione hello elencata è hello corretto. È possibile modificare le sottoscrizioni con elenco a discesa hello.
  - **Gruppo di risorse**: selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Se si sta creando un nuovo gruppo, nome gruppo di risorse di hello in base tooyour pianificato i valori di configurazione. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Percorso**: selezionare il percorso di hello per la rete virtuale. posizione di Hello determina in cui risiederà risorse hello distribuire toothis rete virtuale.

5. Selezionare **Pin toodashboard** se si desidera che la rete virtuale con facilità in dashboard hello toofind in grado di toobe e quindi fare clic su **crea**. Dopo aver fatto clic **crea**, verrà visualizzato un riquadro nel dashboard che riflette lo stato di avanzamento hello di una rete virtuale. le modifiche apportate al riquadro Hello come hello rete virtuale viene creato.
