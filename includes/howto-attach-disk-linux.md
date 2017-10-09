
<span data-ttu-id="dc623-101">Per altre informazioni sui dischi, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc623-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="dc623-102">Collegare un disco vuoto</span><span class="sxs-lookup"><span data-stu-id="dc623-102">Attach an empty disk</span></span>
1. <span data-ttu-id="dc623-103">Aprire l'interfaccia CLI di Azure 1.0 e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dc623-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="dc623-104">Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="dc623-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="dc623-105">Immettere `azure vm disk attach-new` toocreate e collega un nuovo disco, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="dc623-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="dc623-106">Sostituire *myVM* con nome hello la macchina virtuale di Linux e specificare dimensioni di hello del disco hello in GB, ovvero *100GB* in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="dc623-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="dc623-107">Dopo il disco dati hello viene creato e collegato, è elencata nell'output di hello di `azure vm disk list <virtual-machine-name>` come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="dc623-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="dc623-108">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="dc623-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="dc623-109">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="dc623-109">Attach an existing disk</span></span>
<span data-ttu-id="dc623-110">Per collegare un disco esistente, è necessario che in un account di archiviazione sia disponibile un file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="dc623-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="dc623-111">Aprire l'interfaccia CLI di Azure 1.0 e [tooyour sottoscrizione di Azure connettersi](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dc623-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="dc623-112">Assicurarsi che sia attiva la modalità Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="dc623-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="dc623-113">Controllare se hello disco rigido virtuale che si desidera aggiungere tooattach già caricate tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="dc623-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="dc623-114">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="dc623-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="dc623-115">Se non si trova il disco hello che si desidera toouse, è possibile caricare una sottoscrizione di tooyour disco rigido virtuale locale tramite `azure vm disk create` o `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="dc623-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="dc623-116">Un esempio di `disk create` sarebbe come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dc623-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="dc623-117">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="dc623-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="dc623-118">È inoltre possibile utilizzare `azure vm disk upload` tooupload un account di archiviazione specifico tooa disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="dc623-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="dc623-119">Leggere ulteriori informazioni su hello comandi toomanage i dischi di dati della macchina virtuale di Azure [qui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="dc623-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="dc623-120">Ora si collega hello desiderato macchina virtuale tooyour di disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="dc623-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="dc623-121">Verificare che tooreplace *myVM* con nome hello della macchina virtuale e *myVHD* con il disco rigido virtuale desiderato.</span><span class="sxs-lookup"><span data-stu-id="dc623-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="dc623-122">È possibile verificare il disco di hello è collegato toohello la macchina virtuale con `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="dc623-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="dc623-123">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="dc623-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="dc623-124">Dopo aver aggiunto un disco dati, è necessario sarà necessario toolog nella macchina virtuale toohello e inizializzare disco hello macchina virtuale hello consentono di usare per l'archiviazione disco hello (vedere hello seguendo i passaggi per altre informazioni su come toodo inizializzare disco hello).</span><span class="sxs-lookup"><span data-stu-id="dc623-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

