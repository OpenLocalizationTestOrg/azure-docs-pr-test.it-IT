---
title: Come ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Come ridimensionare una macchina virtuale di Linux, modificando le dimensioni della VM.
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
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="b3038-103">Ridimensionare una macchina virtuale Linux con l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="b3038-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="b3038-104">Dopo aver eseguito il provisioning di una macchina virtuale (VM), è possibile scalare la macchina virtuale in verticale o orizzontale modificando le [dimensioni della VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="b3038-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="b3038-105">In alcuni casi, è necessario prima deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b3038-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="b3038-106">Se le dimensioni desiderate non sono disponibili nel cluster hardware che ospita la VM, è necessario deallocare la VM.</span><span class="sxs-lookup"><span data-stu-id="b3038-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="b3038-107">Questo articolo illustra come ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="b3038-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="b3038-108">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3038-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="b3038-109">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="b3038-109">Resize a VM</span></span>
<span data-ttu-id="b3038-110">Per ridimensionare la VM, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0 ](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b3038-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="b3038-111">Per consultare l'elenco delle dimensioni delle VM disponibili nel cluster hardware in cui è ospitata la macchina virtuale, usare il comando [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="b3038-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="b3038-112">L'esempio seguente elenca le dimensioni di macchina virtuale disponibili per la VM denominata `myVM` nell'area `myResourceGroup` del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="b3038-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="b3038-113">Se le dimensioni di VM desiderate sono presenti nell'elenco, ridimensionare la VM con il comando [az vm resize](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="b3038-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="b3038-114">Nell'esempio seguente viene ridimensionata la VM denominata `myVM` alle dimensioni `Standard_DS3_v2`:</span><span class="sxs-lookup"><span data-stu-id="b3038-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="b3038-115">Durante questo processo, la VM viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="b3038-115">The VM restarts during this process.</span></span> <span data-ttu-id="b3038-116">Dopo il riavvio, viene eseguito un nuovo mappaggio del sistema operativo esistente e dei dischi dati.</span><span class="sxs-lookup"><span data-stu-id="b3038-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="b3038-117">Qualsiasi elemento presente nel disco temporaneo andrà perso.</span><span class="sxs-lookup"><span data-stu-id="b3038-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="b3038-118">Se le dimensioni della VM desiderate non sono presenti nell'elenco, è necessario innanzitutto deallocare la macchina virtuale con il comando [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="b3038-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="b3038-119">Questo processo consente il ridimensionamento della macchina virtuale a qualsiasi dimensione disponibile supportata dall'area e l'avvio della stessa.</span><span class="sxs-lookup"><span data-stu-id="b3038-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="b3038-120">I passaggi seguenti consentono di deallocare, ridimensionare e quindi avviare la VM denominata `myVM` nel gruppo di risorse denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b3038-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="b3038-121">La deallocazione della VM rilascia anche degli indirizzi IP dinamici assegnati alla VM.</span><span class="sxs-lookup"><span data-stu-id="b3038-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="b3038-122">I dischi del sistema operativo e dei dati non sono coinvolti.</span><span class="sxs-lookup"><span data-stu-id="b3038-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3038-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3038-123">Next steps</span></span>
<span data-ttu-id="b3038-124">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="b3038-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="b3038-125">Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set].</span><span class="sxs-lookup"><span data-stu-id="b3038-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
