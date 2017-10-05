---
title: Problemi di riavvio o ridimensionamento della VM | Documentazione Microsoft
description: Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="16b08-103">Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="16b08-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16b08-104">Classico</span><span class="sxs-lookup"><span data-stu-id="16b08-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="16b08-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="16b08-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="16b08-106">Quando si prova ad avviare una macchina virtuale (VM) di Azure arrestata o se ne ridimensiona una esistente, l'errore comune che si verifica è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="16b08-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="16b08-107">L'errore si verifica quando il cluster o l'area non ha risorse disponibili o non può supportare le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="16b08-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="16b08-108">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="16b08-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="16b08-109">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="16b08-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="16b08-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="16b08-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="16b08-111">Per la versione di Resource Manager, vedere [qui](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16b08-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="16b08-112">Raccogliere log di controllo</span><span class="sxs-lookup"><span data-stu-id="16b08-112">Collect audit logs</span></span>
<span data-ttu-id="16b08-113">Per avviare la risoluzione dei problemi, raccogliere i log di controllo per identificare l'errore associato al problema.</span><span class="sxs-lookup"><span data-stu-id="16b08-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="16b08-114">Nel portale di Azure fare clic su **Esplora** > **Macchine virtuali** > *Macchina virtuale Linuz* > **Impostazioni** > **Log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="16b08-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="16b08-115">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="16b08-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="16b08-116">Si prova ad avviare una VM arrestata ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="16b08-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="16b08-117">Causa</span><span class="sxs-lookup"><span data-stu-id="16b08-117">Cause</span></span>
<span data-ttu-id="16b08-118">La richiesta di avvio della VM arrestata deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16b08-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="16b08-119">Tuttavia, il cluster non ha spazio disponibile per soddisfare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="16b08-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="16b08-120">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="16b08-120">Resolution</span></span>
* <span data-ttu-id="16b08-121">Creare un nuovo servizio cloud e associarlo a un'area o una rete virtuale basata sull'area, ma non a un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="16b08-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="16b08-122">Eliminare la VM arrestata.</span><span class="sxs-lookup"><span data-stu-id="16b08-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="16b08-123">Ricreare la VM nel nuovo servizio cloud usando i dischi.</span><span class="sxs-lookup"><span data-stu-id="16b08-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="16b08-124">Avviare la macchina virtuale ricreata.</span><span class="sxs-lookup"><span data-stu-id="16b08-124">Start the re-created VM.</span></span>

<span data-ttu-id="16b08-125">Se si verifica un errore durante il tentativo di creare un nuovo servizio cloud, riprovare in un secondo momento o cambiare l'area per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16b08-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16b08-126">Il nuovo servizio cloud avrà un nuovo nome e un indirizzo VIP, quindi si dovranno modificare tali informazioni per tutte le dipendenze che usano queste informazioni per il servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="16b08-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="16b08-127">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="16b08-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="16b08-128">Si prova a ridimensionare una VM esistente ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="16b08-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="16b08-129">Causa</span><span class="sxs-lookup"><span data-stu-id="16b08-129">Cause</span></span>
<span data-ttu-id="16b08-130">La richiesta di ridimensionamento della VM deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16b08-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="16b08-131">Tuttavia, il cluster non supporta le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="16b08-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="16b08-132">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="16b08-132">Resolution</span></span>
<span data-ttu-id="16b08-133">Ridurre le dimensioni della VM richieste e quindi ripetere la richiesta di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="16b08-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="16b08-134">Fare clic su **Esplora tutto** > **Macchine virtuali (classico)** > *la macchina virtuale* > **Impostazioni** > **Dimensioni**.</span><span class="sxs-lookup"><span data-stu-id="16b08-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="16b08-135">Per i passaggi dettagliati, vedere l'articolo relativo al [Ridimensionamento della macchina virtuale](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="16b08-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="16b08-136">Se non è possibile ridurre le dimensioni della VM, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="16b08-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="16b08-137">Creare un nuovo servizio cloud, verificando che non sia collegato a un gruppo di affinità e non sia associato a una rete virtuale collegata a un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="16b08-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="16b08-138">Nel servizio creare una nuova VM con dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="16b08-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="16b08-139">È possibile consolidare tutte le VM nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16b08-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="16b08-140">Se il servizio cloud esistente è associato a una rete virtuale basata sull'area, è possibile connetterlo alla rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="16b08-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="16b08-141">Se il servizio cloud esistente non è associato a una rete virtuale basata sull'area, è necessario eliminare le VM nel servizio cloud esistente e ricrearle nel nuovo servizio cloud dai relativi dischi.</span><span class="sxs-lookup"><span data-stu-id="16b08-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="16b08-142">È tuttavia importante ricordare che il nuovo servizio cloud avrà un nuovo nome e un nuovo indirizzo VIP, quindi sarà necessario aggiornarli per tutte le dipendenze che attualmente usano queste informazioni per il servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="16b08-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16b08-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16b08-143">Next steps</span></span>
<span data-ttu-id="16b08-144">Se si verificano problemi durante la creazione di una nuova VM Linux in Azure, vedere [Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Linux in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16b08-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

