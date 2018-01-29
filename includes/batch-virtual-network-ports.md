- La rete virtuale deve trovarsi nella stessa **area** e nella stessa **sottoscrizione** di Azure dell'account Batch.

- Per i pool creati con una configurazione di macchina virtuale, sono supportate solo le reti virtuali basate su Azure Resource Manager. Per i pool creati con una configurazione di servizi cloud, sono supportate solo le reti virtuali classiche. 
  
- Per usare una rete virtuale classica, l'entità servizio `MicrosoftAzureBatch` deve avere il ruolo di controllo di accesso basato sui ruoli (RBAC) `Classic Virtual Machine Contributor` per la rete virtuale specificata. Tuttavia per usare una rete virtuale basata su Azure Resource Manager, non è necessaria alcuna ulteriore configurazione di autorizzazioni.

- La subnet specificata per il pool deve disporre di indirizzi IP non assegnati sufficienti per contenere il numero di macchine virtuali usate come destinazione per il pool; questo valore corrisponde alla somma delle proprietà `targetDedicatedNodes` e `targetLowPriorityNodes` del pool. Se la subnet non dispone di sufficienti indirizzi IP non assegnati, il pool alloca parzialmente i nodi di calcolo e si verifica un errore di ridimensionamento. 

- La rete virtuale deve consentire la comunicazione dal servizio Batch per essere in grado di pianificare le operazioni sui nodi di calcolo. Questa condizione può essere verificata controllando se la rete virtuale dispone di gruppi di sicurezza di rete (NSG) associati. Se la comunicazione ai nodi di calcolo nella subnet specificata viene negata da un gruppo di sicurezza di rete, il servizio Batch imposta lo stato dei nodi di calcolo su **Non utilizzabile**. 

- Se la rete virtuale specificata dispone di gruppi di sicurezza di rete (NSG) e/o di un firewall, configurare le porte in ingresso e in uscita, come illustrato nelle tabelle seguenti:


  |    Porte di destinazione    |    Indirizzo IP di origine      |   Porta di origine    |    Batch aggiunge gruppi di sicurezza di rete    |    Necessarie per l'utilizzabilità della VM    |    Azione dell'utente   |
  |---------------------------|---------------------------|----------------------------|----------------------------|-------------------------------------|-----------------------|
  |   <ul><li>Per i pool creati con la configurazione macchina virtuale: 29876, 29877</li><li>Per i pool creati con la configurazione di servizi cloud: 10100, 20100 e 30100</li></ul>        |    Solo indirizzi IP del ruolo del servizio Batch | * o 443 |    Sì. Batch aggiunge gruppi di sicurezza di rete al livello di interfacce di rete collegate alle VM. Questi gruppi di sicurezza di rete consentono il traffico solo dagli indirizzi IP del ruolo del servizio Batch. Anche se si aprono queste porte per l'intero Web, il traffico verrà bloccato nella scheda di interfaccia di rete. |    Sì  |  Non è necessario specificare un gruppo di sicurezza di rete, perché Batch consente solo indirizzi IP Batch. <br /><br /> Se si specifica ugualmente un gruppo di sicurezza di rete, assicurarsi che queste porte siano aperte per il traffico in ingresso. <br /><br /> Se si specifica * come IP di origine nel gruppo di sicurezza di rete, Batch aggiunge ancora gruppi di sicurezza di rete al livello di scheda di interfaccia di rete collegata alle VM. |
  |    3389 (Windows), 22 (Linux)               |    Computer utente, usati per il debug, per poter accedere in remoto alla VM.    |   *  | No                                    |    No                    |    Aggiungere gruppi di sicurezza di rete per consentire l'accesso remoto (RDP o SSH) alla VM.   |                                


  |    Porte in uscita    |    Destination    |    Batch aggiunge gruppi di sicurezza di rete    |    Necessarie per l'utilizzabilità della VM    |    Azione dell'utente    |
  |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
  |    443    |    Archiviazione di Azure    |    No    |    Sì    |    Se si aggiungono gruppi di sicurezza di rete, assicurarsi che questa porta sia aperta per il traffico in uscita.    |

   Assicurarsi anche che l'endpoint di Archiviazione di Azure possa essere risolto da qualsiasi server DNS personalizzato che fornisce informazioni alla rete virtuale. In particolare, gli URL con formato `<account>.table.core.windows.net`, `<account>.queue.core.windows.net` e `<account>.blob.core.windows.net` devono essere risolvibili. 

   Se si aggiunge un gruppo di sicurezza di rete basato su Resource Manager, è possibile usare i [tag di servizio](../articles/virtual-network/security-overview.md#service-tags) per selezionare gli indirizzi IP di archiviazione dell'area specifica per le connessioni in uscita. Si noti che gli indirizzi IP di archiviazione devono trovarsi nella stessa area dell'account Batch e della rete virtuale. I tag servizio sono attualmente disponibili in anteprima in alcune aree di Azure.