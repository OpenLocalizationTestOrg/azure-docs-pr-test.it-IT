---
title: aaaHow funziona Hyper-V replica tooAzure in Azure Site Recovery? | Microsoft Docs
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata quando la replica locale tooAzure macchine virtuali Hyper-V con il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 3b64156307f37764a8315dec68cf297acf279530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work-in-site-recovery"></a>Come funziona tooAzure replica Hyper-V in Site Recovery?


Questo articolo vengono descritti i componenti di hello e processi per la replica locale macchine virtuali Hyper-V, tooAzure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.

Site Recovery consente di replicare macchine virtuali Hyper-V in cluster Hyper-V e host autonomi gestiti con o senza System Center Virtual Machine Manager (VMM).

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componenti dell'architettura

Non è coinvolto un numero di componenti per la replica delle macchine virtuali Hyper-V tooAzure.

**Componente** | **Posizione** | **Dettagli**
--- | --- | ---
**Azzurro** | In Azure sono necessari un account Microsoft Azure, un account di archiviazione di Azure e una rete di Azure. | Dati replicati vengono archiviati nell'account di archiviazione hello e macchine virtuali di Azure vengono create con i dati replicato hello quando si verifica il failover da sito locale.<br/><br/> Hello macchine virtuali di Azure connettersi toohello rete virtuale di Azure quando vengono creati.
**Server VMM** | Gli host Hyper-V si trovano in cloud VMM. | Se l'host Hyper-V vengono gestite nei cloud VMM, si registra il server VMM hello in hello che insieme di credenziali di servizi di ripristino.<br/><br/> Nel server VMM hello installare replica tooorchestrate di Provider di Site Recovery hello con Azure.<br/><br/> È necessario logico e le reti VM configurate tooconfigure il mapping di rete. Una rete VM deve essere collegato tooa la rete logica associata a cloud hello.
**Host Hyper-V** | Gli host e i cluster Hyper-V possono essere distribuiti con o senza server VMM. | Se non è presente alcun server VMM, hello Provider di Site Recovery è installato sulla replica di tooorchestrate hello host con il ripristino del sito su hello internet. Se è presente un server VMM, hello Provider sia installato su di esso e non nell'host di hello.<br/><br/> agente di servizi di ripristino Hello viene installato nella replica dei dati toohandle hello host.<br/><br/> Le comunicazioni da hello Provider e agente hello sono protetto e crittografato. I dati replicati nell'archiviazione di Azure vengono anche crittografati.
**VM Hyper-V** | È necessaria una o più macchine virtuali in esecuzione nel server host Hyper-V. | Non è necessario tooexplicitly installati nelle macchine virtuali.

Informazioni sui prerequisiti per la distribuzione hello e requisiti per ognuno di questi componenti in hello [matrice del supporto](site-recovery-support-matrix-to-azure.md).

**Figura 1: Replica di tooAzure siti Hyper-V**

![Componenti](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 2: Replica tooAzure di cloud di Hyper-V in VMM**

![Componenti](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Processo di replica

**Figura 3: Processo di replica e il ripristino per Hyper-V replica tooAzure**

![flusso di lavoro](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Abilitare la protezione

1. Dopo aver abilitato la protezione per una macchina virtuale Hyper-V, in hello portale di Azure o in locale, hello **abilitare la protezione** viene avviato.
2. Hello processo controlla tale macchina hello è conforme ai prerequisiti, prima di richiamare hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la replica con le impostazioni di hello configurati.
3. Hello in cui inizia la replica iniziale richiamando hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) metodo tooinitialize una replica completa di macchina virtuale e tooAzure dischi virtuali della macchina virtuale di trasmissione hello.
4. È possibile monitorare il processo di hello in hello **processi** scheda.      ![Elenco dei processi](media/site-recovery-hyper-v-azure-architecture/image1.png)![Abilitare protezione in dettaglio](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>La replica dei dati iniziale hello

1. Quando viene attivata la replica iniziale, viene acquisito uno [snapshot della VM Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. I dischi rigidi virtuali vengono replicate uno alla volta fino a quando non si tooAzure copiati tutti. Potrebbe richiedere alcuni minuti, a seconda delle dimensioni delle macchine Virtuali, hello e larghezza di banda di rete. toooptimize l'utilizzo della rete, vedere [come toomanage locale dell'utilizzo della larghezza di banda di rete protezione tooAzure](https://support.microsoft.com/kb/3056159).
3. Se le modifiche si verificano durante la replica iniziale è in corso, hello Tracker di replica Hyper-V Replica tiene traccia delle modifiche come i log di replica Hyper-V (hrl). Questi file si trovano in hello stessa cartella dei dischi hello. Ogni disco è un file di hrl associata che verrà inviato toosecondary archiviazione.
4. file di snapshot e di log Hello risorse disco mentre la replica iniziale è in corso.
5. Al termine, la replica iniziale hello snapshot di macchina virtuale hello viene eliminato. Le modifiche delta dei dischi nel registro hello sono disco padre toohello sincronizzato e sottoposto a merge.


### <a name="finalize-protection"></a>Finalizzare la protezione

1. Al termine della replica iniziale di hello, hello **Finalizza la protezione nella macchina virtuale hello** processo Configura rete e altre impostazioni di post-replica, in modo da macchina virtuale hello è protetta.
    ![Processo Finalizza la protezione](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Se si esegue la replica tooAzure, si potrebbe essere necessario impostazioni hello tootweak per la macchina virtuale hello in modo che sia pronta per il failover. A questo punto è possibile eseguire un toocheck di failover di test che funzionino come previsto.

### <a name="replicate-hello-delta"></a>La replica differenziale hello

1. Dopo la replica iniziale hello, delta inizia la sincronizzazione, in base alle impostazioni di replica.
2. Individuazione di replica Hyper-V Replica Hello tiene traccia il disco rigido virtuale di hello modifiche tooa come file hrl. A ogni disco configurato per la replica è associato un file con estensione hrl. Questo log viene inviato l'account di archiviazione del cliente toohello dopo il completamento della replica iniziale. Quando un log è in transito tooAzure, le modifiche di hello nel disco primario hello vengono rilevate in un altro file di log, in hello stessa directory.
3. Durante la replica iniziale e differenziali, è possibile monitorare Ciao VM hello visualizzazione della macchina virtuale. [Altre informazioni](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)  

### <a name="synchronize-replication"></a>Sincronizzare la replica

1. Se la replica differenziale non riesce e una replica completa risulta costosa a livello di larghezza di banda o di tempo richiesto, la macchina virtuale verrà contrassegnata per la risincronizzazione. Ad esempio, se i file hrl hello raggiungono 50% delle dimensioni del disco hello, quindi hello VM verrà contrassegnata per la risincronizzazione.
2.  La risincronizzazione riduce la quantità di hello dei dati inviati dal calcolo i checksum di macchine virtuali di origine e destinazione di hello e l'invio solo i dati delta hello. La risincronizzazione usa un algoritmo di suddivisione in blocchi a blocchi fissi che suddivide appunto i file di origine e di destinazione in blocchi fissi. I valori di checksum per ogni blocco vengono generati e quindi confrontata toodetermine che si blocca dalla destinazione di hello origine necessario toobe toohello applicato.
3. Al termine della risincronizzazione, dovrebbe riprendere la normale replica differenziale. Per impostazione predefinita la risincronizzazione viene pianificata toorun automaticamente fuori dall'orario di ufficio, ma è possibile risincronizzare una macchina virtuale manualmente. Ad esempio, se si verifica un'interruzione di rete o un'altra interruzione, è possibile riprendere la risincronizzazione. toodo, hello seleziona macchina virtuale nel portale di hello > **risincronizzare**.

    ![Risincronizzazione manuale](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a>Logica di retry

Se si verifica un errore di replica, per impostazione predefinita viene effettuato un nuovo tentativo. Tale logica può essere classificata nelle due categorie seguenti:

**Categoria** | **Dettagli**
--- | ---
**Errori irreversibili** | Non viene eseguito alcun nuovo tentativo. Lo stato della macchina virtuale sarà **Critico** e sarà necessario l'intervento di un amministratore. Esempi di questi errori: interrotta la catena di disco rigido virtuale. Stato non valido per la replica hello VM; Errori di autenticazione di rete: errori di autorizzazione. Macchina virtuale non trovati errori (per i server Hyper-V autonomi)
**Errori reversibili** | Tentativi vengono eseguiti ogni intervallo di replica, utilizzando un backoff esponenziale che aumenta l'intervallo tra tentativi hello dall'inizio di hello del primo tentativo di hello da 1, 2, 4, 8 e 10 minuti. Se l'errore persiste, viene eseguito un nuovo tentativo ogni 30 minuti. Alcuni esempi: errori di rete, errori di spazio su disco insufficiente, condizioni di memoria insufficiente. |



## <a name="failover-and-failback-process"></a>Processo di failover e failback

1. È possibile eseguire un pianificato o non pianificato [failover](site-recovery-failover.md) da tooAzure macchine virtuali Hyper-V locale. Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.
4. Dopo aver eseguito il failover hello, si dovrebbe essere hello toosee in grado di creare macchine virtuali di replica in Azure. Se necessario, è possibile assegnare un toohello di indirizzo IP pubblico macchina virtuale.
5. È quindi eseguire il commit hello failover toostart l'accesso a carico di lavoro hello dalla replica hello macchina virtuale di Azure.
6. Quando il sito locale primario è di nuovo disponibile, è possibile [effettuare il failback](site-recovery-failback-from-azure-to-hyper-v.md). Avviare un failover pianificato da Azure toohello primario di sito. Per un failover pianificato, che è possibile selezionare toofailback toohello stessa macchina virtuale o tooan percorso alternativo e sincronizzare le modifiche tra Azure e locali, tooensure senza perdita di dati. Creazione di macchine virtuali in locale, si esegue il commit hello failover.




## <a name="next-steps"></a>Passaggi successivi

Hello revisione [matrice del supporto](site-recovery-support-matrix-to-azure.md)
