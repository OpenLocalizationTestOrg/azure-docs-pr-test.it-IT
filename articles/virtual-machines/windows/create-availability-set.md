---
title: "Creare un set di disponibilità per una VM in Azure | Documentazione Microsoft"
description: "Informazioni su come creare un set di disponibilità gestito o non gestito per le macchine virtuali tramite Azure PowerShell o il portale nel modello di distribuzione di Resource Manager."
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="4de86-104">Aumentare la disponibilità per una macchina virtuale tramite la creazione di un set di disponibilità di Azure</span><span class="sxs-lookup"><span data-stu-id="4de86-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="4de86-105">I set di disponibilità forniscono ridondanza all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4de86-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="4de86-106">È consigliabile raggruppare due o più macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4de86-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="4de86-107">Questa configurazione assicura infatti che, nel corso di un evento di manutenzione pianificata o non pianificata, almeno una delle macchine virtuali sia sempre disponibile e soddisfi per almeno il 99,95% i requisiti del contratto di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="4de86-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="4de86-108">Per altre informazioni, vedere [Contratto di Servizio per Macchine virtuali](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="4de86-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4de86-109">La macchina virtuale deve essere creata nello stesso gruppo di risorse del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4de86-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="4de86-110">Se si desidera includere la VM in un set di disponibilità, è necessario creare quest'ultimo prima o durante la creazione della prima macchina virtuale nel set.</span><span class="sxs-lookup"><span data-stu-id="4de86-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="4de86-111">Se la macchina virtuale usa Managed Disks, è necessario creare il set di disponibilità come set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="4de86-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="4de86-112">Per altre informazioni sulla creazione e sull'uso dei set di disponibilità, vedere l'articolo relativo alla [gestione della disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4de86-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="4de86-113">Utilizzare il portale per creare un set di disponibilità prima di creare le VM</span><span class="sxs-lookup"><span data-stu-id="4de86-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="4de86-114">Nel menu dell'hub, fare clic su **Sfoglia** e selezionare **Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4de86-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="4de86-115">Nel pannello **Set di disponibilità** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4de86-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Schermata che mostra il pulsante Aggiungi per creare un nuovo set di disponibilità.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="4de86-117">Nel pannello **Crea set di disponibilità** compilare le informazioni sul set.</span><span class="sxs-lookup"><span data-stu-id="4de86-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Schermata che mostra le informazioni da immettere per creare il set di disponibilità.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="4de86-119">**Nome** : il nome deve contenere da 1 a 80 caratteri, tra numeri, lettere, punti, caratteri di sottolineatura e trattini.</span><span class="sxs-lookup"><span data-stu-id="4de86-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="4de86-120">Il primo carattere deve essere una lettera o un numero.</span><span class="sxs-lookup"><span data-stu-id="4de86-120">The first character must be a letter or number.</span></span> <span data-ttu-id="4de86-121">L'ultimo carattere deve essere una lettera o un numero o un carattere di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="4de86-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="4de86-122">**Domini di errore** : i domini di errore definiscono il gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="4de86-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="4de86-123">Per impostazione predefinita, le VM sono distribuite in un massimo di tre domini di errore; per la distribuzione possono essere usati da 1 a 3 domini.</span><span class="sxs-lookup"><span data-stu-id="4de86-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="4de86-124">**Domini di aggiornamento**: per impostazione predefinita vengono assegnati cinque domini di aggiornamento, ma è possibile impostarne da 1 a 20.</span><span class="sxs-lookup"><span data-stu-id="4de86-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="4de86-125">I domini di aggiornamento indicano gruppi di macchine virtuali e l'hardware fisico sottostante che possono essere riavviati nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="4de86-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="4de86-126">Ad esempio, se si specificano cinque domini di aggiornamento, quando in un set di disponibilità vengono configurate più di cinque macchine virtuali, la sesta macchina viene inserita nello stesso dominio di aggiornamento della prima, la settima nel dominio di aggiornamento della seconda e così via.</span><span class="sxs-lookup"><span data-stu-id="4de86-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="4de86-127">L'ordine delle operazioni di riavvio potrebbe non essere sequenziale, ma verrà riavviato un solo dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="4de86-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="4de86-128">**Sottoscrizione** : se sono disponibili più sottoscrizioni, selezionare quella da usare.</span><span class="sxs-lookup"><span data-stu-id="4de86-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="4de86-129">**Gruppo di risorse**: per selezionare un gruppo di risorse esistente, fare clic sulla freccia verso il basso e scegliere un gruppo di risorse dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="4de86-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="4de86-130">È inoltre possibile creare un nuovo gruppo di risorse digitando un nome.</span><span class="sxs-lookup"><span data-stu-id="4de86-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="4de86-131">Il nome può contenere lettere, numeri, punti, trattini, caratteri di sottolineatura e parentesi aperte o chiuse,</span><span class="sxs-lookup"><span data-stu-id="4de86-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="4de86-132">mentre non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="4de86-132">The name cannot end in a period.</span></span> <span data-ttu-id="4de86-133">Tutte le VM nel gruppo di disponibilità devono essere create nello stesso gruppo di risorse del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4de86-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="4de86-134">**Percorso** : selezionare un percorso nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="4de86-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="4de86-135">**Gestito**: selezionare *Sì* per creare un set di disponibilità gestito da usare con le macchine virtuali che usano Managed Disks per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4de86-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="4de86-136">Selezionare **No** se le macchine virtuali presenti nel set usano dischi non gestiti in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4de86-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="4de86-137">Dopo aver immesso le informazioni, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4de86-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="4de86-138">Usare il portale per creare una macchina virtuale e un set di disponibilità contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="4de86-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="4de86-139">Quando si crea una nuova VM tramite il portale, è anche possibile creare un nuovo set di disponibilità durante la creazione della prima VM del set.</span><span class="sxs-lookup"><span data-stu-id="4de86-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="4de86-140">Se si sceglie di usare Managed Disks per la macchina virtuale, verrà creato un set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="4de86-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Schermata che illustra la procedura di creazione di un nuovo set di disponibilità in fase di creazione della VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="4de86-142">Aggiungere una nuova VM a un set di disponibilità esistente nel portale</span><span class="sxs-lookup"><span data-stu-id="4de86-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="4de86-143">Per ogni nuova VM da aggiungere al set, assicurarsi di creare la VM nello stesso **gruppo di risorse** e di selezionare il set di disponibilità esistente al Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="4de86-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Schermata che illustra come selezionare un set di disponibilità da utilizzare per la VM.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="4de86-145">Usare PowerShell per creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="4de86-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="4de86-146">In questo esempio viene creato un set di disponibilità denominato **myAvailabilitySet** nel gruppo di risorse **myResourceGroup** nella posizione **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="4de86-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="4de86-147">Questa operazione deve essere eseguita prima di creare la prima VM da inserire nel set.</span><span class="sxs-lookup"><span data-stu-id="4de86-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="4de86-148">Prima di iniziare, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="4de86-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="4de86-149">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="4de86-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="4de86-150">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4de86-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="4de86-151">Se si usano dischi gestiti per le macchine virtuali, digitare:</span><span class="sxs-lookup"><span data-stu-id="4de86-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="4de86-152">Se si usa il proprio account di archiviazione per le macchine virtuali, digitare:</span><span class="sxs-lookup"><span data-stu-id="4de86-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="4de86-153">Per ulteriori informazioni, vedere [New AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="4de86-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4de86-154">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4de86-154">Troubleshooting</span></span>
* <span data-ttu-id="4de86-155">Quando si crea una VM, se il set di disponibilità desiderato non si trova nell'elenco a discesa nel portale, potrebbe essere stato creato in un altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4de86-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="4de86-156">Se non si conosce il gruppo di risorse del set di disponibilità, accedere al menu dell'hub e fare clic su Sfoglia > Gruppi di disponibilità per visualizzare un elenco dei set di disponibilità e dei gruppi di risorse appartenenti a ciascuno.</span><span class="sxs-lookup"><span data-stu-id="4de86-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4de86-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4de86-157">Next steps</span></span>
<span data-ttu-id="4de86-158">Aumentare lo spazio di archiviazione della VM aggiungendo un ulteriore [disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4de86-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

