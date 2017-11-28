---
title: un disco dati da una macchina virtuale di Windows - Azure aaaDetach | Documenti Microsoft
description: Informazioni su un disco dati da una macchina virtuale in Azure tramite il modello di distribuzione di gestione risorse di hello toodetach.
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
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="13e50-103">Funzionamento dei dischi toodetach un tipo di dati da una macchina virtuale di Windows</span><span class="sxs-lookup"><span data-stu-id="13e50-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="13e50-104">Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente.</span><span class="sxs-lookup"><span data-stu-id="13e50-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="13e50-105">Rimuove il disco hello dalla macchina virtuale hello, ma non rimuove dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="13e50-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="13e50-106">Se si scollega un disco, questo non viene automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="13e50-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="13e50-107">Se è stato richiesto tooPremium archiviazione, si continuerà tooincur i costi di archiviazione per il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="13e50-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="13e50-108">Per ulteriori informazioni, vedere troppo[prezzi e fatturazione quando si utilizza l'archiviazione Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="13e50-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="13e50-109">Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.</span><span class="sxs-lookup"><span data-stu-id="13e50-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="13e50-110">Scollegare un disco dati tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="13e50-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="13e50-111">Nell'hub portale hello, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="13e50-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="13e50-112">Selezionare macchina virtuale hello che ha il disco dati hello toodetach desiderato e fare clic su **arrestare** toodeallocate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13e50-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="13e50-113">Nel pannello macchine virtuali di hello, selezionare **dischi**.</span><span class="sxs-lookup"><span data-stu-id="13e50-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="13e50-114">Nella parte superiore di hello di hello **dischi** pannello seleziona **modifica**.</span><span class="sxs-lookup"><span data-stu-id="13e50-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="13e50-115">In hello **dischi** pannello toohello a destra del disco dati hello che si desidera toodetach, fare clic su hello ![immagine del pulsante scollegamento](./media/detach-disk/detach.png) pulsante Disconnetti.</span><span class="sxs-lookup"><span data-stu-id="13e50-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="13e50-116">Una volta rimosso il disco di hello, fare clic su Salva nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="13e50-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="13e50-117">Nel Pannello di hello macchina virtuale, fare clic su **Panoramica** e quindi fare clic su hello **avviare** pulsante nella parte superiore di hello di hello toorestart di hello pannello VM.</span><span class="sxs-lookup"><span data-stu-id="13e50-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="13e50-118">Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.</span><span class="sxs-lookup"><span data-stu-id="13e50-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="13e50-119">Scollegare un disco dati tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="13e50-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="13e50-120">In questo esempio hello primo comando Ottiene hello macchina virtuale denominata **MyVM07** in hello **RG11** gruppo di risorse utilizzando il cmdlet Get-AzureRmVM hello.</span><span class="sxs-lookup"><span data-stu-id="13e50-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="13e50-121">comando archivi hello macchina virtuale in hello Hello **$VirtualMachine** variabile.</span><span class="sxs-lookup"><span data-stu-id="13e50-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="13e50-122">Hello secondo comando rimuove il disco di dati hello denominato DataDisk3 dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="13e50-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="13e50-123">comando finale Hello Aggiorna stato hello del processo di hello macchina virtuale toocomplete hello della rimozione di dischi dati hello.</span><span class="sxs-lookup"><span data-stu-id="13e50-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="13e50-124">Per altre informazioni, vedere [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="13e50-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e50-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13e50-125">Next steps</span></span>
<span data-ttu-id="13e50-126">Se si desidera disco dati di hello tooreuse, è sufficiente [collegarlo tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="13e50-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

