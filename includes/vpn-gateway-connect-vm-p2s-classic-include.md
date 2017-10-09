È possibile connettersi tooa macchina virtuale che viene distribuito tooyour rete virtuale tramite la creazione di una macchina virtuale di tooyour connessione Desktop remoto. Hello migliore tooinitially modo verificare che sia possibile connettersi tooyour macchina virtuale è tooconnect dal relativo IP privati risolvere, anziché il nome di computer. In questo modo, si sta testando toosee se è possibile connettersi, non indica se la risoluzione dei nomi sia configurato correttamente. 

1. Individuare l'indirizzo IP privato hello per la macchina virtuale. È possibile trovare l'indirizzo IP privato hello di una macchina virtuale, entrambi esaminando le proprietà di hello per macchina virtuale nel portale di Azure hello hello o tramite PowerShell.
2. Verificare di essere connessi tooyour virtuale usando hello Point-to-Site VPN connessione. 
3. Aprire connessione Desktop remoto, digitare "RDP" o "Connessione Desktop remoto" nella casella di ricerca hello hello barra delle applicazioni, quindi selezionare una connessione Desktop remoto. È anche possibile aprire connessione Desktop remoto, uso del comando 'mstsc' hello in PowerShell. 
3. In connessione Desktop remoto, immettere l'indirizzo IP privato hello di hello macchina virtuale. È possibile fare clic su "Mostra opzioni" tooadjust ulteriori impostazioni, quindi connettersi.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot un tooa connessione RDP VM

Se si riscontrano problemi nella connessione macchina virtuale tooa tramite la connessione VPN, esistono alcuni aspetti, che è possibile controllare. Per ulteriori informazioni sulla risoluzione dei problemi, vedere [tooa connessioni Desktop remoto di risolvere i problemi VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Verificare che la connessione VPN sia attiva.
- Verificare che ci si connette l'indirizzo IP privato toohello per hello macchina virtuale.
- Utilizzare 'ipconfig' toocheck hello indirizzo IPv4 assegnato scheda Ethernet toohello computer hello da cui si è connessi. Se l'indirizzo IP hello è nell'intervallo di indirizzi hello di rete virtuale che si connette a hello o compresi nell'intervallo di indirizzi hello del VPNClientAddressPool, si tratta di cui viene fatto riferimento tooas uno spazio degli indirizzi sovrapposti. Quando lo spazio degli indirizzi si sovrappone in questo modo, il traffico di rete hello non raggiunge Azure, rimane nella rete locale hello.
- Se è possibile connettersi toohello VM con IP privato hello indirizzo, ma non hello Nome computer, verificare che DNS sia stato configurato correttamente. Per altre informazioni sul funzionamento della risoluzione dei nomi per le macchine virtuali, vedere [Risoluzione dei nomi per le macchine virtuali](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Verificare che il pacchetto di configurazione client VPN hello è stato generato dopo che sono stati specificati indirizzi IP del server DNS hello per hello rete virtuale. Se è stato aggiornato gli indirizzi IP di server DNS di hello, generare e installare un nuovo pacchetto di configurazione client VPN.
