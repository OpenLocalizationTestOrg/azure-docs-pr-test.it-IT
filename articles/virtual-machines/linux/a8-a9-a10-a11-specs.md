---
title: aaaAbout complesse le macchine virtuali con Linux | Documenti Microsoft
description: Ottenere informazioni generali e considerazioni per l'utilizzo delle dimensioni di hello H serie e A8, A9, A10 e A11 complesse per le macchine virtuali Linux
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
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="cd434-103">Informazioni sulle macchine virtuali serie H e serie A a elevato utilizzo di calcolo per Linux</span><span class="sxs-lookup"><span data-stu-id="cd434-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="cd434-104">Ecco informazioni complementari e alcune considerazioni per l'utilizzo di hello serie H Azure più recente e hello precedenti dimensioni A8, A9, A10 e A11, noto anche come *complesse* istanze.</span><span class="sxs-lookup"><span data-stu-id="cd434-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="cd434-105">Questo articolo illustra l'uso di queste dimensioni per macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="cd434-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="cd434-106">È possibile usarle anche per [macchine virtuali di Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cd434-107">Per conoscere le specifiche di base, le capacità di archiviazione e i dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="cd434-108">Rete con RDMA toohello accesso</span><span class="sxs-lookup"><span data-stu-id="cd434-108">Access toohello RDMA network</span></span>
<span data-ttu-id="cd434-109">È possibile creare cluster di macchine virtuali di Linux che supportano RDMA che eseguono una delle seguenti distribuzioni Linux HPC supportate e un vantaggio di tootake implementazione MPI supportato di rete RDMA di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd434-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="cd434-110">Vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per passaggi di configurazione di esempio e le opzioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cd434-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="cd434-111">**Distribuzioni** : È necessario distribuire le macchine virtuali dal supporto per RDMA SUSE Linux Enterprise Server (SLES) o immagini Software Wave non autorizzato (in precedenza OpenLogic) basato su CentOS HPC in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cd434-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="cd434-112">Hello immagini Marketplace seguenti supportano la connettività RDMA:</span><span class="sxs-lookup"><span data-stu-id="cd434-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="cd434-113">SLES 12 SP1 per HPC, SLES 12 SP1 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="cd434-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="cd434-114">HPC 7.1 basata su CentOS, HPC 6.5 basata su CentOS</span><span class="sxs-lookup"><span data-stu-id="cd434-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="cd434-115">Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="cd434-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="cd434-116">Le immagini basate su CentOS HPC hello, gli aggiornamenti kernel sono disabilitati in hello **yum** file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cd434-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="cd434-117">In questo modo hello driver Linux RDMA vengono distribuiti come un pacchetto RPM e gli aggiornamenti dei driver potrebbero non funzionare se kernel hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="cd434-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="cd434-118">**MPI** : Intel MPI Library 5.x.</span><span class="sxs-lookup"><span data-stu-id="cd434-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="cd434-119">A seconda di un'immagine del Marketplace hello prescelto, installazione di gestione delle licenze, separata, o configurazione di Intel MPI potrebbe essere necessarie, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cd434-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="cd434-120">**SLES 12 SP1 per l'immagine HPC** -Intel MPI pacchetti vengono distribuiti in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cd434-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="cd434-121">Installare eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd434-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="cd434-122">**Immagini HPC basate su CentOS** : Intel MPI 5.1 è già installato.</span><span class="sxs-lookup"><span data-stu-id="cd434-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="cd434-123">Configurazione di sistema aggiuntive non necessari toorun di processi MPI nel cluster macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cd434-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="cd434-124">Ad esempio, in un cluster di macchine virtuali, è necessario tooestablish trust tra hello nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="cd434-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="cd434-125">Per alcune impostazioni tipiche, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="cd434-126">Considerazioni per HPC Pack e Linux</span><span class="sxs-lookup"><span data-stu-id="cd434-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="cd434-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, fornisce un'opzione per consentire le istanze con utilizzo intensivo di calcolo di hello toouse con Linux.</span><span class="sxs-lookup"><span data-stu-id="cd434-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="cd434-128">versioni più recenti di Hello di HPC Pack supportano diverse distribuzioni di Linux toorun nel calcolo nodi distribuiti nelle macchine virtuali di Azure, gestito da un nodo head di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cd434-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="cd434-129">Con nodi di calcolo di Linux che supportano RDMA in esecuzione Intel MPI, HPC Pack può pianificare ed eseguire applicazioni MPI Linux rete con RDMA hello tale accesso.</span><span class="sxs-lookup"><span data-stu-id="cd434-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="cd434-130">tooget introduzione, vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="cd434-131">Considerazioni sulla topologia di rete</span><span class="sxs-lookup"><span data-stu-id="cd434-131">Network topology considerations</span></span>
* <span data-ttu-id="cd434-132">Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="cd434-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="cd434-133">Non modificare le impostazioni della scheda Eth1 o tutte le informazioni nel file di configurazione hello che fa riferimento a rete toothis.</span><span class="sxs-lookup"><span data-stu-id="cd434-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="cd434-134">Eth0 è riservato per il normale traffico di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd434-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="cd434-135">In Azure, IP over InfiniBand (IB) non è supportato.</span><span class="sxs-lookup"><span data-stu-id="cd434-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="cd434-136">Solo RDMA over IB è supportato.</span><span class="sxs-lookup"><span data-stu-id="cd434-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cd434-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd434-137">Next steps</span></span>
* <span data-ttu-id="cd434-138">Per informazioni sulla disponibilità e prezzi di dimensioni elevate hello, vedere [prezzi-macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="cd434-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="cd434-139">Per informazioni sulle funzionalità di archiviazione e dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="cd434-140">tooget avviata la distribuzione e l'utilizzo di dimensioni elevate con RDMA su Linux, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd434-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

