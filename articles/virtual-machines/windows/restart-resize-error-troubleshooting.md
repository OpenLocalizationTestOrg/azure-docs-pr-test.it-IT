---
title: aaaVM il riavvio o il ridimensionamento dei problemi in Azure | Documenti Microsoft
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
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="45d38-103">Risolvere i problemi di distribuzione con il riavvio o il ridimensionamento di una VM Windows esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="45d38-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="45d38-104">Quando si tenta di una macchina virtuale di Azure (VM) arrestata toostart, o si ridimensiona una macchina virtuale di Azure esistente, errore comune di hello che si verificano è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="45d38-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="45d38-105">Questo errore si verifica quando cluster hello o area geografica non è risorse disponibili oppure non è supporto hello richiesto di dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45d38-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="45d38-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="45d38-106">Collect activity logs</span></span>
<span data-ttu-id="45d38-107">toostart risoluzione dei problemi, attività di raccolta hello registra errore hello tooidentify associata hello problema.</span><span class="sxs-lookup"><span data-stu-id="45d38-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="45d38-108">Hello seguenti collegamenti contenga informazioni dettagliate sul processo hello:</span><span class="sxs-lookup"><span data-stu-id="45d38-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="45d38-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="45d38-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="45d38-110">Visualizzare toomanage log attività Azure le risorse</span><span class="sxs-lookup"><span data-stu-id="45d38-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="45d38-111">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="45d38-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="45d38-112">Si tenta di toostart una macchina virtuale arrestata ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="45d38-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="45d38-113">Causa</span><span class="sxs-lookup"><span data-stu-id="45d38-113">Cause</span></span>
<span data-ttu-id="45d38-114">richiesta di Hello hello toostart arrestato VM ha toobe tentata al cluster originale hello che ospita il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="45d38-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="45d38-115">Cluster hello è richiesta di spazio libero disponibile toofulfill hello.</span><span class="sxs-lookup"><span data-stu-id="45d38-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="45d38-116">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="45d38-116">Resolution</span></span>
* <span data-ttu-id="45d38-117">Arrestare hello tutte le macchine virtuali in disponibilità hello set e quindi riavviare ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45d38-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="45d38-118">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="45d38-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="45d38-119">Dopo che tutti hello arrestare le macchine virtuali, selezionare hello arrestare le macchine virtuali e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="45d38-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="45d38-120">Ripetere la richiesta di riavvio hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="45d38-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="45d38-121">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="45d38-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="45d38-122">Si tenta di tooresize una macchina virtuale esistente ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="45d38-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="45d38-123">Causa</span><span class="sxs-lookup"><span data-stu-id="45d38-123">Cause</span></span>
<span data-ttu-id="45d38-124">richiesta di Hello tooresize hello VM è toobe tentata al cluster originale hello servizio cloud hello host.</span><span class="sxs-lookup"><span data-stu-id="45d38-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="45d38-125">Tuttavia, non supporta cluster hello hello richiesto dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45d38-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="45d38-126">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="45d38-126">Resolution</span></span>
* <span data-ttu-id="45d38-127">Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45d38-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="45d38-128">Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="45d38-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="45d38-129">Arrestare tutte le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="45d38-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="45d38-130">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="45d38-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="45d38-131">Dopo che tutti hello arrestare le macchine virtuali, ridimensionare hello desiderato VM tooa maggiori dimensioni.</span><span class="sxs-lookup"><span data-stu-id="45d38-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="45d38-132">Seleziona hello ridimensionato macchina virtuale e fare clic su **avviare**, e quindi avviare ogni di hello arrestato macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="45d38-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45d38-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45d38-133">Next steps</span></span>
<span data-ttu-id="45d38-134">Se si verificano problemi durante la creazione di una nuova VM Windows in Azure, vedere [Risolvere i problemi della distribuzione Resource Manager con la creazione di una nuova macchina virtuale Windows in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45d38-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

