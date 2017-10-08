---
title: dimensioni aaaAzure VM Linux - GPU | Documenti Microsoft
description: Elenca hello GPU con ottimizzazione per la dimensioni disponibili diverse per le macchine virtuali Linux in Azure.
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
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="b8cd9-103">Dimensioni delle macchine virtuali Linux GPU</span><span class="sxs-lookup"><span data-stu-id="b8cd9-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="b8cd9-104">Per le procedure di installazione e verifica dei driver, vedere [Installare i driver GPU NVIDIA in VM serie N che eseguono Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b8cd9-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="b8cd9-105">Non è consigliabile l'installazione di server o altri sistemi che utilizzano il driver di nouveau hello in macchine virtuali NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b8cd9-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="b8cd9-106">Prima di installare i driver GPU NVIDIA, è necessario toodisable hello nouveau driver</span><span class="sxs-lookup"><span data-stu-id="b8cd9-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="b8cd9-107">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="b8cd9-107">Other sizes</span></span>
- [<span data-ttu-id="b8cd9-108">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="b8cd9-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="b8cd9-109">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="b8cd9-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="b8cd9-110">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="b8cd9-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="b8cd9-111">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="b8cd9-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="b8cd9-112">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="b8cd9-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="b8cd9-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8cd9-113">Next steps</span></span>
<span data-ttu-id="b8cd9-114">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cd9-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>