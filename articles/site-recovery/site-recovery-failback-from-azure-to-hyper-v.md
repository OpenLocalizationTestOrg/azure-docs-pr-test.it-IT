---
title: aaaFailback in Azure Site Recovery per le macchine virtuali Hyper-v | Documenti Microsoft
description: Azure Site Recovery coordina la replica di hello, failover e il ripristino delle macchine virtuali e server fisici. Scopri il failback da Data Center Azure tooon locale.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Failback in Site Recovery per macchine virtuali Hyper-V

In questo articolo viene descritto come macchine virtuali toofailback protetta da Site Recovery.

## <a name="prerequisites"></a>Prerequisiti
1. Verificare che server di Hyper-V server/hello VMM del sito primario è connesso.
2. È necessario aver completato **Commit** sulla macchina virtuale hello.

## <a name="why-is-there-no-button-called-failback"></a>Perché non è disponibile alcun pulsante denominato "Failback"?
Nel portale di hello, non sussiste alcun movimento esplicito definito failback. Il failback è un passaggio in cui si torna toohello primario di sito. Per definizione, il failover è quando si failover delle macchine virtuali hello da primary(on-premises) sito toorecovery (Azure) e il failback non è failover delle macchine virtuali hello da recovery eseguire tooprimary.

Quando si avvia un failover, il pannello hello informa direzione hello del processo di hello. Se la direzione hello da Azure tooOn locale, è un failback.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Perché è disponibile solo un toofailback movimenti failover pianificato?
Azure è un ambiente a elevata disponibilità e le macchine virtuali saranno sempre disponibili. Il failback è un'attività pianificata, è necessario scegliere un breve tempo di inattività tootake in modo che i carichi di lavoro hello può iniziare a eseguire di nuovo in locale. Non è prevista alcuna perdita di dati. Di conseguenza cui è disponibile solo un movimento del failover pianificato, che verrà disattivare hello macchine virtuali in Azure, scaricare le modifiche più recenti di hello e verificare che sia presente alcuna perdita di dati.

## <a name="initiate-failback"></a>Avviare il failback
Dopo il failover dal percorso primario toosecondary hello, le macchine virtuali replicate non sono protetti da un ripristino del sito e posizione secondaria hello ora funge da percorso attivo hello. Seguire queste procedure toofail toohello indietro sito primario originale. Questa procedura viene descritto come toorun un failover pianificato per il ripristino di un piano. In alternativa è possibile eseguire failover hello per una singola macchina virtuale in hello **macchine virtuali** scheda.

1. Selezionare **Piani di ripristino** > *nome_pianodiripristino*. Fare clic su **Failover** > **Planned Failover**.
2. In hello * * conferma Failover pianificato * * pagina, scegliere i percorsi di origine e destinazione hello. Si noti la direzione di failover hello. Se il failover dal database primario hello lavorato come previsto e tutte le macchine virtuali sono in percorso secondario di hello che questo è solo informativo.
3. Se si esegue il failback da Azure, selezionare le impostazioni in **Sincronizzazione dati**:

   * **Sincronizza i dati prima del failover (sincronizza solo modifiche differenziali)**: questa opzione riduce al minimo i tempi di inattività delle macchine virtuali poiché le sincronizza senza arrestarle. Hello seguenti:
     * Fase 1: Crea snapshot della macchina virtuale hello in Azure e li copia toohello host di Hyper-V locale. macchina Hello continua l'esecuzione in Azure.
     * Fase 2: Arresta macchina virtuale hello in Azure in modo da non esiste alcuna nuova modifica. set di modifiche delta finale Hello sono trasferiti toohello ai server locali e avvio della macchina virtuale locale hello.

    - **Sincronizza i dati durante il failover (download completo)**: usare questa opzione se Azure è in esecuzione da molto tempo. Questa opzione è più veloce perché è previsto che la maggior parte del disco hello è stato modificato e non vogliamo ora toospend nel calcolo del checksum. Esegue il download del disco hello. È inoltre utile quando macchina virtuale di hello locale è stato eliminato.

    >[!NOTE]
    >Si consiglia di usare questa opzione se si è in esecuzione Azure per un periodo di tempo (un mese o più) o macchina virtuale di hello locale è stata eliminata. Questa opzione non esegue alcun calcolo del checksum.
    >
    >




4. Se la crittografia dei dati è abilitato per il cloud di hello, in **chiave di crittografia** certificato selezionare hello emesso quando è abilitata la crittografia dei dati durante l'installazione del Provider nel server VMM hello.
5. Avviare il failover hello. È possibile controllare lo stato di avanzamento di hello failover nella hello **processi** scheda.
6. Se si selezionano i dati di hello opzione toosynchronize hello prima del failover hello, una volta hello iniziale è stata completata la sincronizzazione dei dati e si è pronti tooshut hello di macchine virtuali in Azure, fare clic su **processi** nome del processo di failover pianificato **Completare Failover**. Questo chiude hello Azure macchina, hello trasferimenti più recente diventa macchina virtuale di toohello locale e avvia hello VM locale.
7. È ora possibile accedere in hello toovalidate di macchina virtuale è disponibile come previsto.
8. macchina virtuale Hello è in uno stato in sospeso di commit. Fare clic su **Commit** toocommit hello failover.
9. Ora in ordine fare clic su toocomplete hello failback **inversa replicare** toostart protezione hello di macchina virtuale nel sito primario di hello.

## <a name="failback-tooan-alternate-location"></a>Percorso alternativo tooan di failback
Se è già distribuito protezione tra un [sito Hyper-V e Azure](site-recovery-hyper-v-site-to-azure.md) è tooability toofailback dal percorso locale alternativo tooan Azure. Ciò è utile se occorre tooset nuovo hardware locale. Di seguito viene indicato come procedere.

1. Se si imposta il nuovo hardware hello il ruolo Hyper-V nel server di hello installare Windows Server 2012 R2.
2. Creare un commutatore di rete virtuale con stesso nome che si verifica nel server originale hello hello.
3. Selezionare **elementi protetti** -> **gruppo protezione dati**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> desiderato toofail indietro e selezionare **pianificato Failover**.
4. Fare clic su **Conferma failover pianificato** select **Crea macchina virtuale locale, se non esiste**.
5. In **nome Host** selezionare hello di nuovo i server host Hyper-V in cui si desidera macchina virtuale di tooplace hello.
6. Sincronizzazione dei dati, è consigliabile l'opzione di hello **sincronizzare i dati di hello prima del failover hello**. Questa opzione riduce al minimo i tempi di inattività per le macchine virtuali senza arrestarle. Hello seguenti:

   * Fase 1: Crea snapshot della macchina virtuale hello in Azure e li copia toohello host di Hyper-V locale. macchina Hello continua l'esecuzione in Azure.
   * Fase 2: Arresta macchina virtuale hello in Azure in modo da non esiste alcuna nuova modifica. Hello finale insieme di modifiche vengono trasferite toohello ai server locali e avvio della macchina virtuale locale hello.
7. Fare clic su hello segno di spunta toobegin hello failover (failback).
8. Al termine della sincronizzazione iniziale di hello e si è pronti tooshut verso il basso hello di macchina virtuale in Azure, fare clic su **processi** > <planned failover job> > **completare il Failover**. Questo chiude hello Azure macchina, toohello modifiche più recente di trasferimenti hello macchina virtuale locale e lo avvia.
9. È possibile accedere tooverify di macchina virtuale locale hello che funzionino come previsto. Quindi fare clic su **Commit** toofinish hello failover.
10. Fare clic su **inversa replicare** toostart protezione macchina virtuale di hello in locale.

    > [!NOTE]
    > Se si annulla il processo di failback hello mentre è in fase di sincronizzazione dei dati, hello locale VM sarà in uno stato danneggiato. In questo modo la sincronizzazione dei dati copia i dati più recenti di hello da dischi di dati locale toohello dischi macchina virtuale di Azure e fino al completamento della sincronizzazione hello, i dati su disco hello potrebbero non essere in uno stato coerente. Se dopo la sincronizzazione dei dati viene annullata, viene avviato hello macchina virtuale locale, potrebbe non avviato. Attivare nuovamente failover toocomplete hello la sincronizzazione dei dati.
    >
    >



## <a name="next-steps"></a>Passaggi successivi

Dopo aver completato il processo di failback hello, **Commit** macchina virtuale hello. Commit Elimina hello macchina virtuale di Azure e i relativi dischi e prepara hello VM toobe nuovamente protetti.

Dopo aver **Commit**, è possibile avviare hello *inversa replicare*. Verrà avviata impedire la macchina virtuale hello tooAzure indietro locale. Si noti che in modo da consentire solo le modifiche replicate hello poiché hello macchina virtuale è stata disattivata in Azure e pertanto invia differenziale cambia solo.
