---
title: un failover di test per il server fisico replica tooAzure con Azure Site Recovery aaaRun | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello che è necessario per l'esecuzione di un failover di test [replica tooAzure utilizzando il servizio di Azure Site Recovery hello server fisici."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f8ed5ce585c5574be3018ce15339c4fd3b527eaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-tooazure"></a>Passaggio 11: Eseguire un failover di test dei server fisici tooAzure

In questo articolo viene descritto come toorun un failover di test da on-premise tooAzure server fisici, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

Prima di eseguire un failover di test, che è consigliabile verificare le proprietà del server hello e apportare le modifiche è necessario. è possibile accedere a proprietà della macchina virtuale hello in **gli elementi replicati**. Hello **Essentials** pannello mostra le informazioni sulle impostazioni della macchina e lo stato.

## <a name="managed-disk-considerations"></a>Considerazioni su Managed Disks

[Dischi gestiti](../virtual-machines/windows/managed-disks-overview.md) semplificano la gestione disco per le macchine virtuali di Azure, mediante la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. 

- Quando si abilita la protezione per un server, i dati di macchina virtuale vengono replicati tooa account di archiviazione. Dischi gestiti vengono creati e collegati toohello macchina virtuale solo quando si verifica il failover.
- Dischi gestiti possono essere creati solo per le macchine virtuali di Azure distribuiti tramite il modello di gestione risorse hello.  
- Quando questa impostazione è abilitata, possono essere selezionati solo i set di disponibilità in gruppi di risorse con l'impostazione **Usa il servizio Managed Disks** abilitata. Le macchine virtuali con dischi gestiti devono essere in set di disponibilità con **utilizzare dischi gestiti** impostare troppo**Sì**. Se l'impostazione di hello non è abilitata per le macchine virtuali, è possibile selezionare solo set di disponibilità in gruppi di risorse senza dischi gestiti abilitati.
- [Altre informazioni](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) su Managed Disks e set di disponibilità.
- Se l'account di archiviazione hello usato per la replica è stata crittografata con la crittografia del servizio di archiviazione, è Impossibile creare dischi gestiti durante il failover. In questo caso di non abilitare l'utilizzo di dischi gestiti, o disabilitare la protezione per hello macchina virtuale e riabilitarla toouse un account di archiviazione che non sia abilitata la crittografia. [Altre informazioni](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)


## <a name="network-considerations"></a>Considerazioni sulla rete

È possibile impostare l'indirizzo IP di destinazione hello per una macchina virtuale di Azure creata dopo il failover.

- Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP.
- Se si imposta un indirizzo che non è disponibile al momento del failover, il failover non riesce.
- Hello stesso indirizzo IP di destinazione è utilizzabile per il failover di test, se è disponibile in rete di failover di test hello hello indirizzo.
- numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello:

     - Se il numero di hello di schede di rete nel computer di origine hello hello uguale o minore, hello numero di schede consentite per le dimensioni del computer di destinazione hello, allora destinazione hello avrà hello origine hello stesso numero di schede.
     - Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per le dimensioni di destinazione hello, dimensione massima dei hello destinazione verrà utilizzato.
     - Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.     
   - Se più schede di rete nella macchina virtuale hello verranno tutti connettono toohello stessa rete.
   - Se macchina virtuale hello ha più schede di rete hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.
 - [Altre informazioni](vmware-walkthrough-network.md) sugli indirizzi IP.



## <a name="view-and-modify-vm-settings"></a>Visualizzare e modificare le impostazioni delle VM

È consigliabile verificare le proprietà di hello hello del server di origine prima di eseguire un failover.

1. In **elementi protetti**, fare clic su **elementi replicati**, fare clic su computer hello.
2. In hello **elemento replicato** riquadro, è possibile visualizzare un riepilogo delle informazioni sul computer lo stato di integrità e punti di ripristino disponibile più recenti di hello. Fare clic su **proprietà** tooview ulteriori informazioni, vedere.
3. In **Calcolo e rete** è possibile:
    - Modificare il nome di macchina virtuale di Azure hello. nome Hello deve soddisfare [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Specificare un [gruppo di risorse] successivo al failover.
    - Specificare una dimensione di destinazione per hello macchina virtuale di Azure
    - Selezionare un [set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md).
    - Specificare se toouse [dischi gestiti](#managed-disk-considerations). Selezionare **Sì**, se si desidera tooattach dischi gestiti tooyour computer tooAzure di migrazione.
    - Visualizzare o modificare le impostazioni di rete, inclusi hello/subnet della rete in cui hello macchina virtuale di Azure sarà posizionato dopo il failover e indirizzo IP hello che verrà assegnato tooit.
4. In **dischi**, è possibile visualizzare informazioni sul sistema operativo hello e dischi dati in hello macchina virtuale.

## <a name="run-a-test-failover"></a>Eseguire un failover di test

Dopo aver configurato tutti gli elementi, eseguire una toomake di failover di test che tutto funzioni come previsto.

- Se si desidera tooconnect tooAzure macchine virtuali tramite RDP dopo il failover, [preparare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully toocopy di Active Directory e DNS è necessario nell'ambiente di test. [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations)
 - Per informazioni complete sul failover di test, leggere [questo articolo](site-recovery-test-failover-to-azure.md).
- Ottenere una rapida panoramica video prima di iniziare:

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

Eseguire quindi un failover:

1. toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su computer hello > **+ Test Failover** icona.

    ![Failover di test](./media/physical-walkthrough-test-failover/test-failover.png)

2. toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).  

3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure saranno connesse dopo il failover viene eseguito.

4. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello macchina tooopen le relative proprietà o in hello **Failover di Test** processo nel nome dell'insieme di credenziali > **impostazioni** > **processi**  >  **i processi di ripristino del sito**.

5. Al termine del processo di failover di hello, è necessario inoltre replica hello toosee in grado di macchina virtuale di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.

6. Se sono preparati per le connessioni dopo il failover, dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.

### <a name="delete-test-failover-vms"></a>Eliminare le VM del failover di test

1. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello o computer.
2. In **note**, registrare e salvare eventuali commenti associati hello test failover.
3. azione di pulizia Hello Elimina macchine virtuali di Azure che sono stati creati durante il failover di test.

## <a name="summary"></a>Riepilogo

Se il failover di test hello è stato completato correttamente, i server fisici vengono replicate e aver verificato che possono eseguire il failover tooAzure. È ora possibile eseguire i failover in base ai requisiti aziendali. 

Tenere presente che non è possibile eseguire attualmente dallo stesso server fisico tooa Azure. È necessario eseguire il backup di VM VMware tooa toofail. Il che richiede un'infrastruttura VMware in locale nel back toofail ordine. [Altre informazioni](site-recovery-failback-azure-to-vmware.md) sulle tooVMware macchine virtuali di Azure backup con esito negativo.


## <a name="next-steps"></a>Passaggi successivi

- [Eseguire i failover](site-recovery-failover.md) in base alle esigenze.
