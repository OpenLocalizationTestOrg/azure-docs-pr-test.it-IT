---
title: Creare una macchina virtuale di Azure con rete accelerata | Microsoft Docs
description: Informazioni su come creare una macchina virtuale con rete accelerata.
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
ms.openlocfilehash: 449425189a3b42dcb2c31316c1c8e38fac69d761
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="7e769-103">Creare una macchina virtuale con rete accelerata</span><span class="sxs-lookup"><span data-stu-id="7e769-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="7e769-104">Questa esercitazione spiega come creare una macchina virtuale (VM) di Azure con rete accelerata.</span><span class="sxs-lookup"><span data-stu-id="7e769-104">In this tutorial, you learn how to create an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="7e769-105">La funzionalità di rete accelerata è disponibile a livello generale per Windows e in anteprima pubblica per distribuzioni Linux specifiche.</span><span class="sxs-lookup"><span data-stu-id="7e769-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="7e769-106">La funzionalità rete accelerata abilita Single Root I/O Virtualization (SR-IOV) per le VM, migliorandone le prestazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="7e769-106">Accelerated networking enables single root I/O virtualization (SR-IOV) to a VM, greatly improving its networking performance.</span></span> <span data-ttu-id="7e769-107">Questo percorso a prestazioni elevate ignora l'host del percorso dati riducendo la latenza, l'instabilità e l'utilizzo della CPU e può essere usato con i carichi di lavoro di rete più gravosi nei tipi di VM supportati.</span><span class="sxs-lookup"><span data-stu-id="7e769-107">This high-performance path bypasses the host from the datapath reducing latency, jitter, and CPU utilization, for use with the most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="7e769-108">L'immagine seguente illustra le comunicazioni tra due macchine virtuali (VM), con e senza rete accelerata:</span><span class="sxs-lookup"><span data-stu-id="7e769-108">The following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Confronto](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="7e769-110">Senza rete accelerata, tutto il traffico di rete in ingresso e in uscita dalla VM deve attraversare l'host e il commutatore virtuale.</span><span class="sxs-lookup"><span data-stu-id="7e769-110">Without accelerated networking, all networking traffic in and out of the VM must traverse the host and the virtual switch.</span></span> <span data-ttu-id="7e769-111">Quest'ultimo è responsabile dell'applicazione di tutti i criteri al traffico di rete, ad esempio gruppi di sicurezza di rete, elenchi di controllo di accesso, isolamento e altri servizi di rete virtualizzati.</span><span class="sxs-lookup"><span data-stu-id="7e769-111">The virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services to network traffic.</span></span> <span data-ttu-id="7e769-112">Per altre informazioni sui commutatori virtuali, vedere l'articolo [Hyper-V Network Virtualization and Virtual Switch](https://technet.microsoft.com/library/jj945275.aspx) (Virtualizzazione rete Hyper-V e commutatore virtuale).</span><span class="sxs-lookup"><span data-stu-id="7e769-112">To learn more about virtual switches, read the [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="7e769-113">Con rete accelerata, il traffico di rete raggiunge la scheda di interfaccia di rete della VM e quindi viene inoltrato alla VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-113">With accelerated networking, network traffic arrives at the VM's network interface (NIC), and is then forwarded to the VM.</span></span> <span data-ttu-id="7e769-114">Il carico di tutti i criteri di rete applicati dal commutatore virtuale senza rete accelerata viene ripartito e applicato all'hardware.</span><span class="sxs-lookup"><span data-stu-id="7e769-114">All network policies that the virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="7e769-115">L'applicazione dei criteri all'hardware permette alla scheda di rete di inoltrare il traffico di rete direttamente alla macchina virtuale ignorando l'host e il commutatore virtuale, pur mantenendo tutti i criteri applicati all'host.</span><span class="sxs-lookup"><span data-stu-id="7e769-115">Applying policy in hardware enables the NIC to forward network traffic directly to the VM, bypassing the host and the virtual switch, while maintaining all the policy it applied in the host.</span></span>

<span data-ttu-id="7e769-116">I vantaggi della funzionalità rete accelerata si applicano solo alla VM in cui è abilitata.</span><span class="sxs-lookup"><span data-stu-id="7e769-116">The benefits of accelerated networking only apply to the VM that it is enabled on.</span></span> <span data-ttu-id="7e769-117">Per ottenere risultati ottimali, è consigliabile abilitarla in almeno due VM connesse alla stessa Rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-117">For the best results, it is ideal to enable this feature on at least two VMs connected to the same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="7e769-118">Nella comunicazione tra reti virtuali o nella connessione locale questa funzionalità ha un impatto minimo sulla latenza complessiva.</span><span class="sxs-lookup"><span data-stu-id="7e769-118">When communicating across VNets or connecting on-premises, this feature has minimal impact to overall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="7e769-119">Questa anteprima pubblica di Linux potrebbe non avere lo stesso livello di disponibilità e affidabilità delle funzionalità presenti nella versione con disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="7e769-119">This Linux Public Preview may not have the same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="7e769-120">La funzionalità non è supportata, potrebbe avere funzioni vincolate e potrebbe non essere disponibile in tutte le località di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-120">The feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="7e769-121">Per ricevere le notifiche più aggiornate su disponibilità e stato della funzionalità, vedere la pagina relativa agli aggiornamenti della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-121">For the most up-to-date notifications on availability and status of this feature, check the Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="7e769-122">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="7e769-122">Benefits</span></span>
* <span data-ttu-id="7e769-123">**Latenza più bassa e più pacchetti al secondo (pps):** rimuovendo il commutatore virtuale dal percorso dati viene eliminato il tempo di attesa dei pacchetti nell'host per l'elaborazione dei criteri, aumentando così il numero di pacchetti che possono essere elaborati all'interno della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7e769-123">**Lower Latency / Higher packets per second (pps):** Removing the virtual switch from the datapath removes the time packets spend in the host for policy processing and increases the number of packets that can be processed inside the VM.</span></span>
* <span data-ttu-id="7e769-124">**Instabilità ridotta:** l'elaborazione del commutatore dipende dalla quantità di criteri da applicare e dal carico di lavoro della CPU che esegue l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7e769-124">**Reduced jitter:** Virtual switch processing depends on the amount of policy that needs to be applied and the workload of the CPU that is doing the processing.</span></span> <span data-ttu-id="7e769-125">La ripartizione del carico di applicazione dei criteri nell'hardware elimina tale variabilità recapitando i pacchetti direttamente alla macchina virtuale, rimuovendo l'host dalle comunicazioni con la macchina virtuale nonché tutte le interruzioni software e i cambi di contesto.</span><span class="sxs-lookup"><span data-stu-id="7e769-125">Offloading the policy enforcement to the hardware removes that variability by delivering packets directly to the VM, removing the host to VM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="7e769-126">**Utilizzo ridotto della CPU:** ignorando il commutatore virtuale nell'host si ottiene un minore utilizzo della CPU per l'elaborazione del traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="7e769-126">**Decreased CPU utilization:** Bypassing the virtual switch in the host leads to less CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="7e769-127"><a name="Limitations"></a>Limitazioni</span><span class="sxs-lookup"><span data-stu-id="7e769-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="7e769-128">L'uso della funzionalità Rete accelerata presenta le limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e769-128">The following limitations exist when using this capability:</span></span>

* <span data-ttu-id="7e769-129">**Creazione di un'interfaccia di rete**: la funzionalità rete accelerata può essere abilitata solo per una nuova scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="7e769-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="7e769-130">Non può essere abilitata per una scheda di interfaccia di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="7e769-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="7e769-131">**Creazione di una VM**: una scheda di interfaccia di rete con rete accelerata abilitata può essere collegata a una VM solo durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-131">**VM creation:** A NIC with accelerated networking enabled can only be attached to a VM when the VM is created.</span></span> <span data-ttu-id="7e769-132">Non è possibile collegare la scheda di interfaccia di rete a una VM esistente.</span><span class="sxs-lookup"><span data-stu-id="7e769-132">The NIC cannot be attached to an existing VM.</span></span>
* <span data-ttu-id="7e769-133">**Aree**: le VM Windows con rete accelerata sono disponibili nella maggior parte delle aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="7e769-134">Le VM Linux con rete accelerata sono disponibili in più aree.</span><span class="sxs-lookup"><span data-stu-id="7e769-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="7e769-135">Le aree in cui viene offerta questa funzionalità stanno aumentando.</span><span class="sxs-lookup"><span data-stu-id="7e769-135">The regions this capability is available in is expanding.</span></span> <span data-ttu-id="7e769-136">Per informazioni aggiornate, vedere la pagina relativa agli aggiornamenti su Rete virtuale di Azure riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e769-136">Please see the Azure Virtual Networking Updates blog below for the latest information.</span></span>   
* <span data-ttu-id="7e769-137">**Sistemi operativi supportati**: Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7e769-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="7e769-138">Linux: Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superiore, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (pubblicato da "Rogue Wave Software").</span><span class="sxs-lookup"><span data-stu-id="7e769-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="7e769-139">**Dimensione della VM**: dimensioni di istanza per scopo generico e con ottimizzazione per il calcolo con otto o più memorie centrali.</span><span class="sxs-lookup"><span data-stu-id="7e769-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="7e769-140">Per altre informazioni, vedere gli articoli sulle dimensioni delle VM di [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e769-140">For more information, see the [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="7e769-141">In futuro il set di dimensioni delle istanze di macchina virtuale supportate verrà ampliato.</span><span class="sxs-lookup"><span data-stu-id="7e769-141">The set of supported VM instance sizes will expand in the future.</span></span>
* <span data-ttu-id="7e769-142">**Solo distribuzione tramite Azure Resource Manager (ARM):** la rete accelerata non è disponibile per la distribuzione tramite ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="7e769-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="7e769-143">Le modifiche apportate a queste limitazioni sono annunciate nella pagina relativa agli [aggiornamenti sulla Rete virtuale di Azure](https://azure.microsoft.com/updates/accelerated-networking-in-preview).</span><span class="sxs-lookup"><span data-stu-id="7e769-143">Changes to these limitations are announced through the [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="7e769-144">Creare un'app Windows</span><span class="sxs-lookup"><span data-stu-id="7e769-144">Create a Windows VM</span></span>
<span data-ttu-id="7e769-145">Per creare la VM è possibile usare il portale di Azure o Azure [PowerShell](#windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="7e769-145">You can use the Azure portal or Azure [PowerShell](#windows-powershell) to create the VM.</span></span>

### <span data-ttu-id="7e769-146"><a name="windows-portal"></a>Portale</span><span class="sxs-lookup"><span data-stu-id="7e769-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="7e769-147">In un browser Internet passare al [portale](https://portal.azure.com) di Azure ed eseguire l'accesso con l'[account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-147">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="7e769-148">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="7e769-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="7e769-149">Nel portale fare clic su **+ Nuovo** > **Calcolo** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="7e769-149">In the portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="7e769-150">Nel pannello **Windows Server 2016 Datacenter** che viene visualizzato lasciare selezionato *Resource Manager* sotto **Selezionare un modello di distribuzione** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7e769-150">In the **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="7e769-151">Nel pannello **Informazioni di base** che viene visualizzato immettere i valori seguenti, per le altre opzioni lasciare i valori predefiniti o immettere i valori desiderati e fare clic sul pulsante **OK**:</span><span class="sxs-lookup"><span data-stu-id="7e769-151">In the **Basics** blade that appears, enter the following values, leave the remaining default options or select or enter your own values, and click the **OK** button:</span></span>

    |<span data-ttu-id="7e769-152">Impostazione</span><span class="sxs-lookup"><span data-stu-id="7e769-152">Setting</span></span>|<span data-ttu-id="7e769-153">Valore</span><span class="sxs-lookup"><span data-stu-id="7e769-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="7e769-154">Nome</span><span class="sxs-lookup"><span data-stu-id="7e769-154">Name</span></span>|<span data-ttu-id="7e769-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="7e769-155">MyVm</span></span>|
    |<span data-ttu-id="7e769-156">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7e769-156">Resource group</span></span>|<span data-ttu-id="7e769-157">Lasciare selezionata l'opzione **Crea nuovo** e immettere *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="7e769-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="7e769-158">Località</span><span class="sxs-lookup"><span data-stu-id="7e769-158">Location</span></span>|<span data-ttu-id="7e769-159">Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="7e769-159">West US 2</span></span>|

    <span data-ttu-id="7e769-160">Se non si ha familiarità con Azure, vedere altre informazioni su [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [posizioni](https://azure.microsoft.com/regions) (anche chiamati aree).</span><span class="sxs-lookup"><span data-stu-id="7e769-160">If you're new to Azure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred to as regions).</span></span>
5. <span data-ttu-id="7e769-161">Nel pannello **Scegli una dimensione** che viene visualizzato immettere *8* nella casella **Minimum cores** (Numero minimo di memorie centrali), quindi fare clic su **Visualizza tutto**.</span><span class="sxs-lookup"><span data-stu-id="7e769-161">In the **Choose a size** blade that appears, enter *8* in the **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="7e769-162">Fare clic su **DS4 Standard v2** o qualsiasi VM supportata e quindi sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="7e769-162">Click **DS4_V2 Standard**, or any supported VM, then click the **Select** button.</span></span>
7. <span data-ttu-id="7e769-163">Nel pannello **Impostazioni** lasciare invariate tutte le impostazioni, fare clic solo su **Abilitato** sotto **Rete accelerata** e quindi fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e769-163">In the **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click the **OK** button.</span></span> <span data-ttu-id="7e769-164">**Nota**: se nei passaggi precedenti si selezionano valori per la dimensione della VM, il sistema operativo o la posizione che non sono elencati nella sezione [Limitazioni](#Limitations) di questo articolo, **Rete accelerata** non è visibile.</span><span class="sxs-lookup"><span data-stu-id="7e769-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in the [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="7e769-165">Nel pannello **Riepilogo** che viene visualizzato fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e769-165">In the **Summary** blade that appears, click the **OK** button.</span></span> <span data-ttu-id="7e769-166">Azure inizia a creare la VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-166">Azure starts creating the VM.</span></span> <span data-ttu-id="7e769-167">La creazione della VM richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="7e769-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="7e769-168">Per installare il driver di rete accelerata per Windows completare i passaggi della sezione [Configurare Windows](#configure-windows) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-168">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="7e769-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e769-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="7e769-170">Installare la versione più recente del modulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e769-170">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="7e769-171">Se non si ha familiarità con Azure PowerShell, vedere l'articolo [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e769-171">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="7e769-172">Avviare una sessione di PowerShell facendo clic sul pulsante Start, digitando **powershell** e facendo clic su **PowerShell** fra i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e769-172">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="7e769-173">Nella finestra di PowerShell immettere il comando `login-azurermaccount` per eseguire l'accesso con l'[account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-173">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="7e769-174">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="7e769-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="7e769-175">Nel browser copiare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="7e769-175">In your browser, copy the following script:</span></span>
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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="7e769-176">Nella finestra di PowerShell fare clic con il pulsante destro del mouse per incollare lo script e avviarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7e769-176">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="7e769-177">Vengono richiesti un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="7e769-177">You are prompted for a username and password.</span></span> <span data-ttu-id="7e769-178">Usare queste credenziali per accedere alla VM quando la si connette nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="7e769-178">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="7e769-179">Se lo script non riesce e i valori dello script sono stati modificati prima dell'esecuzione, verificare che i valori utilizzati per la dimensione della VM, il sistema operativo e la posizione siano elencati nella sezione [Limitazioni](#Limitations) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-179">If the script fails, and you changed values in the script before executing it, confirm the values you used for VM size, operating system, and location are listed in the [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="7e769-180">Per installare il driver di rete accelerata per Windows completare i passaggi della sezione [Configurare Windows](#configure-windows) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-180">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="7e769-181"><a name="configure-windows"></a>Configurare Windows</span><span class="sxs-lookup"><span data-stu-id="7e769-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="7e769-182">Dopo aver creato la VM in Azure, è necessario installare il driver di rete accelerata per Windows.</span><span class="sxs-lookup"><span data-stu-id="7e769-182">Once you create the VM in Azure, you must install the accelerated networking driver for Windows.</span></span> <span data-ttu-id="7e769-183">Prima di completare i passaggi seguenti occorre avere creato una VM Windows con rete accelerata mediante i passaggi relativi al [portale](#windows-portal) o a [PowerShell](#windows-powershell) indicati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-183">Before completing the following steps, you must have created a Windows VM with accelerated networking using either the [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="7e769-184">In un browser Internet passare al [portale](https://portal.azure.com) di Azure ed eseguire l'accesso con l'[account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-184">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="7e769-185">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="7e769-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="7e769-186">Nella finestra che contiene il testo *Cerca risorse*, nella parte superiore del portale di Azure, digitare *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="7e769-186">In the box that contains the text *Search resources* at the top of the Azure portal, type *MyVm*.</span></span> <span data-ttu-id="7e769-187">Fare clic su **MyVm** quando viene visualizzato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e769-187">When **MyVm** appears in the search results, click it.</span></span>
3. <span data-ttu-id="7e769-188">Nel pannello **MyVm** che viene visualizzato fare clic sul pulsante **Connetti** nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e769-188">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="7e769-189">**Nota**: se **Creazione in corso** è visibile sotto il pulsante **Connetti**, Azure non ha ancora terminato la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-189">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="7e769-190">Fare clic su **Connetti** solo dopo che **Creazione in corso** non è più visibile sotto il pulsante **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="7e769-190">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
4. <span data-ttu-id="7e769-191">Consentire al browser di scaricare il file **MyVm.rdp**.</span><span class="sxs-lookup"><span data-stu-id="7e769-191">Allow your browser to download the **MyVm.rdp** file.</span></span>  <span data-ttu-id="7e769-192">Dopo averlo scaricato, fare clic sul file per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="7e769-192">Once downloaded, click the file to open it.</span></span> 
5. <span data-ttu-id="7e769-193">Fare clic sul pulsante **Connetti** nella finestra di dialogo **Connessione Desktop remoto** che viene visualizzata e riporta l'avviso che non è possibile identificare l'autore della connessione remota.</span><span class="sxs-lookup"><span data-stu-id="7e769-193">Click the **Connect** button in the **Remote Desktop Connection** box that appears, notifying you that the publisher of the remote connection can't be identified.</span></span>
6. <span data-ttu-id="7e769-194">Nella finestra di dialogo  **Protezione di Windows**  che viene visualizzata fare clic su **Altre scelte** e quindi fare clic su **Usa un account diverso**.</span><span class="sxs-lookup"><span data-stu-id="7e769-194">In the **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="7e769-195">Immettere il nome utente e la password inseriti al passaggio 4 e fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e769-195">Enter the username and password you entered in step 4, then click the **OK** button.</span></span>
7. <span data-ttu-id="7e769-196">Fare clic sul pulsante **Sì** nella finestra di dialogo Connessione desktop remoto che viene visualizzata e riporta l'avviso che l'identità del computer remoto non può essere verificata.</span><span class="sxs-lookup"><span data-stu-id="7e769-196">Click the **Yes** button in the Remote Desktop Connection box that appears, notifying you that the identity of the remote computer cannot be verified.</span></span>
8. <span data-ttu-id="7e769-197">Fare clic con il pulsante destro del mouse sul pulsante Start di Windows e scegliere **Gestione dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="7e769-197">Right-click the Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="7e769-198">Espandere il nodo **Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="7e769-198">Expand the **Network adapters** node.</span></span> <span data-ttu-id="7e769-199">Verificare che sia visualizzata la voce **Scheda Ethernet VF Mellanox ConnectX-3**, come illustra la figura seguente:</span><span class="sxs-lookup"><span data-stu-id="7e769-199">Confirm that the **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in the following picture:</span></span>
   
    ![Gestione dispositivi](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="7e769-201">La funzionalità di rete accelerata è ora abilitata per la VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="7e769-202">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="7e769-202">Create a Linux VM</span></span>
<span data-ttu-id="7e769-203">Per creare una VM Ubuntu o SLES è possibile usare il portale di Azure o Azure [PowerShell](#linux-powershell).</span><span class="sxs-lookup"><span data-stu-id="7e769-203">You can use the Azure portal or Azure [PowerShell](#linux-powershell) to create an Ubuntu or SLES VM.</span></span> <span data-ttu-id="7e769-204">Per le VM RHEL e CentOS, il flusso di lavoro è diverso.</span><span class="sxs-lookup"><span data-stu-id="7e769-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="7e769-205">Vedere le istruzioni riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e769-205">Please see the instructions below.</span></span>

### <span data-ttu-id="7e769-206"><a name="linux-portal"></a>Portale</span><span class="sxs-lookup"><span data-stu-id="7e769-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="7e769-207">Registrarsi per l'anteprima della rete accelerata per Linux completando i passaggi 1-5 della sezione [Creare una VM Linux - PowerShell](#linux-powershell) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-207">Register for the accelerated networking for Linux preview by completing steps 1-5 of the [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="7e769-208">Non è possibile registrarsi per l'anteprima nel portale.</span><span class="sxs-lookup"><span data-stu-id="7e769-208">You cannot register for the preview in the portal.</span></span>
2. <span data-ttu-id="7e769-209">Completare i passaggi 1-8 della sezione [Creare una VM Windows - portale](#windows-portal) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-209">Complete steps 1-8 in the [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="7e769-210">Nel passaggio 2 fare clic su **Ubuntu Server 16.04 LTS** anziché su **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="7e769-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="7e769-211">Per questa esercitazione scegliere di usare una password anziché una chiave SSH, anche se per le distribuzioni di produzione è possibile usare entrambe.</span><span class="sxs-lookup"><span data-stu-id="7e769-211">For this tutorial, choose to use a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="7e769-212">Se l'opzione **Rete accelerata** non è visualizzata quando si completa il passaggio 7 della sezione [Creare una VM Windows - portale](#windows-portal) di questo articolo, è probabile che il motivo sia uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e769-212">If **Accelerated networking** does not appear when you complete step 7 of the [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of the following reasons:</span></span>
    - <span data-ttu-id="7e769-213">Non si è ancora registrati per l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="7e769-213">You are not yet registered for the preview.</span></span> <span data-ttu-id="7e769-214">Verificare che lo stato della registrazione sia **Registered**, come illustrato nel passaggio 4 della sezione [Creare una VM Linux - PowerShell](#linux-powershell) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-214">Confirm that your registration state is **Registered**, as explained in step 4 of the [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="7e769-215">**Nota**: se si è partecipato all'anteprima della rete accelerata per VM Windows (non è più necessario registrarsi per l'uso della rete accelerata per VM Windows), non si viene automaticamente registrati anche per l'anteprima della rete accelerata per VM Linux.</span><span class="sxs-lookup"><span data-stu-id="7e769-215">**Note:** If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="7e769-216">Per partecipare all'anteprima della rete accelerata per VM Linux è necessario registrarsi per tale anteprima.</span><span class="sxs-lookup"><span data-stu-id="7e769-216">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
    - <span data-ttu-id="7e769-217">Non è stata selezionata una dimensione di VM, un sistema operativo o una posizione nella sezione [Limitazioni](#limitations) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-217">You have not selected a VM size, operating system, or location listed in the [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="7e769-218">Per installare il driver di rete accelerata per Linux completare i passaggi della sezione [Configurare Linux](#configure-linux) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-218">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="7e769-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e769-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="7e769-220">Se si creano VM Linux con rete accelerata in una sottoscrizione e quindi si tenta di creare una VM Windows con rete accelerata nella stessa sottoscrizione, la creazione della VM Windows potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="7e769-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt to create a Windows VM with accelerated networking in the same subscription, the Windows VM creation may fail.</span></span> <span data-ttu-id="7e769-221">Durante questa anteprima è consigliabile testare le VM Windows e Linux con rete accelerata in sottoscrizioni distinte.</span><span class="sxs-lookup"><span data-stu-id="7e769-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="7e769-222">Installare la versione più recente del modulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e769-222">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="7e769-223">Se non si ha familiarità con Azure PowerShell, vedere l'articolo [Panoramica di Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e769-223">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="7e769-224">Avviare una sessione di PowerShell facendo clic sul pulsante Start, digitando **powershell** e facendo clic su **PowerShell** fra i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e769-224">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="7e769-225">Nella finestra di PowerShell immettere il comando `login-azurermaccount` per eseguire l'accesso con l'[account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-225">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="7e769-226">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="7e769-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="7e769-227">Registrarsi per l'anteprima della rete accelerata per Azure completando i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e769-227">Register for the accelerated networking for Azure preview by completing the following steps:</span></span>
    - <span data-ttu-id="7e769-228">Inviare un messaggio di posta elettronica a [ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con l'ID sottoscrizione di Azure e l'utilizzo previsto.</span><span class="sxs-lookup"><span data-stu-id="7e769-228">Send an email to [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="7e769-229">Attendere la conferma tramite posta elettronica dell'abilitazione della sottoscrizione da parte di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e769-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="7e769-230">Immettere il comando seguente per verificare di essere registrati per l'anteprima:</span><span class="sxs-lookup"><span data-stu-id="7e769-230">Enter the following command to confirm you are registered for the preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="7e769-231">Non proseguire con il passaggio 5 fino a quando nell'output appare **Registered** dopo aver immesso il comando precedente.</span><span class="sxs-lookup"><span data-stu-id="7e769-231">Do not continue with step 5 until **Registered** appears in the output after you enter the previous command.</span></span> <span data-ttu-id="7e769-232">L'output deve essere simile al seguente prima di continuare:</span><span class="sxs-lookup"><span data-stu-id="7e769-232">Your output must look like the following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="7e769-233">Se si è partecipato all'anteprima della rete accelerata per VM Windows (non è più necessario registrarsi per l'uso della rete accelerata per VM Windows), non si viene automaticamente registrati anche per l'anteprima della rete accelerata per VM Linux.</span><span class="sxs-lookup"><span data-stu-id="7e769-233">If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="7e769-234">Per partecipare all'anteprima della rete accelerata per VM Linux è necessario registrarsi per tale anteprima.</span><span class="sxs-lookup"><span data-stu-id="7e769-234">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
      >
5. <span data-ttu-id="7e769-235">Nel browser copiare lo script seguente, sostituendo Ubuntu o SLES in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7e769-235">In your browser, copy the following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="7e769-236">Anche in questo caso, Redhat e CentOS prevedono un flusso di lavoro diverso, illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e769-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define the new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="7e769-237">Nella finestra di PowerShell fare clic con il pulsante destro del mouse per incollare lo script e avviarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7e769-237">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="7e769-238">Vengono richiesti un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="7e769-238">You are prompted for a username and password.</span></span> <span data-ttu-id="7e769-239">Usare queste credenziali per accedere alla VM quando la si connette nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="7e769-239">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="7e769-240">Se lo script non riesce, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="7e769-240">If the script fails, confirm that:</span></span>
    - <span data-ttu-id="7e769-241">Di essere registrati per l'anteprima, come descritto al passaggio 4</span><span class="sxs-lookup"><span data-stu-id="7e769-241">You are registered for the preview, as explained in step 4</span></span>
    - <span data-ttu-id="7e769-242">Se sono stati modificati i valori di dimensione della VM, tipo di sistema operativo o posizione nello script prima di eseguirlo, che i valori siano elencati nella sezione [Limitazioni](#Limitations) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-242">If you changed VM size, operating system type, or location values in the script before executing it, that the values are listed in the [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="7e769-243">Per installare il driver di rete accelerata per Linux completare i passaggi della sezione [Configurare Linux](#configure-linux) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-243">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="7e769-244"><a name="configure-linux"></a>Configurare Linux</span><span class="sxs-lookup"><span data-stu-id="7e769-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="7e769-245">Dopo aver creato la VM in Azure, è necessario installare il driver di rete accelerata per Linux.</span><span class="sxs-lookup"><span data-stu-id="7e769-245">Once you create the VM in Azure, you must install the accelerated networking driver for Linux.</span></span> <span data-ttu-id="7e769-246">Prima di completare i passaggi seguenti è necessario avere creato una VM Linux con rete accelerata mediante i passaggi relativi al [portale](#linux-portal) o a [PowerShell](#linux-powershell) indicati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e769-246">Before completing the following steps, you must have created a Linux VM with accelerated networking using either the [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="7e769-247">In un browser Internet passare al [portale](https://portal.azure.com) di Azure ed eseguire l'accesso con l'[account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e769-247">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="7e769-248">Se non si ha un account, è possibile registrarsi per ottenere una [versione di prova gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="7e769-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="7e769-249">Nella parte superiore del portale, a destra della barra *Cerca risorse*, fare clic sull'icona **> _** per avviare una cloud shell Bash (anteprima).</span><span class="sxs-lookup"><span data-stu-id="7e769-249">At the top of the portal, to the right of the *Search resources* bar, click the **>_** icon to start a Bash cloud shell (Preview).</span></span> <span data-ttu-id="7e769-250">Il riquadro della cloud shell Bash viene visualizzato nella parte inferiore del portale e dopo alcuni secondi mostra il prompt **username@Azure:~$**.</span><span class="sxs-lookup"><span data-stu-id="7e769-250">The Bash cloud shell pane appears at the bottom of the portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="7e769-251">Anche se è possibile eseguire SSH alla VM dal computer, anziché dalla cloud shell, le istruzioni di questa esercitazione presuppongono che si usi la cloud shell.</span><span class="sxs-lookup"><span data-stu-id="7e769-251">Though you can SSH to the VM from your computer, rather than the cloud shell, the instructions in this tutorial assume you're using the cloud shell.</span></span>
3. <span data-ttu-id="7e769-252">Nella parte superiore del portale, nella finestra che contiene il testo *Cerca risorse*, digitare *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="7e769-252">At the top of the portal, in the box that contains the text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="7e769-253">Fare clic su **MyVm** quando viene visualizzato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e769-253">When **MyVm** appears in the search results, click it.</span></span>
4. <span data-ttu-id="7e769-254">Nel pannello **MyVm** che viene visualizzato fare clic sul pulsante **Connetti** nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e769-254">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="7e769-255">**Nota**: se **Creazione in corso** è visibile sotto il pulsante **Connetti**, Azure non ha ancora terminato la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-255">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="7e769-256">Fare clic su **Connetti** solo dopo che **Creazione in corso** non è più visibile sotto il pulsante **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="7e769-256">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
5. <span data-ttu-id="7e769-257">Azure apre una finestra di dialogo che richiede di immettere il `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="7e769-257">Azure opens a box telling you to enter the `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="7e769-258">Immettere questo comando nella cloud shell (o copiarlo dalla finestra visualizzata nel passaggio 4 e incollarlo nella cloud shell) e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="7e769-258">Enter this command in the cloud shell (or copy it from the box that appeared in step 4 and paste it in to the cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="7e769-259">Scegliere **Sì** come risposta alla domanda se si desidera continuare a connettersi, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="7e769-259">Enter **yes** to the question asking you if you want to continue connecting, then press Enter.</span></span>
7. <span data-ttu-id="7e769-260">Immettere la password specificata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="7e769-260">Enter the password you entered when creating the VM.</span></span> <span data-ttu-id="7e769-261">Dopo aver effettuato l'accesso alla VM, viene visualizzato il prompt adminuser@MyVm:~$.</span><span class="sxs-lookup"><span data-stu-id="7e769-261">Once successfully logged in to the VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="7e769-262">Ora si è connessi alla VM tramite la sessione cloud shell.</span><span class="sxs-lookup"><span data-stu-id="7e769-262">You are now logged in to the VM through the cloud shell session.</span></span> <span data-ttu-id="7e769-263">**Nota**: le sessioni cloud shell vanno in timeout dopo 10 minuti di inattività.</span><span class="sxs-lookup"><span data-stu-id="7e769-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="7e769-264">A questo punto, le istruzioni variano in base alla distribuzione in uso.</span><span class="sxs-lookup"><span data-stu-id="7e769-264">At this point, the instructions vary based on the distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="7e769-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="7e769-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="7e769-266">Al prompt immettere `uname -r` e verificare la versione seguente:</span><span class="sxs-lookup"><span data-stu-id="7e769-266">At the prompt, enter `uname -r` and confirm the version for:</span></span>

    * <span data-ttu-id="7e769-267">Per Ubuntu, "4.4.0-77-generic" o versione superiore</span><span class="sxs-lookup"><span data-stu-id="7e769-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="7e769-268">Per SLES, "4.4.59-92.20-default" o versione superiore</span><span class="sxs-lookup"><span data-stu-id="7e769-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="7e769-269">Creare un legame tra la scheda di interfaccia di rete virtuale standard e la scheda di interfaccia di rete virtuale accelerata eseguendo i comandi che seguono.</span><span class="sxs-lookup"><span data-stu-id="7e769-269">Create a bond between the standard networking vNIC and the accelerated networking vNIC by running the commands that follow.</span></span> <span data-ttu-id="7e769-270">Il traffico di rete usa la scheda di interfaccia di rete virtuale accelerata, più efficiente, mentre il legame assicura che il traffico di rete non venga interrotto tra determinate modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7e769-270">Network traffic uses the higher performing accelerated networking vNIC, while the bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="7e769-271">Al termine dell'esecuzione dello script, la VM verrà riavviata dopo una pausa di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="7e769-271">After running the script, the VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="7e769-272">Dopo il riavvio della VM riconnetterla completando di nuovo i passaggi 5-7.</span><span class="sxs-lookup"><span data-stu-id="7e769-272">Once the VM is restarted, reconnect to it by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="7e769-273">Eseguire il comando `ifconfig`, verificare che sia comparso bond0 e che per l'interfaccia ci sia l'indicazione UP.</span><span class="sxs-lookup"><span data-stu-id="7e769-273">Run the `ifconfig` command and confirm that bond0 has come up and the interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="7e769-274">Le applicazioni che usano la rete accelerata devono comunicare sull'interfaccia *bond0*, non su *eth0*.</span><span class="sxs-lookup"><span data-stu-id="7e769-274">Applications using accelerated networking must communicate over the *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="7e769-275">Il nome di interfaccia può cambiare prima che la rete accelerata raggiunga la disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="7e769-275">The interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="7e769-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="7e769-276">RHEL/CentOS</span></span>

<span data-ttu-id="7e769-277">La creazione di una VM Red Hat Enterprise Linux o CentOS 7.3 richiede alcuni passaggi aggiuntivi per caricare i driver più recenti necessari per SR-IOV e il driver Virtual Function (VF) per la scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="7e769-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps to load the latest drivers needed for SR-IOV and the Virtual Function (VF) driver for the network card.</span></span> <span data-ttu-id="7e769-278">La prima fase delle istruzioni prevede la preparazione di un'immagine che potrà essere usata per creare una o più macchine virtuali con i driver precaricati.</span><span class="sxs-lookup"><span data-stu-id="7e769-278">The first phase of the instructions prepares an image that can be used to make one or more virtual machines that have the drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="7e769-279">Fase 1: Preparare un'immagine di base Red Hat Enterprise Linux o CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="7e769-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="7e769-280">Effettuare il provisioning di una VM CentOS 7.3 non SR-IOV in Azure</span><span class="sxs-lookup"><span data-stu-id="7e769-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="7e769-281">Installare LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="7e769-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="7e769-282">Scaricare i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="7e769-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="7e769-283">Effettuare il deprovisioning della VM</span><span class="sxs-lookup"><span data-stu-id="7e769-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="7e769-284">Nel portale di Azure arrestare la VM e passare ai dischi della VM per acquisire l'URI del disco rigido virtuale del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7e769-284">From Azure portal, stop this VM; and go to VM’s "Disks", capture the OSDisk’s VHD URI.</span></span> <span data-ttu-id="7e769-285">Questo URI contiene il nome del disco rigido virtuale dell'immagine di base e il relativo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7e769-285">This URI contains the base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="7e769-286">Fase 2: Effettuare il provisioning delle nuove VM in Azure</span><span class="sxs-lookup"><span data-stu-id="7e769-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="7e769-287">Effettuare il provisioning delle nuove VM con New-AzureRMVMConfig usando il disco rigido virtuale dell'immagine di base acquisito nella fase 1, con la funzionalità di rete accelerata abilitata nella scheda di interfaccia di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="7e769-287">Provision new VMs based with New-AzureRMVMConfig using the base image VHD captured in phase one, with AcceleratedNetworking enabled on the vNIC:</span></span>

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
    
    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify the base image's VHD URI (from phase one step 5). 
    # Note: The storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need to replace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for the location from which the new image binary large object (BLOB) is copied to start the virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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
    
    # Create the virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="7e769-288">Dopo l'avvio delle VM, controllare il dispositivo VF con "lspci" e verificare la voce Mellanox.</span><span class="sxs-lookup"><span data-stu-id="7e769-288">After VMs boot up, check the VF device by "lspci" and check the Mellanox entry.</span></span> <span data-ttu-id="7e769-289">Nell'output di lspci, ad esempio, dovrebbe essere visualizzato questo elemento:</span><span class="sxs-lookup"><span data-stu-id="7e769-289">For example, we should see this item in the lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="7e769-290">Eseguire lo script di associazione con:</span><span class="sxs-lookup"><span data-stu-id="7e769-290">Run the bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="7e769-291">Riavviare le nuove VM:</span><span class="sxs-lookup"><span data-stu-id="7e769-291">Reboot the new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="7e769-292">La VM verrà avviata con l'interfaccia bond0 configurata e il percorso di rete accelerata abilitato.</span><span class="sxs-lookup"><span data-stu-id="7e769-292">The VM should start with bond0 configured and the Accelerated Networking path enabled.</span></span>  <span data-ttu-id="7e769-293">Eseguire `ifconfig` per verificare.</span><span class="sxs-lookup"><span data-stu-id="7e769-293">Run `ifconfig` to confirm.</span></span>
