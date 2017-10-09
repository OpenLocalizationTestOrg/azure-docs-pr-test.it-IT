Aprire una porta o creare un endpoint, tooa macchina virtuale (VM) in Azure tramite la creazione di un filtro di rete su una subnet o l'interfaccia di rete VM. Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, posizionare in una risorsa toohello gruppo di sicurezza di rete associata che riceve il traffico di hello.

Si userà un esempio comune di traffico Web sulla porta 80. Dopo aver una macchina virtuale che le richieste web tooserve configurato sulla porta TCP standard hello 80 (ricordare servizi appropriati di toostart hello e aprire tutte le regole firewall del sistema operativo su hello VM) è:

1. Creare un gruppo di sicurezza di rete.
2. Creare una regola in ingresso che consenta il traffico con:
   * intervallo di porte di destinazione Hello "80"
   * intervallo di porte di origine Hello "*" (consentire qualsiasi porta di origine)
   * il valore di priorità minore 65.500 (toobe superiore in ordine di priorità predefinito catch-all hello negare regola in entrata)
3. Associare subnet o l'interfaccia di rete VM hello hello il gruppo di sicurezza di rete.

È possibile creare reti complesse configurazioni toosecure ambiente mediante gruppi di sicurezza di rete e le regole. L'esempio usa solo una o due regole che consentono il traffico HTTP o la gestione remota. Per ulteriori informazioni, vedere l'esempio hello ["Ulteriori informazioni"](#more-information-on-network-security-groups) sezione o [che cos'è un gruppo di sicurezza di rete?](../articles/virtual-network/virtual-networks-nsg.md)

