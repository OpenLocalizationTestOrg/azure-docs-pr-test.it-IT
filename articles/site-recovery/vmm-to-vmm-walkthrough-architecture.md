---
title: architettura di hello aaaReview per il sito secondario con tooa di replica Hyper-V con Azure Site Recovery | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dell'architettura di hello per la replica delle macchine virtuali Hyper-V tooa secondario System Center VMM sito locale con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Passaggio 1: Esaminare l'architettura di hello per il sito secondario di Hyper-V replica tooa

Questo articolo vengono descritti i componenti di hello e processi per la replica locale macchine virtuali di Hyper-V (VM) in cloud System Center Virtual Machine Manager (VMM), sito VMM secondario tooa utilizzando hello [Azure Site Recovery](site-recovery-overview.md)di hello portale di Azure.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componenti dell'architettura

Ecco cosa occorre per la replica del sito VMM secondario di macchine virtuali Hyper-V tooa.

**Componente** | **Posizione** | **Dettagli**
--- | --- | ---
**Azzurro** | Sottoscrizione di Azure. | Creare un insieme di credenziali di servizi di ripristino in hello sottoscrizione di Azure, tooorchestrate e gestire la replica tra i percorsi di VMM.
**Server VMM** | È necessario avere a disposizione un percorso VMM primario e uno secondario. | Si consiglia di un server VMM nel sito primario di hello e uno nel sito secondario hello 
**Server Hyper-V** |  Uno o più server Hyper-V host nei cloud VMM primario e secondario di hello. | Dati vengono replicati tra hello server primario e secondario Hyper-V host su hello LAN o VPN, utilizzando l'autenticazione Kerberos o certificati.  
**VM Hyper-V** | Nel server host Hyper-V. | server host di origine Hello deve avere almeno una macchina virtuale che si desidera tooreplicate.

## <a name="replication-process"></a>Processo di replica

1. Impostare hello account Azure, creare un insieme di credenziali di servizi di ripristino e specificare gli elementi da tooreplicate.
2. Configurare hello origine e destinazione le impostazioni di replica, che include l'installazione di hello Provider di Azure Site Recovery nel server VMM e agente di servizi di ripristino di Microsoft Azure hello in ogni host Hyper-V.
3. Creare un criterio di replica per l'origine hello cloud VMM. criteri di Hello sono applicato tooall macchine virtuali presenti negli host nel cloud hello.
4. Abilitare la replica per ogni VMM e viene eseguita la replica iniziale di una macchina virtuale in base alle impostazioni di hello che prescelto.
5. Dopo la replica iniziale, viene avviata la replica delle modifiche differenziali. Le modifiche rilevate per un elemento vengono salvate in un file HRL.


![Tooon tra più sedi locali](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Processo di failover e failback

1. È possibile eseguire un [failover](site-recovery-failover.md) pianificato o non pianificato tra siti locali. Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.
4. Se si esegue un failover non pianificato tooa sito secondario, dopo il failover delle macchine hello nella posizione secondaria hello non sono abilitati per la replica o di protezione. Se si esegue un failover pianificato, dopo il failover hello, le macchine in posizione secondaria hello sono protetti.
5. Quindi, si esegue il commit hello failover toostart accesso hello del carico di lavoro dalla replica hello macchina virtuale.
6. Quando il sito primario è nuovamente disponibile, si avvia tooreplicate replica inversa da hello del sito secondario toohello primario. La replica inversa porta hello le macchine virtuali in uno stato protetto, ma Data Center secondario hello è ancora percorso attivo hello.
7. sito primario di hello toomake nel percorso active hello, si avvia nuovamente un failover pianificato da tooprimary secondario, seguita da un'altra replica inversa.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 2: esaminare i prerequisiti di hello e le limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).
