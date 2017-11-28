# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="e149b-101">Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)</span><span class="sxs-lookup"><span data-stu-id="e149b-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="e149b-102">Questo articolo risponde alle domande frequenti su Managed Disks e Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="e149b-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="e149b-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e149b-103">Managed Disks</span></span>

<span data-ttu-id="e149b-104">**Che cos'è Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e149b-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="e149b-105">Managed Disks è una funzionalità che semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure, gestendo l'account di archiviazione per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e149b-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="e149b-106">Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e149b-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="e149b-107">**Se si crea un disco gestito Standard da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="e149b-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="e149b-108">Un disco gestito Standard creato da un disco rigido virtuale da 80 GB viene considerato come il disco Standard immediatamente successivo in termini di dimensioni, ovvero un disco S10.</span><span class="sxs-lookup"><span data-stu-id="e149b-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="e149b-109">Il costo addebitato corrisponde al prezzo del disco S10.</span><span class="sxs-lookup"><span data-stu-id="e149b-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="e149b-110">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e149b-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e149b-111">**Sono previsti costi di transazione per i dischi gestiti Standard?**</span><span class="sxs-lookup"><span data-stu-id="e149b-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="e149b-112">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-112">Yes.</span></span> <span data-ttu-id="e149b-113">Sì, ogni transazione prevede un addebito.</span><span class="sxs-lookup"><span data-stu-id="e149b-113">You're charged for each transaction.</span></span> <span data-ttu-id="e149b-114">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e149b-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e149b-115">**Per un disco gestito Standard, si riceverà un addebito per le dimensioni effettive dei dati su disco o per la capacità con provisioning del disco?**</span><span class="sxs-lookup"><span data-stu-id="e149b-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="e149b-116">L'addebito viene effettuato in base alla capacità con provisioning del disco.</span><span class="sxs-lookup"><span data-stu-id="e149b-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="e149b-117">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e149b-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e149b-118">**In che modo il prezzo della versione Premium dei dischi gestiti è diverso da quello dei dischi non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="e149b-119">Il prezzo della versione Premium dei dischi gestiti è uguale a quello della versione Premium dei dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="e149b-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="e149b-120">**È possibile modificare il tipo di account di archiviazione (Standard o Premium) dei dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="e149b-121">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-121">Yes.</span></span> <span data-ttu-id="e149b-122">È possibile modificare il tipo di account di archiviazione dei dischi gestiti tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="e149b-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="e149b-123">**È possibile copiare o esportare un disco gestito in un account di archiviazione privato?**</span><span class="sxs-lookup"><span data-stu-id="e149b-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="e149b-124">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-124">Yes.</span></span> <span data-ttu-id="e149b-125">Sì, è possibile esportare i dischi gestiti tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="e149b-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="e149b-126">**È possibile usare un file di disco rigido virtuale in un account di archiviazione di Azure per creare un disco gestito con una sottoscrizione diversa?**</span><span class="sxs-lookup"><span data-stu-id="e149b-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="e149b-127">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-127">No.</span></span>

<span data-ttu-id="e149b-128">**È possibile usare un file di disco rigido virtuale in un account di archiviazione di Azure per creare un disco gestito in un'area geografica diversa?**</span><span class="sxs-lookup"><span data-stu-id="e149b-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="e149b-129">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-129">No.</span></span>

<span data-ttu-id="e149b-130">**Ci sono limitazioni di scalabilità per i clienti che usano dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="e149b-131">Managed Disks elimina i limiti legati agli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e149b-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="e149b-132">Tuttavia, il numero di dischi gestiti per ogni sottoscrizione è limitato a 2.000 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e149b-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="e149b-133">È possibile aumentare questo numero rivolgendosi al supporto.</span><span class="sxs-lookup"><span data-stu-id="e149b-133">You can call support to increase this number.</span></span>

<span data-ttu-id="e149b-134">**È possibile fare uno snapshot incrementale di un disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="e149b-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="e149b-135">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-135">No.</span></span> <span data-ttu-id="e149b-136">La funzionalità snapshot corrente crea una copia completa di un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="e149b-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="e149b-137">Tuttavia è previsto un supporto futuro per gli snapshot incrementali.</span><span class="sxs-lookup"><span data-stu-id="e149b-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="e149b-138">**Le macchine virtuali in un set di disponibilità possono essere composte da una combinazione di dischi gestiti e non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="e149b-139">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-139">No.</span></span> <span data-ttu-id="e149b-140">No, i dischi nelle macchine virtuali in un set di disponibilità devono essere o tutti gestiti o tutti non gestiti.</span><span class="sxs-lookup"><span data-stu-id="e149b-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="e149b-141">Quando si crea un set di disponibilità, è possibile scegliere il tipo di dischi da usare.</span><span class="sxs-lookup"><span data-stu-id="e149b-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="e149b-142">**Managed Disks è l'opzione predefinita nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="e149b-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="e149b-143">Non attualmente, ma diventerà l'impostazione predefinita in futuro.</span><span class="sxs-lookup"><span data-stu-id="e149b-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="e149b-144">**È possibile creare un disco vuoto gestito?**</span><span class="sxs-lookup"><span data-stu-id="e149b-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="e149b-145">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-145">Yes.</span></span> <span data-ttu-id="e149b-146">È possibile creare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="e149b-146">You can create an empty disk.</span></span> <span data-ttu-id="e149b-147">Un disco gestito può essere creato indipendentemente da una macchina virtuale, ad esempio non collegandolo a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e149b-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="e149b-148">**Qual è il numero di domini di errore supportati per un set di disponibilità con Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e149b-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="e149b-149">Il numero di domini di errore supportato per i set di disponibilità con Managed Disks è di 2 o 3, a seconda dell'area in cui si trovano.</span><span class="sxs-lookup"><span data-stu-id="e149b-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="e149b-150">**Come viene configurato l'account di archiviazione Standard per l'impostazione della diagnostica?**</span><span class="sxs-lookup"><span data-stu-id="e149b-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="e149b-151">Si imposta un account di archiviazione privato per la diagnostica della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e149b-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="e149b-152">In futuro, si intende estendere la diagnostica anche a Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e149b-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="e149b-153">**Che tipo di supporto per il controllo degli accessi in base al ruolo è disponibile per Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e149b-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="e149b-154">Managed Disks supporta tre ruoli predefiniti principali:</span><span class="sxs-lookup"><span data-stu-id="e149b-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="e149b-155">Proprietario: può gestire tutto, compresi gli accessi</span><span class="sxs-lookup"><span data-stu-id="e149b-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="e149b-156">Collaboratore: può gestire tutto ad eccezione degli accessi</span><span class="sxs-lookup"><span data-stu-id="e149b-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="e149b-157">Lettore: può visualizzare tutto, ma non apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="e149b-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="e149b-158">**È possibile copiare o esportare un disco gestito in un account di archiviazione privato?**</span><span class="sxs-lookup"><span data-stu-id="e149b-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="e149b-159">È possibile ottenere un URI di firma di accesso condiviso di sola lettura per il disco gestito e usarla per copiare i contenuti in un account di archiviazione privato o in un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="e149b-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="e149b-160">**È possibile creare una copia del proprio disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="e149b-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="e149b-161">I clienti possono eseguire uno snapshot dei relativi dischi gestiti e usarlo per creare un altro disco gestito.</span><span class="sxs-lookup"><span data-stu-id="e149b-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="e149b-162">**I dischi non gestiti sono ancora supportati?**</span><span class="sxs-lookup"><span data-stu-id="e149b-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="e149b-163">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-163">Yes.</span></span> <span data-ttu-id="e149b-164">Sì, sono supportati sia i dischi gestiti che quelli non gestiti.</span><span class="sxs-lookup"><span data-stu-id="e149b-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="e149b-165">È consigliabile usare i dischi gestiti per i nuovi carichi di lavoro ed eseguire la migrazione dei carichi di lavoro correnti a dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="e149b-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="e149b-166">**Se si crea un disco da 128 GB e si aumentano le dimensioni a 130 GB, verranno addebitati i costi relativi al livello di dimensioni successivo (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="e149b-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="e149b-167">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-167">Yes.</span></span>

<span data-ttu-id="e149b-168">**È possibile creare dischi gestiti per l'archiviazione con ridondanza locale, l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza della zona?**</span><span class="sxs-lookup"><span data-stu-id="e149b-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="e149b-169">Attualmente Azure Managed Disks supporta solo dischi gestiti per l'archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="e149b-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="e149b-170">**È possibile ridurre/ridimensionare i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="e149b-171">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-171">No.</span></span> <span data-ttu-id="e149b-172">Questa funzionalità non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="e149b-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="e149b-173">**È possibile modificare la proprietà del nome del computer quando si usa un disco del sistema operativo specializzato (non preparato con Utilità preparazione sistema o generalizzato) per il provisioning di una VM?**</span><span class="sxs-lookup"><span data-stu-id="e149b-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="e149b-174">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-174">No.</span></span> <span data-ttu-id="e149b-175">Non è possibile aggiornare la proprietà del nome del computer.</span><span class="sxs-lookup"><span data-stu-id="e149b-175">You can't update the computer name property.</span></span> <span data-ttu-id="e149b-176">La nuova VM eredita la proprietà dalla VM padre usata per creare il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e149b-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="e149b-177">**Dove si possono trovare modelli di Azure Resource Manager di esempio per creare macchine virtuali con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="e149b-178">Elenco di modelli che usano Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e149b-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="e149b-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="e149b-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="e149b-180">Managed Disks e crittografia del servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e149b-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="e149b-181">**La crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="e149b-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="e149b-182">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-182">Yes.</span></span>

<span data-ttu-id="e149b-183">**Chi gestisce le chiavi di crittografia?**</span><span class="sxs-lookup"><span data-stu-id="e149b-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="e149b-184">Le chiavi di crittografia sono gestite da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e149b-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="e149b-185">**È possibile disabilitare la crittografia del servizio di archiviazione per i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="e149b-186">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-186">No.</span></span>

<span data-ttu-id="e149b-187">**La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**</span><span class="sxs-lookup"><span data-stu-id="e149b-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="e149b-188">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-188">No.</span></span> <span data-ttu-id="e149b-189">È disponibile in tutte le aree in cui è disponibile Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e149b-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="e149b-190">Managed Disks è disponibile in tutte le aree pubbliche e in Germania.</span><span class="sxs-lookup"><span data-stu-id="e149b-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="e149b-191">**Come si può determinare se un disco gestito è crittografato?**</span><span class="sxs-lookup"><span data-stu-id="e149b-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="e149b-192">Si può scoprire quando è stato creato il disco gestito tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="e149b-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="e149b-193">Se è stato creato dopo il 9 giugno 2017, il disco è crittografato.</span><span class="sxs-lookup"><span data-stu-id="e149b-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="e149b-194">**Come è possibile crittografare i dischi esistenti creati prima del 10 giugno 2017?**</span><span class="sxs-lookup"><span data-stu-id="e149b-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="e149b-195">A partire dal 10 giugno 2017, i nuovi dati scritti nei dischi gestiti esistenti vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e149b-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="e149b-196">È anche prevista l'implementazione della crittografia dei dati esistenti, che verrà eseguita in modo asincrono in background.</span><span class="sxs-lookup"><span data-stu-id="e149b-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="e149b-197">Se è necessario crittografare i dati esistenti adesso, creare una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="e149b-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="e149b-198">I nuovi dischi verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="e149b-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="e149b-199">Copiare i dischi gestiti tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e149b-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="e149b-200">Copiare i dischi gestiti tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="e149b-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e149b-201">**Le immagini e gli snapshot gestiti vengono crittografati?**</span><span class="sxs-lookup"><span data-stu-id="e149b-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="e149b-202">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-202">Yes.</span></span> <span data-ttu-id="e149b-203">Tutte le immagini e gli snapshot gestiti creati dopo il 9 giugno 2017 vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e149b-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="e149b-204">**È possibile convertire macchine virtuali con dischi non gestiti ubicati in account di archiviazione che sono o sono stati crittografati in precedenza in VM con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="e149b-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="e149b-205">Sì</span><span class="sxs-lookup"><span data-stu-id="e149b-205">Yes</span></span>

<span data-ttu-id="e149b-206">**Un disco rigido virtuale esportato da un disco gestito o uno snapshot verrà crittografato?**</span><span class="sxs-lookup"><span data-stu-id="e149b-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="e149b-207">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-207">No.</span></span> <span data-ttu-id="e149b-208">Se però si esporta un disco rigido virtuale da un disco gestito o uno snapshot crittografato a un account di archiviazione crittografato, verrà crittografato.</span><span class="sxs-lookup"><span data-stu-id="e149b-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="e149b-209">Dischi Premium, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="e149b-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="e149b-210">**Se una macchina virtuale usa una serie di dimensioni che supporta Archiviazione Premium, ad esempio DSv2, è possibile collegare dischi dati sia Premium che Standard?**</span><span class="sxs-lookup"><span data-stu-id="e149b-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="e149b-211">Sì.</span><span class="sxs-lookup"><span data-stu-id="e149b-211">Yes.</span></span>

<span data-ttu-id="e149b-212">**È possibile collegare dischi sia Premium che Standard a una serie di dimensioni che non supporta Archiviazione Premium, come le serie D, Dv2, G o F?**</span><span class="sxs-lookup"><span data-stu-id="e149b-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="e149b-213">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-213">No.</span></span> <span data-ttu-id="e149b-214">È possibile collegare solo dischi dati Standard alle macchine virtuali che non usano una serie di dimensioni con supporto di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="e149b-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="e149b-215">**Se si crea un disco dati Premium da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="e149b-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="e149b-216">Un disco dati Premium creato da un disco rigido virtuale da 80 GB viene considerato come il disco Premium immediatamente successivo in termini di dimensioni, ovvero un disco P10.</span><span class="sxs-lookup"><span data-stu-id="e149b-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="e149b-217">Il costo addebitato corrisponde al prezzo del disco P10.</span><span class="sxs-lookup"><span data-stu-id="e149b-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="e149b-218">**Sono previsti costi per transazione per usare Archiviazione Premium?**</span><span class="sxs-lookup"><span data-stu-id="e149b-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="e149b-219">È previsto un costo fisso per ogni dimensione di disco con provisioning di un certo numero di IOPS e di una certa velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="e149b-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="e149b-220">Gli altri costi sono la larghezza di banda in uscita e la capacità di snapshot, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="e149b-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="e149b-221">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e149b-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e149b-222">**Quali sono i limiti per IOPS e velocità effettiva che è possibile ottenere dalla cache del disco?**</span><span class="sxs-lookup"><span data-stu-id="e149b-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="e149b-223">I limiti combinati per la cache e l'unità SSD locale per la serie DS sono 4.000 IOPS per core e 33 MB al secondo per core.</span><span class="sxs-lookup"><span data-stu-id="e149b-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="e149b-224">La serie GS offre 5,000 IOPS per core e 50 MB al secondo per core.</span><span class="sxs-lookup"><span data-stu-id="e149b-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="e149b-225">**Sono supportate le unità SSD locali per le macchine virtuali di Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e149b-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="e149b-226">L'unità SSD locale è un archivio temporaneo che è incluso in una macchina virtuale di Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e149b-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="e149b-227">Questa archiviazione temporanea non comporta costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="e149b-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="e149b-228">Si consiglia di non usare questa unità SSD locale per archiviare dati applicazione, perché non vengono salvati in modo permanente nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e149b-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="e149b-229">**L'uso di TRIM su dischi Premium ha ripercussioni?**</span><span class="sxs-lookup"><span data-stu-id="e149b-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="e149b-230">L'uso di TRIM su dischi Azure Premium o Standard non ha alcun impatto negativo.</span><span class="sxs-lookup"><span data-stu-id="e149b-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="e149b-231">Dimensioni dei nuovi dischi, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="e149b-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="e149b-232">**Quali sono le dimensioni massime supportate per i dischi dati e del sistema operativo?**</span><span class="sxs-lookup"><span data-stu-id="e149b-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="e149b-233">Il tipo di partizione supportata da Azure per un disco del sistema operativo è MBR (Master Boot Record).</span><span class="sxs-lookup"><span data-stu-id="e149b-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="e149b-234">Il formato MBR supporta dischi di dimensioni fino a 2 TB.</span><span class="sxs-lookup"><span data-stu-id="e149b-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="e149b-235">Azure supporta dischi del sistema operativo di dimensioni massime pari a 2 TB.</span><span class="sxs-lookup"><span data-stu-id="e149b-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="e149b-236">Azure supporta fino a 4 TB per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="e149b-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="e149b-237">**Quali sono le dimensioni massime supportate per un BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="e149b-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="e149b-238">Le dimensioni massime supportate da Azure per un BLOB di pagine sono di 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="e149b-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="e149b-239">Non sono supportati BLOB di pagine di dimensioni superiori a 4 TB (4.095 GB) collegati a una VM come dischi dati o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e149b-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="e149b-240">**È necessario usare una nuova versione degli strumenti di Azure per creare, collegare, ridimensionare e caricare dischi più grandi di 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="e149b-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="e149b-241">Non è necessario aggiornare gli strumenti di Azure esistenti per creare, collegare o ridimensionare i dischi di dimensioni superiori a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="e149b-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="e149b-242">Per caricare il file VHD dall'ambiente locale direttamente in Azure come BLOB di pagine o disco non gestito, è necessario usare i set di strumenti più recenti:</span><span class="sxs-lookup"><span data-stu-id="e149b-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="e149b-243">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="e149b-243">Azure tools</span></span>      | <span data-ttu-id="e149b-244">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="e149b-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="e149b-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e149b-245">Azure PowerShell</span></span> | <span data-ttu-id="e149b-246">Numero di versione 4.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="e149b-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="e149b-247">Interfaccia della riga di comando di Azure v1</span><span class="sxs-lookup"><span data-stu-id="e149b-247">Azure CLI v1</span></span>     | <span data-ttu-id="e149b-248">Numero di versione 0.10.13: versione di maggio 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="e149b-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="e149b-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="e149b-249">AzCopy</span></span>           | <span data-ttu-id="e149b-250">Numero di versione 6.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="e149b-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="e149b-251">Il supporto per l'interfaccia della riga di comando di Azure v2 e Azure Storage Explorer sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="e149b-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="e149b-252">**Le dimensioni del disco P4 e P6 sono supportate per i dischi gestiti o i BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="e149b-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="e149b-253">No.</span><span class="sxs-lookup"><span data-stu-id="e149b-253">No.</span></span> <span data-ttu-id="e149b-254">Le dimensioni del disco P4 (32 GB) e P6 (64 GB) sono supportate solo per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="e149b-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="e149b-255">Il supporto per dischi non gestiti e BLOB di pagine sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="e149b-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="e149b-256">**Come viene fatturato un disco gestito Premium di dimensioni inferiori a 64 GB creato prima dell'abilitazione dei dischi più piccoli (intorno al 15 giugno 2017)?**</span><span class="sxs-lookup"><span data-stu-id="e149b-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="e149b-257">I dischi Premium esistenti di dimensioni inferiori a 64 GB continuano a essere fatturati in base al piano tariffario P10.</span><span class="sxs-lookup"><span data-stu-id="e149b-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="e149b-258">**Come è possibile modificare il piano tariffario dei dischi Premium di dimensioni inferiori a 64 GB da P10 a P4 o P6?**</span><span class="sxs-lookup"><span data-stu-id="e149b-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="e149b-259">È possibile creare uno snapshot dei dischi di piccole dimensioni e quindi creare un disco per passare automaticamente al piano tariffario a P4 o P6 in base alla dimensione del disco di cui viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e149b-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="e149b-260">Cosa fare se non è disponibile una risposta alla domanda?</span><span class="sxs-lookup"><span data-stu-id="e149b-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="e149b-261">Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.</span><span class="sxs-lookup"><span data-stu-id="e149b-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="e149b-262">È possibile pubblicare una domanda nei commenti alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e149b-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="e149b-263">Per interagire con il team di Archiviazione di Azure e altri membri della community in merito a questo articolo, usare il [forum MSDN di Archiviazione di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="e149b-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="e149b-264">Per richiedere funzionalità, inviare richieste e idee al [forum dei commenti su Archiviazione di Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="e149b-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
