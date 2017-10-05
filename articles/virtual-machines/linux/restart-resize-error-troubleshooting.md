---
title: Problemi di riavvio o ridimensionamento della VM in Azure | Documentazione Microsoft
description: Risolvere i problemi della distribuzione Resource Manager con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="dd295-103">Risolvere i problemi di distribuzione con il riavvio o il ridimensionamento di una macchina virtuale Linux esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="dd295-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="dd295-104">Quando si prova ad avviare una macchina virtuale (VM) di Azure arrestata o se ne ridimensiona una esistente, l'errore comune che si verifica è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="dd295-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="dd295-105">L'errore si verifica quando il cluster o l'area non ha risorse disponibili o non può supportare le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="dd295-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="dd295-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="dd295-106">Collect activity logs</span></span>
<span data-ttu-id="dd295-107">Per avviare la risoluzione dei problemi, raccogliere i log delle attività per identificare l'errore associato al problema.</span><span class="sxs-lookup"><span data-stu-id="dd295-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="dd295-108">I collegamenti seguenti contengono informazioni dettagliate sul processo:</span><span class="sxs-lookup"><span data-stu-id="dd295-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="dd295-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="dd295-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="dd295-110">Visualizzare i log attività per gestire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="dd295-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="dd295-111">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="dd295-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="dd295-112">Si prova ad avviare una VM arrestata ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="dd295-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="dd295-113">Causa</span><span class="sxs-lookup"><span data-stu-id="dd295-113">Cause</span></span>
<span data-ttu-id="dd295-114">La richiesta di avvio della VM arrestata deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dd295-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="dd295-115">Tuttavia, il cluster non ha spazio disponibile per soddisfare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="dd295-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="dd295-116">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="dd295-116">Resolution</span></span>
* <span data-ttu-id="dd295-117">Arrestare tutte le VM nel set di disponibilità e quindi riavviare ogni VM.</span><span class="sxs-lookup"><span data-stu-id="dd295-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="dd295-118">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="dd295-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="dd295-119">Dopo l'arresto di tutte le VM, selezionare le VM arrestate e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="dd295-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="dd295-120">Ripetere la richiesta di riavvio in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="dd295-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="dd295-121">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="dd295-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="dd295-122">Si prova a ridimensionare una VM esistente ma viene visualizzato un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="dd295-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="dd295-123">Causa</span><span class="sxs-lookup"><span data-stu-id="dd295-123">Cause</span></span>
<span data-ttu-id="dd295-124">La richiesta di ridimensionamento della VM deve essere eseguita nel cluster originale che ospita il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dd295-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="dd295-125">Tuttavia, il cluster non supporta le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="dd295-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="dd295-126">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="dd295-126">Resolution</span></span>
* <span data-ttu-id="dd295-127">Ripetere la richiesta usando una VM di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="dd295-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="dd295-128">Se le dimensioni della VM richieste non possono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="dd295-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="dd295-129">Arrestare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="dd295-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="dd295-130">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="dd295-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="dd295-131">Dopo l'arresto di tutte le VM, ridimensionare la VM desiderata impostando una dimensione maggiore.</span><span class="sxs-lookup"><span data-stu-id="dd295-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="dd295-132">Selezionare la VM ridimensionata e fare clic su **Avvia**, quindi avviare ognuna delle VM arrestate.</span><span class="sxs-lookup"><span data-stu-id="dd295-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd295-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd295-133">Next steps</span></span>
<span data-ttu-id="dd295-134">Se si verificano problemi durante la creazione di una nuova VM Linux in Azure, vedere [Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Linux in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd295-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

