---
title: aaaBackup e ripristino di emergenza per i dischi Azure IaaS | Documenti Microsoft
description: "In questo articolo verrà illustrato come tooplan per il Backup e ripristino di emergenza delle macchine virtuali IaaS (VM) e dischi in Azure. Questo documento è relativo a dischi gestiti e non gestiti"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Backup e ripristino di emergenza per dischi IaaS di Azure

In questo articolo verrà illustrato come tooplan per il Backup e ripristino di emergenza delle macchine virtuali IaaS (VM) e dischi in Azure. Questo documento è relativo a dischi gestiti e non gestiti.

Prima di tutto parleremo hello errore incorporate funzionalità di tolleranza in hello piattaforma Azure che consentono di proteggersi da errori locali. Quindi si parlerà di scenari di emergenza hello non completamente coperti da funzionalità incorporate di hello, che è l'argomento principale di hello interessato da questo documento. Verranno forniti anche alcuni esempi di scenari di carico di lavoro per cui è possibile applicare diverse considerazioni relative a backup e ripristino di emergenza. Verranno infine esaminate le soluzioni possibili per il ripristino di emergenza di dischi IaaS. 

## <a name="introduction"></a>Introduzione

Hello piattaforma Azure utilizzati vari metodi per la ridondanza e protezione toohelp tolleranza di errore da errori hardware localizzati che possono verificarsi. Errori locali possono includere problemi con un computer server di archiviazione di Azure contenente errori di un'unità SSD o HDD o parte dei dati di hello per un disco virtuale in tale server. Gli errori dei componenti hardware isolato tale situazione possono verificarsi durante le normali operazioni e piattaforma hello è progettato toobe toothese resilienti errori. Le emergenze gravi possono provocare errori o inaccessibilità per un numero elevato di server di archiviazione o per un intero data center. Mentre le macchine virtuali e dischi in genere sono protetti da errori localizzati, ulteriori passaggi sono necessari tooprotect il carico di lavoro a livello di area irreversibile tentativi non riusciti (ad esempio un errore grave) che possono influenzare la macchina virtuale e i dischi.

Inoltre toohello possibilità di errori di piattaforma, possono verificarsi problemi con i dati o un'applicazione hello cliente. Ad esempio, una nuova versione dell'applicazione potrebbe inavvertitamente effettuare un'interruzione toohello dati delle modifiche. In tal caso, è un'applicazione hello toorevert e hello dati tooa versione precedente contiene hello ultimo stato noto soddisfacente. A questo scopo, sono necessari backup regolari.

Per il ripristino di emergenza locale, è necessario eseguire il backup VM IaaS dischi tooa diverso paese. 

Prima di esaminare le opzioni di backup e ripristino di emergenza, è utile esaminare i metodi disponibili per la gestione degli errori localizzati.

### <a name="azure-iaas-resiliency"></a>Resilienza IaaS di Azure

*Resilienza* fa riferimento a tolleranza di errore toohello normali errori che si verificano in componenti hardware. Resilienza è hello possibilità toorecover dagli errori e continuare toofunction. Non è su come evitare errori, ma risponde toofailures in modo da evitare tempi di inattività o perdita di dati. obiettivo di Hello di resilienza è tooreturn hello tooa completamente funzionante lo stato dell'applicazione dopo un errore. Macchine virtuali di Azure e i dischi sono toobe progettato toocommon resilienti hardware errori. Esaminiamo come piattaforma IaaS di Azure hello fornisce la resilienza.

Una macchina virtuale è costituito principalmente da due parti: (1) un calcolo, server e dischi persistenti hello (2). Entrambi influiscono sulla tolleranza di errore hello di una macchina virtuale.

Se il server host di calcolo di Azure hello che ospita la macchina virtuale di cui si verifichi un errore hardware (che è raro), Azure è progettato tooautomatically ripristino hello macchina virtuale in un altro server. In questo caso, si verificherà un riavvio e hello VM sarà eseguire il backup in un secondo momento. Azure rileva tali errori hardware automaticamente ed esegue i ripristini toohelp verificare che il cliente hello VM sarà disponibile appena possibile.

Relative ai dischi IaaS, è fondamentale per la piattaforma di archiviazione permanente hello durabilità dei dati. Azure dotate di applicazioni aziendali importanti in esecuzione su IaaS e dipendono persistenza hello dei dati di hello. La progettazione della protezione di Azure per questi dischi IaaS prevede tre copie ridondanti dei dati archiviati localmente, in modo da offrire una durabilità elevata rispetto agli errori locali. Se uno dei componenti hardware hello che contiene il disco non riesce, è possibile che la macchina virtuale non venga interessata perché sono presenti due copie aggiuntive toosupport disco richieste. Funziona correttamente anche se i due diversi componenti hardware che supporta un disco non riuscire in hello stesso tempo (che sarebbe molto raro). toohelp verificare sempre mantiene tre repliche, il servizio di archiviazione di Azure hello genera automaticamente una nuova copia dei dati in background hello se uno dei tre copie hello diventa non disponibile. Pertanto non deve essere necessario toouse RAID con dischi di Azure per la tolleranza di errore. Un RAID 0 semplice configurazione dovrebbe essere sufficiente per lo striping dischi hello toocreate necessari volumi di grandi dimensioni.

Grazie a questa architettura, **Azure ha offerto in modo costante una durabilità di livello aziendale per dischi IaaS, con una percentuale di [frequenza di errori annualizzata](https://en.wikipedia.org/wiki/Annualized_failure_rate) pari a ZERO, ovvero la migliore del settore.**

Problemi hardware localizzati in hello calcolano host o nel servizio di archiviazione hello piattaforma può comportare talvolta indisponibilità temporanea per la macchina virtuale che è coperto da hello hello [SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) per la disponibilità di macchina virtuale. Azure offre anche un Contratto di servizio leader di settore per singole istanze di VM che usano dischi di Archiviazione Premium.

toosafeguard i carichi di lavoro di applicazione dall'inattività a causa di toohello temporanea indisponibilità di un disco o di una macchina virtuale, i clienti possono usare [set di disponibilità](../../virtual-machines/windows/manage-availability.md). Due o più macchine virtuali in un set di disponibilità fornisce la ridondanza per un'applicazione hello. Azure crea quindi queste VM e questi dischi in domini di errore separati con diverso tipo di alimentazione, diverse risorse di rete e diversi componenti del server. Di conseguenza, gli errori hardware localizzato in genere non influiscono più macchine virtuali in hello impostare hello stesso tempo, garantendo una disponibilità elevata per l'applicazione. Viene considerato che una disponibilità toouse buona norma imposta quando è necessaria la disponibilità elevata. Per ulteriori informazioni, vedere gli aspetti di ripristino di emergenza hello descritti di seguito.

### <a name="backup-and-disaster-recovery"></a>Backup e ripristino di emergenza

Ripristino di emergenza (ripristino di emergenza) è hello possibilità toorecover da incidenti rari ma principali: errori non temporanei e larga scala, ad esempio interruzioni del servizio che interessa un'intera area. Il ripristino di emergenza include il backup dei dati e l'archiviazione e può includere l'intervento manuale, ad esempio il ripristino di un database dal backup.

Hello protezione incorporata della piattaforma Azure in caso di errori localizzato potrebbe non garantire una protezione completa hello macchine virtuali e dischi in caso di hello di principali emergenze che possono causare interruzioni su larga scala. ad esempio eventi irreversibili come uragani, terremoti, incendi o errori su larga scala delle unità hardware che colpiscono un data center. Inoltre, possono verificarsi errori a causa di problemi di tooapplication o dati.

toohelp proteggere i carichi di lavoro IaaS interruzioni, è consigliabile pianificare per il ripristino tooenable ridondanza e i backup. Ripristino di emergenza, è consigliabile pianificare backup in una posizione geografica diversa dal sito primario di hello e ridondanza. Ciò consente di garantire il backup non è interessato dalle hello stesso evento che originariamente interessati hello macchina virtuale o dischi. Per altre informazioni, vedere [Disaster Recovery for Applications built on Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) (Ripristino di emergenza per applicazioni basate su Azure).

Le considerazioni di ripristino di emergenza possono includere hello seguenti aspetti:

1. Disponibilità elevata è il possibilità hello di hello toocontinue di applicazione in esecuzione in uno stato integro, senza tempi di inattività significativi. Per "Integro", si intende un'applicazione hello è reattiva e gli utenti possono connettersi toohello applicazione e interagire con esso. Alcuni database e applicazioni mission-critical possono essere necessari toobe disponibile sempre, anche se sono presenti errori nella piattaforma hello. Per questi carichi di lavoro, potrebbe essere necessario tooplan ridondanza per un'applicazione hello, nonché dati hello.

2. Durabilità dei dati: In alcuni casi, la considerazione principale hello consiste nel garantire dati hello viene mantenuti in caso di hello un'emergenza. Potrebbe essere quindi necessario un backup dei dati in una posizione diversa. Tali carichi di lavoro, potrebbe essere necessario non ridondanza completa per un'applicazione hello, ma un backup regolare dei dischi hello.

## <a name="backup-and-dr-scenarios"></a>Scenari di backup e ripristino di emergenza

Ecco alcuni esempi tipici scenari di applicazione del carico di lavoro e le considerazioni di hello per la pianificazione di ripristino di emergenza.

### <a name="scenario-1-major-database-solutions"></a>Scenario 1: Principali soluzioni di database

Si consideri un server di database di produzione, ad esempio SQL Server oppure Oracle, in grado di supportare la disponibilità elevata. Le applicazioni di produzione cruciali e gli utenti dipendono da questo database. piano di ripristino di emergenza Hello per questo sistema potrebbe essere necessario hello toosupport seguenti requisiti:

1. I dati devono essere protetti e recuperabili.
2.  Il server deve essere disponibile per l'uso.

Tale operazione potrebbe richiedere la gestione di una replica di database hello in un'area diversa come backup. A seconda dei requisiti di hello per la disponibilità di server e il ripristino dei dati, soluzione hello potrebbe variare da un attivo-attivo o attivo-passivo replica sito tooperiodic backup non in linea dei dati di hello. I database relazionali come SQL Server e Oracle offrono diverse opzioni per la replica. Per SQL Server è possibile usare [SQL Server Always On Availability Groups](https://msdn.microsoft.com/library/hh510230.aspx) (Gruppi di disponibilità AlwaysOn di SQL Server) per ottenere la disponibilità elevata.

Anche i database NoSQL come MongoDB supportano le [repliche](https://docs.mongodb.com/manual/replication/) per la ridondanza. le repliche di Hello per la disponibilità elevata possono essere utilizzate.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scenario 2: Cluster di VM ridondanti

Si consideri un carico di lavoro gestito da un cluster di VM che forniscono ridondanza e bilanciamento del carico, ad esempio un cluster Cassandra distribuito in un'area. Questo tipo di architettura fornisce già un livello elevato di ridondanza entro tale area. Tuttavia, tooprotect hello il carico di lavoro da un errore a livello regionale, considerare la distribuzione di cluster hello in due aree o la regione tooanother backup periodici.

### <a name="scenario-3-iaas-application-workload"></a>Scenario 3: Carico di lavoro delle applicazioni IaaS

Potrebbe trattarsi di un carico di lavoro tipico in esecuzione in una VM di Azure, È possibile ad esempio, un server web o file che contiene il contenuto di hello e altre risorse di un sito. Potrebbe anche essere un'applicazione di business personalizzata in esecuzione in una macchina virtuale archiviati relativi dati, risorse e lo stato dell'applicazione nei dischi di macchina virtuale hello. In questo caso, è importante toomake assicurarsi di che eseguire backup a intervalli regolari. Frequenza di backup dovrebbe essere basata su natura hello del carico di lavoro VM hello. Ad esempio, se un'applicazione hello viene eseguito ogni giorno e modifica i dati, quindi hello devono eseguire backup ogni ora.

Un altro esempio è costituito da un server di report che esegue il pull dei dati da altre origini e genera report aggregati. Perdita di questa macchina virtuale o dischi comporti toohello perdita di hello report. Tuttavia, potrebbe essere possibile toorerun hello reporting processo e l'output di hello rigenerare. In tal caso, non è importante una perdita di dati anche se il server di report hello viene raggiunto con un'emergenza, è possibile un livello di tolleranza per perdere parte dei dati di hello in hello server di report. In tal caso, i backup meno frequenti è un costo di hello tooreduce opzione.

### <a name="scenario-4-iaas-application-data-issues"></a>Scenario 4: Problemi relativi ai dati delle applicazioni IaaS

È presente un'applicazione che calcola, gestisce e fornisce dati commerciali cruciali, ad esempio le informazioni sui prezzi. Una nuova versione dell'applicazione contiene un bug del software che non è corretto calcolata hello prezzi e serviti dalla piattaforma hello hello esistente commerce dati danneggiati. In questo caso, hello migliore sarebbe toorevert toohello versione precedente di un'applicazione hello e dati hello prima. tooenable, questo backup periodici take del sistema.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Soluzione per il ripristino di emergenza: servizio Backup di Azure

Il [servizio Backup di Azure](https://azure.microsoft.com/services/backup/) può essere usato per il backup e il ripristino e funziona con [dischi gestiti](../../virtual-machines/windows/managed-disks-overview.md) e [non gestiti](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). È possibile creare un processo di backup con backup basati su orari specifici e con criteri semplici per il ripristino delle VM e la conservazione dei backup. 

Se si utilizza [dischi di archiviazione Premium](storage-premium-storage.md), [dischi gestiti](../../virtual-machines/windows/managed-disks-overview.md), o altri tipi di disco con hello [archiviazione localmente ridondante (LRS)](storage-redundancy.md#locally-redundant-storage) opzione, è particolarmente importante tooleverage backup di ripristino di emergenza periodici. Backup di Azure archivia i dati di hello nell'insieme di credenziali di servizi di ripristino per la conservazione a lungo termine. Scegliere hello [archiviazione con ridondanza geografica (GRS)](storage-redundancy.md#geo-redundant-storage) opzione per l'insieme di credenziali di servizi di ripristino Backup hello. Garantisce che i backup vengono replicate tooa area Azure diversa per protezione da calamità.

Per [dischi non gestito](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), è possibile usare il tipo di archiviazione con ridondanza di hello per i dischi di IaaS, ma assicurarsi che i Backup di Azure sia abilitato con l'opzione di archiviazione con ridondanza geografica per l'insieme di credenziali di servizi di ripristino hello hello.

**Se si utilizza hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opzione per i dischi non gestito, è comunque necessario snapshot coerenti per il Backup e ripristino di emergenza.** È necessario usare il [servizio Backup di Azure](https://azure.microsoft.com/services/backup/) o [snapshot coerenti](#alternative-solution-consistent-snapshots).

di seguito Hello è un riepilogo delle soluzioni di ripristino di emergenza.

| Scenario | Replica automatica | Soluzione di ripristino di emergenza |
| --- | --- | --- |
| *Dischi di Archiviazione Premium* | Locale ([Archiviazione con ridondanza locale](storage-redundancy.md#locally-redundant-storage)) | [Backup di Azure](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Locale ([Archiviazione con ridondanza locale](storage-redundancy.md#locally-redundant-storage)) | [Backup di Azure](https://azure.microsoft.com/services/backup/) |
| *Dischi non gestiti con archiviazione con ridondanza locale* | Locale ([Archiviazione con ridondanza locale](storage-redundancy.md#locally-redundant-storage)) | [Backup di Azure](https://azure.microsoft.com/services/backup/) |
| *Dischi non gestiti con archiviazione con ridondanza geografica* | Tra aree ([Archiviazione con ridondanza geografica](storage-redundancy.md#geo-redundant-storage)) | [Backup di Azure](https://azure.microsoft.com/services/backup/)<br/>[Snapshot coerenti](#alternative-solution-consistent-snapshots) |
| *Dischi non gestiti con archiviazione con ridondanza geografica e accesso in lettura* | Tra aree ([Archiviazione con ridondanza geografica e accesso in lettura](storage-redundancy.md#read-access-geo-redundant-storage)) | [Backup di Azure](https://azure.microsoft.com/services/backup/)<br/>[Snapshot coerenti](#alternative-solution-consistent-snapshots) |

Disponibilità elevata meglio possibile soddisfatti da tramite l'utilizzo di hello di dischi gestiti in un Set di disponibilità insieme ai Backup di Azure. Se si usano i dischi non gestiti, è comunque possibile usare Backup di Azure per il ripristino di emergenza. Se si è grado toouse Backup di Azure, quindi scegliere [snapshot coerenti](#alternative-solution-consistent-snapshots) come descritto in una sezione successiva è una soluzione alternativa per il Backup e ripristino di emergenza.

Le opzioni per la disponibilità elevata, il backup e il ripristino di emergenza a livello di applicazione o infrastruttura possono essere rappresentate come segue:

| *Level* | Disponibilità elevata   | Backup/Ripristino di emergenza |
| --- | --- | --- |
| *Applicazione* | SQL AlwaysOn | Backup di Azure |
| *Infrastruttura*  | Set di disponibilità  | Archiviazione con ridondanza geografica con snapshot coerenti |

### <a name="using-hello-azure-backup-service"></a>Utilizzo di hello servizio Backup di Azure

[Backup di Azure](../../backup/backup-azure-vms-introduction.md) può eseguire il backup delle macchine virtuali in esecuzione Windows o Linux toohello insieme di credenziali di Azure Recovery Services. Backup e ripristino dei dati aziendali critici è complicata dal fatto di hello che dati aziendali critici devono eseguire il backup durante le applicazioni di hello che producono hello dati sono in esecuzione. tooaddress, Azure Backup include backup coerenti con l'applicazione per i carichi di lavoro con tooensure servizio Shadow del Volume (VSS) hello che vengano scritti dati correttamente toostorage. Per le macchine virtuali Linux, solo i backup coerenti con i file sono possibili, poiché non dispone di funzionalità equivalenti tooVSS Linux.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Quando Azure Backup avvia un processo di backup in fase di hello pianificata, attiva estensione backup di hello installata in hello VM tootake uno snapshot del punto nel tempo. Viene eseguito uno snapshot in coordinamento con VSS tooget uno snapshot coerente dei dischi hello nella macchina virtuale hello senza tooshut, verso il basso. estensione del backup Hello in hello VM Scarica tutte le operazioni di scrittura prima di eseguire uno snapshot coerente hello di tutti i dischi di hello. Dopo che hello dello snapshot, i dati hello viene trasferiti dall'insieme di credenziali backup toohello Azure Backup. toomake hello processo di backup più efficiente, servizio hello identifica e trasferisce solo i blocchi di hello di dati che sono stati modificati dopo l'ultimo backup hello.


toorestore, è possibile visualizzare i backup disponibili hello tramite Backup di Azure e quindi avviare un ripristino. È possibile creare e ripristinare i backup di Azure tramite hello [portale di Azure](https://portal.azure.com/), [tramite PowerShell](../../backup/backup-azure-vms-automation.md ), o tramite hello [CLI di Azure](https://docs.microsoft.com/azure/xplat-cli-install). Per altre informazioni, vedere Backup di Azure.

### <a name="steps-tooenable-backup"></a>Passaggi tooEnable Backup

i passaggi seguenti Hello sono tooenable utilizzati in genere i backup delle macchine virtuali utilizzando hello [portale Azure](https://portal.azure.com/). La procedura presenterà alcune variazioni in base allo scenario esatto. Fare riferimento toohello [Azure Backup](../../backup/backup-azure-vms-introduction.md) documentazione per i dettagli completi. Backup di Azure [supporta anche le VM con Managed Disks](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Creare un insieme di credenziali di servizi di ripristino per una macchina virtuale tramite hello alla procedura seguente:

    a.  Utilizzo di hello [portale di Azure](https://portal.azure.com/), selezionare tutte le risorse e cercare "Insiemi di credenziali di servizi di ripristino".

    b.  In hello servizi di ripristino di insiemi di credenziali di menu, fare clic su Aggiungi e seguire hello passaggi toocreate un nuovo insieme di credenziali hello hello VM stessa area. Ad esempio, se la macchina virtuale è nell'area Stati Uniti occidentali, scegliere Stati Uniti occidentali per insieme di credenziali hello.

2.  Verificare la replica di archiviazione hello per hello appena creato l'insieme di credenziali. toodo, questo insieme di credenziali di accesso hello da hello servizi di ripristino gli insiemi di credenziali blade e passare toohello impostazioni/Backup configurazione. Verificare l'opzione di archiviazione con ridondanza geografica hello è selezionata per impostazione predefinita. Ciò garantisce che l'insieme di credenziali viene replicata automaticamente tooa data center secondario. Ad esempio, l'insieme di credenziali negli Stati Uniti occidentali saranno automaticamente replicati tooEast Stati Uniti.

3.  Configurare i criteri di backup hello e selezionare hello VM hello stessa interfaccia utente.

4.  Verificare che hello che backup Agent viene installato nella macchina virtuale hello. Se la macchina virtuale viene creata usando un'immagine della raccolta di Azure, l'agente di Backup hello è già installato. In caso contrario (ovvero, se si utilizza un'immagine personalizzata), utilizzare istruzioni troppo[hello installazione agente della macchina virtuale nella macchina virtuale hello](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Verificare che tale macchina virtuale di hello consente la connettività di rete per hello toofunction di servizio di backup. Seguire queste istruzioni per la [Connettività di rete](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Al termine di hello sopra passaggi, verrà eseguito il backup di hello a intervalli regolari, come specificato nel criterio di backup hello. Se necessario, è possibile attivare il backup prima di hello manualmente dal dashboard dell'insieme di credenziali di hello in hello portale di Azure.

Per l'automazione di Azure Backup tramite script, fare riferimento troppo[i cmdlet di PowerShell per il backup VM](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Procedura per il ripristino

Se è necessario toorepair o si ricompila una macchina virtuale, è possibile ripristinare hello macchina virtuale da uno qualsiasi dei punti di ripristino dei backup hello nell'insieme di credenziali hello. Esistono un paio di diverse opzioni per eseguire il ripristino di hello:

1.  È possibile creare una nuova VM come rappresentazione temporizzata della macchina virtuale sottoposta a backup.

2.  È possibile ripristinare i dischi hello e quindi usare il modello di hello per toocustomize VM hello e ricompilazione hello ripristinato macchina virtuale. 

Vedere le istruzioni troppo[macchine virtuali di Azure usare portale toorestore](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). documento di Hello illustra anche passaggi specifici di hello per il ripristino dei backup macchine virtuali toohello abbinata data center mediante l'insieme di credenziali di backup con ridondanza geografica nel caso di hello di emergenza in hello data center principale. In tal caso, Azure Backup utilizza il servizio di calcolo hello dalla macchina virtuale di hello area secondaria toocreate hello ripristinato.

È anche possibile usare PowerShell per il [ripristino di una VM](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) o per la [creazione di una nuova VM dai dischi ripristinati](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Soluzione alternativa: snapshot coerenti

Se si è grado toouse hello servizio Backup di Azure, è possibile implementare un proprio meccanismo di backup con snapshot. È complicato toocreate snapshot coerenti per tutti i dischi usati da una macchina virtuale e quindi replica tali area tooanother snapshot. Per questo motivo, Azure considera un'opzione migliore rispetto alla creazione di una soluzione personalizzata hello sfruttando il servizio di Backup. Se si utilizza l'archiviazione RA-GRS/archiviazione con ridondanza geografica per i dischi, gli snapshot vengono automaticamente replicati tooa data center secondario. Se si utilizza l'archiviazione con ridondanza locale per i dischi, è necessario dati hello tooreplicate manualmente. Per altre informazioni, vedere [Eseguire il backup dei dischi di VM non gestiti con snapshot incrementali](../../virtual-machines/windows/incremental-snapshots.md).

Uno snapshot è una rappresentazione di un oggetto in un punto specifico del tempo. Uno snapshot genererà fatturazione per hello incrementale dimensioni dati hello contiene. Per altre informazioni, vedere [Creare uno snapshot del BLOB](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Creazione di snapshot durante hello macchina virtuale è in esecuzione

Mentre è possibile creare uno snapshot in qualsiasi momento, se hello macchina virtuale è in esecuzione, è ancora dati da trasmettere in flusso toohello dischi e snapshot hello può contenere parziale operazioni in corso. Inoltre, se sono coinvolti più dischi, snapshot hello di dischi diversi potrebbe essersi verificato in momenti diversi, ovvero che questi snapshot potrebbero non essere coordinati. Ciò risulta particolarmente problematico per i volumi con striping, i cui file possono essere danneggiati in caso di modifiche durante il backup.

tooavoid questa situazione, il processo di backup hello deve implementare hello alla procedura seguente:

1.  Blocca tutti i dischi di hello

2.  Svuotare tutti hello scrittura in sospeso

3.  Quindi, [creare uno snapshot del blob](../blobs/storage-blob-snapshots.md) per tutti i dischi di hello

Alcune applicazioni di Windows come SQL Server forniscono un meccanismo di backup coordinato tramite backup coerenti con l'applicazione di VSS toocreate. In Linux, è possibile utilizzare uno strumento come fsfreeze per coordinare i dischi di hello, che forniranno i backup coerenti con i file, ma non applicazione-snapshot coerenti. Questo processo è complicato ed è quindi consigliabile prendere in considerazione l'uso di [Backup di Azure](../../backup/backup-azure-vms-introduction.md) o di una soluzione di backup di terze parti che implementa già questa funzionalità.

Hello sopra processo comporterà una raccolta di snapshot coordinato per tutti i dischi di macchina virtuale di hello, che rappresenta una visualizzazione in un momento specifica di hello macchina virtuale. Si tratta di un punto di ripristino del backup per hello macchina virtuale. È possibile ripetere il processo di hello in backup periodici toocreate di intervalli pianificati. Per vedere di seguito i passaggi di hello troppo[area tooanother i backup di copia hello](#copy-the-snapshots-to-another-region) per ripristino di emergenza.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Creazione di snapshot durante hello VM è offline

Un altro di backup coerenti con l'opzione di toocreate arresto hello VM e blob di acquisire snapshot di ogni disco. Questa procedura risulta più semplice rispetto alla coordinazione di snapshot di una VM in esecuzione ma richiede qualche minuto di inattività. Per questo processo, seguire questa procedura:

1. Arrestare VM hello.

2. Creare uno snapshot di ogni BLOB di disco rigido virtuale, operazione che richiede solo pochi secondi.

    toocreate uno snapshot, è possibile utilizzare [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), hello [API Rest di archiviazione Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [CLI di Azure](https://docs.microsoft.com/azure/xplat-cli-install), o uno dei hello le librerie Client di archiviazione di Azure, ad esempio [ libreria client di archiviazione Hello per .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Avvia macchina virtuale, che termina i tempi di inattività hello hello. In genere l'intero processo hello viene completata entro pochi minuti.

Questo processo produce una raccolta di snapshot coerenti per tutti i dischi di hello, fornire un punto di ripristino del backup per hello macchina virtuale. Vedere di seguito per area di hello passaggi toocopy hello snapshot tooanother per ripristino di emergenza.

### <a name="copy-hello-snapshots-tooanother-region"></a>Copia hello snapshot tooanother area

Creazione di snapshot hello da sola potrebbe non essere sufficiente per ripristino di emergenza. È anche necessario replicare area tooanother backup snapshot di hello.

Se si utilizza GRS o RA-GRS per i dischi, quindi hello gli snapshot sono area secondaria toohello replicati automaticamente. Possono essere presenti alcuni minuti di ritardo prima che la replica hello e se hello data center principale si arresta prima gli snapshot hello completare la replica, non sarà in grado di tooaccess snapshot hello hello data center secondario. probabilità di Hello di questo oggetto è ridotto.

> [!Note] 
> Solo con i dischi hello in un account GRS o RA-GRS non protegge hello VM in situazioni di emergenza. È necessario creare anche snapshot coordinati o usare Backup di Azure. Si tratta di toorecover richiesto uno stato coerente di tooa macchina virtuale.

Se si utilizza l'archiviazione con ridondanza locale, è necessario copiare account di archiviazione diverso tooa hello snapshot subito dopo la creazione dello snapshot hello. destinazione della copia Hello potrebbe essere un account di archiviazione con ridondanza locale in un'area diversa, risultante in copia hello in un'area remota. È inoltre possibile copiare account di archiviazione RA-GRS tooan snapshot hello in hello stessa area. In questo caso, snapshot hello sarà area secondaria remoto toohello replicate in modo differito. Il backup è protetto da situazioni di emergenza nel sito primario di hello dopo hello copia e la replica è stata completata.

toocopy gli snapshot incrementali per ripristino di emergenza in modo efficiente, rivedere le istruzioni di hello in [eseguire il backup di Azure i dischi di macchina virtuale non gestiti con snapshot incrementali](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Ripristino da snapshot

tooretrieve uno snapshot, copiarlo toomake un nuovo blob. Se si copia snapshot hello dall'account primario hello, è possibile copiare hello snapshot sul blob di base toohello snapshot hello, pertanto ripristino hello disco toohello snapshot. Questo è noto come snapshot hello innalzamento di livello. Se si copia di backup di snapshot hello da un account secondario (nel caso di hello di RA-GRS), deve essere copiato tooa account principale. È possibile copiare uno snapshot [tramite PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) o tramite l'utilità AzCopy hello. Per ulteriori informazioni, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

Nel caso di hello di macchine virtuali con più dischi, è necessario copiare tutto il punto di ripristino di snapshot hello che fanno parte di hello stesso coordinato. Quando si copiano BLOB VHD toowritable di hello snapshot, è possibile utilizzare la macchina virtuale utilizzando il modello di hello per hello VM toorecreate BLOB hello.

## <a name="other-options"></a>Altre opzioni

### <a name="sql-server"></a>SQL Server

SQL Server in esecuzione in una macchina virtuale ha un proprio toobackup funzionalità incorporate il tooAzure di database di SQL Server archiviazione Blob o una condivisione file. Se l'account di archiviazione hello è GRS o RA-GRS, è possibile accedere in hello account di archiviazione data center secondario in caso di hello un'emergenza, i backup con hello stesse restrizioni, come descritto in precedenza. Per altre informazioni, vedere [Backup e ripristino per SQL Server in Macchine virtuali di Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). In aggiunta toobackup e ripristino, [SQL Server di gruppi di disponibilità AlwaysOn](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) consente di mantenere le repliche secondarie di database toogreatly ridurre i tempi di ripristino di emergenza hello.

## <a name="other-considerations"></a>Altre considerazioni

In questo articolo ha descritto come toobackup o acquisire snapshot nelle macchine virtuali e i relativi dischi toosupport il ripristino di emergenza e come toouse tali toorecover. Con il modello di gestione risorse di Azure hello, molte persone usano modelli toocreate le proprie macchine virtuali e altre infrastrutture in Azure. È possibile utilizzare un toocreate modello una macchina virtuale con hello stessa configurazione ogni volta. Se si utilizzano immagini personalizzate per la creazione delle macchine virtuali, è necessario anche assicurarsi che le immagini sono protetti tramite un toostore account RA-GRS li.

È quindi possibile che il processo di backup sia una combinazione di due elementi:

1. Dati di backup hello (dischi)
2. Configurazione di backup hello (modelli, immagini personalizzate)

A seconda opzione backup hello che scelta, è possibile backup hello toohandle di dati hello e configurazione di hello, o servizio di backup hello può gestire tutto che per l'utente.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Appendice - impatto hello di archiviazione con ridondanza locale, GRS e RA-GRS

Per gli account di archiviazione di Azure sono disponibili tre tipi di ridondanza dei dati da tenere in considerazione per il ripristino di emergenza, ovvero archiviazione con ridondanza locale, archiviazione con ridondanza geografica e archiviazione con ridondanza geografica e accesso in lettura. 

Localmente archiviazione ridondante (LRS) mantiene tre copie dei dati di hello hello nello stesso data center. Quando si scrivono dati hello, vengono aggiornate tutte le tre copie prima del completamento toohello chiamante, in modo che si sono identici. Il disco è protetto da errori locali, poiché è molto improbabile che tutte le tre copie potrebbero essere interessate hello contemporaneamente. Nel caso di hello di archiviazione con ridondanza locale, non è non ridondanza geografica, disco hello non è protetta da errori irreversibili che possono influire su un'unità di intero data center o di archiviazione.

Con GRS e RA-GRS, vengono mantenute tre copie dei dati nell'area primaria di hello (selezionato dall'utente) e vengono mantenute tre più copie dei dati in un'area secondaria corrispondente (impostata da Azure). Ad esempio, se si archiviano dati negli Stati Uniti occidentali, dati hello sarà tooEast replicati negli Stati Uniti. Questa operazione viene eseguita in modo asincrono e si verifica un ritardo di piccole dimensioni tra gli aggiornamenti toohello primario e secondario. Le repliche di dischi hello nel sito secondario hello sono coerenti in base al disco (con ritardo hello), ma le repliche di più dischi attivi potrebbero non essere sincronizzate **reciprocamente**. sono necessari toohave repliche coerenti in più dischi, snapshot coerenti.

Hello differenza principale tra GRS e RA-GRS è con RA-GRS, è possibile leggere la copia secondaria hello in qualsiasi momento. Se si verifica un problema che esegue il rendering dei dati di hello nell'area primaria hello inaccessibile, hello team di Azure renderà ogni accesso toorestore sforzo. Se hello primario è inattivo, se si dispone di RA-GRS è abilitata, è possibile accedere a dati hello in hello data center secondario. Pertanto, se si prevede di tooread dalla replica hello mentre hello primario non è accessibile, quindi RA-GRS da considerare.

Se si scopre toobe un'interruzione significativa, hello team di Azure è possibile attivare un failover geografico e modificare hello primario DNS voci toopoint toosecondary archiviazione. A questo punto, se sono entrambi GRS o RA-GRS è abilitata, è possibile accedere ai dati di hello nell'area di hello utilizzati hello toobe secondario. In altre parole, se l'account di archiviazione è l'archiviazione con ridondanza geografica e si è verificato un problema, è possibile accedere archiviazione secondaria hello solo se è disponibile un failover geografico.

Per ulteriori informazioni, vedere [quali toodo se si verifica un'interruzione di servizio di archiviazione Azure](storage-disaster-recovery-guidance.md). 

Si noti che Microsoft controlla il verificarsi di un failover. Il failover non è controllato per i singoli account di archiviazione e non viene quindi determinato dai singoli clienti. tooimplement il ripristino di emergenza per gli account di archiviazione specifico o i dischi di macchina virtuale, è necessario utilizzare le tecniche di hello descritte in precedenza in questo articolo.
