---
title: un disco dati da una VM Linux - Azure aaaDetach | Documenti Microsoft
description: Informazioni toodetach un disco dati da una macchina virtuale in Azure utilizzando CLI 2.0 o hello portale di Azure.
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
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="fc1ab-103">Funzionamento dei dischi toodetach un tipo di dati da una macchina virtuale di Linux</span><span class="sxs-lookup"><span data-stu-id="fc1ab-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="fc1ab-104">Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="fc1ab-105">Rimuove il disco hello dalla macchina virtuale hello, ma non rimuove dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="fc1ab-106">Se si scollega un disco, questo non viene automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="fc1ab-107">Se è stato richiesto tooPremium archiviazione, si continuerà tooincur i costi di archiviazione per il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="fc1ab-108">Per ulteriori informazioni, vedere troppo[prezzi e fatturazione quando si utilizza l'archiviazione Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="fc1ab-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="fc1ab-109">Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="fc1ab-110">Scollegare un disco dati tramite l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="fc1ab-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="fc1ab-111">Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="fc1ab-112">Scollegare un disco dati tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="fc1ab-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="fc1ab-113">Nell'hub portale hello, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="fc1ab-114">Selezionare macchina virtuale hello che ha il disco dati hello toodetach desiderato e fare clic su **arrestare** toodeallocate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="fc1ab-115">Nel pannello macchine virtuali di hello, selezionare **dischi**.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="fc1ab-116">Nella parte superiore di hello di hello **dischi** pannello seleziona **modifica**.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="fc1ab-117">In hello **dischi** pannello toohello a destra del disco dati hello che si desidera toodetach, fare clic su hello ![immagine del pulsante scollegamento](./media/detach-disk/detach.png) pulsante Disconnetti.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="fc1ab-118">Una volta rimosso il disco di hello, fare clic su Salva nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="fc1ab-119">Nel Pannello di hello macchina virtuale, fare clic su **Panoramica** e quindi fare clic su hello **avviare** pulsante nella parte superiore di hello di hello toorestart di hello pannello VM.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="fc1ab-120">Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.</span><span class="sxs-lookup"><span data-stu-id="fc1ab-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="fc1ab-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc1ab-121">Next steps</span></span>
<span data-ttu-id="fc1ab-122">Se si desidera disco dati di hello tooreuse, è sufficiente [collegarlo tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc1ab-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

