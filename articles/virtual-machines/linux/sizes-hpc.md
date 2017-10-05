---
title: Dimensioni delle macchine virtuali Linux in Azure -HPC | Documentazione Microsoft
description: Elenca le diverse dimensioni disponibili per le macchine virtuali High Performance Computing Linux in Azure.
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
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="cc970-103">Dimensioni delle macchine virtuali High Performance Computing (HPC) Linux</span><span class="sxs-lookup"><span data-stu-id="cc970-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="cc970-104">Istanze con supporto per RDMA</span><span class="sxs-lookup"><span data-stu-id="cc970-104">RDMA-capable instances</span></span>
<span data-ttu-id="cc970-105">Un subset delle istanze a elevato uso di calcolo (H16r, H16mr, A8 e A9) è dotato di un'interfaccia di rete per la connettività ad accesso diretto a memoria remota (RDMA).</span><span class="sxs-lookup"><span data-stu-id="cc970-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="cc970-106">Questa interfaccia è un'aggiunta all'interfaccia di rete di Azure standard disponibile per gli altri formati di VM.</span><span class="sxs-lookup"><span data-stu-id="cc970-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="cc970-107">Questa interfaccia consente alle istanze con supporto per RDMA di comunicare attraverso una rete InfiniBand che funziona a velocità FDR per macchine virtuali H16r e H16mr e a velocità QDR per macchine virtuali A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="cc970-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="cc970-108">Queste funzionalità RDMA possono migliorare la scalabilità e le prestazioni delle applicazioni di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="cc970-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="cc970-109">Di seguito sono riportati i requisiti per le macchine virtuali Linux con supporto per RDMA per accedere alla rete RDMA di Azure:</span><span class="sxs-lookup"><span data-stu-id="cc970-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="cc970-110">**Distribuzioni**: è necessario distribuire le macchine virtuali da immagini SLES (SUSE Linux Enterprise Server) con supporto per RDMA o da immagini Rogue Wave Software (in precedenza OpenLogic) basate su CentOS in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cc970-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="cc970-111">Le immagini Marketplace seguenti supportano la connettività RDMA:</span><span class="sxs-lookup"><span data-stu-id="cc970-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="cc970-112">SLES 12 SP1 per HPC o SLES 12 SP1 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="cc970-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="cc970-113">HPC basata su CentOS 7.3, HPC basata su CentOS 7.1, HPC basata su CentOS 6.8 o HPC basata su CentOS 6.5</span><span class="sxs-lookup"><span data-stu-id="cc970-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="cc970-114">Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="cc970-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="cc970-115">Nelle immagini HPC basate su CentOS gli aggiornamenti del kernel sono disabilitati nel file di configurazione **yum** .</span><span class="sxs-lookup"><span data-stu-id="cc970-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="cc970-116">In questo modo i driver Linux RDMA vengono distribuiti come pacchetto RPM e gli aggiornamenti dei driver potrebbero non funzionare se il kernel viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="cc970-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="cc970-117">**MPI** : Intel MPI Library 5.x.</span><span class="sxs-lookup"><span data-stu-id="cc970-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="cc970-118">A seconda dell'immagine Marketplace scelta, può essere necessario separare licenze, installazione o configurazione di Intel MPI, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cc970-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="cc970-119">**Immagine SLES 12 SP1 per HPC** - I pacchetti Intel MPI vengono distribuiti nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cc970-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="cc970-120">Eseguire l'installazione con questo comando:</span><span class="sxs-lookup"><span data-stu-id="cc970-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="cc970-121">**Immagini HPC basate su CentOS** : Intel MPI 5.1 è già installato.</span><span class="sxs-lookup"><span data-stu-id="cc970-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="cc970-122">Per eseguire processi MPI su macchine virtuali n cluster, è necessaria una configurazione di sistema aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="cc970-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="cc970-123">In un cluster di macchine virtuali, ad esempio, è necessario stabilire una relazione di trust tra i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="cc970-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="cc970-124">Per le impostazioni tipiche, vedere [Configurazione di un cluster Linux RDMA per eseguire applicazioni MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc970-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="cc970-125">Considerazioni sulla topologia di rete</span><span class="sxs-lookup"><span data-stu-id="cc970-125">Network topology considerations</span></span>
* <span data-ttu-id="cc970-126">Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="cc970-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="cc970-127">Non modificare le impostazioni di Eth1 o le informazioni nel file di configurazione riferite a questa rete.</span><span class="sxs-lookup"><span data-stu-id="cc970-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="cc970-128">Eth0 è riservato per il normale traffico di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc970-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="cc970-129">In Azure, IP over InfiniBand (IB) non è supportato.</span><span class="sxs-lookup"><span data-stu-id="cc970-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="cc970-130">Solo RDMA over IB è supportato.</span><span class="sxs-lookup"><span data-stu-id="cc970-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="cc970-131">Utilizzo di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="cc970-131">Using HPC Pack</span></span>
<span data-ttu-id="cc970-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), la soluzione di gestione di processi e cluster HPC gratuita di Microsoft, è un'opzione per l'uso di istanze a elevato utilizzo di calcolo con Linux.</span><span class="sxs-lookup"><span data-stu-id="cc970-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="cc970-133">La versione più recente di HPC Pack supporta varie distribuzioni Linux per l'esecuzione su nodi di calcolo distribuiti in VM di Azure, gestite da un nodo head di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cc970-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="cc970-134">Grazie ai nodi di calcolo Linux con supporto per RDMA che eseguono Intel MPI, HPC Pack può pianificare ed eseguire applicazioni Linux MPI che hanno accesso alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="cc970-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="cc970-135">Vedere l'articolo di [introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc970-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="cc970-136">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="cc970-136">Other sizes</span></span>
- [<span data-ttu-id="cc970-137">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="cc970-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="cc970-138">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="cc970-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="cc970-139">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="cc970-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="cc970-140">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="cc970-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="cc970-141">GPU</span><span class="sxs-lookup"><span data-stu-id="cc970-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="cc970-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc970-142">Next steps</span></span>

- <span data-ttu-id="cc970-143">Per iniziare a distribuire e usare dimensioni a elevato uso di calcolo con RDMA in Linux, vedere [Configurare un cluster Linux RDMA per eseguire applicazioni MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc970-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="cc970-144">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc970-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




