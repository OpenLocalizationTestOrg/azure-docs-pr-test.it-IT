---
title: una macchina virtuale nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Creare una macchina virtuale Windows in hello portale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="efcf0-103">Creare una macchina virtuale Windows in esecuzione in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="efcf0-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="efcf0-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="efcf0-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="efcf0-105">PowerShell: distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="efcf0-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="efcf0-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="efcf0-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="efcf0-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="efcf0-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="efcf0-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="efcf0-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="efcf0-109">Informazioni su come troppo[eseguire questi passaggi tramite il modello di distribuzione di gestione risorse di hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) utilizzando hello **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="efcf0-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="efcf0-110">In questa esercitazione illustra come toocreate di Azure macchina virtuale (VM) in esecuzione Windows in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="efcf0-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="efcf0-111">Si userà un'immagine di Windows Server, ad esempio, ma che è solo una di hello molte immagini offerte di Azure.</span><span class="sxs-lookup"><span data-stu-id="efcf0-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="efcf0-112">Si noti che le opzioni dell’immagine dipendono dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="efcf0-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="efcf0-113">Ad esempio, le immagini del desktop di Windows potrebbero essere disponibile tooMSDN sottoscrittori.</span><span class="sxs-lookup"><span data-stu-id="efcf0-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="efcf0-114">In questa sezione illustra come hello toouse **Dashboard** in hello tooselect portale Azure e quindi creare macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="efcf0-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="efcf0-115">È inoltre possibile creare VM usando le [proprie immagini](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="efcf0-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="efcf0-116">toolearn su questo e altri metodi, vedere [toocreate modi diversi una macchina virtuale Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efcf0-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="efcf0-117"><a id="createvirtualmachine"></a>Crea macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="efcf0-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="efcf0-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efcf0-118">Next steps</span></span>
* <span data-ttu-id="efcf0-119">Informazioni su come troppo[creare una macchina virtuale con modello di distribuzione di gestione risorse di hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="efcf0-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="efcf0-120">Accedere a macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="efcf0-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="efcf0-121">Per istruzioni, vedere [accedere alla macchina virtuale tooa che esegue Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="efcf0-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="efcf0-122">Collegare un dati toostore su disco.</span><span class="sxs-lookup"><span data-stu-id="efcf0-122">Attach a disk toostore data.</span></span> <span data-ttu-id="efcf0-123">È possibile collegare sia dischi vuoti sia dischi contenenti dati.</span><span class="sxs-lookup"><span data-stu-id="efcf0-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="efcf0-124">Per istruzioni, vedere hello [collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="efcf0-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
