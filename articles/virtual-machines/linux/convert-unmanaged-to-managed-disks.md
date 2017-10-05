---
title: Convertire una macchina virtuale Linux in Azure da dischi non gestiti a dischi gestiti - Azure Managed Disks | Microsoft Docs
description: Come convertire una macchina virtuale Linux da dischi non gestiti a dischi gestiti usando l'interfaccia della riga di comando di Azure 2.0 nel modello di distribuzione Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="7e0a4-103">Convertire una macchina virtuale Linux da dischi non gestiti a dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="7e0a4-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="7e0a4-104">Se sono presenti macchine virtuali Linux che usano dischi non gestiti, è possibile convertire le macchine virtuali in modo che usino dischi gestiti mediante il servizio [Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="7e0a4-105">Questo processo consente di convertire sia il disco del sistema operativo che eventuali dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="7e0a4-106">Questo articolo illustra come convertire le macchine virtuali usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="7e0a4-107">Se è necessario installarla o aggiornarla, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="7e0a4-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7e0a4-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="7e0a4-109">Convertire VM a istanza singola</span><span class="sxs-lookup"><span data-stu-id="7e0a4-109">Convert single-instance VMs</span></span>
<span data-ttu-id="7e0a4-110">Questa sezione descrive come convertire i dischi delle macchine virtuali di Azure a istanza singola da non gestiti a gestiti.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="7e0a4-111">Se le macchine virtuali si trovano in un set di disponibilità, vedere la sezione successiva. È possibile usare questo processo per convertire le macchine virtuali da dischi non gestiti Premium (SDD) a dischi gestiti Premium o da dischi non gestiti standard (HDD) a dischi gestiti standard.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="7e0a4-112">Deallocare la macchina virtuale con il comando [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="7e0a4-113">L'esempio seguente dealloca la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="7e0a4-114">Convertire la macchina virtuale per l'utilizzo di dischi gestiti con il comando [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="7e0a4-115">Il processo seguente converte la macchina virtuale denominata `myVM`, incluso il disco del sistema operativo ed eventuali dischi dati:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="7e0a4-116">Avviare la macchina virtuale dopo la conversione in dischi gestiti con il comando [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="7e0a4-117">L'esempio seguente avvia la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="7e0a4-118">Convertire VM in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="7e0a4-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="7e0a4-119">Se le macchine virtuali che si desidera convertire in dischi gestiti si trovano in un set di disponibilità, è innanzitutto necessario convertire il set di disponibilità in un set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="7e0a4-120">Tutte le macchine virtuali nel set di disponibilità devono essere deallocate prima di convertire il set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="7e0a4-121">Pianificare la conversione di tutte le macchine virtuali per l'utilizzo di dischi gestiti dopo la conversione del set di disponibilità stesso in un set gestito.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="7e0a4-122">Avviare quindi tutte le macchine virtuali e continuare a usarle normalmente.</span><span class="sxs-lookup"><span data-stu-id="7e0a4-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="7e0a4-123">Elencare tutte le macchine virtuali in un set di disponibilità con il comando [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="7e0a4-124">L'esempio seguente elenca tutte le macchine virtuali nel set di disponibilità denominato `myAvailabilitySet` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="7e0a4-125">Deallocare tutte le macchine virtuali con il comando [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="7e0a4-126">L'esempio seguente dealloca la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="7e0a4-127">Convertire il set di disponibilità con il comando [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="7e0a4-128">L'esempio seguente converte il set di disponibilità denominato `myAvailabilitySet` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="7e0a4-129">Convertire tutte le macchine virtuali per l'utilizzo di dischi gestiti con il comando [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="7e0a4-130">Il processo seguente converte la macchina virtuale denominata `myVM`, incluso il disco del sistema operativo ed eventuali dischi dati:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="7e0a4-131">Avviare tutte le macchine virtuali dopo la conversione in dischi gestiti con il comando [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="7e0a4-132">Nell'esempio seguente viene avviata la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7e0a4-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="7e0a4-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e0a4-133">Next steps</span></span>
<span data-ttu-id="7e0a4-134">Per altre informazioni sulle opzioni di archiviazione, vedere [Panoramica di Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e0a4-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
