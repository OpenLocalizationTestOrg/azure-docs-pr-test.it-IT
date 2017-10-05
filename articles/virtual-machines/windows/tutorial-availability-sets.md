---
title: "Esercitazione sui set di disponibilità per macchine virtuali Windows in Azure | Microsoft Docs"
description: "Informazioni sui set di disponibilità per macchine virtuali Windows in Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="c8e82-103">Come usare i set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-103">How to use availability sets</span></span>

<span data-ttu-id="c8e82-104">In questa esercitazione si apprenderà come aumentare la disponibilità e l'affidabilità delle soluzioni delle proprie macchine virtuali in Azure tramite una funzionalità denominata set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c8e82-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="c8e82-105">I set di disponibilità assicurano che le macchine virtuali distribuite in Azure vengano distribuite tra più cluster hardware isolati.</span><span class="sxs-lookup"><span data-stu-id="c8e82-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="c8e82-106">Questa operazione assicura che, se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme delle macchine virtuali verrà interessato e la soluzione complessiva rimarrà disponibile e operativa dal punto di vista dei clienti che la usano.</span><span class="sxs-lookup"><span data-stu-id="c8e82-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="c8e82-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="c8e82-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8e82-108">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-108">Create an availability set</span></span>
> * <span data-ttu-id="c8e82-109">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c8e82-110">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="c8e82-110">Check available VM sizes</span></span>

<span data-ttu-id="c8e82-111">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c8e82-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c8e82-112">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c8e82-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c8e82-113">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c8e82-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="c8e82-114">Informazioni generali sui set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-114">Availability set overview</span></span>

<span data-ttu-id="c8e82-115">Un set di disponibilità è una funzionalità di raggruppamento logico che è possibile usare in Azure per garantire che le risorse delle macchine virtuali inserite dall'utente siano isolate tra loro quando vengono distribuite all'interno di un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e82-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="c8e82-116">Azure garantisce che le macchine virtuali inserite all'interno di un set di disponibilità vengano eseguite tra più server fisici, rack di calcolo, unità di archiviazione e commutatori di rete.</span><span class="sxs-lookup"><span data-stu-id="c8e82-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="c8e82-117">Ciò garantisce che in caso di errore hardware o software in Azure, verrà interessato solo un sottoinsieme delle macchine virtuali e l'applicazione complessiva si manterrà aggiornata e continuerà a essere disponibile per i clienti.</span><span class="sxs-lookup"><span data-stu-id="c8e82-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="c8e82-118">L'uso dei set di disponibilità è una funzionalità essenziale da sfruttare quando si desidera creare soluzioni di cloud affidabili.</span><span class="sxs-lookup"><span data-stu-id="c8e82-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="c8e82-119">Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database.</span><span class="sxs-lookup"><span data-stu-id="c8e82-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="c8e82-120">Con Azure è possibile definire due set di disponibilità prima di distribuire le macchine virtuali: un set di disponibilità per il livello "Web" e un set di disponibilità per il livello "database".</span><span class="sxs-lookup"><span data-stu-id="c8e82-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="c8e82-121">Quando si crea una nuova macchina virtuale, è quindi possibile specificare il set di disponibilità come parametro per il comando az vm create. Azure automaticamente garantirà che le macchine virtuali create all'interno del set di disponibilità vengano isolate su più risorse hardware fisiche.</span><span class="sxs-lookup"><span data-stu-id="c8e82-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="c8e82-122">Ciò significa che, se l'hardware fisico su cui è in esecuzione una delle macchine virtuali dei server di database o dei server Web presenta un problema, le altre istanze delle macchine virtuali dei server Web e di database rimarranno in esecuzione correttamente perché si trovano su un hardware diverso.</span><span class="sxs-lookup"><span data-stu-id="c8e82-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="c8e82-123">Usare sempre i set di disponibilità quando si vogliono distribuire soluzioni affidabili basate su macchine virtuali all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e82-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="c8e82-124">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-124">Create an availability set</span></span>

<span data-ttu-id="c8e82-125">È possibile creare un set di disponibilità con il comando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="c8e82-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="c8e82-126">In questo esempio, sia il numero di domini di aggiornamento che quello di domini di errore vengono impostati su *2* per il set di disponibilità denominato *myAvailabilitySet* nel gruppo di risorse *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="c8e82-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="c8e82-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c8e82-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="c8e82-128">Creare macchine virtuali in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="c8e82-129">Per garantire la corretta distribuzione delle macchine virtuali in tutto l'hardware, le VM devono essere create all'interno del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c8e82-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="c8e82-130">Non è possibile aggiungere una macchina virtuale esistente a un set di disponibilità dopo la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="c8e82-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="c8e82-131">L'hardware in un percorso è suddiviso in più domini di aggiornamento e domini di errore.</span><span class="sxs-lookup"><span data-stu-id="c8e82-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="c8e82-132">I **domini di aggiornamento** sono gruppi di macchine virtuali con relativo hardware fisico sottostante che è possibile riavviare nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="c8e82-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="c8e82-133">Le macchine virtuali nello stesso **dominio di errore** condividono risorse di archiviazione comuni, nonché un alimentatore e un commutatore di rete comune.</span><span class="sxs-lookup"><span data-stu-id="c8e82-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="c8e82-134">Quando si crea la configurazione di una macchina virtuale usando il comando [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), si specifica il set di disponibilità usando il parametro `-AvailabilitySetId` per specificare l'ID del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c8e82-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="c8e82-135">Creare 2 macchine virtuali con il comando [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c8e82-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify the availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="c8e82-136">La creazione e la configurazione di entrambe le macchine virtuali richiedono alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c8e82-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="c8e82-137">Al termine, si avranno 2 macchine virtuali distribuite nell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="c8e82-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="c8e82-138">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="c8e82-138">Check for available VM sizes</span></span> 

<span data-ttu-id="c8e82-139">È possibile aggiungere più macchine virtuali al set di disponibilità in un secondo momento, ma è necessario sapere quali dimensioni di macchina virtuale sono disponibili nell'hardware.</span><span class="sxs-lookup"><span data-stu-id="c8e82-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="c8e82-140">Usare il comando [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) per elencare tutte le dimensioni disponibili nel cluster hardware per il set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c8e82-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="c8e82-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8e82-141">Next steps</span></span>

<span data-ttu-id="c8e82-142">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="c8e82-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8e82-143">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-143">Create an availability set</span></span>
> * <span data-ttu-id="c8e82-144">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="c8e82-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c8e82-145">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="c8e82-145">Check available VM sizes</span></span>

<span data-ttu-id="c8e82-146">Passare all'esercitazione successiva per informazioni sui set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c8e82-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8e82-147">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c8e82-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


