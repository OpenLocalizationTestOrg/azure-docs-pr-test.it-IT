---
title: aaaMap reti per il sito secondario macchina virtuale Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come toomap reti per la replica delle macchine virtuali Hyper-V tooa VMM del sito secondario con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Passaggio 7: Eseguire il mapping di reti per il sito secondario di macchina virtuale Hyper-V replica tooa


Dopo l'impostazione [impostazioni di origine e destinazione](vmm-to-vmm-walkthrough-source-target.md) per la replica Hyper-V, macchine virtuali (VM) tooa System Center Virtual Machine Manager (VMM) del sito secondario, utilizzare questo mapping di rete tooconfigure articolo per virtuale Hyper-V Machine (VM) replica tooa secondario del sito, utilizzando [Azure Site Recovery](site-recovery-overview.md).

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

- Leggere le informazioni sul [mapping di rete](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) prima di iniziare.
- Verificare che le macchine virtuali nei server VMM siano connessi tooa rete VM.

## <a name="configure-network-mapping"></a>Configurare il mapping di rete

1. In **Mapping di rete** > **Mapping di rete** fare clic su **+Mapping di rete**.
2. In **aggiungere mapping di rete** , selezionare l'origine hello e i server VMM di destinazione. vengono recuperate le reti VM Hello associate al server VMM hello.
3. In **rete di origine**selezionare hello rete toouse elenco hello di reti VM associate al server VMM primario hello.
4. In **rete di destinazione**selezionare hello rete toouse nel server VMM secondario hello. Fare quindi clic su **OK**.

    ![Mapping di rete](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:

* Le macchine virtuali di replica esistente che corrispondono toohello rete VM di origine sarà connessa toohello rete VM di destinazione.
* Nuove macchine virtuali che sono connessi toohello rete VM di origine sarà connessa toohello rete mappata di destinazione dopo la replica.
* Se si modifica un mapping esistente con una nuova rete, macchine virtuali di replica verranno connesse usando le nuove impostazioni hello.
* Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 8: configurare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).
