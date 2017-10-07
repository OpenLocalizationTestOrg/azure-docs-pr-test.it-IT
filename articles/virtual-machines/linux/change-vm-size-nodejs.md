---
title: aaaHow tooresize una VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Scala verso il basso di una macchina virtuale Linux, modificando o tooscale backup hello come dimensione della macchina virtuale.
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
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="aadc5-103">Ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="aadc5-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="aadc5-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="aadc5-104">Overview</span></span>

<span data-ttu-id="aadc5-105">Dopo avere stabilito una macchina virtuale (VM), è possibile applicare la scalabilità hello VM verso l'alto o verso il basso modificando hello [dimensioni delle macchine Virtuali][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="aadc5-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="aadc5-106">In alcuni casi, è necessario deallocare prima hello VM.</span><span class="sxs-lookup"><span data-stu-id="aadc5-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="aadc5-107">Questa situazione può verificarsi se hello nuova dimensione non è disponibile nel cluster hardware hello che ospita hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aadc5-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="aadc5-108">Questo articolo viene illustrato come tooresize una VM Linux utilizzando hello [CLI di Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="aadc5-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="aadc5-109">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="aadc5-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="aadc5-110">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="aadc5-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="aadc5-111">[Azure CLI 1.0](#resize-a-linux-vm) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="aadc5-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="aadc5-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="aadc5-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="aadc5-113">Ridimensionare una VM di Linux</span><span class="sxs-lookup"><span data-stu-id="aadc5-113">Resize a Linux VM</span></span>
<span data-ttu-id="aadc5-114">tooresize una macchina virtuale, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="aadc5-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="aadc5-115">Eseguire il comando CLI seguente hello.</span><span class="sxs-lookup"><span data-stu-id="aadc5-115">Run hello following CLI command.</span></span> <span data-ttu-id="aadc5-116">Questo comando Elenca le dimensioni VM hello che sono disponibili nel cluster hardware hello hello VM ospita.</span><span class="sxs-lookup"><span data-stu-id="aadc5-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="aadc5-117">Se lo si desidera hello dimensioni sono elencata, eseguire hello successivo comando tooresize hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aadc5-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="aadc5-118">Hello VM verrà riavviato durante questo processo.</span><span class="sxs-lookup"><span data-stu-id="aadc5-118">hello VM will restart during this process.</span></span> <span data-ttu-id="aadc5-119">Dopo il riavvio di hello, il sistema operativo esistente e i dischi di dati verranno reimpostati.</span><span class="sxs-lookup"><span data-stu-id="aadc5-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="aadc5-120">Qualsiasi elemento sul disco temporaneo hello andranno persa.</span><span class="sxs-lookup"><span data-stu-id="aadc5-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="aadc5-121">Hello utilizzare `--enable-boot-diagnostics` opzione Abilita [diagnostica di avvio][boot-diagnostics], toolog qualsiasi toostartup correlati a errori.</span><span class="sxs-lookup"><span data-stu-id="aadc5-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="aadc5-122">In caso contrario, se lo si desidera hello dimensioni non sono elencata, eseguire hello seguenti comandi toodeallocate hello VM, ridimensionarlo e quindi riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aadc5-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="aadc5-123">Deallocazione di hello VM rilascia anche indirizzi IP dinamici assegnati toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aadc5-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="aadc5-124">Hello del sistema operativo e i dischi di dati non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="aadc5-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="aadc5-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aadc5-125">Next steps</span></span>
<span data-ttu-id="aadc5-126">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set].</span><span class="sxs-lookup"><span data-stu-id="aadc5-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
