---
title: Risolvere i problemi di distribuzione di VM Linux - Resource Manager | Documentazione Microsoft
description: Risolvere i problemi della distribuzione Resource Manager quando si crea una nuova macchina virtuale Linux in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: aea5db05843b0175b8ef8b713944e12262e33010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="872c4-103">Risolvere i problemi della distribuzione Resource Manager con la creazione di una nuova macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="872c4-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="872c4-104">Problemi principali</span><span class="sxs-lookup"><span data-stu-id="872c4-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="872c4-105">Per altri problemi e domande sulla distribuzione delle VM, vedere [Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="872c4-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="872c4-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="872c4-106">Collect activity logs</span></span>
<span data-ttu-id="872c4-107">Per avviare la risoluzione dei problemi, raccogliere i log delle attività per identificare l'errore associato al problema.</span><span class="sxs-lookup"><span data-stu-id="872c4-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="872c4-108">I collegamenti seguenti contengono informazioni dettagliate sul processo da seguire.</span><span class="sxs-lookup"><span data-stu-id="872c4-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="872c4-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="872c4-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="872c4-110">Visualizzare i log attività per gestire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="872c4-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="872c4-111">**S:** se il sistema operativo Linux è generalizzato e viene caricato e/o acquisito con l'impostazione generalizzata, non si verificheranno errori.</span><span class="sxs-lookup"><span data-stu-id="872c4-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="872c4-112">Analogamente, se il sistema operativo Linux è specializzato e viene caricato e/o acquisito con l'impostazione specializzata, non si verificheranno errori.</span><span class="sxs-lookup"><span data-stu-id="872c4-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="872c4-113">**Errori di caricamento:**</span><span class="sxs-lookup"><span data-stu-id="872c4-113">**Upload Errors:**</span></span>

<span data-ttu-id="872c4-114">**N<sup>1</sup>:** se il sistema operativo è un sistema Linux generalizzato e viene caricato come specializzato, si verificherà un errore di timeout del provisioning perché la macchina virtuale risulta bloccata nella fase di provisioning.</span><span class="sxs-lookup"><span data-stu-id="872c4-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="872c4-115">**N<sup>2</sup>:** se il sistema operativo è un sistema Linux specializzato e viene caricato come generalizzato, si verificherà un errore di provisioning perché la nuova macchina virtuale viene eseguita con il nome computer, il nome utente e la password originali.</span><span class="sxs-lookup"><span data-stu-id="872c4-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="872c4-116">**Risoluzione:**</span><span class="sxs-lookup"><span data-stu-id="872c4-116">**Resolution:**</span></span>

<span data-ttu-id="872c4-117">Per risolvere entrambi questi errori, caricare il disco rigido virtuale originale, disponibile in locale, con la stessa impostazione usata per il sistema operativo (generalizzato/specializzato).</span><span class="sxs-lookup"><span data-stu-id="872c4-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="872c4-118">Per caricare il disco come generalizzato, ricordarsi di eseguire prima -deprovision.</span><span class="sxs-lookup"><span data-stu-id="872c4-118">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="872c4-119">**Errori di acquisizione:**</span><span class="sxs-lookup"><span data-stu-id="872c4-119">**Capture Errors:**</span></span>

<span data-ttu-id="872c4-120">**N<sup>3</sup>:** se il sistema operativo è un sistema Linux generalizzato e viene acquisito come specializzato, si verificherà un errore di timeout del provisioning perché la macchina virtuale originale non può essere usata essendo contrassegnata come generalizzata.</span><span class="sxs-lookup"><span data-stu-id="872c4-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="872c4-121">**N<sup>4</sup>:** se il sistema operativo è un sistema Linux specializzato e viene acquisito come generalizzato, si verificherà un errore di provisioning perché la nuova macchina virtuale viene eseguita con il nome computer, il nome utente e la password originali.</span><span class="sxs-lookup"><span data-stu-id="872c4-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="872c4-122">La VM originale, inoltre, non può essere usata perché è contrassegnata come specializzata.</span><span class="sxs-lookup"><span data-stu-id="872c4-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="872c4-123">**Risoluzione:**</span><span class="sxs-lookup"><span data-stu-id="872c4-123">**Resolution:**</span></span>

<span data-ttu-id="872c4-124">Per risolvere entrambi questi errori, eliminare l'immagine corrente dal portale e [acquisirla di nuovo dai dischi rigidi virtuali correnti](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) con la stessa impostazione usata per il sistema operativo (generalizzato/specializzato).</span><span class="sxs-lookup"><span data-stu-id="872c4-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="872c4-125">Problema: Immagine personalizzata/della raccolta/del marketplace - errore di allocazione</span><span class="sxs-lookup"><span data-stu-id="872c4-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="872c4-126">Questo errore si verifica nelle situazioni in cui la nuova richiesta di VM viene aggiunta a un cluster che non può supportare le dimensioni della VM richieste oppure non ha spazio disponibile sufficiente per soddisfare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="872c4-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="872c4-127">**Causa 1:** il cluster non supporta le dimensioni della VM richieste.</span><span class="sxs-lookup"><span data-stu-id="872c4-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="872c4-128">**Risoluzione 1:**</span><span class="sxs-lookup"><span data-stu-id="872c4-128">**Resolution 1:**</span></span>

* <span data-ttu-id="872c4-129">Ripetere la richiesta usando una VM di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="872c4-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="872c4-130">Se le dimensioni della VM richieste non possono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="872c4-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="872c4-131">Arrestare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="872c4-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="872c4-132">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="872c4-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="872c4-133">Dopo l'arresto di tutte le VM, creare la nuova VM con le dimensioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="872c4-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="872c4-134">Avviare prima di tutto la nuova VM e quindi selezionare le VM arrestate e fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="872c4-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="872c4-135">**Causa 2:** il cluster non ha risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="872c4-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="872c4-136">**Risoluzione 2:**</span><span class="sxs-lookup"><span data-stu-id="872c4-136">**Resolution 2:**</span></span>

* <span data-ttu-id="872c4-137">Ripetere la richiesta in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="872c4-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="872c4-138">Se la nuova VM può far parte di un set di disponibilità diverso</span><span class="sxs-lookup"><span data-stu-id="872c4-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="872c4-139">Creare una nuova VM in un altro set di disponibilità nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="872c4-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="872c4-140">Aggiungere la nuova VM alla stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="872c4-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="872c4-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="872c4-141">Next steps</span></span>
<span data-ttu-id="872c4-142">Se si incontrano problemi quando si avvia una VM Linux arrestata o si ridimensiona una VM Linux esistente in Azure, vedere [Risolvere i problemi della distribuzione di Resource Manager con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="872c4-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

