Esistono vari motivi, quando non è possibile avviare o connettersi tooan applicazione in esecuzione in una macchina virtuale di Azure (VM). Motivi includono un'applicazione hello non è in esecuzione o in attesa sulle porte hello previsto, hello porta di attesa blocco oppure le regole non correttamente il passaggio di applicazione toohello il traffico di rete. In questo articolo viene descritto un approccio metodico toofind e problema hello corretto.

Se si verificano problemi di connessione tooyour macchina virtuale tramite RDP o SSH, vedere uno dei seguenti hello innanzitutto articoli:

* [Risoluzione dei problemi tooa connessioni Desktop remoto basato su Windows macchina virtuale di Azure](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Risoluzione dei problemi di Secure Shell (SSH) connessioni tooa basati su Linux macchina virtuale di Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../articles/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di entrambi i modelli, ma Microsoft consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.

## <a name="quick-start-troubleshooting-steps"></a>Passaggi rapidi per la risoluzione dei problemi
Nel caso di problemi di connessione dell'applicazione tooan, provare a hello seguendo i passaggi di risoluzione dei problemi generali. Dopo ogni passaggio, provare a eseguire nuovamente l'applicazione tooyour connessione:

* Riavviare la macchina virtuale hello
* Ricreare l'endpoint di hello / regole del firewall / regole di gruppo () di sicurezza di rete
  * [Modello di Resource Manager: Gestire gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Modello Classico: Gestire gli endpoint dei servizi cloud](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Connettersi da un percorso diverso, ad esempio da una diversa rete virtuale di Azure
* Ridistribuire una macchina virtuale hello
  * [Ridistribuire una VM Windows](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Ridistribuire una VM Linux](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Ricreare una macchina virtuale hello

Per ulteriori informazioni, vedere [Risoluzione dei problemi di connettività dell’Endpoint (errori RDP/SSH/HTTP, ecc.)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Panoramica dettagliata della risoluzione dei problemi
Ci sono quattro aree principali accesso hello tootroubleshoot di un'applicazione in esecuzione in una macchina virtuale di Azure.

![risolvere il problema che impedisce l'avvio dell'applicazione](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. applicazione Hello in esecuzione su hello macchina virtuale di Azure.
   * Applicazione hello stessa venga eseguito correttamente
2. Hello macchina virtuale di Azure.
   * Hello macchina virtuale stessa viene eseguita correttamente e risponde toorequests?
3. Endpoint di rete di Azure.
   * Endpoint del servizio cloud per le macchine virtuali nel modello di distribuzione classica hello.
   * Gruppi di sicurezza di rete e regole NAT in ingresso per le macchine virtuali nel modello di distribuzione Resource Manager.
   * Possibile traffico da utenti toohello VM/applicazione sulle porte hello previsto?
4. Il dispositivo periferico di Internet.
   * Le regole del firewall applicate impediscono al traffico di fluire in modo corretto?

Per i computer client che accedono a un'applicazione hello tramite una connessione site-to-site, VPN o ExpressRoute, aree principali hello che possono causare problemi sono un'applicazione hello e hello macchina virtuale di Azure.

origine hello toodetermine del problema di hello e la correzione, seguire questi passaggi.

## <a name="step-1-access-application-from-target-vm"></a>Passaggio 1: accedere all'applicazione dalla VM di destinazione
Provare a un'applicazione hello tooaccess con programma client in modo appropriato hello hello VM in cui è in esecuzione. Utilizzare un nome host locale hello, l'indirizzo IP locale hello o hello indirizzo di loopback (127.0.0.1).

![avviare l'applicazione direttamente da hello VM](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Ad esempio, se un'applicazione hello è un server web, aprire un browser su hello VM e provare a una pagina web ospitata su hello VM tooaccess.

Se è possibile accedere a un'applicazione hello, andare troppo[passaggio 2](#step2).

Se è possibile accedere a un'applicazione hello, verificare hello seguenti impostazioni:

* un'applicazione Hello è in esecuzione nella macchina virtuale di destinazione hello.
* un'applicazione Hello è in ascolto sulle porte TCP e UDP di hello previsto.

In Windows e macchine virtuali basate su Linux, usare hello **netstat - a** comando tooshow hello porte in ascolto attive. Esaminare l'output di hello per le porte hello previsto in cui l'applicazione deve essere in ascolto. Riavviare l'applicazione hello o configurare porte hello previsto toouse in base alle esigenze e riprovare a eseguire un'applicazione hello tooaccess localmente.

## <a id="step2"></a>Passaggio 2: Applicazione di accedere da un'altra macchina virtuale in hello stessa rete virtuale
Provare l'applicazione hello tooaccess da una macchina virtuale di diversa ma in hello stessa rete virtuale, usando il nome host della macchina virtuale di hello o assegnato Azure public, private o provider di indirizzo IP. Per le macchine virtuali create utilizzando il modello di distribuzione classica hello, non utilizzare alcun indirizzo IP pubblico hello del servizio cloud hello.

![applicazione avviata da una macchina virtuale diversa](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Ad esempio, se un'applicazione hello è un server web, provare tooaccess una pagina web da un browser in una macchina virtuale diversa in hello stessa rete virtuale.

Se è possibile accedere a un'applicazione hello, andare troppo[passaggio 3](#step3).

Se è possibile accedere a un'applicazione hello, verificare hello seguenti impostazioni:

* firewall host Hello nella destinazione hello VM consenta il traffico di risposta in uscita e la richiesta in ingresso hello.
* Rilevamento delle intrusioni o software in esecuzione sulla destinazione hello VM di monitoraggio della rete consenta il traffico di hello.
* Endpoint di servizi cloud o i gruppi di sicurezza di rete sono consenta il traffico hello:
  * [Modello Classico: Gestire gli endpoint dei servizi cloud](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Modello di Resource Manager: Gestire gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Un componente separato in esecuzione nella macchina virtuale nel percorso hello tra test hello macchina virtuale e la macchina virtuale, ad esempio un servizio di bilanciamento del carico o un firewall, consenta il traffico di hello.

In una macchina virtuale basato su Windows, è possibile utilizzare Windows Firewall con sicurezza avanzata toodetermine se le regole del firewall hello escludere il traffico in ingresso e in uscita dell'applicazione.

## <a id="step3"></a>Passaggio 3: Applicazione di accedere da rete virtuale hello esterna
Provare a un'applicazione hello tooaccess da un computer all'esterno di hello di rete virtuale come macchina virtuale hello in cui è in esecuzione l'applicazione hello. Usare una rete diversa come computer client originale.

![avviare l'applicazione da un computer all'esterno di rete virtuale hello](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Ad esempio, se un'applicazione hello è un server web, provare a pagina web di hello tooaccess da un browser in esecuzione in un computer che si trova nella rete virtuale hello.

Se è possibile accedere a un'applicazione hello, verificare hello seguenti impostazioni:

* Per le macchine virtuali create utilizzando il modello di distribuzione classica hello:
  
  * Verificare che la configurazione endpoint hello per hello che VM consenta il traffico in ingresso hello, in particolare protocollo hello (TCP o UDP) e i numeri di porta pubblica e privata hello.
  * Verificare che elenchi di controllo di accesso (ACL) su endpoint hello non impediscano il traffico in ingresso da Internet hello.
  * Per ulteriori informazioni, vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Per le macchine virtuali create utilizzando hello modello di distribuzione di gestione risorse:
  
  * Verificare che hello configurazione della regola NAT in ingresso per la macchina virtuale consenta il traffico in ingresso hello, in particolare protocollo hello (TCP o UDP) e i numeri di porta pubblica e privata hello hello.
  * Verificare che i gruppi di sicurezza di rete sono consenta richiesta in ingresso hello e il traffico di risposta in uscita.
  * Per ulteriori informazioni, vedere [Che cos'è un gruppo di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md)

Se l'endpoint o macchina virtuale hello è un membro di un set con bilanciamento del carico:

* Verificare che il protocollo probe hello (TCP o UDP) e il numero di porta siano corretti.
* Se hello probe protocollo e porta è diversa da hello set con carico bilanciato protocollo e porta:
  * Verificare che un'applicazione hello è in ascolto sul protocollo di probe hello (TCP o UDP) e numero di porta (utilizzare **netstat – a** su hello VM di destinazione).
  * Verificare che il firewall host hello nella destinazione hello che VM consente richiesta in ingresso probe hello e il traffico di risposta in uscita probe.

Se è possibile accedere a un'applicazione hello, verificare che consenta il dispositivo perimetrale Internet:

* traffico di richiesta in uscita dell'applicazione Hello da toohello di computer macchina virtuale di Azure del client.
* Hello il traffico di risposta dell'applicazione in ingresso da hello macchina virtuale di Azure.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Passaggio 4 se è possibile accedere a un'applicazione hello, impostazioni IP verificare toocheck hello. 

Per altre informazioni, vedere [Panoramica del monitoraggio della rete in Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Risorse aggiuntive
[Risoluzione dei problemi tooa connessioni Desktop remoto basato su Windows macchina virtuale di Azure](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Risoluzione dei problemi di Secure Shell (SSH) connessioni tooa basati su Linux macchina virtuale di Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

