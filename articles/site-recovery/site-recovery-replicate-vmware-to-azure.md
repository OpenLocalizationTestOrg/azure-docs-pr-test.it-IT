---
title: La replica di applicazioni (VMware tooAzure) | Documenti Microsoft
description: In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione su VMware in Azure.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>La replica di applicazioni in esecuzione su macchine virtuali VMware tooAzure



In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione su VMware in Azure.
## <a name="prerequisites"></a>Prerequisiti

Hello si presume che sia già

1.  [Configurare l'ambiente di origine locale](site-recovery-set-up-vmware-to-azure.md)
2.  [Configurare l'ambiente di destinazione in Azure](site-recovery-prepare-target-vmware-to-azure.md).


## <a name="enable-replication"></a>Abilitare la replica
#### <a name="before-you-start"></a>Prima di iniziare
Quando si esegue la replica di macchine virtuali VMware, tenere presente quanto segue:

* L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.
* Le VM VMware vengono rilevate ogni 15 minuti. Potrebbero essere necessari 15 minuti o più per tali tooappear nel portale di hello dopo l'individuazione. Allo stesso modo, l'individuazione può richiedere anche più di 15 minuti quando si aggiunge un nuovo host vSphere o un server vCenter.
* Le modifiche dell'ambiente nella macchina virtuale hello (ad esempio, l'installazione degli strumenti di VMware) possono richiedere 15 minuti o più toobe aggiornata nel portale di hello.
* È possibile controllare hello individuati ultima ora per le macchine virtuali VMware in hello **ultimo contatto in** field per hello vCenter server/host vSphere, su hello **server di configurazione** blade.
* tooadd macchine per la replica senza attendere l'individuazione pianificata hello, evidenziare il server di configurazione di hello (non selezionata), fare clic su hello **aggiornamento** pulsante.
* Quando si abilita la replica, se viene preparata macchina hello, server process hello installa automaticamente il servizio di mobilità hello su di esso.


**Per abilitare la replica, procedere come descritto di seguito**.

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. Dopo aver abilitato la replica per hello prima volta, fare clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine aggiuntive.
2. In hello **origine** pannello > **origine**, selezionare il server di configurazione di hello.
3. In **Tipo di computer** selezionare **Macchine virtuali** o **Computer fisici**.
4. In **vCenter/vSphere Hypervisor**, selezionare i server vCenter hello che gestisce host vSphere hello, o host hello. Questa impostazione non si applica se si esegue la replica di computer fisici.
5. Selezionare il server di elaborazione hello. Se è ancora stato creato alcun server di elaborazione aggiuntive questo sarà il nome di hello hello del server di configurazione. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. In **destinazione** selezionare hello sottoscrizione e il gruppo di risorse hello in cui si desidera hello toocreate eseguito il failover delle macchine virtuali. Scegliere modello di distribuzione hello che si desidera toouse in Azure (classica o risorsa di gestione) per il failover le macchine virtuali hello.
7. Selezionare l'account di archiviazione di Azure hello desiderato toouse per la replica dei dati. Si noti che:

   * È possibile selezionare un account di archiviazione Standard o Premium. Se si seleziona un account premium, è necessario un account di archiviazione standard aggiuntivi toospecify per i log di replica in corso. Gli account devono essere in hello stessa area hello insieme di credenziali di servizi di ripristino.
   * Se si desidera toouse un account di archiviazione diverso rispetto a quelle si dispone, è possibile creare uno*collegamento segnaposto per la creazione di account di archiviazione tramite resource manager che rientrano nella Guida introduttiva*. Fare clic su un account di archiviazione tramite Gestione risorse, toocreate **Crea nuovo**. Se si desidera che un account di archiviazione utilizzando il modello classico hello toocreate, non che [nel portale di Azure hello](../storage/common/storage-create-storage-account.md).

8. Si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure, quando si riattivata dopo il failover. deve essere rete Hello hello stessa area hello insieme di credenziali di servizi di ripristino. Selezionare **Configura ora per macchine virtuali selezionate**, tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente** tooselect hello Azure rete al computer. Se non si dispone di una rete, è necessario troppo[crearlo](#set-up-an-azure-network). Fare clic su una rete di gestione di risorse, toocreate **Crea nuovo**. Se si desidera toocreate una rete usando il modello classico di hello, [nel portale di Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. In **proprietà** > **configurare proprietà**, selezionare account hello che verrà usato da hello processo server tooautomatically installare il servizio Mobility hello computer hello.  
11. Per impostazione predefinita, vengono replicati tutti i dischi. Fare clic su dischi tooexclude dalla replica, **tutti i dischi** e cancellare tutti i dischi non si desidera tooreplicate.  Fare quindi clic su **OK**. È possibile impostare proprietà aggiuntive in un secondo momento. [Altre informazioni](site-recovery-exclude-disk.md) sull'esclusione di dischi.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. In **le impostazioni di replica** > **configurare le impostazioni di replica**, verificare che hello si seleziona il criterio di replica corretto. È possibile modificare le impostazioni dei criteri di replica in **Impostazioni** > **Criteri di replica** > nome dei criteri > **Modifica impostazioni**. Le modifiche applicate tooa criteri verranno applicati tooreplicating e nuove macchine.
13. Abilitare **la coerenza tra più macchine** se si desidera toogather macchine in un gruppo di replica e specificare un nome per il gruppo di hello. Fare quindi clic su **OK**. Si noti che:

    * Le macchine virtuali in un gruppo di replica vengono replicate insieme hanno punti di ripristino condivisi coerenti con l'arresto anomalo del sistema e coerenti con l'app quando si esegue il failover.
    * È consigliabile raggruppare le macchine virtuali e i server fisici in modo da rispecchiare i carichi di lavoro. Abilitare la coerenza tra più macchine può influire sulle prestazioni del carico di lavoro e deve essere utilizzato solo se sono in esecuzione macchine hello stesso carico di lavoro ed è necessaria la coerenza.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Fare clic su **Abilita la replica**. È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.

> [!NOTE]
> Se la macchina hello è pronto per hello installazione push mobilità verrà installato il componente del servizio quando è abilitata la protezione. Dopo aver hello componente viene installato ha esito negativo e il computer di hello che avvia un processo di protezione. Dopo l'errore hello è necessario toomanually riavviare ogni macchina. Dopo la protezione di hello hello riavvio del processo inizia nuovamente e viene eseguita la replica iniziale.
>
>

## <a name="view-and-manage-vm-properties"></a>Visualizzare e gestire le proprietà della macchina virtuale

È consigliabile verificare le proprietà di hello hello computer di origine. Tenere presente il nome della macchina virtuale di Azure hello deve essere conformi ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Fare clic su **impostazioni** > **gli elementi replicati** > e selezionare hello macchina. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.
2. In **proprietà**, è possibile visualizzare la replica e le informazioni di failover per hello macchina virtuale.
3. In **di calcolo e rete** > **calcolo proprietà**, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione. Se si desidera, modificare toocomply nome hello ai requisiti di Azure.
    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  È possibile selezionare un [gruppo di risorse](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) il cui computer andrà a fare parte del post-failover. Questa impostazione può essere modificata in qualsiasi momento prima del failover. Registra il failover, se si esegue la migrazione di gruppo di risorse diverso hello macchina tooa quindi verranno interrotte le impostazioni di protezione di una macchina.
5. È possibile selezionare un [set di disponibilità](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) se il computer necessario toobe far parte di post di un failover. Mentre si seleziona il set di disponibilità, tenere presente che:

    * Verrà elencato solo i gruppi di disponibilità appartenenti toohello specificato gruppo di risorse  
    * I computer con reti virtuali diverse non possono fare parte dello stesso set di disponibilità
    * Solo le macchine virtuali della stessa dimensione possono fare parte della stesso set di disponibilità
5. È inoltre possibile visualizzare e aggiungere le informazioni di rete di destinazione hello, subnet e indirizzi IP che verranno assegnato toohello macchina virtuale di Azure.
6. In **dischi**, è possibile vedere hello del sistema operativo e dischi dati in hello VM che verranno replicati.

### <a name="network-adapters-and-ip-addressing"></a>Schede di rete e indirizzi IP 

- È possibile impostare l'indirizzo IP di destinazione hello. Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP. Se si imposta un indirizzo che non è disponibile in caso di failover, failover hello non funzionerà. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.
- numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:
    - Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
    - Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
    - Se, ad esempio un computer di origine ha due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.
    - Se più schede di rete nella macchina virtuale hello verranno tutti connettono toohello stessa rete.
    - Se macchina virtuale hello ha più schede di rete hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.
   



## <a name="common-issues"></a>Problemi comuni

* Le dimensioni di ogni disco devono essere inferiori a 1 TB.
* disco Hello del sistema operativo deve essere un disco di base e un disco dinamico non
* Per la generazione 2/UEFI abilitato le macchine virtuali, la famiglia di sistemi operativi hello deve essere Windows e il disco di avvio deve essere minore di 300GB

## <a name="next-steps"></a>Passaggi successivi

Una volta hello della protezione è stata completata, è possibile provare [failover](site-recovery-failover.md) toocheck indica se l'applicazione viene visualizzato in Azure o non.

Nel caso in cui si desidera toodisable protezione, controllare la modalità troppo[pulire le impostazioni di registrazione e protezione](site-recovery-manage-registration-and-protection.md)
