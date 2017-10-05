---
title: "Aggiornare un set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Aggiornare un set di scalabilità di macchine virtuali di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: c7093e221ff8fe69ded1cfbce4f3ddeb1a195666
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="c8a44-103">Aggiornare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c8a44-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="c8a44-104">Questo articolo descrive come eseguire un aggiornamento del sistema operativo a un set di scalabilità di macchine virtuali di Azure senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="c8a44-104">This article describes how you can roll out an OS update to an Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="c8a44-105">In questo contesto, un aggiornamento del sistema operativo riguarda la modifica della versione/SKU del sistema operativo oppure la modifica dell'URI di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c8a44-105">In this context, an OS update involves changing the version or SKU of the OS or changing the URI of a custom image.</span></span> <span data-ttu-id="c8a44-106">L'aggiornamento senza tempi di inattività implica l'aggiornamento di una macchina virtuale alla volta o in gruppi, ad esempio un dominio di errore alla volta, anziché contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c8a44-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="c8a44-107">In questo modo, è possibile mantenere in esecuzione tutte le macchine virtuali non in fase di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8a44-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="c8a44-108">Per evitare ambiguità, si distinguono quattro tipi di aggiornamento del sistema operativo che è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="c8a44-108">To avoid ambiguity, let’s distinguish four types of OS update you might want to perform:</span></span>

* <span data-ttu-id="c8a44-109">La modifica della versione o della SKU di un'immagine della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="c8a44-109">Changing the version or SKU of a platform image.</span></span> <span data-ttu-id="c8a44-110">Ad esempio la modifica della versione Ubuntu 14.04.2-LTS da 14.04.201506100 a 14.04.201507060 o la modifica della SKU Ubuntu 15.10/più recente a 16.04.0-LTS/più recente.</span><span class="sxs-lookup"><span data-stu-id="c8a44-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 to 14.04.201507060, or changing the Ubuntu 15.10/latest SKU to 16.04.0-LTS/latest.</span></span> <span data-ttu-id="c8a44-111">Questo scenario è illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c8a44-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="c8a44-112">La modifica dell'URI che punta a una nuova versione di un'immagine personalizzata creata (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="c8a44-112">Changing the URI that points to a new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="c8a44-113">Questo scenario è illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c8a44-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="c8a44-114">Modifica del riferimento all'immagine di un set di scalabilità creato con i dischi gestiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a44-114">Changing the image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="c8a44-115">L'applicazione di patch del sistema operativo da una macchina virtuale (esempi di questo tipo includono l'installazione di una patch di sicurezza e l'esecuzione di Windows Update).</span><span class="sxs-lookup"><span data-stu-id="c8a44-115">Patching the OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="c8a44-116">Questo scenario è supportato ma non è trattato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c8a44-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="c8a44-117">I set di scalabilità delle macchine virtuali che vengono distribuiti come parte di un cluster di [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) non sono trattati qui.</span><span class="sxs-lookup"><span data-stu-id="c8a44-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="c8a44-118">Per altre informazioni sulle patch di Service Fabric vedere [Applicare patch al sistema operativo Windows nel cluster di Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).</span><span class="sxs-lookup"><span data-stu-id="c8a44-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="c8a44-119">La sequenza di base per la modifica della versione/SKU del sistema operativo di un'immagine della piattaforma o dell'URI di un'immagine personalizzata è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c8a44-119">The basic sequence for changing the OS version/SKU of a platform image or the URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="c8a44-120">Ottenere il modello del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c8a44-120">Get the virtual machine scale set model.</span></span>
2. <span data-ttu-id="c8a44-121">Modificare la versione, la SKU, il riferimento all'immagine o il valore dell'URI del modello.</span><span class="sxs-lookup"><span data-stu-id="c8a44-121">Change the version, SKU, image reference, or URI value in the model.</span></span>
3. <span data-ttu-id="c8a44-122">Aggiornare il modello.</span><span class="sxs-lookup"><span data-stu-id="c8a44-122">Update the model.</span></span>
4. <span data-ttu-id="c8a44-123">Eseguire una chiamata *manualUpgrade* sulle macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c8a44-123">Do a *manualUpgrade* call on the virtual machines in the scale set.</span></span> <span data-ttu-id="c8a44-124">Questo passaggio è applicabile solo se la proprietà *upgradePolicy* è impostata su **Manuale** nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c8a44-124">This step is only relevant if *upgradePolicy* is set to **Manual** in your scale set.</span></span> <span data-ttu-id="c8a44-125">Se è impostata su **Automatico**, tutte le macchine virtuali vengono aggiornate contemporaneamente, con conseguente tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="c8a44-125">If it is set to **Automatic**, all the virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="c8a44-126">Tenendo conto di queste informazioni, si noti come è possibile aggiornare la versione di un set di scalabilità in PowerShell e tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="c8a44-126">With this information in mind, let’s see how you could update the version of a scale set in PowerShell, and by using the REST API.</span></span> <span data-ttu-id="c8a44-127">Questi esempi riguardano il caso di un'immagine di piattaforma, ma le informazioni fornite in questo articolo saranno sufficienti a adattare il processo per un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c8a44-127">These examples cover the case of a platform image, but this article provides enough information for you to adapt this process to a custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="c8a44-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8a44-128">PowerShell</span></span>
<span data-ttu-id="c8a44-129">Questo esempio aggiorna un set di scalabilità di una macchina virtuale Windows creando una nuova versione 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="c8a44-129">This example updates a Windows virtual machine scale set (creating to the new version 4.0.20160229.</span></span> <span data-ttu-id="c8a44-130">Dopo l'aggiornamento del modello viene eseguito un aggiornamento di un'istanza di macchina virtuale alla volta.</span><span class="sxs-lookup"><span data-stu-id="c8a44-130">After updating the model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get the VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update the virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="c8a44-131">Nel caso di un aggiornamento dell'URI per un'immagine personalizzata anziché della modifica di una versione di immagine della piattaforma, sostituire la riga "set the new version" con un comando che aggiornerà l'URI dell'immagine di origine.</span><span class="sxs-lookup"><span data-stu-id="c8a44-131">If you are updating the URI for a custom image instead of changing a platform image version, replace the “set the new version” line with a command that will update the source image URI.</span></span> <span data-ttu-id="c8a44-132">Ad esempio, se il set di scalabilità è stato creato senza usare i dischi gestiti di Azure, l'aggiornamento sarebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c8a44-132">For example, if the scale set was created without using Azure Managed Disks, the update would look like this:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="c8a44-133">Se un set di scalabilità basato sull'immagine è stato creato usando i dischi gestiti di Azure, il riferimento all'immagine verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8a44-133">If a custom image based scale set was created using Azure Managed Disks, then the image reference would be updated.</span></span> <span data-ttu-id="c8a44-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8a44-134">For example:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="the-rest-api"></a><span data-ttu-id="c8a44-135">API REST</span><span class="sxs-lookup"><span data-stu-id="c8a44-135">The REST API</span></span>
<span data-ttu-id="c8a44-136">Di seguito sono riportati due esempi di Python che usano l'API REST di Azure per implementare un aggiornamento di versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c8a44-136">Here are a couple of Python examples that use the Azure REST API to roll out an OS version update.</span></span> <span data-ttu-id="c8a44-137">Entrambi usano la libreria [azurerm](https://pypi.python.org/pypi/azurerm) semplificata della funzione wrapper dell'API REST di Azure per eseguire un'operazione GET sul modello del set di scalabilità, seguiti da un'operazione PUT con un modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8a44-137">Both use the lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions to do a GET on the scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="c8a44-138">Gli esempi esaminano le viste delle istanze della macchina virtuale per l'individuazione delle macchine virtuali tramite il dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8a44-138">They also look at virtual machine instances views to identify the virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="c8a44-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="c8a44-139">Vmssupgrade</span></span>
 <span data-ttu-id="c8a44-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) è uno script Python utile per implementare un aggiornamento del sistema operativo per un set di scalabilità di macchine virtuali in esecuzione, un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="c8a44-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used to roll out an OS upgrade to a running virtual machine scale set one update domain at a time.</span></span>

![Script Vmssupgrade per la scelta delle macchine virtuali o di un dominio di aggiornamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="c8a44-142">Questo script consente di scegliere le macchine virtuali specifiche per aggiornare o specificare un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8a44-142">This script lets you choose specific virtual machines to update or specify an update domain.</span></span> <span data-ttu-id="c8a44-143">Supporta la modifica di una versione dell'immagine della piattaforma o la modifica dell'URI di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c8a44-143">It supports changing a platform image version or changing the URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="c8a44-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="c8a44-144">Vmsseditor</span></span>
<span data-ttu-id="c8a44-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) è un editor generico per i set di scalabilità di macchine virtuali che mostra lo stato della macchina virtuale come heatmap in cui una riga rappresenta un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8a44-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="c8a44-146">Tra le altre cose, è possibile aggiornare il modello per un set di scalabilità con una nuova versione, SKU o URI dell'immagine personalizzata e quindi selezionare i domini di errore da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="c8a44-146">Among other things, you can update the model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains to upgrade.</span></span> <span data-ttu-id="c8a44-147">A questo scopo, tutte le macchine virtuali in questo dominio di aggiornamento vengono aggiornate al nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="c8a44-147">When you do so, all the virtual machines in that update domain are upgraded to the new model.</span></span> <span data-ttu-id="c8a44-148">In alternativa, è possibile eseguire un aggiornamento in sequenza in base alla dimensione di batch scelta.</span><span class="sxs-lookup"><span data-stu-id="c8a44-148">Alternatively, you can do a rolling upgrade based on the batch size of your choice.</span></span>  

<span data-ttu-id="c8a44-149">La schermata seguente illustra un modello di un set di scalabilità per Ubuntu 14.04-2LTS versione 14.04.201507060.</span><span class="sxs-lookup"><span data-stu-id="c8a44-149">The following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="c8a44-150">Da quando è stata acquisita questa schermata, sono state aggiunte a questo strumento molte opzioni.</span><span class="sxs-lookup"><span data-stu-id="c8a44-150">Many more options have been added to this tool since this screenshot was taken.</span></span>

![Modello Vmsseditor di un set di scalabilità per Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="c8a44-152">Dopo aver selezionato **Aggiorna** e **Dettagli**, le macchine virtuali nel dominio di aggiornamento 0 avviano l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8a44-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start to update.</span></span>

![Vmsseditor che illustra un aggiornamento in corso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

