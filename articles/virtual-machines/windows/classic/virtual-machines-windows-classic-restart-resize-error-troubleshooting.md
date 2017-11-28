---
title: aaaVM il riavvio o problemi di ridimensionamento | Documenti Microsoft
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
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="9873f-103">Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Windows esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="9873f-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9873f-104">Classico</span><span class="sxs-lookup"><span data-stu-id="9873f-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="9873f-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="9873f-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="9873f-106">Quando si tenta di una macchina virtuale di Azure (VM) arrestata toostart, o si ridimensiona una macchina virtuale di Azure esistente, errore comune di hello che si verificano è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="9873f-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="9873f-107">Questo errore si verifica quando cluster hello o area geografica non è risorse disponibili oppure non è supporto hello richiesto di dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9873f-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9873f-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9873f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9873f-109">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9873f-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="9873f-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="9873f-111">Raccogliere log di controllo</span><span class="sxs-lookup"><span data-stu-id="9873f-111">Collect audit logs</span></span>
<span data-ttu-id="9873f-112">toostart risoluzione dei problemi, controllo hello collect registra errore hello tooidentify associata hello problema.</span><span class="sxs-lookup"><span data-stu-id="9873f-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="9873f-113">Nel portale di Azure hello, fare clic su **Sfoglia** > **macchine virtuali** > *la macchina virtuale Windows*  >   **Impostazioni** > **log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="9873f-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="9873f-114">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="9873f-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="9873f-115">Si tenta di toostart una macchina virtuale arrestata ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="9873f-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="9873f-116">Causa</span><span class="sxs-lookup"><span data-stu-id="9873f-116">Cause</span></span>
<span data-ttu-id="9873f-117">richiesta di Hello hello toostart arrestato VM ha toobe tentata al cluster originale hello che ospita il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="9873f-118">Cluster hello è richiesta di spazio libero disponibile toofulfill hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="9873f-119">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="9873f-119">Resolution</span></span>
* <span data-ttu-id="9873f-120">Creare un nuovo servizio cloud e associarlo a un'area o una rete virtuale basata sull'area, ma non a un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="9873f-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="9873f-121">Eliminare hello arrestato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9873f-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="9873f-122">Ricreare hello macchina virtuale nel nuovo servizio cloud di hello usando dischi hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="9873f-123">Avviare hello ricreato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9873f-123">Start hello re-created VM.</span></span>

<span data-ttu-id="9873f-124">Se si verifica un errore durante il tentativo di toocreate un nuovo servizio cloud, riprovare più tardi o modificare hello area per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9873f-125">nuovo servizio cloud di Hello avrà un nuovo nome e l'indirizzo VIP, pertanto è necessario toochange tali informazioni per tutte le dipendenze di hello che utilizzano tali informazioni per il servizio cloud esistente hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="9873f-126">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="9873f-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="9873f-127">Si tenta di tooresize una macchina virtuale esistente ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="9873f-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="9873f-128">Causa</span><span class="sxs-lookup"><span data-stu-id="9873f-128">Cause</span></span>
<span data-ttu-id="9873f-129">richiesta di Hello tooresize hello VM è toobe tentata al cluster originale hello servizio cloud hello host.</span><span class="sxs-lookup"><span data-stu-id="9873f-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="9873f-130">Tuttavia, non supporta cluster hello hello richiesto dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9873f-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="9873f-131">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="9873f-131">Resolution</span></span>
<span data-ttu-id="9873f-132">Ridurre hello richiesto dimensioni della macchina virtuale e riprovare hello ridimensionare richiesta.</span><span class="sxs-lookup"><span data-stu-id="9873f-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="9873f-133">Fare clic su **Esplora tutto** > **Macchine virtuali (classico)** > *la macchina virtuale* > **Impostazioni** > **Dimensioni**.</span><span class="sxs-lookup"><span data-stu-id="9873f-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="9873f-134">Per informazioni dettagliate, vedere [ridimensionare una macchina virtuale hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="9873f-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="9873f-135">Se non è possibile tooreduce hello dimensioni della macchina virtuale, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9873f-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="9873f-136">Creare un nuovo servizio cloud, assicurandosi che non è collegato il gruppo di affinità tooan e non è associata a una rete virtuale che è il gruppo di affinità tooan collegato.</span><span class="sxs-lookup"><span data-stu-id="9873f-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="9873f-137">Nel servizio creare una nuova VM con dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="9873f-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="9873f-138">È possibile consolidare tutte le macchine virtuali in hello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9873f-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="9873f-139">Se il servizio cloud esistente è associato a una rete virtuale basata sull'area, è possibile connettersi hello nuovo cloud servizio toohello rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="9873f-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="9873f-140">Se il servizio cloud esistente di hello non è associato a una rete virtuale basata sull'area, quindi si hanno toodelete hello macchine virtuali nel servizio cloud esistente hello e ricrearle in hello nuovo servizio cloud dei dischi.</span><span class="sxs-lookup"><span data-stu-id="9873f-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="9873f-141">Tuttavia, è importante tooremember che nuovo servizio cloud di hello avrà un nuovo nome e l'indirizzo VIP, pertanto sarà necessario tooupdate per tutte le dipendenze di hello che attualmente utilizzano queste informazioni per il servizio cloud esistente hello.</span><span class="sxs-lookup"><span data-stu-id="9873f-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9873f-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9873f-142">Next steps</span></span>
<span data-ttu-id="9873f-143">Se si verificano problemi durante la creazione di una VM Windows in Azure, vedere [Risolvere i problemi di distribuzione quando si crea una nuova macchina virtuale Windows in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9873f-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

