---
title: aaaSet le impostazioni di replica per Azure Site Recovery | Documenti Microsoft
description: "Descrive la modalità di cloud di tooAzure toodeploy Site Recovery tooorchestrate replica, il failover e ripristino di macchine virtuali Hyper-V in VMM."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Gestire i criteri di replica per VMware tooAzure


## <a name="create-a-replication-policy"></a>Creare un criterio di replica

1. Selezionare **Gestisci** > **Site Recovery Infrastructure** (Infrastruttura di Site Recovery).
2. Selezionare **Criteri di replica** in **For VMware and Physical machines** (Per VMware e computer fisici).
3. Selezionare **+Replication policy** (+Criteri di replica).

    ![Creare criteri di replica](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Immettere il nome di criterio hello.

5. In **soglia RPO**, specificare il limite RPO hello. Quando la replica continua supera questo limite, verranno generati avvisi.
6. In **conservazione del punto di ripristino**, specificare (in ore) hello durata del periodo di memorizzazione hello per ogni punto di ripristino. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di un periodo di memorizzazione.

    > [!NOTE]
    > Ore too24 periodo di conservazione è supportato per l'archiviazione replicata toopremium macchine. Ore too72 periodo di conservazione è supportato per l'archiviazione replicata toostandard macchine.

    > [!NOTE]
    > Viene creato automaticamente un criterio di replica per il failback.

7. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.

8. Fare clic su **OK**. criteri di Hello devono essere creato in 30 secondi too60.

![Generazione dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Associare un server di configurazione ai criteri di replica
1. Scegliere toowhich criteri di replica hello si desidera tooassociate hello configurazione server.
2. Fare clic su **Associa**.
![Associare i server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Selezionare il server di configurazione di hello hello elenco dei server.
4. Fare clic su **OK**. il server di configurazione di Hello deve essere associato una tootwo minuti.

![Associazione del server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Modificare un criterio di replica
1. Scegliere il criterio di replica hello per cui si desidera tooedit le impostazioni di replica.
![Modificare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Fare clic su **Edit Settings**.
![Modificare le impostazioni dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Modificare le impostazioni di hello in base alle esigenze.
4. Fare clic su **Salva**. criteri di Hello deve essere salvato in due toofive minuti, a seconda di quanti macchine virtuali utilizza tale criterio di replica.

![Salvare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Annullare l'associazione del server di configurazione dai criteri di replica
1. Scegliere toowhich criteri di replica hello si desidera tooassociate hello configurazione server.
2. Fare clic su **Annulla associazione**.
3. Selezionare il server di configurazione di hello hello elenco dei server.
4. Fare clic su **OK**. il server di configurazione di Hello deve dissociato in uno tootwo minuti.

    > [!NOTE]
    > Se è presente almeno un elemento replicato mediante criteri di hello è non è possibile annullare l'associazione di un server di configurazione. Assicurarsi che non sono presenti elementi replicati mediante criteri di hello prima annullare l'associazione del server di configurazione hello.

## <a name="delete-a-replication-policy"></a>Eliminare un criterio di replica

1. Scegliere il criterio di replica hello che si desidera toodelete.
2. Fare clic su **Elimina**. criteri di Hello devono essere eliminati in 30 secondi too60.

    > [!NOTE]
    > Se dispone di almeno una configurazione server associato tooit, è possibile eliminare un criterio di replica. Verificare che non sono presenti elementi replicati mediante criteri di hello e di eliminare che tutti hello associati server di configurazione prima di eliminare i criteri di hello.
