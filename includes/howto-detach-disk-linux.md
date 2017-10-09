<span data-ttu-id="f33d2-101">Quando non è più necessario un disco dati collegato tooa virtual machine (VM), è possibile scollegarlo facilmente.</span><span class="sxs-lookup"><span data-stu-id="f33d2-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="f33d2-102">Quando si scollega un disco da hello VM, hello disco non è stato rimosso dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="f33d2-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="f33d2-103">Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.</span><span class="sxs-lookup"><span data-stu-id="f33d2-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="f33d2-104">Una macchina virtuale in Azure usa diversi tipi di dischi, ad esempio un disco del sistema operativo, un disco temporaneo locale e un disco dati facoltativo.</span><span class="sxs-lookup"><span data-stu-id="f33d2-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="f33d2-105">Per informazioni dettagliate, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f33d2-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f33d2-106">A meno che non si elimina anche hello VM non è possibile scollegare un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f33d2-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="f33d2-107">Trovare il disco hello</span><span class="sxs-lookup"><span data-stu-id="f33d2-107">Find hello disk</span></span>
<span data-ttu-id="f33d2-108">Prima di poter scollegare un disco da una macchina virtuale è necessario toofind out hello numero LUN, che è un identificatore hello disco toobe scollegato.</span><span class="sxs-lookup"><span data-stu-id="f33d2-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="f33d2-109">toodo che, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f33d2-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="f33d2-110">Aprire l'interfaccia CLI di Azure e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f33d2-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="f33d2-111">Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="f33d2-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="f33d2-112">Individuare i dischi collegati tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f33d2-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="f33d2-113">Hello esempio seguente vengono elencati i dischi per la macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f33d2-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="f33d2-114">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="f33d2-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="f33d2-115">Si noti hello LUN o hello **numero di unità logica** per disco hello che si desidera toodetach.</span><span class="sxs-lookup"><span data-stu-id="f33d2-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="f33d2-116">Rimuovere il disco di sistema operativo riferimenti toohello</span><span class="sxs-lookup"><span data-stu-id="f33d2-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="f33d2-117">Prima di scollegare il disco hello Guest Linux hello, è necessario assicurarsi che tutte le partizioni disco hello non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="f33d2-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="f33d2-118">Verificare che il sistema operativo hello non tooremount loro dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="f33d2-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="f33d2-119">Questi passaggi Annulla configurazione hello probabilmente creato quando [collegamento](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco hello.</span><span class="sxs-lookup"><span data-stu-id="f33d2-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="f33d2-120">Hello utilizzare `lsscsi` identificatore di comando toodiscover hello del disco.</span><span class="sxs-lookup"><span data-stu-id="f33d2-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="f33d2-121">`lsscsi` può essere installato tramite `yum install lsscsi` (su distribuzioni basate su Red Hat) o `apt-get install lsscsi` (su distribuzioni basate su Debian).</span><span class="sxs-lookup"><span data-stu-id="f33d2-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="f33d2-122">È possibile trovare l'identificatore del disco hello desiderata utilizzando il numero LUN hello.</span><span class="sxs-lookup"><span data-stu-id="f33d2-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="f33d2-123">ultimo numero di Hello nella tupla hello in ogni riga è hello LUN.</span><span class="sxs-lookup"><span data-stu-id="f33d2-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="f33d2-124">Nel seguente esempio di hello `lsscsi`, LUN 0 esegue il mapping troppo*dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="f33d2-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="f33d2-125">Utilizzare `fdisk -l <disk>` partizioni hello toodiscover associate hello disco toobe scollegato.</span><span class="sxs-lookup"><span data-stu-id="f33d2-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="f33d2-126">esempio Hello Mostra output di hello per `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="f33d2-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="f33d2-127">Smonta ogni partizione per disco hello.</span><span class="sxs-lookup"><span data-stu-id="f33d2-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="f33d2-128">Smonta Hello esempio `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f33d2-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="f33d2-129">Hello utilizzare `blkid` comando toodiscovery hello UUID per tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="f33d2-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="f33d2-130">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="f33d2-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="f33d2-131">Rimuovere le voci in hello **/e così via/fstab** file associato con i percorsi di dispositivo hello o UUID per tutte le partizioni per hello disco toobe scollegato.</span><span class="sxs-lookup"><span data-stu-id="f33d2-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="f33d2-132">Le voci per questo esempio potrebbero essere:</span><span class="sxs-lookup"><span data-stu-id="f33d2-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="f33d2-133">oppure</span><span class="sxs-lookup"><span data-stu-id="f33d2-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="f33d2-134">Scollegare il disco hello</span><span class="sxs-lookup"><span data-stu-id="f33d2-134">Detach hello disk</span></span>
<span data-ttu-id="f33d2-135">Dopo aver trovato il numero LUN hello del disco di hello e i riferimenti del sistema operativo hello rimosso, si è pronti toodetach è:</span><span class="sxs-lookup"><span data-stu-id="f33d2-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="f33d2-136">Scollegare il disco selezionato di hello dalla macchina virtuale hello eseguendo il comando hello `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="f33d2-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="f33d2-137">Nell'esempio seguente viene Hello scollegato LUN `0` dalla macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f33d2-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="f33d2-138">È possibile verificare se il disco hello ottenuto disconnessa eseguendo `azure vm disk list` nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f33d2-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="f33d2-139">Hello seguente esempio viene controllato hello macchina virtuale denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f33d2-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="f33d2-140">l'output è simile toohello seguente esempio, disco dati hello non è più allegato Hello:</span><span class="sxs-lookup"><span data-stu-id="f33d2-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="f33d2-141">disco Hello scollegato rimane nel servizio di archiviazione ma non è più macchine virtuali tooa associata.</span><span class="sxs-lookup"><span data-stu-id="f33d2-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

