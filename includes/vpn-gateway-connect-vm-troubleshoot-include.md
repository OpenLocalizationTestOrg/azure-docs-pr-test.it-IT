Se si riscontrano problemi nella connessione macchina virtuale tooa tramite la connessione VPN, verificare i seguenti di hello:

- Verificare che la connessione VPN sia attiva.
- Verificare che ci si connette l'indirizzo IP privato toohello per hello macchina virtuale.
- Se è possibile connettersi toohello VM con IP privato hello indirizzo, ma non hello Nome computer, verificare che DNS sia stato configurato correttamente. Per altre informazioni sul funzionamento della risoluzione dei nomi per le macchine virtuali, vedere [Risoluzione dei nomi per le macchine virtuali](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Quando connettono tramite Point-to-Site, controllare hello elementi aggiuntivi seguenti:

- Utilizzare 'ipconfig' toocheck hello indirizzo IPv4 assegnato scheda Ethernet toohello computer hello da cui si è connessi. Se l'indirizzo IP hello è nell'intervallo di indirizzi hello di rete virtuale che si connette a hello o compresi nell'intervallo di indirizzi hello del VPNClientAddressPool, si tratta di cui viene fatto riferimento tooas uno spazio degli indirizzi sovrapposti. Quando lo spazio degli indirizzi si sovrappone in questo modo, il traffico di rete hello non raggiunge Azure, rimane nella rete locale hello.
- Verificare che il pacchetto di configurazione client VPN hello è stato generato dopo che sono stati specificati indirizzi IP del server DNS hello per hello rete virtuale. Se è stato aggiornato gli indirizzi IP di server DNS di hello, generare e installare un nuovo pacchetto di configurazione client VPN.

Per ulteriori informazioni sulla risoluzione dei problemi di una connessione RDP, vedere [tooa connessioni Desktop remoto di risolvere i problemi VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
