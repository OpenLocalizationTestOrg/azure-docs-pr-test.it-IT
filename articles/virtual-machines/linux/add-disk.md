---
title: Aggiungere un disco a una macchina virtuale Linux con l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Questo articolo illustra come aggiungere un disco permanente alla macchina virtuale Linux con l'interfaccia della riga di comando di Azure 1.0 e 2.0.
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
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a><span data-ttu-id="e2adb-104">Aggiungere un disco a una VM Linux</span><span class="sxs-lookup"><span data-stu-id="e2adb-104">Add a disk to a Linux VM</span></span>
<span data-ttu-id="e2adb-105">Questo articolo illustra come collegare un disco persistente alla VM per poter mantenere i dati, anche se si effettua di nuovo il provisioning della VM per manutenzione o ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e2adb-105">This article shows how to attach a persistent disk to your VM so that you can preserve your data - even if your VM is reprovisioned due to maintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="e2adb-106">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="e2adb-106">Quick Commands</span></span>
<span data-ttu-id="e2adb-107">L'esempio seguente collega un `50`disco GB alla macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e2adb-107">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="e2adb-108">Per usare i dischi gestiti:</span><span class="sxs-lookup"><span data-stu-id="e2adb-108">To use managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="e2adb-109">Per usare i dischi non gestiti:</span><span class="sxs-lookup"><span data-stu-id="e2adb-109">To use unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="e2adb-110">Collegare un disco gestito</span><span class="sxs-lookup"><span data-stu-id="e2adb-110">Attach a managed disk</span></span>

<span data-ttu-id="e2adb-111">L'uso di dischi gestiti consente di concentrarsi sulle macchine virtuali e sui relativi dischi senza doversi preoccupare degli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2adb-111">Using managed disks enables you to focus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="e2adb-112">È possibile creare e collegare rapidamente un disco gestito a una macchina virtuale tramite lo stesso gruppo di risorse di Azure oppure è possibile creare qualsiasi numero di dischi e collegarli.</span><span class="sxs-lookup"><span data-stu-id="e2adb-112">You can quickly create and attach a managed disk to a VM using the same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-to-a-vm"></a><span data-ttu-id="e2adb-113">Collegare un nuovo disco a una VM</span><span class="sxs-lookup"><span data-stu-id="e2adb-113">Attach a new disk to a VM</span></span>

<span data-ttu-id="e2adb-114">Se è necessario solo un nuovo disco nella macchina virtuale, è possibile usare il comando `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-114">If you just need a new disk on your VM, you can use the `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="e2adb-115">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="e2adb-115">Attach an existing disk</span></span> 

<span data-ttu-id="e2adb-116">In molti casi si collegano dischi già creati.</span><span class="sxs-lookup"><span data-stu-id="e2adb-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="e2adb-117">Viene prima trovato l'ID disco, passato in seguito al comando `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-117">You first find the disk id and then pass that to the `az vm disk attach` command.</span></span> <span data-ttu-id="e2adb-118">Nell'esempio seguente viene usato un disco creato con `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-118">The following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="e2adb-119">L'output è simile al seguente (è possibile usare l'opzione `-o table` con qualsiasi comando per formattare l'output):</span><span class="sxs-lookup"><span data-stu-id="e2adb-119">The output looks something like the following (you can use the `-o table` option to any command to format the output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="e2adb-120">Collegare un disco non gestito</span><span class="sxs-lookup"><span data-stu-id="e2adb-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="e2adb-121">Il collegamento di un nuovo disco è un'operazione rapida se non è necessario creare un disco nello stesso account di archiviazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2adb-121">Attaching a new disk is quick if you do not mind creating a disk in the same storage account as your VM.</span></span> <span data-ttu-id="e2adb-122">Digitare `azure vm disk attach-new` per creare e collegare un nuovo disco GB per la VM.</span><span class="sxs-lookup"><span data-stu-id="e2adb-122">Type `azure vm disk attach-new` to create and attach a new GB disk for your VM.</span></span> <span data-ttu-id="e2adb-123">Se non si indica in modo esplicito un account di archiviazione, tutti i dischi creati vengono assegnati allo stesso account di archiviazione in cui si trova il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e2adb-123">If you do not explicitly identify a storage account, any disk you create is placed in the same storage account where your OS disk resides.</span></span> <span data-ttu-id="e2adb-124">L'esempio seguente collega un `50`disco GB alla macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e2adb-124">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="e2adb-125">Connettersi alla VM Linux per montare il nuovo disco</span><span class="sxs-lookup"><span data-stu-id="e2adb-125">Connect to the Linux VM to mount the new disk</span></span>
> [!NOTE]
> <span data-ttu-id="e2adb-126">In questo argomento la connessione a una VM viene effettuata con nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="e2adb-126">This topic connects to a VM using usernames and passwords.</span></span> <span data-ttu-id="e2adb-127">Per usare coppie di chiavi pubbliche e private per comunicare con la VM, vedere [Come usare SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2adb-127">To use public and private key pairs to communicate with your VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="e2adb-128">È necessario SSH nella VM di Azure per partizionare, formattare e montare il nuovo disco in modo che la VM di Linux possa usarlo.</span><span class="sxs-lookup"><span data-stu-id="e2adb-128">You need to SSH into your Azure VM to partition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="e2adb-129">Se non si conoscono le modalità connessione tramite **SSH**, il comando assume il formato `ssh <username>@<FQDNofAzureVM> -p <the ssh port>` e ha l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="e2adb-129">If you're not familiar with connecting with **ssh**, the command takes the form `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, and looks like the following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="e2adb-130">Output</span><span class="sxs-lookup"><span data-stu-id="e2adb-130">Output</span></span>

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="e2adb-131">Ora che si è connessi alla macchina virtuale, si è pronti per collegare un disco.</span><span class="sxs-lookup"><span data-stu-id="e2adb-131">Now that you're connected to your VM, you're ready to attach a disk.</span></span>  <span data-ttu-id="e2adb-132">Trovare prima il disco usando `dmesg | grep SCSI`. Il metodo usato per trovare il nuovo disco può variare.</span><span class="sxs-lookup"><span data-stu-id="e2adb-132">First find the disk, using `dmesg | grep SCSI` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="e2adb-133">In questo caso, avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e2adb-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="e2adb-134">Output</span><span class="sxs-lookup"><span data-stu-id="e2adb-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="e2adb-135">e, nel caso di questo argomento, il disco `sdc` è il disco desiderato.</span><span class="sxs-lookup"><span data-stu-id="e2adb-135">and in the case of this topic, the `sdc` disk is the one that we want.</span></span> <span data-ttu-id="e2adb-136">Eseguire ora la partizione del disco con `sudo fdisk /dev/sdc`. Presupponendo che in questo caso il disco sia `sdc`, renderlo un disco principale nella partizione 1 e accettare le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e2adb-136">Now partition the disk with `sudo fdisk /dev/sdc` -- assuming that in your case the disk was `sdc`, and make it a primary disk on partition 1, and accept the other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="e2adb-137">Output</span><span class="sxs-lookup"><span data-stu-id="e2adb-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

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

<span data-ttu-id="e2adb-138">Creare la partizione digitando `p` al prompt:</span><span class="sxs-lookup"><span data-stu-id="e2adb-138">Create the partition by typing `p` at the prompt:</span></span>

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
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="e2adb-139">E scrivere un file system nella partizione usando il comando **mkfs** , specificando il tipo di file system e il nome del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2adb-139">And write a file system to the partition by using the **mkfs** command, specifying your filesystem type and the device name.</span></span> <span data-ttu-id="e2adb-140">In questo argomento, vengono usati `ext4` e `/dev/sdc1` riportati sopra:</span><span class="sxs-lookup"><span data-stu-id="e2adb-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="e2adb-141">Output</span><span class="sxs-lookup"><span data-stu-id="e2adb-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
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

<span data-ttu-id="e2adb-142">Creare ora una directory per montare il nuovo file system usando `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="e2adb-142">Now we create a directory to mount the file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="e2adb-143">E montare la directory usando `mount`:</span><span class="sxs-lookup"><span data-stu-id="e2adb-143">And you mount the directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="e2adb-144">Il disco dati è ora pronto per l'uso come `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-144">The data disk is now ready to use as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="e2adb-145">Output</span><span class="sxs-lookup"><span data-stu-id="e2adb-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="e2adb-146">Per assicurarsi che l'unità venga rimontata automaticamente dopo un riavvio, è necessario aggiungerla al file /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="e2adb-146">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="e2adb-147">È anche consigliabile che l'UUID (Universally Unique IDentifier) usato in /etc/fstab faccia riferimento all'unità anziché al solo nome del dispositivo, ad esempio `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-147">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="e2adb-148">Se il sistema operativo rileva un errore del disco durante l'avvio, l'uso di UUID evita che venga montato il disco non corretto in una posizione specificata.</span><span class="sxs-lookup"><span data-stu-id="e2adb-148">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="e2adb-149">Ai dischi dati rimanenti verrebbero quindi assegnati gli stessi ID di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2adb-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="e2adb-150">Per individuare l'UUID della nuova unità, usare l'utilità **blkid** :</span><span class="sxs-lookup"><span data-stu-id="e2adb-150">To find the UUID of the new drive, use the **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="e2adb-151">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e2adb-151">The output looks similar to the following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="e2adb-152">Se il file **/etc/fstab** non viene modificato in modo corretto, il sistema potrebbe diventare non avviabile.</span><span class="sxs-lookup"><span data-stu-id="e2adb-152">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="e2adb-153">In caso di dubbi, fare riferimento alla documentazione della distribuzione per informazioni su come modificare correttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="e2adb-153">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="e2adb-154">È inoltre consigliabile creare una copia di backup del file /etc/fstab prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="e2adb-154">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="e2adb-155">Successivamente, aprire il file **/etc/fstab** in un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="e2adb-155">Next, open the **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="e2adb-156">In questo esempio viene usato il valore UUID del nuovo dispositivo **/dev/sdc1** creato nei passaggi precedenti e il punto di montaggio **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="e2adb-156">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="e2adb-157">Alla fine del file **/etc/fstab** aggiungere la riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e2adb-157">Add the following line to the end of the **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="e2adb-158">Se si rimuove successivamente un disco dati senza modificare fstab, è possibile che si verifichi un errore di avvio della VM.</span><span class="sxs-lookup"><span data-stu-id="e2adb-158">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="e2adb-159">La maggior parte delle distribuzioni offre le opzioni fstab `nofail` e/o `nobootwait`.</span><span class="sxs-lookup"><span data-stu-id="e2adb-159">Most distributions provide either the `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="e2adb-160">Queste opzioni consentono l'avvio di un sistema anche se il montaggio del disco non riesce in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="e2adb-160">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="e2adb-161">Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e2adb-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="e2adb-162">L'opzione **nofail** garantisce che l'avvio della VM anche se il file system è danneggiato o se non è presente il disco in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="e2adb-162">The **nofail** option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="e2adb-163">Senza questa opzione potrebbero verificarsi comportamenti come quelli descritti in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Impossibile eseguire una connessione SSH a VM Linux a causa di errori FSTAB).</span><span class="sxs-lookup"><span data-stu-id="e2adb-163">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="e2adb-164">Supporto delle funzioni TRIM/UNMAP per Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="e2adb-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="e2adb-165">Alcuni kernel di Linux supportano operazioni TRIM/UNMAP allo scopo di rimuovere i blocchi inutilizzati sul disco.</span><span class="sxs-lookup"><span data-stu-id="e2adb-165">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="e2adb-166">Nel servizio di archiviazione standard, questa caratteristica è particolarmente utile per informare Azure che le pagine eliminate non sono più valide e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="e2adb-166">This is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="e2adb-167">Così facendo, è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="e2adb-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="e2adb-168">Esistono due modi per abilitare la funzione TRIM in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="e2adb-168">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="e2adb-169">Come di consueto, consultare la documentazione della distribuzione per stabilire l'approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="e2adb-169">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="e2adb-170">Usare l'opzione di montaggio `discard` in `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2adb-170">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="e2adb-171">In alcuni casi l'opzione `discard` può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e2adb-171">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="e2adb-172">In alternativa, è possibile eseguire il comando `fstrim` manualmente dalla riga di comando oppure aggiungerlo a crontab per eseguirlo a intervalli regolari:</span><span class="sxs-lookup"><span data-stu-id="e2adb-172">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="e2adb-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e2adb-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="e2adb-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="e2adb-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="e2adb-175">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e2adb-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="e2adb-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2adb-176">Next Steps</span></span>
* <span data-ttu-id="e2adb-177">Tenere presente che il nuovo disco non è disponibile per la VM se la macchina virtuale viene riavviata, a meno che non si scrivano queste informazioni nel file [fstab](http://en.wikipedia.org/wiki/Fstab) .</span><span class="sxs-lookup"><span data-stu-id="e2adb-177">Remember, that your new disk is not available to the VM if it reboots unless you write that information to your [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="e2adb-178">Per assicurarsi che la VM di Linux sia configurata correttamente, vedere le raccomandazioni per [ottimizzare le prestazioni della macchina virtuale di Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="e2adb-178">To ensure your Linux VM is configured correctly, review the [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="e2adb-179">Espandere la capacità di archiviazione aggiungendo altri dischi e [configurare RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e2adb-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

