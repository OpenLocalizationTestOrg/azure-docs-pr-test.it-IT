---
title: una VM tooLinux disco tramite aaaAdd hello CLI di Azure | Documenti Microsoft
description: Informazioni su tooadd tooyour un disco permanente VM Linux con hello Azure CLI 1.0 e 2.0.
keywords: macchina virtuale Linux, aggiungere un disco di risorse
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>Aggiungere un tooa disco VM Linux
Questo articolo illustra come tooattach un permanente disco tooyour macchina virtuale in modo che è possibile mantenere i dati, anche se la macchina virtuale reprovisioning scadenza toomaintenance o ridimensionamento. 

## <a name="quick-commands"></a>Comandi rapidi
Hello seguente esempio associa un `50`GB disco toohello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

toouse dischi gestiti:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

dischi toouse non gestita:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Collegare un disco gestito

Utilizzo di dischi gestiti consente toofocus le macchine virtuali e i relativi dischi senza doversi preoccupare degli account di archiviazione di Azure. È possibile creare e collegare un disco gestito rapidamente tooa VM utilizzando hello nello stesso gruppo di risorse di Azure oppure è possibile creare qualsiasi numero di dischi e quindi collegarli.


### <a name="attach-a-new-disk-tooa-vm"></a>Collegare un nuovo tooa disco VM

Se è necessario un nuovo disco nella macchina virtuale, è possibile utilizzare hello `az vm disk attach` comando.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Collegare un disco esistente 

In molti casi si collegano dischi già creati. È innanzitutto individuare l'id disco hello e quindi passare tale toohello `az vm disk attach` comando. esempio Hello utilizza un disco creato con `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Hello output sarà simile alla seguente hello (è possibile utilizzare hello `-o table` opzione tooany comando tooformat hello output):

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a>Collegare un disco non gestito

Collegamento di un nuovo disco risulta più rapida se non è importante creare un disco in hello stesso account di archiviazione della macchina virtuale. Tipo `azure vm disk attach-new` toocreate e collegare un nuovo disco GB per la macchina virtuale. Se non si identificano in modo esplicito un account di archiviazione, qualsiasi disco creato viene inserito nella hello stesso account di archiviazione in cui risiede il disco del sistema operativo. Hello seguente esempio associa un `50`GB disco toohello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Connettersi di nuovo disco VM Linux toomount hello toohello
> [!NOTE]
> In questo argomento si connette tooa VM utilizzando nomi utente e password. toouse coppie di chiavi pubbliche e private toocommunicate con la macchina virtuale, vedere [come tooUse SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

È necessario tooSSH in toopartition la macchina virtuale di Azure, formattare e montare il nuovo disco in modo che le VM Linux possono utilizzarlo. Se non si ha familiarità con la connessione con **ssh**, comando hello hello formato `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`e simile hello seguente:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Output

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

Ora che si è connessi tooyour macchina virtuale, si è pronti tooattach un disco.  Prima di tutto trovare hello disco, utilizzando `dmesg | grep SCSI` (metodo hello è utilizzare toodiscover il nuovo disco può variare). In questo caso, avrà un aspetto simile al seguente:

```bash
dmesg | grep SCSI
```

Output

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

e nel caso di hello di questo argomento, hello `sdc` disco è hello quello che si desidera. Ora la partizione hello disco con `sudo fdisk /dev/sdc` , supponendo che il case hello disco è `sdc`e renderlo un disco primario nella partizione 1 e di accettare hello altre impostazioni predefinite.

```bash
sudo fdisk /dev/sdc
```

Output

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

Creare una partizione hello digitando `p` al prompt dei comandi hello:

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

E la scrittura di una partizione toohello utilizzando hello **mkfs** comando, specificando il nome del dispositivo filesystem hello e di tipo. In questo argomento, vengono usati `ext4` e `/dev/sdc1` riportati sopra:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Output

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

Ora è creare una directory toomount hello file system utilizzando `mkdir`:

```bash
sudo mkdir /datadrive
```

E si monta hello directory utilizzando `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

disco dati Hello è ora pronto toouse come `/datadrive`.

```bash
ls
```

Output

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

unità di hello tooensure viene rimontato automaticamente dopo un riavvio del sistema che deve essere aggiunto file /etc/fstab. toohello. Inoltre, è consigliabile che hello UUID (Universally Unique IDentifier) è utilizzato in /etc/hosts/fstab toorefer toohello unità anziché il nome di dispositivo hello solo (ad esempio, `/dev/sdc1`). Se hello del sistema operativo rileva un errore del disco durante l'avvio, l'utilizzo di hello UUID evita disco non corretta di hello viene montato tooa percorso specificato. Ai dischi dati rimanenti verrebbero quindi assegnati gli stessi ID di dispositivo. toofind hello UUID della nuova unità hello, utilizzare hello **ID blocco** utilità:

```bash
sudo -i blkid
```

output di Hello è simile toohello seguenti:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Modifica in modo non corretto di hello **/e così via/fstab** file potrebbe causare un avvio del sistema. In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file. È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.
> 
> 

Aprire quindi hello **/e così via/fstab** file in un editor di testo:

```bash
sudo vi /etc/fstab
```

In questo esempio, si utilizza hello UUID valore per hello nuovo **dev/sdc1** dispositivo che è stato creato in precedenza hello e punto di montaggio hello **/datadrive**. Aggiungere hello successivo toohello riga alla fine di hello **/e così via/fstab** file:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Rimozione di un disco dati in un secondo momento senza dover modificare fstab potrebbe causare hello VM toofail tooboot. La maggior parte delle distribuzioni forniscono entrambi hello `nofail` e/o `nobootwait` fstab opzioni. Queste opzioni consentono di tooboot un sistema anche se il disco di hello, toomount non riesce in fase di avvio. Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.
> 
> Hello **nofail** opzione assicura che hello VM viene avviata anche se filesystem hello è danneggiato o hello disco non esiste in fase di avvio. Senza questa opzione, si verifichino comportamento come descritto in [non SSH tooLinux VM a causa di errori tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Supporto delle funzioni TRIM/UNMAP per Linux in Azure
Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello. Ciò risulta particolarmente utile in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate. Così facendo, è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.

Esistono due modi tooenable TRIM supportano le VM Linux. Come al solito, consultare la distribuzione hello approccio consigliato:

* Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni. In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Passaggi successivi
* Tenere presente che il nuovo disco non è disponibile toohello VM se il riavvio venga eseguito a meno che non si scrive tale tooyour informazioni [fstab](http://en.wikipedia.org/wiki/Fstab) file.
* tooensure VM Linux è configurato correttamente, esaminare hello [ottimizzare le prestazioni di computer Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) indicazioni.
* Espandere la capacità di archiviazione aggiungendo altri dischi e [configurare RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per migliorare le prestazioni.

