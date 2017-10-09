> [!NOTE]
> * gateway VPN Hello indirizzo IP pubblico verrà modificato durante la migrazione da un vecchio tooa SKU SKU di nuovo.
> * È possibile eseguire la migrazione classico VPN gateway toohello SKU di nuovo. Classico VPN gateway può utilizzare solo hello legacy SKU (precedente).
> 

Non è possibile ridimensionare la VPN di Azure gateway tra hello SKU precedente e hello nuove famiglie SKU. Se si dispone di gateway VPN nel modello di distribuzione di gestione risorse di hello che usano una versione precedente di hello di hello SKU, è possibile eseguire la migrazione toohello SKU di nuovo. toomigrate, si elimina il gateway VPN esistente di hello per la rete virtuale, quindi crearne uno nuovo.

Flusso di lavoro della migrazione:

1. Rimuovere qualsiasi gateway di rete virtuale toohello connessioni.
2. Eliminare il gateway VPN precedente hello.
3. Creare nuovo gateway VPN di hello.
4. Aggiornare il dispositivo VPN locale con hello nuovo VPN gateway indirizzo IP (per le connessioni da sito a sito).
5. Valore dell'indirizzo IP gateway hello per tutti i gateway di rete virtuale a rete locale si connetterà gateway toothis di aggiornamento.
6. Scaricare nuovi pacchetti di configurazione di client VPN per i client P2S la connessione di rete virtuale toohello tramite il gateway VPN.
7. Ricreare i gateway di rete virtuale toohello connessioni hello.
