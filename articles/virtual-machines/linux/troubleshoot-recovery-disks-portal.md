---
title: aaaUse una risoluzione dei problemi di macchina virtuale nel portale di Azure hello Linux | Documenti Microsoft
description: Informazioni su come i problemi di macchine virtuali Linux tootroubleshoot tramite connessione hello del sistema operativo disco tooa ripristino VM hello portale di Azure
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM utilizzando hello portale di Azure
Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso. Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente. I dettagli di questo articolo come toouse hello tooconnect portale Azure il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale.

## <a name="recovery-process-overview"></a>Panoramica del processo di ripristino
processo di risoluzione dei problemi di Hello è indicato di seguito:

1. Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.
2. Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.
3. Connettersi toohello risoluzione dei problemi di macchina virtuale. Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.
4. Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.
5. Creare una macchina virtuale con disco rigido virtuale originale di hello.


## <a name="determine-boot-issues"></a>Individuare i problemi di avvio
Esaminare la diagnostica di avvio hello e VM schermata toodetermine perché la macchina virtuale non è in grado di tooboot correttamente. Un esempio comune è una voce non valida in `/etc/fstab`, oppure l'eliminazione o lo spostamento di un disco rigido virtuale sottostante.

Selezionare la macchina virtuale nel portale di hello e quindi scorrere verso il basso toohello **supporto + Troubleshooting** sezione. Fare clic su **diagnostica di avvio** trasmessi i messaggi della console hello tooview dalla VM. Console hello revisione registra toosee se è possibile determinare perché hello VM sta riscontrando un problema. Hello seguente illustra che una macchina virtuale è bloccata in modalità di manutenzione che richiede l'intervento manuale:

![Visualizzazione dei registri della console nella diagnostica di avvio della macchina virtuale](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

È anche possibile fare clic su **schermata** in alto hello di hello Avvio diagnostica log toodownload una cattura di schermata di VM hello.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualizzare i dettagli del disco rigido virtuale esistente
Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD). 

Selezionare il gruppo di risorse dal portale di hello, quindi selezionare l'account di archiviazione. Fare clic su **BLOB**, come illustrato nell'esempio seguente hello:

![Selezionare il BLOB di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

In genere è presente un contenitore denominato **vhds** che contiene i dischi rigidi virtuali. Selezionare hello contenitore tooview un elenco dei dischi rigidi virtuali. Nome della nota hello del disco rigido virtuale (prefisso hello è in genere hello nome della macchina virtuale):

![Identificare il disco rigido virtuale nel contenitore di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Selezionare il disco rigido virtuale esistente dall'elenco di hello e copiare hello URL per l'utilizzo in hello alla procedura seguente:

![Copiare l'URL del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Eliminare la VM esistente
In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte. Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni. Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC). Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale. Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale. lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.

primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso. L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione. Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.

Selezionare la macchina virtuale nel portale di hello, quindi fare clic su **eliminare**:

![Schermata di diagnostica di avvio della macchina virtuale che mostra un errore di avvio](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale. lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Collegare tooanother disco rigido virtuale esistente VM
Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi. Per collegare toothis disco rigido virtuale esistente hello VM toobe in grado di toobrowse di risoluzione dei problemi e modificare il contenuto del disco hello. Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system. Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.

1. Selezionare il gruppo di risorse dal portale di hello, quindi selezionare la macchina virtuale di risoluzione dei problemi. Selezionare **Dischi** e quindi fare clic su **Collega esistente**:

    ![Collegare un disco esistente nel portale di hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect il disco rigido virtuale esistente, fare clic su **File VHD**:

    ![Cercare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Selezionare l'account e il contenitore di archiviazione, quindi fare clic sul disco rigido virtuale esistente. Fare clic su hello **selezionare** pulsante tooconfirm prescelto:

    ![Selezionare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Con il disco rigido virtuale ora selezionato, fare clic su **OK** tooattach hello disco rigido virtuale esistente:

    ![Confermare il collegamento del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Dopo alcuni secondi, hello **dischi** riquadro per la macchina virtuale sono elencati il disco rigido virtuale esistente collegato come disco dati:

    ![Disco rigido virtuale esistente collegato come disco dati](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Montare il disco di dati collegato hello

> [!NOTE]
> Hello negli esempi seguenti in dettaglio i passaggi di hello necessari in una VM Ubuntu. Se si utilizza una distribuzione Linux diversi, ad esempio Red Hat Enterprise Linux o SUSE, hello percorsi dei file di log e `mount` comandi potrebbero essere leggermente diversi. Consultare la documentazione di toohello per la distribuzione specifiche per le modifiche appropriate hello nei comandi.

1. Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour SSH. Se il disco è hello prima dati disco collegato tooyour risoluzione dei problemi di macchina virtuale, è probabilmente connesso troppo`/dev/sdc`. Utilizzare `dmseg` toolist dischi collegati:

    ```bash
    dmesg | grep SCSI
    ```
    Hello l'output è simile toohello seguente esempio:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    In hello sopra riportato, sia su disco del sistema operativo hello `/dev/sda` e disco temporaneo di hello fornito per ogni macchina virtuale è in `/dev/sdb`. Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.

2. Creare una directory toomount il disco rigido virtuale esistente. esempio Hello crea una directory denominata `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Se si dispone di più partizioni sul disco rigido virtuale esistente, è possibile montare partizione hello necessario. esempio Hello Monta prima partizione primaria hello in `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > È consigliabile che i dischi dati toomount nelle macchine virtuali in Azure tramite hello identificatore univoco universale (UUID) del disco rigido virtuale hello. Per questo scenario di risoluzione dei problemi breve, il montaggio hello disco rigido virtuale eseguendo hello UUID non è necessario. Tuttavia, il normale utilizzo, la modifica `/etc/fstab` dischi rigidi virtuali toomount utilizzando il nome di dispositivo anziché potrebbe provocare l'UUID hello tooboot toofail macchina virtuale.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Risolvere i problemi del disco rigido virtuale originale
Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze. Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.

## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Smontare e scollegare il disco rigido virtuale originale
Una volta risolti gli errori, scollegare hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi. È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.

1. Da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale, effettuare lo smontaggio hello disco rigido virtuale esistente. Modificare innanzitutto dalla directory padre hello per il punto di montaggio:

    ```bash
    cd /
    ```

    Smonta ora hello disco rigido virtuale esistente. esempio Hello Smonta dispositivo hello `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello. Selezionare la macchina virtuale nel portale di hello e fare clic su **dischi**. Selezionare il disco rigido virtuale esistente quindi fare clic su **Scollega**:

    ![Scollegare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Attendere hello VM è stato scollegato disco dati hello prima di continuare.

## <a name="create-vm-from-original-hard-disk"></a>Creare una macchina virtuale dal disco rigido originale
utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando. Fare clic su hello **distribuire tooAzure** pulsante come indicato di seguito:

![Distribuire una macchina virtuale da un modello di GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

modello Hello viene caricata in hello portale di Azure per la distribuzione. Immettere un nome hello per la nuova macchina virtuale e le risorse di Azure esistente e incollare hello URL tooyour disco rigido virtuale esistente. distribuzione di hello toobegin, fare clic su **acquisto**:

![Distribuire una macchina virtuale dal modello](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Riabilitare la diagnostica di avvio
Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente. toocheck hello lo stato di diagnostica di avvio e attivare se necessario, selezionare la macchina virtuale nel portale di hello. In **Monitoraggio**, fare clic su **Impostazioni di diagnostica**. Verificare che sia stato hello **su**, e hello segno di spunta accanto troppo**diagnostica di avvio** è selezionata. Se si apportano modifiche, fare clic su **Salva**:

![Aggiornare le impostazioni di diagnostica di avvio](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Per altre informazioni sull'uso di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
