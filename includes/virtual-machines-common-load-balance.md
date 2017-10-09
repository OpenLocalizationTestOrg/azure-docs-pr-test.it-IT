

Per i servizi di infrastruttura di Azure sono disponibili due livelli di bilanciamento del carico:

* **Livello di DNS**: bilanciamento del carico per i servizi cloud toodifferent il traffico in diversi data center, toodifferent siti Web di Azure si trova in data center diversi o tooexternal endpoint. Questa operazione viene eseguita con gestione traffico di Azure e hello Round Robin di metodo di bilanciamento del carico.
* **Livello di rete**: bilanciamento del carico in ingresso Internet traffico toodifferent macchine virtuali di un servizio cloud o bilanciamento del carico del traffico tra macchine virtuali in un servizio cloud o rete virtuale. Questa operazione viene eseguita con bilanciamento del carico di Azure hello.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Bilanciamento del carico di Gestione traffico per servizi cloud e siti Web
Gestione traffico permette la distribuzione di hello toocontrol di tooendpoints di traffico utente, che possono includere servizi cloud, siti Web, siti esterni e altri profili di Traffic Manager. Funzionamento di gestione traffico applicando una query di criteri intelligente motore tooDomain Name System (DNS) per i nomi di dominio hello delle risorse Internet. I servizi cloud o siti Web possono essere eseguiti in diversi Data Center parti HelloWorld.

È necessario utilizzare gli endpoint esterni di tooconfigure REST o Windows PowerShell o profili di gestione traffico come endpoint.

Gestione traffico Usa tre bilanciamento del carico di traffico toodistribute metodi:

* **Failover**: utilizzare questo metodo quando si desidera che toouse un endpoint primario per tutto il traffico, ma fornire backup nel caso in cui hello primario diventa non disponibile.
* **Prestazioni**: utilizzare questo metodo quando si dispone di endpoint in aree geografiche diverse e si desidera richiedere endpoint "più vicino" client toouse hello in termini di latenza più bassa hello.
* **Round Robin:** utilizzare questo metodo quando si desidera toodistribute carico in un set di cloud services in hello stesso Data Center o in servizi cloud o siti Web in Data Center diversi.

Per altre informazioni, vedere [Informazioni sui metodi di bilanciamento del carico di Gestione traffico](../articles/traffic-manager/traffic-manager-routing-methods.md).

Hello seguente diagramma viene illustrato un esempio di metodo di bilanciamento del carico Round Robin per la distribuzione del traffico tra i servizi cloud diversi hello.

![bilanciamento del carico](./media/virtual-machines-common-load-balance/TMSummary.png)

il processo di base di Hello è seguente hello:

1. Un client Internet corrispondente tooa web servizio DNS una query.
2. DNS inoltra hello Nome query richiesta tooTraffic Manager.
3. Gestione traffico Seleziona servizio cloud successivo hello hello elenco Round Robin e invia nuovamente hello nome DNS. server DNS del client di Hello Internet consente di risolvere l'indirizzo IP tooan nome hello e lo invia toohello client a Internet.
4. Hello Internet si connette con il servizio cloud hello scelto da Gestione traffico.

Per altre informazioni, vedere [Gestione traffico](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Bilanciamento del traffico di Azure per macchine virtuali
Macchine virtuali in hello nello stesso servizio cloud o rete virtuale possa comunicare direttamente con gli indirizzi IP privati. I computer e i servizi all'esterno di hello servizio cloud o rete virtuale può comunicare solo con macchine virtuali in un servizio cloud o rete virtuale con un endpoint configurato. Un endpoint è un mapping di un indirizzo IP pubblico e un indirizzo IP privato della porta toothat e la porta di una macchina virtuale o un ruolo web all'interno di un servizio cloud di Azure.

Hello bilanciamento del carico di Azure distribuisce in modo casuale un tipo specifico di traffico in ingresso tra più macchine virtuali o servizi in una configurazione conosciuta come un set con carico bilanciato. Ad esempio, è possibile distribuire il carico di hello del traffico di richiesta web in più server web o ruoli web.

Hello diagramma seguente mostra un endpoint con bilanciamento del carico per il traffico web (non crittografato) standard che viene condiviso tra tre macchine virtuali per hello porta pubblica e privata TCP 80. Queste tre macchine virtuali appartengono a un set con carico bilanciato.

![bilanciamento del carico](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Per altre informazioni, vedere [Bilanciamento del carico di Azure](../articles/load-balancer/load-balancer-overview.md). Per hello passaggi toocreate un set con carico bilanciato, vedere [configurare un set con carico bilanciato](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure è inoltre in grado di bilanciare il carico all'interno di un servizio cloud o una rete virtuale. Questo è noto come bilanciamento del carico interno e può essere usato in hello seguenti modi:

* Saldo tooload tra i server in diversi livelli di un'applicazione a più livelli (ad esempio, tra i livelli web e database).
* tooload saldo line-of-business (LOB) le applicazioni ospitate in Azure senza ulteriore carico bilanciamento del carico hardware o software.
* tooinclude server locali nel set di hello del computer il cui traffico con carico bilanciato.

Simile tooAzure bilanciamento del carico, bilanciamento del carico interno è facilitata dalla configurazione di un set con carico bilanciato interno.

Hello seguente diagramma viene illustrato un esempio di un endpoint con bilanciamento del carico interno per un'applicazione line-of-business (LOB) che viene condiviso tra tre macchine virtuali in una rete virtuale cross-premise.

![bilanciamento del carico](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Considerazioni sul bilanciamento del carico
Un servizio di bilanciamento del carico è configurato per impostazione predefinita tootimeout una sessione inattiva 4 minuti. Se l'applicazione di bilanciamento del carico ha lasciato una connessione inattiva per più di 4 minuti e non dispone di una configurazione Keep-Alive, hello connessione verrà interrotta. È possibile modificare tooallow comportamento del servizio di bilanciamento carico di hello un [impostazione di timeout più lungo di bilanciamento del carico di Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Altra considerazione è il tipo di hello di modalità di distribuzione supportata dal bilanciamento del carico di Azure. È possibile configurare l'affinità IP di origine (IP di origine, IP di destinazione) o il protocollo IP di origine (IP di origine, IP di destinazione e protocollo). Per altre informazioni, vedere l'articolo relativo alla [modalità di distribuzione del servizio di bilanciamento del carico di Azure (affinità IP di origine)](../articles/load-balancer/load-balancer-distribution-mode.md) .

## <a name="next-steps"></a>Passaggi successivi
Per hello passaggi toocreate un set con carico bilanciato, vedere [configurare un set con carico bilanciato interno](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Per altre informazioni sul bilanciamento del carico, vedere [Bilanciamento del carico interno](../articles/load-balancer/load-balancer-internal-overview.md).

