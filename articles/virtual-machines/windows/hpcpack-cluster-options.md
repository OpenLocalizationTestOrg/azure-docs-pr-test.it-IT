---
title: opzioni nel cloud hello del cluster HPC Pack aaaWindows | Documenti Microsoft
description: Informazioni sulle opzioni con Microsoft HPC Pack toocreate e gestire un Windows elaborazione a elevate prestazioni cluster (HPC) in hello cloud di Azure
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="38737-103">Opzioni con HPC Pack toocreate e gestire un cluster Windows HPC in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="38737-104">Questo articolo illustra le opzioni toocreate HPC Pack carichi di lavoro Windows toorun cluster.</span><span class="sxs-lookup"><span data-stu-id="38737-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="38737-105">Sono inoltre disponibili opzioni per la creazione di HPC Pack cluster toorun [carichi di lavoro HPC Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38737-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="38737-106">Eseguire un cluster HPC Pack nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="38737-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="38737-107">Modelli di Azure</span><span class="sxs-lookup"><span data-stu-id="38737-107">Azure templates</span></span>
* <span data-ttu-id="38737-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Modelli di cluster HPC Pack 2016)</span><span class="sxs-lookup"><span data-stu-id="38737-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="38737-109">(Marketplace) [Cluster HPC Pack per carichi di lavoro di Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="38737-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="38737-110">(Marketplace) [Cluster HPC Pack per carichi di lavoro di Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="38737-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="38737-111">(Guida introduttiva) [Creare un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="38737-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="38737-112">(Guida introduttiva) [Creare un cluster HPC con un'immagine di nodo di calcolo personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="38737-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="38737-113">Immagini di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="38737-113">Azure VM images</span></span>
* [<span data-ttu-id="38737-114">Nodo head HPC Pack 2016 in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="38737-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="38737-115">Nodo di calcolo HPC Pack 2016 in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="38737-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="38737-116">Nodo head HPC Pack 2016 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38737-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="38737-117">Nodo di calcolo HPC Pack 2016 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38737-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="38737-118">Nodo head HPC Pack 2012 R2 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38737-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="38737-119">Nodo di calcolo HPC Pack 2012 R2 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38737-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="38737-120">Nodo di calcolo HPC Pack con Excel su Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38737-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="38737-121">Script di distribuzione di PowerShell</span><span class="sxs-lookup"><span data-stu-id="38737-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="38737-122">Creare un cluster HPC con hello script di distribuzione IaaS di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="38737-123">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="38737-123">Tutorials</span></span>
* [<span data-ttu-id="38737-124">Esercitazione: Distribuire un cluster HPC Pack 2016 in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="38737-125">Esercitazione: Introduzione a un cluster HPC Pack in Azure toorun Excel e i carichi di lavoro SOA</span><span class="sxs-lookup"><span data-stu-id="38737-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="38737-126">Distribuzione manuale con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="38737-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="38737-127">Configurare hello nodo head di un cluster HPC Pack in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="38737-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="38737-128">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="38737-128">Cluster management</span></span>
* [<span data-ttu-id="38737-129">Gestire i nodi di calcolo in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="38737-130">Aumentare e ridurre le risorse di calcolo di Azure in un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="38737-131">Inviare i cluster di HPC Pack tooan processi in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="38737-132">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="38737-133">Gestire un cluster HPC Pack in Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38737-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="38737-134">Aggiungere il cluster HPC Pack tooan di lavoro ruolo nodi</span><span class="sxs-lookup"><span data-stu-id="38737-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="38737-135">Potenziamento tooAzure istanze di lavoro con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="38737-136">Esercitazione: Configurare un cluster ibrido con HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="38737-137">Aggiungere Azure "potenziamento" nodi tooan HPC Pack nodo head in Azure</span><span class="sxs-lookup"><span data-stu-id="38737-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="38737-138">Integrazione con Azure Batch</span><span class="sxs-lookup"><span data-stu-id="38737-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="38737-139">Potenziamento tooAzure Batch con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="38737-140">Creare cluster RDMA per carichi di lavoro MPI</span><span class="sxs-lookup"><span data-stu-id="38737-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="38737-141">Configurare un cluster di Windows RDMA con applicazioni MPI toorun di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="38737-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

