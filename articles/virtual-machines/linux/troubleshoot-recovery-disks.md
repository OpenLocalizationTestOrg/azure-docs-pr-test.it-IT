---
title: aaaUse una risoluzione dei problemi di VM con hello Azure CLI 2.0 Linux | Documenti Microsoft
description: Informazioni su come tootroubleshoot VM Linux problemi tramite connessione hello del sistema operativo disco tooa ripristino VM hello Azure CLI 2.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino tooa hello del sistema operativo del disco VM con hello Azure CLI 2.0
Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso. Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente. I dettagli di questo articolo come toouse hello tooconnect CLI di Azure 2.0 il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Panoramica del processo di ripristino
processo di risoluzione dei problemi di Hello è indicato di seguito:

1. Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.
2. Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.
3. Connettersi toohello risoluzione dei problemi di macchina virtuale. Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.
4. Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.
5. Creare una macchina virtuale con disco rigido virtuale originale di hello.

tooperform passaggi di risoluzione dei problemi è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.


## <a name="determine-boot-issues"></a>Individuare i problemi di avvio
Esaminare hello output seriale toodetermine perché la macchina virtuale non è in grado di tooboot correttamente. Un esempio comune è una voce non valida in `/etc/fstab`, o hello sottostante il disco rigido virtuale viene eliminato o spostato.

Ottenere i log di avvio hello con [az vm get diagnostica di avvio-avvio-log](/cli/azure/vm/boot-diagnostics#get-boot-log). Hello seguente esempio mostra come ottenere output seriale hello dalla macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Esaminare hello output seriale toodetermine hello VM motivi tooboot. Se l'output di hello seriale non fornisce alcuna indicazione, potrebbe essere necessario tooreview i file di log in `/var/log` dopo aver hello virtuale disco rigido connesso tooa risoluzione dei problemi di macchina virtuale.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualizzare i dettagli del disco rigido virtuale esistente
Prima di collegare la macchina virtuale di tooanother di disco rigido virtuale (VHD), è necessario tooidentify hello URI del disco del sistema operativo hello. 

Visualizzare le informazioni sulla macchina virtuale con il comando [az vm show](/cli/azure/vm#show). Hello utilizzare `--query` disco toohello del sistema operativo di flag tooextract hello URI. esempio Hello Ottiene informazioni sul disco per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Hello URI è simile a troppo**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Eliminare la VM esistente
In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte. Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni. Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC). Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale. Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale. lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.

primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso. L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione. Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.

Elimina macchina virtuale con hello [az vm eliminare](/cli/azure/vm#delete). Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale. lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Collegare tooanother disco rigido virtuale esistente VM
Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi. Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello. Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system. Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.

Collegare hello disco rigido virtuale esistente con [az disco macchina virtuale non gestita-collegare](/cli/azure/vm/unmanaged-disk#attach). Quando si collega hello disco rigido virtuale esistente, specificare disco toohello URI hello ottenuto in precedenza hello `az vm show` comando. esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Montare il disco di dati collegato hello

> [!NOTE]
> Hello negli esempi seguenti in dettaglio i passaggi di hello necessari in una VM Ubuntu. Se si utilizza una distribuzione Linux diversi, ad esempio Red Hat Enterprise Linux o SUSE, hello percorsi dei file di log e `mount` comandi potrebbero essere leggermente diversi. Consultare la documentazione di toohello per la distribuzione specifiche per le modifiche appropriate hello nei comandi.

1. Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour SSH. Se il disco è hello prima dati disco collegato tooyour risoluzione dei problemi di macchina virtuale, disco hello è probabilmente connesso troppo`/dev/sdc`. Utilizzare `dmseg` tooview dischi collegati:

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
Una volta risolti gli errori, si smontare e Scollega hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi. È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.

1. Da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale, effettuare lo smontaggio hello disco rigido virtuale esistente. Modificare innanzitutto dalla directory padre hello per il punto di montaggio:

    ```bash
    cd /
    ```

    Smonta ora hello disco rigido virtuale esistente. esempio Hello Smonta dispositivo hello `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello. Uscire da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale. Hello elenco collegato tooyour dischi dati risoluzione dei problemi di macchina virtuale con [elenco disco non gestita di vm az](/cli/azure/vm/unmanaged-disk#list). gli elenchi di hello dischi dati di esempio seguente Hello collegato toohello macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Si noti il nome di hello per il disco rigido virtuale esistente. Ad esempio, il nome di hello di un disco con hello URI di **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** è **myVHD**. 

    Scollegare il disco dati hello dalla VM [az vm non gestita disco scollegare](/cli/azure/vm/unmanaged-disk#detach). esempio Hello Scollega disco hello denominato `myVHD` dalla macchina virtuale denominata hello `myVMRecovery` in hello `myResourceGroup` gruppo di risorse:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creare una macchina virtuale dal disco rigido originale
utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modello JSON effettivi Hello è hello link riportato di seguito:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

modello Hello distribuisce una macchina virtuale tramite hello URI VHD da hello in precedenza di comando. Distribuire il modello di hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create). Fornire hello URI tooyour disco rigido virtuale originale e quindi specificare il tipo di hello del sistema operativo, dimensioni della macchina virtuale e nome della macchina virtuale come segue:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Riabilitare la diagnostica di avvio
Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente. Abilitare la diagnostica di avvio con il comando [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable). esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myDeployedVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
