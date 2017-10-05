---
title: Scollegare un disco dati da una VM Windows - Azure | Microsoft Docs
description: Informazioni su come scollegare un disco dati da una macchina virtuale in Azure usando il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="aa012-103">Come scollegare un disco dati da una macchina virtuale di Windows</span><span class="sxs-lookup"><span data-stu-id="aa012-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="aa012-104">Quando un disco dati collegato a una macchina virtuale non è più necessario, è possibile scollegarlo con facilità.</span><span class="sxs-lookup"><span data-stu-id="aa012-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="aa012-105">Il disco verrà rimosso dalla macchina virtuale, ma non dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="aa012-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="aa012-106">Se si scollega un disco, questo non viene automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="aa012-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="aa012-107">Se è stata eseguita la sottoscrizione all'archiviazione Premium, si continueranno a sostenere costi di archiviazione per il disco.</span><span class="sxs-lookup"><span data-stu-id="aa012-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="aa012-108">Per altre informazioni fare riferimento a [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="aa012-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="aa012-109">Se si vogliono riusare i dati presenti nel disco, è possibile ricollegarlo alla stessa macchina virtuale o collegarlo a una nuova.</span><span class="sxs-lookup"><span data-stu-id="aa012-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="aa012-110">Scollegare un disco dati tramite il portale</span><span class="sxs-lookup"><span data-stu-id="aa012-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="aa012-111">Nell'hub del portale selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="aa012-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="aa012-112">Selezionare la macchina virtuale con il disco dati che si vuole scollegare e fare clic su **Arresta** per deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa012-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="aa012-113">Nel pannello delle macchine virtuali selezionare **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="aa012-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="aa012-114">Nella parte superiore del pannello **Dischi** selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="aa012-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="aa012-115">Nel pannello **Dischi**, fare clic sul pulsante per scollegare il disco ![Immagine del pulsante per scollegare il disco](./media/detach-disk/detach.png) nella parte più a destra del disc dati.</span><span class="sxs-lookup"><span data-stu-id="aa012-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="aa012-116">Dopo aver rimosso il disco, fare clic su Salva nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="aa012-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="aa012-117">Nel pannello delle macchine virtuali fare clic su **Panoramica** e quindi fare clic su **Avvia** nella parte superiore del pannello per riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa012-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="aa012-118">Il disco rimane nello spazio di archiviazione ma non è più collegato a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa012-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="aa012-119">Scollegare un disco dati tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa012-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="aa012-120">In questo esempio, il primo comando consente di denominare la macchina virtuale **MyVM07** nel gruppo di risorse **RG11** usando il cmdlet Get-AzureRmVM.</span><span class="sxs-lookup"><span data-stu-id="aa012-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="aa012-121">Il comando archivia la macchina virtuale nella variabile **$VirtualMachine** .</span><span class="sxs-lookup"><span data-stu-id="aa012-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="aa012-122">Il secondo comando rimuove il disco dati denominato DataDisk3 dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aa012-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="aa012-123">L'ultimo comando aggiorna lo stato della macchina virtuale per completare il processo di rimozione del disco dati.</span><span class="sxs-lookup"><span data-stu-id="aa012-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="aa012-124">Per altre informazioni, vedere [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="aa012-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa012-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa012-125">Next steps</span></span>
<span data-ttu-id="aa012-126">Se si desidera riutilizzare il disco dati, è sufficiente [collegarlo a un'altra VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="aa012-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

