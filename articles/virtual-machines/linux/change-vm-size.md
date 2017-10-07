---
title: aaaHow tooresize una VM Linux con hello Azure CLI 2.0 | Documenti Microsoft
description: Scala verso il basso di una macchina virtuale Linux, modificando o tooscale backup hello come dimensione della macchina virtuale.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="8971c-103">Ridimensionare una macchina virtuale Linux con l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="8971c-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="8971c-104">Dopo avere stabilito una macchina virtuale (VM), è possibile applicare la scalabilità hello VM verso l'alto o verso il basso modificando hello [dimensioni delle macchine Virtuali][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="8971c-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="8971c-105">In alcuni casi, è necessario deallocare prima hello VM.</span><span class="sxs-lookup"><span data-stu-id="8971c-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="8971c-106">Se lo si desidera hello dimensione non è disponibile nel cluster hardware hello che ospita hello VM, è necessario toodeallocate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8971c-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="8971c-107">In questo articolo illustra in dettaglio come tooresize una VM Linux con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="8971c-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8971c-108">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8971c-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="8971c-109">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="8971c-109">Resize a VM</span></span>
<span data-ttu-id="8971c-110">tooresize una macchina virtuale, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8971c-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="8971c-111">Ridimensiona elenco hello di vista della macchina virtuale a disponibilità nel cluster hardware hello ospita hello VM con [az vm elenco-vm--opzioni di ridimensionamento](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="8971c-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="8971c-112">Hello esempio seguente vengono elencate le dimensioni delle macchine Virtuali per macchina virtuale denominata hello `myVM` nel gruppo di risorse hello `myResourceGroup` area:</span><span class="sxs-lookup"><span data-stu-id="8971c-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="8971c-113">Se lo si desidera hello dimensioni della macchina virtuale sono elencata, ridimensionare hello macchina virtuale con [az vm ridimensionare](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="8971c-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="8971c-114">Hello seguente esempio ridimensiona hello macchina virtuale denominata `myVM` toohello `Standard_DS3_v2` dimensioni:</span><span class="sxs-lookup"><span data-stu-id="8971c-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="8971c-115">Hello VM viene riavviato durante questo processo.</span><span class="sxs-lookup"><span data-stu-id="8971c-115">hello VM restarts during this process.</span></span> <span data-ttu-id="8971c-116">Dopo il riavvio di hello, il sistema operativo esistente e i dischi di dati vengono rimappati.</span><span class="sxs-lookup"><span data-stu-id="8971c-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="8971c-117">Qualsiasi elemento sul disco temporaneo hello viene persa.</span><span class="sxs-lookup"><span data-stu-id="8971c-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="8971c-118">Se lo si desidera hello dimensioni della macchina virtuale non sono elencata, è necessario toofirst deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="8971c-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="8971c-119">Questo processo consente hello VM toothen essere ridimensionato tooany dimensioni disponibili hello area supporta e quindi avviato.</span><span class="sxs-lookup"><span data-stu-id="8971c-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="8971c-120">Hello segue deallocare, ridimensionare e quindi avviare hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="8971c-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="8971c-121">Deallocazione di hello VM rilascia anche indirizzi IP dinamici assegnati toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8971c-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="8971c-122">Hello del sistema operativo e i dischi di dati non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="8971c-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8971c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8971c-123">Next steps</span></span>
<span data-ttu-id="8971c-124">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set].</span><span class="sxs-lookup"><span data-stu-id="8971c-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
