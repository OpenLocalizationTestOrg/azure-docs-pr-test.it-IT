---
title: il mapping di rete per la replica delle macchine virtuali Hyper-V in VMM aaaConfigure cloud tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooconfigure il mapping di rete durante la replica delle macchine virtuali Hyper-V in VMM cloud tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Passaggio 9: Configurare il mapping di rete per Hyper-V replica (con VMM) tooAzure

Dopo aver impostato hello [le impostazioni di replica di origine e destinazione](vmm-to-azure-walkthrough-source-target.md), utilizzare questo mapping toomap di articolo tooconfigure rete tra le reti VM di VMM in locale e le reti di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Prima di iniziare

- Informazioni sul [mapping di rete](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Preparare VMM per il mapping di rete](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Verificare che le macchine virtuali nel server VMM hello siano rete VM tooa connessi e di aver creato almeno una rete virtuale di Azure. Più reti VM possono essere mappate tooa singola rete di Azure.

## <a name="configure-mapping"></a>Configurare il mapping

Per configurare il mapping, procedere come segue:

1. In **infrastruttura di Site Recovery** > **mapping di rete** > **Mapping di rete**, fare clic su hello **+ Mapping di rete**  icona.

    ![Mapping di rete](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. In **aggiungere mapping di rete**, selezionare server VMM di origine hello e **Azure** come destinazione di hello.
3. Verificare la sottoscrizione hello e modello di distribuzione hello dopo il failover.
4. In **rete di origine**selezionare rete VM di hello origine locale si desidera toomap dall'elenco di hello associato al server VMM hello.
5. In **rete di destinazione**, selezionare hello in quale replica di macchine virtuali di Azure sarà disponibile quando si crea rete di Azure. Fare quindi clic su **OK**.

    ![Mapping di rete](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:

* Macchine virtuali esistenti in una rete VM origine hello sono connessi toohello rete di destinazione quando avviare il mapping. Rete VM di origine connesso toohello di nuove macchine virtuali connessi toohello eseguito il mapping di rete di Azure, quando viene eseguita la replica.
* Se si modifica un mapping di rete esistente, macchine virtuali di replica è possibile connettersi utilizzando le nuove impostazioni hello.
* Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica si connette toothat subnet di destinazione dopo il failover.
* Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello si connette toohello prima subnet nella rete hello.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 10: creare un criterio di replica](vmm-to-azure-walkthrough-replication.md)
