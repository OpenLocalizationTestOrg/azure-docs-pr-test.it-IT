---
title: dimensioni aaaAzure VM Linux - HPC | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibile per Linux elaborazione a elevate prestazioni macchine virtuali in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="65486-103">Dimensioni delle macchine virtuali High Performance Computing (HPC) Linux</span><span class="sxs-lookup"><span data-stu-id="65486-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="65486-104">Istanze con supporto per RDMA</span><span class="sxs-lookup"><span data-stu-id="65486-104">RDMA-capable instances</span></span>
<span data-ttu-id="65486-105">Un subset delle istanze con utilizzo intensivo di calcolo di hello (H16r, H16mr, A8 e A9) funzionalità di un'interfaccia di rete per la connettività diretto a memoria remota (RDMA) di accesso.</span><span class="sxs-lookup"><span data-stu-id="65486-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="65486-106">Questa interfaccia viene inoltre dimensioni di macchina virtuale disponibile tooother interfaccia toohello rete di Azure standard.</span><span class="sxs-lookup"><span data-stu-id="65486-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="65486-107">Questa interfaccia consente toocommunicate istanze che supportano RDMA hello in una rete InfiniBand, operando a tariffe FDR per le macchine virtuali H16r e H16mr e di tariffe QDR per le macchine virtuali A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="65486-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="65486-108">È possibile migliorare le funzionalità RDMA hello scalabilità e prestazioni delle applicazioni di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="65486-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="65486-109">Di seguito sono i requisiti per le macchine virtuali Linux che supportano RDMA tooaccess hello rete RDMA di Azure:</span><span class="sxs-lookup"><span data-stu-id="65486-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="65486-110">**Distribuzioni** : È necessario distribuire le macchine virtuali dal supporto per RDMA SUSE Linux Enterprise Server (SLES) o immagini Software Wave non autorizzato (in precedenza OpenLogic) basato su CentOS HPC in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="65486-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="65486-111">Hello immagini Marketplace seguenti supportano la connettività RDMA:</span><span class="sxs-lookup"><span data-stu-id="65486-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="65486-112">SLES 12 SP1 per HPC o SLES 12 SP1 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="65486-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="65486-113">HPC basata su CentOS 7.3, HPC basata su CentOS 7.1, HPC basata su CentOS 6.8 o HPC basata su CentOS 6.5</span><span class="sxs-lookup"><span data-stu-id="65486-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="65486-114">Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="65486-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="65486-115">Le immagini basate su CentOS HPC hello, gli aggiornamenti kernel sono disabilitati in hello **yum** file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="65486-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="65486-116">In questo modo hello driver Linux RDMA vengono distribuiti come un pacchetto RPM e gli aggiornamenti dei driver potrebbero non funzionare se kernel hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="65486-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="65486-117">**MPI** : Intel MPI Library 5.x.</span><span class="sxs-lookup"><span data-stu-id="65486-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="65486-118">A seconda di un'immagine del Marketplace hello prescelto, installazione di gestione delle licenze, separata, o configurazione di Intel MPI potrebbe essere necessarie, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="65486-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="65486-119">**SLES 12 SP1 per l'immagine HPC** -Intel MPI pacchetti vengono distribuiti in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="65486-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="65486-120">Installare eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65486-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="65486-121">**Immagini HPC basate su CentOS** : Intel MPI 5.1 è già installato.</span><span class="sxs-lookup"><span data-stu-id="65486-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="65486-122">Configurazione di sistema aggiuntive non necessari toorun di processi MPI nel cluster macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65486-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="65486-123">Ad esempio, in un cluster di macchine virtuali, è necessario tooestablish trust tra hello nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="65486-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="65486-124">Per alcune impostazioni tipiche, vedere [impostare una di applicazioni MPI cluster toorun Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="65486-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="65486-125">Considerazioni sulla topologia di rete</span><span class="sxs-lookup"><span data-stu-id="65486-125">Network topology considerations</span></span>
* <span data-ttu-id="65486-126">Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="65486-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="65486-127">Non modificare le impostazioni della scheda Eth1 o tutte le informazioni nel file di configurazione hello che fa riferimento a rete toothis.</span><span class="sxs-lookup"><span data-stu-id="65486-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="65486-128">Eth0 è riservato per il normale traffico di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="65486-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="65486-129">In Azure, IP over InfiniBand (IB) non è supportato.</span><span class="sxs-lookup"><span data-stu-id="65486-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="65486-130">Solo RDMA over IB è supportato.</span><span class="sxs-lookup"><span data-stu-id="65486-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="65486-131">Utilizzo di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="65486-131">Using HPC Pack</span></span>
<span data-ttu-id="65486-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, è un'opzione per consentire le istanze con utilizzo intensivo di calcolo di hello toouse con Linux.</span><span class="sxs-lookup"><span data-stu-id="65486-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="65486-133">versioni più recenti di Hello di HPC Pack supportano diverse distribuzioni di Linux toorun nel calcolo nodi distribuiti nelle macchine virtuali di Azure, gestito da un nodo head di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="65486-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="65486-134">Con nodi di calcolo di Linux che supportano RDMA in esecuzione Intel MPI, HPC Pack può pianificare ed eseguire applicazioni MPI Linux rete con RDMA hello tale accesso.</span><span class="sxs-lookup"><span data-stu-id="65486-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="65486-135">Vedere l'articolo di [introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65486-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="65486-136">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="65486-136">Other sizes</span></span>
- [<span data-ttu-id="65486-137">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="65486-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="65486-138">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="65486-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="65486-139">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="65486-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="65486-140">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="65486-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="65486-141">GPU</span><span class="sxs-lookup"><span data-stu-id="65486-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="65486-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65486-142">Next steps</span></span>

- <span data-ttu-id="65486-143">tooget avviata la distribuzione e l'utilizzo di dimensioni elevate con RDMA su Linux, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65486-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="65486-144">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="65486-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




