1. <span data-ttu-id="e61db-101">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e61db-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e61db-102">A partire da in alto a sinistra di hello, fare clic su **nuovo > calcolo > Data Center di Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="e61db-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Passare toohello immagini di macchina virtuale di Azure nel portale di hello](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="e61db-104">Scegliere modello di distribuzione classica hello hello Datacenter di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e61db-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="e61db-105">Fare clic su Crea.</span><span class="sxs-lookup"><span data-stu-id="e61db-105">Click Create.</span></span>

    ![Schermata che mostra le immagini di macchina virtuale di Azure hello disponibile nel portale di hello](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="e61db-107">1. Pannello Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="e61db-107">1. Basics blade</span></span>

<span data-ttu-id="e61db-108">Pannello nozioni di base Hello richiede informazioni amministrative per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="e61db-109">Immettere un **nome** per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="e61db-110">Nell'esempio hello _HeroVM_ hello nome della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="e61db-111">nome Hello deve essere 1-15 caratteri e non può contenere caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="e61db-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="e61db-112">Immettere un **nome utente** e un nome sicuro **Password** che vengono utilizzati toocreate un account locale nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="e61db-113">Hello account locale viene utilizzato in tooand toosign gestire hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e61db-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="e61db-114">Nell'esempio hello _azureuser_ è il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="e61db-115">Hello password deve essere 8-123 caratteri e soddisfare tre hello quattro seguenti i requisiti di complessità: una lettera minuscola, una lettera maiuscola, un numero e un carattere speciale.</span><span class="sxs-lookup"><span data-stu-id="e61db-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="e61db-116">Sono disponibili altre informazioni sui [requisiti relativi a nome utente e password](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="e61db-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="e61db-117">Hello **sottoscrizione** è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e61db-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="e61db-118">Un'impostazione comune è "Uso prepagato".</span><span class="sxs-lookup"><span data-stu-id="e61db-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="e61db-119">Selezionare un oggetto esistente **gruppo di risorse** o nome di tipo hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="e61db-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="e61db-120">Nell'esempio hello _HeroVMRG_ nome hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e61db-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="e61db-121">Selezionare un Data Center Azure **percorso** in cui si desidera toorun VM hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="e61db-122">Nell'esempio hello **Stati Uniti orientali** hello posizione.</span><span class="sxs-lookup"><span data-stu-id="e61db-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="e61db-123">Al termine, fare clic su **Avanti** toocontinue toohello Avanti blade.</span><span class="sxs-lookup"><span data-stu-id="e61db-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Schermata che mostra le impostazioni di hello in Pannello di hello nozioni di base per la configurazione di una macchina virtuale di Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="e61db-125">2. Pannello Dimensioni</span><span class="sxs-lookup"><span data-stu-id="e61db-125">2. Size blade</span></span>

<span data-ttu-id="e61db-126">Pannello dimensioni Hello identifica i dettagli di configurazione hello di hello VM ed elenca varie opzioni che includono del sistema operativo, numero di processori, tipo di archiviazione su disco e costi di utilizzo mensile stimato.</span><span class="sxs-lookup"><span data-stu-id="e61db-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="e61db-127">Scegliere una dimensione di macchina virtuale e quindi fare clic su **selezionare** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e61db-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="e61db-128">In questo esempio, _DS1_\__V2 Standard_ è hello dimensione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e61db-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Schermata del Pannello di dimensioni hello che mostra hello dimensioni delle macchine Virtuali di Azure che è possibile selezionare](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="e61db-130">3. Pannello Impostazioni</span><span class="sxs-lookup"><span data-stu-id="e61db-130">3. Settings blade</span></span>

<span data-ttu-id="e61db-131">pannello impostazioni Hello richiede le opzioni di archiviazione e rete.</span><span class="sxs-lookup"><span data-stu-id="e61db-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="e61db-132">È possibile accettare le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-132">You can accept hello default settings.</span></span> <span data-ttu-id="e61db-133">Se necessario, Azure crea le voci appropriate.</span><span class="sxs-lookup"><span data-stu-id="e61db-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="e61db-134">Se sono state selezionate dimensioni di macchina virtuale che lo supportano, è possibile provare il servizio Archiviazione Premium di Azure selezionando Premium (SSD) nel Tipo di disco.</span><span class="sxs-lookup"><span data-stu-id="e61db-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="e61db-135">Al termine delle modifiche, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e61db-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="e61db-136">4. Pannello Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e61db-136">4. Summary blade</span></span>

<span data-ttu-id="e61db-137">Pannello riepilogo Hello Elenca le impostazioni di hello specificate in pannelli precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="e61db-138">Fare clic su **OK** quando si è pronti toomake immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Pannello riepilogo report fornendo specificate le impostazioni della macchina virtuale hello](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="e61db-140">Dopo la creazione di macchine virtuali hello, vengono visualizzati hello nuova macchina virtuale nel portale di hello **tutte le risorse**e viene visualizzato un riquadro della macchina virtuale hello nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="e61db-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="e61db-141">Hello corrispondente cloud storage account e inoltre vengono creati ed elencati.</span><span class="sxs-lookup"><span data-stu-id="e61db-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="e61db-142">Macchina virtuale hello sia il servizio cloud vengono avviate automaticamente e il relativo stato viene elencato come **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e61db-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurare gli endpoint di agente di macchine Virtuali e hello della macchina virtuale hello](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
