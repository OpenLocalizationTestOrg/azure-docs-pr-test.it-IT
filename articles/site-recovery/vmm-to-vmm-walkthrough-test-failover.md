---
title: un failover di test per il sito secondario macchina virtuale Hyper-V replica tooa con Azure Site Recovery aaaRun | Documenti Microsoft
description: Viene descritto come un failover di test per la macchina virtuale Hyper-V replica tooa toorun sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Passaggio 10: Eseguire un failover di test per il sito secondario di Hyper-V replica tooa


Dopo aver abilitato la replica per le macchine virtuali Hyper-V (VM) con [Azure Site Recovery](site-recovery-overview.md), utilizzare questo toorun articolo un failover di test. Un failover di test verifica che la replica funzioni, senza alcuna conseguenza sull'ambiente di produzione. 


Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

- Quando si è attivato un failover di test, è possibile specificare hello rete toowhich hello replica di test che si connetteranno le macchine virtuali. [Altre informazioni](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sulle opzioni di rete hello.
- È consigliabile non scegliere una rete selezionata durante il mapping di rete.
- Hello istruzioni riportate in questo articolo viene descritto come toofail su una singola macchina virtuale. Conoscenza [la creazione di piani di ripristino](site-recovery-create-recovery-plans.md) se si desidera toofail insieme in più macchine virtuali.
- Consultare l'articolo relativo alle [limitazioni per i failover di test](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- indirizzo IP assegnato tooa VM durante il test failover Hello è hello stesso indirizzo IP che hello VM riceverebbe per un failover pianificato o non pianificato (presumendo che che l'indirizzo IP hello è disponibile in rete di failover di test hello). Se l'indirizzo IP hello non è disponibile in rete di failover di test hello, hello VM riceve un altro indirizzo IP disponibile in rete di failover di test hello.
- Se si desidera toodo un failover di test della rete di produzione, per la convalida completa della macchina di connettività di rete end-to-end, si noti che:
    - Hello che VM primaria devono essere arrestati quando si sta eseguendo il failover di test hello. In caso contrario, due macchine virtuali con hello stessa identità verrà eseguito in hello stessa rete in hello contemporaneamente. 
    - Se si apportano modifiche di macchine virtuali tootest, tali modifiche vengono perse quando si pulizia hello failover di test. Queste modifiche non vengono replicata toohello indietro VM primaria.
    - Test di una rete di produzione lead toodowntime per i carichi di lavoro di produzione. Chiedere agli utenti non toouse hello app durante l'analisi di ripristino di emergenza hello.  


## <a name="run-a-test-failover-for-a-vm"></a>Eseguire un failover di test per una macchina virtuale

1. toofail su una singola macchina virtuale, in **elementi replicati**, fare clic su hello VM > **Failover di Test**.
2. In **Test Failover**, specificare la modalità di macchine virtuali di test verranno connesse toonetworks dopo il failover di test di hello. 
3. Fare clic su **OK** toobegin hello failover. Avanzamento delle hello **processi** scheda.
5. Al termine del failover, verificare che avvia le macchine virtuali di test hello correttamente.
6. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello.
7. In **note**, registrare e salvare eventuali commenti associati hello test failover. Questo passaggio Elimina hello le macchine virtuali e reti che sono state create durante il failover di test.


## <a name="next-steps"></a>Passaggi successivi

Dopo aver testato distribuzione hello, ulteriori informazioni su altri tipi di [failover](site-recovery-failover.md).
