---
title: aaaEnable tooAzure di replica per le macchine virtuali Hyper-V in VMM cloud con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come cloud tooenable tooAzure di replica per le macchine virtuali Hyper-V in VMM, con hello servizio Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Passaggio 11: Abilitare la replica tooAzure per le macchine virtuali Hyper-V nei cloud VMM

Dopo aver configurato un criterio di replica, utilizzare questo articolo tooenable la replica per le macchine virtuali Hyper-V locale (VM) gestita nei cloud di System Center Virtual Machine Manager (VMM)), tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md)di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

Verificare che l'account di Azure è hello corretto [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate macchine virtuali di Azure. [Altre informazioni](../active-directory/role-based-access-built-in-roles.md) sul controllo degli accessi in base al ruolo di Azure.

## <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica

Per impostazione predefinita, vengono replicati tutti i dischi in un computer. È possibile escludere dischi dalla replica. Ad esempio non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato ogni volta che un computer o applicazione viene riavviata (ad esempio pagefile.sys o tempdb di SQL Server). [Altre informazioni](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicare le VM

Abilitare la replica per le macchine virtuali nel modo seguente:  

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. Dopo aver abilitato la replica per hello prima volta, fare clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine aggiuntive.

    ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. In hello **origine** blade, server VMM selezionare hello e hello cloud in cui hello Hyper-V si trovano gli host. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. In **destinazione**, selezionare la sottoscrizione di hello, modello di distribuzione dopo il failover, e hello account di archiviazione in uso per i dati replicati.

    ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Selezionare l'account di archiviazione hello da toouse. Se si desidera toouse un account di archiviazione diverso rispetto a quelle si dispone, è possibile [crearlo](#set-up-an-azure-storage-account). Se si utilizza un account di archiviazione premium per i dati replicati, è necessario tooselect un ulteriore spazio di archiviazione standard account toostore i log di replica che consentono di acquisire le modifiche locali tooon data.toocreate un account di archiviazione utilizzando il modello di gestione risorse hello Fare clic su **Crea nuovo**. Se si desidera che un account di archiviazione utilizzando il modello classico hello toocreate, [nel portale di Azure hello](../storage/common/storage-create-storage-account.md). Fare quindi clic su **OK**.
5. Si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure, quando vengono creati dopo il failover. Selezionare **Configura ora per macchine virtuali selezionate**, tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente**, tooselect hello Azure rete al computer. Se si desidera toouse una rete diversa da quelle si dispone, è possibile [crearlo](#set-up-an-azure-network). Fare clic su modello di gestione risorse di hello toocreate una rete usando **Crea nuovo**. Se si desidera toocreate una rete usando il modello classico di hello, [nel portale di Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.
6. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. In **proprietà** > **configurare proprietà**selezionare hello del sistema operativo per le macchine virtuali selezionata hello e hello disco del sistema operativo.

    - Verificare il nome di macchina virtuale di Azure hello (nome di destinazione) sia conforme ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Per impostazione predefinita sono selezionati tutti i dischi di hello di hello VM per la replica, ma è possibile cancellare i dischi tooexclude li.

        - Si consiglia di larghezza di banda replica tooreduce tooexclude dischi. Ad esempio, non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato un computer o App ogni volta che viene riavviato (ad esempio pagefile.sys o tempdb di Microsoft SQL Server). È possibile escludere il disco di hello dalla replica dal disco hello deselezionando la casella.
        - Solo i dischi di base possono essere esclusi dalla replica. Non è possibile escludere dischi del sistema operativo
        - e non è consigliabile escludere dischi dinamici. Site Recovery non può determinare se un disco rigido virtuale all'interno della macchina virtuale guest è di base o dinamico. Se non sono esclusi tutti i dischi dei volumi dinamici dipendenti, disco dinamico protetto hello verrà visualizzata come un disco guasto quando hello VM viene eseguito il failover e hello dati presenti sul disco non saranno accessibili.
        - Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera tooadd o esclude un disco, necessitano di protezione toodisable per hello macchina virtuale e riabilitarla.
        - Per i dischi creati manualmente in Azure non viene eseguito il failback. Ad esempio, se si esito negativo su tre dischi e creare due direttamente nella macchina virtuale di Azure, solo hello tre dischi che sono stati eseguiti il failover non verranno eseguiti nuovamente da Azure tooHyper-V. È possibile includere i dischi creati manualmente il failback oppure la replica inversa da tooAzure Hyper-V.
        - Se si esclude un disco è sufficiente per toooperate un'applicazione, dopo il failover tooAzure occorre toocreate manualmente in Azure, in modo che hello replicati applicazione può essere eseguito. In alternativa, è possibile integrare automazione di Azure in un piano di ripristino disco hello toocreate durante il failover della macchina hello.

    Fare clic su **OK** toosave modifiche. È possibile impostare proprietà aggiuntive in un secondo momento.

    ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. In **le impostazioni di replica** > **configurare le impostazioni di replica**, selezionare i criteri di replica hello da tooapply per hello protetto le macchine virtuali. Fare quindi clic su **OK**. È possibile modificare il criterio di replica hello in **criteri di replica** > Nome criterio > **Modifica impostazioni**. Le modifiche applicate vengono usate per i computer di cui è già in corso la replica e per i nuovi computer.

   ![Abilitare la replica](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito, hello macchina è pronta per il failover.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 12: eseguire un failover di test](vmm-to-azure-walkthrough-test-failover.md)
