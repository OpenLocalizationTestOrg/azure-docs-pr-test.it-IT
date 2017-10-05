---
title: Opzioni cluster HPC Linux Pack nel cloud | Microsoft Docs
description: Informazioni sulle opzioni con Microsoft HPC Pack per creare e gestire un cluster HPC (High Performance Computing) Linux nel cloud di Azure
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 616006d29149f7f47b03bd127cf3c83ad63a5c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="a5335-103">Opzioni con pacchetto HPC per creare e gestire un cluster HPC in Azure per i carichi di lavoro di Linux</span><span class="sxs-lookup"><span data-stu-id="a5335-103">Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="a5335-104">In questo articolo sono trattate le opzioni per l'uso di HPC Pack per l'esecuzione di carichi di lavoro di Linux.</span><span class="sxs-lookup"><span data-stu-id="a5335-104">This article focuses on options to use HPC Pack to run Linux workloads.</span></span> <span data-ttu-id="a5335-105">Esistono anche opzioni per l'esecuzione di [carichi di lavoro di Windows HPC con HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5335-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="a5335-106">Eseguire un cluster HPC Pack nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="a5335-107">Modelli di Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-107">Azure templates</span></span>
* <span data-ttu-id="a5335-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Modelli di cluster HPC Pack 2016)</span><span class="sxs-lookup"><span data-stu-id="a5335-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="a5335-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="a5335-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="a5335-110">(Guida introduttiva) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="a5335-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="a5335-111">Script di distribuzione di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5335-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="a5335-112">Creare un cluster HPC Linux con lo script di distribuzione IaaS di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="a5335-112">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="a5335-113">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="a5335-113">Tutorials</span></span>
* [<span data-ttu-id="a5335-114">Esercitazione: introduzione all’uso di nodi di calcolo Linux in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="a5335-115">Esercitazione: eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="a5335-116">Esercitazione: eseguire OpenFOAM con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="a5335-117">Esercitazione: eseguire STAR-CCM+ con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="a5335-118">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="a5335-118">Cluster management</span></span>
* [<span data-ttu-id="a5335-119">Inviare i processi a un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-119">Submit jobs to an HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="a5335-120">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="a5335-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="a5335-121">Creare cluster RDMA per carichi di lavoro MPI</span><span class="sxs-lookup"><span data-stu-id="a5335-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="a5335-122">Esercitazione: eseguire OpenFOAM con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="a5335-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="a5335-123">Configurazione di un cluster Linux RDMA per eseguire applicazioni MPI</span><span class="sxs-lookup"><span data-stu-id="a5335-123">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

