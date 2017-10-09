# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="aa5e5-101">Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)</span><span class="sxs-lookup"><span data-stu-id="aa5e5-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="aa5e5-102">Questo articolo risponde alle domande frequenti su Managed Disks e Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="aa5e5-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="aa5e5-103">Managed Disks</span></span>

<span data-ttu-id="aa5e5-104">**Che cos'è Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="aa5e5-105">Managed Disks è una funzionalità che semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure, gestendo l'account di archiviazione per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="aa5e5-106">Per ulteriori informazioni, vedere hello [Panoramica di dischi gestiti](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="aa5e5-107">**Se si crea un disco gestito Standard da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="aa5e5-108">Un disco gestito standard creato da un disco rigido virtuale di 80 GB viene considerato come dimensione disponibile su disco standard successiva hello, che è un disco S10.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="aa5e5-109">Vengono addebitati in base toohello S10 disco sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="aa5e5-110">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="aa5e5-111">**Sono previsti costi di transazione per i dischi gestiti Standard?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="aa5e5-112">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-112">Yes.</span></span> <span data-ttu-id="aa5e5-113">Sì, ogni transazione prevede un addebito.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-113">You're charged for each transaction.</span></span> <span data-ttu-id="aa5e5-114">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="aa5e5-115">**Per un disco gestito standard, addebitata per dimensioni effettive di hello dei dati di hello su disco hello o per la capacità di hello il provisioning del disco hello?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="aa5e5-116">Vengono addebitati in base alle capacità di hello il provisioning del disco hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="aa5e5-117">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="aa5e5-118">**In che modo il prezzo della versione Premium dei dischi gestiti è diverso da quello dei dischi non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="aa5e5-119">Hello sui prezzi dei dischi premium gestiti hello come i dischi premium non gestito.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="aa5e5-120">**È possibile modificare hello archiviazione tipo di account (Standard o Premium) di dischi personali gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="aa5e5-121">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-121">Yes.</span></span> <span data-ttu-id="aa5e5-122">Per cambiare tipo di account di archiviazione hello i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="aa5e5-123">**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="aa5e5-124">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-124">Yes.</span></span> <span data-ttu-id="aa5e5-125">È possibile esportare i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="aa5e5-126">**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito con una sottoscrizione diversa?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="aa5e5-127">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-127">No.</span></span>

<span data-ttu-id="aa5e5-128">**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito in un'area diversa?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="aa5e5-129">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-129">No.</span></span>

<span data-ttu-id="aa5e5-130">**Ci sono limitazioni di scalabilità per i clienti che usano dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="aa5e5-131">Dischi gestiti Elimina i limiti di hello associati agli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="aa5e5-132">Tuttavia, il numero di hello di dischi gestiti per ogni sottoscrizione è limitata too2, 000 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="aa5e5-133">È possibile chiamare il supporto tooincrease questo numero.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="aa5e5-134">**È possibile fare uno snapshot incrementale di un disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="aa5e5-135">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-135">No.</span></span> <span data-ttu-id="aa5e5-136">funzionalità di snapshot corrente Hello crea una copia completa di un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="aa5e5-137">Tuttavia, si pianificare toosupport snapshot incrementali in hello future.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="aa5e5-138">**Le macchine virtuali in un set di disponibilità possono essere composte da una combinazione di dischi gestiti e non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="aa5e5-139">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-139">No.</span></span> <span data-ttu-id="aa5e5-140">Hello macchine virtuali in un set di disponibilità deve utilizzare dischi gestiti o tutti i dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="aa5e5-141">Quando si crea un set di disponibilità, è possibile scegliere quale tipo di disco desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="aa5e5-142">**È l'opzione predefinita di dischi gestiti hello in hello portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="aa5e5-143">Non attualmente, ma sarà utilizzata l'impostazione predefinita, hello in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="aa5e5-144">**È possibile creare un disco vuoto gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="aa5e5-145">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-145">Yes.</span></span> <span data-ttu-id="aa5e5-146">È possibile creare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-146">You can create an empty disk.</span></span> <span data-ttu-id="aa5e5-147">Un disco gestito può essere creato in modo indipendente da una macchina virtuale, ad esempio, senza collegarlo tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="aa5e5-148">**Numero di domini di errore hello è supportato per un set di disponibilità che usa dischi gestiti novità**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="aa5e5-149">A seconda area hello set di disponibilità hello che utilizza dischi gestiti in cui si trova, numero di domini di errore hello supportato è 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="aa5e5-150">**È come account di archiviazione standard hello per configurare diagnostica?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="aa5e5-151">Si imposta un account di archiviazione privato per la diagnostica della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="aa5e5-152">In futuro hello, contiamo tooswitch Diagnostica dischi tooManaged anche.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="aa5e5-153">**Che tipo di supporto per il controllo degli accessi in base al ruolo è disponibile per Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="aa5e5-154">Managed Disks supporta tre ruoli predefiniti principali:</span><span class="sxs-lookup"><span data-stu-id="aa5e5-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="aa5e5-155">Proprietario: può gestire tutto, compresi gli accessi</span><span class="sxs-lookup"><span data-stu-id="aa5e5-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="aa5e5-156">Collaboratore: può gestire tutto ad eccezione degli accessi</span><span class="sxs-lookup"><span data-stu-id="aa5e5-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="aa5e5-157">Lettore: può visualizzare tutto, ma non apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="aa5e5-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="aa5e5-158">**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="aa5e5-159">È possibile ottenere una firma di accesso condiviso di sola lettura URI per hello gestito su disco e usarlo toocopy hello contenuto tooa archiviazione privato locale o account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="aa5e5-160">**È possibile creare una copia del proprio disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="aa5e5-161">Clienti di uno snapshot di propri dischi gestiti e quindi utilizzare un altro disco gestito toocreate snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="aa5e5-162">**I dischi non gestiti sono ancora supportati?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="aa5e5-163">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-163">Yes.</span></span> <span data-ttu-id="aa5e5-164">Sì, sono supportati sia i dischi gestiti che quelli non gestiti.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="aa5e5-165">È consigliabile usare dischi gestiti per i nuovi carichi di lavoro e la migrazione dei dischi di toomanaged i carichi di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="aa5e5-166">**Se si crea un disco da 128 GB e quindi aumentare hello dimensioni too130 GB, verrà addebitato dimensioni del disco successiva hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="aa5e5-167">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-167">Yes.</span></span>

<span data-ttu-id="aa5e5-168">**È possibile creare dischi gestiti per l'archiviazione con ridondanza locale, l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza della zona?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="aa5e5-169">Attualmente Azure Managed Disks supporta solo dischi gestiti per l'archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="aa5e5-170">**È possibile ridurre/ridimensionare i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="aa5e5-171">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-171">No.</span></span> <span data-ttu-id="aa5e5-172">Questa funzionalità non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="aa5e5-173">**È possibile modificare proprietà del nome computer hello quando specializzata (non creati tramite l'utilità preparazione sistema hello o generalizzata) disco del sistema operativo è tooprovision usato una macchina virtuale?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="aa5e5-174">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-174">No.</span></span> <span data-ttu-id="aa5e5-175">È possibile aggiornare una proprietà del nome computer hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-175">You can't update hello computer name property.</span></span> <span data-ttu-id="aa5e5-176">Hello nuova macchina virtuale eredita da padre hello VM, che è stato disco del sistema operativo utilizzato toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="aa5e5-177">**Dove trovare i modelli per Gestione risorse di Azure esempio toocreate macchine virtuali con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="aa5e5-178">Elenco di modelli che usano Managed Disks</span><span class="sxs-lookup"><span data-stu-id="aa5e5-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="aa5e5-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="aa5e5-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="aa5e5-180">Managed Disks e crittografia del servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="aa5e5-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="aa5e5-181">**La crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="aa5e5-182">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-182">Yes.</span></span>

<span data-ttu-id="aa5e5-183">**Che gestisce le chiavi di crittografia hello?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="aa5e5-184">Microsoft gestisce le chiavi di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="aa5e5-185">**È possibile disabilitare la crittografia del servizio di archiviazione per i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="aa5e5-186">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-186">No.</span></span>

<span data-ttu-id="aa5e5-187">**La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="aa5e5-188">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-188">No.</span></span> <span data-ttu-id="aa5e5-189">È disponibile in tutte le aree di hello in cui i dischi gestiti è disponibili.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="aa5e5-190">Managed Disks è disponibile in tutte le aree pubbliche e in Germania.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="aa5e5-191">**Come si può determinare se un disco gestito è crittografato?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="aa5e5-192">È possibile scoprire hello ora di creazione un disco gestito dal portale di Azure hello, hello CLI di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="aa5e5-193">Se hello viene eseguita dopo il 9 giugno 2017, il disco è crittografato.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="aa5e5-194">**Come è possibile crittografare i dischi esistenti creati prima del 10 giugno 2017?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="aa5e5-195">A partire da 10 giugno 2017, dischi gestiti tooexisting nuovi dati vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="aa5e5-196">È inoltre pianificare i dati esistenti tooencrypt e crittografia hello avverrà in modo asincrono in background hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="aa5e5-197">Se è necessario crittografare i dati esistenti adesso, creare una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="aa5e5-198">I nuovi dischi verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="aa5e5-199">Copiare i dischi gestiti tramite hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="aa5e5-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="aa5e5-200">Copiare i dischi gestiti tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa5e5-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="aa5e5-201">**Le immagini e gli snapshot gestiti vengono crittografati?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="aa5e5-202">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-202">Yes.</span></span> <span data-ttu-id="aa5e5-203">Tutte le immagini e gli snapshot gestiti creati dopo il 9 giugno 2017 vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="aa5e5-204">**È possibile convertire le macchine virtuali con dischi non gestiti che si trovano sugli account di archiviazione o sono stati crittografati in precedenza toomanaged dischi?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="aa5e5-205">Sì</span><span class="sxs-lookup"><span data-stu-id="aa5e5-205">Yes</span></span>

<span data-ttu-id="aa5e5-206">**Un disco rigido virtuale esportato da un disco gestito o uno snapshot verrà crittografato?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="aa5e5-207">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-207">No.</span></span> <span data-ttu-id="aa5e5-208">Ma se si esporta un disco rigido virtuale tooan crittografate account di archiviazione da un disco gestito crittografato o di uno snapshot, quindi viene crittografato.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="aa5e5-209">Dischi Premium, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="aa5e5-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="aa5e5-210">**Se una macchina virtuale usa una serie di dimensioni che supporta Archiviazione Premium, ad esempio DSv2, è possibile collegare dischi dati sia Premium che Standard?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="aa5e5-211">Sì.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-211">Yes.</span></span>

<span data-ttu-id="aa5e5-212">**È possibile collegare sia premium e standard dischi tooa dimensioni serie di dati non supporta l'archiviazione Premium, ad esempio la serie D, Dv2, G o F**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="aa5e5-213">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-213">No.</span></span> <span data-ttu-id="aa5e5-214">È possibile collegare solo i tooVMs dischi dati standard che non usano una serie di dimensioni che supporta l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="aa5e5-215">**Se si crea un disco dati Premium da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="aa5e5-216">Un disco dati premium creato da un disco rigido virtuale di 80 GB viene considerato come dimensioni del disco premium disponibile con Avanti hello, che è un disco P10.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="aa5e5-217">Vengono addebitati in base toohello P10 disco sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="aa5e5-218">**Sono presenti i costi di transazione toouse archiviazione Premium?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="aa5e5-219">È previsto un costo fisso per ogni dimensione di disco con provisioning di un certo numero di IOPS e di una certa velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="aa5e5-220">Hello altri costi sono la larghezza di banda in uscita e la capacità di snapshot, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="aa5e5-221">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="aa5e5-222">**Quali sono i limiti di hello per IOPS e la velocità effettiva che è possibile ottenere dalla cache di hello disco?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="aa5e5-223">limiti combinati per cache di Hello e unità SSD locale per una serie di dominio Active Directory sono 4.000 IOPS per ogni core e 33 MB al secondo per ogni core.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="aa5e5-224">Hello serie GS offre 5.000 IOPS per ogni core e 50 MB al secondo per i componenti di base.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="aa5e5-225">**È supportata da unità SSD locale per una macchina virtuale i dischi gestiti hello?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="aa5e5-226">Hello SSD locale temporanea di archiviazione è incluso in una macchina virtuale i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="aa5e5-227">Questa archiviazione temporanea non comporta costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="aa5e5-228">È consigliabile non utilizzare questo toostore SSD locale i dati delle applicazioni perché non è persistente nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="aa5e5-229">**Sono presenti eventuali ripercussioni per hello, utilizzare di TRIM su dischi premium?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="aa5e5-230">Non viene utilizzato toohello svantaggio di TRIM su dischi premium di Azure o i dischi standard.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="aa5e5-231">Dimensioni dei nuovi dischi, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="aa5e5-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="aa5e5-232">**Che cos'è hello disco massime supportate per il sistema operativo e i dischi dati?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="aa5e5-233">tipo di partizione Hello che supporta Azure per un disco del sistema operativo è il record di avvio principale hello (MBR).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="aa5e5-234">formato MBR Hello supporta dimensioni di un disco di too2 TB.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="aa5e5-235">dimensione massima di Hello che supporta Azure per un disco del sistema operativo è di 2 TB.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="aa5e5-236">Azure supporta backup too4 TB per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="aa5e5-237">**Che cos'è hello pagina blob massime supportate?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="aa5e5-238">Hello pagina blob massime che supporta Azure è 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="aa5e5-239">Maggiore di 4 TB (4.095 GB) collegati tooa macchina virtuale come dischi del sistema operativo o di dati BLOB di pagine non è supportato.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="aa5e5-240">**Necessario toouse una nuova versione di strumenti di Azure toocreate, allegare, ridimensionare e caricare dischi superiori a 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="aa5e5-241">È necessario tooupgrade il toocreate gli strumenti di Azure esistente, collegare o ridimensionare i dischi di dimensioni superiori a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="aa5e5-242">tooupload file disco rigido virtuale locale direttamente tooAzure come un blob di pagine o un disco non gestito, è necessario set di strumenti più recenti toouse hello:</span><span class="sxs-lookup"><span data-stu-id="aa5e5-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="aa5e5-243">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="aa5e5-243">Azure tools</span></span>      | <span data-ttu-id="aa5e5-244">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="aa5e5-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="aa5e5-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa5e5-245">Azure PowerShell</span></span> | <span data-ttu-id="aa5e5-246">Numero di versione 4.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="aa5e5-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="aa5e5-247">Interfaccia della riga di comando di Azure v1</span><span class="sxs-lookup"><span data-stu-id="aa5e5-247">Azure CLI v1</span></span>     | <span data-ttu-id="aa5e5-248">Numero di versione 0.10.13: versione di maggio 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="aa5e5-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="aa5e5-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="aa5e5-249">AzCopy</span></span>           | <span data-ttu-id="aa5e5-250">Numero di versione 6.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="aa5e5-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="aa5e5-251">supporto di Hello per v2 CLI di Azure e Azure Storage Explorer sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="aa5e5-252">**Le dimensioni del disco P4 e P6 sono supportate per i dischi gestiti o i BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="aa5e5-253">No.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-253">No.</span></span> <span data-ttu-id="aa5e5-254">Le dimensioni del disco P4 (32 GB) e P6 (64 GB) sono supportate solo per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="aa5e5-255">Il supporto per dischi non gestiti e BLOB di pagine sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="aa5e5-256">**Se il premio esistente gestiti disco minore di 64 GB è stato creato prima il disco di piccole dimensioni hello è stato abilitato (circa 15 giugno 2017), come la fatturazione?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="aa5e5-257">Dischi di piccole dimensioni premium esistenti minore di 64 GB continuare toobe fatturato secondo toohello P10 piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="aa5e5-258">**Come è possibile passare a livelli disco hello di dischi di piccole dimensioni premium minore di 64 GB da P10 tooP4 o P6?**</span><span class="sxs-lookup"><span data-stu-id="aa5e5-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="aa5e5-259">È possibile creare uno snapshot di dischi di piccole dimensioni e quindi creare un hello di commutatore tooautomatically disco prezzi tooP4 livello o P6 in base alle dimensioni di hello il provisioning.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="aa5e5-260">Cosa fare se non è disponibile una risposta alla domanda?</span><span class="sxs-lookup"><span data-stu-id="aa5e5-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="aa5e5-261">Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="aa5e5-262">È possibile pubblicare una domanda alla fine di hello di questo articolo in commenti hello.</span><span class="sxs-lookup"><span data-stu-id="aa5e5-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="aa5e5-263">tooengage con il team di archiviazione di Azure hello e altri membri della community su questo articolo, utilizzare hello MSDN [forum di Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="aa5e5-264">funzionalità toorequest, inviare toohello le richieste e idee [forum sul feedback su archiviazione di Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="aa5e5-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
