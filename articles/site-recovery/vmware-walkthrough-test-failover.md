---
title: un failover di test per VMware replica tooAzure aaaRun | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello che è necessario per l'esecuzione di un failover di test per le macchine virtuali VMware replica tooAzure utilizzando il servizio di Azure Site Recovery hello."
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
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>Passaggio 12: Eseguire un tooAzure di failover di test per le macchine virtuali VMware

In questo articolo viene descritto come un failover di test da on-premise VMware virtual toorun macchine tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

Prima di eseguire un failover di test, che è consigliabile verificare le proprietà della VM hello e apportare le modifiche è necessario. è possibile accedere a proprietà della macchina virtuale hello in **gli elementi replicati**. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.

## <a name="managed-disk-considerations"></a>Considerazioni su Managed Disks

[Dischi gestiti](../virtual-machines/windows/managed-disks-overview.md) semplificano la gestione disco per le macchine virtuali di Azure, mediante la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. 

- Quando si abilita la protezione per una macchina virtuale, i dati di macchina virtuale vengono replicati tooa account di archiviazione. Dischi gestiti vengono creati e collegati toohello macchina virtuale solo quando si verifica il failover.
- Dischi gestiti possono essere creati solo per le macchine virtuali distribuite tramite il modello di gestione risorse hello.  
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

È consigliabile verificare le proprietà di hello hello computer di origine prima di eseguire un failover.

1. In **elementi protetti**, fare clic su **elementi replicati**, fare clic su hello macchina virtuale.
2. In hello **elemento replicato** riquadro, è possibile visualizzare un riepilogo delle informazioni di macchina virtuale, lo stato di integrità e punti di ripristino disponibile più recenti di hello. Fare clic su **proprietà** tooview ulteriori informazioni, vedere.
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

1. toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su hello VM > **+ Test Failover** icona.

    ![Failover di test](./media/vmware-walkthrough-test-failover/test-failover.png)

2. toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).  

3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure saranno connesse dopo il failover viene eseguito.

4. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **Failover di Test** processo nel nome dell'insieme di credenziali > **impostazioni** > **processi**  >  **i processi di ripristino del sito**.

5. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.

6. Se sono preparati per le connessioni dopo il failover, dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.

7. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note**, registrare e salvare eventuali commenti associati hello test failover. Questa operazione eliminerà le macchine virtuali hello creati durante il failover di test.



## <a name="next-steps"></a>Passaggi successivi

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.
- [Altre informazioni](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers) per eseguire la migrazione di computer invece della replica e del failback.
- [Conoscenza failback](site-recovery-failback-azure-to-vmware.md), toofail back e replicare macchine virtuali di Azure, eseguire il backup del sito primario locale toohello.
