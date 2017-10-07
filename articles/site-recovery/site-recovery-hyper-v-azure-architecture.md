---
title: aaaHow funziona Hyper-V replica tooAzure in Site Recovery? | Microsoft Docs
description: Questo articolo offre una panoramica del funzionamento della replica Hyper-V in Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Come funziona tooAzure replica Hyper-V?

Leggere questa architettura di articolo toounderstand hello e flussi di lavoro per Hyper-V replica tooAzure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

È possibile replicare hello tooAzure seguenti:
- **Hyper-V con VMM**: macchine virtuali presenti negli host Hyper-V locali gestiti nei cloud System Center Virtual Machine Manager (VMM). Gli host possono eseguire qualsiasi [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). È possibile replicare macchine virtuali Hyper-V che eseguono qualsiasi sistema operativo guest [supportato da Hyper-V e Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Hyper-V senza VMM**: macchine virtuali locali presenti negli host Hyper-V che non sono gestiti nei cloud VMM. Gli host possono eseguire qualsiasi di hello [i sistemi operativi supportati](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). È possibile replicare macchine virtuali Hyper-V che eseguono qualsiasi sistema operativo guest [supportato da Hyper-V e Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Componenti dell'architettura

**Area** | **Componente** | **Dettagli**
--- | --- | ---
**Azzurro** | In Azure sono necessari un account Microsoft Azure, un account di archiviazione di Azure e una rete di Azure. | La risorsa di archiviazione e la rete possono essere account basati su Resource Manager o classici.<br/><br/> Dati replicati vengono archiviati nell'account di archiviazione hello e macchine virtuali di Azure vengono create con i dati replicato hello quando si verifica il failover da sito locale.<br/><br/> Hello macchine virtuali di Azure connettersi toohello rete virtuale di Azure quando vengono creati.
**Server VMM** | Host Hyper-V situati in cloud VMM | Se l'host Hyper-V vengono gestite nei cloud VMM, si registra il server VMM hello in hello che insieme di credenziali di servizi di ripristino.<br/><br/> Nel server VMM hello installare replica tooorchestrate di Provider di Site Recovery hello con Azure.<br/><br/> È necessario logico e le reti VM configurate tooconfigure il mapping di rete. Una rete VM deve essere collegato tooa la rete logica associata a cloud hello.
**Host Hyper-V** | I server Hyper-V possono essere distribuiti con o senza server VMM. | Se non è presente alcun server VMM, hello Provider di Site Recovery è installato sulla replica di tooorchestrate hello host con il ripristino del sito su hello internet. Se è presente un server VMM, hello Provider sia installato su di esso e non nell'host di hello.<br/><br/> agente di servizi di ripristino Hello viene installato nella replica dei dati toohandle hello host.<br/><br/> Le comunicazioni da hello Provider e agente hello sono protetto e crittografato. I dati replicati nell'archiviazione di Azure vengono anche crittografati.
**VM Hyper-V** | È necessario uno o più macchine virtuali nel server host Hyper-V di hello. | Non è necessario tooexplicitly installati nelle macchine virtuali

## <a name="deployment-steps"></a>Passaggi di distribuzione

1. **Azure**: impostare hello componenti di Azure. È consigliabile configurare gli account di archiviazione e di rete prima di iniziare la distribuzione di Site Recovery.
2. **Insieme di credenziali**: si crea un insieme di credenziali di Servizi di ripristino per Site Recovery e si configurano le impostazioni dell'insieme di credenziali, incluse la configurazione delle impostazioni di origine e di destinazione, l'impostazione di un criterio di replica e l'abilitazione della replica.
3. **Origine e destinazione**:
    - **Host Hyper-V nei cloud VMM**: come parte della definizione delle impostazioni di origine, scaricare e installare hello Provider di Azure Site Recovery nel server VMM hello e agente di servizi di ripristino di Azure hello in ogni host Hyper-V. origine Hello è hello VMM server. destinazione Hello è Azure.
    - Host Hyper-V senza VMM: quando si specificano le impostazioni di origine, scaricare e installare hello Provider e agente in ogni host Hyper-V. Durante la distribuzione raccogliere host hello in un sito Hyper-V e specificare il sito come origine di hello. destinazione Hello è Azure.

    ![VMM/Hyper-V replica tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![tooAzure di replica Hyper-V del sito](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Criteri di replica**: si crea un criterio di replica per il sito Hyper-V hello o cloud VMM. criteri di Hello sono macchine virtuali tooall applicato presenti negli host nel sito di hello o cloud.
5. **Abilitazione della replica**: si abilita la replica per le macchine virtuali Hyper-V. Viene eseguita la replica iniziale in base alle impostazioni di criteri di replica hello. Vengono rilevate le modifiche ai dati e la replica di tooAzure le modifiche delta inizia dopo il completamento della replica iniziale hello. Le modifiche rilevate per un elemento vengono salvate in un file HRL.
6. **Failover di test**: eseguire un toomake di failover di test che tutto funzioni come previsto.

Altre informazioni sulla distribuzione:
- [Introduzione a macchina virtuale Hyper-V replica tooAzure - con VMM](site-recovery-vmm-to-azure.md)
- [Introduzione a macchina virtuale Hyper-V replica tooAzure - senza VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Flusso di lavoro di replica Hyper-V

### <a name="enable-protection"></a>Abilitare la protezione

1. Dopo aver abilitato la protezione per una macchina virtuale Hyper-V, in hello portale di Azure o in locale, hello **abilitare la protezione** viene avviato.
2. Hello processo controlla tale macchina hello è conforme ai prerequisiti, prima di richiamare hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la replica con le impostazioni di hello configurati.
3. Hello in cui inizia la replica iniziale richiamando hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) metodo tooinitialize una replica completa di macchina virtuale e tooAzure dischi virtuali della macchina virtuale di trasmissione hello.
4. È possibile monitorare il processo di hello in hello **processi** scheda.      ![Elenco dei processi](media/site-recovery-hyper-v-azure-architecture/image1.png)![Abilitare protezione in dettaglio](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Replica iniziale

1. Quando viene attivata la replica iniziale, viene acquisito uno [snapshot della VM Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. I dischi rigidi virtuali vengono replicate uno alla volta fino a quando non si tooAzure copiati tutti. Potrebbe richiedere alcuni minuti, a seconda delle dimensioni delle macchine Virtuali, hello e larghezza di banda di rete. toooptimize l'utilizzo della rete, vedere [come toomanage locale dell'utilizzo della larghezza di banda di rete protezione tooAzure](https://support.microsoft.com/kb/3056159).
3. Se le modifiche si verificano durante la replica iniziale è in corso, hello Tracker di replica Hyper-V Replica tiene traccia delle modifiche come i log di replica Hyper-V (hrl). Questi file si trovano in hello stessa cartella dei dischi hello. Ogni disco è un file di hrl associata che verrà inviato toosecondary archiviazione.
4. file di snapshot e di log Hello risorse disco mentre la replica iniziale è in corso.
5. Al termine, la replica iniziale hello snapshot di macchina virtuale hello viene eliminato. Le modifiche delta dei dischi nel registro hello sono disco padre toohello sincronizzato e sottoposto a merge.


### <a name="finalize-protection"></a>Finalizzare la protezione

1. Al termine della replica iniziale di hello, hello **Finalizza la protezione nella macchina virtuale hello** processo Configura rete e altre impostazioni di post-replica, in modo da macchina virtuale hello è protetta.
    ![Processo Finalizza la protezione](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Se si esegue la replica tooAzure, si potrebbe essere necessario impostazioni hello tootweak per la macchina virtuale hello in modo che sia pronta per il failover. A questo punto è possibile eseguire un toocheck di failover di test che funzionino come previsto.

### <a name="delta-replication"></a>Replica dei dati

1. Dopo la replica iniziale hello, delta inizia la sincronizzazione, in base alle impostazioni di replica.
2. Individuazione di replica Hyper-V Replica Hello tiene traccia il disco rigido virtuale di hello modifiche tooa come file hrl. A ogni disco configurato per la replica è associato un file con estensione hrl. Questo log viene inviato l'account di archiviazione del cliente toohello dopo il completamento della replica iniziale. Quando un log è in transito tooAzure, le modifiche di hello nel disco primario hello vengono rilevate in un altro file di log, in hello stessa directory.
3. Durante la replica iniziale e differenziali, è possibile monitorare Ciao VM hello visualizzazione della macchina virtuale. [Altre informazioni](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)  

### <a name="replication-synchronization"></a>Sincronizzazione della replica

1. Se la replica differenziale non riesce e una replica completa risulta costosa a livello di larghezza di banda o di tempo richiesto, la macchina virtuale verrà contrassegnata per la risincronizzazione. Ad esempio, se i file hrl hello raggiungono 50% delle dimensioni del disco hello, quindi hello VM verrà contrassegnata per la risincronizzazione.
2.  La risincronizzazione riduce la quantità di hello dei dati inviati dal calcolo i checksum di macchine virtuali di origine e destinazione di hello e l'invio solo i dati delta hello. La risincronizzazione usa un algoritmo di suddivisione in blocchi a blocchi fissi che suddivide appunto i file di origine e di destinazione in blocchi fissi. I valori di checksum per ogni blocco vengono generati e quindi confrontata toodetermine che si blocca dalla destinazione di hello origine necessario toobe toohello applicato.
3. Al termine della risincronizzazione, dovrebbe riprendere la normale replica differenziale. Per impostazione predefinita la risincronizzazione viene pianificata toorun automaticamente fuori dall'orario di ufficio, ma è possibile risincronizzare una macchina virtuale manualmente. Ad esempio, se si verifica un'interruzione di rete o un'altra interruzione, è possibile riprendere la risincronizzazione. toodo, hello seleziona macchina virtuale nel portale di hello > **risincronizzare**.

    ![Risincronizzazione manuale](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Tentativi

Se si verifica un errore di replica, per impostazione predefinita viene effettuato un nuovo tentativo. Tale logica può essere classificata nelle due categorie seguenti:

**Categoria** | **Dettagli**
--- | ---
**Errori irreversibili** | Non viene eseguito alcun nuovo tentativo. Lo stato della macchina virtuale sarà **Critico** e sarà necessario l'intervento di un amministratore. Esempi di questi errori: interrotta la catena di disco rigido virtuale. Stato non valido per la replica hello VM; Errori di autenticazione di rete: errori di autorizzazione. Macchina virtuale non trovati errori (per i server Hyper-V autonomi)
**Errori reversibili** | Tentativi vengono eseguiti ogni intervallo di replica, utilizzando un backoff esponenziale che aumenta l'intervallo tra tentativi hello dall'inizio di hello del primo tentativo di hello da 1, 2, 4, 8 e 10 minuti. Se l'errore persiste, viene eseguito un nuovo tentativo ogni 30 minuti. Alcuni esempi: errori di rete, errori di spazio su disco insufficiente, condizioni di memoria insufficiente. |

## <a name="protection-and-recovery-lifecycle"></a>Ciclo di vita di protezione e ripristino

![flusso di lavoro](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Passaggi successivi

- [Verificare i prerequisiti di distribuzione](site-recovery-prereq.md)
- Risolvere gli eventuali problemi tramite:
    - [Monitorare e risolvere i problemi di protezione](site-recovery-monitoring-and-troubleshooting.md)
    - [Contattare il supporto Microsoft](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Errori comuni e soluzioni](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
