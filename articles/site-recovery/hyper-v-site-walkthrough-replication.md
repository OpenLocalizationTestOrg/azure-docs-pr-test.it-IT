---
title: aaaSet un criterio di replica per macchina virtuale Hyper-V replica (senza System Center VMM) tooAzure con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica per la replica di archiviazione di macchine virtuali Hyper-V tooAzure"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Passaggio 9: Configurare un criterio di replica per macchina virtuale Hyper-V replica tooAzure

Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica tooAzure macchine virtuali Hyper-V (senza System Center VMM) usando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Informazioni sugli snapshot

Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello.
    - Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot.
    - Se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.

## <a name="set-up-a-replication-policy"></a>Configurare criteri di replica

1. toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri.
3. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).

    > [!NOTE]
    > Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30. limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium. [Altre informazioni](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **conservazione del punto di ripristino**, specificare in ore il tempo è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali possono essere ripristinati tooany punto all'interno di una finestra.
5. In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.
6. In **ora inizio replica iniziale**, specificare quando toostart hello la replica iniziale. la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità. Fare quindi clic su **OK**.

    ![Criteri di replica](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Quando si crea un nuovo criterio, è associata automaticamente a sito Hyper-V hello. È possibile associare un sito Hyper-V (e hello macchine virtuali in esso) a più criteri di replica in **replica** > criteri-name > **associare sito Hyper-V**.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 10: abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)
