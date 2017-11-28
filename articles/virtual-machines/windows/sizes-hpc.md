---
title: dimensioni delle macchine Virtuali di Windows di aaaAzure - HPC | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibile per Windows elaborazione a elevate prestazioni macchine virtuali in Azure.
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
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="513b1-103">Dimensioni delle VM High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="513b1-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="513b1-104">Istanze con supporto per RDMA</span><span class="sxs-lookup"><span data-stu-id="513b1-104">RDMA-capable instances</span></span>
<span data-ttu-id="513b1-105">Un subset delle istanze con utilizzo intensivo di calcolo di hello (H16r, H16mr, A8 e A9) funzionalità di un'interfaccia di rete per la connettività diretto a memoria remota (RDMA) di accesso.</span><span class="sxs-lookup"><span data-stu-id="513b1-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="513b1-106">Questa interfaccia viene inoltre dimensioni di macchina virtuale disponibile tooother interfaccia toohello rete di Azure standard.</span><span class="sxs-lookup"><span data-stu-id="513b1-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="513b1-107">Questa interfaccia consente toocommunicate istanze che supportano RDMA hello in una rete InfiniBand, operando a tariffe FDR per le macchine virtuali H16r e H16mr e di tariffe QDR per le macchine virtuali A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="513b1-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="513b1-108">È possibile migliorare le funzionalità RDMA hello scalabilità e prestazioni delle applicazioni di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="513b1-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="513b1-109">Di seguito sono i requisiti per le macchine virtuali Windows con supporto per RDMA tooaccess hello rete RDMA di Azure:</span><span class="sxs-lookup"><span data-stu-id="513b1-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="513b1-110">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="513b1-110">**Operating system**</span></span>
  
  <span data-ttu-id="513b1-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="513b1-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="513b1-112">Windows Server 2016 non supporta attualmente la connettività RDMA in Azure.</span><span class="sxs-lookup"><span data-stu-id="513b1-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="513b1-113">**Impostare la disponibilità o un servizio cloud** : le macchine virtuali che supportano RDMA hello Distribuisci in hello stesso set (quando si utilizza il modello di distribuzione del hello Azure Resource Manager) di disponibilità o hello nello stesso servizio cloud (quando si utilizza il modello di distribuzione classica hello).</span><span class="sxs-lookup"><span data-stu-id="513b1-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="513b1-114">Se si utilizza Azure Batch, le macchine virtuali che supportano RDMA hello deve essere in hello stesso pool.</span><span class="sxs-lookup"><span data-stu-id="513b1-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="513b1-115">**MPI** : Microsoft MPI (MS-MPI) 2012 R2 o versione successiva, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="513b1-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="513b1-116">Implementazioni MPI supportate utilizzano hello toocommunicate di interfaccia Microsoft Network Direct tra istanze.</span><span class="sxs-lookup"><span data-stu-id="513b1-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="513b1-117">**Spazio degli indirizzi di rete RDMA** -rete RDMA hello in Azure riserva hello indirizzo spazio 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="513b1-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="513b1-118">toorun di applicazioni MPI in istanze distribuite in una rete virtuale di Azure, assicurarsi che spazio degli indirizzi di rete virtuale hello non si sovrapponga rete RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="513b1-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="513b1-119">**Estensione HpcVmDrivers VM** -nelle macchine virtuali che supportano RDMA, è necessario aggiungere hello HpcVmDrivers estensione tooinstall rete driver di dispositivo Windows per la connettività RDMA.</span><span class="sxs-lookup"><span data-stu-id="513b1-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="513b1-120">(In alcune distribuzioni di istanze A8 e A9, hello estensione HpcVmDrivers viene aggiunto automaticamente.) tooadd hello VM estensione tooa VM, è possibile utilizzare [Azure PowerShell](/powershell/azure/overview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="513b1-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="513b1-121">Hello comando Installa hello estensione HpcVMDrivers di versione 1.1 più recente in una macchina virtuale che supportano RDMA esistente denominata seguente *myVM* distribuito nel gruppo di risorse hello denominato *myResourceGroup* in hello  *Stati Uniti occidentali* area:</span><span class="sxs-lookup"><span data-stu-id="513b1-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="513b1-122">Per altre informazioni, vedere [Estensioni e funzionalità della macchina virtuale](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="513b1-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="513b1-123">È anche possibile operare con le estensioni per le macchine virtuali distribuite in hello [modello di distribuzione classica](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="513b1-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="513b1-124">Utilizzo di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="513b1-124">Using HPC Pack</span></span>

<span data-ttu-id="513b1-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, è una delle opzioni per si toocreate un cluster di calcolo in applicazioni MPI basati su Windows Azure toorun e altri carichi di lavoro HPC.</span><span class="sxs-lookup"><span data-stu-id="513b1-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="513b1-126">HPC Pack 2012 R2 e versioni successive includono un ambiente di runtime per MS-MPI che utilizza hello rete RDMA di Azure quando distribuito in macchine virtuali che supportano RDMA.</span><span class="sxs-lookup"><span data-stu-id="513b1-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="513b1-127">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="513b1-127">Other sizes</span></span>
- [<span data-ttu-id="513b1-128">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="513b1-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="513b1-129">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="513b1-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="513b1-130">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="513b1-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="513b1-131">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="513b1-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="513b1-132">Ottimizzate per la GPU</span><span class="sxs-lookup"><span data-stu-id="513b1-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="513b1-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="513b1-133">Next steps</span></span>

- <span data-ttu-id="513b1-134">Per elenchi di controllo toouse hello complesse le istanze con HPC Pack in Windows Server, vedere [configurazione di un cluster di Windows RDMA con applicazioni MPI di HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="513b1-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="513b1-135">le istanze con utilizzo intensivo di calcolo di toouse durante l'esecuzione di applicazioni MPI con Azure Batch, vedere [multi-istanza usare attività toorun applicazioni di interfaccia MPI (Message Passing) in Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="513b1-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="513b1-136">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="513b1-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




