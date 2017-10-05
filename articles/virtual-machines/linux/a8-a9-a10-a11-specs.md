---
title: Informazioni sulle macchine virtuali a elevato uso di calcolo con Linux | Microsoft Docs
description: Informazioni generali e considerazioni sull'uso delle dimensioni serie H e A8, A9, A10 e A11 a elevato utilizzo di calcolo per macchine virtuali Linux
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a2307f7055966ec7146b5da0b4daf1ad469abe2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="6a33b-103">Informazioni sulle macchine virtuali serie H e serie A a elevato utilizzo di calcolo per Linux</span><span class="sxs-lookup"><span data-stu-id="6a33b-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="6a33b-104">Informazioni generali e considerazioni sull'uso delle nuove dimensioni di Azure serie H e delle precedenti dimensioni A8, A9, A10 e A11, note anche come istanze *a elevato utilizzo di calcolo* .</span><span class="sxs-lookup"><span data-stu-id="6a33b-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="6a33b-105">Questo articolo illustra l'uso di queste dimensioni per macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="6a33b-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="6a33b-106">È possibile usarle anche per [macchine virtuali di Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="6a33b-107">Per conoscere le specifiche di base, le capacità di archiviazione e i dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="6a33b-108">Accesso alla rete RDMA</span><span class="sxs-lookup"><span data-stu-id="6a33b-108">Access to the RDMA network</span></span>
<span data-ttu-id="6a33b-109">È possibile creare cluster di macchine virtuali Linux con supporto per RDMA che eseguono una delle distribuzioni HPC Linux riportate di seguito e un'implementazione MPI supportata per sfruttare i vantaggi di una rete RDMA di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a33b-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="6a33b-110">Per le opzioni di distribuzione e la procedura di configurazione di esempio, vedere [Configurare un cluster Linux RDMA per eseguire applicazioni MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="6a33b-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="6a33b-111">**Distribuzioni**: è necessario distribuire le macchine virtuali da immagini SLES (SUSE Linux Enterprise Server) con supporto per RDMA o da immagini Rogue Wave Software (in precedenza OpenLogic) basate su CentOS in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6a33b-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="6a33b-112">Le immagini Marketplace seguenti supportano la connettività RDMA:</span><span class="sxs-lookup"><span data-stu-id="6a33b-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="6a33b-113">SLES 12 SP1 per HPC, SLES 12 SP1 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="6a33b-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="6a33b-114">HPC 7.1 basata su CentOS, HPC 6.5 basata su CentOS</span><span class="sxs-lookup"><span data-stu-id="6a33b-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="6a33b-115">Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="6a33b-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="6a33b-116">Nelle immagini HPC basate su CentOS gli aggiornamenti del kernel sono disabilitati nel file di configurazione **yum** .</span><span class="sxs-lookup"><span data-stu-id="6a33b-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="6a33b-117">In questo modo i driver Linux RDMA vengono distribuiti come pacchetto RPM e gli aggiornamenti dei driver potrebbero non funzionare se il kernel viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6a33b-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="6a33b-118">**MPI** : Intel MPI Library 5.x.</span><span class="sxs-lookup"><span data-stu-id="6a33b-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="6a33b-119">A seconda dell'immagine Marketplace scelta, può essere necessario separare licenze, installazione o configurazione di Intel MPI, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6a33b-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="6a33b-120">**Immagine SLES 12 SP1 per HPC** - I pacchetti Intel MPI vengono distribuiti nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6a33b-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="6a33b-121">Eseguire l'installazione con questo comando:</span><span class="sxs-lookup"><span data-stu-id="6a33b-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="6a33b-122">**Immagini HPC basate su CentOS** : Intel MPI 5.1 è già installato.</span><span class="sxs-lookup"><span data-stu-id="6a33b-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="6a33b-123">Per eseguire processi MPI su macchine virtuali n cluster, è necessaria una configurazione di sistema aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="6a33b-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="6a33b-124">In un cluster di macchine virtuali, ad esempio, è necessario stabilire una relazione di trust tra i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6a33b-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="6a33b-125">Per le impostazioni tipiche, vedere [Configurazione di un cluster Linux RDMA per eseguire applicazioni MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="6a33b-126">Considerazioni per HPC Pack e Linux</span><span class="sxs-lookup"><span data-stu-id="6a33b-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="6a33b-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), la soluzione Microsoft gratuita per la gestione di cluster e processi, fornisce un'opzione per l'uso di istanze a elevato utilizzo di calcolo con Linux.</span><span class="sxs-lookup"><span data-stu-id="6a33b-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="6a33b-128">La versione più recente di HPC Pack supporta varie distribuzioni Linux per l'esecuzione su nodi di calcolo distribuiti in VM di Azure, gestite da un nodo head di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6a33b-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="6a33b-129">Grazie ai nodi di calcolo Linux con supporto per RDMA che eseguono Intel MPI, HPC Pack può pianificare ed eseguire applicazioni Linux MPI che hanno accesso alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="6a33b-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="6a33b-130">Per iniziare, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="6a33b-131">Considerazioni sulla topologia di rete</span><span class="sxs-lookup"><span data-stu-id="6a33b-131">Network topology considerations</span></span>
* <span data-ttu-id="6a33b-132">Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="6a33b-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="6a33b-133">Non modificare le impostazioni di Eth1 o le informazioni nel file di configurazione riferite a questa rete.</span><span class="sxs-lookup"><span data-stu-id="6a33b-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="6a33b-134">Eth0 è riservato per il normale traffico di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a33b-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="6a33b-135">In Azure, IP over InfiniBand (IB) non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6a33b-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="6a33b-136">Solo RDMA over IB è supportato.</span><span class="sxs-lookup"><span data-stu-id="6a33b-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6a33b-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a33b-137">Next steps</span></span>
* <span data-ttu-id="6a33b-138">Per informazioni dettagliate sulla disponibilità e i prezzi delle dimensioni a elevato utilizzo di calcolo, vedere [Macchine virtuali - Prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="6a33b-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="6a33b-139">Per informazioni sulle funzionalità di archiviazione e dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="6a33b-140">Per iniziare a distribuire e usare dimensioni a elevato uso di calcolo con RDMA in Linux, vedere [Configurare un cluster Linux RDMA per eseguire applicazioni MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a33b-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

