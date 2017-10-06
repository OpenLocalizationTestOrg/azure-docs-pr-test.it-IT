---
title: aaaReplicate le macchine virtuali VMware e server fisici tooAzure (classico legacy) | Documenti Microsoft
description: Viene descritto come tooreplicate locale macchine virtuali e tooAzure di server fisici Windows/Linux usando Azure Site Recovery in una distribuzione nel portale classico hello legacy.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Replicare le macchine virtuali VMware e server fisici tooAzure con Azure Site Recovery usando il portale classico di hello (legacy)
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmware-to-azure.md)
> * [Portale classico](site-recovery-vmware-to-azure-classic.md)
> * [Portale classico (legacy)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Benvenuti tooAzure Site Recovery. Questo articolo descrive una distribuzione legacy per replicare le macchine virtuali VMware in locale o tooAzure di server fisici Windows/Linux usando Azure Site Recovery nel portale classico hello.

## <a name="overview"></a>Panoramica
Le organizzazioni devono una strategia di BCDR che determina come le app, i carichi di lavoro e i dati rimangono in esecuzione e disponibili durante i tempi di inattività pianificati ed e ripristino le condizioni di lavoro toonormal appena possibile. La strategia di continuità aziendale e ripristino di emergenza deve garantire la sicurezza dei dati aziendali e la possibilità di recuperarli, oltre alla disponibilità costante dei carichi di lavoro in caso di emergenza.

Il ripristino del sito è un servizio di Azure che contribuisce strategia BCDR tooyour dall'orchestrazione replica dei server fisici locali e macchine virtuali toohello cloud (Azure) o Data Center secondario tooa. Quando si verificano interruzioni nella propria posizione primaria, è possibile failover toohello posizione secondaria tookeep App e carichi di lavoro disponibili. Non si posizione primaria tooyour indietro quando vengono restituite le operazioni di toonormal. Per altre informazioni, vedere [Che cos'è Site Recovery?](site-recovery-overview.md)

> [!WARNING]
> Questo articolo contiene **istruzioni legacy**. Non usare queste informazioni per nuove distribuzioni. In alternativa, [seguire queste istruzioni](site-recovery-vmware-to-azure.md) toodeploy Site Recovery nel portale di Azure hello o [utilizzare queste istruzioni](site-recovery-vmware-to-azure-classic.md) tooconfigure hello avanzata di distribuzione nel portale classico hello. Se già stato distribuito utilizzando il metodo hello descritto in questo articolo, è consigliabile eseguire la migrazione toohello avanzata di distribuzione nel portale classico hello.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>La migrazione della distribuzione toohello avanzata
In questa sezione è applicabile solo se è già stato distribuito il ripristino del sito utilizzando istruzioni hello in questo articolo.

toomigrate la distribuzione esistente, è necessario:

1. Distribuire nuovi componenti di Site Recovery nel sito locale.
2. Configurare le credenziali per l'individuazione automatica delle macchine virtuali VMware nel server di configurazione hello.
3. Individuare i server VMware hello con server di configurazione hello.
4. Creare un nuovo gruppo protezione dati con server di configurazione hello.

Prima di iniziare:

* È consigliabile impostare una finestra di manutenzione per la migrazione.
* Hello **eseguire la migrazione di macchine** opzione è disponibile solo se si dispone di gruppi protezione dati esistenti che sono stati creati durante una distribuzione legacy.
* Dopo aver completato i passaggi della migrazione hello può richiedere 15 minuti o più credenziali di hello toorefresh e toodiscover e aggiorna le macchine virtuali in modo che è possibile aggiungerli tooa gruppo di protezione dati. È possibile aggiornare manualmente anziché attendere.

Eseguire la migrazione nel modo seguente:

1. Conoscenza [avanzata di distribuzione nel portale classico hello](site-recovery-vmware-to-azure-classic.md). Hello revisione avanzata [architettura](site-recovery-vmware-to-azure-classic.md), e [prerequisiti](site-recovery-vmware-to-azure-classic.md).
2. Disinstallare il servizio di mobilità hello dai computer che si sta attualmente la replica. Una nuova versione del servizio hello verrà installata nei computer hello quando vengono aggiunte toohello nuovo gruppo protezione dati.
3. Scaricare un [chiave di registrazione dell'insieme di credenziali](site-recovery-vmware-to-azure-classic.md) e [guidata di installazione unificata hello](site-recovery-vmware-to-azure-classic.md) tooinstall hello configurazione server, server di elaborazione e master componenti server di destinazione. Altre informazioni sulla [pianificazione della capacità](site-recovery-vmware-to-azure-classic.md).
4. [Impostare credenziali](site-recovery-vmware-to-azure-classic.md) che il ripristino del sito è possibile utilizzare tooaccess VMware server tooautomatically individuare le macchine virtuali VMware. Vedere la sezione relativa alle [autorizzazioni necessarie](site-recovery-vmware-to-azure-classic.md).
5. Aggiungere [server vCenter o host vSphere](site-recovery-vmware-to-azure-classic.md). Può richiedere 15 minuti per ulteriori informazioni per i server tooappear nel portale di Site Recovery hello.
6. Creare un [nuovo gruppo protezione dati](site-recovery-vmware-to-azure-classic.md). Potrebbe essere necessaria fino too15 minuti per toorefresh portale hello in modo che le macchine virtuali hello vengono individuate e visualizzati. Se non si desidera toowait è possibile evidenziare un nome di server di gestione di hello (selezionarla) > **aggiornamento**.
7. Scegliere Nuovo gruppo protezione dati di hello **eseguire la migrazione di macchine**.

    ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. In **Seleziona macchine** il gruppo protezione dati selezionare hello toomigrate da desiderato e hello macchine da toomigrate.

    ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. In **configurare le impostazioni di destinazione** specificare se si desidera toouse hello stesse impostazioni per tutte le macchine e i server di elaborazione selezionare hello e account di archiviazione di Azure. Se non si dispone di un server di elaborazione separato in questo sarà l'indirizzo IP di hello hello hello server del server di configurazione.

    ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migrazione di account di archiviazione](../resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per gli account di archiviazione utilizzati per la distribuzione di Site Recovery.

1. In **specificare account**, selezionare account hello creato per hello processo server tooaccess hello macchina toopush hello nuova versione del servizio di mobilità hello.

   ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Il ripristino del sito verrà eseguita la migrazione di account di archiviazione Azure i dati replicati toohello fornito dall'utente. Facoltativamente è possibile riutilizzare l'account di archiviazione hello utilizzati nella distribuzione legacy hello.
3. Dopo il processo di hello verranno sincronizzati automaticamente le macchine virtuali al termine. Al termine della sincronizzazione è possibile eliminare le macchine virtuali hello dal gruppo protezione dati legacy hello.
4. Dopo aver eseguito la migrazione di tutti i computer è possibile eliminare il gruppo di protezione legacy hello.
5. Tenere presente le proprietà di toospecify hello failover delle macchine e hello le impostazioni di rete di Azure al termine della sincronizzazione.
6. Se si dispone di piani di ripristino esistenti, è possibile eseguirne la migrazione distribuzione toohello avanzata con hello **eseguire la migrazione del piano di ripristino** opzione. Questa operazione deve essere eseguita solo dopo la migrazione di tutti i computer protetti.

   ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Dopo aver completato la migrazione continua con hello [articolo migliorata](site-recovery-vmware-to-azure-classic.md). rest Hello di questo articolo legacy non sarà più possibile rilevanti e non devi toofollow qualsiasi più passaggi hello descritti in it * *.
>
>

## <a name="what-do-i-need"></a>Che cosa occorre?
Questo diagramma mostra i componenti di distribuzione hello.

![Nuovo insieme di credenziali](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

Sono necessari gli elementi seguenti:

| **Componente** | **Distribuzione** | **Dettagli** |
| --- | --- | --- |
| **Server di configurazione** |Standard A3 macchina virtuale di Azure in hello stessa sottoscrizione di Site Recovery. |il server di configurazione di Hello coordina le comunicazioni tra macchine virtuali protette, il server di elaborazione hello e server di destinazione master in Azure. Configura la replica e coordina il ripristino in Azure quando si verifica il failover. |
| **Server master di destinazione** |Una macchina virtuale di Azure, ovvero un server di Windows in base a un'immagine della raccolta Windows Server 2012 R2 (macchine Windows tooprotect) o come un server Linux dipende da un'immagine della raccolta OpenLogic CentOS 6.6 (macchine Linux tooprotect).<br/><br/> Per le dimensioni sono disponibili tre opzioni: A4 Standard, D14 Standard e DS4 Standard.<br/><br/> server Hello è connesso toohello stessa rete del server di configurazione hello Azure.<br/><br/> Impostare nel portale di Site Recovery hello |Riceve e mantiene i dati replicati dai computer protetti tramite VHD collegati creati nell'archiviazione BLOB dell'account di archiviazione di Azure.<br/><br/> Selezionare DS4 Standard in modo specifico per la configurazione della protezione per carichi di lavoro che richiedono prestazioni elevate omogenee e a bassa latenza con l'account di archiviazione Premium. |
| **Server di elaborazione** |Un server virtuale o fisico locale che esegue Windows Server 2012 R2.<br/><br/> È consigliabile è posizionata su hello stessa rete e segmento LAN hello per le macchine che si desidera tooprotect, ma può essere eseguita su una rete diversa purché dispongano di macchine virtuali protette L3 tooit visibilità di rete.<br/><br/> È possibile configurare e registrarlo toohello server di configurazione nel portale di Site Recovery hello. |Macchine virtuali protette inviano server di elaborazione locale toohello replica dei dati. Contiene dati di replica di toocache una cache basata su disco che riceve. Esegue una serie di azioni su tali dati.<br/><br/> Ottimizza i dati per la memorizzazione nella cache, la compressione e crittografia prima dell'invio nel server di destinazione master toohello.<br/><br/> Gestisce l'installazione push del servizio di mobilità hello.<br/><br/> Esegue l'individuazione automatica delle macchine virtuali VMware. |
| **Computer locali** |Macchine virtuali VMware locali oppure server fisici che eseguono Windows o Linux. |Vengono configurate le impostazioni di replica applicabili a uno o più computer. È possibile eseguire il failover di un singolo computer o, più comunemente, di più computer raccolti in un piano di ripristino. |
| **Servizio Mobility** |Installato in ogni macchina virtuale o un server fisico desiderato tooprotect<br/><br/> Può essere installato manualmente o inserito e installato automaticamente dal server di elaborazione hello quando si abilita la replica per un computer. |servizio di mobilità Hello invia i server di elaborazione dati toohello durante la replica iniziale (risincronizzazione). Dopo aver hello macchina si trova in uno stato protetto (al termine della risincronizzazione) hello servizio di mobilità acquisisce toodisk scritture in memoria e li invia a server di elaborazione toohello. La coerenza delle applicazioni per i server Windows si ottiene tramite VSS. |
| **Insieme di credenziali di Azure Site Recovery** |Creare un insieme di credenziali di Site Recovery con una sottoscrizione di Azure e registrare i server nell'insieme di credenziali hello. |insieme di credenziali Hello coordina e gestisce la replica dei dati, il failover e ripristino tra il sito locale e Azure. |
| **Meccanismo di replica** |**Tramite Internet hello**: comunica e vengono replicati i dati da tooAzure server locale protetto utilizzando un canale protetto SSL/TLS su hello internet. Questo è l'opzione predefinita di hello.<br/><br/> **VPN/ExpressRoute**: comunica e replica i dati tra i server locali e Azure tramite una connessione VPN. È necessario tooset una VPN da sito a sito o una connessione ExpressRoute tra il sito locale e la rete di Azure.<br/><br/> È possibile selezionare la modalità tooreplicate durante la distribuzione di Site Recovery. È possibile modificare il meccanismo di hello dopo la configurazione senza conseguenze per la replica delle macchine virtuali esistenti. |Nessuna delle due opzioni richiede si tooopen le porte di rete in ingresso nei computer protetti. Tutte le comunicazioni di rete viene avviata da sito locale hello. |

## <a name="capacity-planning"></a>Pianificazione della capacità
aree principali Hello tooconsider, occorre:

* **Ambiente di origine**: hello infrastruttura VMware, le impostazioni del computer di origine e requisiti.
* **Server del componente**: hello server di elaborazione, il server di configurazione e il server di destinazione master

### <a name="considerations-for-hello-source-environment"></a>Considerazioni per l'ambiente di origine hello
* **Dimensione massima del disco**: dimensioni massime correnti hello del disco hello che può essere una macchina virtuale tooa associata sono di 1 TB. Dimensioni massime di hello di un disco di origine che può essere replicato anche sono pertanto limitato too1 TB.
* **Dimensione massima per ogni origine**: dimensioni massime di hello un singolo computer di origine sono 31 TB (con i 31 dischi) e con un'istanza di D14 effettuato il provisioning per il server di destinazione master hello.
* **Numero di origini per ogni server di destinazione master** - È possibile proteggere più computer di origine con un singolo server di destinazione master. Tuttavia, un computer di origine singolo può essere protetto tra più server di destinazione master, perché come dischi di replicano, un disco rigido virtuale che rispecchia le dimensioni di hello del disco hello viene creato nell'archiviazione blob di Azure e collegato come un server di destinazione master toohello disco dati.  
* **Frequenza di modifica giornaliera massima per ogni origine**, sono disponibili tre fattori considerati quando si considera hello consigliato toobe modificare frequenza per ogni origine. Per motivi di destinazione in base hello sono necessari due IOPS su disco di destinazione hello per ogni operazione nell'origine hello. Questo avviene perché una lettura di dati precedente e la scrittura di nuovi dati hello avverrà sul disco di destinazione hello.
  * **Ogni giorno modificare velocità supportata dal server di elaborazione hello**: un computer di origine non può estendersi su più server di elaborazione. Un server singolo processo può supportare fino too1 TB del tasso di modifica giornaliero. 1 TB, pertanto è supportata per una macchina di origine di frequenza di modifica di hello massima giornaliera dei dati.
  * **Velocità effettiva massima supportata dal disco di destinazione hello**, varianza del valore massimo per il disco di origine non può essere più di 144 GB/giorno (con dimensioni di 8 KB scrittura). Vedere la tabella hello nella sezione di destinazione master hello di velocità effettiva di hello e IOPs della destinazione hello per varie dimensioni di scrittura. Questo numero deve essere divisi per due perché ogni origine IOP genera 2 IOPS su disco di destinazione hello. Conoscenza [Azure obiettivi di scalabilità e prestazioni](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) durante la configurazione di destinazione hello per gli account di archiviazione premium.
  * **Velocità effettiva massima supportata dall'account di archiviazione hello**, un'origine non può estendersi a più account di archiviazione. Dato che un account di archiviazione che utilizza un massimo di 20.000 richieste al secondo e che ogni origine IOP genera 2 IOPS server di destinazione master hello, è consigliabile che mantenere numero hello di operazioni IOPS tra hello origine too10, 000. Conoscenza [Azure obiettivi di scalabilità e prestazioni](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) quando si configura hello origine per gli account di archiviazione premium.

### <a name="considerations-for-component-servers"></a>Considerazioni relative ai server dei componenti
Tabella 1 sono riepilogate le dimensioni delle macchine virtuali hello per la configurazione di hello e i server di destinazione master.

| **Componente** | **Istanze di Azure distribuite** | **Core** | **Memoria** | **Numero massimo di dischi** | **Dimensioni disco** |
| --- | --- | --- | --- | --- | --- |
| Server di configurazione |A3 standard |4 |7 GB |8 |1023 GB |
| Server master di destinazione |A4 standard |8 |14 GB |16 |1023 GB |
| D14 standard |16 |112 GB |32 |1023 GB | |
| DS4 standard |8 |28 GB |16 |1023 GB | |

**Tabella 1**

#### <a name="process-server-considerations"></a>Considerazioni sui server di elaborazione
In genere dimensionamento del processo server dipende dalle modifiche giornaliere hello in tutti i carichi di lavoro protetti.

* È necessario sufficiente attività tooperform di calcolo, ad esempio inline compressione e crittografia.
* server di elaborazione Hello utilizza la cache basata su disco. Verificare che hello consigliato spazio nella cache e velocità effettiva del disco è disponibile toofacilitate le modifiche dei dati hello archiviate nell'evento hello del collo di bottiglia di rete o di interruzione.
* Assicurarsi di larghezza di banda sufficiente affinché hello server di elaborazione possono caricare hello toohello destinazione master server tooprovide dati continua la protezione dei dati.

Tabella 2 fornisce un riepilogo delle linee guida di hello processo server.

| **Frequenza di modifica dei dati** | **CPU** | **Memoria** | **Dimensione disco cache** | **Velocità effettiva disco cache** | **Ingresso/uscita larghezza di banda** |
| --- | --- | --- | --- | --- | --- |
| Meno di 300 GB |4 vCPU (2 socket * 2 core a 2,5 GHz) |4 GB |600 GB |too10 7 MB al secondo |30 Mbps/21 Mbps |
| too600 300 GB |8 vCPU (2 socket * 4 core a 2,5 GHz) |6 GB |600 GB |too15 11 MB al secondo |60 Mbps/42 Mbps |
| 600 GB too1 TB |12 vCPU (2 socket * 6 core a 2,5 GHz) |8 GB |600 GB |too20 16 MB al secondo |100 Mbps/70 Mbps |
| Più di 1 TB |Distribuire un altro server di elaborazione | | | | |

**Tabella 2**

Dove:

* In ingresso è la larghezza di banda di download (intranet tra il server di origine e di processo hello).
* In uscita è il caricamento della larghezza di banda (internet tra server di elaborazione hello e server di destinazione master). I valori relativi all'uscita presuppongono una compressione media del server di elaborazione del 30%.
* Per il disco cache è consigliabile un disco separato dal sistema operativo di almeno 128 GB per tutti i server di elaborazione.
* Per hello velocità effettiva di cache su disco dopo l'archiviazione è stato utilizzato per quelle di benchmarking: 8 unità SAS di 10 RPM con una configurazione RAID 10.

#### <a name="configuration-server-considerations"></a>Considerazioni relative ai server di configurazione
Ogni server di configurazione può supportare fino a too100 macchine di origine con volumi di 3 e 4. Se la distribuzione ha dimensioni maggiori, è consigliabile distribuire un altro server di configurazione. Vedere la tabella 1 per le proprietà di macchina virtuale predefinite hello hello del server di configurazione.

#### <a name="master-target-server-and-storage-account-considerations"></a>Considerazioni relative al server di destinazione master e all'account di archiviazione
archiviazione Hello per ogni server di destinazione master include un disco del sistema operativo, un volume di conservazione e dischi dati. unità di conservazione Hello gestisce journal hello delle modifiche su disco per la durata di hello del periodo di memorizzazione hello definito nel portale di Site Recovery hello.  Fare riferimento tooTable 1 per la proprietà della macchina virtuale hello del server di destinazione master hello. Tabella 3 viene illustrato l'utilizzano dischi hello a4.

| **Istanza** | **Disco del sistema operativo** | **Conservazione** | **Dischi dati** |
| --- | --- | --- | --- |
| **Conservazione** |**Dischi dati** | | |
| A4 standard |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |15 dischi (15 * 1023 GB) |
| D14 standard |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |31 dischi (15 * 1023 GB) |
| DS4 standard |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |15 dischi (15 * 1023 GB) |

**Tabella 3**

Dipende dalla pianificazione della capacità per il server di destinazione master hello:

* Limitazioni e prestazioni dell'archiviazione di Azure
  * numero massimo di Hello di elevata utilizzati dischi per una macchina virtuale di livello Standard, è di circa 40 (IOPS 20.000/500 per disco) in un singolo account di archiviazione. Informazioni sugli [obiettivi di scalabilità per account di archiviazione Standard](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) e [account di archiviazione Premium](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Frequenza di modifica giornaliera
* Archiviazione del volume di conservazione.

Si noti che:

* Un'origine non può estendersi su più account di archiviazione. Si applica disco dati toohello che gli account di archiviazione toohello selezionati quando si configura la protezione. i dischi di memorizzazione del sistema operativo e hello Hello andare in genere toohello distribuiti automaticamente l'account di archiviazione.
* volume di archiviazione di conservazione Hello necessarie dipende dalle modifiche giornaliere hello e numero di giorni di conservazione di hello. archiviazione di conservazione obbligatorio per ogni server di destinazione master Hello = varianza totale dall'origine al giorno * numero di giorni di conservazione.
* Ogni server di destinazione master ha un solo volume di conservazione. volume di conservazione Hello viene condivisa tra server di destinazione master toohello collegati dischi hello. ad esempio:
  * Se è presente una macchina di origine con 5 dischi e ogni disco genera 120 IOPS (dimensioni di 8 KB) nell'origine hello, questo si traduce too240 di IOPS per disco (2 operazioni su disco di destinazione hello per ogni origine dei / o). 240 IOPS è all'interno di hello Azure limite di IOPS disco pari a 500.
  * Nel volume di conservazione hello, questa diventa 120 * 5 = 600 IOPS e ciò può diventare un collo di bottiglia. In questo scenario, una buona strategia potrebbe essere tooadd volume di conservazione di più dischi toohello e span quest'ultimo, come una configurazione di striping RAID. Ciò migliorerà le prestazioni IOPS hello vengono distribuiti in più unità. numero di Hello di unità toobe aggiunto toohello volume di conservazione sarà come segue:
    * IOPS totali dall'ambiente di origine / 500
    * Varianza totale al giorno dall'ambiente di origine (senza compressione) / 287 GB. 287 GB è la velocità effettiva massima hello è supportata da un disco di destinazione al giorno. Questa metrica variano in base alle dimensioni di scrittura hello con un fattore pari a 8 KB, perché in questo caso è 8 KB tre si presuppone che le dimensioni di scrittura. Se, ad esempio, dimensione scrittura hello è 4 KB, velocità effettiva sarà 287/2. E se la dimensione di scrittura hello è 16 KB, velocità effettiva sarà 287 * 2.
* numero di account di archiviazione richiesto Hello = origine totale IOPs/10000.

## <a name="before-you-start"></a>Prima di iniziare
| **Componente** | **Requisiti** | **Dettagli** |
| --- | --- | --- |
| **Account di Azure** |È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). | |
| **Archiviazione di Azure** |È necessario un toostore replicati dati dell'account di archiviazione di Azure<br/><br/> Deve essere uno di questi account hello un [Account di archiviazione con ridondanza geografica Standard](../storage/common/storage-redundancy.md#geo-redundant-storage) o [Account di archiviazione Premium](../storage/common/storage-premium-storage.md).<br/><br/> È necessario in hello stessa area hello servizio Azure Site Recovery e associato hello stessa sottoscrizione. Non è supportata spostamento hello di account di archiviazione creati utilizzando hello [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse.<br/><br/> leggere più toolearn [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md) | |
| **Rete virtuale di Azure** |È necessario che una rete virtuale di Azure in cui hello verrà distribuiti il server di configurazione e il server di destinazione master. Dovrebbe essere hello stessa sottoscrizione e area geografica dell'insieme di credenziali di Azure Site Recovery hello. Se si desiderano tooreplicate dati su un hello connessione Azure ExpressRoute o VPN virtuale rete deve essere rete locale tooyour connesso tramite una connessione ExpressRoute o una VPN Site-to-Site. | |
| **Risorse di Azure** |Assicurarsi di avere sufficiente toodeploy risorse di Azure tutti i componenti. Per altre informazioni, vedere [Limiti relativi alle sottoscrizioni di Azure](../azure-subscription-service-limits.md). | |
| **Macchine virtuali di Azure** |Macchine virtuali da tooprotect devono essere conformi ai [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Numero di dischi**: in un singolo server protetto è possibile supportare un massimo di 31 dischi.<br/><br/> **Dimensioni del disco**: la capacità dei singoli dischi non deve superare 1023 GB.<br/><br/> **Clustering**: i server di cluster non sono supportati.<br/><br/> **Avvio**: l'avvio UEFI (Unified Extensible Firmware Interface)/EFI (Extensible Firmware Interface) non è supportato.<br/><br/> **Volumi**: i volumi crittografati con Bitlocker non sono supportati.<br/><br/> **Nomi dei server**: i nomi devono contenere da 1 a 63 caratteri (lettere, numeri e trattini). nome Hello deve iniziare con una lettera o un numero e terminare con una lettera o un numero. Una volta un computer protetto è possibile modificare hello nomi di Azure. | |
| **Server di configurazione** |Verrà creato nella sottoscrizione per il server di configurazione di hello standard delle macchine virtuali A3 basati su un'immagine della raccolta di Azure Site Recovery Windows Server 2012 R2. Viene creata come hello prima istanza in un nuovo servizio cloud. Se si seleziona la rete Internet pubblica come tipo di connettività hello per il servizio cloud hello di hello configurazione server verrà creato con un indirizzo IP pubblico riservato.<br/><br/> il percorso di installazione di Hello deve essere solo caratteri inglesi. | |
| **Server master di destinazione** |Macchina virtuale di Azure, A4 Standard, D14 Standard o DS4 Standard.<br/><br/> il percorso di installazione di Hello deve essere solo caratteri inglesi. Ad esempio in cui deve essere il percorso di hello **/usr/local/ASR** per un server di destinazione master Linux. | |
| **Server di elaborazione** |È possibile distribuire server di elaborazione hello in computer fisico o macchina virtuale che esegue Windows Server 2012 R2 con aggiornamenti più recenti di hello. Eseguire l'installazione in C:/.<br/><br/> Si consiglia di posizionare i server hello in hello stessa rete e subnet hello macchine da tooprotect.<br/><br/> Installare VMware vSphere CLI 5.5.0 nel server di elaborazione hello. componente di Hello VMware vSphere CLI è necessario nel server di elaborazione hello in ordine toodiscover le macchine virtuali gestite da un server vCenter o macchine virtuali in esecuzione in un host ESXi.<br/><br/> il percorso di installazione di Hello deve essere solo caratteri inglesi.<br/><br/> Il file system ReFS non è supportato. | |
| **VMware** |Server VMware vCenter per la gestione degli hypervisor VMware vSphere. Dovrebbe essere in esecuzione vCenter versione 5.1 o 5.5 con gli aggiornamenti più recenti di hello.<br/><br/> Uno o più hypervisor vSphere contenente macchine virtuali VMware è tooprotect. Hello hypervisor deve essere in esecuzione ESX/ESXi versione 5.1 o 5.5 con gli aggiornamenti più recenti di hello.<br/><br/> Nelle macchine virtuali VMware devono essere installati e in esecuzione gli strumenti VMware. | |
| **Computer Windows** |Per i server fisici o le macchine virtuali VMWare protette che eseguono Windows esistono diversi requisiti.<br/><br/> Sistema operativo a 64 bit supportato: **Windows Server 2012 R2**, **Windows Server 2012** o **Windows Server 2008 R2 con SP1 o versioni successive**.<br/><br/> Hello nome host, i punti di montaggio, i nomi dei dispositivi, il percorso di sistema Windows (ad esempio: C:\Windows) deve essere solo in inglese.<br/><br/> sistema operativo Hello deve essere installato nell'unità C:\.<br/><br/> Sono supportati solo i dischi di base. I dischi dinamici non sono supportati.<br/><br/> Regole firewall nel computer protetto dovrebbero consentire loro tooreach hello master e configurazione server di destinazione in Azure.p ><p>È necessario un account amministratore tooprovide (deve essere un amministratore locale nel computer di Windows hello) toopush installare hello servizio di mobilità nei server di Windows. Se l'account di hello fornito è un account non di dominio, occorre toodisable controllo di accesso remoto nel computer locale hello. toodo questo hello Aggiungi voce di registro di sistema LocalAccountTokenFilterPolicy DWORD con un valore pari a 1 in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. voce del Registro di sistema di hello tooadd da CLI aprire cmd o powershell e immettere  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Altre informazioni](https://msdn.microsoft.com/library/aa826699.aspx) sul controllo di accesso.<br/><br/> Dopo il failover, se si desidera collegare tooWindows di macchine virtuali in Azure con Desktop remoto assicurarsi che Desktop remoto è abilitato per hello nel computer locale. Se non si connette tramite VPN, le regole del firewall devono consentire le connessioni Desktop remoto su hello internet. | |
| **Computer Linux** |Un sistema operativo supportato a 64 bit: **Centos 6.4 6.5, 6.6**; **Oracle Enterprise Linux 6.4 6.5 esegue kernel compatibile di hello Red Hat o non interrompibile Enterprise Kernel Release 3 (UEK3)**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Regole firewall nel computer protetto dovrebbero consentire loro configurazione hello tooreach e server di destinazione master in Azure.<br/><br/> il file /etc/hosts nel computer protetto devono contenere le voci che eseguono il mapping degli indirizzi tooIP nome host locale hello associati a tutte le schede di rete <br/><br/> Se si desidera tooconnect tooan virtuali di Azure computer Linux in esecuzione dopo il failover tramite Secure Shell client (ssh), verificare che il servizio di Secure Shell su hello protetto hello macchina è impostata toostart automaticamente all'avvio del sistema del sistema e che le regole del firewall consentono un ssh connessione tooit.<br/><br/> nome host Hello, punti di montaggio, i nomi dei dispositivi e i percorsi di sistema di Linux e i nomi di file (ad esempio/e così via, in /usr.) devono essere solo in inglese.<br/><br/> Protezione può essere abilitata per le macchine locali con hello archiviazione seguenti:-<br>File system: EXT3, ETX4, ReiserFS, XFS<br>Software con percorsi multipli: mapper dispositivi (con percorsi multipli)<br>Gestore volumi: LVM2<br>I server fisici con archiviazione del controller HP CCISS non sono supportati. | |
| **Terze parti** |Alcuni componenti di distribuzione in questo scenario dipendono dal software di terze parti toofunction correttamente. Per un elenco completo, vedere [Informazioni e comunicazioni sul software di terze parti](#third-party) | |

### <a name="network-connectivity"></a>Connettività di rete
Si sono disponibili due opzioni durante la configurazione di connettività di rete tra il sito locale e hello rete virtuale di Azure in cui hello vengono distribuiti i componenti dell'infrastruttura (server di configurazione, i server di destinazione master). È necessario toodecide quali toouse opzione connettività di rete prima di distribuire il server di configurazione. È necessario toochoose questa impostazione in fase di hello della distribuzione. L'impostazione non può essere modificata in seguito.

**Internet:** comunicazione e la replica dei dati tra server locali di hello (server di elaborazione, macchine virtuali protette) e i server del componente dell'infrastruttura di Azure hello (server di configurazione, il server di destinazione master) avviene tramite un protetto SSL / Connessione TLS dal endpoint pubblici di toohello locale nei server di destinazione master e di configurazione di hello. (l'unica eccezione hello è connessione hello tra server di elaborazione hello e server di destinazione master hello sulla porta TCP 9080 che viene crittografata. Solo informazioni di controllo relative toohello protocollo di replica per l'installazione della replica verrà scambiato in questa connessione.)

![Diagramma di distribuzione Internet](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: replica dei dati tra server locali di hello (server di elaborazione, macchine virtuali protette) e i server del componente dell'infrastruttura di Azure hello (server di configurazione, il server di destinazione master) e la comunicazione avviene tramite una connessione VPN tra la rete locale e hello Azure in cui hello vengono distribuiti i server di destinazione master e server di configurazione di rete virtuale. Verificare che la rete locale sia connessa toohello rete virtuale di Azure tramite una connessione ExpressRoute o una connessione VPN da sito a sito.

![Diagramma di distribuzione VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Passaggio 1: Creare un insieme di credenziali
1. Accedi toohello [portale di gestione](https://portal.azure.com).
2. Espandere **Servizi dati** > **Servizi di ripristino** e fare clic su **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Fare clic su **Create vault**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Controllare tooconfirm barra di stato hello che hello insieme di credenziali è stato creato correttamente. insieme di credenziali Hello verrà elencato come **Active** su hello principale **servizi di ripristino** pagina.

## <a name="step-2-deploy-a-configuration-server"></a>Passaggio 2: Distribuire un server di configurazione
### <a name="configure-server-settings"></a>Configurare le impostazioni del server
1. In hello **servizi di ripristino** pagina, fare clic su pagina di avvio rapido di hello insieme di credenziali tooopen hello. Guida introduttiva può anche essere aperto in qualsiasi momento facendo clic sull'icona hello.

    ![Quick Start Icon](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Nell'elenco a discesa hello, selezionare **tra un sito locale con server VMware/fisici e Azure**.
3. In **Preparare le risorse (Azure) di destinazione** fare clic su **Distribuisci server di configurazione**.

    ![Distribuisci server di configurazione](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. In **Dettagli del nuovo server di configurazione** specificare:

   * Un nome per la configurazione hello server e credenziali tooit tooconnect.
   * In tipo di connettività di rete hello elenco a discesa selezionare **rete Internet pubblica** o **VPN**. Si noti che non è possibile modificare questa impostazione dopo averla applicata.
   * Selezionare hello rete di Azure in cui hello server deve essere collocato. Se si usa VPN assicurarsi che hello rete di Azure sia rete locale connesso tooyour come previsto.
   * Specificare l'indirizzo IP interno hello e la subnet che verrà assegnato toohello server. Si noti che i primi quattro indirizzi IP in una qualsiasi subnet hello sono riservati per scopi interni in Azure. Usare gli altri indirizzi IP disponibili.

     ![Distribuisci server di configurazione](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Quando fa clic su **OK** verrà creata nella sottoscrizione per il server di configurazione di hello una macchina virtuale di A3 standard basata su un'immagine della raccolta di Azure Site Recovery Windows Server 2012 R2. Viene creata come hello prima istanza in un nuovo servizio cloud. Se si seleziona tooconnect sul servizio cloud di hello internet hello viene creato con un indirizzo IP pubblico riservato. È possibile monitorare lo stato di avanzamento in hello **processi** scheda.

    ![Monitorare lo stato](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Se ci si connette tramite hello internet, dopo che il server di configurazione hello è nota distribuito hello pubblica IP indirizzo assegnato tooit su hello **macchine virtuali** pagina hello portale di Azure. Quindi, nella hello **endpoint** scheda Nota hello pubblica la porta HTTPS mappato tooprivate porta 443. Queste informazioni in un secondo momento sarà necessario quando si registra i server di elaborazione e di destinazione master hello con il server di configurazione di hello. il server di configurazione di Hello viene distribuito con questi endpoint:

   * HTTPS: Una porta pubblica è toocoordinate utilizzate la comunicazione tra server del componente e hello di Azure tramite internet. Porta privata 443 è toocoordinate utilizzate la comunicazione tra server del componente e Azure tramite VPN.
   * Custom: Una porta pubblica viene utilizzata per la comunicazione di strumento di failback su hello internet. La porta privata 9443 viene usata per la comunicazione con lo strumento di failback tramite VPN.
   * PowerShell: porta privata 5986
   * Desktop remoto: porta privata 3389

   ![Endpoint VM](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Non eliminare o modificare il numero di porta pubblico o privato hello degli endpoint creati durante la distribuzione di server di configurazione.
   >
   >

il server di configurazione di Hello viene distribuito in un servizio cloud di Azure creato automaticamente con un indirizzo IP riservato. indirizzi riservati Hello sono tooensure necessario che l'indirizzo IP del servizio di configurazione server cloud hello rimane uguale hello dopo il riavvio di hello macchine virtuali (incluso il server di configurazione di hello) nel servizio cloud hello. Hello indirizzo IP pubblico riservato sarà necessario toobe manualmente non riservati quando il server di configurazione hello viene rimosso o verrà rimosso riservato. Esiste un limite predefinito di 20 indirizzi IP pubblici riservati per ogni sottoscrizione. [Altre informazioni](../virtual-network/virtual-networks-reserved-private-ip.md) sugli indirizzi IP riservati.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Registrare il server di configurazione di hello nell'insieme di credenziali hello
1. In hello **avvio rapido** pagina fare clic su **preparare le risorse di destinazione** > **scaricare una chiave di registrazione**. file di chiave Hello viene generato automaticamente. È valido 5 giorni dopo essere stato generato. Copiare il file server di configurazione toohello.
2. In **macchine virtuali** server di configurazione hello selezionare dall'elenco di macchine virtuali hello. Aprire hello **Dashboard** scheda e fare clic su **Connetti**. **Aprire** hello scaricato toolog file RDP nel server di configurazione hello tramite Desktop remoto. Se si sta usando una VPN, utilizzare l'indirizzo IP interno hello (indirizzo hello specificato al momento della distribuzione del server di configurazione hello) per una connessione Desktop remoto da sito locale hello. l'installazione guidata di Azure Site Recovery configurazione Server Hello viene eseguito automaticamente quando si accede per hello prima volta.

    ![Registrazione](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. In **installazione Software di terze parti** fare clic su **accetto** toodownload e installare MySQL.

    ![Installazione di MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. In **i dettagli del Server MySQL** creare credenziali toolog sull'istanza del server MySQL hello.

    ![Credenziali di MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. In **impostazioni Internet** specificare la modalità server di configurazione hello si connetteranno toohello internet. Si noti che:

   * Se si desidera toouse un proxy personalizzato è necessario configurarlo prima di installare hello Provider.
   * Quando fa clic su **Avanti** connessione proxy di hello toocheck verrà eseguito da un test.
   * Se si utilizza un proxy personalizzato, o il proxy predefinito richiede l'autenticazione, occorre dettagli del proxy hello tooenter, incluse le credenziali, porta e indirizzo hello.
   * Hello URL seguenti devono essere accessibile tramite proxy hello:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Se sono basate sull'indirizzo IP regole firewall verificare che le regole di hello siano impostate comunicazione tooallow hello configurazione server toohello degli indirizzi IP descritti [intervalli IP dei Data Center Azure](https://msdn.microsoft.com/library/azure/dn175718.aspx) e il protocollo HTTPS (443). È necessario che gli intervalli IP toowhite-elenco di hello regione di Azure che si prevede di toouse e quello di Stati Uniti occidentali.

     ![Registrazione del proxy](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. In **impostazioni localizzazione messaggio di errore del Provider** specificare in quale lingua si desidera tooappear i messaggi di errore.

    ![Registrazione di messaggi di errore](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. In **Azure Site Recovery registrazione** Sfoglia e i file di chiave hello selezionare copiato toohello server.

    ![Registrazione del file di chiave](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Nella pagina di completamento hello della procedura guidata hello selezionare queste opzioni:

   * Selezionare **avvia finestra di dialogo Gestione Account** deve aprire toospecify che hello finestra di dialogo Gestione account dopo aver completato la procedura guidata hello.
   * Selezionare **creare un'icona sul desktop per Cspsconfigtool** tooadd un collegamento sul desktop nel server di configurazione hello in modo che sia possibile aprire hello **Gestisci account** finestra di dialogo in qualsiasi momento senza la necessità di hello toorerun procedura guidata.

     ![Completare la registrazione](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Fare clic su **fine** guidata hello toocomplete. Verrà generata una passphrase. Copiare il percorso sicuro tooa. Si sarà necessario tooauthenticate e registrare processo hello e i server di destinazione master con il server di configurazione di hello. Integrità canale tooensure è utilizzato anche nelle comunicazioni di server di configurazione. È possibile rigenerare la passphrase hello ma sarà necessario toore la registrazione di destinazione master hello e i server di elaborazione con hello nuova passphrase.

    ![Passphrase](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Dopo la registrazione del server di configurazione hello verrà elencato nella hello **server di configurazione** pagina nell'insieme di credenziali hello.

### <a name="set-up-and-manage-accounts"></a>Impostare e gestire gli account
Durante la distribuzione il ripristino del sito richiede le credenziali per hello seguenti azioni:

* Un account di VMware, per permettere a Site Recovery di rilevare automaticamente le macchine virtuali nei server vCenter o negli host vSphere.
* Quando si aggiungono macchine per la protezione, in modo che il ripristino del sito può installare il servizio di mobilità hello su di essi.

Dopo aver registrato il server di configurazione di hello è possibile aprire hello **Gestisci account** tooadd finestra di dialogo e gestire gli account che devono essere utilizzati per eseguire queste azioni. Esistono un paio di modi toodo questo:

* Aprire il collegamento hello si è scelto di toocreated per la finestra di dialogo hello hello ultima pagina del programma di installazione per il server di configurazione hello (cspsconfigtool).
* Finestra di dialogo Apri hello nel completamento dell'installazione del server di configurazione.

1. In **Gestisci account** click **Aggiungi account**. È inoltre possibile modificare ed eliminare account esistenti.

    ![Gestisci account](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. In **dettagli Account** specificare un toouse nome di account in Azure e le credenziali (nome di dominio/utente).

    ![Gestisci account](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Connettere il server di configurazione toohello
Esistono due server di configurazione toohello di tooconnect modi:

* Tramite una connessione VPN da sito a sito o ExpressRoute
* Su hello internet

Si noti che:

* Una connessione internet utilizza gli endpoint di hello della macchina virtuale hello in combinazione con hello indirizzo IP virtuale pubblico del server di hello.
* Una connessione VPN Usa indirizzo IP interno hello del server hello insieme alle porte private dell'endpoint di hello.
* Se è toodecide una sola volta tooconnect (dati di controllo e della replica) dal toohello Server on-premise vari server del componente (server di configurazione, il server di destinazione master) in esecuzione in Azure tramite una connessione VPN o internet hello. Non è possibile modificare questa impostazione in un secondo momento. Se non si sarà necessario tooredeploy hello scenario e ricrea la protezione dei computer.  

## <a name="step-3-deploy-hello-master-target-server"></a>Passaggio 3: Distribuire il server di destinazione master hello
1. Fare clic su **Preparare le risorse (Azure) di destinazione** > **Distribuisci server di destinazione master**.
2. Specificare le credenziali e i dettagli del server di destinazione principale hello. server Hello saranno distribuiti in hello stessa rete del server di configurazione hello Azure. Quando si fa clic toocomplete una macchina virtuale di Azure verrà creata con un'immagine della raccolta Windows o Linux.

    ![Impostazioni del server di destinazione](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Si noti che i primi quattro indirizzi IP in una qualsiasi subnet hello sono riservati per scopi interni in Azure. Specificare gli altri indirizzi IP disponibili.

> [!NOTE]
> Selezionare Standard DS4 durante la configurazione di protezione per i carichi di lavoro che richiedono prestazioni dei / o elevata coerente e bassa latenza in ordine toohost i/o intensivo carichi di lavoro con [Account di archiviazione Premium](../storage/common/storage-premium-storage.md).
>
>

1. Viene creata una macchina virtuale del server di destinazione master Windows con gli endpoint indicati di seguito. Si noti che gli endpoint pubblici vengono creati solo se la connessione su hello internet.

   * Custom: Porta pubblica utilizzata dai dati di replica di hello processo server toosend tramite hello internet. Porta privata 9443 viene utilizzata da hello processo server toosend replica dati toohello server di destinazione master tramite VPN.
   * Personalizzata1: Utilizzato da hello processo server toosend metadati su hello la porta pubblica internet. Porta privata 9080 viene utilizzata dal server di destinazione master di hello processo server toosend metadati toohello tramite VPN.
   * PowerShell: porta privata 5986
   * Desktop remoto: porta privata 3389
2. Viene creata una macchina virtuale del server di destinazione master Linux con gli endpoint indicati di seguito. Si noti che vengono creati gli endpoint pubblici solo se ci si connette tramite hello internet.

   * Custom: Porta pubblica utilizzata dai dati di replica di processo server toosend tramite hello internet. Porta privata 9443 viene utilizzata da hello processo server toosend replica dati toohello server di destinazione master tramite VPN.
   * Personalizzata1: Porta pubblica è utilizzata da hello processo server toosend metadati su hello internet. Porta privata 9080 viene utilizzata dal server di destinazione master di hello processo server toosend metadati toohello tramite VPN
   * SSH: porta privata 22

     > [!WARNING]
     > Non eliminare o modificare il numero di porta pubblico o privato hello di qualsiasi endpoint hello creati durante la distribuzione di server di destinazione master hello.
     >
     >
3. In **macchine virtuali** attendere hello toostart di macchina virtuale.

   * Se si tratta di una nota di Windows server verso il basso dettagli hello del desktop remoto.
   * Se si tratta di un server Linux e ci si connette tramite VPN nota hello indirizzo IP interno della macchina virtuale hello. Se ci si connette tramite hello internet nota hello indirizzo IP pubblico.
4. Accedere a installazione di toocomplete server hello e registrarlo con il server di configurazione di hello.
5. Se si usa Windows:

   1. Avviare una macchina virtuale di toohello connessione desktop remoto. Hello prima volta che accede a uno script verrà eseguito in una finestra di PowerShell. Non chiuderla. Al termine dello strumento di configurazione dell'agente Host hello viene aperta automaticamente server hello tooregister.
   2. In **configurazione dell'agente Host** specificare l'indirizzo IP interno hello del server di configurazione hello e la porta 443. È possibile utilizzare l'indirizzo interno hello e la porta privata 443, anche se ci si connette tramite VPN non perché la macchina virtuale di hello è collegato toohello stessa rete del server di configurazione hello Azure. Lasciare abilitata l'opzione **Use HTTPS** . Immettere la passphrase hello per server di configurazione hello annotati in precedenza. Fare clic su **OK** server hello tooregister. È possibile ignorare le opzioni di hello NAT. in quanto non vengono usate.
   3. Se il requisito di unità di conservazione stimato è più di 1 TB, è possibile configurare volume di conservazione hello (r) mediante un disco virtuale e [spazi di archiviazione](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Server di destinazione master Windows](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Se si usa Linux:

   1. Verificare che è stato installato hello più recente Linux Integration Services (LIS) installato prima di installare il server di destinazione master hello. È possibile trovare una versione più recente di LIS hello insieme alle istruzioni su come tooinstall [qui](https://www.microsoft.com/download/details.aspx?id=46842). Riavviare il computer di hello dopo l'installazione di LIS hello.
   2. In **Preparare le risorse (Azure) di destinazione** fare clic su **Scarica e installa il software aggiuntivo (solo per il server di destinazione master Linux)**. Hello copia scaricato tar file toohello macchina virtuale utilizzando un client FTP sicuro. In alternativa è possibile accedere al server di destinazione master linux distribuito toohello e utilizzare *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* file hello di hello toodownload.
   3. Accedere al server toohello utilizzando un client Secure Shell. Se si è connessi toohello rete tramite VPN di Azure usare l'indirizzo IP interno hello. In caso contrario, utilizzare l'indirizzo IP esterno hello ed endpoint pubblico di hello SSH.
   4. Estrarre i file hello dal programma di installazione compresso con gzip hello eseguendo: **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![server di destinazione master Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Assicurarsi di essere in toowhich directory hello è stato estratto il contenuto di hello del file con estensione tar hello.
   6. Copia hello server passphrase tooa locale file di configurazione utilizzando il comando hello **echo  *`<passphrase>`*  > passphrase.txt**
   7. Eseguire il comando hello "**sudo. /Install -t entrambi - a -R host /usr/local/ASR -d MasterTarget -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**".

      ![Registrare il server di destinazione](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Attendere alcuni minuti (10-15) e in controllo pagina hello indicato come registrato nel server di destinazione master hello **server** > **server di configurazione** **idettaglidelServer** scheda. Se si eseguono Linux e non ha registrato ripetere host hello strumento di configurazione /usr/local/ASR/Vx/bin/hostconfigcli. È necessario tooset le autorizzazioni di accesso eseguendo chmod come radice.

    ![Verificare il server di destinazione](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Potrebbe essere necessaria fino too15 minuti dopo la registrazione è stata completata per toobe server di destinazione master hello elencato nel portale di hello. tooupdate immediatamente, fare clic su **aggiornamento** su hello **server di configurazione** pagina.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Passaggio 4: Distribuire server di elaborazione locale hello
Prima di iniziare, è consigliabile configurare un indirizzo IP statico nel server di elaborazione hello in modo che è sicuramente toobe permanente attraverso riavvii.

1. Fare clic su avvio rapido > **installare Server di elaborazione locale** > **scaricare e installare il server di elaborazione hello**.

    ![Installare il server di elaborazione](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Hello copia scaricato server toohello di file zip in cui si userà il server di elaborazione tooinstall hello. file zip Hello contiene due file di installazione:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Decomprimere hello archivio e copia hello file tooa percorso di installazione su server hello.
4. Eseguire hello **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** file di installazione e seguire le istruzioni di hello. Consente di installare i componenti di terze parti necessari per la distribuzione di hello.
5. Eseguire quindi **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. In hello **modalità Server** pagina selezionare **Server di elaborazione**.
7. In hello **dettagli sull'ambiente** hello pagina seguente:

    - Se si desidera fare clic su macchine virtuali VMware di tooprotect **Sì**
    - Se si desidera che solo i server fisici tooprotect e non deve dunque vCLI VMware installato nel server di elaborazione hello. fare clic su **No** e continuare.

1. Si noti seguenti hello quando si installa vCLI VMware:

   * **È supportato solo VMware vSphere CLI 5.5.0**. server di elaborazione Hello non funziona con le altre versioni o gli aggiornamenti di vSphere CLI.
   * Scaricare vSphere CLI 5.5.0 da [qui.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Se è installato vSphere CLI appena prima di iniziare l'installazione di server di elaborazione hello, non rileva il programma di installazione, attendere fino a toofive minuti prima di riprovare l'installazione. In questo modo si garantisce che tutte le variabili di ambiente hello necessari per il rilevamento di vSphere CLI sono state inizializzate in modo corretto.
2. In **selezione NIC per Server di elaborazione** scheda di rete selezionare hello è necessario utilizzare il server di elaborazione hello.

   ![Selezionare la scheda](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. In **Dettagli del server di configurazione**:

   * Per indirizzo IP hello e la porta, se ci si connette tramite VPN specificare indirizzo IP interno hello hello del server di configurazione e la 443 per la porta hello. In caso contrario specificare indirizzo IP virtuale pubblico di hello e mappato endpoint HTTP pubblico.
   * Digitare la passphrase hello hello del server di configurazione.
   * Deselezionare **firma software servizio di mobilità verificare** se si desidera toodisable verifica quando si usa servizio di push automatico tooinstall hello. Verifica della firma necessita della connettività internet dal server di elaborazione hello.
   * Fare clic su **Avanti**.

   ![Registrare il server di configurazione](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. In **Selezionare l'unità di installazione** selezionare un'unità cache. server di elaborazione Hello deve un'unità di cache con un minimo di 600 GB di spazio libero. Fare clic su **Installa**.

   ![Registrare il server di configurazione](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Si noti che potrebbe essere necessario installazione hello toocomplete di toorestart hello server. In **Server di configurazione** > **i dettagli del Server** controllare tale server di elaborazione hello viene visualizzata ed è stato registrato nell'insieme di credenziali hello.

> [!NOTE]
> Potrebbe essere necessaria fino too15 minuti dopo la registrazione è stata completata per hello processo server tooappear come elencato nella sezione server di configurazione hello. tooupdate immediatamente, aggiornare il server di configurazione hello facendo clic sul pulsante Aggiorna hello nella parte inferiore di hello hello server della pagina di configurazione
>
>

![Convalidare il server di elaborazione](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Se si non disabilita la verifica della firma per il servizio di mobilità hello durante la registrazione di server di elaborazione hello è possibile farlo in un secondo momento come indicato di seguito:

1. Accedere al server di elaborazione hello come amministratore e aprire il file hello C:\pushinstallsvc\pushinstaller.conf per la modifica. Nella sezione hello **[PushInstaller.transport]** aggiungere questa riga: **SignatureVerificationChecks = "0"**. Salvare e chiudere il file hello.
2. Riavviare servizio InMage PushInstall hello.

## <a name="step-5-update-site-recovery-components"></a>Passaggio 5: Aggiornare i componenti di Site Recovery
I componenti di ripristino del sito vengono aggiornati da tootime ora. Quando sono disponibili nuovi aggiornamenti è necessario installare tali hello seguente ordine:

1. Server di configurazione
2. Server di elaborazione
3. Server master di destinazione
4. Strumento di failback (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Ottenere e installare gli aggiornamenti di hello
1. È possibile ottenere gli aggiornamenti per i server di destinazione master, processi e configurazione di hello da Site Recovery hello **Dashboard**. Per l'installazione di Linux estrarre file hello dal programma di installazione compresso con gzip hello ed eseguire il comando hello "sudo. /Install" aggiornamento hello tooinstall.
2. [Scaricare](http://go.microsoft.com/fwlink/?LinkID=533813) hello aggiornamento più recente di hello Failback tool(vContinuum).
3. Se si eseguono le macchine virtuali o i server fisici che è già installato servizio di mobilità di hello, è possibile ottenere gli aggiornamenti per il servizio hello come indicato di seguito:

   * **Opzione 1**: scaricare gli aggiornamenti seguenti.
     * [Windows Server (solo 64 bit)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (solo 64 bit)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5 (solo 64 bit)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (solo 64 bit)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Dopo aver aggiornato i messaggi hello del processo server hello versione aggiornata del servizio di mobilità hello saranno disponibili nella cartella C:\pushinstallsvc\repository hello nel server di elaborazione hello.
   * **Opzione 2**: se si dispone di un computer con una versione precedente di hello installato servizio di mobilità, è possibile aggiornare automaticamente il servizio di mobilità hello computer hello dal portale di gestione di hello.

     1. Verificare che server di elaborazione hello viene aggiornato.
     2. Verificare che il computer protetto di hello sia conforme a hello [prerequisiti](#install-the-mobility-service-automatically) per inserire automaticamente il servizio di mobilità hello, in modo che aggiornamento hello funziona come previsto.
     3. Gruppo protezione dati selezionare hello, evidenziazione hello protected computer e fare clic su **servizio di mobilità aggiornamento**. Questo pulsante è disponibile solo se è presente una versione più recente del servizio di mobilità hello.

         ![Selezionare il server vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

In Seleziona account specificare servizio di mobilità di hello amministratore account toobe utilizzato tooupdate hello nel server protetto hello. Fare clic su OK e attendere toocomplete processo hello attivato.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Passaggio 6: Aggiungere server vCenter o host vSphere
1. Fare clic su **server** > **server di configurazione** > server di configurazione >**aggiungere Server vCenter** tooadd un host di server o vSphere vCenter.

    ![Selezionare il server vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Specificare i dettagli per server hello o l'host e server di elaborazione selezionare hello che verrà utilizzato toodiscover è.

   * Se non è in esecuzione sulla porta 443 predefinita di hello server vCenter hello specificare il numero di porta hello in cui hello vCenter server è in esecuzione.
   * server di elaborazione Hello deve essere nella stessa rete come hello vCenter server/host vSphere e deve essere VMware vSphere CLI installata 5.5.0 di hello.

     ![Impostazioni del server vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Al termine dell'individuazione server vCenter hello sarà elencata sotto i dettagli del server configuration hello.

    ![Impostazioni del server vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Se si utilizza un server di hello tooadd account senza privilegi di amministratore o un host, assicurarsi che disponga di hello hello seguenti privilegi:

   * Per gli account vCenter devono essere abilitati i privilegi Datacenter, Datastore, Folder, Host, Network, Resource, Storage views, Virtual machine e vSphere Distributed Switch abilitati.
   * gli account di host di vSphere devono avere hello Data Center, l'archivio dati, cartella, Host, rete, risorsa, macchina virtuale e privilegi Switch distribuiti vSphere abilitati

## <a name="step-7-create-a-protection-group"></a>Passaggio 7: Creare un gruppo di protezione
1. Aprire **Elementi protetti** > **Gruppo di protezione** > **Crea gruppo di protezione**.

    ![Crea gruppo di protezione](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. In hello **specifica le impostazioni del gruppo di protezione** pagina specificare un nome per il gruppo di hello e server di configurazione selezionare hello in cui si desidera che il gruppo di hello toocreate.

    ![Impostazioni del gruppo di protezione](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. In hello **specificare le impostazioni di replica** pagina configurare le impostazioni di replica hello che verranno utilizzate per tutte le macchine hello gruppo hello.

    ![Replica del gruppo di protezione](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Impostazioni:

   * **La coerenza Multi VM**: se attivare questa opzione crea punti di ripristino coerenti con l'applicazione condivisa tra più computer hello in gruppo protezione dati hello. Questa impostazione è molto utile durante l'esecuzione di tutti i computer hello in gruppo protezione dati hello hello stesso carico di lavoro. Tutti i computer sarà ripristinato toohello stesso punto dati. Disponibile solo per i server Windows.
   * **Soglia RPO**: verranno generati avvisi quando la replica di protezione dei dati continua di hello RPO supera valore di soglia RPO hello configurato.
   * **Conservazione del punto di ripristino**: Specifica il periodo di memorizzazione hello. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di questa finestra.
   * **Frequenza di snapshot coerenti con l'applicazione**: specifica con quale frequenza verranno creati i punti di ripristino contenenti snapshot coerenti con l'applicazione.

È possibile monitorare il gruppo di protezione dati hello che vengono creati in hello **elementi protetti** pagina.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Passaggio 8: Configurare i computer desiderati tooprotect
È necessario tooinstall hello servizio Mobility nelle macchine virtuali e server fisici che si desidera tooprotect. Questa operazione può essere eseguita in due modi:

* Push e installare il servizio hello in ogni computer dal server di elaborazione hello automaticamente.
* Installare manualmente il servizio di hello.

### <a name="install-hello-mobility-service-automatically"></a>Installare il servizio di mobilità hello automaticamente
Quando si aggiungono macchine tooa protezione gruppo hello servizio di mobilità è inserito automaticamente e installata in ogni computer da server di elaborazione hello.

**Automaticamente l'installazione push del servizio di mobilità hello in Windows Server:**

1. Installare gli aggiornamenti più recenti di hello per il server di elaborazione hello, come descritto in [passaggio 5: installare gli aggiornamenti più recenti](#step-5-install-latest-updates)e assicurarsi che il server di elaborazione hello è disponibile.
2. Verificare che non c'è connettività di rete tra il computer di origine hello e hello server di elaborazione e tale macchina di origine hello sia accessibile dal server di elaborazione hello.  
3. Configurare hello Windows firewall tooallow **condivisione File e stampanti** e **Strumentazione gestione Windows**. In impostazioni di Windows Firewall, selezionare l'opzione hello "Consenti app o funzionalità attraverso Firewall" e selezionare applicazioni hello come illustrato nell'immagine di hello riportata di seguito. Per i computer appartenenti al dominio tooa è possibile configurare i criteri firewall hello con un oggetto Criteri di gruppo.

    ![Impostazioni del firewall](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. l'installazione push Hello account utilizzato tooperform hello deve essere nel gruppo Administrators hello macchina hello desiderato tooprotect. Queste credenziali vengono utilizzate solo per l'installazione push del servizio di mobilità hello ed è necessario specificare quando si aggiunge un gruppo di protezione dati tooa macchina.
5. Hello fornito l'account non è un account di dominio, occorre toodisable controllo di accesso remoto nel computer locale hello. toodo questo hello Aggiungi voce di registro di sistema LocalAccountTokenFilterPolicy DWORD con un valore pari a 1 in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. voce del Registro di sistema di hello tooadd da CLI aprire cmd o powershell e immettere  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Automaticamente l'installazione push del servizio di mobilità hello in server Linux:**

1. Installare gli aggiornamenti più recenti di hello per il server di elaborazione hello, come descritto in [passaggio 5: installare gli aggiornamenti più recenti](#step-5-install-latest-updates)e assicurarsi che il server di elaborazione hello è disponibile.
2. Verificare che non c'è connettività di rete tra il computer di origine hello e hello server di elaborazione e tale macchina di origine hello sia accessibile dal server di elaborazione hello.  
3. Verificare che l'account hello è un utente root nel server di hello origine Linux.
4. Verificare che il file /etc/hosts hello sull'origine hello Linux server contiene voci che mappa gli indirizzi tooIP nome host locale hello associati a tutte le schede di rete.
5. Installare openssh più recente di hello, openssh-server, pacchetti openssl sulla macchina di hello desiderato tooprotect.
6. Assicurarsi che SSH sia abilitato e in esecuzione sulla porta 22.
7. Abilitare l'autenticazione SFTP di sottosistema e password nel file sshd_config hello come segue:

   * a) Accedere come utente ROOT.
   * b) in hello file via/ssh/file sshd_config, trova hello riga che inizia con **PasswordAuthentication**.
   * c) rimuovere il commento riga hello e hello valore da "no" troppo "yes".

       ![Mobility di Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) riga di hello trova che inizia con sottosistema e rimuovere il commento riga hello.

       ![Mobility push Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Verificare la variante Linux macchina di origine hello è supportato.

### <a name="install-hello-mobility-service-manually"></a>Installare manualmente il servizio di mobilità hello
i pacchetti software Hello utilizzato tooinstall hello mobilità servizio si trovano in server di elaborazione hello in C:\pushinstallsvc\repository. Accedere al server di elaborazione hello e copia hello installazione appropriato pacchetto toohello macchina di origine basato su tabella hello riportata di seguito:-

| Sistema operativo di origine | Pacchetto del servizio Mobility nel server di elaborazione |
| --- | --- |
| Windows Server (solo 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (solo 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (solo 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (solo 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**hello tooinstall servizio di mobilità manualmente in un server Windows**, hello seguenti:

1. Hello copia **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** pacchetto dal percorso di directory hello processo server elencate nella tabella di hello sopra toohello macchina di origine.
2. Installare il servizio di mobilità hello eseguendo hello eseguibile nel computer di origine hello.
3. Seguire le istruzioni di installazione di hello.
4. Selezionare **servizio di mobilità** come ruolo hello e fare clic su **Avanti**.

    ![Installare il servizio Mobility](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. La directory di installazione hello come percorso di installazione predefinito hello e fare clic su **installare**.
6. In **configurazione dell'agente Host** specificare l'indirizzo IP hello e la porta HTTPS hello del server di configurazione.

   * Se ci si connette tramite internet specificare hello hello indirizzo IP virtuale pubblico e pubblica endpoint HTTPS come porta hello.
   * Se ci si connette tramite VPN specificare l'indirizzo IP interno hello e 443 per la porta hello. Lasciare selezionata l'opzione **Use HTTPS** .

     ![Installare il servizio Mobility](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Specificare la passphrase di hello configurazione server e fare clic su **OK** hello tooregister servizio di mobilità con il server di configurazione di hello.

**toorun dalla riga di comando hello:**

1. Copiare hello passphrase hello CX toohello file "C:\connection.passphrase" hello server ed eseguire questo comando. In questo esempio CX i 104.40.75.37 e hello porta HTTPS è 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Installare manualmente il servizio di mobilità hello in un server Linux**:

1. Copiare l'archivio di tar appropriato hello basato sulla tabella hello sopra riportata, dal computer di origine toohello di hello processo server.
2. Aprire un programma shell ed estrarre percorso locale tooa archivio con estensione tar compresso hello eseguendo`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Creare un file passphrase.txt in hello toowhich di directory locale è stato estratto il contenuto di hello dell'archivio tar hello immettendo  *`echo <passphrase> >passphrase.txt`*  dalla shell.
4. Installare il servizio Mobility hello immettendo  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Specificare la porta e indirizzo IP hello:

   * Se ci si connette il server di configurazione toohello su internet specificare hello configurazione server virtuale indirizzo IP pubblico e pubblica endpoint HTTPS in hello `<IP address>` e `<port>`.
   * Se ci si connette tramite una connessione VPN specificare 443 e l'indirizzo IP interno hello.

**toorun dalla riga di comando hello**:

1. Copiare la passphrase hello dal file toohello hello CX "passphrase.txt" nel server di hello ed eseguire questo comando. In questo esempio CX i 104.40.75.37 e hello porta HTTPS è 62519:

tooinstall in un server di produzione:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall nel server di destinazione hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Quando si aggiunta gruppo di protezione dati tooa macchine che già eseguono una versione appropriata del servizio di mobilità hello quindi l'installazione push hello viene ignorata.
>
>

## <a name="step-9-enable-protection"></a>Passaggio 9: Abilitare la protezione
protezione tooenable aggiungere macchine virtuali e gruppo di server fisici tooa protezione dati. Prima di iniziare, tenere presente quanto segue:

* Macchine virtuali vengono individuate ogni 15 minuti e può richiedere fino a too15 minuti relativa tooappear in Azure Site Recovery dopo l'individuazione.
* Le modifiche dell'ambiente nella macchina virtuale hello (ad esempio, l'installazione degli strumenti di VMware) possono richiedere anche too15 minuti toobe aggiornato in Site Recovery.
* È possibile controllare hello individuati ultima volta in hello **ultimo contatto in** campo per hello vCenter/ESXi di server host hello **server di configurazione** pagina.
* Se si dispone di un gruppo protezione dati già creato, aggiunta un host di Server o ESXi vCenter dopo che avrà 15 minuti per toorefresh portale di Azure Site Recovery hello e per macchine virtuali toobe elencati in hello **Aggiungi un gruppo di protezione tooa macchine**  finestra di dialogo.
* Se si desidera tooproceed immediatamente con l'aggiunta di gruppo tooprotection macchine senza attendere l'individuazione pianificata hello, evidenziare il server di configurazione di hello (selezionarla) e fare clic su hello **aggiornamento** pulsante.
* Quando si aggiunta macchine virtuali o un gruppo di protezione di computer fisici tooa, server process hello inserisce automaticamente e installa il servizio di mobilità hello nel server di origine hello se hello non è già installato.
* Per il meccanismo di push automatico hello toowork assicurarsi aver configurato i computer protetti come descritto nel passaggio precedente hello.

Aggiungere i computer come segue:

1. Fare clic su **Elementi protetti** > **Gruppo di protezione** > **Computer** > **Aggiungi computer**. Come procedura consigliata, è consigliabile che i gruppi protezione dati devono rispecchiare i carichi di lavoro in modo che si aggiungono macchine in esecuzione un'applicazione specifica di toohello nello stesso gruppo.
2. In **Seleziona macchine virtuali** per la protezione dei server fisici, in hello **aggiungere le macchine fisiche** guidata specificare l'indirizzo IP hello e il nome descrittivo. Selezionare quindi la famiglia di sistemi operativi hello.

    ![Aggiungere un server V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. In **Seleziona macchine virtuali** se si proteggono macchine virtuali VMware, selezionare un server vCenter che gestisce le macchine virtuali host EXSi hello in cui vengono eseguiti (o), quindi macchine hello.

    ![Aggiungere un server V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. In **risorse di destinazione specificare** selezionare i server di destinazione master hello e toouse di archiviazione per la replica e consente di indicare se le impostazioni di hello devono essere utilizzate per tutti i carichi di lavoro. Selezionare [Account di archiviazione Premium](../storage/common/storage-premium-storage.md) durante la configurazione della protezione per i carichi di lavoro che richiedono coerente delle prestazioni dei / o alta e bassa latenza nei carichi di lavoro con utilizzo intensivo ordine toohost IO. Se si desidera toouse un account di archiviazione Premium per i dischi del carico di lavoro, è necessario toouse hello Master di destinazione della serie DS. Non è possibile usare dischi di archiviazione Premium su destinazioni master diverse dalla serie DS.

   > [!NOTE]
   > Non è supportata spostamento hello di account di archiviazione creati utilizzando hello [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse.
   >
   >

    ![Server vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. In **specificare account** selezionare hello account toouse per l'installazione di servizio di mobilità hello nei computer protetti. le credenziali dell'account Hello sono necessari per l'installazione automatica di hello servizio di mobilità. Se non è possibile selezionare un account, assicurarsi di configurare uno come descritto nel passaggio 2. Si noti che questo account non è accessibile da Azure. Per Windows account hello del server deve disporre di privilegi di amministratore nel server di origine hello. Per Linux hello è necessario account radice.

    ![Credenziali Linux](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Fare clic su hello segno di spunta toofinish aggiunta macchine toohello protezione toostart e gruppo di replica iniziale per ogni computer. È possibile monitorare lo stato su hello **processi** pagina.

    ![Aggiungere un server V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. Per monitorare lo stato della protezione, fare clic su **Elementi protetti** > nome del gruppo di protezione > **Macchine virtuali**. Dopo il completamento della replica iniziale e macchine hello stanno sincronizzando i dati verranno visualizzati **Protected** stato.

    ![Processi di macchine virtuali](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Impostare le proprietà dei computer protetti
1. Quando lo stato della macchina virtuale è **Protetto** , sarà possibile configurarne le proprietà di failover. In dettagli del gruppo di protezione hello selezionare hello hello computer e aprire **configura** scheda.
2. È possibile modificare il nome hello che verrà assegnato al computer toohello in Azure dopo il failover e hello dimensioni di macchina virtuale di Azure. È inoltre possibile selezionare hello Azure rete toowhich hello macchina verrà connessa dopo il failover.

   > [!NOTE]
   > [Migrazione delle reti](../resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per le reti utilizzate per la distribuzione di Site Recovery.
   >
   >

    ![Impostare le proprietà di una macchina virtuale](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Si noti che:

* nome di Hello di hello Azure macchina deve essere conforme ai requisiti di Azure.
* Per impostazione predefinita le macchine virtuali replicate in Azure non sono connessi tooan rete di Azure. Se si desidera toocommunicate assicurarsi che le macchine virtuali replicate tooset hello stessa rete di Azure per loro.
* Se si ridimensiona un volume in una macchina virtuale VMware o un server fisico, questo entra in uno stato critico. Se è necessario dimensioni hello toomodify, hello seguenti:

  * a) modificare l'impostazione delle dimensioni di hello.
  * b) in hello **macchine virtuali** , selezionare una macchina virtuale hello e fare clic su **rimuovere**.
  * c) in **Rimuovi macchina virtuale** selezionare opzione hello **Disabilita protezione (usare per il ripristino drill e il ridimensionamento del volume)**. Questa opzione Disabilita la protezione, ma mantiene i punti di ripristino hello in Azure.

      ![Impostare le proprietà di una macchina virtuale](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) riabilitare la protezione per la macchina virtuale hello. Quando si riabilita la protezione dei dati di hello per il volume ridimensionato hello sarà tooAzure trasferiti.

## <a name="step-10-run-a-failover"></a>Passaggio 10: Eseguire un failover
Attualmente è possibile eseguire solo failover non pianificati per le macchine virtuali VMware e i server fisici protetti. Si noti hello segue:

* Prima di avviare un failover, assicurarsi che i server di destinazione master e di configurazione hello siano in esecuzione e integro. In caso contrario, il failover avrà esito negativo.
* I computer di origine non vengono arrestati nell'ambito di un failover non pianificato. Eseguire un failover non pianificato arresta la replica dei dati per i server protetti hello. Si sarà necessario macchine hello toodelete dal gruppo protezione dati hello e aggiungerli nuovamente nell'ordine toostart proteggere computer nuovo termine hello failover non pianificato.
* Se si desidera toofail sulla senza perdere i dati, assicurarsi che le macchine virtuali del sito primario hello sono disattivate prima di iniziare il failover hello.

1. In hello **piani di ripristino** pagina e aggiungere un piano di ripristino. Specificare i dettagli per il piano di hello e selezionare **Azure** come destinazione di hello.

    ![Configurare un piano di ripristino](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. In **seleziona macchina virtuale** selezionare un gruppo protezione dati e quindi selezionare le macchine nel piano di ripristino toohello tooadd gruppo hello. [Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.

    ![Aggiungi macchine virtuali.](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Se necessario è possibile personalizzare i gruppi del piano di toocreate hello e ordine della sequenza hello in cui macchine recupero hello piano viene eseguito il failover. È anche possibile aggiungere istruzioni per azioni manuali e script. Hello script quando ripristino tooAzure può essere aggiunti tramite [runbook di automazione di Azure](site-recovery-runbook-automation.md).
4. In hello **piani di ripristino** pagina piano hello selezionare e fare clic su **Failover non pianificato**.
5. In **conferma Failover** controllare la direzione del failover hello (tooAzure) e selezionare toofail punto di ripristino hello su a.
6. Attendere toocomplete processo di failover hello e quindi verificare che il failover hello funziona come previsto e che hello replicate le macchine virtuali inizio correttamente in Azure.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Passaggio 11: Eseguire il failback dei computer sottoposti a failover da Azure
[Altre informazioni](site-recovery-failback-azure-to-vmware-classic-legacy.md) sul toobring la non riuscita nel computer in esecuzione in Azure nuovamente tooyour nell'ambiente locale.

## <a name="manage-your-process-servers"></a>Gestire i server di elaborazione
server di elaborazione Hello invia server di destinazione master toohello dati di replica in Azure e individua nuova VMware le macchine virtuali aggiunte tooa vCenter server. Nelle seguenti circostanze hello è server di elaborazione hello toochange nella distribuzione:

* Se si arresta il server di elaborazione corrente hello
* Se il punto di ripristino (RPO) obiettivo aumenta tooan livello non accettabile per l'organizzazione.

Se necessario che è possibile spostare la replica di alcuni o tutti i VMware locale virtuale hello macchine e i server fisici tooa diverso processo server. ad esempio:

* **Errore**: se un server di elaborazione non riesce o non è disponibile, è possibile spostare server di elaborazione tooanother replica macchina virtuale protetta. I metadati della macchina di origine hello e computer di replica saranno spostati toohello nuovo server di elaborazione e dati viene risincronizzati. il nuovo server di elaborazione Hello verranno connesse automaticamente toohello vCenter server tooperform l'individuazione automatica. È possibile monitorare lo stato di hello del server di elaborazione dashboard di Site Recovery hello.
* **Il bilanciamento del carico tooadjust RPO**, per migliorare il bilanciamento del carico è possibile selezionare un server di elaborazione diverso nel portale di Site Recovery hello, spostare la replica di uno o più tooit macchine per il bilanciamento del carico manuale. In questo caso, i metadati di origine selezionato hello e computer di replica sono spostato toohello nuovo server di elaborazione. server di elaborazione Hello originale rimane connesso toohello vCenter server.

### <a name="monitor-hello-process-server"></a>Server di monitoraggio hello processo
Se un server di elaborazione è in uno stato critico in hello Dashboard di ripristino del sito verrà visualizzato un avviso di stato. È possibile fare clic sulla scheda eventi di hello stato tooopen hello e quindi eseguire il drill-down toospecific processi nella scheda processi hello.

### <a name="modify-hello-process-server-used-for-replication"></a>Modificare il server di elaborazione hello utilizzato per la replica
1. Aprire **Server** > **Server di configurazione**. Selezionare il server di configurazione e aprire **Dettagli server**.
2. Fare clic su **i server di elaborazione** > **Cambia Server di elaborazione** server toohello successivo si desidera toomodify.

    ![Modificare il server di elaborazione 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. In **Cambia Server di elaborazione** > **il Server di elaborazione di destinazione** selezionare hello nuovo server toouse desiderato e quindi selezionare le macchine virtuali di hello che si desidera tooreplicate toohello nuovo server. Fare clic su hello informazioni icona Avanti toohello nome del server per i dettagli di spazio libero e di memoria utilizzata. spazio medio Hello che sarà necessarie tooreplicate ogni macchina virtuale selezionata toohello nuovo server di elaborazione è visualizzato toohelp apportate caricare decisioni.

    ![Modificare il server di elaborazione 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Fare clic su hello segno di spunta toobegin replica toohello nuovo server di elaborazione. Si noti che se si rimuovono tutte le macchine virtuali da un server di elaborazione stato critico consigliabile non vengono più visualizzati un avviso critico nel dashboard di hello.

## <a name="third-party-software-notices-and-information"></a>Informazioni e comunicazioni sul software di terze parti
Do Not Translate or Localize

software Hello e in esecuzione nel firmware hello prodotto Microsoft o servizio è basato su o integra materiale proveniente dai hello progetti elencati sotto (collettivamente, "terze parti Code").  Microsoft è hello autore originale non di hello codice di terze parti.  copyright originale Hello e la licenza, in cui Microsoft ha ricevuto tale codice di terze parti, sono set specificato di seguito.

informazioni di Hello nella sezione si riferisce il codice di terze parti componenti dei progetti hello elencati di seguito. Such licenses and information are provided for informational purposes only.  Questo codice di terze parti è in corso tooyou relicensed da Microsoft in termini di hello prodotto o servizio Microsoft di licenza software Microsoft.  

informazioni di Hello nella sezione B sono per quanto riguarda i componenti del codice di terze parti che vengono eseguiti tooyou disponibili da Microsoft in condizioni di licenza originale hello.

è possibile trovare completo del file Hello in hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
