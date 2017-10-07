---
title: domande frequenti Backup aaaAzure | Documenti Microsoft
description: "Risposte alle domande toocommon sul: funzionalità di Backup di Azure tra servizi di ripristino gli insiemi di credenziali, ciò che è possibile eseguire il backup, come funziona, crittografia e limiti. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup e ripristino di emergenza; servizio Backup
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Domande su hello servizio Azure Backup
In questo articolo ha risposte toocommon domande toohelp comprendere rapidamente i componenti di hello Azure Backup. In alcune delle risposte hello, sono disponibili articoli toohello collegamenti con informazioni complete. È possibile porre domande su Azure Backup, fare clic su **commenti** (toohello a destra). I commenti vengono visualizzati nella parte inferiore di hello di questo articolo. Un account Livefyre è toocomment obbligatorio. È anche possibile pubblicare domande sul servizio Azure Backup hello in hello [forum di discussione](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly analisi hello sezioni di questo articolo, utilizzare destra toohello collegamenti hello in **In questo articolo**.


## <a name="recovery-services-vault"></a>Insieme di credenziali dei servizi di ripristino

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>C'è alcun limite sul numero di hello degli insiemi di credenziali che possono essere creati in ogni sottoscrizione di Azure? <br/>
Sì. A partire da settembre 2016 è possibile creare 25 insiemi di credenziali di backup o dei servizi di ripristino per ogni sottoscrizione. È possibile creare i servizi di ripristino too25 insiemi di credenziali, per ogni area non supportata di Backup di Azure, per ogni sottoscrizione. Se sono necessari più insiemi di credenziali, creare una sottoscrizione aggiuntiva.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Sono previsti limiti al numero di hello del server o computer che possono essere registrati in ogni insieme di credenziali? <br/>
Sì, è possibile registrare fino a too50 macchine per ogni insieme di credenziali. Per le macchine virtuali IaaS di Azure, hello limite è di 200 macchine virtuali per ogni insieme di credenziali. Se è necessario tooregister altre macchine, creare un altro insieme di credenziali.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Se l'organizzazione ha un insieme di credenziali, come è possibile isolare i dati di un server da un altro server durante il ripristino dei dati?<br/>
Tutti i server che sono registrato toohello stesso insieme di credenziali è possibile ripristinare dati di backup da altri server di hello *che utilizzano hello stessa passphrase*. Se sono presenti server i cui dati di backup si desidera tooisolate da altri server nell'organizzazione, utilizzare una passphrase designata per tali server. Ad esempio, per i server del reparto risorse umane può essere usata una passphrase, per quelli dell'ufficio contabilità un'altra e per quelli di archiviazione un'altra ancora.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>È possibile eseguire la migrazione dei dati o dell'insieme di credenziali per il backup tra sottoscrizioni? <br/>
No. insieme di credenziali Hello viene creato a livello di sottoscrizione e non può essere riassegnata tooanother sottoscrizione dopo averla creata.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Gli insiemi di credenziali di Servizi di ripristino sono basati su Resource Manager. Gli insiemi di credenziali di Backup (modalità classica) sono ancora supportati? <br/>
Tutti gli archivi di Backup esistenti in hello [portale classico](https://manage.windowsazure.com) continuare toobe supportato. Tuttavia, è non possibile utilizzare non è più insiemi di credenziali hello toodeploy portale classico nuovi Backup. Si consiglia di utilizzare gli insiemi di credenziali di servizi di ripristino per tutte le distribuzioni perché miglioramenti futuri applicano tooRecovery servizi insiemi di credenziali, solo. Se si tenta un insieme di credenziali di Backup nel portale classico hello toocreate, sarà reindirizzato toohello [portale di Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>È possibile eseguire la migrazione un archivio di servizi di ripristino di Backup dell'insieme di credenziali tooa? <br/>
Sfortunatamente no, non è possibile migrare hello contenuto di un tooa insieme di credenziali di Backup che dell'insieme di credenziali di servizi di ripristino. Questa funzionalità verrà presto aggiunta, ma non è attualmente disponibile.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>È stato eseguito il backup di VM della versione classica in un insieme di credenziali di backup. È possibile eseguire la migrazione di macchine virtuali dalla modalità di gestione in modalità classica tooResource e la protezione in un insieme di credenziali di servizi di ripristino?
Classico i punti di ripristino di macchine Virtuali in un insieme di credenziali di backup non vengono migrati insieme di credenziali di servizi di ripristino tooa automaticamente quando si sposta hello VM da tooResource classico in modalità di gestione. Seguire questi passaggi tootransfer i backup VM:

1. Nell'insieme di credenziali Backup hello passare toohello **elementi protetti** e selezionare hello macchina virtuale. Fare clic su [Arresta protezione](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Lasciare *deselezionata* l'opzione **Elimina i dati di backup associati**.
2. Eliminare l'estensione di snapshot di backup/hello dalla hello macchina virtuale.
3. Eseguire la migrazione di macchine virtuali hello dalla modalità di gestione tooResource modalità classica. Verificare che le informazioni di archiviazione e rete hello macchina virtuale toohello corrispondente viene anche eseguita la migrazione tooResource modalità di gestione.
4. Creare un insieme di credenziali di servizi di ripristino e configurare i backup su hello migrazione macchina virtuale utilizzando **Backup** azione nella parte superiore del dashboard dell'insieme di credenziali. Per informazioni dettagliate sul backup dei servizi di ripristino tooa macchina virtuale insieme di credenziali, vedere l'articolo di hello, [proteggere macchine virtuali di Azure con un insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agente di Backup di Azure
Per un elenco dettagliato delle domande, vedere le [domande frequenti sul backup di file-cartelle di Azure](backup-azure-file-folder-backup-faq.md)

## <a name="azure-vm-backup"></a>Backup di macchine virtuali di Azure
Per un elenco dettagliato delle domande, vedere le [domande frequenti sul backup di macchine virtuali di Azure](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>Eseguire il backup dei server VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>È possibile eseguire il backup VMware vCenter server tooAzure?

Sì. È possibile utilizzare tooback Azure Backup Server VMware vCenter e ESXi tooAzure. Per informazioni sulla versione di VMware hello supportato, vedere l'articolo hello [una matrice di protezione di Azure Backup Server](backup-mabs-protection-matrix.md). Per istruzioni dettagliate, vedere [tooback utilizzare Azure Backup Server di un server VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Server di Backup di Azure e System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>È possibile utilizzare Azure Backup Server toocreate un backup del ripristino Bare Metal (BMR) per un server fisico? <br/>
Sì.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>È possibile registrare gli insiemi di credenziali toomultiple i Server DPM? <br/>
No. Un server DPM o MABS può essere registrato tooonly un insieme di credenziali.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Quale versione di System Center Data Protection Manager è supportata? <br/>
Si consiglia di installare hello [più recente](http://aka.ms/azurebackup_agent) Azure Backup agent sul hello aggiornamento cumulativo più recente (UR) per System Center Data Protection Manager (DPM). A partire da agosto 2016, aggiornamento cumulativo 11 è aggiornamento più recente di hello.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>È stato installato Azure Backup agent tooprotect file e cartelle. È possibile installare ora toowork System Center DPM con Azure Backup agent tooprotect locale i carichi di lavoro di applicazione/VM tooAzure? <br/>
toouse Backup di Azure con System Center Data Protection Manager (DPM), installare DPM e quindi installare l'agente di Backup di Azure. Installazione dei componenti di Azure Backup hello in questo ordine assicura l'agente Azure Backup hello funziona con DPM. L'installazione dell'agente di Backup di Azure hello prima di installare Data Protection Manager non è consigliato o supportato.


## <a name="how-azure-backup-works"></a>Funzionamento di Backup di Azure
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Se si annulla un processo di backup una volta avviata, sono hello trasferiti i dati di backup eliminati? <br/>
No. Tutti i dati trasferiti in insieme di credenziali hello, prima di processo di backup hello è stata annullata, rimangono nell'insieme di credenziali hello. Azure Usa Backup un toooccasionally meccanismo di checkpoint aggiungere dati di backup toohello checkpoint durante hello backup. Poiché sono presenti checkpoint nei dati di backup hello, processo di backup successivo hello possibile convalidare l'integrità dei file hello hello. processo di backup successivo Hello sarà dati incrementali toohello il backup in precedenza. I backup incrementali solo il trasferimento dati nuovi o modificati, che equivale toobetter utilizzo della larghezza di banda.

Se si annulla un processo di backup per una macchina virtuale di Azure, tutti i dati trasferiti vengono ignorati. processo di backup successivo Hello trasferisce i dati incrementali dal hello ultimo processo riuscito ha backup.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Esistono limiti in relazione a quando o quante volte può essere pianificato un processo di backup?<br/>
Sì. È possibile eseguire i processi di backup in Windows Server o workstation Windows Backup toothree volte al giorno. È possibile eseguire i processi di backup in System Center DPM backup tootwice al giorno. È possibile eseguire un processo di backup per le VM IaaS una volta al giorno. È possibile utilizzare criteri di pianificazione per Windows Server o toospecify workstation Windows hello pianificazioni giornaliere o settimanale. Con System Center DPM, è possibile specificare pianificazioni giornaliere, settimanali, mensili e annuali.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Perché è pari a hello hello dati trasferiti toohello che credenziali minore dati hello che sottoposti a backup di servizi di ripristino?<br/>
 Tutti i dati di hello che viene eseguito il backup di Azure Backup Agent o SCDPM o Server di Backup di Azure vengono compressi e crittografati prima di essere trasferiti. Una volta applicata la crittografia e compressione hello, dati hello nell'insieme di credenziali backup hello sono inferiore al 30-40%.

## <a name="what-can-i-back-up"></a>Backup consentiti
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Quali sistemi operativi sono supportati da Backup di Azure? <br/>
Backup di Azure supporta hello segue l'elenco dei sistemi operativi per il backup: file e cartelle e le applicazioni di carico di lavoro protette con Azure Backup Server e System Center Data Protection Manager (DPM).

| Sistema operativo | Piattaforma | SKU |
|:--- | --- |:--- |
| Windows 8 e versioni più recenti di SP |64 bit |Enterprise, Pro |
| Windows 7 e versioni più recenti di SP |64 bit |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 e versioni più recenti di SP |64 bit |Enterprise, Pro |
| Windows 10 |64 bit |Enterprise, Pro, Home |
| Windows Server 2016 |64 bit |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 e più recenti SPs |64 bit |Standard, Datacenter, Foundation |
| Windows Server 2012 e versioni più recenti di SP |64 bit |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 e versioni più recenti di SP |64 bit |Standard, Workgroup | 
| Windows Storage Server 2012 R2 e versioni più recenti di SP |64 bit |Standard, Workgroup |
| Windows Storage Server 2012 e versioni più recenti di SP |64 bit |Standard, Workgroup |
| Windows Server 2012 R2 e più recenti SPs |64 bit |Essential |
| Windows Server 2008 R2 SP1, |64 bit |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bit |Standard, Enterprise, Datacenter, Foundation |

**Per il backup di VM di Azure**

* **Linux**: Backup di Azure supporta [un elenco di distribuzioni approvate da Azure](../virtual-machines/linux/endorsed-distros.md) , ad eccezione di CoreOS Linux.  Altri Bring-Your-proprietari-distribuzioni di Linux potrebbe essere inoltre funzionare, purché sia disponibile nella macchina virtuale hello agente VM hello e il supporto per Python esiste.
* **Windows Server**: le versioni precedenti a Windows Server 2008 R2 non sono supportate.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>È previsto un limite alle dimensioni di hello di ogni origine dati viene eseguito il backup? <br/>
Non sussiste alcun limite hello quantità di dati che è possibile eseguire il backup dell'insieme di credenziali tooa. Backup di Azure Limita dimensioni massime di hello per l'origine dati hello, tuttavia, questi limiti sono di grandi dimensioni. A partire da agosto 2015, dimensione massima di hello per un'origine dati per i sistemi operativi supportato hello è:

| Numero S. | Sistema operativo | Dimensione massima origine dati |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 o versioni successive |54400 GB |
| 2 |Windows 8 o versione successiva |54400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Hello nella tabella seguente illustra la modalità di determinazione di ciascuna dimensione dell'origine dati.

| Origine dati | Dettagli |
|:---:|:--- |
| Volume |quantità di Hello di dati da sottoporre a backup singolo volume di un computer client o server |
| Macchina virtuale Hyper-V |Somma dei dati di tutti i dischi rigidi virtuali hello della macchina virtuale hello viene eseguito il backup |
| Database di Microsoft SQL Server |Dimensioni di un singolo database SQL di cui viene eseguito il backup |
| Microsoft SharePoint |Somma dei database di configurazione e il contenuto di hello all'interno di una farm di SharePoint viene eseguito il backup |
| Microsoft Exchange |Somma di tutti i database di Exchange in un server di Exchange di cui viene eseguito il backup |
| Stato del sistema/ripristino bare metal |Ogni copia del ripristino bare metal o stato del sistema del computer hello viene eseguito il backup |

Per il backup di macchina virtuale di Azure, ogni macchina virtuale può disporre dei dischi dati too16 con ogni disco di dati di dimensioni 1023GB o meno. 

## <a name="retention-policy-and-recovery-points"></a>Criteri di conservazione e punti di ripristino
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Esiste una differenza tra i criteri di conservazione hello per Data Protection Manager e Windows Server/client (ovvero, in Windows Server senza Data Protection Manager)?<br/>
No, sia DPM che Windows Server/client prevedono criteri di conservazione giornalieri, settimanali, mensili e annuali.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>È possibile configurare i criteri di conservazione in modo selettivo, ad esempio con frequenza settimanale e giornaliera, ma non annuale e mensile?<br/>
Sì, hello struttura di conservazione dei Backup di Azure consente toohave flessibilità completa nella definizione di criteri di conservazione hello in base alle esigenze.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>È possibile "pianificare un backup" alle 18.00 e specificare criteri di conservazione con un orario diverso?<br/>
No. I criteri di conservazione possono essere applicati solo ai punti di backup. Nella seguente immagine di hello, criteri di conservazione hello viene specificato per i backup eseguiti in 12 am e pm 6. <br/>

![Pianificare backup e conservazione](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Se una copia di backup verrà conservato per un lungo periodo di tempo, è necessario più tempo toorecover un punto dati meno recente? <br/>
No-tempo hello toorecover hello meno recente o hello punto più recente è hello stesso. Ogni punto di ripristino si comporta come un punto completo.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Se ogni punto di ripristino come un punto completo, ha un impatto sul spazio di archiviazione backup totale fatturabile hello?<br/>
I punti di conservazione tipici a lungo termine archiviano i dati di backup come punti completi. punti completo Hello sono archiviazione *inefficiente* ma sono più semplici e toorestore più veloce. Le copie incrementali sono archiviazione *efficiente* ma è necessario toorestore una catena di dati, che hanno effetto i tempi di ripristino. Azure offre della architettura archiviazione di Backup hello meglio in modo ottimale l'archiviazione dei dati per i ripristini veloci e costi di archiviazione insufficiente. Questo approccio all'archiviazione dati assicura che la larghezza di banda in ingresso e in uscita venga usata in modo efficiente. Entrambi hello tempo in cui dati di archiviazione e hello toorecover hello dati richiesti, viene mantenuta tooa minimo. Sono disponibili altre informazioni sull'efficienza dei [backup incrementali](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/).

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>È previsto un limite sul numero di hello dei punti di ripristino che è possibile creare?<br/>
È possibile creare i punti di ripristino too9999 per ogni istanza protetta. Un'istanza protetta è un computer, un server (fisico o virtuale) o un carico di lavoro configurato tooback backup tooAzure dati. Per ulteriori informazioni, vedere le spiegazioni hello [Backup e conservazione](./backup-introduction-to-azure-backup.md#backup-and-retention), e [che cos'è un'istanza protetta](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Come molte attività di ripristino è possibile eseguire sui dati hello che viene eseguito il backup tooAzure?<br/>
Non è previsto alcun limite per il numero di hello di ripristini da Backup di Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Durante il ripristino dei dati, posso pagare per il traffico in uscita hello da Azure? <br/>
No. Sono disponibili i ripristini e non vengono addebitate le spese per il traffico in uscita hello.

## <a name="azure-backup-encryption"></a>Crittografia in Backup di Azure
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Dati hello inviati tooAzure crittografati <br/>
Sì. Dati vengono crittografati nel computer client/server/SCDPM di hello locale utilizzando AES256 e hello dati vengono inviati tramite una connessione HTTPS protetta.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Sia i dati di backup hello in Azure in forma crittografata?<br/>
Sì. inviare i dati di Hello tooAzure rimangano crittografati (a riposo). Microsoft non implica la decrittografia dei dati di backup hello in qualsiasi momento. Per eseguire il backup di una macchina virtuale di Azure, Backup di Azure si basa sulla crittografia della macchina virtuale hello. Ad esempio, se la macchina virtuale viene crittografata con crittografia del disco di Azure, o di altre tecnologie di crittografia, Azure Backup utilizza tale toosecure crittografia dei dati.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Qual è hello lunghezza minima della chiave di crittografia utilizzato tooencrypt dati di backup? <br/>
chiave di crittografia Hello deve essere lunga almeno 16 caratteri quando si usa l'agente Azure backup. Per macchine virtuali di Azure, non è disponibile alcun toolength limite delle chiavi utilizzate dal KeyVault di Azure. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Cosa succede se sono disponibili la chiave di crittografia hello? È possibile ripristinare dati hello (o) Microsoft possono ripristinare i dati di hello? <br/>
dati di backup hello Hello tooencrypt utilizzati chiave sono presenti solo in locale di cliente hello. Microsoft non mantiene una copia in Azure e non dispone di qualsiasi chiave toohello di accesso. Se il cliente hello misplaces chiave hello, Microsoft non è possibile ripristinare i dati di backup hello.
