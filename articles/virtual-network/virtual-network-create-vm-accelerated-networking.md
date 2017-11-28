---
title: una macchina virtuale di Azure con accelerazione di rete aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una macchina virtuale con accelerazione di rete.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="9dac8-103">Creare una macchina virtuale con rete accelerata</span><span class="sxs-lookup"><span data-stu-id="9dac8-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="9dac8-104">In questa esercitazione, è illustrato come toocreate una macchina virtuale di Azure (VM) con accelerazione di rete.</span><span class="sxs-lookup"><span data-stu-id="9dac8-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="9dac8-105">La funzionalità di rete accelerata è disponibile a livello generale per Windows e in anteprima pubblica per distribuzioni Linux specifiche.</span><span class="sxs-lookup"><span data-stu-id="9dac8-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="9dac8-106">Rete accelerata consente single root i/o virtualization (SR-IOV) tooa VM, migliorando le prestazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="9dac8-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="9dac8-107">Questo percorso ad alte prestazioni Ignora host hello dal relativo al percorso dati hello riducendo la latenza e instabilità utilizzo della CPU, per l'utilizzo con hello più esigenti rete carichi di lavoro supportati tipi di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="9dac8-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="9dac8-108">Hello seguente immagine Mostra comunicazione tra due macchine virtuali (VM) con e senza la configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="9dac8-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Confronto](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="9dac8-110">Senza la configurazione di rete, tutto il traffico di rete da e verso hello VM deve attraversare host hello e commutatore virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="9dac8-111">commutatore virtuale Hello fornisce tutti i criteri, ad esempio come gruppi di sicurezza di rete accedere gli elenchi di controllo, l'isolamento e altro traffico di rete virtualizzata servizi toonetwork.</span><span class="sxs-lookup"><span data-stu-id="9dac8-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="9dac8-112">informazioni sui commutatori virtuali, leggere hello toolearn [virtualizzazione rete Hyper-V e il commutatore virtuale](https://technet.microsoft.com/library/jj945275.aspx) articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="9dac8-113">Con la rete con accelerata, traffico di rete arriva all'interfaccia di rete della macchina virtuale di hello (NIC) e verrà quindi inoltrato toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="9dac8-114">Tutti i criteri di rete che hello commutatore virtuale applicata senza rete accelerata vengono scaricate e applicate nell'hardware.</span><span class="sxs-lookup"><span data-stu-id="9dac8-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="9dac8-115">L'applicazione dei criteri in hardware Abilita hello NIC tooforward traffico di rete direttamente toohello macchina virtuale, ignorando host hello e lo switch virtuale hello, mantenendo tutti i criteri di hello in host hello è applicata.</span><span class="sxs-lookup"><span data-stu-id="9dac8-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="9dac8-116">Hello vantaggi delle reti con accelerazione si applicano solo toohello è abilitato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="9dac8-117">Per ottenere risultati ottimali hello è ideale tooenable questa funzionalità in almeno due macchine virtuali connesse toohello stessa rete virtuale di Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="9dac8-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="9dac8-118">Durante la comunicazione tra reti virtuali o la connessione locale, questa funzionalità presenta una latenza toooverall un impatto minimo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="9dac8-119">Questo Linux anteprima pubblica potrebbe non disporre hello dello stesso livello di disponibilità e affidabilità come le funzioni che sono in genere versione disponibilità.</span><span class="sxs-lookup"><span data-stu-id="9dac8-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="9dac8-120">Hello funzionalità non è supportato, può avere vincolato funzionalità e potrebbero non essere disponibili in tutte le posizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dac8-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="9dac8-121">Per più le notifiche di hello su disponibilità e lo stato di questa funzionalità, controllo pagina degli aggiornamenti di hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dac8-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="9dac8-122">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="9dac8-122">Benefits</span></span>
* <span data-ttu-id="9dac8-123">**Latenza più bassa / superiore pacchetti al secondo (pps):** rimozione hello il commutatore virtuale dal relativo al percorso dati hello rimuove hello tempo pacchetti nell'host di hello per l'elaborazione di criteri e aumenta hello numero di pacchetti che possono essere elaborati all'interno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="9dac8-124">**Ridotto instabilità:** commutatore virtuale elaborazione dipende dalla quantità hello di criteri che deve toobe applicato e hello del carico di lavoro di hello CPU che esegue l'elaborazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="9dac8-125">Offload hardware toohello imposizione dei criteri di hello rimuove tale variabilità offrendo pacchetti direttamente attiva toohello VM, rimuovendo la comunicazione tra tooVM di hello host e tutti i software interrupt e contesto.</span><span class="sxs-lookup"><span data-stu-id="9dac8-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="9dac8-126">**Ridurre l'utilizzo della CPU:** esclusione hello il commutatore virtuale nell'host di hello comporta l'utilizzo della CPU tooless per elaborare il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="9dac8-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="9dac8-127"><a name="Limitations"></a>Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9dac8-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="9dac8-128">Hello limitazioni seguenti esiste quando si utilizza questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="9dac8-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="9dac8-129">**Creazione di un'interfaccia di rete**: la funzionalità rete accelerata può essere abilitata solo per una nuova scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="9dac8-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="9dac8-130">Non può essere abilitata per una scheda di interfaccia di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="9dac8-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="9dac8-131">**Creazione della macchina virtuale:** una scheda NIC con la rete accelerata abilitata possono solo essere collegato tooa VM quando hello viene creata la VM.</span><span class="sxs-lookup"><span data-stu-id="9dac8-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="9dac8-132">Hello NIC non può essere collegato tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="9dac8-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="9dac8-133">**Aree**: le VM Windows con rete accelerata sono disponibili nella maggior parte delle aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dac8-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="9dac8-134">Le VM Linux con rete accelerata sono disponibili in più aree.</span><span class="sxs-lookup"><span data-stu-id="9dac8-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="9dac8-135">Questa funzionalità è disponibile nelle aree di Hello all'espansione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="9dac8-136">Vedere blog di Azure Aggiorna rete virtuale hello sotto per informazioni più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="9dac8-137">**Sistemi operativi supportati**: Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9dac8-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="9dac8-138">Linux: Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superiore, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (pubblicato da "Rogue Wave Software").</span><span class="sxs-lookup"><span data-stu-id="9dac8-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="9dac8-139">**Dimensione della VM**: dimensioni di istanza per scopo generico e con ottimizzazione per il calcolo con otto o più memorie centrali.</span><span class="sxs-lookup"><span data-stu-id="9dac8-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="9dac8-140">Per ulteriori informazioni, vedere hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="9dac8-141">set di dimensioni di istanza di macchina virtuale supportate Hello verranno espanse in hello future.</span><span class="sxs-lookup"><span data-stu-id="9dac8-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="9dac8-142">**Solo distribuzione tramite Azure Resource Manager (ARM):** la rete accelerata non è disponibile per la distribuzione tramite ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="9dac8-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="9dac8-143">Limitazioni di toothese le modifiche vengono annunciate tramite hello [le funzionalità di rete virtuale di Azure Aggiorna](https://azure.microsoft.com/updates/accelerated-networking-in-preview) pagina.</span><span class="sxs-lookup"><span data-stu-id="9dac8-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="9dac8-144">Creare un'app Windows</span><span class="sxs-lookup"><span data-stu-id="9dac8-144">Create a Windows VM</span></span>
<span data-ttu-id="9dac8-145">È possibile utilizzare hello portale di Azure o Azure [PowerShell](#windows-powershell) toocreate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="9dac8-146"><a name="windows-portal"></a>Portale</span><span class="sxs-lookup"><span data-stu-id="9dac8-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="9dac8-147">Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9dac8-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9dac8-148">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9dac8-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9dac8-149">Nel portale di hello, fare clic su **+ nuovo** > **calcolo** > **Data Center di Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="9dac8-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="9dac8-150">In hello **Data Center di Windows Server 2016** pannello viene visualizzato, lasciare *Gestione risorse* selezionato in **selezionare un modello di distribuzione**, fare clic su **crea** .</span><span class="sxs-lookup"><span data-stu-id="9dac8-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="9dac8-151">In hello **nozioni di base** blade che viene visualizzata, immettere i seguenti valori hello, lasciare hello rimanenti opzioni predefinite o selezionare o immettere valori personalizzati, quindi scegliere hello **OK** pulsante:</span><span class="sxs-lookup"><span data-stu-id="9dac8-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="9dac8-152">Impostazione</span><span class="sxs-lookup"><span data-stu-id="9dac8-152">Setting</span></span>|<span data-ttu-id="9dac8-153">Valore</span><span class="sxs-lookup"><span data-stu-id="9dac8-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="9dac8-154">Nome</span><span class="sxs-lookup"><span data-stu-id="9dac8-154">Name</span></span>|<span data-ttu-id="9dac8-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="9dac8-155">MyVm</span></span>|
    |<span data-ttu-id="9dac8-156">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9dac8-156">Resource group</span></span>|<span data-ttu-id="9dac8-157">Lasciare selezionata l'opzione **Crea nuovo** e immettere *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="9dac8-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="9dac8-158">Località</span><span class="sxs-lookup"><span data-stu-id="9dac8-158">Location</span></span>|<span data-ttu-id="9dac8-159">Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="9dac8-159">West US 2</span></span>|

    <span data-ttu-id="9dac8-160">Se si tooAzure nuovo, altre informazioni, vedere [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [percorsi](https://azure.microsoft.com/regions) (che sono anche definiti tooas aree).</span><span class="sxs-lookup"><span data-stu-id="9dac8-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="9dac8-161">In hello **scegliere una dimensione** blade che viene visualizzata, immettere *8* in hello **numero minimo di core** casella, quindi fare clic su **visualizzare tutti**.</span><span class="sxs-lookup"><span data-stu-id="9dac8-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="9dac8-162">Fare clic su **DS4_V2 Standard**, o qualsiasi macchina virtuale è supportato, quindi fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="9dac8-163">In hello **impostazioni** pannello visualizzato, lasciare tutte le impostazioni come-è, ad eccezione di fare clic su **abilitato** in **Accelerated rete**, quindi fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="9dac8-164">**Nota:** se, nei passaggi precedenti, si selezionano i valori per dimensioni, il sistema operativo o percorso macchina virtuale che non sono elencati in hello [limitazioni](#Limitations) sezione di questo articolo, **Accelerated rete**non è visibile.</span><span class="sxs-lookup"><span data-stu-id="9dac8-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="9dac8-165">In hello **riepilogo** pannello visualizzato, fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="9dac8-166">Azure avvia hello VM di creazione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="9dac8-167">La creazione della VM richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9dac8-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="9dac8-168">hello tooinstall accelerated driver di rete per Windows, hello completato i passaggi in hello [configurare Windows](#configure-windows) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="9dac8-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dac8-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="9dac8-170">Installare hello la versione più recente di Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="9dac8-171">Se si tooAzure nuovo PowerShell, leggere hello [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="9dac8-172">Avviare una sessione di PowerShell facendo clic sul pulsante Start di Windows hello, digitando **powershell**, quindi fare clic su **PowerShell** dai risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="9dac8-173">Nella finestra di PowerShell, immettere hello `login-azurermaccount` toosign comando con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9dac8-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9dac8-174">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9dac8-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="9dac8-175">Nel browser, copiare lo script seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9dac8-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="9dac8-176">Nella finestra di PowerShell, fare doppio clic su script hello toopaste e avviare l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="9dac8-177">Vengono richiesti un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="9dac8-177">You are prompted for a username and password.</span></span> <span data-ttu-id="9dac8-178">Utilizzare queste toolog credenziali in toohello VM quando ci si connette tooit nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="9dac8-179">Se si verifica un errore di script hello e modificate nello script hello valori prima dell'esecuzione, verificare i valori hello è utilizzato per le dimensioni di macchina virtuale, il sistema operativo, e posizione sono elencate nella hello [limitazioni](#Limitations) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="9dac8-180">hello tooinstall accelerated driver di rete per Windows, hello completato i passaggi in hello [configurare Windows](#configure-windows) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="9dac8-181"><a name="configure-windows"></a>Configurare Windows</span><span class="sxs-lookup"><span data-stu-id="9dac8-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="9dac8-182">Dopo aver creato hello VM in Azure, è necessario installare i driver di rete con accelerazione hello per Windows.</span><span class="sxs-lookup"><span data-stu-id="9dac8-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="9dac8-183">Prima di completare hello alla procedura seguente, è necessario avere creato una macchina virtuale Windows con la rete accelerata utilizzando entrambi hello [portale](#windows-portal) o [PowerShell](#windows-powershell) i passaggi in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="9dac8-184">Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9dac8-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9dac8-185">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9dac8-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9dac8-186">Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="9dac8-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="9dac8-187">Quando **MyVm** viene visualizzato nei risultati della ricerca hello, selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="9dac8-188">In hello **MyVm** pannello visualizzato, fare clic su hello **Connetti** pulsante hello alto a sinistra del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="9dac8-189">**Nota:** se **creazione** è visibile in hello **Connetti** pulsante, Azure non è ancora terminata hello VM di creazione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="9dac8-190">Fare clic su **Connetti** solo dopo che non si visualizzano più **creazione** in hello **Connetti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="9dac8-191">Consenti il hello toodownload browser **MyVm.rdp** file.</span><span class="sxs-lookup"><span data-stu-id="9dac8-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="9dac8-192">Una volta scaricato, fare clic su tooopen file hello è.</span><span class="sxs-lookup"><span data-stu-id="9dac8-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="9dac8-193">Fare clic su hello **Connetti** pulsante hello **connessione Desktop remoto** visualizzata, viene indicato che hello non è possibile identificare l'autore della connessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="9dac8-194">In hello **la sicurezza di Windows** casella viene visualizzata, fare clic su **altre scelte**, quindi fare clic su **utilizzare un account diverso**.</span><span class="sxs-lookup"><span data-stu-id="9dac8-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="9dac8-195">Immettere nome utente hello e la password immessa nel passaggio 4, quindi fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="9dac8-196">Fare clic su hello **Sì** pulsante nella finestra di connessione Desktop remoto hello visualizzata, viene indicato che è Impossibile verificare l'identità di hello del computer remoto hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="9dac8-197">Fare doppio clic su pulsante Start di Windows hello e fare clic su **Gestione dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="9dac8-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="9dac8-198">Espandere hello **schede di rete** nodo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="9dac8-199">Verificare che hello **scheda Ethernet di funzione virtuale Mellanox ConnectX-3** viene visualizzato, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="9dac8-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Gestione dispositivi](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="9dac8-201">La funzionalità di rete accelerata è ora abilitata per la VM.</span><span class="sxs-lookup"><span data-stu-id="9dac8-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="9dac8-202">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="9dac8-202">Create a Linux VM</span></span>
<span data-ttu-id="9dac8-203">È possibile utilizzare hello portale di Azure o Azure [PowerShell](#linux-powershell) toocreate un Ubuntu o SLES VM.</span><span class="sxs-lookup"><span data-stu-id="9dac8-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="9dac8-204">Per le VM RHEL e CentOS, il flusso di lavoro è diverso.</span><span class="sxs-lookup"><span data-stu-id="9dac8-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="9dac8-205">Vedere le istruzioni di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="9dac8-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="9dac8-206"><a name="linux-portal"></a>Portale</span><span class="sxs-lookup"><span data-stu-id="9dac8-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="9dac8-207">Registrazione per l'accelerazione di rete per l'anteprima di Linux, completare i passaggi da 1 a 5 di hello hello [creare una VM Linux - PowerShell](#linux-powershell) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="9dac8-208">È possibile registrare per l'anteprima di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="9dac8-209">Completare i passaggi 1-8 in hello [creare una macchina virtuale Windows - portale](#windows-portal) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="9dac8-210">Nel passaggio 2 fare clic su **Ubuntu Server 16.04 LTS** anziché su **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="9dac8-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="9dac8-211">Per questa esercitazione, scegliere toouse una password, anziché una chiave SSH, anche se per le distribuzioni di produzione, è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="9dac8-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="9dac8-212">Se **Accelerated rete** non viene visualizzato al termine di passaggio 7 di hello [creare una macchina virtuale Windows - portale](#windows-portal) sezione di questo articolo, è probabile che per uno dei seguenti motivi hello:</span><span class="sxs-lookup"><span data-stu-id="9dac8-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="9dac8-213">Per l'anteprima di hello non ancora registrato.</span><span class="sxs-lookup"><span data-stu-id="9dac8-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="9dac8-214">Verificare che lo stato di registrazione sia **registrati**, come illustrato nel passaggio 4 di hello [creare una VM Linux - Powershell](#linux-powershell) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="9dac8-215">**Nota:** se si è partecipato alla hello Accelerated di rete per l'anteprima di macchine virtuali di Windows (il non toouse tooregister necessario più tempo accelerazione di rete per le macchine virtuali di Windows), non vengono registrate automaticamente per hello Accelerated rete per Visualizzare in anteprima le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="9dac8-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="9dac8-216">È necessario registrare hello Accelerated di rete per le macchine virtuali Linux anteprima tooparticipate in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="9dac8-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="9dac8-217">Non è stata selezionata una dimensione, del sistema operativo o percorso indicato nella hello VM [limitazioni](#limitations) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="9dac8-218">hello tooinstall accelerated driver di rete per Linux, hello completato i passaggi in hello [configurare Linux](#configure-linux) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="9dac8-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dac8-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="9dac8-220">Se si creare macchine virtuali Linux con la rete in una sottoscrizione e quindi tenta una macchina virtuale Windows con la rete accelerata in hello toocreate stessa sottoscrizione, creazione della macchina virtuale di Windows hello potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="9dac8-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="9dac8-221">Durante questa anteprima è consigliabile testare le VM Windows e Linux con rete accelerata in sottoscrizioni distinte.</span><span class="sxs-lookup"><span data-stu-id="9dac8-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="9dac8-222">Installare hello la versione più recente di Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="9dac8-223">Se si tooAzure nuovo PowerShell, leggere hello [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="9dac8-224">Avviare una sessione di PowerShell facendo clic sul pulsante Start di Windows hello, digitando **powershell**, quindi fare clic su **PowerShell** dai risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="9dac8-225">Nella finestra di PowerShell, immettere hello `login-azurermaccount` toosign comando con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9dac8-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9dac8-226">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9dac8-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="9dac8-227">Registrazione per l'accelerazione di rete per Azure hello anteprima completando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9dac8-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="9dac8-228">Inviare un messaggio di posta elettronica troppo[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con l'ID sottoscrizione di Azure e l'utilizzo previsto.</span><span class="sxs-lookup"><span data-stu-id="9dac8-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="9dac8-229">Attendere la conferma tramite posta elettronica dell'abilitazione della sottoscrizione da parte di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9dac8-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="9dac8-230">Immettere hello tooconfirm comando che sono registrati per l'anteprima di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dac8-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="9dac8-231">Non proseguire con il passaggio 5 fino a **registrati** viene visualizzato nell'output dopo l'immissione hello precedente comando hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="9dac8-232">L'output deve essere simile seguente hello output prima di continuare:</span><span class="sxs-lookup"><span data-stu-id="9dac8-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="9dac8-233">Se si è partecipato alla hello Accelerated di rete per l'anteprima di macchine virtuali di Windows (il non toouse tooregister necessario più tempo accelerazione di rete per le macchine virtuali di Windows), non vengono registrate automaticamente per hello Accelerated di rete per l'anteprima di macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="9dac8-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="9dac8-234">È necessario registrare hello Accelerated di rete per le macchine virtuali Linux anteprima tooparticipate in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="9dac8-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="9dac8-235">Nel browser, copiare lo script sostituendo Ubuntu o SLES desiderato seguente hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="9dac8-236">Anche in questo caso, Redhat e CentOS prevedono un flusso di lavoro diverso, illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9dac8-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="9dac8-237">Nella finestra di PowerShell, fare doppio clic su script hello toopaste e avviare l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="9dac8-238">Vengono richiesti un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="9dac8-238">You are prompted for a username and password.</span></span> <span data-ttu-id="9dac8-239">Utilizzare queste toolog credenziali in toohello VM quando ci si connette tooit nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="9dac8-240">Se hello script non riesce, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="9dac8-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="9dac8-241">Sono registrati per l'anteprima di hello, come illustrato nel passaggio 4</span><span class="sxs-lookup"><span data-stu-id="9dac8-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="9dac8-242">Se si modificati dimensioni, tipo di sistema operativo o i valori di posizione nello script hello VM prima dell'esecuzione, sono elencati i valori hello in hello [limitazioni](#Limitations) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="9dac8-243">hello tooinstall accelerated driver di rete per Linux, hello completato i passaggi in hello [configurare Linux](#configure-linux) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="9dac8-244"><a name="configure-linux"></a>Configurare Linux</span><span class="sxs-lookup"><span data-stu-id="9dac8-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="9dac8-245">Dopo aver creato hello VM in Azure, è necessario installare i driver di rete con accelerazione hello per Linux.</span><span class="sxs-lookup"><span data-stu-id="9dac8-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="9dac8-246">Prima di completare hello alla procedura seguente, è necessario avere creato una VM Linux con la rete accelerata utilizzando entrambi hello [portale](#linux-portal) o [PowerShell](#linux-powershell) i passaggi in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="9dac8-247">Aprire un browser Internet, hello Azure [portale](https://portal.azure.com) e accedere con di Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9dac8-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9dac8-248">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9dac8-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9dac8-249">Nella parte superiore di hello del diritto toohello portale, di hello di hello *individuare risorse* barra, fare clic su hello **> _** toostart icona una shell di cloud Bash (anteprima).</span><span class="sxs-lookup"><span data-stu-id="9dac8-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="9dac8-250">Hello Bash cloud shell riquadro viene visualizzato nella parte inferiore di hello del portale hello e dopo alcuni secondi, presenta un  **username@Azure:~ $** prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9dac8-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="9dac8-251">Se è possibile SSH toohello macchina virtuale del computer, piuttosto che shell cloud hello, istruzioni di hello in questa esercitazione si presuppone che shell cloud hello in uso.</span><span class="sxs-lookup"><span data-stu-id="9dac8-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="9dac8-252">Nella parte superiore di hello del portale hello, nella casella hello contenente testo hello *individuare risorse*, tipo *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="9dac8-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="9dac8-253">Quando **MyVm** viene visualizzato nei risultati della ricerca hello, selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="9dac8-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="9dac8-254">In hello **MyVm** pannello visualizzato, fare clic su hello **Connetti** pulsante hello alto a sinistra del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="9dac8-255">**Nota:** se **creazione** è visibile in hello **Connetti** pulsante, Azure non è ancora terminata hello VM di creazione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="9dac8-256">Fare clic su **Connetti** solo dopo che non si visualizzano più **creazione** in hello **Connetti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9dac8-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="9dac8-257">Azure consente di aprire una finestra informa hello tooenter `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="9dac8-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="9dac8-258">Immettere questo comando hello cloud shell (o copia dalla casella hello che venivano visualizzate nel passaggio 4 e incollarlo nella shell di cloud toohello), quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9dac8-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="9dac8-259">Invio **Sì** toohello desiderano se si desidera che la connessione toocontinue, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9dac8-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="9dac8-260">Immettere la password di hello che immessi durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="9dac8-261">Dopo aver connesso toohello macchina virtuale, viene visualizzato un adminuser@MyVm:~ prompt$.</span><span class="sxs-lookup"><span data-stu-id="9dac8-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="9dac8-262">Si è connessi a questo punto toohello VM tramite una sessione della shell hello cloud.</span><span class="sxs-lookup"><span data-stu-id="9dac8-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="9dac8-263">**Nota**: le sessioni cloud shell vanno in timeout dopo 10 minuti di inattività.</span><span class="sxs-lookup"><span data-stu-id="9dac8-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="9dac8-264">A questo punto, le istruzioni di hello variano in base distribuzione hello in uso.</span><span class="sxs-lookup"><span data-stu-id="9dac8-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="9dac8-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="9dac8-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="9dac8-266">Al prompt dei comandi hello, immettere `uname -r` e verificare la versione di hello per:</span><span class="sxs-lookup"><span data-stu-id="9dac8-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="9dac8-267">Per Ubuntu, "4.4.0-77-generic" o versione superiore</span><span class="sxs-lookup"><span data-stu-id="9dac8-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="9dac8-268">Per SLES, "4.4.59-92.20-default" o versione superiore</span><span class="sxs-lookup"><span data-stu-id="9dac8-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="9dac8-269">Creare un legame tra vNIC di rete standard hello e vNIC rete hello accelerata dall'esecuzione di comandi hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="9dac8-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="9dac8-270">Il traffico di rete utilizza hello migliori prestazioni con accelerata rete scheda di rete virtuale, mentre obbligazione hello assicura che il traffico di rete non venga interrotta tra alcune modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="9dac8-271">Dopo l'esecuzione dello script, hello hello VM verrà riavviato dopo un secondo 60 sospendere.</span><span class="sxs-lookup"><span data-stu-id="9dac8-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="9dac8-272">Una volta hello VM viene riavviata, riconnettersi tooit completando i passaggi da 5 a 7 nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9dac8-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="9dac8-273">Eseguire hello `ifconfig` comando e verificare che è risultata bond0 interfaccia hello è visualizzato come backup.</span><span class="sxs-lookup"><span data-stu-id="9dac8-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="9dac8-274">Le applicazioni con una rete con accelerata devono comunicare su hello *bond0* interfaccia, non *eth0*.</span><span class="sxs-lookup"><span data-stu-id="9dac8-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="9dac8-275">può modificare il nome di interfaccia Hello prima accelerata rete raggiunge disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="9dac8-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="9dac8-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="9dac8-276">RHEL/CentOS</span></span>

<span data-ttu-id="9dac8-277">Creazione di una macchina virtuale 7.3 CentOS Red Hat Enterprise Linux richiede alcuni ulteriori passaggi tooload hello più recente i driver necessari per SR-IOV e hello driver VF (Virtual Function) della scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="9dac8-278">Hello prima fase di istruzioni hello prepara un'immagine che può essere utilizzato toomake uno o più macchine virtuali che includono driver hello precaricati.</span><span class="sxs-lookup"><span data-stu-id="9dac8-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="9dac8-279">Fase 1: Preparare un'immagine di base Red Hat Enterprise Linux o CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="9dac8-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="9dac8-280">Effettuare il provisioning di una VM CentOS 7.3 non SR-IOV in Azure</span><span class="sxs-lookup"><span data-stu-id="9dac8-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="9dac8-281">Installare LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="9dac8-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="9dac8-282">Scaricare i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="9dac8-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="9dac8-283">Effettuare il deprovisioning della VM</span><span class="sxs-lookup"><span data-stu-id="9dac8-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="9dac8-284">Dal portale di Azure, arrestare la macchina virtuale; e passare i "dischi del tooVM", URI VHD dell'hello OSDisk acquisizione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="9dac8-285">Questo URI contiene hello base nome dell'immagine disco rigido virtuale e il relativo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9dac8-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="9dac8-286">Fase 2: Effettuare il provisioning delle nuove VM in Azure</span><span class="sxs-lookup"><span data-stu-id="9dac8-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="9dac8-287">Eseguire il provisioning di nuove macchine virtuali in base con New-AzureRMVMConfig utilizzando hello base immagine VHD acquisito in fase di uno, con AcceleratedNetworking abilitata nella scheda di rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="9dac8-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="9dac8-288">Dopo l'avviano di macchine virtuali, controllare il dispositivo di VF hello da "lspci" e verificare voce Mellanox hello.</span><span class="sxs-lookup"><span data-stu-id="9dac8-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="9dac8-289">Ad esempio, questo elemento di output di hello lspci dovremmo vedere:</span><span class="sxs-lookup"><span data-stu-id="9dac8-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="9dac8-290">Eseguire script partnership hello da:</span><span class="sxs-lookup"><span data-stu-id="9dac8-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="9dac8-291">Riavviare il computer hello nuove macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="9dac8-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="9dac8-292">Hello VM deve iniziare con bond0 configurato e hello percorso Accelerated rete abilitato.</span><span class="sxs-lookup"><span data-stu-id="9dac8-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="9dac8-293">Eseguire `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="9dac8-293">Run `ifconfig` tooconfirm.</span></span>
