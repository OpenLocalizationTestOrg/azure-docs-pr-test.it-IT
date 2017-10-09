---
title: la replica per le macchine virtuali Hyper-V replica tooAzure (senza System Center VMM) con Azure Site Recovery aaaEnable | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooenable tooAzure di replica è necessario per le macchine virtuali Hyper-V tramite il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Passaggio 10: Abilitare la replica per le macchine virtuali Hyper-V replica tooAzure


In questo articolo viene descritto come replica tooenable per locale macchine virtuali Hyper-V (non gestite da System Center VMM) tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Prima di iniziare

Prima di iniziare, assicurarsi che l'account utente di Azure è necessario hello [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.

## <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica

Per impostazione predefinita, vengono replicati tutti i dischi in un computer. È possibile escludere dischi dalla replica. Ad esempio non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato ogni volta che un computer o applicazione viene riavviata (ad esempio pagefile.sys o tempdb di SQL Server). [Altre informazioni](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Replicare le VM

Abilitare la replica per le macchine virtuali nel modo seguente:          

1. Fare clic su **Eseguire la replica dell'applicazione** > **Origine**. Dopo aver configurato la replica per hello prima volta, è possibile fare clic su **+ replicare** replica tooenable per computer aggiuntivi.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. In **origine**, selezionare il sito hello Hyper-V. Fare quindi clic su **OK**.
3. In **destinazione**, selezionare una sottoscrizione di insieme di credenziali hello e hello failover modello toouse in Azure (classica o risorsa management) dopo il failover.
4. Selezionare l'account di archiviazione hello da toouse. Se non si dispone di un account a cui si vuole toouse, è possibile [crearlo](#set-up-an-azure-storage-account). Fare quindi clic su **OK**.
5. Quando si crea il failover, si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure.

    - tooapply hello rete impostazioni tooall macchine si abilita per la replica, selezionare **Configura ora per macchine virtuali selezionate**.
    - Selezionare **configurare successivamente** tooselect hello Azure rete al computer.
    - Se non si dispone di una rete a cui si desidera toouse, è possibile [crearlo](#set-up-an-azure-network). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.

   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. In **proprietà** > **configurare proprietà**selezionare hello del sistema operativo per le macchine virtuali selezionata hello e hello disco del sistema operativo.
8. Verificare il nome di macchina virtuale di Azure hello (nome di destinazione) sia conforme ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Per impostazione predefinita sono selezionati tutti i dischi di hello di hello VM per la replica. Cancella dischi tooexclude li.
10. Fare clic su **OK** toosave modifiche. È possibile impostare proprietà aggiuntive in un secondo momento.

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. In **le impostazioni di replica** > **configurare le impostazioni di replica**, selezionare i criteri di replica hello da tooapply per hello protetto le macchine virtuali. Fare quindi clic su **OK**. È possibile modificare il criterio di replica hello in **criteri di replica** > criteri-name > **Modifica impostazioni**. Le modifiche applicate verranno usate per i computer di cui è già in corso la replica e per i nuovi computer.


   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.


## <a name="next-steps"></a>Passaggi successivi


Andare troppo[passaggio 11: eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)
