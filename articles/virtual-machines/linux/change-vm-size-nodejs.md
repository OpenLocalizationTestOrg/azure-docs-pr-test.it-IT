---
title: Come ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Come ridimensionare una macchina virtuale di Linux, modificando le dimensioni della VM.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72f5a3cd6463befd5108040ed166984281bfc5f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="cf21f-103">Ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cf21f-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="cf21f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cf21f-104">Overview</span></span>

<span data-ttu-id="cf21f-105">Dopo aver eseguito il provisioning di una macchina virtuale (VM), è possibile scalare la macchina virtuale in verticale o orizzontale modificando le [dimensioni della VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="cf21f-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="cf21f-106">In alcuni casi, è necessario prima deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cf21f-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="cf21f-107">Questa situazione può verificarsi se le nuove dimensioni non sono disponibili nel cluster hardware che ospita la VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="cf21f-108">Questo articolo illustra come ridimensionare una VM Linux mediante l'[interfaccia della riga di comando di Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="cf21f-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cf21f-109">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="cf21f-109">CLI versions to complete the task</span></span>
<span data-ttu-id="cf21f-110">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="cf21f-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="cf21f-111">[Interfaccia della riga di comando di Azure 1.0](#resize-a-linux-vm): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="cf21f-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cf21f-112">[Interfaccia della riga di comando di Azure 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="cf21f-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="cf21f-113">Ridimensionare una VM di Linux</span><span class="sxs-lookup"><span data-stu-id="cf21f-113">Resize a Linux VM</span></span>
<span data-ttu-id="cf21f-114">Per ridimensionare una VM, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="cf21f-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="cf21f-115">Eseguire il comando dell'interfaccia della riga di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cf21f-115">Run the following CLI command.</span></span> <span data-ttu-id="cf21f-116">Questo comando elenca le dimensioni delle VM che sono disponibili nel cluster hardware in cui è ospitata la VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="cf21f-117">Se le dimensioni desiderate sono nell'elenco, eseguire il comando seguente per ridimensionare la VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="cf21f-118">Durante questo processo verrà riavviata la VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-118">The VM will restart during this process.</span></span> <span data-ttu-id="cf21f-119">Dopo il riavvio, si rimappano il sistema operativo esistente e i dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="cf21f-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="cf21f-120">Qualsiasi elemento presente nel disco temporaneo andrà perso.</span><span class="sxs-lookup"><span data-stu-id="cf21f-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="cf21f-121">L'uso dell'opzione `--enable-boot-diagnostics` consente alla [diagnostica di avvio][boot-diagnostics] di registrare eventuali errori correlati all'avvio.</span><span class="sxs-lookup"><span data-stu-id="cf21f-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="cf21f-122">In caso contrario, se la dimensione desiderata non è nell'elenco, eseguire i comandi seguenti per deallocare la VM, ridimensionarla e quindi riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="cf21f-123">La deallocazione della VM rilascia anche degli indirizzi IP dinamici assegnati alla VM.</span><span class="sxs-lookup"><span data-stu-id="cf21f-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="cf21f-124">I dischi del sistema operativo e dei dati non sono coinvolti.</span><span class="sxs-lookup"><span data-stu-id="cf21f-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="cf21f-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf21f-125">Next steps</span></span>
<span data-ttu-id="cf21f-126">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="cf21f-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="cf21f-127">Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set].</span><span class="sxs-lookup"><span data-stu-id="cf21f-127">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
