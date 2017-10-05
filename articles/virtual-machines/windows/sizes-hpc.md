---
title: Dimensioni delle macchine virtuali Windows di Azure - HPC | Documentazione Microsoft
description: Elenca le diverse dimensioni disponibili per le macchine virtuali High Performance Computing Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="f0781-103">Dimensioni delle VM High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="f0781-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="f0781-104">Istanze con supporto per RDMA</span><span class="sxs-lookup"><span data-stu-id="f0781-104">RDMA-capable instances</span></span>
<span data-ttu-id="f0781-105">Un subset delle istanze a elevato uso di calcolo (H16r, H16mr, A8 e A9) è dotato di un'interfaccia di rete per la connettività ad accesso diretto a memoria remota (RDMA).</span><span class="sxs-lookup"><span data-stu-id="f0781-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="f0781-106">Questa interfaccia è un'aggiunta all'interfaccia di rete di Azure standard disponibile per gli altri formati di VM.</span><span class="sxs-lookup"><span data-stu-id="f0781-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="f0781-107">Questa interfaccia consente alle istanze con supporto per RDMA di comunicare attraverso una rete InfiniBand che funziona a velocità FDR per macchine virtuali H16r e H16mr e a velocità QDR per macchine virtuali A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="f0781-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="f0781-108">Queste funzionalità RDMA possono migliorare la scalabilità e le prestazioni delle applicazioni di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="f0781-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="f0781-109">Per accedere alla rete RDMA di Azure, i requisiti per le macchine virtuali Windows con supporto per RDMA sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0781-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="f0781-110">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="f0781-110">**Operating system**</span></span>
  
  <span data-ttu-id="f0781-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f0781-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f0781-112">Windows Server 2016 non supporta attualmente la connettività RDMA in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0781-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="f0781-113">**Set di disponibilità o servizio cloud**: distribuire le VM con supporto per RDMA nello stesso set di disponibilità, se si usa il modello di distribuzione Azure Resource Manager, o nello stesso servizio cloud, se si usa il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f0781-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="f0781-114">Se si usa Azure Batch, le VM con supporto di RDMA devono trovarsi nello stesso pool.</span><span class="sxs-lookup"><span data-stu-id="f0781-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="f0781-115">**MPI** : Microsoft MPI (MS-MPI) 2012 R2 o versione successiva, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="f0781-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="f0781-116">Le implementazioni MPI supportate usano l'interfaccia Microsoft Network Direct per la comunicazione tra le istanze.</span><span class="sxs-lookup"><span data-stu-id="f0781-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="f0781-117">**Spazio degli indirizzi della rete RDMA** : la rete RDMA in Azure riserva lo spazio degli indirizzi 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="f0781-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="f0781-118">Per eseguire applicazioni MPI in istanze distribuite in una rete virtuale di Azure, assicurarsi che lo spazio degli indirizzi di rete virtuale non si sovrapponga alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="f0781-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="f0781-119">**Estensione macchina virtuale HpcVmDrivers**: nelle VM con supporto per RDMA, è necessario aggiungere l'estensione HpcVmDrivers per installare i driver dei dispositivi di rete Windows per la connettività RDMA.</span><span class="sxs-lookup"><span data-stu-id="f0781-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="f0781-120">In alcune distribuzioni di istanze A8 e A9 l'estensione HpcVmDrivers viene aggiunta automaticamente. Per aggiungere l'estensione macchina virtuale a una macchina virtuale, è possibile usare i cmdlet di [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0781-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="f0781-121">Il comando seguente installa l'ultima versione 1.1 dell'estensione HpcVMDrivers in una macchina virtuale esistente con supporto per RDMA, denominata *myVM* distribuita nel gruppo di risorse denominato *myResourceGroup* nell'area *Stati Uniti occidentali*:</span><span class="sxs-lookup"><span data-stu-id="f0781-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="f0781-122">Per altre informazioni, vedere [Estensioni e funzionalità della macchina virtuale](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0781-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f0781-123">È anche possibile usare estensioni delle macchine virtuali nel [modello di distribuzione classico](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="f0781-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="f0781-124">Utilizzo di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="f0781-124">Using HPC Pack</span></span>

<span data-ttu-id="f0781-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), la soluzione di gestione di processi e cloud HPC gratuita di Microsoft, è un'opzione per creare un cluster di elaborazione in Azure per l'esecuzione di applicazioni MPI basate su Windows e altri carichi di lavoro HPC.</span><span class="sxs-lookup"><span data-stu-id="f0781-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="f0781-126">HPC Pack 2012 R2 e versioni successive include un ambiente di runtime per MS-MPI che può usare la rete RDMA di Azure quando viene distribuito in macchine virtuali con supporto per RDMA.</span><span class="sxs-lookup"><span data-stu-id="f0781-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="f0781-127">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="f0781-127">Other sizes</span></span>
- [<span data-ttu-id="f0781-128">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="f0781-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="f0781-129">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="f0781-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="f0781-130">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="f0781-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="f0781-131">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="f0781-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="f0781-132">Ottimizzate per la GPU</span><span class="sxs-lookup"><span data-stu-id="f0781-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="f0781-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0781-133">Next steps</span></span>

- <span data-ttu-id="f0781-134">Per gli elenchi di controllo per usare le istanze a elevato utilizzo di calcolo con HPC Pack in Windows Server, vedere [Configurare un cluster di Windows RDMA con HPC Pack per eseguire applicazioni MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0781-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="f0781-135">Per usare istanze a elevato uso di calcolo quando si eseguono applicazioni MPI con Azure Batch, vedere [Usare le attività a istanze multiple per eseguire applicazioni MPI (Message Passing Interface) in Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="f0781-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="f0781-136">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0781-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




