---
title: imposta una scala di macchina virtuale di Azure aaaUpgrade | Documenti Microsoft
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
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="3e0e6-103">Aggiornare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3e0e6-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="3e0e6-104">Questo articolo descrive come è possibile distribuire un sistema operativo aggiornamento tooan macchina virtuale di Azure set di scalabilità senza tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="3e0e6-105">In questo contesto, un aggiornamento del sistema operativo comporta la modifica di versione di hello o SKU di hello del sistema operativo o hello URI di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="3e0e6-106">L'aggiornamento senza tempi di inattività implica l'aggiornamento di una macchina virtuale alla volta o in gruppi, ad esempio un dominio di errore alla volta, anziché contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="3e0e6-107">In questo modo, è possibile mantenere in esecuzione tutte le macchine virtuali non in fase di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="3e0e6-108">tooavoid ambiguità, si distingue quattro tipi di aggiornamento del sistema operativo potrebbe essere necessario tooperform:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="3e0e6-109">Modifica di versione di hello o SKU di un'immagine della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="3e0e6-110">Ad esempio la modifica Ubuntu versione 14.04.2-LTS da 14.04.201506100 too14.04.201507060 o la modifica hello Ubuntu più recente 15.10 SKU too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="3e0e6-111">Questo scenario è illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="3e0e6-112">Modifica hello URI che punta tooa nuova versione di un'immagine personalizzata è stata compilata (**proprietà** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **immagine** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="3e0e6-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="3e0e6-113">Questo scenario è illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="3e0e6-114">Modifica hello immagine riferimento di un set di scalabilità che è stato creato utilizzando i dischi gestiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="3e0e6-115">L'applicazione di patch hello del sistema operativo da una macchina virtuale (esempi di questo tipo includono l'installazione di una patch di sicurezza e l'esecuzione di Windows Update).</span><span class="sxs-lookup"><span data-stu-id="3e0e6-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="3e0e6-116">Questo scenario è supportato ma non è trattato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="3e0e6-117">I set di scalabilità delle macchine virtuali che vengono distribuiti come parte di un cluster di [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) non sono trattati qui.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="3e0e6-118">Per altre informazioni sulle patch di Service Fabric vedere [Applicare patch al sistema operativo Windows nel cluster di Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).</span><span class="sxs-lookup"><span data-stu-id="3e0e6-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="3e0e6-119">Hello base hello di sequenza per la modifica del sistema operativo, versione/SKU di un'immagine della piattaforma o URI di un'immagine personalizzata hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="3e0e6-120">Ottenere modello scala hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="3e0e6-121">Versione di hello modifica SKU, riferimento a un'immagine o valore URI nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="3e0e6-122">Aggiornare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-122">Update hello model.</span></span>
4. <span data-ttu-id="3e0e6-123">Eseguire un *manualUpgrade* chiamare su macchine virtuali hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="3e0e6-124">Questo passaggio è rilevante solo se *upgradePolicy* è troppo**manuale** nel set della scalabilità.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="3e0e6-125">Se è impostato troppo**automatico**, tutte le macchine virtuali hello vengono aggiornate contemporaneamente, con conseguente rallentamento dei tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="3e0e6-126">Con queste informazioni in considerazione, vediamo come è possibile aggiornare la versione hello di un set in PowerShell e tramite l'API REST hello di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="3e0e6-127">Questi esempi riguardano caso hello di un'immagine della piattaforma, ma in questo articolo fornisce informazioni sufficienti affinché si tooadapt immagine personalizzata di tooa questo processo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="3e0e6-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e0e6-128">PowerShell</span></span>
<span data-ttu-id="3e0e6-129">Questo esempio viene aggiornato un set di scalabilità di macchine virtuali di Windows (creazione toohello nuova versione 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="3e0e6-130">Dopo aver aggiornato il modello di hello, esegue un'istanza di macchina virtuale un aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="3e0e6-131">Se si sta aggiornando hello URI per un'immagine personalizzata anziché la modifica di una versione dell'immagine della piattaforma, sostituire "set hello nuova versione" hello riga con un comando che verrà aggiornata hello URI dell'immagine di origine.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="3e0e6-132">Ad esempio, se il set di scalabilità di hello è stato creato senza l'utilizzo di dischi gestiti di Azure, aggiornamento hello avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="3e0e6-133">Se un'immagine personalizzata in base a set di scalabilità è stata creata utilizzando i dischi gestiti di Azure, quindi riferimento all'immagine di hello verranno aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="3e0e6-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="3e0e6-135">Hello API REST</span><span class="sxs-lookup"><span data-stu-id="3e0e6-135">hello REST API</span></span>
<span data-ttu-id="3e0e6-136">Di seguito sono riportati alcuni esempi di Python che utilizzano hello tooroll di API REST di Azure di un aggiornamento di versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="3e0e6-137">Entrambi utilizzano lightweight hello [azurerm](https://pypi.python.org/pypi/azurerm) libreria di API REST di Azure wrapper funzioni toodo un'operazione GET su scala hello Imposta modello, seguito da un'operazione PUT con un modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="3e0e6-138">Sono anche esaminare le visualizzazioni di istanze di macchina virtuale macchine virtuali di hello tooidentify dal dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="3e0e6-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="3e0e6-139">Vmssupgrade</span></span>
 <span data-ttu-id="3e0e6-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) script Python usato tooroll out un tooa di aggiornamento del sistema operativo in esecuzione sulla scalabilità della macchina virtuale è impostato un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Script Vmssupgrade per la scelta delle macchine virtuali o di un dominio di aggiornamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="3e0e6-142">Questo script consente di scegliere tooupdate specifiche macchine virtuali o specificare un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="3e0e6-143">Supporta la modifica di una versione dell'immagine della piattaforma o hello URI di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="3e0e6-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="3e0e6-144">Vmsseditor</span></span>
<span data-ttu-id="3e0e6-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) è un editor generico per i set di scalabilità di macchine virtuali che mostra lo stato della macchina virtuale come heatmap in cui una riga rappresenta un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="3e0e6-146">Tra le altre cose, è possibile aggiornare il modello di hello per un set di scalabilità con una nuova versione, SKU o URI dell'immagine personalizzata e quindi selezionare tooupgrade di domini di errore.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="3e0e6-147">Quando si esegue questa operazione, tutte le macchine virtuali hello in tale dominio di aggiornamento vengono aggiornati toohello nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="3e0e6-148">In alternativa, è possibile eseguire un aggiornamento in sequenza in base alle dimensioni di batch hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="3e0e6-149">Hello schermata riportata di seguito viene illustrato un modello di un set per Ubuntu 14.04-2LTS versione 14.04.201507060 di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="3e0e6-150">Strumento toothis sono state aggiunte molte altre opzioni dopo questa schermata.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Modello Vmsseditor di un set di scalabilità per Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="3e0e6-152">Dopo aver fatto clic **aggiornamento** e quindi **Ottieni dettagli**, tooupdate l'avvio delle macchine virtuali in UD 0.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor che illustra un aggiornamento in corso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

