---
title: aaaInstall SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft
description: Come tooinstall SAP HANA in un SAP HANA in Azure (istanza di grandi dimensioni).
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Come tooinstall e configurare SAP HANA (istanze di grandi dimensioni) in Azure

Di seguito sono tooknow alcune definizioni importanti prima di leggere questa Guida. In [Panoramica e architettura di SAP HANA (istanze Large) in Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) vengono illustrate le due classi diverse di istanze Large di Hana con:

- S72, S72m, S144, S144m, S192 e S192m, con cui verrà fatto riferimento hello tooas 'una classe Type' di SKU.
- S384, S384m, S384xm, S576, S768 e S960, con cui verrà fatto riferimento tooas hello 'Class Type II' di SKU.

Identificatore della classe Hello è toobe corso utilizzati hello istanza di grandi dimensioni HANA documentazione tooeventually riferimento toodifferent funzionalità e requisiti di base per gli SKU istanza grande HANA.

Altre definizioni di uso frequente includono:
- **Indicatore di istanza di grandi dimensioni:** uno stack infrastruttura hardware SAP HANA TDI certificate e dedicati toorun le istanze di SAP HANA in Azure.
- **SAP HANA in Azure (istanze di grandi dimensioni):** nome ufficiale per l'offerta di hello in Azure toorun HANA istanze in SAP HANA TDI Certificate hardware che viene distribuito in timbri di istanza di grandi dimensioni in diverse aree di Azure. Hello correlati termine **istanza grande HANA** è l'abbreviazione di SAP HANA in Azure (istanze di grandi dimensioni) e viene ampiamente utilizzata questa Guida alla distribuzione tecnica.


installazione di Hello di SAP HANA è responsabilità dell'utente, è possibile iniziare l'attività hello dopo la consegna di un nuovo SAP HANA nel server di Azure (istanze di grandi dimensioni). E, dopo aver ottenuto stabilita connettività hello tra Azure VNet(s) e hello unità HANA istanza di grandi dimensioni. 

> [!Note]
> Criteri SAP, per l'installazione di hello di SAP HANA deve essere eseguita da una persona Certificate tooperform le installazioni di SAP HANA. Una persona, che ha superato hello Certificate associare tecnologia SAP esame, esami di certificazione di installazione di SAP HANA, o da un certificato SAP integratore (SI).

Controllare di nuovo, specialmente se si pianificano tooinstall 2.0 HANA [&#2235581; nota con il supporto di SAP - SAP HANA: i sistemi operativi supportati](https://launchpad.support.sap.com/#/notes/2235581/E) nell'ordine toomake che tale hello sistema operativo è supportato con SAP HANA hello rilasciare si deciso tooinstall. Si rende conto che hello del sistema operativo supportate per HANA 2.0 ha più restrizioni rispetto hello sistemi operativi supportati per HANA 1.0. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Primi passaggi dopo la ricezione di hello HANA grandi istanza unità

**Primo passaggio** dopo la ricezione hello HANA istanza di grandi dimensioni e possedere istanze toohello accesso e la connettività, è tooregister hello del sistema operativo dell'istanza di hello con il provider del sistema operativo. Questo passaggio include la registrazione del sistema operativo Linux SUSE in un'istanza di SMT SUSE che è necessario toohave distribuito in una macchina virtuale in Azure. unità di istanza di grandi dimensioni HANA Hello possono connettersi istanza SMT toothis (vedere più avanti in questa documentazione). O il sistema operativo RedHat toobe registrato con hello occorre tooconnect di gestione della sottoscrizione di Red Hat. Vedere anche le osservazioni in questo [documento](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Questo passaggio è anche necessario toobe toopatch in grado di hello del sistema operativo. Attività che è responsabilità di hello del cliente hello. Per SUSE, cercare documentazione tooinstall e configurare SMT [qui](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Secondo passaggio** è toocheck per nuove patch e le correzioni di hello specifico del sistema operativo/versione. Controllare se il livello di patch hello dell'istanza di grandi dimensioni HANA hello è stato più recente di hello. In base a temporizzazione immagine del sistema operativo patch/versioni e modifiche toohello che possibile distribuire Microsoft, potrebbero esserci casi in cui la patch più recenti di hello non può essere inclusa. È pertanto obbligatoria dopo l'esecuzione di un'unità, istanza di grandi dimensioni HANA toocheck se patch rilevanti per sicurezza, funzionalità, prestazioni e disponibilità sono state rilasciate nel frattempo dal fornitore Linux particolare hello e necessario toobe applicato.

**Terzo passaggio** è toocheck out hello note SAP rilevanti per l'installazione e configurazione di SAP HANA in hello specifico del sistema operativo/versione. A causa di toochanging indicazioni o modifiche tooSAP note o le configurazioni che dipendono da scenari di installazione, Microsoft non sarà sempre in grado di toohave un'unità di istanza di grandi dimensioni HANA perfettamente configurata. Di conseguenza è obbligatoria per l'utente come un cliente, tooread hello note su SAP correlati tooSAP HANA l'esatta versione di Linux. Inoltre, controllare configurazioni hello hello del sistema operativo/versione necessarie e applicare impostazioni di configurazione hello in cui non è già stato fatto.

In specifico, controllare hello seguenti parametri e infine regolata in base a:

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

A partire da SP1 SLES12 e RHEL 7.2, è necessario impostare questi parametri in un file di configurazione nella directory /etc/sysctl.d hello. Ad esempio, un file di configurazione con nome hello 91-NetApp-HANA.conf deve essere creato. Per le versioni precedenti di SLES e RHEL, questi parametri devono essere impostati in in/etc/sysctl.conf.

Per RHEL tutte le versioni e a partire da SLES12, hello 
- sunrpc.tcp_slot_table_entries = 128

deve essere impostato in in/etc/modprobe.d/sunrpc-local.conf. Se il file hello non esiste, deve innanzitutto creato aggiungendo hello seguente voce: 
- options sunrpc tcp_max_slot_table_entries=128

**Quarto passaggio** è ora di sistema toocheck hello dell'unità istanza HANA grandi dimensioni. le istanze di Hello vengono distribuite con un fuso orario del sistema che rappresentano il percorso di hello di hello area Azure hello in che HANA grandi indicatore dell'istanza si trova. Si è ora di sistema hello toochange libero o il fuso orario di istanze di hello che si è proprietari. In questo modo e ordinamento delle altre istanze nel tenant, preparato che è necessario tooadapt hello fuso orario di hello appena recapitati istanze. Le operazioni di Microsoft non hanno approfondite fuso orario del sistema hello impostate con le istanze di hello dopo il passaggio di hello. Di conseguenza le istanze appena distribuite potrebbero non essere impostate in hello stesso fuso orario come hello uno è stato cambiato in. Di conseguenza, è responsabilità toocheck cliente e se è necessario adattare hello fuso orario di istanze di hello trasmesso. 

**Quinto passaggio** è toocheck via/host. Come ottengano trasmesso i pannelli hello, presentano diversi indirizzi IP assegnati per scopi diversi (vedere la sezione successiva). Controllare il file di ecc/host hello. Nei casi in cui vengono aggiunte unità in un tenant esistente, non è prevista e così via toohave gli host dei sistemi di hello appena distribuito gestiti in modo corretto con indirizzi IP hello dei precedenti sistemi recapitati. Pertanto è compito dell'utente come le impostazioni corrette di cliente toocheck hello, che un'istanza appena distribuita può interagire e risolvere i nomi di hello unità precedentemente distribuito nel tenant. 

## <a name="networking"></a>Rete
Si suppone che siano seguite indicazioni hello progettare le reti virtuali di Azure e connessione alle istanze di grandi dimensioni di reti virtuali toohello HANA come descritto in questi documenti:

- [Panoramica e architettura di SAP HANA (istanze di grandi dimensioni) in Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infrastruttura e connettività a SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Esistono alcuni dettagli degni toomention sulle reti hello di singole unità hello. Ogni unità di istanza di grandi dimensioni HANA dotato di due o tre indirizzi IP assegnati tootwo o tre porte NIC dell'unità di hello. Tre indirizzi IP vengono utilizzati in configurazioni con scalabilità orizzontale HANA e uno scenario di replica DFS HANA hello. Uno degli indirizzi IP hello assegnato toohello NIC dell'unità hello rientra hello pool IP del Server che è stato descritto in hello [architettura in Azure e SAP HANA (istanza di grandi dimensioni) Panoramica](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

distribuzione di Hello per le unità con due indirizzi IP assegnati dovrebbe essere simile:

- eth0.xx deve avere un indirizzo IP assegnato non compreso nell'intervallo di indirizzi del Pool di IP di Server che è stato inviato tooMicrosoft hello. Questo indirizzo IP deve essere utilizzato per la gestione di /etc/hosts di hello del sistema operativo.
- eth1.xx deve avere un indirizzo IP assegnato utilizzato per la comunicazione tooNFS. Pertanto, questi indirizzi non **non** necessario toobe mantenute in via/host ordine tooallow istanza tooinstance del traffico tenant hello.

Una configurazione del pannello con due indirizzi IP assegnati non è appropriata per i casi di distribuzione di tipo replica del sistema HANA o di HANA con scalabilità orizzontale. Se con due indirizzi IP assegnati solo e che si voglia toodeploy tale configurazione, contattare SAP HANA nella gestione del servizio Azure tooget un terzo di indirizzi IP in una terza VLAN assegnato. Per le unità HANA istanza di grandi dimensioni con tre indirizzi IP assegnati in tre porte NIC, hello utilizzo applicate regole seguenti:

- eth0.xx deve avere un indirizzo IP assegnato non compreso nell'intervallo di indirizzi del Pool di IP di Server che è stato inviato tooMicrosoft hello. Pertanto questo indirizzo IP non deve essere utilizzato per la gestione di /etc/hosts di hello del sistema operativo.
- eth1.xx deve avere un indirizzo IP assegnato utilizzato per l'archiviazione tooNFS di comunicazione. Questo tipo di indirizzi, quindi, non deve essere conservato in etc/host.
- eth2.xx devono essere esclusivamente utilizzati toobe mantenute in via/host per la comunicazione tra istanze diverse di hello. Questi indirizzi sarebbe inoltre hello indirizzi IP mantenuto in configurazioni con scalabilità orizzontale HANA come indirizzi IP che HANA utilizza per la configurazione tra i nodi hello toobe.



## <a name="storage"></a>Archiviazione

Hello layout di archiviazione per SAP HANA in Azure (istanze di grandi dimensioni) è configurata per SAP HANA sulla gestione dei servizi di Azure tramite SAP consigliata le linee guida, come documentato nel [i requisiti di archiviazione di SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper relativo alle. Hello approssimative dimensioni dei volumi diversi hello con hello diverse SKU di istanze di grandi dimensioni HANA ottenuto documentati in [architettura in Azure e SAP HANA (istanza di grandi dimensioni) Panoramica](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Nella hello nella tabella seguente sono elencate le convenzioni di denominazione Hello hello di volumi di archiviazione:

| Utilizzo delle risorse di archiviazione | Nome del montaggio | Nome del volume | 
| --- | --- | ---|
| Dati HANA | /hana/data/SID/mnt0000<m> | Storage IP:/hana_data_SID_mnt00001_tenant_vol |
| Log HANA | /hana/log/SID/mnt0000<m> | Storage IP:/hana_log_SID_mnt00001_tenant_vol |
| Backup dei log HANA | /hana/log/backups | Storage IP:/hana_log_backups_SID_mnt00001_tenant_vol |
| Condivisione HANA | /hana/shared/SID | Storage IP:/hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | Storage IP:/hana_shared_SID_mnt00001_tenant_vol/usr_sap |

In cui SID = hello HANA instance ID di sistema 

Tenant corrisponde a un'enumerazione interna delle operazioni durante la distribuzione di un tenant.

Come si può notare, condividono HANA condiviso e usr/sap hello stesso volume. nomenclatura Hello dei punti di montaggio hello includono l'ID di sistema di istanze HANA hello, nonché il numero di montaggio hello hello. Nelle distribuzioni con aumento delle prestazioni è disponibile un solo montaggio, ad esempio mnt00001. Nelle distribuzioni con scalabilità orizzontale, invece, il numero di montaggi corrisponde al numero di nodi di lavoro e nodi master. Per l'ambiente di scalabilità orizzontale hello, i dati del log, volumi di backup di log sono condivisi e collegate tooeach nodo nella configurazione di scalabilità orizzontale hello. Per le configurazioni che eseguono più istanze SAP, un set di volumi diversi è unità di istanza di grandi dimensioni HAN toohello creato e collegato.

Durante la lettura carta hello e cerca un'unità di istanza di grandi dimensioni HANA, si rende conto che unità hello forniti con il volume di disco anziché più elastico per HANA/dati e che è associato ad alcun volume HANA / / backup del log. motivo di Hello perché è ridimensionato hello HANA/dati talmente grandi è che gli snapshot di archiviazione hello che offriamo per un cliente in uso hello stesso volume del disco. Hello significa che più snapshot di archiviazione che si eseguono, hello più lo spazio è usato dagli snapshot nei volumi di archiviazione assegnato. Hello HANA / / backup del log è non pensiero toobe hello volume tooput i backup di database in. È di dimensioni toobe utilizzato come volume di backup per i backup del log delle transazioni HANA hello. Nelle future versioni di archiviazione hello snapshot snapshot di modalità self-service, che si utilizzerà toohave questo volume specifico più frequenti. E con quelle più frequenti sito di ripristino di emergenza toohello repliche se lo si desidera toooption-in per la funzionalità di ripristino di emergenza hello fornite dall'infrastruttura di istanza di grandi dimensioni HANA hello. Per informazioni dettagliate, vedere [Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze Large) in Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Inoltre toohello archiviazione fornito, è possibile acquistare capacità di archiviazione aggiuntivo in incrementi di 1 TB. Questo ulteriore spazio di archiviazione può essere aggiunti come nuovi volumi tooa HANA istanze di grandi dimensioni.

Durante il caricamento con SAP HANA sulla gestione dei servizi di Azure, il cliente hello specifica un ID utente (UID) e l'ID di gruppo (GID) per il gruppo di utenti e sapsys sidadm hello (ex: 1000,500) è necessario durante l'installazione del sistema SAP HANA hello, vengono utilizzati questi stessi valori. Come si desidera toodeploy più istanze HANA in un'unità, è possibile ottenere più set di volumi (un set per ogni istanza). Di conseguenza, al momento della distribuzione è necessario toodefine:

- Hello SID di hello diverse HANA istanze (sidadm derivato esplicitamente).
- Dimensioni di memoria di diverse istanze HANA hello. Poiché le dimensioni di memoria hello per le istanze definisce le dimensioni di hello dei volumi di hello in ogni set di volumi singolo.

In base alle raccomandazioni di provider di archiviazione hello montaggio le opzioni seguenti è configurato per tutti i volumi montati (esclude avvio LUN):

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

Questi punti vengono configurati nella fstab/e così via, ad esempio hello illustrato nel seguente grafico di montaggio:

![fstab di volumi montati in un'unità di istanze Large di HANA](./media/hana-installation/image1_fstab.PNG)

output di Hello del comando hello df -h in un'unità di istanza di grandi dimensioni HANA S72m sarebbe simile:

![fstab di volumi montati in un'unità di istanze Large di HANA](./media/hana-installation/image2_df_output.PNG)


controller di archiviazione Hello e timbri di grandi dimensioni istanza hello i nodi sono sincronizzati tooNTP server. Con la sincronizzazione hello SAP HANA in unità di Azure (istanze di grandi dimensioni) e macchine virtuali di Azure in un server NTP, non deve esistere alcun problema di deviazione notevole quantità di tempo tra l'infrastruttura di hello e unità di calcolo hello in Azure o istanza di dimensioni elevate timbri.

In ordine toooptimize archiviazione toohello SAP HANA utilizzata di sotto, è necessario impostare anche i seguenti parametri di configurazione di SAP HANA hello:

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
Per le versioni di SAP HANA 1.0 backup tooSPS12, questi parametri possono essere impostati durante l'installazione di hello del database SAP HANA hello, come descritto in [SAP nota #2267798 - configurazione del Database SAP HANA hello](https://launchpad.support.sap.com/#/notes/2267798)

È anche possibile configurare parametri hello dopo l'installazione del database SAP HANA hello tramite hello hdbparam framework. 

In SAP HANA 2.0 framework hdbparam hello è stato deprecato. Di conseguenza è necessario impostare i parametri di hello utilizzando i comandi SQL. Per informazioni dettagliate, vedere [SAP Note #2399079: Elimination of hdbparam in HANA 2](https://launchpad.support.sap.com/#/notes/2399079) (Nota SAP #2399079: eliminazione di hdbparam HANA 2).


## <a name="operating-system"></a>Sistema operativo

Lo spazio di swapping di hello recapitato immagine del sistema operativo è impostato too2 GB in base toohello [&#1999997; nota con il supporto di SAP - domande frequenti: SAP HANA memoria](https://launchpad.support.sap.com/#/notes/1999997/E). Un'impostazione diversa desiderato deve toobe impostati dall'utente come un cliente.

[SUSE Linux Enterprise Server 12 SP1 per le applicazioni SAP](https://www.suse.com/products/sles-for-sap/hana) hello la distribuzione di Linux installato per SAP HANA in Azure (istanze di grandi dimensioni). Questa distribuzione particolare fornisce funzionalità di SAP &quot;predefinito hello&quot; (inclusi i parametri preimpostati per l'esecuzione in modo efficace di SAP in SLES).

Vedere [risorse libreria/White paper](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) nel sito Web SUSE hello e [SAP in SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) su hello SAP Community rete (SCN) per varie risorse utili relative toodeploying SAP HANA in SLES (tra cui hello configurazione della disponibilità elevata, le operazioni di protezione avanzata tooSAP specifico e altro ancora).

Collegamenti aggiuntivi utili correlati a SAP in SUSE:

- [Sito relativo a SAP HANA in SUSE Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113) (Procedura consigliata per SAP: replica di accodamento e SAP NetWeaver in SUSE Linux Enterprise 12).
- [ClamSAP: SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (ClamSAP: protezione da virus SLES per SAP), incluso SLES 12 for SAP Applications

SAP tooimplementing applicabile note sul supporto per SAP HANA SLES 12:

- [SAP Support Note #1944799 – SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html) (Nota di supporto SAP n. 1944799: linee guida di SAP HANA per l'installazione del sistema operativo SLES)
- [SAP Support Note #2205917 – SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E) (Nota di supporto SAP n. 2205917: impostazioni del sistema operativo consigliate per il database di SAP HANA per SLES 12 for SAP Applications)
- [SAP Support Note #1984787 – SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787) (Nota di supporto SAP n. 1984787 - SUSE Linux Enterprise Server 12: note di installazione)
- [SAP Support Note #171356 – SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787) (Nota di supporto SAP n. 171356: informazioni generali sul software SAP in Linux)
- [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Nota di supporto SAP n. 1391070: soluzioni UUID Linux)

[Red Hat Enterprise Linux for SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) è un'altra offerta per l'esecuzione di SAP HANA in istanze di grandi dimensioni di HANA. Sono disponibili le versioni RHEL 6.7 e 7.2. 

Utili collegamenti aggiuntivi correlati a SAP in Red Hat:
- [Sito SAP HANA on Red Hat Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

SAP tooimplementing applicabile note sul supporto per SAP HANA in Red Hat:

- [SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879/E) (Nota di supporto SAP n. 2009879: linee guida di SAP HANA per il sistema operativo Red Hat Enterprise Linux, RHEL)
- [SAP Support Note #2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690) (Nota di supporto n. 2292690 - SAP HANA DB: impostazioni del sistema operativo consigliate per RHEL 7)
- [SAP Support Note #2247020 - SAP HANA DB: Recommended OS settings for RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020) (Nota di supporto n. 2247020 - SAP HANA DB: impostazioni del sistema operativo consigliate per RHEL 6.7)
- [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Nota di supporto SAP n. 1391070: soluzioni UUID Linux)
- [SAP Support Note #2228351 - Linux: SAP HANA Database SPS 11 revision 110 (or higher) on RHEL 6 or SLES 11](https://launchpad.support.sap.com/#/notes/2228351) (Nota di supporto SAP n. 2228351 - Linux: SAP HANA Database SPS 11 revisione 110 (o successiva) in RHEL 6 o SLES 11)
- [SAP Support Note #2397039 - FAQ: SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039) (Nota di supporto SAP n. 2397039 - Domande frequenti: SAP in RHEL)
- [SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410) (Nota di supporto SAP n. 1496410 - Red Hat Enterprise Linux 6.x: installazione e aggiornamento)
- [SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167) (Nota di supporto SAP n. 2002167 - Red Hat Enterprise Linux 7.x: installazione e aggiornamento)

## <a name="time-synchronization"></a>Sincronizzazione degli orari

Le applicazioni SAP basate sull'architettura di SAP NetWeaver hello sono sensibili alle differenze di tempo per vari componenti che costituiscono hello hello sistema SAP. ABAP SAP breve dump con titolo errore hello di ZDATE\_grande\_ora\_DIFF è probabilmente, così come queste breve dump hello ora di sistema di server diversi o macchine virtuali è la deviazione troppo distanti tra loro.

Per SAP HANA in Azure (istanze di grandi dimensioni), la sincronizzazione dell'ora eseguita in Azure &#39; t applicare toohello unità di calcolo in timbri di grandi dimensioni istanza hello. Questa sincronizzazione non è applicabile all'esecuzione delle applicazioni SAP in VM native di Azure, poiché Azure assicura la corretta sincronizzazione dell'ora del sistema. Di conseguenza, una volta server deve essere configurato che può essere utilizzata dal server applicazioni SAP in esecuzione in macchine virtuali di Azure e SAP HANA hello database istanze in esecuzione in istanze di grandi dimensioni HANA. infrastruttura di archiviazione Hello timbri di istanza di grandi dimensioni è ora sincronizzato con i server NTP.

## <a name="setting-up-smt-server-for-suse-linux"></a>Configurazione del server SMT per SUSE Linux
Le istanze di grandi dimensioni di SAP HANA non dispone di connettività diretta toohello Internet. Pertanto, non è un tooregister processo semplice, quali unità con il provider di sistema operativo hello e toodownload e applicare patch. Nel caso di hello di SUSE Linux, una soluzione potrebbe essere tooset di un server SMT in una macchina virtuale di Azure. Mentre hello macchina virtuale di Azure deve toobe ospitato in una rete virtuale di Azure, che è connesso toohello HANA istanza di grandi dimensioni. Con il server tali SMT, unità di istanza di grandi dimensioni HANA hello può registrare e scaricare le patch. 

SUSE fornisce una guida più dettagliata in [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf) (Strumento di gestione delle sottoscrizioni per SLES 12 SP2). 

Come condizione preliminare per l'installazione di un server SMT che svolge attività hello per le istanze di grandi HANA hello, occorre:

- Una rete virtuale di Azure che è connesso toohello circuito Expressroute istanza grande HANA.
- Un account SUSE associato a un'organizzazione. Mentre l'organizzazione hello sarebbe necessario toohave alcuni sottoscrizione SUSE valida.

### <a name="installation-of-smt-server-on-azure-vm"></a>Installazione di un server SMT in una VM di Azure

In questo passaggio è installare server SMT hello in una macchina virtuale di Azure. prima di misura Hello è toolog in toohello [SUSE clienti](https://scc.suse.com/)

Come si è connessi, passare tooOrganization--> le credenziali dell'organizzazione. In questa sezione è necessario trovare credenziali hello che sono necessarie tooset server SMT hello.

terzo passaggio Hello è tooinstall una macchina virtuale Linux SUSE nel hello rete virtuale di Azure. hello toodeploy macchina virtuale, eseguire un'immagine della raccolta SLES 12 SP2 di Azure. Nel processo di distribuzione hello, non definire un nome DNS e non utilizzare indirizzi IP statici, come illustrato in questa schermata

![Distribuzione del server SMT](./media/hana-installation/image3_vm_deployment.png)

Hello macchina virtuale distribuita è stata una VM più piccola e ottenuto l'indirizzo IP interno hello nella rete virtuale di Azure di 10.34.1.4 hello. Nome della macchina virtuale hello è smtserver. Dopo l'installazione di hello, hello connettività toohello HANA grandi unità istanza selezionata. Dipende da come è organizzata la risoluzione dei nomi potrebbe essere necessario risoluzione tooconfigure dell'unità di istanza di grandi dimensioni HANA hello in via/host della macchina virtuale di Azure hello. Aggiungere una macchina virtuale che verrà toobe utilizzato i patch hello toohold di toohello disco aggiuntivo. disco di avvio Hello stesso potrebbe essere troppo piccolo. In caso di hello illustrato, disco hello ottenuto montato troppo/srv/www/htdocs come illustrato nella seguente schermata hello. Dovrebbe essere sufficiente un disco da 100 GB.

![Distribuzione del server SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Log in unità di istanza di grandi dimensioni HANA toohello, mantenere /etc/hosts e verificare se è possibile raggiungere hello macchina virtuale di Azure che si suppone server SMT di hello toorun rete hello.

Dopo questa verifica viene completata correttamente, è necessario toolog nella macchina virtuale di Azure che deve essere eseguita server SMT hello toohello. Se si utilizza toolog putty in toohello VM, è necessario tooexecute questa sequenza di comandi nella finestra di bash:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Dopo avere eseguito questi comandi, riavviare le impostazioni di hello tooactivate bash. Avviare quindi YAST.

In YAST, passare tooSoftware manutenzione e cercare smt. Selezionare smt, che passa automaticamente tooyast2 smt, come illustrato di seguito

![SMT in yast](./media/hana-installation/image5_smt_in_yast.PNG)


Accettare hello per l'installazione in smtserver hello. Una volta installato, andare configurazione del server SMT toohello e immettere le credenziali aziendali di hello di hello SUSE clienti è stato recuperato in precedenza. Inoltre, immettere il nome host macchina virtuale di Azure come hello SMT URL del Server. In questa dimostrazione è https://smtserver visualizzato nel grafico successivo hello.

![Configurazione del server SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Come passaggio successivo, è necessario tootest se hello connessione toohello SUSE clienti funziona. Come illustrato nella seguente grafica, in caso di dimostrazione hello, hello ha esito negativo.

![Test connessione tooSUSE clienti](./media/hana-installation/image7_test_connect.png)

Una volta il programma di installazione SMT hello viene avviato, è necessario tooprovide una password del database. Poiché si tratta di una nuova installazione, è necessario toodefine che la password come illustrato nel grafico successivo hello.

![Definire la password per il database](./media/hana-installation/image8_define_db_passwd.PNG)

è l'interazione Avanti Hello è quando viene creato un certificato. Scorrere finestra di dialogo hello come indicato di seguito e passaggio hello deve continuare.

![Creare un certificato per il server SMT](./media/hana-installation/image9_certificate_creation.PNG)

Potrebbero essere presenti alcuni minuti impiegati nel passaggio hello 'Controllo di eseguire la sincronizzazione' alla fine di hello della configurazione di hello. Dopo l'installazione di hello e configurazione del server SMT hello, è necessario trovare repository directory hello in hello montaggio punto /srv/www/htdocs/inoltre alcune le sottodirectory nel repository. 

Riavviare il server SMT hello e i servizi correlati con i comandi.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Download di pacchetti nel server SMT

Dopo che tutti hello riavvio dei servizi, selezionare hello pacchetti appropriati in Gestione SMT utilizzando Yast. selezione pacchetto Hello dipendono dall'immagine del sistema operativo hello del server istanza grande HANA hello e non dal hello SLES versione o una versione di hello macchina virtuale in esecuzione hello SMT server. Seguito è riportato un esempio della schermata di selezione hello.

![Selezionare i pacchetti](./media/hana-installation/image10_select_packages.PNG)

Dopo avere completato con selezione pacchetto hello, è necessario toostart copia iniziale di hello del server di hello Seleziona pacchetti toohello SMT impostati. Questa copia viene attivata nella shell di hello utilizzando hello comando smt-mirror come illustrato di seguito


![Scaricare i pacchetti tooSMT server](./media/hana-installation/image11_download_packages.PNG)

Come viene visualizzato in precedenza, i pacchetti hello devono ottenere copiati nella directory hello create in hello montaggio punto /srv/www/htdocs. Il processo potrebbe richiedere un po' di tempo. Dipende da quanti pacchetti si seleziona, potrebbero richiedere più tooone ora.
Il completamento del processo, è necessario il programma di installazione di toomove toohello SMT client. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Configurare il client SMT hello in unità di istanza di grandi dimensioni HANA

in questo caso, Hello client sono unità di istanza di grandi dimensioni HANA hello. programma di installazione server SMT Hello copiato clientSetup4SMT.sh script hello in hello macchina virtuale di Azure. Copiare lo script toohello unità HANA istanza di grandi dimensioni si desidera tooconnect tooyour SMT server. Avviare script hello con l'opzione -h hello e assegnargli come nome del server SMT hello del parametro. Nell'esempio viene usato smtserver.

![Configurare il client SMT](./media/hana-installation/image12_configure_client.PNG)

Potrebbe esserci uno scenario in cui hello caricamento del certificato hello dal server hello client hello ha avuto esito positivo, ma è Impossibile eseguire la registrazione di hello come illustrato di seguito.

![Registrazione del client non riuscita](./media/hana-installation/image13_registration_failed.PNG)

Se è Impossibile eseguire la registrazione di hello, leggere questo [SUSE supporta documento](https://www.suse.com/de-de/support/kb/doc/?id=7006024) ed eseguire i passaggi di hello descritti sono.

> [!IMPORTANT] 
> Come nome del server è necessario il nome hello tooprovide di hello macchina virtuale, in questo caso smtserver, senza il nome di dominio completo hello. Solo hello VM nome works. 

Dopo l'esecuzione di questi passaggi, è necessario hello tooexecute comando seguente nell'unità di istanza di grandi dimensioni HANA hello

```
SUSEConnect –cleanup
```

> [!Note] 
> Nei test eseguiti sempre abbiamo toowait alcuni minuti dopo il passaggio. Hello clientSetup4SMT.sh l'esecuzione immediata, dopo hello misure correttive descritto nell'articolo SUSE hello è terminata con messaggi di che tale certificato hello non può essere ancora. Un'attesa di 5-10 minuti prima dell'esecuzione di clientSetup4SMT.sh consente in genere di configurare correttamente il client.

Se è verificato il problema hello necessari in base ai passaggi hello dell'articolo SUSE hello toofix, è necessario clientSetup4SMT.sh toorestart nell'unità di istanza di grandi dimensioni HANA hello nuovamente. L'operazione dovrebbe essere completata correttamente, come illustrato di seguito.

![Registrazione del client riuscita](./media/hana-installation/image14_finish_client_config.PNG)

Con questo passaggio, è configurato il client SMT hello di hello istanza grande HANA unità tooconnect server SMT hello che è stato installato nella macchina virtuale di Azure hello. È ora possibile richiedere 'zypper backup' o 'zypper in' tooinstall OS patch tooHANA istanze di grandi dimensioni o installare altri pacchetti. È inteso che è solo possibile ottenere le patch che è stato scaricato prima nel server SMT hello.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Esempio di installazione di SAP HANA in istanze Large di HANA
In questa sezione viene illustrato come tooinstall SAP HANA in un'unità HANA istanza di grandi dimensioni. lo stato iniziale di Hello abbiamo l'aspetto:

- È fornito a Microsoft tutti hello dati toodeploy è un'istanza di SAP HANA grandi dimensioni.
- Istanza di grandi dimensioni di SAP HANA hello ricevuto da Microsoft.
- È stata creata una rete virtuale di Azure che è una rete locale connesso tooyour.
- Si è connessi circuito ExpressRotue hello per le istanze di grandi dimensioni HANA toohello stessa rete virtuale di Azure.
- È stata installata una VM di Azure da usare come jumpbox per istanze Large di HANA.
- Sono apportate assicurarsi che sia possibile connettersi da hello jump tooyour istanza grande HANA unità e viceversa.
- È stata selezionata se tutti i pacchetti necessari di hello e patch sono installate.
- Leggere le note SAP hello e la documentazione relative all'installazione HANA su hello del sistema operativo, si utilizza e assicurarsi che scelta versione HANA hello è supportato nella versione di hello del sistema operativo.

Gli elementi visualizzati nelle sequenze Avanti hello è disponibile come download hello di toohello jump la macchina virtuale, in questo caso è in esecuzione in un sistema operativo Windows, la copia di hello di unità di istanza di grandi dimensioni HANA toohello pacchetti hello e sequenza hello del programma di installazione di hello hello HANA installazione pacchetti.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Download di bit di installazione di SAP HANA hello
Poiché non dispone di unità di istanza di grandi dimensioni HANA hello toohello connettività diretta a internet, è possibile direttamente scaricare i pacchetti di installazione hello dalle toohello SAP HANA grandi istanza VM. tooovercome hello mancante connettività internet diretta, è necessario casella passa hello. Scaricare hello pacchetti toohello jump casella macchina virtuale.

In ordine toodownload hello HANA i pacchetti di installazione, è necessario un SAP S-utente o un altro utente, che consente di tooaccess hello Marketplace SAP. Completare questa sequenza di schermate dopo l'accesso:

Andare troppo[SAP Service Marketplace](https://support.sap.com/en/index.html) > fare clic su Scarica Software > aggiornamento e installazioni > dall'indice alfabetico > in H-SAP HANA Platform Edition > SAP HANA piattaforma Edition 2.0 > installazione > hello Download file seguenti

![Scaricare i file di installazione di HANA](./media/hana-installation/image16_download_hana.PNG)

In caso di dimostrazione hello, sono state scaricate pacchetti di installazione di SAP HANA 2.0. Nella finestra hello jump Azure VM si espande autoestrazione hello nella directory di hello, come illustrato di seguito.

![Estrarre i file di installazione di HANA](./media/hana-installation/image17_extract_hana.PNG)

Come vengono estratti gli archivi di hello, copiare directory hello creata dall'estrazione hello, in caso di hello sopra 51052030, toohello HANA grandi unità di istanza nel volume /hana/shared hello in una directory in cui che è stato creato.

> [!Important]
> Non copiare i pacchetti di installazione hello nella radice di hello o LUN di avvio perché lo spazio viene limitato e deve toobe utilizzato da altri processi nonché.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Installare SAP HANA in unità di istanza di grandi dimensioni HANA hello
In ordine tooinstall SAP HANA, è necessario toolog in come radice di utente. Solo radice è sufficiente tooinstall autorizzazioni SAP HANA.
Hello occorre innanzitutto toodo è tooset autorizzazioni sulla directory hello copiate in hana/condiviso. le autorizzazioni di Hello devono tooset come

```
chmod –R 744 <Installation bits folder>
```

Se si desidera tooinstall SAP HANA utilizzando hello grafica del programma di installazione, hello gtk2 pacchetto esigenze toobe installati nelle istanze di grandi dimensioni HANA hello. Controllare se è installato con il comando hello

```
rpm –qa | grep gtk2
```

Ulteriori passaggi, ci stiamo che illustra l'installazione di SAP HANA hello con interfaccia utente grafica di hello. Come passaggio successivo, passare alla directory di installazione hello e passare alla sottodirectory hello HDB_LCM_LINUX_X86_64. Inizia

```
./hdblcmgui 
```
da tale directory. A questo punto vengono recupero illustrate una sequenza di schermate in cui è necessario dati hello tooprovide per l'installazione di hello. In caso di hello illustrato, si sta installazione server di database SAP HANA hello e i componenti client di SAP HANA hello. Viene quindi selezionato il valore "SAP HANA Database" (Database SAP HANA), come mostrato di seguito.

![Selezionare HANA nell'installazione](./media/hana-installation/image18_hana_selection.PNG)

Nella schermata successiva hello, si sceglie hello 'Installare un nuovo sistema'

![Selezionare una nuova installazione di HANA](./media/hana-installation/image19_select_new.PNG)

Dopo questo passaggio, è necessario tooselect tra diversi componenti aggiuntivi che è inoltre possibile installare server di database SAP HANA toohello.

![Selezionare altri componenti di HANA](./media/hana-installation/image20_select_components.PNG)

A scopo di hello di questa documentazione, si sceglie hello SAP HANA Client e hello SAP HANA Studio. È stata installata anche un'istanza con scalabilità verticale. Nella schermata successiva hello, è pertanto necessario toochoose 'Host singolo System' 

![Selezionare l'installazione con scalabilità verticale](./media/hana-installation/image21_single_host.PNG)

Nella schermata successiva hello, è necessario tooprovide alcuni dati

![Specificare il SID di SAP HANA](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Come ID sistema HANA (SID), è necessario tooprovide hello stesso SID, come specificato Microsoft durante la distribuzione istanza grande HANA hello ordinato. Scelta di un SID diverso rende l'installazione di hello non riuscire a causa di problemi relativi alle autorizzazioni tooaccess su volumi diversi hello

Come directory di installazione è utilizzare directory /hana/shared hello. Nel passaggio successivo hello, è necessario percorsi hello tooprovide hello HANA file di dati e i file di log di hello HANA


![Specificare la posizione dei log HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> È necessario definire come file di dati e log hello volumi già fornita con i punti di montaggio hello contenenti hello SID prescelto nella selezione schermata hello prima di questa schermata. Se hello SID mancata corrispondenza con hello uno digitato, nella schermata di hello, prima di tornare indietro e modificare hello valore toohello SID sono presenti punti di montaggio hello.

Nel passaggio successivo hello, esaminare il nome host hello e infine correggerlo. 

![Verificare il nome host](./media/hana-installation/image24_review_host_name.PNG)

Nel passaggio successivo hello, è necessario anche dati tooretrieve fornito tooMicrosoft quando sono stati ordinati distribuzione istanza grande HANA hello. 

![Specificare un UID e un GID per l'utente di sistema](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> È necessario tooprovide hello stesso ID utente di sistema e ID del gruppo di utenti Microsoft fornita come ordine di distribuzione unità hello. Se non si riesce hello toogive molto stesso ID, installazione hello di SAP HANA nell'unità di istanza di grandi dimensioni HANA hello ha esito negativo.

Nelle schermate hello due, non viene mostrato in questa documentazione, è necessario password hello tooprovide per utente di sistema hello del database SAP HANA hello e una password di hello per l'utente sapadm hello, che viene utilizzato per l'agente Host SAP che viene installata come parte di hello istanza del database SAP HANA Hello.

Dopo aver definito la password di hello, una schermata di conferma verrà visualizzati. controllare tutti i dati di hello elencati e continuare l'installazione di hello. Viene visualizzata una schermata di stato di avanzamento che lo stato dell'installazione, ad esempio hello di sotto di hello documenti

![Verificare lo stato dell'installazione](./media/hana-installation/image27_show_progress.PNG)

Come termine hello installazione, è consigliabile un'immagine come segue quello hello

![L'installazione è stata completata](./media/hana-installation/image28_install_finished.PNG)

A questo punto, istanza di SAP HANA hello deve essere installato e in esecuzione e pronto per l'utilizzo. È necessario essere in grado di tooconnect tooit da SAP HANA Studio. Assicurarsi inoltre di verificare la presenza di patch più recenti di hello di SAP HANA e applicare le patch.
























































 







 




