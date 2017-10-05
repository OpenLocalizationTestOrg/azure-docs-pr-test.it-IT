---
title: Opzioni cluster HPC Pack Windows nel cloud | Microsoft Docs
description: Informazioni sulle opzioni con Microsoft HPC Pack per creare e gestire un cluster high performance computing (HPC) Windows nel cloud di Azure
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
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="0757c-103">Opzioni con HPC Pack per creare e gestire un cluster Windows HPC in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="0757c-104">Questo articolo descrive le opzioni per la creazione di cluster HPC Pack per eseguire carichi di lavoro di Windows.</span><span class="sxs-lookup"><span data-stu-id="0757c-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="0757c-105">Esistono anche opzioni per la creazione di cluster HPC Pack per eseguire [carichi di lavoro di Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0757c-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="0757c-106">Eseguire un cluster HPC Pack nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="0757c-107">Modelli di Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-107">Azure templates</span></span>
* <span data-ttu-id="0757c-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Modelli di cluster HPC Pack 2016)</span><span class="sxs-lookup"><span data-stu-id="0757c-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="0757c-109">(Marketplace) [Cluster HPC Pack per carichi di lavoro di Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="0757c-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="0757c-110">(Marketplace) [Cluster HPC Pack per carichi di lavoro di Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="0757c-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="0757c-111">(Guida introduttiva) [Creare un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="0757c-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="0757c-112">(Guida introduttiva) [Creare un cluster HPC con un'immagine di nodo di calcolo personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="0757c-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="0757c-113">Immagini di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-113">Azure VM images</span></span>
* [<span data-ttu-id="0757c-114">Nodo head HPC Pack 2016 in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0757c-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="0757c-115">Nodo di calcolo HPC Pack 2016 in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0757c-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="0757c-116">Nodo head HPC Pack 2016 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0757c-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="0757c-117">Nodo di calcolo HPC Pack 2016 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0757c-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="0757c-118">Nodo head HPC Pack 2012 R2 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0757c-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="0757c-119">Nodo di calcolo HPC Pack 2012 R2 in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0757c-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="0757c-120">Nodo di calcolo HPC Pack con Excel su Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0757c-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="0757c-121">Script di distribuzione di PowerShell</span><span class="sxs-lookup"><span data-stu-id="0757c-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="0757c-122">Creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="0757c-123">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="0757c-123">Tutorials</span></span>
* [<span data-ttu-id="0757c-124">Esercitazione: Distribuire un cluster HPC Pack 2016 in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0757c-125">Esercitazione: Introduzione all’uso di un cluster HPC Pack in Azure per l’esecuzione di carichi di lavoro di Excel e SOA</span><span class="sxs-lookup"><span data-stu-id="0757c-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="0757c-126">Distribuzione manuale nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="0757c-127">Configurare il nodo head di un cluster HPC Pack in una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="0757c-128">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="0757c-128">Cluster management</span></span>
* [<span data-ttu-id="0757c-129">Gestire i nodi di calcolo in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="0757c-130">Aumentare e ridurre le risorse di calcolo di Azure in un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="0757c-131">Inviare i processi a un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0757c-132">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="0757c-133">Gestire un cluster HPC Pack in Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0757c-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="0757c-134">Aggiungere nodi di ruolo di lavoro a un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="0757c-135">Potenziare le istanze del ruolo di lavoro di Azure con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="0757c-136">Esercitazione: Configurare un cluster ibrido con HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="0757c-137">Aggiungere nodi di "potenziamento" di Azure a un nodo head HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="0757c-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="0757c-138">Integrazione con Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0757c-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="0757c-139">Potenziare Azure Batch con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0757c-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="0757c-140">Creare cluster RDMA per carichi di lavoro MPI</span><span class="sxs-lookup"><span data-stu-id="0757c-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="0757c-141">Configurare un cluster RDMA di Windows con HPC Pack per eseguire applicazioni MPI</span><span class="sxs-lookup"><span data-stu-id="0757c-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

