---
title: "Uso dei dischi gestiti con i set di scalabilità delle macchine virtuali di Azure | Microsoft Docs"
description: "Informazioni su come e perché usare dischi gestiti con i set di scalabilità delle macchine virtuali"
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
ms.openlocfilehash: 3ab1d432a2f90db57b99f0e7d419d85e2958c308
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="c2587-103">Set di scalabilità VM di Azure e dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="c2587-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="c2587-104">I [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) di Azure supportano macchine virtuali con dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="c2587-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="c2587-105">L'uso di dischi gestiti con i set di scalabilità presenta diversi vantaggi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="c2587-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="c2587-106">Non è più necessario creare in anticipo e gestire gli account di archiviazione per archiviare i dischi del sistema operativo per i set di scalabilità delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c2587-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span></span>

* <span data-ttu-id="c2587-107">È possibile collegare dischi dati gestiti al set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c2587-107">You can attach managed data disks to the scale set.</span></span>

* <span data-ttu-id="c2587-108">Grazie al disco gestito, un set di scalabilità può contenere fino a un massimo di 1.000 macchine virtuali se basato su un'immagine di piattaforma o di 100 macchine virtuali se basato su un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c2587-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="c2587-109">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c2587-109">Get started</span></span>

<span data-ttu-id="c2587-110">Un modo semplice per iniziare a usare i set di scalabilità con i dischi gestiti consiste nel distribuirne uno dal Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2587-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span></span> <span data-ttu-id="c2587-111">Per altre informazioni, vedere [questo articolo](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="c2587-112">Un altro modo semplice per iniziare è usare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) per distribuire un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c2587-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span></span> <span data-ttu-id="c2587-113">Nell'esempio seguente viene illustrato come creare un set di scalabilità basato su Ubuntu con 10 macchine virtuali, ognuna con un disco dati da 50 e da 100 GB:</span><span class="sxs-lookup"><span data-stu-id="c2587-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="c2587-114">In alternativa, è possibile esaminare il [repository di Modelli di avvio rapido di Azure in GitHub](https://github.com/Azure/azure-quickstart-templates) e consultare le cartelle contenenti `vmss` per vedere esempi preesistenti di modelli di distribuzione di set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c2587-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="c2587-115">Per individuare quali modelli usano già i dischi gestiti, è possibile fare riferimento a [questo elenco](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2587-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2587-116">Next steps</span></span>

<span data-ttu-id="c2587-117">Per altre informazioni sui dischi gestiti in generale, vedere [questo articolo](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="c2587-118">Per informazioni su come convertire un modello di Resource Manager per eseguire il provisioning dei set di scalabilità con i dischi gestiti, consultare [questo articolo](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-118">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="c2587-119">Le stesse modifiche applicate ai modelli di Resource Manager si applicano anche all'API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2587-119">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span></span>

<span data-ttu-id="c2587-120">Per altre informazioni sull'uso dei dischi di dati gestiti con i set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-120">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="c2587-121">Per iniziare a usare i set di scalabilità di grandi dimensioni, fare riferimento a [questo articolo](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c2587-121">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


