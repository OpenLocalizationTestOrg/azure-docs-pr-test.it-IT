---
title: Problemi di riavvio o ridimensionamento della VM in Azure | Documentazione Microsoft
description: Risolvere i problemi della distribuzione Resource Manager con il riavvio e il ridimensionamento di una macchina virtuale Windows esistente in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 078c4666f047604b1732e828d27e7e26383aa616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="085c8-103">Risolvere i problemi di distribuzione con il riavvio o il ridimensionamento di una VM Windows esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="085c8-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="085c8-104">Quando si prova ad avviare una macchina virtuale (VM) di Azure arrestata o se ne ridimensiona una esistente, l'errore comune che si verifica è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="085c8-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="085c8-105">L'errore si verifica quando il cluster o l'area non ha risorse disponibili o non può supportare le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="085c8-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="085c8-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="085c8-106">Collect activity logs</span></span>
<span data-ttu-id="085c8-107">Per avviare la risoluzione dei problemi, raccogliere i log delle attività per identificare l'errore associato al problema.</span><span class="sxs-lookup"><span data-stu-id="085c8-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="085c8-108">I collegamenti seguenti contengono informazioni dettagliate sul processo:</span><span class="sxs-lookup"><span data-stu-id="085c8-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="085c8-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="085c8-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="085c8-110">Visualizzare i log attività per gestire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="085c8-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="085c8-111">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="085c8-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="085c8-112">Si prova ad avviare una VM arrestata ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="085c8-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="085c8-113">Causa</span><span class="sxs-lookup"><span data-stu-id="085c8-113">Cause</span></span>
<span data-ttu-id="085c8-114">La richiesta di avvio della VM arrestata deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="085c8-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="085c8-115">Tuttavia, il cluster non ha spazio disponibile per soddisfare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="085c8-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="085c8-116">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="085c8-116">Resolution</span></span>
* <span data-ttu-id="085c8-117">Arrestare tutte le VM nel set di disponibilità e quindi riavviare ogni VM.</span><span class="sxs-lookup"><span data-stu-id="085c8-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="085c8-118">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="085c8-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="085c8-119">Dopo l'arresto di tutte le VM, selezionare le VM arrestate e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="085c8-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="085c8-120">Ripetere la richiesta di riavvio in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="085c8-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="085c8-121">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="085c8-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="085c8-122">Si prova a ridimensionare una VM esistente ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="085c8-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="085c8-123">Causa</span><span class="sxs-lookup"><span data-stu-id="085c8-123">Cause</span></span>
<span data-ttu-id="085c8-124">La richiesta di ridimensionamento della VM deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="085c8-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="085c8-125">Tuttavia, il cluster non supporta le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="085c8-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="085c8-126">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="085c8-126">Resolution</span></span>
* <span data-ttu-id="085c8-127">Ripetere la richiesta usando una VM di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="085c8-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="085c8-128">Se le dimensioni della VM richieste non possono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="085c8-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="085c8-129">Arrestare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="085c8-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="085c8-130">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="085c8-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="085c8-131">Dopo l'arresto di tutte le VM, ridimensionare la VM desiderata impostando una dimensione maggiore.</span><span class="sxs-lookup"><span data-stu-id="085c8-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="085c8-132">Selezionare la VM ridimensionata e fare clic su **Avvia**, quindi avviare ognuna delle VM arrestate.</span><span class="sxs-lookup"><span data-stu-id="085c8-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="085c8-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="085c8-133">Next steps</span></span>
<span data-ttu-id="085c8-134">Se si verificano problemi durante la creazione di una nuova VM Windows in Azure, vedere [Risolvere i problemi della distribuzione Resource Manager con la creazione di una nuova macchina virtuale Windows in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="085c8-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

