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
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="ea159-104">Aggiungere un tooa disco VM Linux</span><span class="sxs-lookup"><span data-stu-id="ea159-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="ea159-105">Questo articolo illustra come tooattach un permanente disco tooyour macchina virtuale in modo che è possibile mantenere i dati, anche se la macchina virtuale reprovisioning scadenza toomaintenance o ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="ea159-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="ea159-106">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="ea159-106">Quick Commands</span></span>
<span data-ttu-id="ea159-107">Hello seguente esempio associa un `50`GB disco toohello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ea159-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="ea159-108">toouse dischi gestiti:</span><span class="sxs-lookup"><span data-stu-id="ea159-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="ea159-109">dischi toouse non gestita:</span><span class="sxs-lookup"><span data-stu-id="ea159-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="ea159-110">Collegare un disco gestito</span><span class="sxs-lookup"><span data-stu-id="ea159-110">Attach a managed disk</span></span>

<span data-ttu-id="ea159-111">Utilizzo di dischi gestiti consente toofocus le macchine virtuali e i relativi dischi senza doversi preoccupare degli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea159-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="ea159-112">È possibile creare e collegare un disco gestito rapidamente tooa VM utilizzando hello nello stesso gruppo di risorse di Azure oppure è possibile creare qualsiasi numero di dischi e quindi collegarli.</span><span class="sxs-lookup"><span data-stu-id="ea159-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="ea159-113">Collegare un nuovo tooa disco VM</span><span class="sxs-lookup"><span data-stu-id="ea159-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="ea159-114">Se è necessario un nuovo disco nella macchina virtuale, è possibile utilizzare hello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="ea159-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="ea159-115">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="ea159-115">Attach an existing disk</span></span> 

<span data-ttu-id="ea159-116">In molti casi si collegano dischi già creati.</span><span class="sxs-lookup"><span data-stu-id="ea159-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="ea159-117">È innanzitutto individuare l'id disco hello e quindi passare tale toohello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="ea159-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="ea159-118">esempio Hello utilizza un disco creato con `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="ea159-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="ea159-119">Hello output sarà simile alla seguente hello (è possibile utilizzare hello `-o table` opzione tooany comando tooformat hello output):</span><span class="sxs-lookup"><span data-stu-id="ea159-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="ea159-120">Collegare un disco non gestito</span><span class="sxs-lookup"><span data-stu-id="ea159-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="ea159-121">Collegamento di un nuovo disco risulta più rapida se non è importante creare un disco in hello stesso account di archiviazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ea159-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="ea159-122">Tipo `azure vm disk attach-new` toocreate e collegare un nuovo disco GB per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ea159-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="ea159-123">Se non si identificano in modo esplicito un account di archiviazione, qualsiasi disco creato viene inserito nella hello stesso account di archiviazione in cui risiede il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ea159-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="ea159-124">Hello seguente esempio associa un `50`GB disco toohello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ea159-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="ea159-125">Connettersi di nuovo disco VM Linux toomount hello toohello</span><span class="sxs-lookup"><span data-stu-id="ea159-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="ea159-126">In questo argomento si connette tooa VM utilizzando nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="ea159-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="ea159-127">toouse coppie di chiavi pubbliche e private toocommunicate con la macchina virtuale, vedere [come tooUse SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea159-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="ea159-128">È necessario tooSSH in toopartition la macchina virtuale di Azure, formattare e montare il nuovo disco in modo che le VM Linux possono utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="ea159-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="ea159-129">Se non si ha familiarità con la connessione con **ssh**, comando hello hello formato `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`e simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ea159-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="ea159-130">Output</span><span class="sxs-lookup"><span data-stu-id="ea159-130">Output</span></span>

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

<span data-ttu-id="ea159-131">Ora che si è connessi tooyour macchina virtuale, si è pronti tooattach un disco.</span><span class="sxs-lookup"><span data-stu-id="ea159-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="ea159-132">Prima di tutto trovare hello disco, utilizzando `dmesg | grep SCSI` (metodo hello è utilizzare toodiscover il nuovo disco può variare).</span><span class="sxs-lookup"><span data-stu-id="ea159-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="ea159-133">In questo caso, avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ea159-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="ea159-134">Output</span><span class="sxs-lookup"><span data-stu-id="ea159-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="ea159-135">e nel caso di hello di questo argomento, hello `sdc` disco è hello quello che si desidera.</span><span class="sxs-lookup"><span data-stu-id="ea159-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="ea159-136">Ora la partizione hello disco con `sudo fdisk /dev/sdc` , supponendo che il case hello disco è `sdc`e renderlo un disco primario nella partizione 1 e di accettare hello altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="ea159-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="ea159-137">Output</span><span class="sxs-lookup"><span data-stu-id="ea159-137">Output</span></span>

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

<span data-ttu-id="ea159-138">Creare una partizione hello digitando `p` al prompt dei comandi hello:</span><span class="sxs-lookup"><span data-stu-id="ea159-138">Create hello partition by typing `p` at hello prompt:</span></span>

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

<span data-ttu-id="ea159-139">E la scrittura di una partizione toohello utilizzando hello **mkfs** comando, specificando il nome del dispositivo filesystem hello e di tipo.</span><span class="sxs-lookup"><span data-stu-id="ea159-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="ea159-140">In questo argomento, vengono usati `ext4` e `/dev/sdc1` riportati sopra:</span><span class="sxs-lookup"><span data-stu-id="ea159-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="ea159-141">Output</span><span class="sxs-lookup"><span data-stu-id="ea159-141">Output</span></span>

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

<span data-ttu-id="ea159-142">Ora è creare una directory toomount hello file system utilizzando `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="ea159-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="ea159-143">E si monta hello directory utilizzando `mount`:</span><span class="sxs-lookup"><span data-stu-id="ea159-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="ea159-144">disco dati Hello è ora pronto toouse come `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="ea159-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="ea159-145">Output</span><span class="sxs-lookup"><span data-stu-id="ea159-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="ea159-146">unità di hello tooensure viene rimontato automaticamente dopo un riavvio del sistema che deve essere aggiunto file /etc/fstab. toohello.</span><span class="sxs-lookup"><span data-stu-id="ea159-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="ea159-147">Inoltre, è consigliabile che hello UUID (Universally Unique IDentifier) è utilizzato in /etc/hosts/fstab toorefer toohello unità anziché il nome di dispositivo hello solo (ad esempio, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="ea159-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="ea159-148">Se hello del sistema operativo rileva un errore del disco durante l'avvio, l'utilizzo di hello UUID evita disco non corretta di hello viene montato tooa percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="ea159-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="ea159-149">Ai dischi dati rimanenti verrebbero quindi assegnati gli stessi ID di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ea159-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="ea159-150">toofind hello UUID della nuova unità hello, utilizzare hello **ID blocco** utilità:</span><span class="sxs-lookup"><span data-stu-id="ea159-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="ea159-151">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea159-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="ea159-152">Modifica in modo non corretto di hello **/e così via/fstab** file potrebbe causare un avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="ea159-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="ea159-153">In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="ea159-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="ea159-154">È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="ea159-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="ea159-155">Aprire quindi hello **/e così via/fstab** file in un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="ea159-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="ea159-156">In questo esempio, si utilizza hello UUID valore per hello nuovo **dev/sdc1** dispositivo che è stato creato in precedenza hello e punto di montaggio hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="ea159-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="ea159-157">Aggiungere hello successivo toohello riga alla fine di hello **/e così via/fstab** file:</span><span class="sxs-lookup"><span data-stu-id="ea159-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="ea159-158">Rimozione di un disco dati in un secondo momento senza dover modificare fstab potrebbe causare hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="ea159-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="ea159-159">La maggior parte delle distribuzioni forniscono entrambi hello `nofail` e/o `nobootwait` fstab opzioni.</span><span class="sxs-lookup"><span data-stu-id="ea159-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="ea159-160">Queste opzioni consentono di tooboot un sistema anche se il disco di hello, toomount non riesce in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="ea159-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="ea159-161">Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ea159-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="ea159-162">Hello **nofail** opzione assicura che hello VM viene avviata anche se filesystem hello è danneggiato o hello disco non esiste in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="ea159-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="ea159-163">Senza questa opzione, si verifichino comportamento come descritto in [non SSH tooLinux VM a causa di errori tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="ea159-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="ea159-164">Supporto delle funzioni TRIM/UNMAP per Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="ea159-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="ea159-165">Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello.</span><span class="sxs-lookup"><span data-stu-id="ea159-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="ea159-166">Ciò risulta particolarmente utile in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="ea159-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="ea159-167">Così facendo, è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="ea159-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="ea159-168">Esistono due modi tooenable TRIM supportano le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="ea159-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="ea159-169">Come al solito, consultare la distribuzione hello approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="ea159-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="ea159-170">Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ea159-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="ea159-171">In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ea159-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="ea159-172">In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:</span><span class="sxs-lookup"><span data-stu-id="ea159-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="ea159-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ea159-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="ea159-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="ea159-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="ea159-175">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ea159-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="ea159-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea159-176">Next Steps</span></span>
* <span data-ttu-id="ea159-177">Tenere presente che il nuovo disco non è disponibile toohello VM se il riavvio venga eseguito a meno che non si scrive tale tooyour informazioni [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span><span class="sxs-lookup"><span data-stu-id="ea159-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="ea159-178">tooensure VM Linux è configurato correttamente, esaminare hello [ottimizzare le prestazioni di computer Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) indicazioni.</span><span class="sxs-lookup"><span data-stu-id="ea159-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="ea159-179">Espandere la capacità di archiviazione aggiungendo altri dischi e [configurare RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ea159-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

