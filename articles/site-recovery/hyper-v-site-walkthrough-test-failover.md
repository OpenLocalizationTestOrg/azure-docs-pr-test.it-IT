---
title: un failover di test per Hyper-V replica (senza System Center VMM) tooAzure aaaRun | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello che è necessario per l'esecuzione di un failover di test per le macchine virtuali Hyper-V replica tooAzure utilizzando il servizio di Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>Passaggio 11: Eseguire un failover di test per Hyper-V replica tooAzure

In questo articolo viene descritto come toorun un failover di test dal locale macchine virtuali Hyper-V (non gestite da System Center VMM) tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Prima di iniziare

Prima di eseguire un failover di test, che è consigliabile verificare le proprietà della VM hello e apportare le modifiche è necessario. è possibile accedere a proprietà della macchina virtuale hello in **gli elementi replicati**. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.

## <a name="managed-disk-considerations"></a>Considerazioni su Managed Disks

[Dischi gestiti](../virtual-machines/windows/managed-disks-overview.md) semplificano la gestione disco per le macchine virtuali di Azure, mediante la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. 

- Dischi gestiti vengono creati e collegati toohello macchina virtuale solo quando si verifica un failover tooAzure. Quando si abilita la protezione, i dati da macchine virtuali locali vengono replicati toostorage account.
- Dischi gestiti possono essere creati solo per le macchine virtuali che vengono distribuite tramite il modello di distribuzione Gestione risorse di hello.
- Il failback da Azure tooan locale ambiente Hyper-V non è attualmente supportato per i computer con dischi gestiti. È necessario impostare solo **utilizzare dischi gestiti** troppo**Sì** se si sta eseguendo una migrazione solo (failover tooAzure senza il failback)
- Quando questa impostazione è abilitata, possono essere selezionati solo i set di disponibilità in gruppi di risorse con l'impostazione **Usa il servizio Managed Disks** abilitata. Le macchine virtuali con dischi gestiti devono essere in set di disponibilità con **utilizzare dischi gestiti** impostare troppo**Sì**. Se l'impostazione di hello non è abilitata per le macchine virtuali, è possibile selezionare solo set di disponibilità in gruppi di risorse senza dischi gestiti abilitati. [Altre informazioni](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)
- - Se l'account di archiviazione hello usato per la replica è stata crittografata con la crittografia del servizio di archiviazione, è Impossibile creare dischi gestiti durante il failover. In questo caso di non abilitare l'utilizzo di dischi gestiti, o disabilitare la protezione per hello macchina virtuale e riabilitarla toouse un account di archiviazione che non sia abilitata la crittografia. [Altre informazioni](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)

 
## <a name="network-considerations"></a>Considerazioni sulla rete
    
- È possibile impostare l'indirizzo IP di hello destinazione toobe usato per hello Azure VM dopo il failover. Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP. Se si imposta un indirizzo che non è disponibile in caso di failover, hello failover avrà esito negativo. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.
- numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:
    - Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
    - Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
    - Se, ad esempio un computer di origine ha due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.     
- Se hello macchina virtuale dispone di più schede di rete verranno tutti connettono toohello stessa rete.
- Se macchina virtuale hello ha più schede di rete hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.


## <a name="view-and-manage-vm-settings"></a>Visualizzare e gestire le impostazioni delle VM

È consigliabile verificare le proprietà di hello hello computer di origine prima di eseguire un failover.

1. In **elementi protetti**, fare clic su **elementi replicati**, fare clic su hello macchina virtuale.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. In hello **elemento replicato** riquadro, è possibile visualizzare un riepilogo delle informazioni di macchina virtuale, lo stato di integrità e punti di ripristino disponibile più recenti di hello. Fare clic su **proprietà** tooview ulteriori informazioni, vedere.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. In **Calcolo e rete** è possibile:
    - Modificare il nome di macchina virtuale di Azure hello. nome Hello deve soddisfare [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Specificare un [gruppo di risorse] successivo al failover.
    - Specificare una dimensione di destinazione per hello macchina virtuale di Azure
    - Selezionare un [set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md).
    - Specificare se toouse [dischi gestiti](#managed-disk-considerations). Selezionare **Sì**, se si desidera tooattach dischi gestiti tooyour computer tooAzure di migrazione.
    - Visualizzare o modificare le impostazioni di rete, inclusi hello/subnet della rete in cui hello macchina virtuale di Azure sarà posizionato dopo il failover e indirizzo IP hello che verrà assegnato tooit.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. In **dischi**, è possibile visualizzare informazioni sul sistema operativo hello e dischi dati in hello macchina virtuale.


## <a name="run-a-test-failover"></a>Eseguire un failover di test

A questo punto, eseguire una toomake di failover di test che tutto funzioni come previsto.

- Se si desidera tooconnect tooAzure macchine virtuali tramite RDP dopo il failover, [preparare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully toocopy di Active Directory e DNS è necessario nell'ambiente di test. [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations)
 - Per informazioni complete sul failover di test, leggere [questo articolo](site-recovery-test-failover-to-azure.md).
 
 Eseguire quindi un failover:

1. toofail su un singolo computer, in **elementi replicati**, fare clic su hello VM > **+ Test Failover** icona.
2. toofail sul ripristino di un piano, in **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).
3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure saranno connesse dopo il failover viene eseguito.
4. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **Failover di Test** processo nel nome dell'insieme di credenziali > **processi** > **i processi di ripristino del sito**.
5. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.
6. Se sono preparati per le connessioni dopo il failover, dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.
7. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note** registrare e salvare eventuali commenti associati hello test failover. Questa operazione eliminerà hello le macchine virtuali che sono state create durante il failover di test.



## <a name="next-steps"></a>Passaggi successivi

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.
- [Conoscenza failback](site-recovery-failback-from-azure-to-hyper-v.md), toofail back e replicare macchine virtuali di Azure, eseguire il sito Hyper-V di toohello primario locale.

