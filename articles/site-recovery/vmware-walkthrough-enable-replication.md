---
title: la replica per le macchine virtuali VMware replica tooAzure con Azure Site Recovery aaaEnable | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooenable tooAzure di replica è necessario per le macchine virtuali VMware tramite il servizio di Azure Site Recovery hello"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Passaggio 11: Abilitare la replica per tooAzure macchine virtuali VMware


In questo articolo viene descritto come replica tooenable per on-premise VMware virtual macchine tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

- Le macchine virtuali VMware è necessario hello [componente del servizio di mobilità installato](vmware-walkthrough-install-mobility.md). -Se una macchina virtuale viene preparata per l'installazione push, il server di elaborazione hello installa automaticamente il servizio di mobilità hello quando si abilita la replica.
- L'account utente di Azure necessario specifico [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) replica tooenable di tooAzure una macchina virtuale
- Quando si aggiungono o si modificano le macchine virtuali, può richiedere too15 minuti o più per effetto tootake modifiche e per essi tooappear nel portale di hello.
- È possibile controllare l'ora di ultimo individuato hello per le macchine virtuali in **server di configurazione** > **ultimo contatto in**.
- tooadd macchine virtuali senza attendere l'individuazione pianificata hello, evidenziazione hello del server di configurazione (non selezionata), fare clic su **aggiornamento**.



## <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica

Per impostazione predefinita, vengono replicati tutti i dischi in un computer. È possibile escludere dischi dalla replica. Ad esempio non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato ogni volta che un computer o applicazione viene riavviata (ad esempio pagefile.sys o tempdb di SQL Server). [Altre informazioni](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicare le VM

Prima di iniziare, guardare una rapida panoramica video

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**.
2. In **origine**, selezionare il server di configurazione di hello.
3. In **Tipo di computer** selezionare **Macchine virtuali**.
4. In **vCenter/vSphere Hypervisor**, selezionare i server vCenter hello che gestisce host vSphere hello, o host hello.
5. Selezionare il server di elaborazione hello. Se è ancora stato creato alcun server di elaborazione aggiuntive, questo sarà il server di configurazione di hello. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. In **destinazione**, selezionare la sottoscrizione hello e hello gruppo di risorse in cui si desidera hello toocreate failover le macchine virtuali. Scegliere modello di distribuzione hello che si desidera toouse in Azure (classica o risorsa management), per eseguire il failover le macchine virtuali hello.


7. Selezionare l'account di archiviazione di Azure hello desiderato toouse per la replica dei dati. Se non si desidera toouse un account già stato configurato, è possibile creare uno nuovo.

8. Si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure, quando vengono creati dopo il failover. Selezionare **Configura ora per macchine virtuali selezionate**, tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente** tooselect hello Azure rete al computer. Se non si desidera toouse una rete esistente, è possibile crearne uno.

    ![Abilitare la replica](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. In **proprietà** > **configurare proprietà**, selezionare account hello che verrà usato da hello processo server tooautomatically installare il servizio Mobility hello computer hello.
11. Per impostazione predefinita, vengono replicati tutti i dischi. Fare clic su **tutti i dischi** e cancellare tutti i dischi non si desidera tooreplicate. Fare quindi clic su **OK**. È possibile impostare proprietà aggiuntive delle VM in un secondo momento.

    ![Abilitare la replica](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. In **le impostazioni di replica** > **configurare le impostazioni di replica**, verificare che hello si seleziona il criterio di replica corretto. Se si modifica un criterio, le modifiche saranno tooreplicating applicato macchina e toonew macchine.
12. Abilitare **la coerenza tra più macchine** se si desidera toogather macchine in un gruppo di replica e specificare un nome per il gruppo di hello. Fare quindi clic su **OK**. Si noti che:

    * I computer in gruppi di replica vengono replicati insieme e hanno punti di ripristino condivisi coerenti con l'arresto anomalo del sistema e coerenti con l'app in caso di failover.
    * È consigliabile raggruppare le macchine virtuali e i server fisici in modo da rispecchiare i carichi di lavoro. Abilitazione della coerenza tra più macchine può influire sulle prestazioni del carico di lavoro e deve essere utilizzato solo se sono in esecuzione macchine hello stesso carico di lavoro ed è necessaria la coerenza.

    ![Abilitare la replica](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Fare clic su **Abilita la replica**. È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 12: eseguire un failover di test](vmware-walkthrough-test-failover.md)
