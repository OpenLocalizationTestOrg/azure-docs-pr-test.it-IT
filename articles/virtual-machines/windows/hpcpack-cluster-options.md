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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Opzioni con HPC Pack toocreate e gestire un cluster Windows HPC in Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Questo articolo illustra le opzioni toocreate HPC Pack carichi di lavoro Windows toorun cluster. Sono inoltre disponibili opzioni per la creazione di HPC Pack cluster toorun [carichi di lavoro HPC Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Eseguire un cluster HPC Pack nelle VM di Azure
### <a name="azure-templates"></a>Modelli di Azure
* (GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Modelli di cluster HPC Pack 2016)
* (Marketplace) [Cluster HPC Pack per carichi di lavoro di Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [Cluster HPC Pack per carichi di lavoro di Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Guida introduttiva) [Creare un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Guida introduttiva) [Creare un cluster HPC con un'immagine di nodo di calcolo personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Immagini di macchina virtuale di Azure
* [Nodo head HPC Pack 2016 in Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Nodo di calcolo HPC Pack 2016 in Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Nodo head HPC Pack 2016 in Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Nodo di calcolo HPC Pack 2016 in Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Nodo head HPC Pack 2012 R2 in Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Nodo di calcolo HPC Pack 2012 R2 in Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Nodo di calcolo HPC Pack con Excel su Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Script di distribuzione di PowerShell
* [Creare un cluster HPC con hello script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Esercitazioni
* [Esercitazione: Distribuire un cluster HPC Pack 2016 in Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Esercitazione: Introduzione a un cluster HPC Pack in Azure toorun Excel e i carichi di lavoro SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Distribuzione manuale con hello portale di Azure
* [Configurare hello nodo head di un cluster HPC Pack in una macchina virtuale di Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Gestione dei cluster
* [Gestire i nodi di calcolo in un cluster HPC Pack in Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Aumentare e ridurre le risorse di calcolo di Azure in un cluster HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Inviare i cluster di HPC Pack tooan processi in Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Job management in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)
* [Gestire un cluster HPC Pack in Azure con Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Aggiungere il cluster HPC Pack tooan di lavoro ruolo nodi
* [Potenziamento tooAzure istanze di lavoro con HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Esercitazione: Configurare un cluster ibrido con HPC Pack in Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Aggiungere Azure "potenziamento" nodi tooan HPC Pack nodo head in Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integrazione con Azure Batch
* [Potenziamento tooAzure Batch con HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Creare cluster RDMA per carichi di lavoro MPI
* [Configurare un cluster di Windows RDMA con applicazioni MPI toorun di HPC Pack](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

