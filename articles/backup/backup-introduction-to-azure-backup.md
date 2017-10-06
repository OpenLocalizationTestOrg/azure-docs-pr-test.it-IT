---
title: "aaaWhat è Azure Backup? | Microsoft Docs"
description: Utilizzare tooback Backup di Azure e ripristino di dati e i carichi di lavoro da Windows Server, workstation Windows, server System Center DPM e macchine virtuali di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup e ripristino; servizi di ripristino; soluzioni di backup
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Panoramica delle funzionalità di hello in Backup di Azure
Backup di Azure è servizio hello basato su Azure è possibile utilizzare tooback (o proteggere) e il ripristino dei dati nel cloud di Microsoft hello. Backup di Azure sostituisce la soluzione di backup locale o esterna esistente con una soluzione basata sul cloud affidabile, sicura e conveniente. Backup di Azure offre più i componenti disponibili per download e distribuzione su computer appropriato hello, server, o nel cloud hello. componente Hello o agent, da distribuire dipende da ciò che si desidera tooprotect. Tutti i componenti di Backup di Azure (indipendentemente dal fatto per la protezione dei dati in locale o nel cloud hello) possono essere utilizzato tooback le credenziali di servizi di ripristino dati tooa in Azure. Vedere hello [tabella i componenti di Azure Backup](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (più avanti in questo articolo) per informazioni su quali dati specifici del componente toouse tooprotect, le applicazioni o carichi di lavoro.

[Panoramica video di Backup di Azure](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Perché usare Backup di Azure
Le soluzioni tradizionali di backup sono stati ulteriormente sviluppati cloud hello tootreat come un endpoint, o destinazione di archiviazione statica, nastro o toodisks simili. Anche se questo approccio è semplice, è limitato e non usufruire di una piattaforma cloud sottostante, che converte tooan costosa inefficiente soluzione. Altre soluzioni sono costose perché alla fine si paga hello tipo errato, o l'archiviazione che non è necessario. Altre soluzioni spesso sono inefficienti perché non offrono è tipo hello o la quantità di spazio di archiviazione che è necessario o attività amministrative richiedono troppo tempo. Backup di Azure offre invece i vantaggi principali seguenti:

**Gestione dell'archiviazione automatica** : gli ambienti ibridi richiedono spesso l'archiviazione eterogenea - alcuni locali e alcuni in hello cloud. Con Backup di Azure non sono previsti costi per l'uso di dispositivi di archiviazione locale. Backup di Azure alloca e gestisce automaticamente le risorse di archiviazione di backup e usa un modello di pagamento in base al consumo. Pagamento-come-si-utilizzo significa che si paga solo per l'archiviazione di hello utilizzata. Per ulteriori informazioni, vedere hello [Azure prezzi articolo](https://azure.microsoft.com/pricing/details/backup).

**Scalabilità illimitata** - Backup di Azure Usa hello power sottostante e senza limiti di scala di hello Azure cloud toodeliver a disponibilità elevata - con alcuna manutenzione o il monitoraggio di overhead. È possibile impostare le informazioni di tooprovide avvisi sugli eventi, ma non è necessario tooworry sulla disponibilità elevata per i dati nel cloud hello.

**Più opzioni di archiviazione**. Un aspetto della disponibilità elevata è la replica di archiviazione. Backup di Azure offre due tipi di replica: [archiviazione con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage) e [archiviazione con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage). Scegliere l'opzione di archiviazione di backup hello in base alle esigenze:

* I dati vengono replicati archiviazione localmente ridondante (LRS) tre volte, crea tre copie dei dati, in un determinato Data Center in hello stessa area. L'archiviazione con ridondanza locale è un'opzione a costo contenuto per la protezione dei dati da errori hardware locali.

* Archiviazione con ridondanza geografica (GRS) consente di replicare l'area secondaria tooa dati (centinaia di miglia dalla posizione primaria di hello hello dei dati di origine). L'archiviazione con ridondanza geografica è più costosa dell'archiviazione con ridondanza locale, ma offre un livello più elevato di durabilità per i dati, anche in presenza di un'interruzione di area.

**Trasferimento di dati senza limiti** - Backup di Azure non limita la quantità hello di connessioni in ingresso o in uscita di trasferimento dei dati. Anche i Backup di Azure non viene addebitata l'hello i dati trasferiti. Tuttavia, se si utilizza hello importazione/esportazione di Azure servizio tooimport grandi quantità di dati, è un costo associato ai dati in ingresso. Per altre informazioni su questi costi, vedere [Flusso di lavoro del backup offline in Backup di Azure](backup-azure-backup-import-export.md). Dati in uscita fa riferimento toodata trasferito da un insieme di credenziali di servizi di ripristino durante un'operazione di ripristino.

**La crittografia dei dati** -consente la crittografia dei dati per la trasmissione sicura e l'archiviazione dei dati nel cloud pubblico hello. Archiviare passphrase di crittografia hello in locale e si è mai trasmessi o archiviato in Azure. Se è necessario toorestore qualsiasi hello, solo hanno passphrase di crittografia di dati o della chiave.

**Backup coerenti con l'applicazione** -backup di un file server, una macchina virtuale o un database SQL, la necessità che dispone di un punto di ripristino tutti tooknow necessari copia di backup di dati toorestore hello. Backup di Azure offre backup coerenti con l'applicazione, che garantire correzioni aggiuntive non sono necessari toorestore hello dati. Ripristino dei dati coerenti con l'applicazione riduce il tempo di ripristino hello, consentendo tooa restituito da tooquickly dello stato di esecuzione.

**Conservazione a lungo termine** -anziché passare copie di backup da disco tootape e mobile hello nastro tooan luogo protetto fuori sede, è possibile utilizzare Azure per la conservazione a breve termine e a lungo termine. Azure non limita hello tempo i dati rimangono nell'insieme di credenziali di Backup o i servizi di ripristino di. È possibile conservare i dati in un insieme di credenziali per il tempo desiderato. Backup di Azure ha un limite di 9999 punti di ripristino per ogni istanza protetta. Vedere hello [Backup e conservazione](backup-introduction-to-azure-backup.md#backup-and-retention) sezione in questo articolo per una spiegazione di questo limite può impatto esigenze di backup.  

## <a name="which-azure-backup-components-should-i-use"></a>Quali componenti di Backup di Azure è opportuno usare?
Se si è sicuri di quale componente di Backup di Azure funziona per le proprie esigenze, vedere hello seguente tabella per informazioni su ciò che è possibile proteggere con ciascun componente. Hello portale di Azure fornisce una procedura guidata, integrato nel portale di hello tooguide tramite scelta hello toodownload componente e distribuire. la procedura guidata Hello, che fa parte di hello creazione dell'insieme di credenziali di servizi di ripristino, illustra hello procedura per la selezione di un obiettivo di backup e scegliendo tooprotect di dati o un'applicazione hello.

| Componente | Vantaggi | Limiti | Quali elementi vengono protetti? | Dove vengono archiviati i backup? |
| --- | --- | --- | --- | --- |
| Agente di Backup di Azure (MARS) |<li>Backup di file e cartelle nel sistema operativo Windows fisico o virtuale. Le VM possono trovarsi in locale o in Azure.<li>Non è necessario un server di backup separato. |<li>Backup 3 volte al giorno <li>Senza riconoscimento dell'applicazione; ripristino solo a livello di file, cartelle e volumi, <li>  Nessun supporto per Linux. |<li>File, <li>Cartelle |Insieme di credenziali dei servizi di ripristino |
| System Center DPM |<li>Snapshot con riconoscimento dell'applicazione (servizio Copia Shadow del volume)<li>Completa la flessibilità per quando il backup tootake<li>Granularità ripristino (tutto)<li>Possibilità di usare un insieme di credenziali di Servizi di ripristino<li>Supporto di Linux in macchine virtuali Hyper-V e VMware <li>Eseguire il backup e il ripristino di VM VMware usando DPM 2012 R2 |Non è possibile eseguire il backup del carico di lavoro di Oracle.|<li>File, <li>Cartelle,<li> Volumi, <li>Macchine virtuali,<li> Applicazioni,<li> Carichi di lavoro |<li>Insieme di credenziali di Servizi di ripristino,<li> Disco collegato al computer locale,<li>  Nastro (solo in locale) |
| Server di backup di Azure |<li>Snapshot con riconoscimento dell'app (servizio Copia Shadow del volume)<li>Completa la flessibilità per quando il backup tootake<li>Granularità ripristino (tutto)<li>Possibilità di usare un insieme di credenziali di Servizi di ripristino<li>Supporto di Linux in macchine virtuali Hyper-V e VMware<li>Eseguire il backup e il ripristino di VM VMware <li>Non richiede una licenza per System Center |<li>Non è possibile eseguire il backup del carico di lavoro di Oracle.<li>Richiede sempre una sottoscrizione di Azure attiva<li>Nessun supporto per il backup su nastro |<li>File, <li>Cartelle,<li> Volumi, <li>Macchine virtuali,<li> Applicazioni,<li> Carichi di lavoro |<li>Insieme di credenziali di Servizi di ripristino,<li> Disco collegato al computer locale |
| Backup di VM IaaS di Azure |<li>Backup nativi per Windows/Linux<li>Non è richiesta l'installazione un agente specifico<li>Backup a livello di infrastruttura senza che sia necessaria un'infrastruttura di backup |<li>Backup delle VM una volta al giorno <li>Ripristino delle VM solo a livello di disco<li>Non può eseguire il backup in locale |<li>Macchine virtuali, <li>Tutti i dischi (tramite PowerShell) |<p>Insieme di credenziali dei servizi di ripristino</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Quali sono gli scenari di distribuzione hello per ogni componente?
| Componente | Può essere distribuito in Azure? | Può essere distribuito in locale? | Archiviazione di destinazione supportata |
| --- | --- | --- | --- |
| Agente di Backup di Azure (MARS) |<p>**Sì**</p> <p>l'agente di Backup di Azure Hello può essere distribuito in qualsiasi macchina virtuale di Windows Server in esecuzione in Azure.</p> |<p>**Sì**</p> <p>l'agente di Backup Hello può essere distribuito su qualsiasi macchina virtuale Windows Server o computer fisico.</p> |<p>Insieme di credenziali dei servizi di ripristino</p> |
| System Center DPM |<p>**Sì**</p><p>Altre informazioni, vedere [come tooprotect carichi di lavoro in Azure tramite System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Sì**</p> <p>Altre informazioni, vedere [come tooprotect carichi di lavoro e macchine virtuali nel Data Center](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Disco collegato al computer locale,</p> <p>Insieme di credenziali di Servizi di ripristino,</p> <p>nastro (solo in locale)</p> |
| Server di backup di Azure |<p>**Sì**</p><p>Altre informazioni, vedere [come tooprotect carichi di lavoro in Azure tramite Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>**Sì**</p> <p>Altre informazioni, vedere [come tooprotect carichi di lavoro in Azure tramite Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>Disco collegato al computer locale,</p> <p>Insieme di credenziali dei servizi di ripristino</p> |
| Backup di VM IaaS di Azure |<p>**Sì**</p><p>Parte dell'infrastruttura di Azure</p><p>Specializzato per il [backup di macchine virtuali di infrastruttura distribuita come servizio (IaaS) di Azure](backup-azure-vms-introduction.md).</p> |<p>**No**</p> <p>Utilizzare System Center DPM tooback backup di macchine virtuali nel Data Center.</p> |<p>Insieme di credenziali dei servizi di ripristino</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Applicazioni e carichi di lavoro di cui è possibile eseguire il backup
Hello nella tabella seguente fornisce una matrice di dati hello e carichi di lavoro che possono essere protetti tramite Azure Backup. documentazione sulla distribuzione di toohello di collegamenti per la soluzione nella colonna di soluzioni di Hello Azure Backup. Ogni componente di Backup di Azure può essere distribuito con un modello di distribuzione classica (distribuzione di Service Manager) o di Resource Manager.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Dati o carico di lavoro | Ambiente di origine | Soluzione di Backup di Azure |
| --- | --- | --- |
| File e cartelle |Windows Server |<p>[Agente di Backup di Azure](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| File e cartelle |Computer Windows |<p>[Agente di Backup di Azure](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| Macchina virtuale Hyper-V (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| Macchina virtuale Hyper-V (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente Azure Backup hello)</p> <p>[Azure Backup Server](backup-azure-microsoft-azure-backup.md) (include l'agente Azure Backup hello)</p> |
| VM IaaS di Azure (Windows) |in esecuzione in Azure |[Backup di Azure (estensione VM)](backup-azure-vms-introduction.md) |
| VM IaaS di Azure (Linux) |in esecuzione in Azure |[Backup di Azure (estensione VM)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Supporto Linux
Hello nella tabella seguente sono illustrati i componenti di Azure Backup hello che dispongono del supporto per Linux.  

| Componente | Supporto Linux (approvato per Azure) |
| --- | --- |
| Agente di Backup di Azure (MARS) |No (solo agente basato su Windows) |
| System Center DPM |<li> Backup coerenti con i file di macchine virtuali guest Linux in Hyper-V e VMWare<br/> <li> Ripristino di macchine virtuali guest Linux in Hyper-V e VMWare </br> </br>  *Backup coerente con i file non disponibile per le VM di Azure* <br/> |
| Server di backup di Azure |<li>Backup coerenti con i file di macchine virtuali guest Linux in Hyper-V e VMWare<br/> <li> Ripristino di macchine virtuali guest Linux in Hyper-V e VMWare </br></br> *Backup coerente con i file non disponibile per le VM di Azure*  |
| Backup di VM IaaS di Azure |Backup coerente con le applicazioni tramite il [framework dello script di pre-backup e post-backup](backup-azure-linux-app-consistent.md)<br/> [Ripristino granulare di file](backup-azure-restore-files-from-vm.md)<br/> [Ripristinare tutti i dischi di macchina virtuale](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Ripristino della macchina virtuale](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Uso di macchine virtuali di Archiviazione Premium con Backup di Azure
Backup di Azure protegge le macchine virtuali di Archiviazione Premium. Archiviazione Premium di Azure è un'unità SSD (unità SSD)-basato su carichi di lavoro I/O-con utilizzo intensivo di archiviazione progettata toosupport. Archiviazione Premium è una soluzione interessante per i carichi di lavoro delle macchine virtuali. Per ulteriori informazioni sull'archiviazione Premium, vedere l'articolo hello [archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro di macchina virtuale Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Backup di macchine virtuali di Archiviazione Premium
Durante il backup di macchine virtuali di archiviazione Premium, il servizio di Backup hello crea un percorso temporaneo di gestione temporanea, denominata "AzureBackup-", nell'account di archiviazione Premium hello. dimensioni Hello di hello percorso di gestione temporanea sono toohello uguale di snapshot di punto di ripristino hello. Assicurarsi di hello account di archiviazione Premium è sufficiente spazio libero tooaccommodate hello temporaneo percorso di gestione temporanea. Per ulteriori informazioni, vedere l'articolo hello [dei limiti di archiviazione premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Al termine del processo di backup hello, hello percorso di gestione temporanea viene eliminata. Hello prezzi di archiviazione utilizzato per hello percorso di gestione temporanea sono coerenti con tutte [prezzi di archiviazione Premium](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Non modificare o modificare hello percorso di gestione temporanea.
>
>

### <a name="restore-premium-storage-vms"></a>Ripristino di macchine virtuali di Archiviazione Premium
Macchine virtuali di archiviazione Premium può essere ripristinato tooeither archiviazione Premium o toonormal archiviazione. Il ripristino tooPremium di back-una macchina virtuale di archiviazione Premium ripristino punto di archiviazione è normale processo di ripristino di hello. Tuttavia, può essere conveniente toorestore uno spazio di archiviazione macchina virtuale di archiviazione Premium toostandard punto di ripristino. Se è necessario un subset di file da hello VM, è possibile utilizzare questo tipo di ripristino.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Uso delle macchine virtuali con dischi gestiti con Backup di Azure
Backup di Azure protegge le macchine virtuali con dischi gestiti. I dischi gestiti rendono superflua la gestione degli account di archiviazione delle macchine virtuali e semplificano notevolmente il provisioning delle VM.

### <a name="back-up-managed-disk-vms"></a>Eseguire il backup di macchine virtuali con dischi gestiti
Il backup delle macchine virtuali nei dischi gestiti non presenta differenze rispetto al backup delle macchine virtuali di Resource Manager. Nel portale di Azure hello, è possibile configurare il processo backup di hello direttamente da hello visualizzazione della macchina virtuale o da servizi di ripristino hello insieme di credenziali di visualizzazione. È possibile eseguire il backup delle macchine virtuali nei dischi gestiti tramite raccolte RestorePoint basate su dischi gestiti. Backup di Azure supporta anche il backup delle macchine virtuali con dischi gestiti crittografate con Crittografia dischi di Azure.

### <a name="restore-managed-disk-vms"></a>Ripristinare le macchine virtuali con dischi gestiti
Backup di Azure consente toorestore una macchina virtuale completata con dischi gestiti, o il ripristino gestito di account di archiviazione tooa dischi. Azure gestisce i dischi di hello gestito durante il processo di ripristino hello. (Customer hello) gestire account di archiviazione hello creato come parte del processo di ripristino hello. Quando il ripristino gestito crittografate macchine virtuali, hello chiavi e segreti della macchina virtuale devono essere presenti nell'operazione di ripristino hello toostarting precedente hello insieme di credenziali chiave.

## <a name="what-are-hello-features-of-each-backup-component"></a>Quali sono le funzionalità di hello di ogni componente di Backup?
Hello le sezioni seguenti fornisce le tabelle che consentono di riepilogare disponibilità hello o il supporto di diverse funzionalità in ogni componente di Backup di Azure. Vedere le informazioni di hello ogni per ulteriore assistenza, dettagli nella tabella seguente.

### <a name="storage"></a>Archiviazione
| Funzionalità | Agente di Backup di Azure | System Center DPM | Server di backup di Azure | Backup di VM IaaS di Azure |
| --- | --- | --- | --- | --- |
| Insieme di credenziali dei servizi di ripristino |![Sì][green] |![Sì][green] |![Sì][green] |![sì][green] |
| Archiviazione su disco | |![sì][green] |![sì][green] | |
| Archiviazione su nastro | |![Sì][green] | | |
| Compressione <br/>(nell'insieme di credenziali di Servizi di ripristino) |![Sì][green] |![Sì][green] |![sì][green] | |
| Backup incrementale |![sì][green] |![Sì][green] |![Sì][green] |![sì][green] |
| Deduplicazione dei dischi | |![Parzialmente][yellow] |![Parzialmente][yellow] | | |

![chiave tabella](./media/backup-introduction-to-azure-backup/table-key.png)

insieme di credenziali di servizi di ripristino Hello è una destinazione di archiviazione preferito hello in tutti i componenti. System Center DPM e il Server di Backup di Azure sono inoltre disponibili hello opzione toohave una copia locale del disco. Tuttavia, solo System Center DPM fornisce dispositivo di archiviazione di hello opzione toowrite dati tooa nastro.

#### <a name="compression"></a>Compressione
I backup vengono compressi hello tooreduce richiesto spazio di archiviazione. Hello unico componente che non utilizza la compressione è l'estensione della macchina virtuale hello. copie di estensione VM Hello tutti i dati di backup di toohello di account servizi di ripristino l'archiviazione dell'insieme di credenziali in hello stessa area. Quando si trasferiscono dati hello, viene usata alcuna compressione. Il trasferimento dei dati di hello senza compressione leggermente ingrandisce archiviazione hello utilizzato. Tuttavia, l'archiviazione dei dati di hello senza la compressione consente di ripristino più veloce, fosse necessario tale punto di ripristino.


#### <a name="disk-deduplication"></a>Deduplicazione dei dischi
È possibile usare la deduplicazione durante la distribuzione di System Center DPM o del server di Backup di Azure [in una macchina virtuale Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server esegue la deduplicazione dei dati (a livello di host hello) nei dischi rigidi virtuali (VHD) che sono collegati toohello di macchina virtuale come archiviazione di backup.

> [!NOTE]
> La deduplicazione non è disponibile in Azure per i componenti di Backup. Quando System Center DPM e il Server di Backup vengono distribuiti in Azure, i dischi di archiviazione hello collegati toohello che macchina virtuale non può essere deduplicati.
>
>

### <a name="incremental-backup-explained"></a>Descrizione del backup incrementale
Ogni componente di Backup di Azure supporta il backup incrementale indipendentemente dall'archiviazione di destinazione hello (disco, nastro, insieme di credenziali di servizi di ripristino). Backup incrementale assicura che i backup archiviazione e l'ora efficiente, trasferendo solo le modifiche apportate dall'ultimo backup hello.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Confronto tra backup completo, differenziale e incrementale

L'uso dell'archiviazione, l'obiettivo del tempo di ripristino (RTO) e l'uso della rete variano per ogni metodo di backup. tookeep hello backup costo totale di proprietà (TCO) verso il basso, è necessario toounderstand come soluzione di backup migliore hello toochoose. Hello immagine seguente confronta Backup completo, Backup differenziali e Backup incrementale. Nell'immagine di hello, origine dati, che un oggetto è composto da 10 archiviazione blocchi A1-A10, che viene eseguito il backup mensile. Blocchi A2, A3, A4 e A9 modificare in hello primo mese e bloccare le modifiche di A5 in hello mese successivo.

![immagine che mostra i confronti dei metodi di backup](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Con **Full Backup**, ogni copia di backup contiene hello intera origine dei dati. Il backup completo usa una grande quantità di larghezza di banda e archiviazione di rete, ogni volta che viene trasferita una copia di backup.

**Backup differenziale** archivia solo hello blocchi modificati dall'hello backup completo iniziale, che comporta una minore quantità di consumo di rete e archiviazione. I backup differenziali non conservano copie ridondanti dei dati non modificati. Tuttavia, poiché i blocchi di dati di hello rimangono invariati tra i backup successivi verranno trasferiti, archiviati, backup differenziali sono inefficienti. In hello secondo mese, i blocchi modificati A2, A3, A4 e A9 vengono eseguito il backup. In hello terzo mese, questi stessi blocchi di backup vengono eseguiti, oltre a blocco modificata A5. Hello dei blocchi modificato continuare toobe eseguito fino a quando non si verifica di backup completo successivo hello.

**Backup incrementale** raggiunge ad elevata efficienza di archiviazione e rete archiviando solo i blocchi di hello di dati modificati dal backup precedente hello. Con backup incrementale, non è necessario tootake backup completo. Nell'esempio hello, dopo l'esecuzione di backup completo hello è per hello primo mese, i blocchi modificati A2, A3, A4 e A9 sono contrassegnati come modificati e trasferiti per hello secondo mese. In hello terzo mese, viene modificato solo blocco A5 è contrassegnato e trasferiti. Spostare meno dati comporta risparmi in termini di risorse di archiviazione e di rete, per un minor costo totale di proprietà.   

### <a name="security"></a>Sicurezza
| Funzionalità | Agente di Backup di Azure | System Center DPM | Server di backup di Azure | Backup di VM IaaS di Azure |
| --- | --- | --- | --- | --- |
| Sicurezza di rete<br/> (tooAzure) |![Sì][green] |![Sì][green] |![sì][green] |![Parzialmente][yellow] |
| Sicurezza dei dati<br/> (in Azure) |![Sì][green] |![Sì][green] |![sì][green] |![Parzialmente][yellow] |

![chiave tabella](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Sicurezza di rete
Tutto il traffico da toohello il server di che dell'insieme di credenziali di servizi di ripristino backup viene crittografato usando Advanced Encryption Standard 256. dati di backup Hello viene inviati tramite una connessione HTTPS protetta. dati di backup Hello vengono inoltre archiviati nell'insieme di credenziali di servizi di ripristino hello in forma crittografata. Solo, hello clienti di Azure, è hello passphrase toounlock questi dati. Microsoft non può decrittografare i dati di backup hello in qualsiasi momento.

> [!WARNING]
> Dopo aver stabilito l'insieme di credenziali di servizi di ripristino hello, solo si dispone di accesso toohello crittografia chiave. Microsoft non mantiene una copia della chiave di crittografia e non dispone di accesso toohello chiave. Se la chiave hello posizione errata, Microsoft non è possibile ripristinare i dati di backup hello.
>
>

#### <a name="data-security"></a>Sicurezza dei dati
Backup di macchine virtuali di Azure richiede l'impostazione di crittografia *all'interno di* macchina virtuale hello. Usare BitLocker nelle macchine virtuali Windows e **DM-Crypt** nelle macchine virtuali Linux. Backup di Azure non esegue automaticamente la crittografia dei dati di backup provenienti da questo percorso.

### <a name="network"></a>Rete
| Funzionalità | Agente di Backup di Azure | System Center DPM | Server di backup di Azure | Backup di VM IaaS di Azure |
| --- | --- | --- | --- | --- |
| Compressione di rete <br/>(troppo**backup server**) | |![Sì][green] |![Sì][green] | |
| Compressione di rete <br/>(troppo**insieme di credenziali di servizi di ripristino**) |![Sì][green] |![Sì][green] |![Sì][green] | |
| Protocollo di rete <br/>(troppo**backup server**) | |TCP |TCP | |
| Protocollo di rete <br/>(troppo**insieme di credenziali di servizi di ripristino**) |HTTPS |HTTPS |HTTPS |HTTPS |

![chiave tabella](./media/backup-introduction-to-azure-backup/table-key-2.png)

Hello estensione della macchina virtuale (in hello VM IaaS) legge dati hello direttamente dall'account di archiviazione Azure hello in rete di archiviazione hello, pertanto non è necessario toocompress il traffico.

Se si utilizza un server di System Center DPM o di un Server di Backup di Azure come un server di backup secondario, comprimere i dati di hello dal server di backup toohello hello server primario. La compressione dei dati prima di eseguirne il backup tooDPM o il Server di Backup di Azure, risparmiare larghezza di banda.

#### <a name="network-throttling"></a>Limitazione della larghezza di banda della rete
l'agente di Backup di Azure Hello offre la limitazione delle richieste di rete, che consente di toocontrol modalità di utilizzo della larghezza di banda di rete durante il trasferimento dei dati. La limitazione delle richieste può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico internet. La limitazione delle richieste per i dati di trasferimento applica tooback backup e ripristino.

## <a name="backup-and-retention"></a>Backup e conservazione

Backup di Azure ha un limite di 9999 punti di ripristino, noti anche come copie di backup o snapshot, per ogni *istanza protetta*. Un'istanza protetta è un computer, un server (fisico o virtuale) o un carico di lavoro configurato tooback backup tooAzure dati. Per ulteriori informazioni, vedere la sezione hello, [che cos'è un'istanza protetta](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Un'istanza è protetta dopo il salvataggio di una copia di backup dei dati. copia di dati di backup Hello è protezione hello. Se i dati di origine hello è stata persi o danneggiato, copia di backup hello può ripristinare i dati di origine hello. Hello nella tabella seguente mostra frequenza backup hello massima per ogni componente. Configurazione dei criteri di backup determina la rapidità si utilizzano i punti di ripristino hello. Ad esempio, se si crea un punto di ripristino ogni giorno, è possibile mantenere i punti di ripristino per 27 anni prima di eseguirli. Se si crea un punto di ripristino mensili, puoi mantenere i punti di ripristino 833 anni precedenti si esaurisca. Hello servizio di Backup non impostare un limite di tempo di scadenza in un punto di ripristino.

|  | Agente di Backup di Azure | System Center DPM | Server di backup di Azure | Backup di VM IaaS di Azure |
| --- | --- | --- | --- | --- |
| Frequenza di backup<br/> (insieme di credenziali tooRecovery Services) |3 backup al giorno |2 backup al giorno |2 backup al giorno |1 backup al giorno |
| Frequenza di backup<br/> (toodisk) |Non applicabile |<li>Ogni 15 minuti per SQL Server <li>Ogni ora per altri carichi di lavoro |<li>Ogni 15 minuti per SQL Server <li>Ogni ora per altri carichi di lavoro</p> |Non applicabile |
| Opzioni di conservazione |Giornaliera, settimanale, mensile, annuale |Giornaliera, settimanale, mensile, annuale |Giornaliera, settimanale, mensile, annuale |Giornaliera, settimanale, mensile, annuale |
| Punti di ripristino massimo per ogni istanza protetta |9999|9999|9999|9999|
| Periodo massimo di conservazione |Dipende dalla frequenza dei backup |Dipende dalla frequenza dei backup |Dipende dalla frequenza dei backup |Dipende dalla frequenza dei backup |
| Punti di ripristino nel disco locale |Non applicabile |<li>64 per i file server<li>448 per i server applicazioni |<li>64 per i file server<li>448 per i server applicazioni |Non applicabile |
| Punti di ripristino su nastro |Non applicabile |Senza limiti |Non applicabile |Non applicabile |

## <a name="what-is-a-protected-instance"></a>Che cos'è un'istanza protetta?
Un'istanza protetta è un computer di riferimento generico tooa Windows, un server (fisico o virtuale), database SQL o che è stato configurato tooback backup tooAzure. Un'istanza è protetta quando si configura un criterio di backup per il computer di hello, server o database e crea una copia di backup dei dati di hello. Le copie successive hello dei dati di backup per l'istanza protetto (denominati punti di ripristino), aumentare hello di spazio di archiviazione utilizzato. È possibile creare i punti di ripristino too9999 per un'istanza protetta. Se si elimina un punto di ripristino dall'archiviazione, non viene considerato in totale punto di ripristino 9999 hello.
Alcuni esempi comuni di istanze protette sono macchine virtuali, i server applicazioni, database e del sistema operativo di Windows hello personal computer. ad esempio:

* Una macchina virtuale in esecuzione dell'infrastruttura di hypervisor Hyper-V o IaaS di Azure hello. sistemi operativi guest di Hello per la macchina virtuale hello può essere Windows Server o Linux.
* Un server applicazioni: server applicazioni hello può essere un computer fisico o macchina virtuale che esegue Windows Server e carichi di lavoro con dati che devono essere toobe sottoposti a backup. Carichi di lavoro comuni sono Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server e il ruolo File Server hello in Windows Server. tooback di questi carichi di lavoro, è necessario System Center Data Protection Manager (DPM) o il Server di Backup di Azure.
* Un personal computer, workstation o sistema operativo di Windows hello portatile.


## <a name="what-is-a-recovery-services-vault"></a>Informazioni sull'insieme di credenziali di Servizi di ripristino
Un insieme di credenziali di servizi di ripristino è che un'entità di archiviazione online in Azure utilizzata toohold dati, ad esempio copie di backup, i punti di ripristino e i criteri di backup. È possibile utilizzare i dati di backup toohold gli insiemi di credenziali di servizi di ripristino per le workstation e server in locale e servizi di Azure. Gli archivi di servizi di ripristino rendono tooorganize semplice ai dati di backup, riducendo l'overhead di gestione. È possibile creare un numero qualsiasi di insiemi di credenziali di Servizi di ripristino all'interno di una sottoscrizione.

I criteri di backup, si basano su Azure Service Manager, sono stati prima versione di hello dell'insieme di credenziali hello. Recupero servizi insiemi di credenziali, che è possibile aggiungere funzionalità del modello hello Gestione risorse di Azure, sono seconda versione di hello dell'insieme di credenziali hello. Vedere hello [articolo introduttivo insieme di credenziali di servizi di ripristino](backup-azure-recovery-services-vault-overview.md) per una descrizione completa delle differenze di funzionalità hello. È più possibile creare utilizzare hello portale toocreate gli insiemi di credenziali di Backup, ma sono ancora supportati gli insiemi di credenziali di Backup.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> **15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell. <br/> **Entro il 1° novembre 2017**:
>- Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Differenze tra Backup di Azure e Azure Site Recovery
Backup di Azure e Azure Site Recovery sono correlate in quanto entrambi i servizi eseguono il backup e il ripristino dei dati, tuttavia soddisfano obiettivi diversi per la continuità aziendale e il ripristino di emergenza nell'azienda. Utilizzare tooprotect Azure Backup e ripristino dei dati a un livello più granulare. Ad esempio, se una presentazione in un computer portatile risulta danneggiata, utilizzare presentazione hello toorestore di Backup di Azure. Se si desidera tooreplicate hello configurazione e i dati in una macchina virtuale in un altro Data Center, è possibile usare Azure Site Recovery.

Backup di Azure protegge i dati in locale e nel cloud hello. Azure Site Recovery coordina la replica, il failover e il failback di macchine virtuali e server fisici. Entrambi i servizi sono importanti perché la soluzione di ripristino di emergenza deve tookeep i dati ripristinabili e protetto (Backup) *e* mantenere i carichi di lavoro disponibile (il ripristino del sito) quando si verificano interruzioni.

Hello concetti seguenti consentono di prendere decisioni importanti intorno a backup e ripristino di emergenza.

| Concetto | Dettagli | Backup | Ripristino di emergenza |
| --- | --- | --- | --- |
| Obiettivo del punto di ripristino (RPO) |quantità di Hello perdita di dati accettabili in toobe eseguita è necessario un ripristino. |Le soluzioni di backup presentano un'ampia variabilità a livello di RPO accettabile. I backup delle macchine virtuali hanno in genere un RPO di un giorno, mentre i backup dei database hanno RPO fino a un minimo di 15 minuti. |Le soluzioni di ripristino di emergenza hanno RPO bassi. Hello copia di ripristino di emergenza può essere protetto da pochi secondi o di pochi minuti. |
| Obiettivo del tempo di ripristino (RTO) |Hello tempo totale impiegato toocomplete un recupero o ripristino. |A causa di hello RPO più grande, quantità hello di dati che è una soluzione di backup necessario tooprocess è in genere molto più alto, con la conseguente toolonger RTO. Ad esempio, può richiedere giorni toorestore dati dai nastri, a seconda di hello tempo nastro hello tootransport da una posizione esterna. |Soluzioni di ripristino di emergenza sono più piccoli RTO perché sono più sincronizzate con origine hello. Numero di modifiche è necessario toobe elaborati. |
| Conservazione |Quanto tempo i dati devono toobe archiviati |Per scenari che richiedono il ripristino operativo, per danneggiamento dei dati, eliminazione accidentale dei file o errori del sistema operativo, i dati di backup vengono in genere conservati per un massimo di 30 giorni.<br>Dal punto di vista della conformità, i dati potrebbe essere necessario toobe archiviati per i mesi o anche anni. In questi casi, i dati di backup sono particolarmente adatti per l'archiviazione. |Ripristino di emergenza deve solo dati di ripristino operativo, che in genere richiede alcune ore o backup tooa giorno. A causa di acquisizione di dati con granularità fine hello nelle soluzioni di ripristino di emergenza, non è consigliabile utilizzare i dati di ripristino di emergenza per la conservazione a lungo termine. |

## <a name="next-steps"></a>Passaggi successivi
Utilizzare uno dei seguenti esercitazioni per ottenere istruzioni dettagliate, per la protezione dei dati in Windows Server o protezione di una macchina virtuale (VM) hello in Azure:

* [Eseguire il backup di file e cartelle](backup-try-azure-backup-in-10-mins.md)
* [Eseguire il backup di macchine virtuali di Azure](backup-azure-vms-first-look-arm.md)

Per informazioni dettagliate sulla protezione di altri carichi di lavoro, vedere uno di questi articoli:

* [Eseguire il backup di Windows Server](backup-configure-vault.md)
* [Eseguire il backup di carichi di lavoro delle applicazioni](backup-azure-microsoft-azure-backup.md)
* [Eseguire il backup di VM IaaS di Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
