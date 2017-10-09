# <a name="container-service-frequently-asked-questions"></a>Domande frequenti sul servizio contenitore

## <a name="orchestrators"></a>Agenti di orchestrazione

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Quali agenti di orchestrazione contenitore sono supportati nel servizio contenitore di Azure? 

È previsto il supporto per DC/OS open source, Docker Swarm e Kubernetes. Per ulteriori informazioni, vedere hello [Panoramica](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>La modalità Docker Swarm è supportata? 

Modalità sciame non è attualmente supportata, ma è roadmap servizio hello. 

### <a name="does-azure-container-service-support-windows-containers"></a>Il servizio contenitore di Azure supporta i contenitori Windows?  

Attualmente sono supportati i contenitori Linux con tutti gli agenti di orchestrazione. Il supporto per i contenitori Windows con Kubernetes è disponibile in anteprima.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>È consigliabile un agente di orchestrazione specifico nel servizio contenitore di Azure? 
In genere non viene consigliato un agente di orchestrazione specifico. Se si ha esperienza con uno dei orchestrators hello è supportato, è possibile applicare tale esperienza acquisita nel servizio contenitore di Azure. Le tendenze dei dati suggeriscono tuttavia che DC/OS è il prodotto collaudato per i carichi di lavoro di Big Data e IoT, Kubernetes è ideale per i carichi di lavoro nativi del cloud e Docker Swarm è noto per l'integrazione con gli strumenti di Docker e la facile curva di apprendimento.

A seconda dello scenario, è anche possibile compilare e gestire soluzioni contenitore personalizzate con altri servizi di Azure. Questi servizi includono [Macchine virtuali](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [App Web](../articles/app-service-web/app-service-web-overview.md) e [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Qual è la differenza hello tra il motore di ACS e il servizio contenitore di Azure? 
Servizio di contenitore di Azure è un servizio di Azure eseguito il contratto di servizio con funzionalità hello portale di Azure, gli strumenti da riga di comando di Azure e le API di Azure. servizio Hello consente tooquickly implementare e gestire i cluster che esegue strumenti di orchestrazione contenitore standard con un numero relativamente ridotto di opzioni di configurazione. 

[Modulo di gestione ACS](http://github.com/Azure/acs-engine) è un progetto open source che consente di configurare power users toocustomize hello cluster a ogni livello. Questa possibilità tooalter hello configurazione sia l'infrastruttura software significa che non offriamo alcun contratto di servizio per il motore di ACS. Supporto viene gestito tramite il progetto open source hello su GitHub anziché tramite canali ufficiali di Microsoft. 

## <a name="cluster-management"></a>Gestione dei cluster

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Come si creano le chiavi SSH per il cluster?

È possibile utilizzare gli strumenti standard nel toocreate del sistema operativo una coppia chiave SSH RSA pubblica e privata per l'autenticazione hello le macchine virtuali Linux per il cluster. Per istruzioni, vedere hello [OS X e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) informazioni aggiuntive. 

Se si utilizza [comandi CLI di Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un contenitore del servizio cluster, SSH chiavi possono essere generate automaticamente per il cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Come si crea un'entità servizio per il cluster Kubernetes?

Un ID dell'entità servizio di Azure Active Directory e la password sono anche necessari toocreate un cluster Kubernetes contenitore nel servizio di Azure. Per ulteriori informazioni, vedere [sulle entità servizio hello per un cluster Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Se si utilizza [comandi CLI di Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un Kubernetes, servizio cluster principale credenziali possono essere generate automaticamente per il cluster.

### <a name="how-large-a-cluster-can-i-create"></a>Quali possono essere le dimensioni dei cluster creati?
È possibile creare un cluster con 1, 3 o 5 nodi master È possibile scegliere di nodi agente too100.

> [!IMPORTANT]
> Per i cluster di grandi dimensioni e a seconda delle dimensioni della macchina virtuale desiderato per i nodi di hello, potrebbe essere necessario quota di core hello tooincrease nella sottoscrizione. toorequest un aumento della quota, aprire un [richiesta di supporto clienti online](../articles/azure-supportability/how-to-create-azure-support-request.md) senza alcun costo. Con un [account gratuito di Azure](https://azure.microsoft.com/free/)è possibile usare solo un numero limitato di core di calcolo di Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Come aumentare il numero di hello di schemi dopo la creazione di un cluster? 
Una volta creato il cluster hello, numero hello di schemi è fisso e non può essere modificato. Durante la creazione di cluster hello hello idealmente selezionare più schemi per la disponibilità elevata.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Come aumentare il numero di hello di agenti dopo la creazione di un cluster? 
È possibile scalare il numero di hello di agenti cluster hello utilizzando hello portale di Azure o strumenti da riga di comando. Vedere [Ridimensionare un cluster del servizio contenitore di Azure](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Quali sono gli URL di hello dei master e gli agenti? 
gli URL di Hello del cluster di risorse nel servizio contenitore di Azure si basano hello prefisso è specificare e nome dell'area di Azure si è scelto per la distribuzione di hello hello nome DNS. Ad esempio, il nome di dominio completo hello (FQDN) del nodo principale hello è di questo form:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

È possibile trovare gli URL utilizzati per il cluster in hello portale di Azure, hello Esplora inventario risorse di Azure o altri strumenti di Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Come si può stabilire la versione dell'agente di orchestrazione in esecuzione nel cluster?

* Controller di dominio o del sistema operativo: Vedere hello [documentazione Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: eseguire `docker version`
* Kubernetes: eseguire `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Come aggiornare orchestrator hello dopo la distribuzione?

Attualmente, il servizio contenitore di Azure non fornisce strumenti tooupgrade hello versione orchestrator hello che è stato distribuito il cluster. Se il servizio contenitore supporta una versione successiva, è possibile distribuire un nuovo cluster. Un'altra opzione consiste strumenti specifici orchestrator toouse se sono disponibili tooupgrade un cluster sul posto. Per un esempio, vedere [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/) (Aggiornamento di DC/OS).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Dove trovare il cluster toomy stringa di hello SSH connessione?

È possibile trovare la stringa di connessione hello in hello portale di Azure o utilizzando gli strumenti da riga di comando di Azure. 

1. Nel portale di hello passare toohello gruppo di risorse per la distribuzione di cluster hello.  

2. Fare clic su **Panoramica** e fare clic sul collegamento hello **distribuzioni** in **Essentials**. 

3. In hello **cronologia della distribuzione** pannello, fare clic su distribuzione hello il cui nome inizia con **microsoft acs** seguito da una data di distribuzione. Esempio: microsoft-acs-201701310000.  

4. In hello **riepilogo** pagina **output**, vengono forniti i collegamenti di cluster diversi. **SSHMaster0** fornisce un SSH connessione stringa toohello prima master nel cluster del servizio di contenitore. 

Come indicato in precedenza, è possibile utilizzare anche gli strumenti di Azure toofind hello nome di dominio completo del database master hello. Verificare una connessione SSH toohello master utilizzando hello FQDN del master hello hello del nome utente specificato durante la creazione di cluster hello. ad esempio:

```bash
ssh userName@masterFQDN –A –p 22 
```

Per ulteriori informazioni, vedere [cluster del servizio di contenitore di Azure Connect tooan](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Passaggi successivi

* [Altre informazioni](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) sul servizio contenitore di Azure.
* Distribuire un cluster di servizio di contenitore mediante hello [portale](../articles/container-service/dcos-swarm/container-service-deployment.md) o [CLI di Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
