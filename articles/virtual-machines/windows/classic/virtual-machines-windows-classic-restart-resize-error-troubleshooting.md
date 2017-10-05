---
title: Problemi di riavvio o ridimensionamento della VM | Documentazione Microsoft
description: Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Windows esistente in Azure
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 7fe0636366c60d4679cfc69bd96cd532695b080e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="fa4bc-103">Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Windows esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="fa4bc-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa4bc-104">Classico</span><span class="sxs-lookup"><span data-stu-id="fa4bc-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="fa4bc-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="fa4bc-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="fa4bc-106">Quando si prova ad avviare una macchina virtuale (VM) di Azure arrestata o se ne ridimensiona una esistente, l'errore comune che si verifica è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="fa4bc-107">L'errore si verifica quando il cluster o l'area non ha risorse disponibili o non può supportare le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa4bc-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa4bc-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fa4bc-109">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="fa4bc-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="fa4bc-111">Raccogliere log di controllo</span><span class="sxs-lookup"><span data-stu-id="fa4bc-111">Collect audit logs</span></span>
<span data-ttu-id="fa4bc-112">Per avviare la risoluzione dei problemi, raccogliere i log di controllo per identificare l'errore associato al problema.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="fa4bc-113">Nel portale di Azure fare clic su **Esplora** > **Macchine virtuali** > *Macchina virtuale Windows* > **Impostazioni** > **Log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="fa4bc-114">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="fa4bc-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="fa4bc-115">Si prova ad avviare una VM arrestata ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fa4bc-116">Causa</span><span class="sxs-lookup"><span data-stu-id="fa4bc-116">Cause</span></span>
<span data-ttu-id="fa4bc-117">La richiesta di avvio della VM arrestata deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="fa4bc-118">Tuttavia, il cluster non ha spazio disponibile per soddisfare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="fa4bc-119">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="fa4bc-119">Resolution</span></span>
* <span data-ttu-id="fa4bc-120">Creare un nuovo servizio cloud e associarlo a un'area o una rete virtuale basata sull'area, ma non a un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="fa4bc-121">Eliminare la VM arrestata.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="fa4bc-122">Ricreare la VM nel nuovo servizio cloud usando i dischi.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="fa4bc-123">Avviare la macchina virtuale ricreata.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-123">Start the re-created VM.</span></span>

<span data-ttu-id="fa4bc-124">Se si verifica un errore durante il tentativo di creare un nuovo servizio cloud, riprovare più tardi o cambiare l'area per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-124">If you get an error when trying to create a new cloud service, either retry later or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa4bc-125">Il nuovo servizio cloud avrà un nuovo nome e un indirizzo VIP, quindi si dovranno modificare tali informazioni per tutte le dipendenze che usano queste informazioni per il servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-125">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="fa4bc-126">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="fa4bc-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="fa4bc-127">Si prova a ridimensionare una VM esistente ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fa4bc-128">Causa</span><span class="sxs-lookup"><span data-stu-id="fa4bc-128">Cause</span></span>
<span data-ttu-id="fa4bc-129">La richiesta di ridimensionamento della VM deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="fa4bc-130">Tuttavia, il cluster non supporta le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="fa4bc-131">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="fa4bc-131">Resolution</span></span>
<span data-ttu-id="fa4bc-132">Ridurre le dimensioni della VM richieste e quindi ripetere la richiesta di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="fa4bc-133">Fare clic su **Esplora tutto** > **Macchine virtuali (classico)** > *la macchina virtuale* > **Impostazioni** > **Dimensioni**.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="fa4bc-134">Per i passaggi dettagliati, vedere l'articolo relativo al [Ridimensionamento della macchina virtuale](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa4bc-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="fa4bc-135">Se non è possibile ridurre le dimensioni della VM, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="fa4bc-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="fa4bc-136">Creare un nuovo servizio cloud, verificando che non sia collegato a un gruppo di affinità e non sia associato a una rete virtuale collegata a un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="fa4bc-137">Nel servizio creare una nuova VM con dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="fa4bc-138">È possibile consolidare tutte le VM nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="fa4bc-139">Se il servizio cloud esistente è associato a una rete virtuale basata sull'area, è possibile connetterlo alla rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="fa4bc-140">Se il servizio cloud esistente non è associato a una rete virtuale basata sull'area, è necessario eliminare le VM nel servizio cloud esistente e ricrearle nel nuovo servizio cloud dai relativi dischi.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="fa4bc-141">È tuttavia importante ricordare che il nuovo servizio cloud avrà un nuovo nome e un nuovo indirizzo VIP, quindi sarà necessario aggiornarli per tutte le dipendenze che attualmente usano queste informazioni per il servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="fa4bc-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa4bc-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa4bc-142">Next steps</span></span>
<span data-ttu-id="fa4bc-143">Se si verificano problemi durante la creazione di una VM Windows in Azure, vedere [Risolvere i problemi di distribuzione quando si crea una nuova macchina virtuale Windows in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa4bc-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

