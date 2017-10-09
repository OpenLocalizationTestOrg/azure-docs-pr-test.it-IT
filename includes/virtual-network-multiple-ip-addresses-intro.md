> [!div class="op_single_selector"]
> * [Portale](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [Interfaccia della riga di comando 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [Interfaccia della riga di comando 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Modello](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Una macchina virtuale di Azure (VM) include uno o più interfacce di rete (NIC) collegati tooit. Qualsiasi scheda di rete può avere uno o tooit assegnato di indirizzi IP pubblici e privati più statico o dinamico. L'assegnazione di più IP indirizzi tooa VM consente hello seguenti funzionalità:

* Ospitare più siti Web o servizi con indirizzi IP e certificati SSL diversi in un singolo server.
* Fungere da appliance virtuale di rete, ad esempio un firewall o un servizio di bilanciamento del carico.
* Hello tooadd possibilità qualsiasi IP privato hello risolve per le schede di interfaccia di hello tooan pool back-end di bilanciamento del carico di Azure. In hello oltre, hello solo indirizzo IP primario per hello che NIC primario può essere aggiunto pool back-end tooa. ulteriori informazioni sugli toolearn come tooload bilanciare più configurazioni IP, leggere hello [il bilanciamento del carico di più configurazioni IP](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.

Ogni macchina virtuale di tooa NIC associata contiene uno o più configurazioni IP associata tooit. A ogni configurazione viene assegnato un indirizzo IP privato statico o dinamico. Ogni configurazione può inoltre essere uno tooit di risorsa associata di indirizzo IP pubblico. Entrambi un dinamico o statico pubblico IP indirizzo assegnato tooit dispone di una risorsa di indirizzo IP pubblica. gli indirizzi toolearn più sull'indirizzo IP in Azure, leggere hello [agli indirizzi IP in Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) articolo. 

È un limite toohow molti IP privato è possibile assegnare indirizzi tooa scheda di rete. È inoltre disponibile un limite toohow molti indirizzi IP pubblici che possono essere usati in una sottoscrizione di Azure. Vedere hello [Azure limita](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) articolo per informazioni dettagliate.
