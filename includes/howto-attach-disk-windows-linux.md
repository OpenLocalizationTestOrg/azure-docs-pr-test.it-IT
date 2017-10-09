


## <a name="attach-an-empty-disk"></a><span data-ttu-id="f2a67-101">Collegare un disco vuoto</span><span class="sxs-lookup"><span data-stu-id="f2a67-101">Attach an empty disk</span></span>
<span data-ttu-id="f2a67-102">Collegare un disco vuoto è tooadd un modo semplice un tipo di dati su disco, poiché Azure crea file con estensione vhd hello automaticamente e lo archivia nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="f2a67-103">Fare clic su **macchine virtuali (classico)**, e quindi selezionare hello VM appropriato.</span><span class="sxs-lookup"><span data-stu-id="f2a67-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="f2a67-104">Nel menu Impostazioni hello, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="f2a67-104">In hello Settings menu, click **Disks**.</span></span>

   ![Collegare un nuovo disco vuoto](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="f2a67-106">Nella barra dei comandi di hello, fare clic su **nuovo collegamento**.</span><span class="sxs-lookup"><span data-stu-id="f2a67-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="f2a67-107">Hello **Collega nuovo disco** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f2a67-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Collegare un nuovo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="f2a67-109">Compilare hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="f2a67-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="f2a67-110">In **nome File**, accettare il nome di predefinito hello o digitare un altro per i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="f2a67-111">disco dati Hello utilizza un nome generato automaticamente, anche se si digita un nome diverso per i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="f2a67-112">Seleziona hello **tipo** del disco dati hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="f2a67-113">Tutte le macchine virtuali supportano dischi Standard.</span><span class="sxs-lookup"><span data-stu-id="f2a67-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="f2a67-114">Molte macchine virtuali supportano anche dischi Premium.</span><span class="sxs-lookup"><span data-stu-id="f2a67-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="f2a67-115">Seleziona hello **dimensioni (GB)** del disco dati hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="f2a67-116">Per **Memorizzazione nella cache dell'host** scegliere Nessuna o Sola lettura.</span><span class="sxs-lookup"><span data-stu-id="f2a67-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="f2a67-117">Fare clic su OK toofinish.</span><span class="sxs-lookup"><span data-stu-id="f2a67-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="f2a67-118">Dopo il disco dati hello viene creato e collegato, è elencata nella sezione di dischi hello di hello VM.</span><span class="sxs-lookup"><span data-stu-id="f2a67-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Disco dati nuovo e vuoto collegato correttamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="f2a67-120">Dopo aver aggiunto un disco dati, è necessario toolog in toohello VM e inizializzare il disco hello in modo che può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="f2a67-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="f2a67-121">Procedura: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="f2a67-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="f2a67-122">Per collegare un disco esistente, è necessario che in un account di archiviazione sia disponibile un file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="f2a67-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="f2a67-123">Hello utilizzare [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) account di archiviazione di cmdlet tooupload hello VHD file toohello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="f2a67-124">Dopo aver creato e caricato i file con estensione vhd hello, è possibile collegare tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f2a67-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="f2a67-125">Fare clic su **macchine virtuali (classico)**, e quindi selezionare hello macchina virtuale appropriata.</span><span class="sxs-lookup"><span data-stu-id="f2a67-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="f2a67-126">Nel menu Impostazioni hello, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="f2a67-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="f2a67-127">Nella barra dei comandi di hello, fare clic su **collegamento esistente**.</span><span class="sxs-lookup"><span data-stu-id="f2a67-127">On hello command bar, click **Attach existing**.</span></span>

    ![Collegare il disco dati](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="f2a67-129">Fare clic su **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="f2a67-129">Click **Location**.</span></span> <span data-ttu-id="f2a67-130">visualizzare gli account di archiviazione disponibile Hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-130">hello available storage accounts display.</span></span> <span data-ttu-id="f2a67-131">Selezionare quindi un account di archiviazione appropriato tra quelli elencati.</span><span class="sxs-lookup"><span data-stu-id="f2a67-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Selezionare un account di archiviazione per il disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="f2a67-133">Un **account di archiviazione** ha uno o più contenitori con unità disco (dischi rigidi virtuali).</span><span class="sxs-lookup"><span data-stu-id="f2a67-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="f2a67-134">Selezionare il contenitore appropriato di hello da quelli elencati.</span><span class="sxs-lookup"><span data-stu-id="f2a67-134">Select hello appropriate container from those listed.</span></span>

    ![Finestra di selezione del contenitore delle macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="f2a67-136">Hello **dischi rigidi virtuali** pannello elenca le unità disco hello contenute nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="f2a67-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="f2a67-137">Fare clic su uno dei dischi hello e quindi fare clic su Seleziona.</span><span class="sxs-lookup"><span data-stu-id="f2a67-137">Click one of hello disks, and then click Select.</span></span>

    ![Finestra di selezione dell'immagine del disco per le macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="f2a67-139">Hello **collegare un disco esistente** pannello visualizzato nuovamente, con percorso hello contenente l'account di archiviazione hello, contenitore e macchina virtuale toohello tooadd di disco rigido selezionato (vhd).</span><span class="sxs-lookup"><span data-stu-id="f2a67-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="f2a67-140">Impostare **ospitare la memorizzazione nella cache** toonone o lettura, quindi fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="f2a67-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Disco dati correttamente collegato](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
