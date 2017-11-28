---
title: Scollegare un disco dati da una macchina virtuale Linux - Azure | Microsoft Docs
description: Informazioni su come scollegare un disco dati da una macchina virtuale in Azure tramite l'interfaccia della riga di comando 2.0 o il portale di Azure.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="aedd2-103">Come scollegare un disco dati da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="aedd2-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="aedd2-104">Quando un disco dati collegato a una macchina virtuale non è più necessario, è possibile scollegarlo con facilità.</span><span class="sxs-lookup"><span data-stu-id="aedd2-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="aedd2-105">Il disco verrà rimosso dalla macchina virtuale, ma non dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="aedd2-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="aedd2-106">Se si scollega un disco, questo non viene automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="aedd2-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="aedd2-107">Se è stata eseguita la sottoscrizione all'archiviazione Premium, si continueranno a sostenere costi di archiviazione per il disco.</span><span class="sxs-lookup"><span data-stu-id="aedd2-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="aedd2-108">Per altre informazioni fare riferimento a [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="aedd2-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="aedd2-109">Se si vogliono riusare i dati presenti nel disco, è possibile ricollegarlo alla stessa macchina virtuale o collegarlo a una nuova.</span><span class="sxs-lookup"><span data-stu-id="aedd2-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="aedd2-110">Scollegare un disco dati tramite l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="aedd2-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="aedd2-111">Il disco rimane nello spazio di archiviazione ma non è più collegato a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aedd2-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="aedd2-112">Scollegare un disco dati tramite il portale</span><span class="sxs-lookup"><span data-stu-id="aedd2-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="aedd2-113">Nell'hub del portale selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="aedd2-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="aedd2-114">Selezionare la macchina virtuale con il disco dati che si vuole scollegare e fare clic su **Arresta** per deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aedd2-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="aedd2-115">Nel pannello delle macchine virtuali selezionare **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="aedd2-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="aedd2-116">Nella parte superiore del pannello **Dischi** selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="aedd2-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="aedd2-117">Nel pannello **Dischi**, fare clic sul pulsante per scollegare il disco ![Immagine del pulsante per scollegare il disco](./media/detach-disk/detach.png) nella parte più a destra del disc dati.</span><span class="sxs-lookup"><span data-stu-id="aedd2-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="aedd2-118">Dopo aver rimosso il disco, fare clic su Salva nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="aedd2-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="aedd2-119">Nel pannello delle macchine virtuali fare clic su **Panoramica** e quindi fare clic su **Avvia** nella parte superiore del pannello per riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aedd2-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="aedd2-120">Il disco rimane nello spazio di archiviazione ma non è più collegato a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aedd2-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="aedd2-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aedd2-121">Next steps</span></span>
<span data-ttu-id="aedd2-122">Se si intende usare nuovamente il disco dati, è sufficiente [collegarlo a un'altra macchina virtuale](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aedd2-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

