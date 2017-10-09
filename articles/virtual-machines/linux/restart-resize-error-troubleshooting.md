---
title: aaaVM il riavvio o il ridimensionamento dei problemi in Azure | Documenti Microsoft
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
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="3d08f-103">Risolvere i problemi di distribuzione con il riavvio o il ridimensionamento di una macchina virtuale Linux esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="3d08f-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="3d08f-104">Quando si tenta di una macchina virtuale di Azure (VM) arrestata toostart, o si ridimensiona una macchina virtuale di Azure esistente, errore comune di hello che si verificano è un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="3d08f-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="3d08f-105">Questo errore si verifica quando cluster hello o area geografica non è risorse disponibili oppure non è supporto hello richiesto di dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d08f-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="3d08f-106">Raccogliere i log di attività</span><span class="sxs-lookup"><span data-stu-id="3d08f-106">Collect activity logs</span></span>
<span data-ttu-id="3d08f-107">toostart risoluzione dei problemi, attività di raccolta hello registra errore hello tooidentify associata hello problema.</span><span class="sxs-lookup"><span data-stu-id="3d08f-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="3d08f-108">Hello seguenti collegamenti contenga informazioni dettagliate sul processo hello:</span><span class="sxs-lookup"><span data-stu-id="3d08f-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="3d08f-109">Visualizzare le operazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3d08f-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="3d08f-110">Visualizzare toomanage log attività Azure le risorse</span><span class="sxs-lookup"><span data-stu-id="3d08f-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="3d08f-111">Problema: Errore durante l'avvio di una VM arrestata</span><span class="sxs-lookup"><span data-stu-id="3d08f-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="3d08f-112">Si tenta di toostart una macchina virtuale arrestata ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="3d08f-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="3d08f-113">Causa</span><span class="sxs-lookup"><span data-stu-id="3d08f-113">Cause</span></span>
<span data-ttu-id="3d08f-114">richiesta di Hello hello toostart arrestato VM ha toobe tentata al cluster originale hello che ospita il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3d08f-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="3d08f-115">Cluster hello è richiesta di spazio libero disponibile toofulfill hello.</span><span class="sxs-lookup"><span data-stu-id="3d08f-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="3d08f-116">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="3d08f-116">Resolution</span></span>
* <span data-ttu-id="3d08f-117">Arrestare hello tutte le macchine virtuali in disponibilità hello set e quindi riavviare ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d08f-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="3d08f-118">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="3d08f-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="3d08f-119">Dopo che tutti hello arrestare le macchine virtuali, selezionare hello arrestare le macchine virtuali e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="3d08f-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="3d08f-120">Ripetere la richiesta di riavvio hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3d08f-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="3d08f-121">Problema: Errore durante il ridimensionamento di una VM esistente</span><span class="sxs-lookup"><span data-stu-id="3d08f-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="3d08f-122">Si tenta di tooresize una macchina virtuale esistente ma si otterrà un errore di allocazione.</span><span class="sxs-lookup"><span data-stu-id="3d08f-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="3d08f-123">Causa</span><span class="sxs-lookup"><span data-stu-id="3d08f-123">Cause</span></span>
<span data-ttu-id="3d08f-124">richiesta di Hello tooresize hello VM è toobe tentata al cluster originale hello servizio cloud hello host.</span><span class="sxs-lookup"><span data-stu-id="3d08f-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="3d08f-125">Tuttavia, non supporta cluster hello hello richiesto dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d08f-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="3d08f-126">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="3d08f-126">Resolution</span></span>
* <span data-ttu-id="3d08f-127">Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d08f-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="3d08f-128">Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="3d08f-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="3d08f-129">Arrestare tutte le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="3d08f-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="3d08f-130">Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="3d08f-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="3d08f-131">Dopo che tutti hello arrestare le macchine virtuali, ridimensionare hello desiderato VM tooa maggiori dimensioni.</span><span class="sxs-lookup"><span data-stu-id="3d08f-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="3d08f-132">Seleziona hello ridimensionato macchina virtuale e fare clic su **avviare**, e quindi avviare ogni di hello arrestato macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3d08f-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d08f-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d08f-133">Next steps</span></span>
<span data-ttu-id="3d08f-134">Se si verificano problemi durante la creazione di una nuova VM Linux in Azure, vedere [Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Linux in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d08f-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

