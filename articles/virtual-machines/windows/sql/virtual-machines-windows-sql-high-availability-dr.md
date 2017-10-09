---
title: "aaaHigh disponibilità e ripristino di emergenza per SQL Server | Documenti Microsoft"
description: Una discussione su hello vari tipi di strategie HADR per SQL Server in esecuzione in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Disponibilità elevata e ripristino di emergenza per SQL Server nelle macchine virtuali di Azure

Macchine virtuali di Microsoft Azure (VM) con SQL Server consente di ridurre il costo hello di soluzione a elevata disponibilità e ripristino (HADR) del database. Molte soluzioni HADR di SQL Server sono supportate nelle macchine virtuali di Azure, sia come soluzioni solo Azure sia come soluzioni ibride. In una soluzione solo Azure, l'intero sistema HADR di hello viene eseguito in Azure. In una configurazione ibrida, parte della soluzione hello in esecuzione in Azure e hello altra parte viene eseguito in locale nell'organizzazione. Hello flessibilità di hello ambiente Azure consente toomove completamente o parzialmente budget di hello toosatisfy tooAzure requisiti HADR e di SQL Server sistemi di database.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Informazioni sulla necessità di hello per una soluzione HADR
È attivo tooyou tooensure dispone di funzionalità HADR hello hello contratto di servizio (SLA) richiede che il sistema di database. tabelle dei fatti Hello che Azure fornisce meccanismi di disponibilità elevata, ad esempio di correzione del servizio per servizi cloud e rilevamento del ripristino da errore per le macchine virtuali, non garantiscono di per sé che è possibile soddisfare SLA hello desiderato. Questi meccanismi proteggono la disponibilità elevata hello di hello macchine virtuali ma non hello la disponibilità elevata di SQL Server in esecuzione all'interno di hello macchine virtuali. È possibile che toofail istanza di SQL Server hello mentre hello VM è online e integra. Inoltre, i meccanismi di disponibilità elevata hello anche forniti da Azure consentono tempi di inattività delle macchine virtuali hello scadenza tooevents come il recupero da errori hardware o software e aggiornamenti del sistema operativo.

Neppure l'archiviazione con ridondanza geografica di Azure, implementata con una funzionalità denominata replica geografica, costituisce un'adeguata soluzione di ripristino di emergenza per i database. Poiché la replica geografica invia dati in modo asincrono, gli aggiornamenti recenti possono perdersi nell'evento hello di emergenza. Ulteriori informazioni sulla replica geografica limitazioni vengono trattati nelle hello [replica geografica non è supportata per i file di dati e di log in dischi separati](#geo-replication-support) sezione.

## <a name="hadr-deployment-architectures"></a>Architetture di distribuzione HADR
Le tecnologie HADR di SQL Server supportate in Azure includono:

* [Gruppi di disponibilità AlwaysOn](https://technet.microsoft.com/library/hh510230.aspx)
* [Istanze del cluster di failover AlwaysOn](https://technet.microsoft.com/library/ms189134.aspx)
* [Log shipping](https://technet.microsoft.com/library/ms187103.aspx)
* [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Azure](https://msdn.microsoft.com/library/jj919148.aspx)
* [Mirroring del database](https://technet.microsoft.com/library/ms189852.aspx) - Deprecato in SQL Server 2016

È possibile toocombine hello tecnologie insieme tooimplement una soluzione di SQL Server che include la disponibilità elevata e ripristino di emergenza. A seconda di tecnologia hello da utilizzare, una distribuzione ibrida può richiedere un tunnel VPN con hello rete virtuale di Azure. Hello nelle sezioni seguenti vengono illustrano alcune delle architetture di distribuzione di esempio hello.

## <a name="azure-only-high-availability-solutions"></a>Solo Azure: soluzioni di disponibilità elevata

È possibile avere una soluzione a disponibilità elevata per SQL Server a livello di database con Gruppi di disponibilità Always On, denominati gruppi di disponibilità. È anche possibile creare una soluzione a disponibilità elevata a livello di istanza con istanze del cluster di failover Always On, denominate istanze del cluster di failover. Per maggiore ridondanza, è anche possibile creare ridondanza per entrambi i livelli tramite la creazione di gruppi di disponibilità nelle istanze del cluster di failover. 

| Tecnologia | Architetture di esempio |
| --- | --- |
| **Gruppi di disponibilità** |Hello di repliche di disponibilità in esecuzione in macchine virtuali di Azure nella stessa area garantire un'elevata disponibilità. È necessario tooconfigure un controller di dominio macchina virtuale, in quanto il clustering di failover di Windows richiede un dominio di Active Directory.<br/> ![Gruppi di disponibilità](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Per altre informazioni, vedere [Configurare manualmente un gruppo di disponibilità Always On nelle macchine virtuali di Azure tramite Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Istanze del cluster di failover** |Le istanze del cluster di failover, che richiedono l'archiviazione condivisa, possono essere create in 3 modi diversi.<br/><br/>1. Un cluster di failover a due nodi in esecuzione in macchine virtuali di Azure con l'archiviazione associata [Windows Server 2016 spazi di archiviazione diretta \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide una SAN virtuale basata su software.<br/><br/>2. Un cluster di failover a due nodi in esecuzione su macchine virtuali di Azure con archiviazione supportata da una soluzione di clustering di terze parti. Per un esempio specifico che usa SIOS DataKeeper, vedere [High availability for a file share using failover clustering and 3rd party software SIOS DataKeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/) (Disponibilità elevata per una condivisione file basata su clustering di failover e sul software di terze parti SIOS DataKeeper).<br/><br/>3. Un cluster di failover a due nodi in esecuzione su macchine virtuali di Azure con archiviazione a blocchi condivisa su una destinazione iSCSI remota tramite ExpressRoute. Ad esempio, archiviazione privata NetApp (NPS) espone una destinazione iSCSI tramite ExpressRoute con Equinix tooAzure macchine virtuali.<br/><br/>Per l'archiviazione condivisa di terze parti e soluzioni di replica di dati, contattare il fornitore hello per tutti i dati correlati tooaccessing problemi in caso di failover.<br/><br/>Si noti che non è ancora supportato l'uso di istanze del cluster di failover nell' [archivio file di Azure](https://azure.microsoft.com/services/storage/files/) , perché questa soluzione non usa l'archiviazione Premium. Stiamo lavorando toosupport questo breve. |

## <a name="azure-only-disaster-recovery-solutions"></a>Solo Azure: soluzioni di ripristino di emergenza
È possibile disporre di una soluzione di ripristino di emergenza per i database di SQL Server in Azure tramite i gruppi di disponibilità, il mirroring del database o funzionalità di backup e ripristino con i BLOB di archiviazione.

| Tecnologia | Architetture di esempio |
| --- | --- |
| **Gruppi di disponibilità** |Repliche di disponibilità in esecuzione tra più data center nelle macchine virtuali di Azure per il ripristino di emergenza. Questa soluzione per più aree protegge dalla completa interruzione dell'alimentazione del sito. <br/> ![Gruppi di disponibilità](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>All'interno di un'area, tutte le repliche devono essere all'interno di hello stesso servizio cloud e hello stessa rete virtuale. Poiché ogni area sarà caratterizzata da una VNet separata, queste soluzioni richiedono la connettività di rete virtuale tooVNet. Per ulteriori informazioni, vedere [configura una rete virtuale multisito connessione usando il portale di Azure di hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Per istruzioni dettagliate, vedere [Configurare un gruppo di disponibilità SQL Server in macchine virtuali di Azure in aree diverse](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Mirroring del database** |Tutti i server principali, mirror e di controllo in esecuzione in diversi data center per il ripristino di emergenza. È necessario eseguire la distribuzione usando certificati del server perché un dominio di Active Directory non può essere esteso a più data center.<br/>![Mirroring del database](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Backup e ripristino con il servizio di archiviazione BLOB di Azure** |Archiviazione di tooblob direttamente in un Data Center diverso per il ripristino di emergenza backup dei database di produzione.<br/>![Backup e ripristino](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Per altre informazioni, vedere [Backup e ripristino per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>IT ibrido: soluzioni di ripristino di emergenza
È possibile disporre di una soluzione di ripristino di emergenza per i database di SQL Server in un ambiente IT ibrido tramite i gruppi di disponibilità, il mirroring del database, il log shipping e funzionalità di backup e ripristino con l'archiviazione BLOB di Azure.

| Tecnologia | Architetture di esempio |
| --- | --- |
| **Gruppi di disponibilità** |Alcune repliche di disponibilità in esecuzione nelle macchine virtuali di Azure e altre in esecuzione in locale per il ripristino di emergenza tra siti. Hello sito di produzione può essere in locale o in un Data Center Azure.<br/>![Gruppi di disponibilità](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Poiché tutte le repliche di disponibilità devono essere hello stesso cluster di failover, hello cluster deve essere esteso a entrambe le reti (un cluster di failover su più subnet). Questa configurazione richiede una connessione VPN tra Azure e hello rete locale.<br/><br/>Per corretto ripristino di emergenza dei database, è inoltre necessario installare un controller di dominio di replica nel sito di ripristino di emergenza hello.<br/><br/>È possibile toouse hello Aggiunta guidata di Replica in SQL Server Management Studio tooadd tooan una replica di Azure esistente gruppo di disponibilità AlwaysOn. Per ulteriori informazioni, vedere l'esercitazione: estendere tooAzure il gruppo di disponibilità AlwaysOn. |
| **Mirroring del database** |Un partner è in esecuzione in una macchina virtuale di Azure e altri hello in esecuzione in locale per il ripristino di emergenza tra siti utilizzando certificati del server. I partner non è necessario toobe in hello nello stesso dominio di Active Directory ed non è necessaria alcuna connessione VPN.<br/>![Mirroring del database](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Scenario di mirroring di un altro database implica un partner è in esecuzione in una macchina virtuale di Azure e hello altra in esecuzione in locale in hello stesso dominio di Active Directory per il ripristino di emergenza tra siti. Oggetto [connessione VPN tra la rete hello Azure virtuale hello e rete locale](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) è obbligatorio.<br/><br/>Per corretto ripristino di emergenza dei database, è inoltre necessario installare un controller di dominio di replica nel sito di ripristino di emergenza hello. |
| **Log shipping** |Un server in esecuzione in una macchina virtuale di Azure e altri hello in esecuzione in locale per il ripristino di emergenza tra siti. Il log shipping dipende dalla condivisione file di Windows, pertanto una connessione VPN tra hello rete virtuale di Azure e hello locale rete non è obbligatoria.<br/>![Log shipping](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Per corretto ripristino di emergenza dei database, è inoltre necessario installare un controller di dominio di replica nel sito di ripristino di emergenza hello. |
| **Backup e ripristino con il servizio di archiviazione BLOB di Azure** |Database di produzione, eseguire il backup direttamente nell'archiviazione blob tooAzure per il ripristino di emergenza in locale.<br/>![Backup e ripristino](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Per altre informazioni, vedere [Backup e ripristino per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Considerazioni importanti per HADR di SQL Server in Azure
La macchina virtuale, l'archiviazione e la rete di Azure hanno caratteristiche operative diverse rispetto a un'infrastruttura IT locale non virtualizzata. Una corretta implementazione di una soluzione HADR SQL Server in Azure, è necessario capire queste differenze e progettare la soluzione tooaccommodate li.

### <a name="high-availability-nodes-in-an-availability-set"></a>Nodi a disponibilità elevata in un set di disponibilità
Set di disponibilità in Azure consentono di nodi a disponibilità elevata tooplace hello in domini di errore (Fd) e in domini di aggiornamento (UD) separato. Per le macchine virtuali di Azure toobe inserito in hello stesso set di disponibilità, è necessario distribuirle in hello stesso servizio cloud. Solo i nodi di hello nello stesso servizio cloud può partecipare hello stesso set di disponibilità. Per ulteriori informazioni, vedere [Gestisci hello disponibilità delle macchine virtuali](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Comportamento del cluster di failover nella rete di Azure
servizio DHCP non conforme a RFC di Hello in Azure può provocare la creazione di hello di determinati toofail le configurazioni di cluster di failover, a causa di nome di rete cluster toohello viene assegnato un indirizzo IP duplicato, ad esempio hello stesso IP address come uno dei nodi del cluster hello. Si tratta di un problema durante l'implementazione di gruppi di disponibilità, che dipende da funzionalità cluster di failover di Windows hello.

Si consideri uno scenario di hello quando un cluster a due nodi viene creato e portato in linea:

1. Hello cluster torna online e NODE1 richiede un indirizzo IP assegnato dinamicamente per nome di rete cluster hello.
2. Nessun indirizzo IP diverso da indirizzo IP di NODE1 viene fornito dalla hello servizio DHCP, poiché hello servizio DHCP riconosce che la richiesta hello proviene da NODE1 stesso.
3. Windows rileva che un indirizzo duplicato viene assegnato tooNODE1 sia toohello nome di rete di cluster di failover e gruppo di cluster di hello predefinito non toocome online.
4. gruppo cluster predefinito di Hello Sposta tooNODE2, che tratta l'indirizzo IP di NODE1 come indirizzo IP del cluster hello e porta gruppo cluster predefinito di hello online.
5. Quando NODE2 tenta tooestablish connessione con NODE1, pacchetti indirizzati a NODE1 non lasciano mai NODE2 perché viene risolto tooitself di indirizzo IP di NODE1. NODE2 non è possibile stabilire una connessione con NODE1, quindi perde il quorum e arresta hello cluster.
6. Nel frattempo hello, NODE1 può inviare i pacchetti tooNODE2, ma NODE2 non può rispondere. NODE1 perde il quorum e arresta hello cluster.

È possibile evitare questo scenario assegnando un indirizzo IP statico inutilizzato, ad esempio un indirizzo IP locale al collegamento come 169.254.1.1, il nome di rete cluster toohello in ordine toobring hello nome di rete cluster online. toosimplify questo processo, vedere [cluster di failover la configurazione di Windows in Azure per i gruppi di disponibilità](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Per altre informazioni, vedere [Configurare manualmente un gruppo di disponibilità Always On nelle macchine virtuali di Azure tramite Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Supporto del listener del gruppo di disponibilità
I listener del gruppo di disponibilità sono supportati nelle VM di Azure che eseguono Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016. Questo supporto viene realizzato mediante l'utilizzo di hello di endpoint con bilanciamento del carico abilitato nelle macchine virtuali di Azure hello che costituiscono nodi di gruppo di disponibilità. È necessario seguire i passaggi di configurazione speciale per toowork listener hello per le applicazioni client che sono in esecuzione in Azure, nonché quelli eseguiti in locale.

Sono disponibili due opzioni principali per la configurazione del listener: esterno (pubblico) o interno. Hello listener (pubblici) esterno Usa una connessione internet bilanciamento del carico è associato con un IP virtuale (VIP pubblico) che è accessibile tramite hello internet. Un listener interno utilizza un servizio di bilanciamento del carico interno e client supporta solo all'interno di hello stessa rete virtuale. Per un tipo di bilanciamento del carico, è necessario abilitare Direct Server Return. 

Se hello gruppo di disponibilità si estende su più subnet di Azure (ad esempio una distribuzione che attraversa aree di Azure), stringa di connessione client hello deve includere "**MultisubnetFailover = True**". In questo modo le repliche toohello tentativi di connessione parallela in subnet diverse hello. Per istruzioni sull'impostazione di un listener, vedere

* [Configurare un listener ILB per i gruppi di disponibilità in Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Configurare un listener esterno per i gruppi di disponibilità in Azure](../classic/ps-sql-ext-listener.md).

È comunque possibile connettersi separatamente la replica di disponibilità tooeach connettendosi direttamente toohello istanza del servizio. Inoltre, poiché i gruppi di disponibilità sono compatibili con le versioni precedenti con i client di mirroring del database, è possibile connettersi toohello le repliche di disponibilità come partner di mirroring, purché le repliche hello configurate database mirroring toodatabase simile:

* Una replica primaria e una replica secondaria
* Hello replica secondaria è configurata come non leggibile (**secondario leggibile** opzione impostata troppo**n**)

Una stringa di connessione client di esempio corrispondente di configurazione di toothis simile al mirroring del database utilizzando ADO.NET o SQL Server Native Client è inferiore:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Per altre informazioni sulla connettività client, vedere:

* [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Connettere i client tooa sessione di mirroring del Database (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Connessione tooAvailability listener del gruppo IT ibrido](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Utilizzo delle stringhe di connessione per il mirroring del database con Gruppi di disponibilità](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Latenza di rete in ambiente IT ibrido
È necessario distribuire la soluzione HADR con il presupposto hello che possono verificarsi periodi di tempo con latenza di rete elevata tra la rete locale e Azure. Quando si distribuisce tooAzure repliche, utilizzare commit asincrono anziché quello sincrono per la modalità di sincronizzazione hello. Quando la distribuzione di server di mirroring del database locale sia in Azure, utilizzare la modalità a prestazioni elevate hello anziché modalità a sicurezza elevata hello.

### <a name="geo-replication-support"></a>Supporto della replica geografica
La replica geografica nei dischi di Azure non supporta i file di dati hello e file di log di hello stesso database toobe archiviati su dischi separati. L'archiviazione con ridondanza geografica replica le modifiche in ogni disco in modo indipendente e asincrono. Questo meccanismo garantisce l'ordine di scrittura hello all'interno di un disco singolo nella copia replicata geograficamente hello, ma non per tutte le copie replicate geograficamente di più dischi. Se si configura un toostore database, file di dati e del file di log in dischi separati, hello recuperata dischi dopo un'emergenza potranno contenere una copia più aggiornata del file di dati hello hello che file di log, che interrompe hello log write-ahead in SQL Server e hello ACID proprietà delle transazioni. Se non si dispone hello opzione toodisable-replica geografica nell'account di archiviazione hello, è consigliabile mantenere tutti i dati e file di log per un determinato database su hello stesso disco. Se è necessario utilizzare più di un disco a causa delle dimensioni di toohello di hello database, è necessario toodeploy una delle soluzioni di ripristino di emergenza hello elencate in precedenza tooensure ridondanza dei dati.

## <a name="next-steps"></a>Passaggi successivi
Se è necessario toocreate una macchina virtuale di Azure con SQL Server, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

migliori prestazioni hello tooget da SQL Server in esecuzione in una macchina virtuale di Azure, vedere Guida hello in [procedure consigliate per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Altre risorse:
* [Installare una nuova foresta Active Directory in Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Creare cluster di failover per i gruppi di disponibilità in una macchina virtuale di Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

