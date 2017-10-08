---
title: una macchina virtuale di Linux in Azure da codice non aaaConvert dischi toomanaged dischi - Azure gestito | Documenti Microsoft
description: Come tooconvert una VM Linux di dischi non gestito toomanaged dischi tramite Azure CLI 2.0 nel modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="dc7bf-103">Convertire una macchina virtuale Linux da dischi toomanaged dischi non gestito</span><span class="sxs-lookup"><span data-stu-id="dc7bf-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="dc7bf-104">Se si dispone di macchine virtuali Linux esistenti (VM) che usano dischi non gestiti, è possibile convertire hello macchine virtuali gestite toouse dischi tramite hello [dischi gestiti di Azure](../windows/managed-disks-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="dc7bf-105">Questo processo converte disco hello del sistema operativo sia eventuali dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="dc7bf-106">Questo articolo illustra come tooconvert macchine virtuali tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="dc7bf-107">Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="dc7bf-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="dc7bf-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="dc7bf-109">Convertire VM a istanza singola</span><span class="sxs-lookup"><span data-stu-id="dc7bf-109">Convert single-instance VMs</span></span>
<span data-ttu-id="dc7bf-110">Questa sezione vengono trattati come tooconvert a istanza singola macchine virtuali di Azure da codice non dischi toomanaged dischi.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="dc7bf-111">(Se le macchine virtuali si trovano in un set di disponibilità, vedere la sezione successiva di hello). È possibile utilizzare questo toostandard gestiti dischi dischi di macchine virtuali da dischi di toopremium gestiti i dischi premium (SSD) non gestita o da standard (HDD) non gestite di processo tooconvert hello.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="dc7bf-112">Deallocare hello VM utilizzando [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dc7bf-113">esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="dc7bf-114">Convertire i dischi di hello VM toomanaged utilizzando [az vm convertire](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dc7bf-115">Hello seguente converte processo hello macchina virtuale denominata `myVM`, tra cui disco hello del sistema operativo e qualsiasi disco dati:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dc7bf-116">Avviare hello VM dopo i dischi di hello conversione toomanaged utilizzando [inizio vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dc7bf-117">Dopo l'avvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="dc7bf-118">Convertire VM in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="dc7bf-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="dc7bf-119">Se le macchine virtuali hello che si desidera tooconvert toomanaged dischi sono in un set di disponibilità, è necessario innanzitutto tooconvert hello disponibilità set tooa gestito set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="dc7bf-120">Tutte le macchine virtuali nel set di disponibilità hello devono essere deallocate prima di convertire il set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="dc7bf-121">Piano tooconvert tutti i dischi di macchine virtuali toomanaged dopo la disponibilità di hello impostare autonomamente è stato convertito tooa gestito set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="dc7bf-122">Quindi, avviare tutte le macchine virtuali hello e continuare a funzionare come di consueto.</span><span class="sxs-lookup"><span data-stu-id="dc7bf-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="dc7bf-123">Elencare tutte le macchine virtuali in un set di disponibilità con il comando [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="dc7bf-124">Hello esempio seguente vengono elencate tutte le macchine virtuali in disponibilità hello set denominata `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="dc7bf-125">Deallocare tutte le macchine virtuali hello utilizzando [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dc7bf-126">esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dc7bf-127">Convertire disponibilità hello impostare utilizzando [convert di set di disponibilità vm az](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="dc7bf-128">esempio Hello converte disponibilità hello set denominata `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="dc7bf-129">Convertire tutti i dischi di toomanaged hello macchine virtuali tramite [az vm convertire](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dc7bf-130">Hello seguente converte processo hello macchina virtuale denominata `myVM`, tra cui disco hello del sistema operativo e qualsiasi disco dati:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="dc7bf-131">Avviare tutte le macchine virtuali hello dopo i dischi di hello conversione toomanaged utilizzando [inizio vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dc7bf-132">Dopo l'avvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dc7bf-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="dc7bf-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc7bf-133">Next steps</span></span>
<span data-ttu-id="dc7bf-134">Per altre informazioni sulle opzioni di archiviazione, vedere [Panoramica di Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc7bf-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
