---
title: aaaRun Cassandra con Linux in Azure | Documenti Microsoft
description: Come toorun un Cassandra cluster Linux in macchine virtuali di Azure da un'app Node.js
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Esecuzione di Cassandra con Linux in Azure e accesso da Node.js
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Vedere i modelli di Resource Manager per cluster [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) e [Spark e Cassandra in CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Panoramica
Microsoft Azure è una piattaforma cloud aperta che esegue software sia Microsoft che non Microsoft, inclusi sistemi operativi, server applicazioni, middleware di messaggistica, oltre a database SQL e NoSQL da modelli sia commerciali che open source. La compilazione di servizi resilienti su cloud pubblici, incluso Azure, richiede un'attenta pianificazione e un'architettura mirata sia per i server applicazioni che per i livelli di archiviazione. L'architettura di archiviazione distribuita di Cassandra aiuta a compilare con facilità sistemi a disponibilità elevata a tolleranza di errore del cluster. Cassandra è un database NoSQL con scalabilità cloud gestito da Apache Software Foundation all'indirizzo cassandra.apache.org. Cassandra, essendo scritto in Java, viene eseguito su piattaforme sia Windows che Linux.

lo stato attivo Hello di questo articolo è la distribuzione Cassandra tooshow in Ubuntu come cluster singolo e a più data center di usufruire delle macchine virtuali di Microsoft Azure e le reti virtuali. Hello per carichi di lavoro di produzione con ottimizzazione per la distribuzione di cluster nell'ambito di questo articolo poiché richiede la configurazione disco a più nodi, hello toosupport di modellazione dati e progettazione della topologia ad anello appropriato è necessario replica, la coerenza dei dati, la velocità effettiva e requisiti di disponibilità elevata.

Accetta questo articolo tooshow un approccio fondamentali di compilazione hello cluster Cassandra confrontati Docker, Chef o Puppet che possono rendere hello molto più semplice di distribuzione dell'infrastruttura.  

## <a name="hello-deployment-models"></a>Hello modelli di distribuzione
Rete di Microsoft Azure consente la distribuzione di hello di cluster privata isolato, accesso hello dei quali può essere qualsiasi sicurezza di rete con granularità fine fine tooattain con restrizioni.  Poiché in questo articolo è sulla visualizzazione distribuzione Cassandra hello a un livello di base, non focalizzata sul livello di coerenza hello e progettazione di hello ottimale dell'archiviazione per la velocità effettiva. Ecco hello elenco di requisiti di rete per il cluster del ipotetica:

* I sistemi esterni non possono accedere al database Cassandra da Azure o all'esterno di Azure
* Cluster Cassandra ha toobe dietro il bilanciamento del carico per il traffico thrift
* Distribuire i nodi di Cassandra in due gruppi in ogni data center per una migliore disponibilità del cluster
* Bloccare cluster hello in modo che solo l'applicazione server farm disponga di database di access toohello direttamente
* Nessun endpoint di rete pubblico diverso da SSH
* Ogni nodo di Cassandra richiede un indirizzo IP interno fisso

Cassandra può essere distribuito tooa singola regione di Azure o aree toomultiple in base alle natura distribuita hello del carico di lavoro hello. Modello di distribuzione con più aree può essere sfruttate tooserve gli utenti finali più vicino tooa particolare geography tramite hello stessa infrastruttura Cassandra. Nodo incorporato replica farà del Cassandra sincronizzazione hello di multi-master scrive provenienti da più centri dati e presenta una visualizzazione coerenza di hello tooapplications di dati. Distribuzione con più aree può consentire anche con l'attenuazione dei rischi hello hello più ampie Azure delle interruzioni di servizio. La coerenza perfezionabile e la topologia di replica di Cassandra saranno di aiuto anche per soddisfare diverse esigenze RPO delle applicazioni.

### <a name="single-region-deployment"></a>Distribuzione in un'area singola
Si inizierà con una distribuzione di un'area singola e raccolto hello procedurali nella creazione di un modello con più aree. Reti virtuali di Azure sarà usato toocreate isolato subnet in modo che possono essere soddisfatti i requisiti di sicurezza rete hello indicati in precedenza.  il processo di Hello descritto nella creazione di distribuzione in una singola area hello utilizza Ubuntu 14.04 LTS e 2.08 Cassandra; Tuttavia, il processo di hello può facilmente essere adottato toohello altre varianti di Linux. di seguito Hello sono alcune delle caratteristiche di sistema di distribuzione di un'area singola hello hello.  

**Disponibilità elevata:** hello nodi Cassandra illustrati nella figura 1 vengono distribuiti hello disponibilità tootwo imposta in modo che i nodi di hello vengono distribuiti tra più domini di errore per la disponibilità elevata. Macchine virtuali annotate con ogni set di disponibilità è mappato too2 domini di errore.  Microsoft Azure Usa hello concetto di toomanage di dominio di errore non pianificato all'intervallo di tempo (ad esempio, errori hardware o software) il concetto di hello del dominio di aggiornamento (ad esempio host o guest aggiornamenti del sistema operativo l'applicazione di patch /, gli aggiornamenti dell'applicazione) viene utilizzato per la gestione pianificata tempi di inattività. Vedere [il ripristino di emergenza e disponibilità elevata per applicazioni Azure](http://msdn.microsoft.com/library/dn251004.aspx) per ruolo hello dei domini di errore e di aggiornamento nel conseguire la disponibilità elevata.

![Distribuzione in un'area singola](./media/cassandra-nodejs/cassandra-linux1.png)

Figura 1: Distribuzione in un'area singola

Si noti che in fase di hello della redazione del presente documento, Azure non consente il mapping esplicito hello di un gruppo di dominio di errore specifico tooa macchine virtuali. di conseguenza, anche con il modello di distribuzione hello illustrato nella figura 1, è statisticamente probabile che tutte le macchine virtuali hello può essere mappato tootwo domini di errore anziché quattro.

**Il traffico Thrift di bilanciamento del carico:** librerie client Thrift all'interno di server web hello connettano toohello cluster tramite un servizio di bilanciamento del carico interno. Questa operazione richiede il processo di hello di aggiunta di subnet hello carico interno del servizio di bilanciamento toohello "dati" (vedere Figura 1) nel contesto di hello del servizio cloud hello ospita hello Cassandra cluster. Una volta bilanciamento del carico interno hello è definito, ogni nodo richiede toobe di endpoint con carico bilanciato hello aggiunto con annotazioni hello del set con carico bilanciato con nome del servizio di bilanciamento del carico definito. Per ulteriori dettagli, vedere [Bilanciamento del carico interno di Azure ](../../../load-balancer/load-balancer-internal-overview.md).

**I valori di inizializzazione di cluster:** è importante tooselect hello la maggioranza dei nodi a disponibilità elevata per i valori di inizializzazione di nuovi nodi hello comunicherà con topologia di valore di inizializzazione nodi toodiscover hello del cluster di hello. Un nodo di ogni set di disponibilità è impostato come valore di inizializzazione nodi tooavoid singolo punto di errore.

**Fattore di replica e il livello di coerenza:** della Cassandra compilazione in ingresso a disponibilità elevata e durabilità dei dati è caratterizzata da hello fattore di replica (RF - numero di copie di ogni riga archiviata nel cluster hello) e il livello di coerenza (numero di toobe di repliche letti/scritti prima di restituire il chiamante di hello risultato toohello). Fattore di replica viene specificato durante la creazione di spazio delle CHIAVI (database relazionale per simile tooa) hello mentre il livello di coerenza hello viene specificato durante l'esecuzione di query CRUD hello. Vedere la documentazione Cassandra all'indirizzo [configurazione per garantire l'uniformità](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) per i dettagli di coerenza e la formula hello per il calcolo di quorum.

Cassandra supporta due tipi di modelli di integrità dei dati: coerenza e la coerenza eventuale; Hello fattore di replica e il livello di coerenza verrà determinano se i dati di hello saranno coerenti, non appena un'operazione di scrittura viene completata o sarà possibile alla fine coerente. Ad esempio, specificando QUORUM come livello di coerenza verrà sempre hello assicura i dati coerenza durante qualsiasi livello di coerenza, sotto il numero di hello di repliche toobe scritto come tooattain necessari QUORUM (ad esempio uno) comporta la dei dati alla fine coerente.

cluster di 8 nodi Hello illustrato in precedenza, con un fattore di replica del QUORUM e 3 (2 nodi vengono letti o scritti per coerenza) livello di coerenza di lettura/scrittura, in grado di superare perdita teorico hello di al massimo 1 nodo per ogni replica di gruppo prima dell'avvio dell'applicazione hello hello rilevamento errore hello. Si presuppone che tutti gli spazi di chiave hello sono ben equilibrati le richieste di lettura/scrittura.  di seguito Hello sono parametri hello che verrà utilizzato per il cluster hello distribuito:

Configurazione del cluster Cassandra in un'area singola:

| Parametro cluster | Valore | Osservazioni |
| --- | --- | --- |
| Number of Nodes (N) |8 |Numero totale di nodi nel cluster hello |
| Replication Factor (RF) |3 |Numero di repliche di una determinata riga |
| Consistency Level (Write) |QUORUM[(RF/2) +1) = 2] hello result di hello formula viene arrotondata per difetto |Scrive in hello la maggior parte delle 2 repliche prima risposta hello viene inviato toohello chiamante. replica 3 viene scritto in modo coerente alla fine. |
| Consistency Level (Read) |QUORUM [(RF/2) + 1 = 2] il risultato di hello di hello formula viene arrotondato per difetto |Legge 2 repliche prima di inviare chiamante toohello di risposta. |
| Replication Strategy |NetworkTopologyStrategy: per ulteriori informazioni, vedere [Replica dei dati](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) nella documentazione di Cassandra |Riconosce la topologia di distribuzione hello e inserisce le repliche in nodi in modo che tutte le repliche di hello non finiscono in hello stesso rack |
| Snitch |GossipingPropertyFileSnitch: per ulteriori informazioni, vedere [Snitch](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) nella documentazione di Cassandra |NetworkTopologyStrategy viene utilizzato un concetto di topologia di snitch toounderstand hello. GossipingPropertyFileSnitch offre un migliore controllo per eseguire il mapping di ogni centro toodata nodo e rack. cluster Hello utilizza toopropagate possono quindi queste informazioni. Questo è molto più semplice dinamica tooPropertyFileSnitch relativo di impostazione IP |

**Considerazioni di Azure per Cluster Cassandra:** la funzionalità Macchine virtuali di Microsoft Azure utilizza l'archiviazione BLOB di Azure per la persistenza del disco; Archiviazione di Azure consente di salvare 3 repliche di ciascun disco per garantire una durabilità elevata. Ciò significa che ogni riga di dati inseriti in una tabella Cassandra è già archiviata in 3 repliche e pertanto la coerenza dei dati è già preso in considerazione anche se il fattore di replica (RF) hello è 1. problema principale di Hello con fattore di replica da 1 è che un'applicazione hello subiranno tempi di inattività, anche se un singolo nodo Cassandra ha esito negativo. Tuttavia, se un nodo è inattivo per i problemi di hello (ad esempio hardware, errori di software di sistema) riconosciuti dal Controller di infrastruttura di Azure, verrà eseguito il provisioning un nuovo nodo nel posto mediante hello stessa unità di archiviazione. Provisioning di un nuovo nodo tooreplace hello precedente uno potrebbe richiedere alcuni minuti.  Allo stesso modo per attività di manutenzione pianificate, quali le modifiche del sistema operativo guest, vengono aggiornati Cassandra e modifiche all'applicazione Controller di infrastruttura di Azure esegue gli aggiornamenti dei nodi hello in sequenza nel cluster hello.  Pertanto cluster hello potrebbero verificarsi breve tempo di inattività per le partizioni di alcuni aggiornamenti in sequenza possono richiedere anche verso il basso alcuni nodi contemporaneamente. Tuttavia, non sarà persi a causa di ridondanza dell'archiviazione di Azure predefinita toohello dati hello.  

Per i sistemi distribuiti tooAzure che non richiede la disponibilità elevata (ad esempio, 99,9 circa che è equivalente too8.76 ore/anno, vedere [la disponibilità elevata](http://en.wikipedia.org/wiki/High_availability) per informazioni dettagliate) è in grado di toorun con RF = 1 e livello di coerenza = uno.  Per le applicazioni con requisiti di disponibilità elevata, RF = 3 e livello di coerenza = QUORUM tollerano hello tempi di inattività di uno dei nodi di hello quello delle repliche hello. RF = 1 nelle distribuzioni tradizionali (ad esempio locale) non possono essere utilizzati a causa di toohello possibile perdita di dati derivanti da problemi quali errori del disco.   

## <a name="multi-region-deployment"></a>Distribuzione in più aree
Data center-supporto della replica e il modello di coerenza descritto in precedenza consente alla distribuzione di più aree hello predefinito hello senza hello del Cassandra necessario per qualsiasi strumenti esterni. È piuttosto diverso dai database relazionali tradizionali hello in cui il programma di installazione di hello per il mirroring del database per le scritture più master può essere molto complessa. Cassandra in un'area più imposta consente scenari di utilizzo di hello inclusi hello seguenti:

**Distribuzione basati su prossimità:** applicazioni multi-tenant, con Cancella i mapping di utenti del tenant-a-regione, può essere tratto dalla latenza bassa del cluster con più aree di hello. Ad esempio una gestione learning sistemi per istituti di istruzione possono distribuire un cluster distribuito in Stati Uniti orientali e Stati Uniti occidentali aree tooserve hello rispettivi campus per transazionale nonché analitica. dati Hello possono localmente coerenti hello ora letture e scritture che possono essere alla fine coerenti in entrambe le aree hello. Sono disponibili altri esempi quali la distribuzione su supporti, e-commerce, e qualsiasi elemento serva alla base utenti concentrata geograficamente è un buon caso di utilizzo per questo modello di distribuzione.

**Disponibilità elevata:** la ridondanza è un fattore chiave per ottenere un'elevata disponibilità di software e hardware; per ulteriori informazioni, vedere la sezione sulla compilazione di sistemi cloud affidabili in Microsoft Azure. In Microsoft Azure, hello unica modalità affidabile per ottenere ridondanza true è la distribuzione di un cluster con più aree. Le applicazioni possono essere distribuite in modalità attivo-attivo o attivo-passivo e se una delle aree di hello è attivo, gestione traffico di Azure è possibile reindirizzare regione attiva toohello di traffico.  Con la distribuzione di un'area singola hello, se è la disponibilità di hello 99,9, una distribuzione con due aree può raggiungere una disponibilità di 99,9999 calcolato dalla formula hello: (1-(1-0.999) * (1-0,999)) * 100); hello di sopra della carta per i dettagli, vedere.

**Ripristino di emergenza:** il cluster Cassandra con più aree, se correttamente progettato, può far fronte a potenziali interruzioni irreversibili del centro. Se un'area è attivo, hello applicazione distribuita tooother aree possono cominciare a gestire gli utenti finali di hello. Analogamente a qualsiasi altre implementazioni continuità aziendale, un'applicazione hello ha toobe a tolleranza di perdita dei dati dei dati di hello nella pipeline asincrona hello. Tuttavia, Cassandra, ripristino hello notevolmente il processo decisionale di hello tempo a disposizione processi di ripristino di database tradizionale. Figura 2 mostra il modello di distribuzione con più aree tipiche hello con otto nodi in ogni area. Entrambe le aree sono immagini di mirror di loro per hello stesso di simmetria; progettazioni reale dipendono dal tipo di carico di lavoro hello (transazionale o analitico, ad esempio), RPO, RTO, la coerenza dei dati e i requisiti di disponibilità.

![Distribuzione in più aree](./media/cassandra-nodejs/cassandra-linux2.png)

Figura 2: Distribuzione di Cassandra con più aree

### <a name="network-integration"></a>Integrazione della rete
Set di macchine virtuali, reti tooprivate distribuito in due aree comunica con altri tramite un tunnel VPN. tunnel VPN Hello connette due gateway software eseguito il provisioning durante il processo di distribuzione di rete hello. Entrambe le aree sono simili architettura di rete in termini di subnet "web" e "dati"; Rete di Azure consente di creare un numero di subnet hello e applicare gli ACL in base alle esigenze di sicurezza di rete. Durante la progettazione della topologia cluster hello tra data center comunicazione latenza e hello impatto economico dell'hello rete traffico necessità toobe considerati.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Coerenza dei dati per la distribuzione in più data center
Distributed toobe necessità di distribuzioni conoscenza dell'impatto di topologia di cluster hello sulla velocità effettiva e disponibilità elevata. Hello RF e livello di coerenza toobe necessità selezionata in modo che hello quorum non dipende dalla disponibilità hello di tutti i centri dati hello.
Per un sistema che richiede coerenza elevata, un LOCAL_QUORUM per il livello di coerenza (per le letture e scritture) per garantire che tale hello locale letture e scritture sono soddisfatti da hello locale nodi mentre i dati sono replicati in modo asincrono toohello data center remoti.  Tabella 2 riepiloga configurazione hello dettagli per cluster con più aree hello descritte più avanti in hello di rivalutazione.

**Configurazione del cluster Cassandra in due aree**

| Parametro cluster | Valore | Osservazioni |
| --- | --- | --- |
| Number of Nodes (N) |8 + 8 |Numero totale di nodi nel cluster hello |
| Replication Factor (RF) |3 |Numero di repliche di una determinata riga |
| Consistency Level (Write) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] risultato hello della formula hello viene arrotondato per difetto |2 nodi verranno scritti toohello primo centro di dati in modo sincrono; Hello aggiuntive 2 nodi necessari per il quorum verranno scritto in modo asincrono toohello 2nd datacenter. |
| Consistency Level (Read) |LOCAL_QUORUM ((RF/2) + 1) = 2 risultato hello della formula hello viene arrotondato per difetto |Richieste di lettura sono soddisfatti da una sola area; 2 nodi vengono lette prima dell'invio risposta hello client toohello indietro. |
| Replication Strategy |NetworkTopologyStrategy: per ulteriori informazioni, vedere [Replica dei dati](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) nella documentazione di Cassandra |Riconosce la topologia di distribuzione hello e inserisce le repliche in nodi in modo che tutte le repliche di hello non finiscono in hello stesso rack |
| Snitch |GossipingPropertyFileSnitch: per ulteriori informazioni, vedere [Snitch](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) nella documentazione di Cassandra |NetworkTopologyStrategy viene utilizzato un concetto di topologia di snitch toounderstand hello. GossipingPropertyFileSnitch offre un migliore controllo per eseguire il mapping di ogni centro toodata nodo e rack. cluster Hello utilizza toopropagate possono quindi queste informazioni. Questo è molto più semplice dinamica tooPropertyFileSnitch relativo di impostazione IP |

## <a name="hello-software-configuration"></a>Hello configurazione SOFTWARE
Hello seguenti versioni del software viene utilizzato durante la distribuzione di hello:

<table>
<tr><th>Software</th><th>Sorgente</th><th>Versione</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Poiché il download di JRE richiede l'accettazione manuale di licenza di Oracle, distribuzione hello toosimplify, download che tutti hello desktop toohello software richiesti per il caricamento in un secondo momento nell'immagine di modello Ubuntu hello che verrà creata come un cluster di toohello precursore distribuzione.

Scaricare hello sopra software in una directory di download noto (ad esempio %TEMP%/downloads in Windows o ~/Downloads nella maggior parte delle distribuzioni di Linux o Mac) nel computer locale hello.

### <a name="create-ubuntu-vm"></a>CREARE UNA MACCHINA VIRTUALE UBUNTU
In questo passaggio del processo di hello è creerà Ubuntu immagine con il software prerequisito hello hello immagine può essere riutilizzato per il provisioning di più nodi Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>PASSAGGIO 1: Generare la coppia di chiavi SSH
È necessario un X509 chiave pubblica PEM o DER con codifica a provisioning ora hello Azure. Generare una coppia di chiavi pubblica/privata utilizzando istruzioni hello si trova in che modo tooUse SSH con Linux in Azure. Se si prevede di toouse putty.exe come un client SSH nel server Windows o Linux, è necessario tooconvert hello PEM codificato formato tooPPK chiave privata RSA utilizzando puttygen.exe; istruzioni di Hello per questo oggetto sono reperibile in hello sopra la pagina web.

#### <a name="step-2-create-ubuntu-template-vm"></a>PASSAGGIO 2: Creare una macchina virtuale modello Ubuntu
il modello di hello toocreate macchina virtuale, accedere a hello Azure classico hello portale e l'utilizzo seguente sequenza: fare clic su Nuovo, calcolo, macchina virtuale, da raccolta, UBUNTU, Ubuntu Server 14.04 LTS e quindi fare clic sulla freccia a destra di hello. Per un'esercitazione in cui viene descritto come toocreate una VM Linux, vedere Creazione di una macchina virtuale in esecuzione Linux.

Immettere le seguenti informazioni nella schermata di hello "configurazione della macchina virtuale" #1 hello:

<table>
<tr><th>NOME CAMPO              </td><td>       VALORE CAMPO               </td><td>         OSSERVAZIONI                </td><tr>
<tr><td>DATA DI RILASCIO VERSIONE    </td><td> Selezionare una data hello elenco a discesa</td><td></td><tr>
<tr><td>NOME MACCHINA VIRTUALE    </td><td> cass-template                   </td><td> Si tratta di nome host hello di hello VM </td><tr>
<tr><td>LIVELLO                     </td><td> STANDARD                           </td><td> Lasciare l'impostazione predefinita hello              </td><tr>
<tr><td>DIMENSIONE                     </td><td> A1                              </td><td>È necessario seleziona hello che macchina virtuale in base a hello IO; a questo scopo lasciare l'impostazione predefinita di hello </td><tr>
<tr><td> NUOVO NOME UTENTE             </td><td> localadmin                       </td><td> "admin" è un nome utente riservato in Ubuntu 12.xx e versioni successive</td><tr>
<tr><td> AUTENTICAZIONE         </td><td> Fare clic sulla casella di controllo                 </td><td>Selezionare se si desidera toosecure con una chiave SSH </td><tr>
<tr><td> CERTIFICATO             </td><td> nome file del certificato di chiave pubblica hello </td><td> Usare hello chiave pubblica generata in precedenza</td><tr>
<tr><td> Nuova password    </td><td> password complessa </td><td> </td><tr>
<tr><td> Confirm Password    </td><td> password complessa </td><td></td><tr>
</table>

Immettere le seguenti informazioni nella schermata di hello "configurazione della macchina virtuale" #2 hello:

<table>
<tr><th>NOME CAMPO             </th><th> VALORE CAMPO                       </th><th> OSSERVAZIONI                                 </th></tr>
<tr><td> SERVIZIO CLOUD    </td><td> Crea un nuovo servizio cloud    </td><td>Il servizio cloud è un contenitore per le risorse di calcolo come le macchine virtuali</td></tr>
<tr><td> NOME DNS DEL SERVIZIO CLOUD:    </td><td>ubuntu-template.cloudapp.net    </td><td>Assegnare un nome bilanciamento del carico indipendente dal computer</td></tr>
<tr><td> AREA/GRUPPO DI AFFINITÀ/RETE VIRTUALE </td><td>    Stati Uniti occidentali    </td><td> Selezionare un'area da cui le applicazioni web di accesso cluster Cassandra hello</td></tr>
<tr><td>ACCOUNT DI ARCHIVIAZIONE </td><td>    Usare l'impostazione predefinita.    </td><td>Utilizzare l'account di archiviazione predefinito hello o un account di archiviazione creato in precedenza in una determinata area</td></tr>
<tr><td>Set di disponibilità </td><td>    None </td><td>    Lasciare vuoto</td></tr>
<tr><td>ENDPOINT    </td><td>Usare l'impostazione predefinita. </td><td>    Utilizzare la configurazione SSH predefinito hello </td></tr>
</table>

Fare clic sulla freccia destra, lasciare le impostazioni predefinite hello nella schermata di hello #3 e fare clic su hello "controllo" pulsante toocomplete hello VM processo di provisioning. Dopo alcuni minuti, hello VM con hello name "ubuntu-template" deve essere in uno stato "in esecuzione".

### <a name="install-hello-necessary-software"></a>INSTALLARE il SOFTWARE necessario hello
#### <a name="step-1-upload-tarballs"></a>PASSAGGIO 1: Caricare i file tarball
Tramite scp o pscp, hello copia scaricati in precedenza software troppo ~ directory di download con hello seguendo il formato di comando:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Ripetere hello in precedenza di comando per JRE nonché per bits Cassandra hello.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>PASSAGGIO 2: Preparare la struttura di directory hello ed estrarre gli archivi hello
Accedere a hello macchina virtuale e creare la struttura di directory hello ed estrarre software come un utente con privilegi avanzato tramite script bash hello riportato di seguito:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Se si incolla questo script nella finestra vim, rendere ritorno a capo hello che tooremove restituito ('\r ") utilizzando hello comando seguente:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Passaggio 3: Modificare etc/profile
Aggiungere seguente hello al fine di hello:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Passaggio 4: Installare JNA per i sistemi di produzione
Comando che segue di hello utilizzare sequenza: comando che segue hello installazione jna-3.2.7.jar e jna-piattaforma-3.2.7.jar too/usr/share.java directory sudo apt-get installerà libjna java

Creare collegamenti simbolici nella directory $CASS_HOME/lib in modo che lo script di avvio di Cassandra possa trovare questi file jar:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Passaggio 5: Configurare cassandra.yaml
Modificare cassandra.yaml in ogni configurazione della macchina virtuale tooreflect necessarie per tutte le macchine virtuali hello [è verrà modificare questo durante il provisioning effettivo hello]:

<table>
<tr><th>Nome campo   </th><th> Valore  </th><th>    Osservazioni </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> Utilizza il nome di hello che riflette la distribuzione</td></tr>
<tr><td>listen_address    </td><td>[lasciare vuoto]    </td><td> Eliminare "localhost" </td></tr>
<tr><td>rpc_addres   </td><td>[lasciare vuoto]    </td><td> Eliminare "localhost" </td></tr>
<tr><td>seeds    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Elenco di tutti gli indirizzi IP hello designato come i valori di inizializzazione.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Viene utilizzato da hello NetworkTopologyStrateg per l'inferenza hello data center e rack hello di hello VM</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Passaggio 6: Acquisire l'immagine di macchina virtuale hello
Accedere alla macchina virtuale hello usando nome host hello (hk-CA-template.cloudapp.net) e la chiave privata SSH hello creato in precedenza. Vedere come tooUse SSH con Linux in Azure per i dettagli relativi a come toolog utilizzando hello comando ssh o putty.exe.

Eseguire hello sequenza dell'immagine di hello toocapture azioni seguenti:

##### <a name="1-deprovision"></a>1. Effettuare il deprovisioning
Comando hello "sudo waagent-deprovision + user" tooremove informazioni specifiche sull'istanza di macchina virtuale. Per vedere [come una macchina virtuale Linux tooCapture](capture-image.md) tooUse come modello ulteriori dettagli sul processo di acquisizione immagine hello.

##### <a name="2-shutdown-hello-vm"></a>2: hello arresto VM
Verificare che la macchina virtuale hello è evidenziata e fare clic sul collegamento di arresto hello dalla barra dei comandi nella parte inferiore di hello.

##### <a name="3-capture-hello-image"></a>3: immagine di acquisizione hello
Verificare che la macchina virtuale hello è evidenziata e fare clic sul collegamento di acquisizione hello dalla barra dei comandi nella parte inferiore di hello. Nella schermata successiva hello, assegnare un nome di immagine (ad esempio hk-cas-2-08-ub-14-04-2014071), la descrizione dell'immagine appropriata e fare clic su processo di acquisizione hello toofinish contrassegno "controllo" hello.

L'operazione richiederà alcuni secondi e l'immagine hello deve essere disponibile nella sezione immagini personali della raccolta immagini hello. macchina virtuale di origine Hello verrà eliminati automaticamente dopo l'immagine di hello viene acquisita. 

## <a name="single-region-deployment-process"></a>Processo di distribuzione in un'area singola
**Passaggio 1: Creare una rete virtuale hello** accedere hello portale di Azure e creare una rete virtuale (classica) con gli attributi di hello mostrata nella seguente tabella hello. Vedere [creare una rete virtuale (classico) usando il portale di Azure hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) per i passaggi dettagliati del processo di hello.      

<table>
<tr><th>Nome attributo macchina virtuale</th><th>Valore</th><th>Osservazioni</th></tr>
<tr><td>Nome</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>Region</td><td>Stati Uniti occidentali</td><td></td></tr>
<tr><td>Server DNS</td><td>None</td><td>Ignorare questo attributo perché non si userà un server DNS</td></tr>
<tr><td>Spazio di indirizzi</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>IP iniziale</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Aggiungere hello seguenti subnet:

<table>
<tr><th>Nome</th><th>IP iniziale</th><th>CIDR</th><th>Osservazioni</th></tr>
<tr><td>Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Subnet per farm web hello</td></tr>
<tr><td>data</td><td>10.1.2.0</td><td>/24 (251)</td><td>Subnet per i nodi database hello</td></tr>
</table>

Dati e le subnet Web possono essere protetti tramite i gruppi di sicurezza di rete coverage hello che esula dall'ambito di questo articolo.  

**Passaggio 2: Eseguire il provisioning le macchine virtuali** usando l'immagine di hello creato in precedenza, verrà creato hello seguenti macchine virtuali nel cloud hello server "hk-c-svc-Ovest" e associarle toohello rispettive subnet come illustrato di seguito:

<table>
<tr><th>Nome computer    </th><th>Subnet    </th><th>Indirizzo IP    </th><th>Set di disponibilità</th><th>DC/Rack</th><th>Valore di inizializzazione?</th></tr>
<tr><td>hk-c1-west-us    </td><td>data    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>Sì</td></tr>
<tr><td>hk-c2-west-us    </td><td>data    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>No </td></tr>
<tr><td>hk-c3-west-us    </td><td>data    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Sì</td></tr>
<tr><td>hk-c4-west-us    </td><td>data    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>No </td></tr>
<tr><td>hk-c5-west-us    </td><td>data    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Sì</td></tr>
<tr><td>hk-c6-west-us    </td><td>data    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>No </td></tr>
<tr><td>hk-c7-west-us    </td><td>data    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Sì</td></tr>
<tr><td>hk-c8-west-us    </td><td>data    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>No </td></tr>
<tr><td>hk-w1-west-us    </td><td>Web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
<tr><td>hk-w2-west-us    </td><td>Web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
</table>

Creazione di hello sopra l'elenco di macchine virtuali, è necessario hello seguente processo:

1. Creare un servizio cloud vuoto in una determinata area
2. Creare una macchina virtuale dall'immagine acquisita in precedenza hello e collegarla toohello rete virtuale creata in precedenza. Ripetere questo passaggio per tutte le macchine virtuali hello
3. Aggiungere un servizio cloud toohello di bilanciamento del carico interno e collegarlo subnet toohello "dati"
4. Per ogni macchina virtuale creata in precedenza, aggiungere un endpoint con carico bilanciato per il traffico thrift attraverso un bilanciamento del carico interno di toohello creato in precedenza connesso set con carico bilanciato

Hello sopra processo può essere eseguita utilizzando portale di Azure classico; Utilizzare un computer Windows (usare una macchina virtuale in Azure se non si dispone di una macchina Windows tooa di accesso), usare automaticamente tutte le macchine 8 virtuali hello tooprovision script PowerShell seguente.

**Elenco 1: script di PowerShell per il provisioning delle macchine virtuali**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Passaggio 3: Configurare Cassandra in ogni macchina virtuale**

Accedere hello VM ed effettuare hello seguenti:

* Modificare $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello data center e rack proprietà:
  
       dc =EASTUS, rack =rack1
* Modificare i nodi di inizializzazione tooconfigure cassandra.yaml come indicato di seguito:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Passaggio 4: Avviare le macchine virtuali hello e test hello del cluster**

Log in uno dei nodi di hello (ad esempio hk-c1-occidentale, Stati Uniti) e hello esecuzione seguendo lo stato del comando toosee hello del cluster hello:

       nodetool –h 10.1.2.4 –p 7199 status

È necessario visualizzare hello visualizzazione simili toohello uno di seguito per un cluster di 8 nodi:

<table>
<tr><th>Stato</th><th>Indirizzo    </th><th>chiudi    </th><th>Tokens    </th><th>Owns </th><th>Host ID    </th><th>Rack</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87,81 KB    </td><td>256    </td><td>38,0%    </td><td>Guid (removed)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41,08 KB    </td><td>256    </td><td>68,9%     </td><td>Guid (removed)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55,29 KB    </td><td>256    </td><td>68,8%    </td><td>Guid (removed)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Hello test singolo Cluster di area
Utilizzare hello cluster hello tootest di passaggi seguente:

1. Utilizzando il cmdlet Get-AzureInternalLoadbalancer comandi Powershell di hello, ottenere l'indirizzo IP hello del bilanciamento del carico interno hello (ad esempio  10.1.2.101). sintassi di Hello del comando hello è illustrata di seguito: Get-AzureLoadbalancer – ServiceName "hk-c-svc--Stati Uniti occidentali" [Visualizza i dettagli di hello di bilanciamento del carico interno hello con il relativo indirizzo IP]
2. Log in farm web hello VM (ad esempio hk-w1-occidentale, Stati Uniti) tramite Putty o ssh
3. Eseguire $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Utilizzare hello seguente CQL comandi tooverify se hello cluster sia attivo:
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

È necessario visualizzare una visualizzazione simile hello sotto:

<table>
  <tr><th> customer_id </th><th> firstname </th><th> Lastname </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

Si noti che spazio delle chiavi hello creato nel passaggio 4 utilizza SimpleStrategy con un replication_factor 3. SimpleStrategy è consigliato per le distribuzioni in un data center singolo, NetworkTopologyStrategy invece per le distribuzioni in più data center. Un replication_factor pari a 3 garantirà la tolleranza per gli errori dei nodi.

## <a id="tworegion"> </a>Processo di distribuzione in più aree
Verrà sfruttare una distribuzione di un'area singola hello completata e ripetere hello stessa procedura per installare una seconda area hello. Hello chiave differenza hello singolo e di distribuzione in un'area più è l'installazione di tunnel VPN hello per le comunicazioni tra area; si avvia con installazione di rete hello, effettuare il provisioning di macchine virtuali hello e configurare Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Passaggio 1: Creare una rete virtuale hello in hello area 2a
Accedere al portale di Azure classico hello e creare una rete virtuale con Mostra attributi hello nella tabella hello. Vedere [configurare una rete virtuale nel portale di Azure classico hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) per i passaggi dettagliati del processo di hello.      

<table>
<tr><th>Nome attributo    </th><th>Valore    </th><th>Osservazioni</th></tr>
<tr><td>Nome    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>Region    </td><td>Stati Uniti orientali</td><td></td></tr>
<tr><td>Server DNS        </td><td></td><td>Ignorare questo attributo perché non si userà un server DNS</td></tr>
<tr><td>Configura una VPN Point-to-Site</td><td></td><td>        Ignorare questo attributo</td></tr>
<tr><td>Configura una VPN Site-to-Site</td><td></td><td>        Ignorare questo attributo</td></tr>
<tr><td>Spazio di indirizzi    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>IP iniziale    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Aggiungere hello seguenti subnet:

<table>
<tr><th>Nome    </th><th>IP iniziale    </th><th>CIDR    </th><th>Osservazioni</th></tr>
<tr><td>Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Subnet per farm web hello</td></tr>
<tr><td>data    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Subnet per i nodi database hello</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Passaggio 2: Creazione delle reti locali
Una rete locale nella rete virtuale di Azure è uno spazio di indirizzi proxy che esegue il mapping del sito remoto di tooa tra un cloud privato o un'altra area di Azure. Questo spazio di indirizzi proxy è associata tooa gateway remoto per routing toohello rete direttamente le destinazioni di rete. Vedere [configurare tooVNet una rete virtuale connessione](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) per istruzioni hello sulla connessione di rete virtuale a.

Creare due reti locali per hello seguenti dettagli:

| Nome rete | Indirizzo gateway VPN | Spazio di indirizzi | Osservazioni |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |Durante la creazione di rete locale hello assegnare un segnaposto indirizzo del gateway. indirizzo del gateway reale Hello viene compilata una volta creato il gateway hello. Liberare spazio di indirizzo hello che corrisponde esattamente hello rispettiva rete virtuale remota; In questo caso hello rete virtuale creata in hello area Stati Uniti orientali. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |Durante la creazione di rete locale hello assegnare un segnaposto indirizzo del gateway. indirizzo del gateway reale Hello viene compilata una volta creato il gateway hello. Liberare spazio di indirizzo hello che corrisponde esattamente hello rispettiva rete virtuale remota; In questo caso hello rete virtuale creata in hello area Stati Uniti occidentali. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Passaggio 3: Mappa "Local" rete toohello rispettive reti virtuali
Dal portale di Azure classico hello, selezionare ogni rete virtuale, fare clic su "Configura", selezionare "Connetti toohello locale network" e selezionare hello reti locali per hello seguenti dettagli:

| Rete virtuale | Rete locale |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Passaggio 4: Creare i gateway nella rete virtuale 1 e nella rete virtuale 2
Dal dashboard di hello di entrambe le reti virtuali di hello, fare clic su Crea GATEWAY che verrà attivata gateway VPN hello processo di provisioning. Dopo alcuni minuti hello dashboard di ciascuna rete virtuale deve essere visualizzato l'indirizzo gateway effettivo hello.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Passaggio 5: Le reti "Local" aggiornamento con gli indirizzi del rispettivo "Gateway" hello
Modificare entrambi hello locale tooreplace hello segnaposto gateway IP indirizzo con hello reale indirizzo IP di hello appena effettuato il provisioning gateway delle reti. Utilizzare hello seguenti mapping:

<table>
<tr><th>Rete locale    </th><th>Gateway di rete virtuale</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>Gateway di hk-vnet-west-us</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>Gateway di hk-vnet-east-us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Passaggio 6: Aggiornare la chiave condivisa hello
Utilizzare hello seguente chiave Powershell script tooupdate hello IPSec di ciascun gateway VPN [Usa hello i migliori risultati chiave per entrambi i gateway hello]: Set-AzureVNetGatewayKey - VNetName hk-rete virtuale-est-us - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Set-AzureVNetGatewayKey - VNetName hk-rete virtuale--Stati Uniti occidentali - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Passaggio 7: Hello da rete connessione
Dal portale di Azure classico hello, utilizzare il menu "DASHBOARD" hello della connessione di gateway a gateway entrambi hello reti virtuali tooestablish. Utilizzare le voci di menu "CONNETTI" hello nella barra degli strumenti nella parte inferiore di hello. Dopo pochi minuti hello dashboard deve visualizzare i dettagli della connessione hello graficamente.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Passaggio 8: Creare macchine virtuali hello nell'area #2
Creare l'immagine Ubuntu hello come descritto nella distribuzione in un'area #1 dal seguente hello stessi passaggi o copiare hello immagine VHD file toohello account di archiviazione Azure si trova nell'area #2 e immagine hello. Utilizzare questa immagine e creare hello seguente elenco di macchine virtuali in un nuovo servizio cloud hk-c-svc-est-us:

| Nome computer | Subnet | Indirizzo IP | Set di disponibilità | DC/Rack | Valore di inizializzazione? |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |data |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Sì |
| hk-c2-east-us |data |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |No |
| hk-c3-east-us |data |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |Sì |
| hk-c5-east-us |data |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Sì |
| hk-c6-east-us |data |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |No |
| hk-c7-east-us |data |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Sì |
| hk-c8-east-us |data |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |No |
| hk-w1-east-us |Web |10.2.1.4 |hk-w-aset-1 |N/D |N/D |
| hk-w2-east-us |Web |10.2.1.5 |hk-w-aset-1 |N/D |N/D |

Seguire hello stesso istruzioni come area #1 ma si usa lo spazio degli indirizzi 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Passaggio 9: Configurare Cassandra in ogni VM
Accedere hello VM ed effettuare hello seguenti:

1. Modificare $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello data center rack le proprietà e in formato hello: dc = rack EASTUS = rack1
2. Modificare i nodi di inizializzazione tooconfigure cassandra.yaml: i valori di inizializzazione: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>Passaggio 10: Avviare Cassandra
Accedere a ogni macchina virtuale e avviare Cassandra in background hello eseguendo hello comando seguente: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Hello test Cluster con più aree
A questo punto Cassandra è stato distribuito too16 nodi con 8 nodi in ogni area di Azure. Questi nodi sono in hello in virtù del nome cluster comune hello e configurazione di un nodo di valore di inizializzazione hello del cluster stesso. Utilizzare hello cluster hello tootest di processo seguenti:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Passaggio 1: Ottenere l'indirizzo IP del servizio di bilanciamento di carico interno hello per entrambe le aree hello tramite PowerShell
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    Si noti gli indirizzi IP hello (ad esempio - 10.1.2.101, est - ovest 10.2.2.101) visualizzato.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Passaggio 2: Eseguire hello ovest hello dopo la registrazione in hk-w1--Stati Uniti occidentali
1. Eseguire $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Eseguire i seguenti comandi CQL hello:
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

È necessario visualizzare una visualizzazione simile hello sotto:

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Passaggio 3: Eseguire hello nell'area orientale hello dopo la registrazione in hk-w1-est-us:
1. Eseguire $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Eseguire i seguenti comandi CQL hello:
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

È necessario visualizzare hello stesso visualizzare per l'area occidentale hello:

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

Eseguire alcuni comandi di inserimento più e vedere che quelli ottenere replicata toowest-us fa parte di cluster hello.

## <a name="test-cassandra-cluster-from-nodejs"></a>Testare il cluster Cassandra da Node.js
Utilizzando una delle macchine virtuali Linux hello creato in precedenza nel livello "web" hello, si eseguirà un semplice dati di hello inserita in precedenza tooread script Node.js

**Passaggio 1: Installare Node.js e il client Cassandra**

1. Installare Node.js e NPM
2. Installare il pacchetto di nodi "cassandra-client" con NPM
3. Eseguire lo script al prompt dei comandi della shell hello, che visualizza una stringa json hello di hello recuperato dati seguente hello:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusioni
Microsoft Azure è una piattaforma flessibile che consente l'esecuzione di hello di Microsoft nonché a software open source come illustrato in questo esercizio. Cluster a disponibilità elevata Cassandra può essere distribuito in un singolo data center tramite hello estendendo hello nodi del cluster tra più domini di errore. I cluster Cassandra possono essere distribuiti anche in più area di Azure geograficamente distanti per sistemi a prova di emergenza. Azure e consente contemporaneamente Cassandra hello costruzione di scalabilità, disponibilità elevata e servizi di cloud ripristinabili emergenza necessari da internet oggi aumentare i servizi.  

## <a name="references"></a>Riferimenti
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

