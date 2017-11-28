---
title: "Imposta aaaCreate la disponibilità di una macchina virtuale in Azure | Documenti Microsoft"
description: "Informazioni su come imposta toocreate una disponibilità gestito o non gestita disponibilità impostato per le macchine virtuali tramite Azure PowerShell o hello portale nel modello di distribuzione di gestione risorse di hello."
keywords: "set di disponibilità"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="f9820-104">Aumentare la disponibilità per una macchina virtuale tramite la creazione di un set di disponibilità di Azure</span><span class="sxs-lookup"><span data-stu-id="f9820-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="f9820-105">Set di disponibilità di forniscono all'applicazione tooyour di ridondanza.</span><span class="sxs-lookup"><span data-stu-id="f9820-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="f9820-106">È consigliabile raggruppare due o più macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="f9820-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="f9820-107">Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sarà disponibile e soddisfa hello pari al 99,95% SLA di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9820-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="f9820-108">Per ulteriori informazioni, vedere hello [contratto di servizio per le macchine virtuali](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="f9820-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9820-109">Macchine virtuali devono essere create in hello stesso gruppo di risorse come set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="f9820-110">Se si desidera la parte toobe VM di un set di disponibilità, è necessario che la disponibilità di hello toocreate impostare prima o durante la sta creando la prima macchina virtuale nel set di hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="f9820-111">Se la macchina virtuale utilizza dischi gestiti, è necessario creare set di disponibilità hello come un set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="f9820-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="f9820-112">Per ulteriori informazioni sulla creazione e utilizzo di set di disponibilità, vedere [gestione hello disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9820-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="f9820-113">Utilizzare toocreate portale hello un set prima di creare le macchine virtuali di disponibilità</span><span class="sxs-lookup"><span data-stu-id="f9820-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="f9820-114">Nel menu hub hello, fare clic su **Sfoglia** e selezionare **set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="f9820-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="f9820-115">In hello **disponibilità imposta pannello**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f9820-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Schermata che mostra hello pulsante Aggiungi per creare un nuovo set di disponibilità.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="f9820-117">In hello **creare set di disponibilità** pannello, le informazioni di hello completo per il set.</span><span class="sxs-lookup"><span data-stu-id="f9820-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Schermata che mostra hello informazioni sono necessarie tooenter toocreate hello disponibilità impostato.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="f9820-119">**Nome** -nome hello deve essere costituiti da numeri, lettere, punti, caratteri di sottolineatura e trattini, caratteri di 1-80.</span><span class="sxs-lookup"><span data-stu-id="f9820-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="f9820-120">Hello primo carattere deve essere una lettera o un numero.</span><span class="sxs-lookup"><span data-stu-id="f9820-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="f9820-121">ultimo carattere Hello deve essere una lettera, numero o un carattere di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="f9820-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="f9820-122">**Domini di errore** -domini di errore definiscono gruppo hello delle macchine virtuali che condividono un commutatore power di origine e di rete comune.</span><span class="sxs-lookup"><span data-stu-id="f9820-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="f9820-123">Per impostazione predefinita, le macchine virtuali hello sono separate tra i domini di errore toothree e possono essere modificate toobetween 1 e 3.</span><span class="sxs-lookup"><span data-stu-id="f9820-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="f9820-124">**Domini di aggiornamento** : cinque domini di aggiornamento vengono assegnati per impostazione predefinita e può essere impostata toobetween 1 e 20.</span><span class="sxs-lookup"><span data-stu-id="f9820-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="f9820-125">Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f9820-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="f9820-126">Ad esempio, se si specifica update cinque domini, quando sono configurate più di cinque macchine virtuali all'interno di un singolo Set di disponibilità, macchina virtuale sesto hello saranno inseriti hello stesso dominio di aggiornamento come macchina virtuale prima di hello, hello settimo hello stesso UD come hello seconda macchina virtuale e così via.</span><span class="sxs-lookup"><span data-stu-id="f9820-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="f9820-127">ordine di Hello di riavvii hello potrebbe non essere sequenziale, ma verrà riavviato in una fase di aggiornamento di un solo dominio.</span><span class="sxs-lookup"><span data-stu-id="f9820-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="f9820-128">**Sottoscrizione** -selezionare hello toouse sottoscrizione se si dispone di più di uno.</span><span class="sxs-lookup"><span data-stu-id="f9820-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="f9820-129">**Gruppo di risorse** -selezionare un gruppo di risorse esistente facendo clic sulla freccia di hello e selezionando un gruppo di risorse di hello elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="f9820-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="f9820-130">È inoltre possibile creare un nuovo gruppo di risorse digitando un nome.</span><span class="sxs-lookup"><span data-stu-id="f9820-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="f9820-131">Hello nome può contenere nessuno dei hello seguenti caratteri: lettere, numeri, punti, trattini, caratteri di sottolineatura e apertura o la parentesi di chiusura.</span><span class="sxs-lookup"><span data-stu-id="f9820-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="f9820-132">nome Hello non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="f9820-132">hello name cannot end in a period.</span></span> <span data-ttu-id="f9820-133">Tutti i hello macchine virtuali nel gruppo di disponibilità hello necessario toobe creato in hello stesso gruppo di risorse come set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="f9820-134">**Percorso** -selezionare un percorso dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="f9820-135">**Gestito** : selezionare questa opzione *Sì* toocreate una disponibilità gestito imposta toouse con macchine virtuali che usano dischi gestiti per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f9820-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="f9820-136">Selezionare **n** se le macchine virtuali presenti nel set di hello hello Usa i dischi non gestiti in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f9820-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="f9820-137">Una volta immesse le informazioni di hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f9820-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="f9820-138">Utilizzare una macchina virtuale e una disponibilità impostazione hello stesso la toocreate portale hello ora</span><span class="sxs-lookup"><span data-stu-id="f9820-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="f9820-139">Se si sta creando una nuova macchina virtuale tramite il portale di hello, è inoltre possibile creare un nuovo set di disponibilità per hello VM durante la creazione di hello prima macchina virtuale nel set di hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="f9820-140">Se si sceglie di dischi gestiti toouse per la macchina virtuale, verrà creato un set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="f9820-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Screenshot che illustra il processo di hello per la creazione di un nuovo set durante la creazione di VM hello di disponibilità.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="f9820-142">Aggiungere una nuova macchina virtuale tooan esistente set di disponibilità nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="f9820-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="f9820-143">Per ogni VM aggiuntive che crei che deve appartenere nel set di hello, assicurarsi che venga creato in hello stesso **gruppo di risorse** e quindi selezionare hello set nel passaggio 3 di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="f9820-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Screenshot che illustra come impostare toouse di tooselect un gruppo di disponibilità per la macchina virtuale.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="f9820-145">Utilizzare PowerShell toocreate una disponibilità impostato</span><span class="sxs-lookup"><span data-stu-id="f9820-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="f9820-146">Questo esempio viene creato un set denominato di disponibilità **myAvailabilitySet** in hello **myResourceGroup** gruppo di risorse in hello **Stati Uniti occidentali** percorso.</span><span class="sxs-lookup"><span data-stu-id="f9820-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="f9820-147">Questa operazione deve toobe eseguita prima di creare hello prima macchina virtuale che verrà aggiunto il set di hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="f9820-148">Prima di iniziare, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f9820-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="f9820-149">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f9820-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="f9820-150">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9820-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="f9820-151">Se si usano dischi gestiti per le macchine virtuali, digitare:</span><span class="sxs-lookup"><span data-stu-id="f9820-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="f9820-152">Se si usa il proprio account di archiviazione per le macchine virtuali, digitare:</span><span class="sxs-lookup"><span data-stu-id="f9820-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="f9820-153">Per ulteriori informazioni, vedere [New AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="f9820-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f9820-154">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f9820-154">Troubleshooting</span></span>
* <span data-ttu-id="f9820-155">Quando si crea una macchina virtuale, se il set di disponibilità hello desiderato non è nell'elenco a discesa hello nel portale di hello si potrebbe avere creati in un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="f9820-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="f9820-156">Se non si conosce il gruppo di risorse hello per la disponibilità del set di fare clic su Sfoglia e passare menu hub toohello > toosee imposta un elenco della disponibilità e i gruppi di risorse che appartengono a gruppi di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="f9820-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9820-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9820-157">Next steps</span></span>
<span data-ttu-id="f9820-158">Aggiungere ulteriore spazio di archiviazione tooyour VM aggiungendo un ulteriore [disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9820-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

