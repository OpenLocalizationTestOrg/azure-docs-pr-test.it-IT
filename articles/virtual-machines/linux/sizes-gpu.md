---
title: Dimensioni delle macchine virtuali Linux in Azure -GPU | Microsoft Docs
description: Elenca le diverse dimensioni ottimizzate per GPU per le macchine virtuali Linux disponibili in Azure.
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
ms.openlocfilehash: 5c9bf89feba519147b07f2810fe4da882664e89e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="7d5af-103">Dimensioni delle macchine virtuali Linux GPU</span><span class="sxs-lookup"><span data-stu-id="7d5af-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="7d5af-104">Per le procedure di installazione e verifica dei driver, vedere [Installare i driver GPU NVIDIA in VM serie N che eseguono Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="7d5af-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="7d5af-105">Non è consigliabile installare X Server o altri sistemi che usano il driver nouveau in VM NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7d5af-105">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="7d5af-106">Prima di installare i driver NVIDIA GPU, è necessario disabilitare il driver nouveau.</span><span class="sxs-lookup"><span data-stu-id="7d5af-106">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="7d5af-107">Altre dimensioni</span><span class="sxs-lookup"><span data-stu-id="7d5af-107">Other sizes</span></span>
- [<span data-ttu-id="7d5af-108">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="7d5af-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="7d5af-109">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="7d5af-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="7d5af-110">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="7d5af-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="7d5af-111">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="7d5af-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="7d5af-112">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="7d5af-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="7d5af-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d5af-113">Next steps</span></span>
<span data-ttu-id="7d5af-114">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5af-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>