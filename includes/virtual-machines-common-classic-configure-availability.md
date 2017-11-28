


<span data-ttu-id="15532-101">Un set di disponibilità aiuta a mantenere disponibili le macchine virtuali durante il tempo di inattività, ad esempio durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="15532-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="15532-102">L'inserimento di due o più macchine virtuali con configurazione simile in un set di disponibilità crea la ridondanza necessaria a mantenere la disponibilità delle applicazioni o dei servizi eseguiti sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15532-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="15532-103">Per informazioni dettagliate sul funzionamento, vedere [Gestire la disponibilità delle macchine virtuali][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="15532-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="15532-104">Per assicurare la continua disponibilità e l'esecuzione efficiente dell'applicazione, è buona norma usare sia set di disponibilità sia endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="15532-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="15532-105">Per informazioni dettagliate sugli endpoint con bilanciamento del carico, vedere [Bilanciamento del carico per i servizi di infrastruttura di Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="15532-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="15532-106">È possibile aggiungere le macchine virtuali in un set di disponibilità usando una di queste due opzioni:</span><span class="sxs-lookup"><span data-stu-id="15532-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="15532-107">[Opzione 1: Creare una macchina virtuale e un set di disponibilità contemporaneamente][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="15532-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="15532-108">Quindi, aggiungere le nuove macchine virtuali al set.</span><span class="sxs-lookup"><span data-stu-id="15532-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="15532-109">[Opzione 2: Aggiungere una macchina virtuale esistente a un set di disponibilità][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="15532-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="15532-110">Nel modello classico, le macchine virtuali che si desidera inserire nello stesso set di disponibilità devono appartenere allo stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="15532-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="15532-111"><a id="createset"> </a>Opzione 1: Creare una macchina virtuale e un set di disponibilità contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="15532-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="15532-112">A tale scopo, è possibile usare il portale di Azure o i comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15532-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="15532-113">Per usare il Portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="15532-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="15532-114">Accedere al [portale di Azure](https://portal.azure.com), se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="15532-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15532-115">Nel menu Hub fare clic su **+ Nuovo**, quindi su **Macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="15532-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="15532-117">Selezionare l'immagine della macchina virtuale del Marketplace che si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="15532-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="15532-118">È possibile scegliere di creare una macchina virtuale Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="15532-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="15532-119">Per la macchina virtuale selezionata verificare che il modello di distribuzione sia impostato su **Classico**, quindi fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="15532-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="15532-121">Immettere il nome della macchina virtuale, il nome utente e la password (per computer Windows) o la chiave pubblica SSH (per i computer Linux).</span><span class="sxs-lookup"><span data-stu-id="15532-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="15532-122">Scegliere le dimensioni della VM, quindi fare clic su **Seleziona** per continuare.</span><span class="sxs-lookup"><span data-stu-id="15532-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="15532-123">Scegliere **Configurazione facoltativa > Set di disponibilità**, quindi selezionare il set di disponibilità che si vuole aggiungere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15532-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="15532-125">Verificare le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="15532-125">Review your configuration settings.</span></span> <span data-ttu-id="15532-126">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="15532-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="15532-127">Mentre Azure crea la macchina virtuale, è possibile tenere traccia dello stato di avanzamento nel menu Hub in **Macchine virtuali** .</span><span class="sxs-lookup"><span data-stu-id="15532-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="15532-128">Per usare i comandi di Azure PowerShell per creare una macchina virtuale di Azure e aggiungerla a un set di disponibilità nuovo o esistente, vedere [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Usare Azure PowerShell per creare e preconfigurare macchine virtuali Windows)</span><span class="sxs-lookup"><span data-stu-id="15532-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="15532-129"><a id="addmachine"> </a>Opzione 2: Aggiungere una macchina virtuale esistente a un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="15532-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="15532-130">Nel Portale di Azure è possibile aggiungere le macchine virtuali classiche a un set di disponibilità esistente oppure creare un set nuovo per le macchine.</span><span class="sxs-lookup"><span data-stu-id="15532-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="15532-131">(si noti che le macchine virtuali presenti nello stesso set di disponibilità devono appartenere allo stesso servizio cloud). La procedura è quasi la stessa:</span><span class="sxs-lookup"><span data-stu-id="15532-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="15532-132">con Azure PowerShell è possibile aggiungere la macchina virtuale a un set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="15532-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="15532-133">Accedere al [portale di Azure](https://portal.azure.com), se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="15532-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15532-134">Fare clic su **Macchine virtuali (classico)**nel menu Hub.</span><span class="sxs-lookup"><span data-stu-id="15532-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="15532-136">Nell'elenco delle macchine virtuali selezionare il nome della macchina virtuale che si desidera aggiungere al set.</span><span class="sxs-lookup"><span data-stu-id="15532-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="15532-137">Scegliere **Set di disponibilità** in **Impostazioni** della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15532-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="15532-139">Selezionare il set di disponibilità che si desidera aggiungere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15532-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="15532-140">La macchina virtuale deve appartenere allo stesso servizio cloud del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="15532-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="15532-142">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="15532-142">Click **Save**.</span></span>

<span data-ttu-id="15532-143">Per usare i comandi di Azure PowerShell, aprire una sessione di Azure PowerShell con privilegi di amministratore ed attivare il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="15532-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="15532-144">Per i segnaposto, ad esempio &lt;VmCloudServiceName&gt;, sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >, con i nomi corretti.</span><span class="sxs-lookup"><span data-stu-id="15532-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="15532-145">Potrebbe essere necessario riavviare la macchina virtuale per completarne l'aggiunta al set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="15532-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

