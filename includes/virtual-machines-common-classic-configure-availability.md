


<span data-ttu-id="ddf20-101">Un set di disponibilità aiuta a mantenere disponibili le macchine virtuali durante il tempo di inattività, ad esempio durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="ddf20-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="ddf20-102">Inserimento di due o più macchine virtuali configurate in modo simile in un set di disponibilità crea hello ridondanza necessita toomaintain disponibilità di applicazioni di hello o servizi che esegue la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ddf20-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="ddf20-103">Per informazioni dettagliate sul funzionamento, vedere [gestione hello disponibilità delle macchine virtuali][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="ddf20-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="ddf20-104">È una migliore toouse pratica sia set di disponibilità e bilanciamento del carico endpoint toohelp assicurarsi che l'applicazione sia sempre disponibile e in esecuzione in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="ddf20-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="ddf20-105">Per informazioni dettagliate sugli endpoint con bilanciamento del carico, vedere [Bilanciamento del carico per i servizi di infrastruttura di Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="ddf20-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="ddf20-106">È possibile aggiungere le macchine virtuali in un set di disponibilità usando una di queste due opzioni:</span><span class="sxs-lookup"><span data-stu-id="ddf20-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="ddf20-107">[Opzione 1: Creare una macchina virtuale e un gruppo di disponibilità in hello stesso tempo][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="ddf20-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="ddf20-108">Quindi, aggiungere nuove macchine virtuali toohello, imposta quando si creano le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ddf20-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="ddf20-109">[Opzione 2: Aggiungere un set di disponibilità tooan macchina virtuale esistente][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="ddf20-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="ddf20-110">Nel modello classico hello, macchine virtuali che si desidera tooput nei hello stesso set di disponibilità deve appartenere toohello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ddf20-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="ddf20-111"><a id="createset"></a>Opzione 1: creare una macchina virtuale e un gruppo di disponibilità in hello stesso tempo</span><span class="sxs-lookup"><span data-stu-id="ddf20-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="ddf20-112">È possibile utilizzare entrambi hello portale di Azure o Azure PowerShell comandi toodo questo.</span><span class="sxs-lookup"><span data-stu-id="ddf20-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="ddf20-113">hello toouse portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="ddf20-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="ddf20-114">Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ddf20-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ddf20-115">Nel menu hub hello, fare clic su **+ nuovo**, quindi fare clic su **macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="ddf20-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="ddf20-117">Selezionare l'immagine di macchina virtuale Marketplace hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="ddf20-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="ddf20-118">È possibile scegliere toocreate una macchina virtuale Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="ddf20-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="ddf20-119">Per hello selezionato macchina virtuale, verificare che il modello di distribuzione hello sia impostato troppo**classico** e quindi fare clic su **crea**</span><span class="sxs-lookup"><span data-stu-id="ddf20-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="ddf20-121">Immettere il nome della macchina virtuale, il nome utente e la password (per computer Windows) o la chiave pubblica SSH (per i computer Linux).</span><span class="sxs-lookup"><span data-stu-id="ddf20-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="ddf20-122">Scegliere le dimensioni VM hello e quindi fare clic su **selezionare** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ddf20-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="ddf20-123">Scegliere **configurazione facoltativa > set di disponibilità**e selezionare il set di disponibilità hello desiderato tooadd hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ddf20-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="ddf20-125">Verificare le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ddf20-125">Review your configuration settings.</span></span> <span data-ttu-id="ddf20-126">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ddf20-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="ddf20-127">Mentre Azure crea la macchina virtuale, è possibile monitorare lo stato di avanzamento hello in **macchine virtuali** nel menu hub hello.</span><span class="sxs-lookup"><span data-stu-id="ddf20-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="ddf20-128">Azure PowerShell toouse comandi toocreate una macchina virtuale di Azure e aggiungerlo tooa set di disponibilità di nuovo o esistente, vedere [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ddf20-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="ddf20-129"><a id="addmachine"></a>Opzione 2: aggiungere un set di disponibilità tooan macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="ddf20-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="ddf20-130">Nel portale di Azure hello, è possibile aggiungere tooan di macchine virtuali classiche esistenti set di disponibilità esistente o crearne uno nuovo per loro.</span><span class="sxs-lookup"><span data-stu-id="ddf20-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="ddf20-131">(Tenere presente che le macchine virtuali hello in hello stesso set di disponibilità deve appartenere toohello stesso servizio cloud.) passaggi di Hello sono quasi hello stesso.</span><span class="sxs-lookup"><span data-stu-id="ddf20-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="ddf20-132">Con Azure PowerShell, è possibile aggiungere hello macchina virtuale tooan set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="ddf20-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="ddf20-133">Se non è già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ddf20-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ddf20-134">Nel menu Hub hello, fare clic su **macchine virtuali (classico)**.</span><span class="sxs-lookup"><span data-stu-id="ddf20-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="ddf20-136">Elenco di hello di macchine virtuali, selezionare il nome di hello della macchina virtuale hello che si desidera tooadd toohello set.</span><span class="sxs-lookup"><span data-stu-id="ddf20-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="ddf20-137">Scegliere **set di disponibilità** dalla macchina virtuale hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ddf20-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="ddf20-139">Selezionare il set di disponibilità hello desiderato tooadd hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ddf20-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="ddf20-140">macchina virtuale Hello devono appartenere toohello servizio stesso cloud come set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="ddf20-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="ddf20-142">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ddf20-142">Click **Save**.</span></span>

<span data-ttu-id="ddf20-143">comandi di Azure PowerShell toouse, aprire una sessione di PowerShell di Azure a livello di amministratore ed eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ddf20-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="ddf20-144">Per i segnaposto hello (ad esempio &lt;VmCloudServiceName&gt;), sostituire tutto il contenuto all'interno di virgolette hello, inclusi i caratteri di hello < e >, con hello correggere nomi.</span><span class="sxs-lookup"><span data-stu-id="ddf20-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="ddf20-145">macchina virtuale Hello potrebbe essere riavviato toobe toofinish aggiungerlo toohello set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ddf20-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

