---
title: distribuzione della macchina virtuale Windows in Azure aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi della distribuzione Resource Manager quando si crea una nuova macchina virtuale Windows in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="6dd97-103">Risolvere i problemi di distribuzione quando si crea una nuova macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="6dd97-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="6dd97-104">Problemi principali</span><span class="sxs-lookup"><span data-stu-id="6dd97-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="6dd97-105">Per altri problemi e domande sulla distribuzione delle VM, vedere [Risolvere i problemi di distribuzione della macchina virtuale Windows in Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="6dd97-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="6dd97-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="6dd97-106">Collect activity logs</span></span>
<span data-ttu-id="6dd97-107">toostart risoluzione dei problemi, attività di raccolta hello registra errore hello tooidentify associata hello problema.</span><span class="sxs-lookup"><span data-stu-id="6dd97-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="6dd97-108">Hello collegamenti riportati di seguito contengono informazioni dettagliate su hello processo toofollow.</span><span class="sxs-lookup"><span data-stu-id="6dd97-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="6dd97-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="6dd97-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="6dd97-110">Visualizzare toomanage log attività Azure le risorse</span><span class="sxs-lookup"><span data-stu-id="6dd97-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="6dd97-111">**Y:** se hello del sistema operativo è Windows generalizzato, viene caricato e/o acquisito con impostazione hello generalizzato, quindi non essere presenti gli eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="6dd97-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="6dd97-112">Analogamente, se hello del sistema operativo è Windows specializzati e viene caricato e/o acquisito con hello specializzati impostazione, quindi non essere presenti gli eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="6dd97-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="6dd97-113">**Errori di caricamento:**</span><span class="sxs-lookup"><span data-stu-id="6dd97-113">**Upload Errors:**</span></span>

<span data-ttu-id="6dd97-114">**N<sup>1</sup>:** se hello del sistema operativo è generalizzato di Windows e che è stato caricato come specializzato, si otterrà un errore di timeout di provisioning con hello VM bloccato nella schermata di configurazione guidata hello.</span><span class="sxs-lookup"><span data-stu-id="6dd97-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="6dd97-115">**N<sup>2</sup>:** se hello del sistema operativo è Windows specializzati e che è stato caricato come generalizzato, si otterrà un errore di provisioning con hello VM bloccato nella schermata di configurazione guidata hello perché hello nuova macchina virtuale è in esecuzione con computer originale hello nome, nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="6dd97-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="6dd97-116">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="6dd97-116">**Resolution**</span></span>

<span data-ttu-id="6dd97-117">utilizzare entrambi questi errori, tooresolve [tooupload Aggiungi AzureRmVhd hello VHD originale](https://msdn.microsoft.com/library/mt603554.aspx), disponibili in locale, con hello impostazione per hello del sistema operativo (generalizzata o specializzata).</span><span class="sxs-lookup"><span data-stu-id="6dd97-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="6dd97-118">tooupload come generalizzato, tenere presente che innanzitutto toorun sysprep.</span><span class="sxs-lookup"><span data-stu-id="6dd97-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="6dd97-119">**Errori di acquisizione:**</span><span class="sxs-lookup"><span data-stu-id="6dd97-119">**Capture Errors:**</span></span>

<span data-ttu-id="6dd97-120">**N<sup>3</sup>:** se hello del sistema operativo è generalizzato di Windows e l'acquisizione come specializzato, verrà generato un errore di timeout del provisioning poiché hello originale VM non è utilizzabile in quanto è contrassegnato come generalizzato.</span><span class="sxs-lookup"><span data-stu-id="6dd97-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="6dd97-121">**N<sup>4</sup>:** se hello del sistema operativo è Windows specializzati e che viene acquisito come generalizzato, si otterrà un errore di provisioning perché hello nuova macchina virtuale è in esecuzione con il nome del computer originale di hello, username e password.</span><span class="sxs-lookup"><span data-stu-id="6dd97-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="6dd97-122">Inoltre, hello originale VM non è utilizzabile perché è contrassegnato come specializzate.</span><span class="sxs-lookup"><span data-stu-id="6dd97-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="6dd97-123">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="6dd97-123">**Resolution**</span></span>

<span data-ttu-id="6dd97-124">tooresolve entrambi questi errori, eliminare l'immagine corrente hello dal portale hello e [nuovamente acquisita da hello dischi rigidi virtuali correnti](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con hello stessa impostazione di quello per hello del sistema operativo (generalizzata o specializzata).</span><span class="sxs-lookup"><span data-stu-id="6dd97-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="6dd97-125">Problema: Immagine personalizzata/della raccolta/del marketplace; errore di allocazione</span><span class="sxs-lookup"><span data-stu-id="6dd97-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="6dd97-126">Questo errore si verifica nelle situazioni quando hello nuova macchina virtuale richiesta cluster tooa bloccati che non è in grado di supportare dimensioni della macchina virtuale hello richieste, o non dispone di una richiesta di hello tooaccommodate di spazio libero.</span><span class="sxs-lookup"><span data-stu-id="6dd97-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="6dd97-127">**Causa 1:** cluster hello non è in grado di supportare hello richiesto dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6dd97-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="6dd97-128">**Risoluzione 1:**</span><span class="sxs-lookup"><span data-stu-id="6dd97-128">**Resolution 1:**</span></span>

* <span data-ttu-id="6dd97-129">Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6dd97-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="6dd97-130">Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="6dd97-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="6dd97-131">Arrestare tutte le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="6dd97-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="6dd97-132">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="6dd97-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="6dd97-133">Dopo tutte hello arrestare le macchine virtuali, creare hello nuova macchina virtuale in hello dimensioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="6dd97-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="6dd97-134">Avviare hello prima nuova macchina virtuale e quindi selezionare hello arrestare le macchine virtuali e fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="6dd97-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="6dd97-135">**Causa 2:** cluster hello privo di liberare risorse.</span><span class="sxs-lookup"><span data-stu-id="6dd97-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="6dd97-136">**Risoluzione 2:**</span><span class="sxs-lookup"><span data-stu-id="6dd97-136">**Resolution 2:**</span></span>

* <span data-ttu-id="6dd97-137">Ripetere la richiesta hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6dd97-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="6dd97-138">Se hello nuova macchina virtuale è possibile essere incluso un diverso set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="6dd97-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="6dd97-139">Creare una nuova macchina virtuale in un set di disponibilità diverso (in hello stessa regione).</span><span class="sxs-lookup"><span data-stu-id="6dd97-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="6dd97-140">Aggiungere hello nuova VM toohello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6dd97-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd97-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6dd97-141">Next steps</span></span>
<span data-ttu-id="6dd97-142">Se si incontrano problemi quando si avvia una VM Windows arrestata o si ridimensiona una VM Windows esistente in Azure, vedere l'articolo su come [risolvere i problemi della distribuzione di Resource Manager con il riavvio o il ridimensionamento di una macchina virtuale Windows esistente in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6dd97-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

