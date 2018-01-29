Per creare una rete virtuale nel modello di distribuzione Resource Manager usando il portale di Azure, seguire questa procedura. Gli screenshot sono forniti come esempi. Assicurarsi di sostituire i valori con i propri. Per altre informazioni sull'uso delle reti virtuali, vedere la [panoramica sulla rete virtuale](../articles/virtual-network/virtual-networks-overview.md).

>[!NOTE]
>Per consentire a questa rete virtuale di connettersi a una posizione locale, è necessario coordinarsi con l'amministratore di rete locale per definire un intervallo di indirizzi IP da usare in modo specifico per questa rete virtuale. Se su entrambi i lati della connessione VPN è presente un intervallo di indirizzi duplicato, il traffico non viene indirizzato nel modo previsto. Se inoltre si vuole connettere questa rete virtuale a un'altra rete virtuale, lo spazio degli indirizzi non può sovrapporsi a un'altra rete virtuale. Pianificare quindi con attenzione la configurazione della rete.
>
>

1. In un browser passare al [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account Azure.
2. Fare clic su **+** Nel campo **Cerca nel Marketplace** digitare "Rete virtuale". Individuare **Rete virtuale** nell'elenco restituito e fare clic per aprire la pagina **Rete virtuale**.

  ![Pagina per individuare la risorsa Rete virtuale](./media/vpn-gateway-basic-vnet-rm-portal-include/newvnetportal700.png "Pagina per individuare la risorsa Rete virtuale")
3. Nella parte inferiore della pagina Rete virtuale selezionare **Resource Manager** nell'elenco **Selezionare un modello di distribuzione** e quindi fare clic su **Crea**.

  ![Selezionare Resource Manager](./media/vpn-gateway-basic-vnet-rm-portal-include/resourcemanager250.png "Selezionare Resource Manager")
4. Nella pagina **Crea rete virtuale** configurare le impostazioni della rete virtuale. Durante la compilazione dei campi, il punto esclamativo rosso diventa un segno di spunta verde se i caratteri immessi nel campo sono validi. Alcuni valori possono essere compilati automaticamente. In questo caso, sostituire i valori con quelli personalizzati. La pagina **Crea rete virtuale** ha un aspetto simile all'esempio seguente:

  ![Pagina Crea rete virtuale](./media/vpn-gateway-basic-vnet-rm-portal-include/vnet.png "Pagina Crea rete virtuale")
5. **Nome**: immettere un nome per la rete virtuale.
6. **Spazio indirizzi**: immettere lo spazio degli indirizzi. Se si hanno più spazi di indirizzi da aggiungere, aggiungere il primo. È possibile aggiungere altri spazi di indirizzi in un secondo momento, dopo aver creato la rete virtuale.
7. **Sottoscrizione**: verificare che sia visualizzata la sottoscrizione corretta. È possibile cambiare sottoscrizione tramite l'elenco a discesa.
8. **Gruppo di risorse**: selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Se si crea un nuovo gruppo, denominare il gruppo di risorse in base ai valori di configurazione pianificati. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
9. **Località**: selezionare la località della rete virtuale. La località determina la posizione in cui risiedono le risorse distribuite in questa rete virtuale.
10. **Subnet**: aggiungere il nome e l'intervallo di indirizzi della subnet. È possibile aggiungere altre subnet in un secondo momento, dopo aver creato la rete virtuale.
11. Selezionare **Aggiungi al dashboard** se si vuole trovare facilmente la rete virtuale nel dashboard e quindi fare clic su **Crea**.

  ![Aggiungi al dashboard](./media/vpn-gateway-basic-vnet-rm-portal-include/pintodashboard150.png "Aggiungi al dashboard")