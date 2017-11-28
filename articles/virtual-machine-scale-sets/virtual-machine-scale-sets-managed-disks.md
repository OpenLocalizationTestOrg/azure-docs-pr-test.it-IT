---
title: aaaUsing gestiti dischi con Azure scala set di macchine virtuali | Documenti Microsoft
description: "Informazioni su come e perché toouse gestiti dischi con il set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="cadd1-103">Set di scalabilità VM di Azure e dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="cadd1-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="cadd1-104">I [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) di Azure supportano macchine virtuali con dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="cadd1-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="cadd1-105">L'uso di dischi gestiti con i set di scalabilità presenta diversi vantaggi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="cadd1-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="cadd1-106">Non è più necessario toopre-creare e gestire i dischi di archiviazione account toostore hello del sistema operativo per le macchine virtuali del set di scalabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="cadd1-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="cadd1-107">È possibile collegare i set di scalabilità toohello dischi di dati gestiti.</span><span class="sxs-lookup"><span data-stu-id="cadd1-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="cadd1-108">Grazie al disco gestito, un set di scalabilità può contenere fino a un massimo di 1.000 macchine virtuali se basato su un'immagine di piattaforma o di 100 macchine virtuali se basato su un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="cadd1-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="cadd1-109">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="cadd1-109">Get started</span></span>

<span data-ttu-id="cadd1-110">Un modo semplice tooget avviato con il set di scalabilità di un disco gestito è toodeploy da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cadd1-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="cadd1-111">Per altre informazioni, vedere [questo articolo](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="cadd1-112">Un altro modo semplice tooget avviato è toouse [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy una scala impostata.</span><span class="sxs-lookup"><span data-stu-id="cadd1-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="cadd1-113">Hello seguente illustra un Ubuntu toocreate basati su set di scalabilità con 10 macchine virtuali, ognuno con un disco da 50 GB e 100 GB di dati:</span><span class="sxs-lookup"><span data-stu-id="cadd1-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="cadd1-114">In alternativa, è possibile cercare in hello [repository GitHub modelli Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) per le cartelle che contengono `vmss` toosee predefinite esempi di modelli di distribuire i set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cadd1-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="cadd1-115">tootell i modelli sono già in uso dischi gestiti, è possibile fare riferimento troppo[questo elenco](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cadd1-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cadd1-116">Next steps</span></span>

<span data-ttu-id="cadd1-117">Per altre informazioni sui dischi gestiti in generale, vedere [questo articolo](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="cadd1-118">toosee su una scala di gestione risorse modello tooprovision imposta con tooconvert gestiti dischi, vedere [questo articolo](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="cadd1-119">Hello stessi modelli di gestione risorse toohello modifiche si applicano toohello API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="cadd1-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="cadd1-120">toolearn ulteriori informazioni sull'utilizzo di dischi di dati gestiti con il set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="cadd1-121">toobegin lavora con set su larga scala, fare riferimento troppo[questo articolo](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="cadd1-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


