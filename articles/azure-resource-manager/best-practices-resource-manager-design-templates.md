---
title: aaaDesign Azure modelli per soluzioni complesse | Documenti Microsoft
description: Illustra le procedure consigliate per la progettazione di modelli di Azure Resource Manager per scenari complessi
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Modelli di progettazione per modelli di Azure Resource Manager durante la distribuzione di soluzioni complesse
Usando un approccio flessibile basato sui modelli di Azure Resource Manager, è possibile distribuire topologie complesse in modo rapido e coerente. È possibile adattare queste distribuzioni facilmente come core offerte evolvono o varianti di tooaccommodate per scenari di outlier o ai clienti.

Questo argomento fa parte di un white paper di dimensioni maggiori. scaricare hello tooread completo carta, [World classe Azure Resource Manager modelli considerazioni e procedure consigliate di rivelati](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Modelli di combinano i vantaggi di hello di hello sottostante Gestione risorse di Azure con adattabilità hello e migliorare la leggibilità di JavaScript Object Notation (JSON). Utilizzando i modelli, è possibile:

* Distribuire in modo coerente le topologie e i relativi carichi di lavoro.
* Gestire tutte le risorse di un'applicazione contemporaneamente utilizzando gruppi di risorse.
* Applicare l'accesso basato sui ruoli (RBAC) controllo toogrant accesso appropriato toousers, gruppi e servizi.
* Usare le attività di toostreamline associazioni tag, ad esempio fatturazione rollup.

In questo articolo vengono fornite informazioni dettagliate su scenari di utilizzo, architettura e modelli di implementazione identificati durante le sessioni di progettazione e implementazioni reali dei modelli con i clienti di Azure Customer Advisory Team (AzureCAT). Lontano dal academic, questi approcci sono procedure consolidati informati dall'ambiente di sviluppo hello dei modelli per 12 di tecnologie di sistemi operativi basati su Linux top hello, tra cui: Apache Kafka Apache Spark, Cloudera, Couchbase, Hortonworks HDP, DataStax Enterprise con tecnologia Cassandra Apache, Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis e Nagios. 

In questo articolo condivide toohelp queste procedure comprovate progettare modelli di Azure Resource Manager classe world.  

Lavorando con i clienti, è stata identificata una serie di esperienze di utilizzo dei modelli di Resource Manager tra aziende, system integrator (SI) e CSV. Hello sezioni seguenti forniscono una panoramica generale di scenari comuni e i modelli per diversi tipi di cliente.

## <a name="enterprises-and-system-integrators"></a>Aziende e integratori di sistemi
Nelle organizzazioni di grandi dimensioni, si osservano comunemente due consumer di modelli di Resource Manager: team di sviluppo di software interno e IT aziendale. Abbiamo scoperto che scenari hello per hello SIs mappati toohello scenari per le aziende, pertanto hello stesse considerazioni si applicano.

### <a name="internal-software-development-teams"></a>Team di sviluppo di software interno
Se il team sviluppa toosupport software aziendali, modelli forniscono un modo semplice tooquickly distribuire le tecnologie da utilizzare nelle soluzioni di business specifici. È inoltre possibile utilizzare modelli toorapidly creare ambienti di training che consentono di competenze necessarie toogain di membri del team.

È possibile utilizzare modelli come-estendere o comporle tooaccommodate le proprie esigenze. Utilizzando l'associazione di tag all'interno dei modelli, è possibile fornire un riepilogo di fatturazione con varie viste quali team, progetto, utente e formazione.

Le aziende è spesso necessario team di sviluppo software toocreate un modello per la distribuzione uniforme di una soluzione. modello Hello facilita vincoli in modo che alcuni elementi all'interno di tale ambiente rimangono fisse e non possono essere sottoposto a override. Ad esempio, una banca potrebbe richiedere un tooinclude modello RBAC pertanto un programmatore non è possibile modificare una soluzione di servizi bancari account di archiviazione personale toosend dati tooa.

### <a name="corporate-it"></a>IT aziendale
Le organizzazioni IT aziendali in genere utilizzano modelli per la distribuzione di capacità cloud e funzionalità ospitate su cloud.

#### <a name="cloud-capacity"></a>Capacità cloud
Un modo comune per aziendale IT gruppi tooprovide capacità del cloud per i team è con "dimensioni shirt", che sono standard offerta dimensioni piccole, medie e grandi dimensioni. offerte di Hello shirt dimensioni è possono combinare diversi tipi di risorse e le quantità fornendo un livello di standardizzazione che rende possibile toouse modelli. modelli di Hello offrono capacità in modo coerente impone i criteri aziendali e che utilizza tag tooprovide chargeback tooconsuming organizzazioni.

Ad esempio, potrebbe essere necessario tooprovide sviluppo, test o ambienti di produzione all'interno delle quali hello team di sviluppo software possono distribuire le relative soluzioni. ambiente Hello con una topologia di rete predefinite e in cui è possono modificare gli elementi che salve team di sviluppo software, ad esempio le regole che controllano l'accesso toohello internet e dei pacchetti pubblico. È possibile anche i ruoli specifici dell'organizzazione per questi ambienti con diritti di accesso distinti per ambiente hello.

#### <a name="cloud-hosted-capabilities"></a>Funzionalità ospitate nel cloud
È possibile utilizzare modelli toosupport ospitato su cloud funzionalità, tra cui i pacchetti software singolo o composite offerte disponibili toointernal linee di business. Un esempio di offerta combinata è l'analytics-as-a-service, tecnologie di analisi, virtualizzazione e altre tecnologie, fornita in una configurazione ottimizzata e connessa in una topologia di rete predefinita.

Funzionalità ospitato su cloud sono interessate da protezione hello e considerazioni di ruolo definite tramite la capacità del cloud hello offerta in cui sono compilate. Queste funzionalità sono disponibili così come sono oppure come servizio gestito. Per quest'ultimo hello, vincolato a livello di accesso ai ruoli sono richiesti accesso tooenable nell'ambiente di hello ai fini della gestione.

## <a name="cloud-service-vendors"></a>Fornitori di servizi cloud
Dopo la comunicazione con volumi condivisi cluster toomany, identificate più approcci toodeploy servizi per i clienti e i relativi requisiti.

### <a name="csv-hosted-offering"></a>Offerta ospitata su CSV
Quando l'offerta viene ospitata nella propria sottoscrizione di Azure, sono comunemente adottati due approcci di hosting: distribuzione di una implementazione distinta per ogni cliente o distribuzione di unità di scala che supportano un'infrastruttura condivisa usata per tutti i clienti.

* **Distribuzioni distinte per ogni cliente.** Le distribuzioni distinte per ogni cliente richiedono topologie fisse di configurazioni note differenti. Queste distribuzioni possono contenere macchine virtuali (VM) di dimensioni differenti, un numero variabile di nodi e volumi diversi di memoria associata. L'associazione di tag alle distribuzioni è utilizzata per i roll-up di fatturazione per ogni cliente. RBAC può essere abilitato tooallow clienti accesso tooaspects del proprio ambiente cloud.
* **Unità di scala in ambienti multi-tenant condivisi.** Un modello può rappresentare un'unità di scala per ambienti multi-tenant. In questo caso, hello stessa infrastruttura è toosupport utilizzati tutti i clienti. le distribuzioni di Hello rappresentano un gruppo di risorse che forniscono un livello di capacità per hello ospitato offerta, ad esempio numero di utenti e numero di transazioni. Tali unità di scala sono aumentate o diminuite secondo necessità.

### <a name="csv-offering-injected-into-customer-subscription"></a>Offerta CSV inserita nella sottoscrizione del cliente
È opportuno toodeploy il software in sottoscrizioni appartenenti a clienti finali. È possibile utilizzare modelli toodeploy distinti le distribuzioni di Azure conto del cliente.

Le distribuzioni utilizzano RBAC, pertanto è possibile aggiornare e gestire la distribuzione di hello all'interno di account del cliente hello.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise e vendere le offerte tramite un marketplace, ad esempio Azure Marketplace, è possibile sviluppare tipi distinti di modelli toodeliver delle distribuzioni in esecuzione in account di Azure di un cliente. Queste distribuzioni distinte possono essere descritte in genere come taglia (small, medium, large), tipo di prodotto/pubblico (community, sviluppatore, grande impresa) o tipo di funzionalità (di base, disponibilità elevata).  In alcuni casi, questi tipi consentono di toospecify alcuni attributi di distribuzione di hello, ad esempio il tipo di macchina virtuale o il numero di dischi.

## <a name="oss-projects"></a>Progetti OSS
All'interno dei progetti di origine aperti, modelli di gestione risorse abilitare una soluzione rapidamente mediante procedure comprovate toodeploy una community. È possibile archiviare i modelli in un repository di GitHub in modo community hello possibile correggerle nel tempo. Gli utenti distribuiscono questi modelli nelle proprie sottoscrizioni di Azure.

Hello nelle sezioni seguenti identificano hello utili tooconsider prima di progettare la soluzione.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Identificazione degli elementi esterni e interni di una VM
Quando si progetta il modello, è utile toolook requisiti hello in termini di novità esternamente e internamente hello le macchine virtuali (VM):

* Di fuori di conseguenza hello macchine virtuali e altre risorse della distribuzione, ad esempio di topologia di rete hello, assegnazione di tag, riferimenti toohello certificati/i segreti e controllo di accesso basato sui ruoli. Tutte queste risorse fanno parte del modello.
* Configurazione di stato interno significa hello software installato e complessiva desiderato. Altri meccanismi, ad esempio le estensioni di VM o gli script, vengono utilizzati in tutto o in parte. Questi meccanismi possono essere individuati ed eseguiti dal modello hello ma non sono in essa contenuti.

Esempi comuni di attività che si voglia agire "casella hello" includono:  

* Installare o rimuovere funzionalità e ruoli del server
* Installare e configurare il software a livello di nodo o un cluster di hello
* Distribuire siti Web in un server Web
* Distribuire schemi di database
* Gestire il registro di sistema o altri tipi di impostazioni di configurazione
* Gestire file e directory
* Avviare, arrestare e gestire processi e servizi
* Gestire account utente e gruppi locali
* Installare e gestire i pacchetti (file con estensione .msi, .exe, yum e così via)
* Gestire le variabili di ambiente
* Eseguire gli script nativi (Windows PowerShell, bash e così via)

### <a name="desired-state-configuration-dsc"></a>Configurazione dello stato desiderato (DSC)
Pensando di stato interno di hello delle macchine virtuali oltre la distribuzione, si desidera che la distribuzione non "dello sfasamento" dalla configurazione hello è definito e archiviato nel controllo del codice sorgente toomake. Questo approccio assicura che gli sviluppatori o personale addetto alle operazioni non rendere l'ambiente di tooan modifiche ad hoc che non esaminato, testare o registrato nel controllo del codice sorgente. Questo controllo è importante, perché le modifiche manuali hello non sono presenti nel controllo del codice sorgente. Non sono inoltre parte della distribuzione standard di hello e avrà un impatto sulle distribuzioni automatiche future di software hello.

Oltre che dal punto di vista dei dipendenti interni, la configurazione dello stato desiderato è importante anche in termini di sicurezza. Pirati informatici regolarmente sta toocompromise e sfruttare i sistemi software. Quando ha esito positivo, è il file tooinstall comuni e in caso contrario modificare lo stato di hello di un sistema compromesso. Usa configurazione dello stato desiderato, è possibile identificare delta tra hello desiderato e lo stato effettivo e il ripristino di una configurazione conosciuta.

Sono presenti estensioni di risorsa hello più diffusi meccanismi per DSC - PowerShell DSC, Chef e Puppet. Ognuna di queste estensioni possa distribuire stato iniziale di hello della macchina virtuale e anche essere utilizzati toomake che hello desiderato lo stato viene mantenuto.

## <a name="common-template-scopes"></a>Ambiti dei modello comuni
Nella nostra esperienza, abbiamo visto emergere tre ambiti principali per i modelli di soluzioni. Questi tre ambiti: capacità, funzionalità e soluzioni end-to-end: vengono descritte in hello le sezioni seguenti.

### <a name="capacity-scope"></a>Ambito di capacità
Un ambito di capacità offre un set di risorse in una topologia standard che è preconfigurato toobe in conformità con i criteri e normative. esempio di Hello più comune consiste nel distribuire un ambiente di sviluppo standard in uno scenario IT dell'organizzazione o SI.

### <a name="capability-scope"></a>Ambito di funzionalità
Un ambito di funzionalità è incentrato sulla distribuzione e configurazione di una topologia per una determinata tecnologia. Scenari comuni includono tecnologie quali SQL Server, Cassandra, Hadoop.

### <a name="end-to-end-solution-scope"></a>Ambito di soluzione end-to-end
Un ambito della soluzione End-to-End oltre una singola funzionalità di destinazione è invece incentrato sulla fornitura di una soluzione di tooend end costituita da più funzionalità.  

Un ambito di modello con ambito soluzione si manifesta come un set di uno o più modelli con ambito funzionalità con risorse, logica e stato desiderato specifici della soluzione. Un esempio di un modello di soluzione con ambito è un modello di soluzione fine tooend dati pipeline. modello Hello può combinare topologia specifici della soluzione e lo stato con diversi modelli di soluzione con ambito di funzionalità, ad esempio Kafka Storm e Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Scelta del formato libero rispetto a configurazioni note
Si pensi inizialmente un modello deve fornire i consumer flessibilità massima hello, ma in considerazione numerosi fattori influiscono sulla scelta di hello se le configurazioni in formato libero toouse e configurazioni note. In questa sezione identifica i requisiti del cliente chiave hello e considerazioni tecniche a data shaping approccio hello condiviso in questo documento.

### <a name="free-form-configurations"></a>Configurazioni in formato libero
Nell'area di hello in formato libero configurazioni audio ideale. Consentono di tooselect un tipo di macchina virtuale e specificare un numero arbitrario di nodi e i dischi per i nodi collegati, e questa operazione come modello tooa parametri. Questo approccio, tuttavia, non è l'ideale per alcuni scenari.

In [dimensioni per le macchine virtuali](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), vengono identificate i diversi tipi di macchine Virtuali hello e le dimensioni disponibili e ogni numero hello di durevole dischi (2, 4, 8, 16, 32) che può essere collegato. Ogni disco collegato fornisce 500 IOPS ed è possibile raggruppare più dischi per ottenere un multiplo di tale numero di IOPS. Ad esempio, di 16 dischi può essere in pool tooprovide 8.000 IOPS. Il pool viene eseguito con la configurazione nel sistema operativo hello, utilizzando gli spazi di archiviazione di Microsoft Windows o un array of inexpensive disks (RAID) in Linux.

Una configurazione in formato libero consente la selezione di hello diverse istanze di macchina virtuale, macchina virtuale di vari tipi e formati per tali istanze, i dischi diversi per il tipo di macchina virtuale, hello e uno o più script contenuto di tooconfigure hello macchina virtuale.

È comune che una distribuzione disponga di più tipi di nodi, ad esempio nodi master e nodi dati, pertanto questa flessibilità viene spesso fornita per ogni tipo di nodo.

Quando si inizia a cluster toodeploy di alcun significato, iniziare toowork con questi scenari complessi. Se sono stati distribuiti un cluster Hadoop, ad esempio, con 8 nodi master nodi 200 dati e in pool 4 dischi collegati in ogni nodo principale e in pool 16 dischi collegati al nodo di dati, è necessario 208 macchine virtuali e 3,232 dischi toomanage.

Un account di archiviazione verrà limitare le richieste che relative 20.000 identificato transazioni al secondo limitare, pertanto è necessario esaminare il partizionamento di account di archiviazione e utilizzare calcoli numero appropriato di hello toodetermine di storage account tooaccommodate questa topologia precedente. Dato numerose hello combinazioni supportate dall'approccio Freeform hello, calcoli dinamici sono necessari toodetermine hello partizionamento appropriato. Hello linguaggio del modello di gestione risorse di Azure non fornisce attualmente le funzioni matematiche, pertanto è necessario eseguire tali calcoli nel codice, la generazione di un modello univoco, a livello di codice con i dettagli appropriati hello.

In scenari di isolamento e IT aziendale, un utente deve mantenere modelli hello e supporta topologie hello distribuito per una o più organizzazioni. Questo sovraccarico aggiuntivo, ovvero configurazioni e modelli differenti per ogni cliente, è tutt'altro che auspicabile.

È possibile utilizzare questi ambienti toodeploy modelli nella sottoscrizione di Azure del cliente, ma entrambi i team IT aziendali e i volumi condivisi cluster in genere distribuirli nelle proprie sottoscrizioni, utilizzando un toobill funzione chargeback ai clienti. In questi scenari, obiettivo hello è toodeploy capacità per più clienti in un pool di sottoscrizioni e le distribuzioni di keep compresse popolate i problemi di sottoscrizione toominimize sottoscrizioni hello, vale a dire altre sottoscrizioni toomanage. Con le dimensioni di distribuzione dinamico raggiungimento di questo tipo di densità richiede un'attenta pianificazione e sviluppo aggiuntive per lo scaffolding lavoro per conto dell'organizzazione hello.

Inoltre, Impossibile creare sottoscrizioni tramite una chiamata API è necessario procedere manualmente tramite il portale di hello. Man mano che aumenta il numero di hello di sottoscrizioni, eventuali problemi di sottoscrizione risultante è richiesto un intervento manuale, non può essere automatizzata. Con così tanta variabilità in dimensioni hello delle distribuzioni, è necessario effettuare il provisioning di toopre un numero di sottoscrizioni manualmente tooensure sottoscrizioni disponibili.

Considerando tutti questi fattori, l'adozione di una configurazione in formato libero risulta meno accattivante che a prima vista.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Configurazioni noto: hello approccio ridimensionamento shirt
Piuttosto che offrono un modello che fornisce la massima flessibilità e le variazioni innumerevoli, nella nostra esperienza un modello comune è tooprovide hello possibilità tooselect noto configurazioni, in effetti, con dimensioni shirt standard, ad esempio sandbox, piccole, medie e grandi dimensioni. Altri esempi di taglie sono le offerte di prodotti, come Community Edition o Enterprise Edition.  In altri casi, potrebbero essere configurazioni specifiche per i carichi di lavoro di una determinata tecnologia, ad esempio map reduce o no sql.

Molteplici organizzazioni IT aziendali, fornitori di OSS e SI oggi rendono disponibili le loro offerte utilizzando questo approccio in ambienti locali virtualizzati (aziende) o come offerte software-as-a-service (SaaS) (CSV e OSV).

Questo approccio fornisce configurazioni note ed efficienti di dimensioni variabili, preconfigurate per i clienti. Senza configurazioni note, utenti finali devono determinare dimensioni di cluster in modo autonomo, fattore nei vincoli di risorse di piattaforma ed eseguire matematiche tooidentify hello risultante partizionamento dell'account di archiviazione e altre risorse (a causa delle dimensioni toocluster e risorse vincoli). Nota le configurazioni consentono ai clienti tooeasily hello selezionare destra magliette, vale a dire, una distribuzione specificata. Inoltre toomaking una migliore esperienza per cliente hello, un numero ridotto di configurazioni note è più facile toosupport e consentono di offrire un livello di densità.

In un approccio di configurazione nota incentrato sulle taglie, la taglia può inoltre contenere un numero variabile di nodi. Ad esempio, una taglia small può contenere dai 3 ai 10 nodi.  magliette Hello verrà progettato tooaccommodate dei nodi too10 e fornire hello selezioni consumer hello possibilità toomake in formato libero di dimensioni massime di toohello identificato.  

Un magliette in base al tipo di carico di lavoro, potrebbe essere in formato libero ulteriori natura in termini di numero hello di nodi che possono essere distribuite ma disporrà del carico di lavoro distinti nodo dimensioni e la configurazione del software hello nel nodo hello.

Dimensioni shirt in base alle offerte di prodotti, ad esempio community o Enterprise, potrebbe essere tipi di risorse distinto e numero massimo di nodi che possono essere distribuite, in genere legati considerazioni toolicensing o la disponibilità di funzionalità tra diverse offerte hello.

È anche possibile aumentare i clienti con varianti univoche utilizzando i modelli basati su JSON hello. In presenza di outlier, è possibile incorporare la pianificazione appropriata hello e considerazioni per lo sviluppo, il supporto e la determinazione dei costi.

Basato su scenari di utilizzo modelli cliente hello e dai requisiti indicati all'inizio di hello di questo documento, è stato identificato un modello per la scomposizione di modello.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Modelli di soluzione con ambito di capacità e funzionalità
Scomposizione fornisce uno sviluppo tootemplate approccio modulare che supporta il riutilizzo, estendibilità, test e gli strumenti. In questa sezione vengono forniti dettagli su come un approccio di scomposizione può essere applicate tootemplates con un ambito di capacità o funzionalità.

In questo caso, un modello principale riceve i valori dei parametri da un consumer di modello, quindi Collega a valle tooseveral tipi di modelli e gli script, come illustrato di seguito. Parametri, variabili statiche e variabili generate sono valori tooprovide utilizzati da e verso i modelli di hello collegato.

![Parametri del modello](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**I parametri vengono passati al modello principale tooa quindi toolinked modelli**

Hello seguendo lo stato attivo sezioni hello tipi di modelli e gli script che viene scomposto un singolo modello. Nelle sezioni Hello vengono presentati gli approcci per il passaggio di informazioni sullo stato tra modelli hello. Insieme a esempi sono descritti i tipi di script ogni modello e hello nell'immagine di hello. Per un esempio contestuale, vedere "Uso combinato: un'implementazione di esempio", più avanti in questo documento.

### <a name="template-metadata"></a>Metadati del modello
I metadati del modello (file metadata.json hello) contengono coppie chiave/valore che descrivono un modello in JSON, che può essere letto da persone e i sistemi software.

![Metadati del modello](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**I metadati del modello sono descritto nel file metadata.json hello**

Gli agenti software possono recuperare file metadata.json hello e pubblicare informazioni hello e un modello di toohello collegamento in una pagina web o directory. Gli elementi includono *itemDisplayName*, *description*, *summary*, *githubUsername* e *dateUpdated*.

Di seguito è riportato un file di esempio nel suo complesso.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Modello principale
modello principale Hello riceve i parametri da un utente, vengono utilizzate le variabili di oggetto complesso che informazioni toopopulate ed esegue modelli hello collegato.

![Modello principale](./media/best-practices-resource-manager-design-templates/main-template.png)

**modello principale Hello riceve parametri da un utente**

Un parametro fornito è un tipo di configurazione, noto anche come parametro di dimensione shirt hello a causa di valori standard, ad esempio, piccole, medie o grandi dimensioni. In pratica è possibile usare questo parametro in diversi modi. Per ulteriori informazioni, vedere "Modello di risorse di configurazione note", più avanti in questo documento.

Alcune risorse vengono distribuite indipendentemente dalla configurazione hello specificata da un parametro di tipo utente. Queste risorse vengono effettuato il provisioning con un modello di risorsa condivisa singolo e sono condivisi da altri modelli, pertanto il modello di risorsa condivisa hello viene eseguito per primo.

Alcune risorse vengono distribuite facoltativamente indipendentemente dalla configurazione hello specificato.

### <a name="shared-resources-template"></a>Modello di risorse condivise
Questo modello offre risorse comuni a tutte le configurazioni note. Contiene la rete virtuale hello, set di disponibilità e altre risorse che sono necessari, indipendentemente dal modello di configurazione hello distribuito.

![Risorse del modello](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Modello di risorse condivise**

Nomi di risorse, ad esempio il nome di rete virtuale hello basati sul modello principale hello. È possibile specificarli come una variabile all'interno di tale modello o ricevere come un parametro dall'utente hello, come richiesto dall'organizzazione.

### <a name="optional-resources-template"></a>Modello di risorse facoltative
modello di risorse facoltativi Hello contiene risorse che vengono distribuite a livello di codice in base al valore di hello del parametro o variabile.

![Risorse facoltative](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Modello di risorse facoltative**

Ad esempio, è possibile utilizzare un tooconfigure modello di risorse facoltativi un jumpbox che consente l'accesso indiretto tooa distribuito ambiente da hello rete Internet pubblica. Utilizzare tooidentify un parametro o variabile se devono essere attivati jumpbox hello e hello *concat* nome della funzione toobuild hello destinazione per il modello di hello, ad esempio *jumpbox_enabled.json*. Il collegamento di modello, è necessario utilizzare hello risultante tooinstall variabile hello jumpbox.

È possibile collegare il modello di risorse facoltativi hello da più posizioni:

* Quando applicabile tooevery distribuzione, creare un collegamento basati su parametri di modello di risorse condivise hello.
* Quando applicabile tooselect noto configurazioni, ad esempio, installare solo nelle distribuzioni di grandi dimensioni, creare un collegamento basati su parametri o sulla variabile dal modello di configurazione hello.

Se una determinata risorsa è facoltativa potrebbe non essere dovute consumer modello hello ma dal provider di modelli di hello. Ad esempio, potrebbe essere necessario toosatisfy un requisito specifico del prodotto o componente aggiuntivo di prodotto (comune per i volumi condivisi cluster) o criteri tooenforce (comuni per SIs e IT aziendale gruppi). In questi casi, è possibile utilizzare una variabile tooidentify se la risorsa hello deve essere distribuita.

### <a name="known-configuration-resources-template"></a>Modello di risorse di configurazione note
Nel modello principale hello, un parametro può essere esposto tooallow hello modello consumer toospecify toodeploy una configurazione desiderata. Spesso, questa configurazione nota usa un approccio basato sulle taglie con un set di dimensioni di configurazione fisse quali sandbox, small, medium e large.

![Risorse di configurazione note](./media/best-practices-resource-manager-design-templates/known-config.png)

**Modello di risorse di configurazione note**

approccio di dimensioni shirt Hello viene in genere utilizzato, ma i parametri di hello possono rappresentare qualsiasi set di configurazione conosciuta. Ad esempio, è possibile specificare un set di ambienti per un'applicazione aziendale, ad esempio sviluppo, test e prodotto. Oppure è possibile utilizzarlo per un servizio cloud per toorepresent diversa scala unità, versioni o configurazioni di prodotto, ad esempio Community, Developer o Enterprise.

Come con il modello di risorsa condivisa hello, le variabili vengono passate modello configurazioni note toohello dal:

* Un utente finale, ovvero parametri hello inviato toohello principale dei modelli.
* Un'organizzazione: hello, ovvero le variabili nel modello principale hello che rappresentano i requisiti interni o i criteri.

### <a name="member-resources-template"></a>Modello di risorse membro
All'interno di una configurazione nota sono spesso inclusi uno o più tipi di nodi membro. Ad esempio, con Hadoop si hanno nodi master e nodi dati. Installando MongoDB, si hanno nodi dati e un arbitro. Distribuendo DataStax, si hanno nodi dati e una VM con OpsCenter installato.

![Risorse membro](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Modello di risorse membro**

Ogni tipo di nodi può avere dimensioni diverse delle macchine virtuali, i numeri di dischi collegati, gli script tooinstall e impostare i nodi di hello, configurazioni di porta per le macchine virtuali hello, numero di istanze e altri dettagli. In modo che ogni tipo di nodo ottenga il proprio modello di risorse di membro, che contiene hello informazioni dettagliate per la distribuzione e configurazione di un'infrastruttura nonché per l'esecuzione di script toodeploy e configurare software all'interno di hello macchina virtuale.

Per le VM, in genere vengono utilizzati due tipi di script, ovvero script ampiamente riutilizzabili e script personalizzati.

### <a name="widely-reusable-scripts"></a>Script ampiamente riutilizzabili
Gli script ampiamente riutilizzabili possono essere impiegati in più tipi di modelli. Uno degli esempi di migliori hello di questi script riutilizzabili ampiamente imposta RAID su Linux toopool dischi e ottenere un numero maggiore di operazioni IOPS. Indipendentemente dal software di hello viene installato nella macchina virtuale hello, questo script fornisce riutilizzo delle procedure comprovate per scenari comuni.

![Script riutilizzabili](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**I modelli di risorse membro possono chiamare script ampiamente riutilizzabili**

### <a name="custom-scripts"></a>Script personalizzati
I modelli chiamano comunemente uno o più script che consentono di installare e configurare il software all'interno delle VM. È stato osservato uno schema comune con le topologie di grandi dimensioni in cui vengono distribuite più istanze di uno o più tipi membro. Per ogni macchina virtuale viene avviato uno script di installazione eseguibile in parallelo, seguito da uno script di configurazione chiamato dopo la distribuzione di tutte le VM (o tutte le VM di un tipo di membro specificato).

![Script personalizzati](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**I modelli di risorse membro possono chiamare script per uno scopo specifico, ad esempio la configurazione della VM**

## <a name="capability-scoped-solution-template-example---redis"></a>Esempio di modello di soluzione con ambito di funzionalità - Redis
tooshow come un'implementazione potrebbe funzionare, esaminiamo un esempio pratico di compilazione di un modello che facilita la distribuzione di hello e configurazione di Redis in dimensioni che vanno shirt standard.  

Per la distribuzione di hello, esistono una serie di risorse condivise (rete virtuale, account di archiviazione, i set di disponibilità) e una risorsa facoltativa (jumpbox). Esistono più configurazioni note rappresentate come taglie (small, medium, large) ma ciascuna con un tipo di nodo singolo. Esistono anche due script specifici per lo scopo (installazione, configurazione).

### <a name="creating-hello-template-files"></a>Creazione di file modello hello
Verrà creato un modello principale denominato azuredeploy.json.

Verrà creato un modello di risorse condivise denominato shared-resources.json

Si crea un modello di risorsa facoltativo tooenable hello di distribuzione di un jumpbox, denominato jumpbox_enabled.json

Redis usa solo un tipo di nodo singolo, in modo che venga creato un unico modello di risorsa membro denominato node-resources.json.

Con Redis, desidera tooinstall ogni singolo nodo e quindi configurare il cluster hello.  Si dispone di script tooaccommodate hello installazione e configurato, redis-cluster-install.sh e redis-cluster-setup.sh.

### <a name="linking-hello-templates"></a>Il collegamento modelli hello
Collegamento di modello modello principale hello collega il modello di risorse condivise toohello crea rete virtuale hello.

Logica viene aggiunto all'interno di consumatori di tooenable hello principale dei modelli di hello modello toospecify se deve essere distribuito un jumpbox. Un *abilitato* valore per hello *EnableJumpbox* parametro indica che hello clienti toodeploy un jumpbox. Quando questo valore viene specificato, il modello di hello concatena *Enabled* come nome di modello di base tooa suffisso per la funzionalità jumpbox hello.

modello principale Hello applica hello *grandi* valore di parametro come nome suffisso tooa modello di base per le dimensioni shirt e quindi usa tale valore in un collegamento di modello out troppo*technology_on_os_large.json*.

topologia Hello è simile al seguente illustrazione.

![Modello di Redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Struttura del modello per un modello di Redis**

### <a name="configuring-state"></a>Configurazione dello stato
Per i nodi nel cluster hello hello, sono disponibili due passaggi stato hello tooconfiguring, rappresentati da script specifico scopo.  Redis le installazioni "cluster redis-install.sh" e "cluster-redis-setup.sh" imposta cluster hello.

### <a name="supporting-different-size-deployments"></a>Supporto di distribuzioni di dimensioni diverse
All'interno di variabili, modello di dimensione shirt hello specifica il numero di hello dei nodi di ogni tipo toodeploy per hello dimensioni specificate (*grandi*). Distribuisce quindi il numero di istanze di macchina virtuale utilizzando i cicli di risorse, fornire nomi univoci tooresources mediante l'aggiunta di un nome di nodo con un numero di sequenza numerica da *copyIndex()*. Che questi passaggi per entrambe le macchine virtuali di area alto e medio, come definito nel modello di nome shirt hello

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Modelli con ambito di soluzione end-to-end e di scomposizione
Un modello di soluzione con ambito di soluzione end-to-end è incentrato sulla fornitura di una soluzione end-to-end.  Questo approccio prevede in genere una composizione di più modelli con ambito di funzionalità con risorse aggiuntive, logica e stato.

Come mostrato nell'immagine di hello riportata di seguito, hello stesso modello utilizzato per i modelli di funzionalità con ambito viene esteso per i modelli con un ambito della soluzione End-to-End.

Un modello di risorse condivise e facoltativo risorse modelli servire hello stessa funzione come capacità hello e funzionalità con ambito approcci di modello, ma hanno come ambito per la soluzione di tooend end hello.

Come soluzione tooend end ambito modelli, inoltre, possono in genere hanno dimensioni shirt, modello di risorse di configurazione noto hello riflette il contenuto richiesto per una determinata configurazione nota della soluzione hello.

modelli di soluzione soluzione tooend toohello pertinenti, nonché modelli di membro di risorse che sono necessari per la soluzione di hello end tooend hello con ambito Hello noto modello di risorse di configurazione collegamenti tooone o altre funzionalità.

Come magliette hello della soluzione hello potrebbe essere diversi da hello singolo funzionalità con ambito di modello, le variabili all'interno di hello noto modello di risorse di configurazione sono utilizzati tooprovide hello i valori appropriati per la soluzione a valle funzionalità con ambita modelli toodeploy hello appropriato magliette.

![End-to-end](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**Hello modello utilizzato per la capacità o modelli di soluzioni di funzionalità con ambito possono essere facilmente esteso per gli ambiti di fine tooend Esplora modello**

## <a name="preparing-templates-for-hello-marketplace"></a>Preparazione di modelli per hello Marketplace
Hello precede immediatamente l'approccio supporta scenari in cui le aziende, SIs e volumi condivisi cluster tooeither si desidera distribuire i modelli di hello o abilitare toodeploy i clienti in modo autonomo.

Un altro scenario desiderato è la distribuzione di un modello tramite il marketplace hello.  Questo approccio di scomposizione funziona per marketplace hello, con alcune piccole modifiche.

Come accennato in precedenza, i modelli possono essere tipi di distribuzione distinto toooffer utilizzato per la vendita nel marketplace hello. Tipi di distribuzioni distinte possono essere le taglie (small, medium, large), il tipo di prodotto/pubblico (community, sviluppatore, grande impresa) o il tipo di funzionalità (di base, disponibilità elevata).

Come indicato di seguito, hello esistente tooend fine soluzione o funzionalità con ambito di modelli può essere facilmente utilizzati toolist hello diverse configurazioni note in marketplace hello.

Hello parametri toohello principale dei modelli vengono innanzitutto modificati tooremove hello denominato tshirtSize in ingresso.

Durante il mapping dei tipi di distribuzione distinto hello toohello noto modello di risorse di configurazione, sarà necessario anche risorse comuni hello e trovare la configurazione hello modello di risorse condivise e potenzialmente quelli nei modelli di risorsa facoltativo.

Se si desidera toopublish marketplace toohello modello, si stabilisce copie distinte del modello principale che sostituisce hello in precedenza disponibili in ingresso parametro della variabile tooa tshirtSize incorporata nel modello di hello.

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Adattamento di una soluzione con ambito di modello per marketplace hello**

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla condivisione dello stato interno e all'esterno di modelli, vedere [condivisione dello stato nei modelli di Azure Resource Manager](best-practices-resource-manager-state.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

