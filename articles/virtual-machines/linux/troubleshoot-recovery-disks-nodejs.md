---
title: aaaUse una risoluzione dei problemi di VM con hello Azure CLI 1.0 Linux | Documenti Microsoft
description: Informazioni su come tootroubleshoot VM Linux problemi tramite connessione hello del sistema operativo disco tooa ripristino VM hello Azure CLI 1.0
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
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM utilizzando hello Azure CLI 1.0
Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso. Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente. I dettagli di questo articolo come toouse hello tooconnect CLI di Azure 1.0 il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale.


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#recovery-process-overview) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="recovery-process-overview"></a>Panoramica del processo di ripristino
processo di risoluzione dei problemi di Hello è indicato di seguito:

1. Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.
2. Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.
3. Connettersi toohello risoluzione dei problemi di macchina virtuale. Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.
4. Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.
5. Creare una macchina virtuale con disco rigido virtuale originale di hello.

Assicurarsi di aver [hello più recente di Azure CLI 1.0](../../cli-install-nodejs.md) installati e registrati e utilizza la modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.


## <a name="determine-boot-issues"></a>Individuare i problemi di avvio
Esaminare hello output seriale toodetermine perché la macchina virtuale non è in grado di tooboot correttamente. Un esempio comune è una voce non valida in `/etc/fstab`, o hello sottostante il disco rigido virtuale viene eliminato o spostato.

Hello seguente esempio mostra come ottenere output seriale hello dalla macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Esaminare hello output seriale toodetermine hello VM motivi tooboot. Se l'output di hello seriale non fornisce alcuna indicazione, potrebbe essere necessario tooreview i file di log in `/var/log` dopo aver hello virtuale disco rigido connesso tooa risoluzione dei problemi di macchina virtuale.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualizzare i dettagli del disco rigido virtuale esistente
Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD). 

Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Cercare `Vhd URI` nell'output di hello da hello precedente comando. output di esempio troncato seguente Hello Mostra hello `Vhd URI` ultima riga hello:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Eliminare la VM esistente
In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte. Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni. Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC). Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale. Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale. lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.

primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso. L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione. Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.

Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale. lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Collegare tooanother disco rigido virtuale esistente VM
Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi. Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello. Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system. Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.

Quando si collega hello disco rigido virtuale esistente, specificare disco toohello di URL hello ottenuto in precedenza hello `azure vm show` comando. esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
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

2. Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello. Uscire da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale. In hello CLI di Azure, hello elenco primo allegato tooyour dischi dati risoluzione dei problemi di macchina virtuale. gli elenchi di hello dischi dati di esempio seguente Hello collegato toohello macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Hello nota `Lun` valore per il disco rigido virtuale esistente. Hello output di comando di esempio seguente mostra hello disco virtuale collegato al LUN 0:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Scollegare il disco dati hello dalla VM utilizzando hello applicabile `Lun` valore:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creare una macchina virtuale dal disco rigido originale
utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modello JSON effettivi Hello è hello link riportato di seguito:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando. esempio Hello distribuisce hello modello toohello gruppo di risorse `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Hello risposta richiesto per il modello di hello ad esempio nome della macchina virtuale (`myDeployedVM` hello seguente esempio), tipo di sistema operativo (`Linux`) e le dimensioni di macchina virtuale (`Standard_DS1_v2`). Hello `osDiskVhdUri` è hello stesso utilizzato in precedenza durante l'associazione toohello disco rigido virtuale esistente hello risoluzione dei problemi di macchina virtuale. Un esempio di output del comando hello e richieste è il seguente:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Riabilitare la diagnostica di avvio

Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente. esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myDeployedVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
