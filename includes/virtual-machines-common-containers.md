Le soluzioni del cloud di Azure si basano sulle macchine virtuali (emulazione di componenti hardware del computer fisico) e consentono così la creazione agile di pacchetti di distribuzioni software e un migliore consolidamento delle risorse rispetto all'hardware fisico. [Docker](https://www.docker.com) contenitori e hello ecosistema docker offre hello notevolmente espanso modi in cui sviluppare, fornire e gestire il software distribuito. Codice dell'applicazione in un contenitore è isolato dalla macchina virtuale host hello e altri contenitori in hello stessa macchina virtuale. Questo isolamento offre maggiore flessibilità di sviluppo e distribuzione.

Azure offre hello valori Docker seguenti:

* [Molti](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [diversi](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) modi toocreate Docker ospita per contenitori toosuit situazione
* Hello [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/) creato un cluster di host contenitore utilizzando, ad esempio orchestrators **maratona** e **swarm**.
* [Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md) e [modelli di gruppo di risorse](../articles/resource-group-authoring-templates.md) toosimplify distribuzione e aggiornamento di applicazioni distribuite complesse
* integrazione con un'ampia gamma di  strumenti di gestione della configurazione sia proprietari che open source

E poiché è possibile creare a livello di codice le macchine virtuali e Linux contenitori in Azure, è inoltre possibile utilizzare macchina virtuale e contenitore *orchestrazione* toocreate gruppi di macchine virtuali (VM) e le applicazioni all'interno sia Linux toodeploy degli strumenti contenitori e ora [contenitori di Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

In questo articolo illustra non solo di questi concetti di alto livello, contiene inoltre una serie di informazioni toomore collegamenti, esercitazioni, e i prodotti correlati utilizzo toocontainer e cluster in Azure. Se si conoscenza tutte queste e si desidera che solo i collegamenti di hello, stanno qui [strumenti per l'utilizzo di contenitori](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>differenza Hello tra macchine virtuali e contenitori
Le macchine virtuali vengono eseguite all'interno di un ambiente di virtualizzazione hardware isolato fornito da un [hypervisor](http://en.wikipedia.org/wiki/Hypervisor). In Azure, hello [macchine virtuali](https://azure.microsoft.com/services/virtual-machines/) service tutte handle per l'utente: creazione di macchine virtuali scegliendo hello del sistema operativo e la configurazione &mdash;oppure caricare un'immagine di macchina virtuale personalizzata. Sono disponibili numerosi strumenti e le macchine virtuali sono una tecnologia collaudata, "avanzata battaglia" hello toomanage disponibili del sistema operativo e le applicazioni che contengono.  Le applicazioni in una macchina virtuale sono nascoste dal sistema operativo host hello. Dal punto di vista di hello di un'applicazione o un utente in una macchina virtuale, hello VM viene visualizzato toobe un computer fisico autonomo.

[Contenitori di Linux](http://en.wikipedia.org/wiki/LXC) e non quelli creati e ospitati tramite gli strumenti di docker, usare un isolamento tooprovide hypervisor. Con i contenitori, l'host contenitore hello utilizza processo e funzionalità di isolamento di file del sistema del contenitore di hello Linux kernel tooexpose toohello, relativo alle App, alcune funzionalità del kernel e il proprio sistema di file isolati. Dal punto di vista di hello di un'app in esecuzione all'interno di un contenitore, il contenitore di hello viene visualizzato toobe un'unica istanza del sistema operativo. Un'app indipendente non può vedere processi o altre risorse all'esterno del relativo contenitore.

In un contenitore Docker vengono usate molte meno risorse rispetto a quelle usate in una macchina virtuale. Contenitori di docker usano un isolamento e l'esecuzione modello dell'applicazione, che non condivide il kernel hello dell'host Docker hello. contenitore Hello è molto basso impatto del disco che non includa hello intero sistema operativo. I tempi di avvio e lo spazio su disco necessario sono notevolmente inferiori rispetto a quelli di una macchina virtuale.
Contenitori di Windows offrono hello stessi vantaggi di contenitori di Linux per App eseguite in Windows. Contenitori di Windows supportano formato di immagine hello Docker e Docker API, ma possono anche essere gestiti con PowerShell. Due runtime contenitore sono disponibili con i contenitori Windows, i contenitori Windows Server e i contenitori Hyper-V. I contenitori Hyper-V offrono un ulteriore livello di isolamento, perché ogni contenitore è ospitato in una macchina virtuale altamente ottimizzata. informazioni sui contenitori di Windows, vedere toolearn [sui contenitori di Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget base sui contenitori di Windows in Azure, di informazioni su come troppo[distribuire un cluster il servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Per quale scopo sono utili i contenitori?

I contenitori permettono di migliorare quanto segue:

* è possibile sviluppare e condivisa liberamente il codice dell'applicazione Hello velocità
* velocità di Hello e di confidenza che un'app può essere testata
* velocità di Hello e confidenza che può essere distribuita un'app

I contenitori vengono eseguiti in un host contenitore o un sistema operativo. In Azure si tratta di una macchina virtuale di Azure. Anche se ti piace già idea hello di contenitori, ancora eseguirai tooneed un'infrastruttura di macchina virtuale ospita hello contenitori, ma i vantaggi di hello sono contenitori non occorre nella macchina virtuale di cui è in esecuzione (anche se il contenitore di hello vuole un Linux o Windows ambiente di esecuzione sarà importanti, ad esempio).


## <a name="what-are-containers-good-for"></a>Per quale scopo sono utili i contenitori?
Fantastica per molte operazioni, ma essi incoraggiare&mdash;come [servizi Cloud di Azure](https://azure.microsoft.com/services/cloud-services/) e [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;hello creazione del singolo servizio, orientata ai servizi microservizio applicazioni distribuite, in quale applicazione progettazione si basa su altre parti di piccole dimensioni e componibile invece che sui componenti più grandi e più fortemente accoppiati.

Ciò vale soprattutto in ambienti di cloud pubblico come Azure, in cui in si possono affittare VM quando e dove si desidera. Non solo si ottengono un isolamento, una rapida distribuzione e gli strumenti di orchestrazione, ma è anche possibile prendere decisioni più efficienti sull’infrastruttura delle applicazioni.

Ad esempio, si potrebbe disporre attualmente di una distribuzione costituita da 9 VM di Azure di grandi dimensioni per un'applicazione distribuita a disponibilità elevata. Se hello componenti dell'applicazione possono essere distribuiti nei contenitori, si potrebbe essere in grado di toouse solo 4 macchine virtuali e distribuire i componenti dell'applicazione all'interno di contenitori di 20 per il bilanciamento del carico e ridondanza.

Questo è un esempio, naturalmente, ma se è possibile farlo nello scenario, è possibile regolare i picchi di toousage con più contenitori anziché più macchine virtuali di Azure e utilizzare hello rimanenti carico complessivo della CPU in modo più efficiente rispetto alla versione precedente.

Inoltre, esistono molti scenari che non si prestano tooa microservizi approccio; si conosceranno meglio se microservizi e i contenitori consentono.

### <a name="container-benefits-for-developers"></a>Vantaggi dei contenitori per gli sviluppatori
In generale, è facile toosee che la tecnologia di contenitore è un passo avanti, ma sono disponibili anche i vantaggi più specifici. Prendiamo ad esempio hello contenitori Docker. In questo argomento non approfondire eccessivamente Docker ora (lettura [novità Docker?](https://www.docker.com/whatisdocker/) per una determinata storia, o [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), ma Docker e relativo ecosistema offrono notevoli vantaggi agli sviluppatori di tooboth e IT professionisti IT.

Gli sviluppatori di eseguire rapidamente, contenitori tooDocker perché sopra tutti rende facile l'utilizzo di contenitori di Linux e Windows:

* Possibile usare i comandi semplici e incrementale toocreate un'immagine fissa che è facile toodeploy e consente di automatizzare la creazione di tali immagini usando un dockerfile
* Gli utenti possono condividere le immagini con facilità utilizzando semplice, [git](https://git-scm.com/)-stile push e pull comandi troppo[pubblica](https://registry.hub.docker.com/) o [registri docker privato](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Possono considerare i componenti dell’applicazione isolata invece che i computer.
* Possono utilizzare un numero elevato di strumenti che comprendono contenitori Docker e immagini di base diverse

### <a name="container-benefits-for-operations-and-it-professionals"></a>Vantaggi dei contenitori per professionisti IT e operazioni
IT e ai professionisti di operazioni anche trarre vantaggio dalla combinazione di hello di contenitori e macchine virtuali.

* i servizi indipendenti sono isolati dall’ambiente di esecuzione host della VM
* il codice indipendente è effettivamente identico
* i servizi indipendenti possono essere avviati, arrestati e spostati rapidamente tra gli ambienti di sviluppo, test e produzione

Le funzionalità come questi&mdash;e vi sono altre&mdash;excite aziende stabilite, in cui le organizzazioni IT professional impostare hello del processo di adattamento risorse&mdash;inclusi pura potenza di elaborazione&mdash; toohello attività obbligatorio toonot solo rimanere in azienda, ma soddisfazione dei clienti e raggiungere. Aziende di piccole dimensioni, ISV e avvii hanno esattamente hello stesso requisito, ma potrebbe descrivono in modo diverso.

## <a name="what-are-virtual-machines-good-for"></a>Per quali scopi sono utili le macchine virtuali?
Le macchine virtuali forniscono backbone hello del cloud computing e che non cambia. Se le macchine virtuali avvia più lentamente, hanno un impatto del disco più grande e non eseguano il mapping direttamente tooa microservizi architettura, hanno molto importanti vantaggi:

1. Per impostazione predefinita, dispongono protezioni di sicurezza predefinite molto più solide per il computer host
2. Supportano qualsiasi sistema operativo tra i più diffusi e le configurazioni di applicazioni
3. Dispongono di ecosistemi di strumenti consolidati per il comando e il controllo
4. Forniscono esecuzione hello contenitori toohost ambiente

ultimo elemento Hello è importante, poiché un'applicazione indipendente richiede comunque un sistema operativo specifico e il tipo di CPU, seconda chiamate hello applicazione hello verranno eseguite. È importante tooremember installare contenitori nelle macchine virtuali perché contengono applicazioni hello da toodeploy; i contenitori non sono sostituzioni per le macchine virtuali o i sistemi operativi.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Confronto a livello generale delle funzionalità delle VM e dei contenitori
Hello nella tabella seguente vengono descritti in un elevato le differenze di tipo hello livello di funzionalità che&mdash;senza molto lavoro supplementare&mdash;esiste tra macchine virtuali e Linux contenitori. Si noti che potrebbe essere più o meno consigliabile seconda applicazione necessita di alcune funzionalità e che come con tutti i software, un lavoro aggiuntivo offre maggiore supporto di funzionalità, in particolare nell'area di hello di sicurezza.

| Funzionalità | VM | Contenitori |
|:--- | --- | --- |
| Supporto alla sicurezza "predefinito" |livello più elevato tooa |tooa livello leggermente inferiore |
| Memoria su disco richiesta |Sistema operativo completo più app |Solo requisiti app |
| Tempo impiegato toostart |Notevolmente più lungo: avvio del sistema operativo più caricamento app |Sostanzialmente più breve: solo le app devono toostart perché kernel è già in esecuzione |
| Portabilità |Portabile con preparazione adeguata |Portabile in formato di immagine; in genere più ridotto |
| Automazione dell’immagine |Varia notevolmente a seconda del sistema operativo e delle app |[Registro di Docker](https://registry.hub.docker.com/); altri |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Creazione e gestione di gruppi di VM e contenitori
A questo punto, qualsiasi architetto, sviluppatore o specialista in operazioni IT potrebbe pensare: "Posso automatizzare TUTTO questo; questo è davvero Data-Center-As-A-Service!".

È vero, può essere, e vi sono un numero qualsiasi di sistemi, molti dei quali sia già disponibile, che è possibile gestire i gruppi di macchine virtuali di Azure e inserire il codice personalizzato tramite script, spesso con hello [CustomScriptingExtension per Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) o Hello [CustomScriptingExtension per Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). È possibile&mdash;e probabilmente l'operazione è già stata eseguita&mdash;automatizzare le distribuzioni di Azure usando gli script di PowerShell o dell'interfaccia della riga di comando di Azure.

Queste funzionalità sono spesso quindi tootools migrati come [Puppet](https://puppetlabs.com/) e [Chef](https://www.chef.io/) tooautomate hello creazione di e configurazione per le macchine virtuali su larga scala. (Di seguito sono riportati alcuni collegamenti troppo[utilizzando questi strumenti con Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Modelli di gruppo di risorse di Azure
Più di recente, Azure rilasciata hello [Gestione risorse di Azure](../articles/resource-manager-deployment-model.md) API REST e toouse di strumenti di PowerShell e CLI di Azure aggiornato è facilmente. È possibile distribuire, modificare o ridistribuire le topologie di tutta l'applicazione tramite [modelli di gestione risorse di Azure](../articles/resource-group-authoring-templates.md) all'utilizzo di API di gestione risorse di Azure hello:

* Hello [portale di Azure utilizzando i modelli](https://github.com/Azure/azure-quickstart-templates)&mdash;hint, utilizzare il pulsante di "DeployToAzure" hello
* Hello [CLI di Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Distribuzione e gestione di interi gruppi di VM di Azure e contenitori
Esistono diversi sistemi più diffusi che consentono di distribuire interi gruppi di VM e installare Docker (o altri sistemi host Linux per contenitori ) su di essi come gruppo automatizzabile. Per collegamenti diretti, vedere hello [contenitori e gli strumenti](#containers-and-vm-technologies) sezione di seguito. Esistono diversi sistemi che eseguono questa misura maggiore o minore di tooa e questo elenco non è completo. A seconda delle proprie competenze e scenari, essi possono essere o meno utili.

Docker mette a disposizione un proprio set di strumenti per la creazione di VM ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) e uno strumento di gestione del cluster del contenitore Docker per il bilanciamento del carico ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Inoltre, hello [Docker di Azure VM Extension](https://github.com/Azure/azure-docker-extension/blob/master/README.md) fornito con il supporto predefinito per [ `docker-compose` ](https://docs.docker.com/compose/), che è possibile distribuire configurato contenitori di applicazioni in più contenitori.

Inoltre, è possibile provare il [Data Center Operating System (DCOS) di Mesosphere](http://docs.mesosphere.com). DCOS si basa sull'hello open source [mesos](http://mesos.apache.org/) "kernel sistemi distribuiti" che consente di tootreat è il Data Center come un servizio indirizzabile. DCOS mette a disposizione pacchetti predefiniti per diversi importanti sistemi come [Spark](http://spark.apache.org/) e [Kafka](http://kafka.apache.org/) (e altri), nonché servizi predefiniti come [Marathon](https://mesosphere.github.io/marathon/) (un sistema di controllo dei contenitori) e [Chronos](https://mesos.github.io/chronos/) (un'utilità di pianificazione distribuita). Mesos è nata attraverso le lezioni apprese con Twitter, AirBnb e altre aziende di scala web. È inoltre possibile utilizzare **swarm** come motore di orchestrazione hello.

Inoltre, [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) è un sistema open source per la gestione di gruppi di VM e contenitori derivato dalle lezioni apprese con Google. È anche possibile usare [kubernetes con intreccio il supporto di rete tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) è open "Platform-as-a-Service" (PaaS) che rende facile toodeploy di origine e la gestione delle applicazioni nel server. Deis si basa su Docker e CoreOS tooprovide un leggero PaaS con un flusso di lavoro ispirati Heroku.

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), una distribuzione Linux con un footprint ottimizzato, supporto Docker e un proprio sistema contenitore denominato [rkt](https://github.com/coreos/rkt), mette anche a disposizione uno strumento di gestione del gruppo di contenitori denominato [fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu, un'altra distribuzione Linux molto diffuso, supporta Docker molto bene, ma supporta anche [Linux clusters (in stile LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Strumenti per lavorare con VM di Azure e contenitori
Per lavorare con i contenitori e le VM di Azure sono necessari degli strumenti. In questa sezione fornisce un elenco di solo alcuni dei concetti più importanti o utili di hello e gli strumenti sui contenitori, gruppi e la configurazione più grande di hello e strumenti di orchestrazione con cui vengono usati.

> [!NOTE]
> Quest'area viene modificato incredibilmente rapidamente e mentre il migliore tookeep verranno eseguite in questo argomento e i relativi collegamenti backup toodate, potrebbe essere anche un'attività Impossibile. Assicurarsi che si effettuano ricerche in interessanti tookeep soggetti backup toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Tecnologie per i contenitori e le VM
Alcune tecnologie per i contenitori di Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS e rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Link ai contenitori Windows:

* [Contenitori Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Link a Visual Studio Docker:

* [Visual Studio Tools per Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Strumenti di Docker:

* [Daemon docker](https://docs.docker.com/installation/#installation)
* Client di Docker
  * [Windows Docker Client su Chocolatey](https://chocolatey.org/packages/docker)
  * [Istruzioni per l’installazione di Docker](https://docs.docker.com/installation/#installation)

Docker su Microsoft Azure:

* [Estensione della VM Docker per Linux in Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Guida dell’utente di Estensione della VM Docker di Azure](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Utilizzo di hello estensione della macchina virtuale Docker da hello interfaccia della riga di comando di Azure (Azure CLI)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Utilizzo di hello estensione della macchina virtuale Docker da hello portale di Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Come macchina di docker toouse in Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Come docker toouse con sciame in Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Introduzione a Docker e Compose in Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Uso di rapidamente un toocreate modello gruppo di risorse di Azure un host Docker in Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [il supporto incorporato per Hello `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) per applicazioni in esso contenute
* [Implementare un registro di Docker privato in Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Distribuzioni Linux ed esempi di Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configurazione, gestione del cluster e orchestrazione del contenitore:

* [Flotta su CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Guida di distribuzione di cluster tooautomated Kubernetes con CoreOS e Intessitura completare](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Visualizzatore Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Data Center Operating System (DCOS) di Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) e [Hudson](http://hudson-ci.org/)

  * [Plug-in dell'agente VM Jenkins per Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [Repository GitHub: plug-in di archiviazione di Jenkins per Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Terze parti: plug-in slave di Hudson per Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Terze parti: plug-in di archiviazione di Hudson per Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Automazione di Azure](https://azure.microsoft.com/services/automation/)

  * [Video: Modalità tooUse automazione di Azure con le macchine virtuali Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Powershell DSC per Linux

  * [Blog: Modalità toodo Powershell DSC per Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: DSC per client Docker](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Passaggi successivi
Vedere [Docker](https://www.docker.com) e [Contenitori Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
