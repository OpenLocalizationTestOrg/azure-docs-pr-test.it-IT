---
title: sito secondario aaaEnable Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come replica tooenable per le macchine virtuali Hyper-V replica tooa sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Passaggio 9: Consentire al sito secondario tooa replica per le macchine virtuali Hyper-V


Dopo aver impostato un criterio di replica, utilizzare questo articolo tooenable replica tooa sito secondario di System Center Virtual Machine Manager (VMM) per on-premise Hyper-V le macchine virtuali (VM), utilizzando [Azure Site Recovery](site-recovery-overview.md).

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Selezionare le macchine virtuali tooreplicate

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. 

    ![Abilitare la replica](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. In **origine**, selezionare il server VMM di hello e cloud in cui hello si trovano gli host Hyper-V da tooreplicate hello. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. In **destinazione**, verificare il server VMM secondario di hello e cloud.
4. In **macchine virtuali**, selezionare le macchine virtuali hello desiderato tooprotect dall'elenco di hello.

    ![Abilitare la protezione delle macchine virtuali](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** azione in **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene completato, il completamento della replica iniziale hello e macchina virtuale di hello è pronta per il failover.

Si noti che:

- È inoltre possibile abilitare la protezione per le macchine virtuali nella console VMM hello. Fare clic su **Abilita protezione** sulla barra degli strumenti hello in proprietà macchina virtuale hello > **Azure Site Recovery** scheda.
- Dopo avere abilitato la replica, è possibile visualizzare le proprietà per hello VM in **elementi replicati**. In hello **Essentials** dashboard, è possibile visualizzare informazioni sui criteri di replica hello per hello macchina virtuale e il relativo stato. Per altri dettagli, fare clic su **Proprietà** .

## <a name="onboard-existing-vms"></a>Eseguire l'onboarding di VM esistenti

Se in VMM sono presenti macchine virtuali replicate tramite la replica Hyper-V, è possibile caricarle per la replica in Azure Site Recovery nel modo seguente:

1. Assicurarsi che nel server hello Hyper-V ospita macchina virtuale esistente si trova nel cloud primario hello hello e tale server Hyper-V hello hosting hello macchina virtuale di replica si trova nel cloud secondario hello.
2. Verificare che sia configurato un criterio di replica per i cloud VMM primario hello.
3. Abilitare la replica per macchina virtuale primaria hello. Azure Site Recovery e VMM assicurarsi che hello stesso host di replica e la macchina virtuale viene rilevato, Azure Site Recovery riutilizzerà e ristabilire la replica hello utilizzando le impostazioni specificate.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 10: eseguire un failover di test](vmm-to-vmm-walkthrough-test-failover.md).
