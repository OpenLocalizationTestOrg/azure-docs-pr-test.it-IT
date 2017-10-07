---
title: aaaSet un criterio di replica per macchina virtuale Hyper-V (con VMM) replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset un criterio di replica per macchina virtuale Hyper-V (con VMM) replica tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Passaggio 10: Configurare un criterio di replica per macchina virtuale Hyper-V replica (con VMM) tooAzure


Dopo l'impostazione [mapping di rete](vmm-to-azure-walkthrough-network-mapping.md), usare questo tooconfigure articolo un criterio di replica T\tooreplicate locale macchine virtuali Hyper-V gestite in tooAzure cloud di System Center Virtual Machine Manager (VMM), utilizzando hello [ Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Creare un criterio

1. toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri.
3. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).

    > [!NOTE]
    >  Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30. limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium. [Altre informazioni](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **conservazione del punto di ripristino**, specificare in ore, per quanto tempo il periodo di memorizzazione hello verrà per ogni punto di ripristino. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di una finestra.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello. Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Si noti che se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.
6. In **ora inizio replica iniziale**, indicare quando toostart hello la replica iniziale. la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità.
7. In **crittografare i dati archiviati in Azure**, specificare se tooencrypt dati rest nell'archiviazione di Azure. Fare quindi clic su **OK**.

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Quando si crea un nuovo criterio automaticamente associato hello cloud VMM. Fare clic su **OK**. È possibile associare altri cloud VMM (e hello macchine virtuali in essi contenuti) con questo criterio di replica in **replica** > Nome criterio > **associare Cloud VMM**.

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 11: abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)
