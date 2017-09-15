


## <a name="attach-an-empty-disk"></a><span data-ttu-id="efd96-101">Collegare un disco vuoto</span><span class="sxs-lookup"><span data-stu-id="efd96-101">Attach an empty disk</span></span>
<span data-ttu-id="efd96-102">Il collegamento di un disco vuoto costituisce un modo semplice per aggiungere un disco dati perché Azure crea automaticamente il file con estensione vhd e lo archivia nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="efd96-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="efd96-103">Fare clic su **Macchine virtuali (versione classica)**, quindi selezionare la VM appropriata.</span><span class="sxs-lookup"><span data-stu-id="efd96-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="efd96-104">Nel menu Impostazioni fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="efd96-104">In the Settings menu, click **Disks**.</span></span>

   ![Collegare un nuovo disco vuoto](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="efd96-106">Sulla barra dei comandi fare clic su **Collega nuovo**.</span><span class="sxs-lookup"><span data-stu-id="efd96-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="efd96-107">Verrà visualizzata la finestra di dialogo **Collega un nuovo disco**.</span><span class="sxs-lookup"><span data-stu-id="efd96-107">The **Attach new disk** dialog box appears.</span></span>

    ![Collegare un nuovo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="efd96-109">Specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="efd96-109">Fill in the following information:</span></span>
    - <span data-ttu-id="efd96-110">In **Nome file**accettare il nome predefinito o digitarne un altro per il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="efd96-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="efd96-111">Il disco dati usa un nome generato automaticamente, anche se si digita un altro nome per il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="efd96-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="efd96-112">Selezionare il **tipo** di disco dati.</span><span class="sxs-lookup"><span data-stu-id="efd96-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="efd96-113">Tutte le macchine virtuali supportano dischi Standard.</span><span class="sxs-lookup"><span data-stu-id="efd96-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="efd96-114">Molte macchine virtuali supportano anche dischi Premium.</span><span class="sxs-lookup"><span data-stu-id="efd96-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="efd96-115">Selezionare le **dimensioni (GB)** del disco dati.</span><span class="sxs-lookup"><span data-stu-id="efd96-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="efd96-116">Per **Memorizzazione nella cache dell'host** scegliere Nessuna o Sola lettura.</span><span class="sxs-lookup"><span data-stu-id="efd96-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="efd96-117">Fare clic su OK per terminare.</span><span class="sxs-lookup"><span data-stu-id="efd96-117">Click OK to finish.</span></span>

4. <span data-ttu-id="efd96-118">Dopo che è stato creato e collegato, il disco dati verrà elencato nella sezione dei dischi della VM.</span><span class="sxs-lookup"><span data-stu-id="efd96-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![Disco dati nuovo e vuoto collegato correttamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="efd96-120">Dopo aver aggiunto un disco dati, è necessario accedere alla VM e inizializzare il disco in modo che possa essere usato.</span><span class="sxs-lookup"><span data-stu-id="efd96-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="efd96-121">Procedura: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="efd96-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="efd96-122">Per collegare un disco esistente, è necessario che in un account di archiviazione sia disponibile un file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="efd96-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="efd96-123">Usare il cmdlet [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) per caricare il file con estensione vhd nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="efd96-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="efd96-124">Dopo aver creato e caricato il file con estensione vhd, è possibile collegarlo a una VM.</span><span class="sxs-lookup"><span data-stu-id="efd96-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="efd96-125">Fare clic su **Macchine virtuali (versione classica)** e quindi selezionare la macchina virtuale appropriata.</span><span class="sxs-lookup"><span data-stu-id="efd96-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="efd96-126">Nel menu Impostazioni fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="efd96-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="efd96-127">Sulla barra dei comandi fare clic su **Collega esistente**.</span><span class="sxs-lookup"><span data-stu-id="efd96-127">On the command bar, click **Attach existing**.</span></span>

    ![Collegare il disco dati](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="efd96-129">Fare clic su **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="efd96-129">Click **Location**.</span></span> <span data-ttu-id="efd96-130">Verranno visualizzati gli account di archiviazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="efd96-130">The available storage accounts display.</span></span> <span data-ttu-id="efd96-131">Selezionare quindi un account di archiviazione appropriato tra quelli elencati.</span><span class="sxs-lookup"><span data-stu-id="efd96-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Selezionare un account di archiviazione per il disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="efd96-133">Un **account di archiviazione** ha uno o più contenitori con unità disco (dischi rigidi virtuali).</span><span class="sxs-lookup"><span data-stu-id="efd96-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="efd96-134">Selezionare il contenitore appropriato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="efd96-134">Select the appropriate container from those listed.</span></span>

    ![Finestra di selezione del contenitore delle macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="efd96-136">Il pannello **VHD** elenca le unità disco presenti nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="efd96-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="efd96-137">Fare clic su uno dei dischi, quindi su Seleziona.</span><span class="sxs-lookup"><span data-stu-id="efd96-137">Click one of the disks, and then click Select.</span></span>

    ![Finestra di selezione dell'immagine del disco per le macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="efd96-139">Verrà di nuovo visualizzato il pannello **Collega un disco esistente** con il percorso dell'account di archiviazione, il contenitore e il disco rigido virtuale selezionato (vhd) da aggiungere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="efd96-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="efd96-140">Impostare **Memorizzazione nella cache dell'host** su Nessuno o Sola lettura, quindi fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="efd96-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Disco dati correttamente collegato](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
